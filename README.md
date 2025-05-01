# Cloud-Security-AWS-IAM
Cloud Security with AWS IAM
# In AWS, a user is a person or a computer that can do things on the cloud, just like you right now!

Today, we’ll be using the AWS Identity and Access Management (IAM) service to control who is authenticated (signed in) and authorized (has permissions) in your AWS console.

We’ll launch an EC2 instance, then control who has access to it by creating some IAM policies and user groups. It will look something like this…

![image](https://github.com/user-attachments/assets/3a1fcaaa-f104-4b40-9cc6-d745b51b1d57)

Get ready to create (and learn from scratch):

💻 EC2 instances
📏 IAM Policies
👩‍👩‍👧‍👧 IAM Users and User Groups
🔖 AWS Account Alias

Let’s roll up our sleeves and get this built in the next hour. 💪

💻 Step #1

Launch EC2 Instances
Let’s start with the first task and boost computing power by launching some EC2 instances.

Log in to your AWS Management Console.
Open your EC2 console — search for it at the search bar.
![image](https://github.com/user-attachments/assets/5bdeef2e-694d-4fc0-a7ef-2e073e6ecf48)

*Here we can switch to the nearest Region based on our location

![image](https://github.com/user-attachments/assets/886a0bdf-a0c0-41c8-a4dc-85da14182c8d)

In your EC2 console, choose Launch instance.

Let’s set up your EC2 instance!

In Name, enter the value.

![image](https://github.com/user-attachments/assets/b3c9827f-cadc-4095-999c-b113f7be1d91)

Choose Add additional tags, which is right next to your Name field.
Choose Add new tag.
For the next tag, use this information:
Key: Env
Value: production

![image](https://github.com/user-attachments/assets/7d0ceb98-a3af-460b-9cf2-6b500ed02e60)

Head on down to see your EC2 settings and make sure the Amazon Machine Image (AMI) is using a Free tier eligible option.

![image](https://github.com/user-attachments/assets/62d63d2d-8604-490c-9ffb-0d5ae0e7dde3)

Take a look at your instance type, it should be t2.micro, 1 GiB under the free tier, since we don’t need a lot of storage.

![image](https://github.com/user-attachments/assets/801889db-8f1a-488d-9242-1248922c0e92)

For Key pair (login), select Proceed without a key pair.

![image](https://github.com/user-attachments/assets/34383443-1c78-41c5-99b9-33681c38b375)

You’re ready! Click Launch instance.

![image](https://github.com/user-attachments/assets/8df87ad5-c110-4a79-af7e-1d12c7033157)

![image](https://github.com/user-attachments/assets/3a855c03-3585-475a-bff9-b3f210053c40)

![image](https://github.com/user-attachments/assets/8e4cef12-19da-4916-9163-bd381cc801f3)

Network settings define how your instances interact with the internet and other AWS resources, determining factors like IP addresses and network routing.

Let’s create our second EC2 instance
Now let’s create one more EC2 instance for the development environment. We’re keeping the same settings from the first instance.

Repeat the same flow, but this time using these tags:

![image](https://github.com/user-attachments/assets/32203664-be57-41aa-bef6-849988de4d07)

Launch your second instance.
Select Instances from your left-hand navigation panel.
If you only see one instance on your page, make sure to use that refresh button!
You may need to refresh your page a couple of times.

![image](https://github.com/user-attachments/assets/646a692c-08c9-4cea-96a6-b4e033c1f401)

Let’s have a look at your wonderful work.
Select the checkbox next to one of your instances, and a pop-up window of information pops up!
Select the Tags tab.

![image](https://github.com/user-attachments/assets/3c2f611d-611a-4da3-a05b-bccb381aa75f)

![image](https://github.com/user-attachments/assets/edb16bb0-b198-44a7-8bbd-1fb40bfbffe6)

Voila — you’ll see the tags you’ve defined right here.

![image](https://github.com/user-attachments/assets/72d58010-0855-440f-9890-89697a0aee01)


📏 Step #2
Create an IAM Policy
🎉 WOOOOOOO! You’ve deployed two EC2 instances, one for your production environment and one for your development environment.

Now let’s move into our second task as NextWork’s engineer — it’s time to onboard the team’s new intern and set up permission policies.

Our intern should have permission to the development EC2 instance but not the production instance. We don’t want them to accidentally shut down the 
platform or push their changes to the production environment while they’re just testing things!

To start this task, we’ll use AWS IAM to give our intern access to the development instance first.

In this step, get ready to:

Create an IAM policy that gives access to the development instance.

Head to your IAM console.

![image](https://github.com/user-attachments/assets/f6a93ce6-1ef4-46e8-ac0f-e0193f3df3c8)

Now on the left-hand navigation panel of your IAM console, choose Policies.

Choose Create policy.
Switch your Policy editor tab to JSON

![image](https://github.com/user-attachments/assets/5d943a76-5150-4c25-97d3-a87a0b16762e)

Here’s the policy you’ll be using! Paste this policy into your editor — replace ALL of the existing code in your editor.

{
“Version”: “2012–10–17”,
“Statement”: [
{
“Effect”: “Allow”,
“Action”: “ec2:*”,
“Resource”: “*”,
“Condition”: {
“StringEquals”: {
“ec2:ResourceTag/Env”: “development”
}
}
},
{
“Effect”: “Allow”,
“Action”: “ec2:Describe*”,
“Resource”: “*”
},
{
“Effect”: “Deny”,
“Action”: [
“ec2:DeleteTags”,
“ec2:CreateTags”
],
“Resource”: “*”
}
]
}

![image](https://github.com/user-attachments/assets/35d29f1e-61ed-4c71-be0d-ad9cf075918f)

Select Next when you’re ready.
Fill in your policy’s details:
Name: NextWorkDevEnvironmentPolicy
Description: IAM Policy for NextWork’s development environment
Choose Create policy.
Oh no! Turns out there’s a rule for the characters allowed in your Policy description. Edit this description to get rid of that error 
(can you tell which character is not valid? There’s a hint given to you right underneath the Description’s text box).
Choose Create policy again when you’re done.

![image](https://github.com/user-attachments/assets/6f4f0d42-1ec1-4bbb-9673-72f200b9fcd4)

🔖 Step #3
Create an AWS Account Alias


Now that we can give our intern access to the development instance, the intern can’t wait to start. They’d love to jump into the team’s AWS account right away!

Sounds great… where should they go to log in?

In this step, get ready to:

Simplify user login to your AWS account using an Account Alias.

Head to your IAM dashboard.
In the right-hand side of the dashboard, choose Create under Account Alias.

![image](https://github.com/user-attachments/assets/10b1f5da-aa18-4965-b6fa-14b5be408070)

In the Preferred alias field, enterd

nextwork-alias-enter your name

![image](https://github.com/user-attachments/assets/113baf1c-49f7-4e40-b5d4-c71a785eeac4)

Then choose Create alias.

👩‍👩‍👧‍👧 Step #4
Create IAM Users and User Groups

Your account alias is looking slick! It should be a lot faster for users to find your account and log in now.

Our new intern doesn’t actually have a way to log in to the team’s AWS account yet… what should their username and password be?

You wouldn’t want to just share your account details with them. After all, you have access to the production instance, which they shouldn’t get access to.

Let’s solve this problem using IAM again — this time we’re using two other tools called groups and users.

In this step, get ready to:
Set up a dedicated IAM group for all NextWork interns, so you can manage all interns’ permissions from one place.Set up a dedicated IAM user for your new intern, so they have a way to log in.

Choose User groups in your left-hand navigation panel.
Choose Create group.
Let’s create your first user group!
To set up your user group:
Name: nextwork-dev-group
Attach permission policies: NextWorkDevEnvironmentPolicy

![image](https://github.com/user-attachments/assets/2f78093d-e3e8-49e6-bccd-15041a03caa3)

Select Create user group

![image](https://github.com/user-attachments/assets/55063589-ecf6-4238-a109-965554957d6c)

Now let’s add Users to your user group.
Choose Users from the left-hand navigation panel.
Choose Create user.
Let’s set up this user! Under User name, enter
nextwork-dev-enter your name

Uncheck the box for Users must create a new password at next sign-in — Recommended.

![image](https://github.com/user-attachments/assets/33d8404c-1000-4d36-8cf3-652a906ef366)

Select Next when you’re ready!
To set permissions for your user, we’ll simply add it to the user group you’ve created. Select the checkbox next to nextwork-dev-group.

![image](https://github.com/user-attachments/assets/ef4fdec6-2d31-415c-88a5-276acb1d87cd)

![image](https://github.com/user-attachments/assets/e54018be-0fc7-49d8-ba7f-51e35b812e4c)

Select Next.
Select Create user!
WOOO it’s a success — now you’re seeing some specific sign-in details for your new user. Stay on this page.

![image](https://github.com/user-attachments/assets/e00fbd9c-1bd4-4cb2-8372-f961230b306b)

🔓 Step #5
Test your intern’s access
The new intern is going to be stoked to receive their keys to the NextWork AWS account — well done 😎 YESS!

Before we pass them their login details, let’s test the interns’ IAM User’s access first. That way we can make sure that they have the right access to our development instance (and not the production instance).

In this step, get ready to:
Log into AWS using the intern’s IAM user.Test the intern’s access to your production and development instance.

Copy the Console sign-in URL. Do not close this tab!
Open a new incognito window on your browser.
Open the new console sign-in URL in your incognito window.
Using the User name and Console password given in your IAM tab, let’s log in!
As a new user, you’ll notice that some of your dashboard panels are showing Access denied already.

![image](https://github.com/user-attachments/assets/8bb76e82-acec-4b6a-b219-76df656c3c3d)

Head to your EC2 console, and make sure you’re in the same Region as the one where you deployed your two production and development instances.
Head to Instances.
Select your production instance, and in the Actions dropdown, select Manage instance state.

![image](https://github.com/user-attachments/assets/8411d966-0785-4ab2-a14a-818c9e108c18)

Let’s try to stop this instance. Select the Stop option, then Change state.

![image](https://github.com/user-attachments/assets/5f4eb846-5513-452a-b8f5-f5abec7a6932)

Select Stop.

![image](https://github.com/user-attachments/assets/9750d21a-03f2-4c21-9a5c-554707fb5cbf)

Now let’s try to stop the development instance.
Head back to the Instances page, and select the checkbox next to nextwork-dev-yourname.
Under the Actions drop-down, select Manage instance state.
Select Stop, then Change state. Select Stop.
Success!

![image](https://github.com/user-attachments/assets/1b1b7846-bf24-4eec-94ee-71ea713eda91)

😮‍💨 All Done!!
Nice work!
WOOHOOOOOOOOO WE DID IT 👏

Congrats on successfully using AWS IAM to control and test user permissions!

🗑️ Before You Go

Delete Your Resources
Make sure you delete all your resources to avoid getting charged. This is a super important task for every single project you set up.

Do you think you can delete the resources you’ve created today?

EC2 development instance

EC2 production instance

IAM user group

IAM user

IAM policy

Wooohoo! Today, you’ve learned how to:
💻 Launch EC2 instances.
🏷️ Use tags for easy identification.
💂 Set up IAM policies accessing EC2 instances based on their environment (development or production).
👩‍👩‍👧‍👧 Create an IAM user and assign them to the appropriate user group with the necessary permissions for their role.
🔓 Test IAM access for the User you’ve created.

