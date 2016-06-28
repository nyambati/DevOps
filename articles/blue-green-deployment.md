# Blue Green deployment

## What is blue-green deployment

Blue-Green deployment is a technique in which you have two identical production environment. One of the environment is called green and the other one Blue. What's with the colours? How does this work? Why would I use this technique? Let's answer those questions.

Imagine you are running a live production system that receives an overwhelming  traffic each day. In your development lifecycle you deploy new features each week, this means that your production environment gets updated frequently. What happens if a deployment fails or doesn't respond as expected? You don't want to find out because it is disastrous.

To curb such a scenario you deploy to two production environments. The way this works is, let us say that we have our blue environment as live, all our traffic is being served by this server and we have a new deployment that we need to roll out.

We will deploy the new version to the Green environment and then re-route traffic to the Green environment when the deployment is done and tested to be sound. This means that Green environment becomes the new live production environment that our users are routed to. Next time we are having a new deployment we will deploy to blue which is currently idle and re-route traffic again.

## Why would I use this technique?
There are many benefits that come with using this approach when deploying to production.

* Reducing downtime -> Deployments always take time before the system goes live. If you are running a small website or app this may not be a significant challenge because of small traffic. Imagine an online store like Amazon, it receives millions of requests per hour, if it goes offline for an hour that means losing customers and making losses, that's not something you will want to happen. Blue-Green enables us to deploy to production and route traffic to the new deploy when it's live and functioning. This means your users will not experience downtime.

* Immediate rollback -> At any instance one of the environments will have the recent stable release of your software. What happens when you deploy to production and then realise that you missed something important or maybe your app is not persisting sessions? Ooops! Imagine logging to Amazon you got that awesome geeky gadget  you have been saving for all year, you purchase it and then you later check your cart and nothing! no geeky gadget. If it was me, I won't be smiling that would be world war right there. Assuming in this situation our defective environment is Blue, we can route all our traffic to Green. This will allow as to fix the bugs before redeploying again. Simple and easy.


## How do I get my app ready for Blue-Green?

There are many practices which we need to be adopted to enable one to get to a Blue-Green deployment process. These practices provide the ability to scale horizontally easily, and roll back and forth without problems.

1. Statelessness

  The application must not persist state to the server. Most applications involve storing user sessions in cookies or tokens. When you are switching from one environment to the other if one user was logged in the Blue environment will loose his/her session once there is a switch to green. This maybe shopping cart data or progress reports etc. You don't want this to happen? to Avoid this you will have to ensure that cookies, cache files, log files, etc are backed by external services like Memcached, Amazon S3, Redis or Papertail. This means that no matter which environment your production app is live your user will have the same data and user experience.

2. Infrastructure Automation

  Orchestrating production server can be a lot of work, Time taken to configure the production environment on each deployment is key. Therefore its best at all time to ensure that these processes are automated. Services like containerization e.g Docker and CI pipelines are some of the tools you should look at in this scenario.

3. Database and Migrations

  Databases can often be a challenge with this technique, particularly when you need to change the schema to support a new version of the software.  Using two production environments may rise to discrepancies. To maintain consistency between two environments it is recommended to use one production database. And what happens when I change schemas in my database? Good Question. This is where migrations come in. With migrations you can be able to manage your database schema based on new feature and software releases. You can roll back and forth without any challenges.


## What tools or services to I need?

There are may tools out there that you can use to setup this environment. The tools that you may choose will heavily depend on your infrastructure and how you application works. Here are couple articles you may look at:

1. [Introduction to Blue/Green Deployment on AWS](https://medium.com/aws-activate-startup-blog/upgrades-without-tears-part-1-introduction-to-blue-green-deployment-on-aws-e5bcf90eb60b#.9cz7o0gai)
2. [DockeBlue-Green Deployment using Containers](https://blog.tutum.co/2015/06/08/blue-green-deployment-using-containers/)
3. [Blue/Green Deploys with Kubernetes and Amazon ELB](https://www.citrix.com/blogs/2015/06/16/bluegreen-deploys-with-kubernetes-and-amazon-elb/)
4. [Blue-Green Deployment with Cloud Foundry](https://docs.cloudfoundry.org/devguide/deploy-apps/blue-green.html)
5. [Blue-Green Deployment](https://blog.anynines.com/blue-green-deployment/)
6. [The DOs and DON'Ts of Blue/Green Deployment](https://cloudnative.io/blog/2015/02/the-dos-and-donts-of-bluegreen-deployment/)
