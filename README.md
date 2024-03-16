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



























