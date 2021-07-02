
[Taken from this article](https://aws.amazon.com/blogs/devops/building-an-end-to-end-kubernetes-based-devsecops-software-factory-on-aws/) Read it for the complete understanding.

# Building an end-to-end Kubernetes-based DevSecOps software factory on AWS

The following diagram shows the architecture of the solution. We use AWS CloudFormation to describe the pipeline as code.

![Pipeline architecture](./containers-pipeline-architecture-blog-v2-1.png)

## The main steps are as follows:

1. When a user commits the code to CodeCommit repository, a CloudWatch event is generated, which triggers CodePipeline to orchestrate the events.
2. CodeBuild packages the build and uploads the artifacts to an S3 bucket.
3. CodeBuild scans the code with git-secrets. If there is any sensitive information in the code such as AWS access keys or secrets keys, CodeBuild fails the build.
4. CodeBuild creates the container image and perform SCA and SAST by scanning the image with Snyk or Anchore. In the provided CloudFormation template, you can pick one of these tools during the deployment. Please note, CodeBuild is fully enabled for a “bring your own tool” approach.
  - (4a) If there are any vulnerabilities, CodeBuild invokes the Lambda function. The function parses the results into AWS Security Finding Format (ASFF) and posts them to Security Hub. Security Hub helps aggregate and view all the vulnerability findings in one place as a single pane of glass. The Lambda function also uploads the scanning results to an S3 bucket.
  - (4b) If there are no vulnerabilities, CodeBuild pushes the container image to Amazon ECR and triggers another scan using built-in Amazon ECR scanning.
5. CodeBuild retrieves the scanning results.
  - (5a) If there are any vulnerabilities, CodeBuild invokes the Lambda function again and posts the findings to Security Hub. The Lambda function also uploads the scan results to an S3 bucket.
  - (5b) If there are no vulnerabilities, CodeBuild deploys the container image to an Amazon EKS staging environment.
6. After the deployment succeeds, CodeBuild triggers the DAST scanning with the OWASP ZAP tool (again, this is fully enabled for a “bring your own tool” approach).
  - (6a) If there are any vulnerabilities, CodeBuild invokes the Lambda function, which parses the results into ASFF and posts it to Security Hub. The function also uploads the scan results to an S3 bucket (similar to step 4a).
7. If there are no vulnerabilities, the approval stage is triggered, and an email is sent to the approver for action via Amazon SNS.
8. After approval, CodeBuild deploys the code to the production Amazon EKS environment.
9. During the pipeline run, CloudWatch Events captures the build state changes and sends email notifications to subscribed users through Amazon SNS.
10. CloudTrail tracks the API calls and sends notifications on critical events on the pipeline and CodeBuild projects, such as UpdatePipeline, DeletePipeline, CreateProject, and DeleteProject, for auditing purposes.
11. AWS Config tracks all the configuration changes of AWS services. The following AWS Config rules are added in this pipeline as security best practices:
  1. __CODEBUILD_PROJECT_ENVVAR_AWSCRED_CHECK__ – Checks whether the project contains environment variables AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY. The rule is NON_COMPLIANT when the project environment variables contain plaintext credentials. This rule ensures that sensitive information isn’t stored in the CodeBuild project environment variables.
  2. __CLOUD_TRAIL_LOG_FILE_VALIDATION_ENABLED__ – Checks whether CloudTrail creates a signed digest file with logs. AWS recommends that the file validation be enabled on all trails. The rule is noncompliant if the validation is not enabled. This rule ensures that pipeline resources such as the CodeBuild project aren’t altered to bypass critical vulnerability checks.



