# Creating-an-AMI-gold-image-IAM-users-and-user-groups

Scenario: Level Up Bank wants to enhance its security measures and streamline their infrastructure management. The bank has 3 different teams which consist of developers, management and a help desk team. Each team requires different levels of access and permissions based on their roles and responsibilities.

Project Overview: This project has 3 tiers of difficulty. Foundational, Advanced and Complex. I will be challenging myself to complete all 3 tiers and will be breaking down each tier’s goals and steps.

# Tier 1: Foundational

The goals for this tier are:

— Create 3 IAM groups with the following permissions:

a. Developers — Should have access to view and RDP into EC2 instances

b. Management — Should only have view permissions, write, and list. They should not be able to create S3 buckets.

c. Help Desk — Should not have full access to EC2 and full access to S3.

— Create 3 Users and add one of the users to each group. Log in as each and verify the following:

a. Verify the Developers Group user is not able to launch or deploy any EC2 instances but can still view any that have been created.

b. Verify the Management group can’t view anything but S3 and even then, can’t create a bucket.

c. Verify that the Help Desk can launch EC2s and create S3 buckets but can’t use some of the other AWS services that you haven’t given access to.

— Have Help Desk deploy and launch a Windows Server 2022 EC2.

— Verify that the Developer can RDP into the Windows Server.

We now have knowledge of what the first task requires, so let’s get started!!!

The very first thing we need to do is create the 3 user groups and give them their respective user group name.

Please head over to the IAM console and click on User groups in the left hand side menu. Click Create group and give it the name Developers. We will not be adding any users just yet. Scroll down and click on Create group. Click on the User group and then the Permissions tab. Under Permissions policies, click Add permissions, Attach policies, Create policy.

![Snipe 1](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/693be0a1-77de-435f-964a-1a20e4d12a80)

In the Policy editor, click on EC2.

![Snipe 2](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/c8684c3f-9feb-430a-a8a2-b4cd3446f397)

Then in the Access level, expand Read and select “DescribeInstances”, scroll down and click Next, name the policy then Create policy.

![Snipe 3](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/b027a50c-a6c9-4b44-9661-6dde176e24e4)

We need to attach the policy to the Developers group. In the Policies section, click the circle next to the policy we just created then click on Actions, Attach. In the next screen, choose the Developers group then Attach policy. Now the policy is attached to the group.

![Snipe 4](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/d7d700ca-3b11-4512-865e-c6485fea07b4)

This time create the Management group. Click Create group then on the Management group in the IAM console. Locate the Permissions tab then click on Attach policies.

![Snipe 5](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/d3724a33-c621-4653-b1b5-d7c139f9a304)

Now click on Create policy. In the Specify permissions screen, locate Select a service and click on S3.

![Snipe 6](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/59b6988d-2b8b-48ae-9402-cca438e7776b)

Locate the Access level section and expand List Read and Write. In the List section, check off “ListAllMyBuckets”, In the Read section, check off “GetObject” and in the Write section check off “PutObject”.

![Snipe 7](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/bfbc5303-2ef0-4b1e-97ac-efd16a3dcbb1)

Granting the ability to view all buckets

![Snipe 8](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/ec9cf070-efeb-47cd-bbc7-a97ae9212134)

Granting the ability to view all objects within all buckets

![Snipe 9](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/78431f80-f490-45b8-ac71-7ea7a5490cd2)

Granting the ability to create new objects in all buckets

Scroll down and click Next. Give the Policy a name and optionally, a description.

![Snipe 10](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/bec97d7d-78a0-4a1c-8a57-12627d72a7c9)

Now click on Create policy. We need to attach it to the Management group. In the Policies section, click the circle next to the policy we just created then click on Actions, Attach. In the next screen, choose the Management group then Attach policy. Now the policy is attached to the group.

We can now create the final group which is the Help Desk group. Perform the same process until you reach the Create policy screen. In the Policy editor for EC2, we have to select the following:

```
“ec2:DescribeImages”,
“ec2:AuthorizeSecurityGroupEgress”,
“ec2:AuthorizeSecurityGroupIngress”,
“ec2:DescribeInstances”,
“ec2:DescribeVpcs”,
“ec2:CreateSecurityGroup”,
“ec2:CreateTags”,
“ec2:DescribeInstanceTypes”,
“ec2:RunInstances”,
“ec2:DescribeSubnets”,
“ec2:DescribeKeyPairs”,
“ec2:DescribeSecurityGroups
```

Scroll down and click Add more permissions, click on S3, Write then select CreateBucket and also select PutEncryptionConfiguration. Scroll down and click Create Policy. Once done, attach it to the Help Desk team.

The next step is to create 3 users and place one in each group.

(For this project, we will not be assigning MFA to any of the accounts)

Navigate to users in IAM and click on Add users. Here we will create the user for the Developers group. I will name it Dev1. Select “provide user access to the AWS Management Console”, select “I want to create an IAM user”, Custom password, (type in a password). Uncheck “User must create a new password at next sign in” (We do not need to leave this enabled for this project). go ahead and click Next.

![Snipe 11](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/ee8745ea-07d2-47af-acda-6bbc3f15fe8e)

In the next screen you will get the chance to place the user into a group. Go ahead and select Developers then Next then Create user.

![Snipe 12](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/b0070cb2-6309-47ab-aed4-bd2573be6fdb)

![Snipe 13](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/594b71a9-5dd8-4eb5-800e-47ca7cdad27d)

Now repeat the same process for the next 2 users. I will name them Manage1 and Help1.

Now we will log into the Help1 user account so that we can launch and EC2 and create an S3 bucket. This will also help us test the permissions that are tied to the other 2 groups.

Open an incognito tab and navigate to the AWS console and log in. Go into the EC2 console and click Launch instance. I will be choosing a free tier Windows server since we have to RDP.

![Snipe 14](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/b00df436-b160-44a0-a2ab-52f5c03cf4b2)

For Instance type I will leave it at t2.micro. Make sure you create a key pair for this instance. For security group, select Create security group and leave “Allow RDP traffic from” selected. Leave everything else as default and click Launch instance.

![Snipe 16](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/5397b5dc-e49c-4bb7-ade3-efd78c15ee59)

*Important* You will not be able to view Instances while logged into the Help1 account as the requirement was to only allow the Helpdesk group to Launch EC2’s. We will have to log into the Dev1 account to view the instance.

But first, we have to create the S3 bucket. Head over to the S3 console and click on Create bucket. Give the bucket a name and leave everything else as default. Now click on Create bucket.

![Snipe 17](https://github.com/Mirahkeyz/Creating-an-AMI-gold-image-IAM-users-and-user-groups/assets/134533695/3630f292-a6e3-479c-b6dc-d296b8da9f7c)


We are done testing the Helpdesk group permissions as we were able to Launch new EC2’s and create S3 buckets.

Let’s log into the Management account next.

Once logged into Manage1, navigate to the S3 console and see if the user is able to view the S3 bucket we created. in the S3 console, click on Buckets located on the left side menu.

The management group is able to view the bucket but cannot access due to Insufficient permissions.



































































