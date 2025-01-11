# NBA Game Day Alerts System
## Overview

The NBA Game Day Alerts System provides real-time notifications for ongoing NBA games, delivering score updates at regular intervals to users via email. This system integrates with several AWS services, including *Amazon SNS*, *AWS Lambda*, and *Amazon EventBridge*, to deliver seamless notifications powered by the *NBA API* (SportsData.io). It’s designed to showcase cloud automation, real-time event processing, and user-centric notifications.

## Key Features

- Retrieves live NBA game scores using the SportsData.io API.
- Sends real-time game score updates to subscribers via Email through Amazon SNS.
- Automated notifications based on a defined schedule using Amazon EventBridge.
- Security-focused design with least privilege for IAM roles and access control.

## Requirements
Before setting up the project, make sure you have:

- A SportsData.io API Key for access to NBA game data.
- An AWS account, with basic knowledge of AWS services like Lambda, SNS, and EventBridge.
- Familiarity with Python 3.x for the Lambda function.

## Architecture
The system architecture consists of the following components:

- NBA Game API: Retrieves live game scores.
- AWS Lambda: Executes the logic for processing and sending notifications.
- Amazon SNS: Handles the delivery of notifications via SMS or email.
- Amazon EventBridge: Triggers regular updates based on a scheduled cron job.

## Technology Stack
- Cloud Platform: AWS
- Key AWS Services: SNS, Lambda, EventBridge
- External API: SportsData.io (NBA Game Data)
- Programming Language: Python 3.x
- Security: IAM roles with least privilege policies

## Project Structure
```
game-day-notifications/
├── src/
│   └── gd_notifications.py      # Lambda function code
├── policies/
│   ├── gd_sns_policy.json       # SNS permissions policy
│   ├── gd_eventbridge_policy.json # EventBridge permissions policy
│   └── gd_lambda_policy.json    # Lambda execution policy
├── .gitignore
└── README.md                    # Project documentation
```

## Getting Started
### Clone the Repository
To get started, first clone the repository to your local machine:
```
git clone https://github.com/YekAz/Gameday-Notifications-System.git
cd Gameday-Notifications-System
```

## Create SNS Topic
1. Open the AWS Management Console.
2. Navigate to the SNS service.
3. Click Create Topic, and select Standard as the topic type.
4. Provide a name (e.g., gd_topic) and note the ARN.
5. Click Create Topic.

## Add Subscriptions
1. After creating the SNS topic, go to the Subscriptions tab.
2. Click Create Subscription and choose the protocol:
    - Email: Enter your email address.
3. Confirm the subscription from your inbox.

## Create IAM Policies
1. Navigate to the IAM service.
2. Under Policies, click Create Policy and choose the JSON tab.
3. Paste the contents from gd_sns_policy.json (located in the policies directory).
4. Replace REGION and ACCOUNT_ID with your respective AWS region and account ID.
5. Click Next: Tags, then Next: Review.
6. Enter the policy name (e.g., gd_sns_policy) and click Create Policy.

## Set Up IAM Role for Lambda
1. In IAM, go to Roles → Create Role.
2. Select AWS Service → Lambda.
3. Attach the following policies:
    - SNS Publish Policy (created earlier)
    - Lambda Basic Execution Role (AWS managed policy)
4. Enter the role name (e.g., gd_role) and click Create Role.
5. Note the Role ARN for later use.

## Deploy the Lambda Function
1. Navigate to the Lambda service in the AWS Management Console.
2. Click Create Function and select Author from Scratch.
3. Enter a function name (e.g., gd_notifications) and choose Python 3.x as the runtime.
4. Assign the IAM Role (gd_role) to the function.
5. Copy the contents of gd_notifications.py and paste it into the inline code editor.
6. Set the following Environment Variables:
    - NBA_API_KEY: Your API key from SportsData.io.
    - SNS_TOPIC_ARN: The ARN of the SNS topic.
7. Click Create Function.

## Configure EventBridge for Automation
1. Go to EventBridge in the AWS Management Console.
2. Select Rules → Create Rule.
3. Choose Event Source → Schedule.
4. Set up the schedule (e.g., for hourly updates).
5. Under Targets, select the Lambda function (gd_notifications).
6. Save the rule to automate notifications.

## Testing the System
1. Open the Lambda function in the AWS Console.
2. Create a test event and execute it.
3. Check the CloudWatch Logs for any errors.
4. Verify that the subscribed users receive SMS or email notifications with the game score updates.

## Conclusion
With this system in place, users will receive real-time NBA game score updates on a regular basis, enhancing their fan experience. The project leverages AWS services for a seamless and automated notification process, making it scalable and efficient for future enhancements.
