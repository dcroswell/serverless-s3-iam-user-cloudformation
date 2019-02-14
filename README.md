# Deploy a Cloudformation stack s3-user-dev to AWS account #

This repository contains **Serverless** code to deploy an IAM user `myS3user` (or a username you can specify) into an AWS account via a **Cloudformation** stack `s3-user-dev`. 
The user will have an attached policy that allows console log in and access to view all S3 resources but not download them.

The user name can be passed in as a parameter or it will be defaulted to `myS3user`.

#### Prerequisites ####

1. Must have **Serverless** installed on your machine (verify with the command: Serverless -v). 
Instructions can be found [here](https://serverless.com/framework/docs/providers/aws/guide/installation/).

2. Must have **AWS** credentials profile in your .aws/credentials file with a user key and user secret that has access to deploy Cloudformation stacks to that account.
Instructions can be found [here](https://serverless.com/framework/docs/providers/aws/guide/credentials/).

## User Creation ##
Once the repository has been cloned to your local directory, run the following command in the project directory using your preferred profile (default profile used below):

*serverless deploy -v --aws-profile default --username myS3user --stage dev*

## Confirmation ##

To confirm a successful deployment, log in to the account with the user name supplied and a password of `myP@ssW0rd`.
If a username was not passed in then use the default user name of `myS3user` and a password of `myP@ssW0rd`.

## Clean Up ##

Once it has been confirmed that the user has been created with the correct access, run the following command to remove the stack:

*serverless remove --aws-profile default --stage dev*

Note: Your stage parameter used above must match the stage name used to create the stack.

## Troubleshooting ##

If the new user created can not log in:

1. Confirm that the stack was created by logging in to the console and checking the resources and events in the Cloudformation console.
2. Confirm that the user was created and has the following policy attached:

```json{
     "Version": "2012-10-17",
     "Statement": [
         {
             "Action": [
                 "s3:*"
             ],
             "Resource": [
                 "arn:aws:s3:::*"
             ],
             "Effect": "Allow"
         },
         {
             "Action": [
                 "s3:GetObject",
                 "s3:DeleteObject"
             ],
             "Resource": [
                 "arn:aws:s3:::*"
             ],
             "Effect": "Deny"
         }
     ]
 }```