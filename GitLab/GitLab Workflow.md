GitLab Workflow

# GitLab Workflow

### Step 1- Create an Issue 
![gitlab1.png](../_resources/0f0af58df7e54340acfec5012c115feb.png)
All changes within GitLab start with an Issue.

Issues can allow you, your team, and your collaborators to share and discuss proposals before, and during, their implementation. However, they can be used for a variety of other purposes, customized to your needs and workflow.

Issues are always associated with a specific project, but if you have multiple projects in a group, you can also view all the issues collectively at the group level.

Common use cases include:

- Discussing the implementation of a new idea
- Tracking tasks and work status
- Accepting feature proposals, questions, support requests, or bug reports
- Elaborating on new code implementations

### Step 2- Create a Merge Request 

![gitlab2.png](../_resources/0f3e8193f3514ebf9dc043045c073e3e.png)
Once you have created an Issue and added your changes and/or additions, you will **Create a Merge Request** to start the CI/CD Process.

Merge requests allow you to visualize and collaborate on the proposed changes to source code that exist as commits on a given Git branch. 

You may hear a merge request referred to as a pull request.

### Step 3- Commit Your Changes

![gitlab3.png](../_resources/fc4f20e40ae84e53bcfc695b7442b9d8.png)
Once your Merge Request has been submitted, you will Commit your changes, which will initiate the CI pipeline.

### Step 4- CI Pipeline Runs

![gitlab4.png](../_resources/d0891756278041f3a5ee99f08f078fb9.png)

During this step, the CI pipeline will run and initiate code builds, run automated tests, and deploy the branch to the staging environment. 

If there are errors, conflicts, or other issues, the pipeline will fail and will provide the appropriate error message for the failure for you to research the issue. 

### Step 5- Review Apps

![gitlab5.png](../_resources/eec4a2a788734aea98af0a711c9db473.png)
Review apps provide an automatic live preview of changes made in a feature branch by spinning up a dynamic environment for your merge requests.

They allow designers and product managers to see your changes without needing to check out your branch and run your changes in a sandbox environment.

### Step 6- Peer Review & Discussion 

![gitlab6.png](../_resources/41dd70e58aa64c449b2409ca87184a3e.png)
In this step, you will have peers or stakeholders review your changes in the review app and ensure there are no conflicts or edits that need to be made before your commits are finalized.

### Step 7- Approve Changes 

![gitlab7.png](../_resources/e01c1ed001944bd0b2b485ef16d0ba5f.png)
Once the peer/stakeholder review is complete, a person with Merge rights/permissions will need to approve your changes.

### Step 8- Merge; Issue Closed

![gitlab8.png](../_resources/7e099744ee8d4fc1b5316cc0892c18dd.png)
Once your merge request is approved, the proposed changes are merged into the Master and your issue is closed.

### Step 9- CD Pipeline Runs 

![gitlab9.png](../_resources/c773b2079b33472ca160da943cd825fd.png)
The Continuous Delivery(CD) pipeline will deploy the changes to the production environment and your changes will be live in the system.

### Step 10- Monitor 
During this step, you monitor your apps to ensure the changes are having the desired effect. 

Keep in mind- with GitLab, it is easy to roll back a change if there is an issue or if anything surfaces in production that needs further adjusting. 

### Summary

![gitlab10.png](../_resources/2155e7dbf59648fd80f361f883f4f170.png)
This is the process we recommend for DevOps teams to follow while using GitLab capabilities within a concurrent development lifecycle.


