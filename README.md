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
















