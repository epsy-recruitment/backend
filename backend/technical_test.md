# Epsy Backend Technical Test

## Business requirements
Your goal is to prepare function that will download encrypted CSV file from S3 bucket that contains list of users’ IDs and use those IDs to fetch extra information about users.

Fetched data should be sent to standard std.out in format:
user_id     | user_info
abcd-123  | {“first_name”: “John”, “last_name”: “Doe”, “birthdate”: “26.09.1986”}

please remember to format “birthdate” to “{Month}.{Day with leading zero}.{Year}”

Unprocessed data should be sent to std.error in format that will let us recognise user and error that happened during processing e.g.
user_id    | error
abcd-123 | Wrong JSON format

## CSV File
File is located in S3://<put address here> and you can decrypt it using key <put private key address here>

## User details service
It is GraphQL endpoint behind Cognito authentication, user and password will be provided to you. 

Please remember to treat this API as any third-party API. Which might fail for multiple reasons. Your code should be prepared for such case.

## Technical requirements
• Python: 3.8+
• Version control: Git
• Interface: CLI or lambda function (serverless.com framework) is fine

## What is important for us during review of your code?
• Complexity of code
• Libraries used
• Consistency across codebase
• Is code following python patterns
• Cleanness of code
• Error handling and error reporting/logging
