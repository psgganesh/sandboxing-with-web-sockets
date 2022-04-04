# Backend SAM CLI template 

This is the code and template for the chat-app.  There are three functions contained within the directories and a SAM template that wires them up to a DynamoDB table and provides the minimal set of permissions needed to run the app:

```
.
├── README.md                   <-- This instructions file
├── onconnect                   <-- Lambda Source code onconnect
├── ondisconnect                <-- Lambda Source code ondisconnect
├── sendmessage                 <-- Lambda Source code sendmessage
└── template.yaml               <-- SAM template for Lambda Functions and DDB
```

# Deploying to your account

You have two choices for how you can deploy this code.

## Serverless Application Repository

The first and fastest way is to use AWS's Serverless Application Respository to directly deploy the components of this app into your account without needing to use any additional tools. You'll be able to review everything before it deploys to make sure you understand what will happen.  Click through to see the [application details](https://serverlessrepo.aws.amazon.com/applications/arn:aws:serverlessrepo:us-east-1:729047367331:applications~simple-websockets-chat-app).

## AWS CLI commands

If you prefer, you can install the [AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html) and use it to package, deploy, and describe your application.  These are the commands you'll need to use:

```
sam deploy --guided

aws cloudformation describe-stacks \
    --stack-name simple-websocket-chat-app --query 'Stacks[].Outputs'
```

**Note:** `.gitignore` contains the `samconfig.toml`, hence make sure backup this file, or modify your .gitignore locally.

## Credits - SAM CLI template 
The SAM CLI template is been refererred from https://github.com/aws-samples/simple-websockets-chat-app