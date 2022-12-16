# Epsy Backend Technical Test

## Background
Our event tracking system generates daily dumps of the data in CSV format stored to S3. 

Sample event consist of timestamp, user, event name - example record will look like:

```csv
1671192760,"79e0bd79-a40c-4167-b927-44341d27ab81","user.logged"
```

Additionally, our platform exposes GraphQL endpoint for user data retrieval. 
API will return user definition object matching [technical_test_schema.graphql](./technical_test_schema.graphql) file.

Both, S3 resource and GraphQL API is protected with username and password (implemented via AWS Cognito). 

## Task
Create command line tool using [click](https://click.palletsprojects.com/en/8.1.x/) framework which will:

### 1. Authenticate user using provided credentials against Cognito IDP
> **TIP**
> 
> `boto3` by default expects AWS Credentials to be provided, that can be changed by setting `signature_version` configuration 
parameter to `botocore.UNSIGNED` 

### 2. Fetch S3 events file from S3 location listed below using boto3 SDK

> **TIP**
> 
> You need to exchange Cognito Identity for AWS Credentials - those can be used for communication with S3
> This can be done by using:
>  - https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/cognito-identity.html#CognitoIdentity.Client.get_id
>  - https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/cognito-identity.html#CognitoIdentity.Client.get_credentials_for_identity

### 3. Use user IDs from downloaded file to call GraphQL API and fetch additional information about those users.

### 4. Provide basic stats about events

- number of events per day
- number of events per user role
- Top 10 users (users with highest number of events) inc. name and last name 

Additional requirements:
1. Fetched additional information should be sent to standard `std.out` in either JSON or table format
2. Any errors should be logged to `std.error` in JSON format


## Input data

### API
Address: `https://v3bdtj5rojdj5okuxsj5lirszi.appsync-api.us-east-1.amazonaws.com/graphql`
Schema: [technical_test_schema.graphql](./technical_test_schema.graphql)
Username and password will be provided in separate message.

> Please note that our API may occasionally return errors, and your code should handle that. 

### S3 Data location
Bucket name:
File key: 



## Technical requirements
- Python 3.8+ compatibility 
- Code should be shared via GitHub (public or private repository)
- Instructions for running the code should be included in `README.md` file.
- All exceptions and processing errors should be written to `std.err`


## FAQ
> ### How much time do I have for the task?
> 
> There is no time limit, but we strongly recommend to timebox your work to maximum of 2 hours

> ### Do I need to implement all requirements?
>
> Steps 1-3 are required, 

> ### May I use stackoverflow, documentation, etc 
>
> Yes, all the resources are allowed, as long as you will be able to explain what code is doing 

> ### I have more ideas how this code can be improved, but there is not enough time 
>
> Feel free to provide all the ideas in your README.md file 

> ### Can I share the code with other companies?
>
> Yes, feel free. But please don't share the username details. 

> ### Do I need to use listed libraries 
>
> Yes, click and boto3 are common libraries in our stack  


## Useful information

- https://aws.amazon.com/appsync/ - GraphQL Server implementation 
- https://aws.amazon.com/cognito/ - IDP implementation 
- https://aws.amazon.com/s3/ - file storage 
- https://boto3.amazonaws.com/v1/documentation/api/latest/index.html - Python AWS SDK 


## What is important for us during review of your code?
- Complexity of the code
- Used libraries
- Consistency across the codebase
- Compatibility with Python standards
- Cleanness of the code
- Error handling and error reporting/logging
- Performance 
- Memory consumption
- Output formatting
- User experience - that tool can be potentially used by non-devs
- Security
- Documentation 
