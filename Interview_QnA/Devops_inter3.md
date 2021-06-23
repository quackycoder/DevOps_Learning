__Taken from this video:__ 

## [DevOps Interview Skills: AWS](https://youtu.be/vsLrQM6Q7jU?list=PL2qztVQdZeHMqF_rk2QDzmhA2ytFjS88b)

- A lot of Devops jobs listed online require AWS and the job skill requirements. 
So how to interview for that and some ways to get the AWS skills you need.

- AWS is just a beast. There are tons of products in AWS and so don't make the mistake of thinking that you have to know all of them.

- I've been working in AWS fora really long time and there's still AWS tools and products that i've never touched and probably never will. 

- So how do you interview for something like that and for me, I think what they're really looking for are just an understanding of like the AWS best practices or AWS better practices. 

- So we're looking for things that are like do you understand identity and access management? I am because that's really one of the key things to securing all of the AWS tools you can control access to every single product in AWS through the use of IAM and the way that you leverage that is you build out these IAM policies so that your developers or your software engineers that you support have access to the products that they need.

- But not to the ones that they don't need and that's not only like restricting access to certain things in AWS but restricting access to certain environments in AWS so that they can have access to dev and test environments but they can't have access to production.
For example IAM is also how you're going to secure different applications and different microservices so that you can ensure that you know your API service running in your staging environment can't talk to the API service talking in production and so whenever i'm interviewing people that's the kind of things that i'm looking at and digging into to see if they really understand that!
 
- That's what it's used for and some of the basics of how to implement that the next thing that i look for whenever i'm talking to a candidate about AWS is networking specifically with VPCs or virtual private clouds because you should be operating inside of VPC. 
What that does is while you're in AWS, it allows you to put this network infrastructure wall around all your services so that the public internet can't be banging on things that you don't want them banging on because that's one of the key things to understand about AWS is every hacker on the planet knows the full range of IP addresses owned by AWS and they just beat on them all day long looking to see who left a port exposed that they can use to exploit that environment.

- So putting your stuff inside of a VPC helps minimize that from happening. At the same time, there are certain things that you do have to expose if you're running a website.

- You have to expose port  to allow HTTPS traffic to your service.

- Make sure that you understand how to do that and how to implement that so that it's done for just that service and not for other things in your environment.

- As well a lot of that ties into security groups and then another part that we're going to talk about are subnets and building out subnets inside your VPC to help segregate different resources so that you don't have staging resources on the same network as production resources.

- When you're interviewing with me about an AWS specific job we're going to talk about some of the common AWS services.

- Again like i mentioned earlier, i don't expect you to know everything about every AWS service.

- There are some big players in there that you should be familiar with ec2 instances you know like how do you launch and configure an ec2 instance. 

- rds instances are another one that you're probably going to be exposed to. So i want to know that you know how to launch and configure an rds instance and provision access to it so that the right resources can access it and the not right resources can't access it.

- Serverless is getting really common or has been common for a while now. So we're going to talk about that and i want to make sure that you understand you know what serverless is, how it functions and some of the imitations that it has as well specifically around concurrency because serverless functions aren't unlimited.
You can only run a certain number of them until you request your quota to be increased and that quota is the key thing i'm looking for because that actually applies to a lot of AWS services whenever you sign up and open your account you are allowed to access a certain number of different things and i'm going to just ask some questions to make sure that you know that the quota exists.

- I don't really care if you know what the exact number is because that's a google search way but i do want to know that you understand that quotas are there and that bumping against that quota is going to shut down your service.

- The last thing that we'll talk about is ECS, the Elastic Container Service because that allows you to run containerized applications in your infrastructure without having to spin up ec2 instances.

- Now you can still do it on ec2 instances but you can also do it without ec2 instances and i really like that feature.

- We might talk about AWS billing as well because for me, that's an incredibly important yet sometimes overlooked component of Devops in AWS.

- It's really really easy to go launch a bunch of in AWS and then at the end of the month you get this bill which can shock and surprise some people and lead to some awkward conversation.

- So, if you're going to work with me i want to make sure that you understand that capacity exists and that you know how to read an AWS bill and know how to track it along the way and manage those costs and implement some of the different things that AWS provides for cost management and AWS like reserved instances.

- Now if you don't have those skills what are you going to do the easiest thing is to just launch an AWS environment on your own and i say easiest but that comes with caveat because now you're putting your credit card number in there right but i think there's a hidden benefit to that because that means you are personally on the hook for managing those AWS costs which is an important part of operating in AWS.

- To manage, you're kind of fronting your own education at that point. So please do be careful when you do that make sure that you don't do something that causes you know a huge build that puts you in financial distress.

- One of the ways you can help avoid that is to set up a billing alert on your personal AWS account so that if the dollar amount exceeds five dollars or ten dollars or a hundred dollars or whatever amount you're comfortable with that.
You get an alert from AWS so you can go in and take whatever corrective action is required before it becomes a financial burden on you and then just to get those different things like go launch an ec2 instance launch an ec2 instance via automation using something like Ansible or Cloudformation then shut it down so that the billing stops.

- Delete the volumes that were created so that you're not getting charged for those.

- Go do the same thing with rds you know and work your way through those different tools 

- Until you have a good understanding of them and again you don't have to be an expert in this.

- Just be able to have a conversation with someone like me about them and then we'll just decide from there whether it's a good fit or whether you've got some more growing to do.
