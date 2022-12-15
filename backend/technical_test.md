# Epsy Backend Technical Test

## Business requirements
Your goal is to prepare application that will:

1. Download a file that contains list of users IDs
2. Use those IDs and call GraphQL API to fetch additional information about those users. API is GraphQL api with Cognito authentication in place. Credentials will be provided to you.
3. Fetched additional information should be sent to standard `std.out` in JSON format
4. Any errors should be logged to `std.error` in JSON format

### File
File location will be shared with you alongside API credentials. It is single file that will have format like:
```csv
418c552f-2e71-4cb6-8b7c-f68a6fdd246a
79e0bd79-a40c-4167-b927-44341d27ab81
9b21be6a-72ea-49c4-8f5f-c18068cc4a70
```

### GraphQL API
Schema can be found in [technical_test_schema.graphql](./technical_test_schema.graphql) file.

Address: `https://v3bdtj5rojdj5okuxsj5lirszi.appsync-api.us-east-1.amazonaws.com/graphql`

Authorization: `API_KEY` was used.

### std.out
Every single row that is processed should be:
1. Sent to a `std.out`
2. In JSON format, where keys need to follow lowercase underscore naming convention e.g. `first_name` rather than `FirstName`
3. Every processed row is a single entry to `std.out` (every line represents single row)

Additional data normalization:
1. API field `birthday` should be in format `{month}/{day}/{year}` e.g. `26/09/1986`

### std.error
As with every API, this GraphQL is not an exception, you might have cases where its timeouts, throws an error or returns wrong data.

In this case rows that couldn't be processed should be sent to `std.error`. With few things kept in mind:
1. Every unprocessed row should be separated entry to `std.error` (every line represents single row)
2. It should have format:
```json
{"user_id":  "<id of user that was unable to process>", "details": "<any extra information that might be helpful when debugging this problem>"}
```

## Technical requirements
Please prepare application with use of Python in `3.8+` version. It can be either CLI tool, serverless project, another API, interface is up to you. 

But please provide us with steps how to run your code in `README.md` file. 

Code can be put in Github repository and link shared with us, so we can review it :)

## What is important for us during review of your code?
* Complexity of the code
* Libraries used
* Consistency across the codebase
* Is the code following python patterns
* Cleanness of the code
* Error handling and error reporting/logging
