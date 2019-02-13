Deploy a Cloudformation stack called s3-user to your AWS account
This repository contains serverless code to deploy a IAM user into your AWS account. The user will be able to view s3 resources but not download them.
The user name can be passed in or it will be defaulted to myS3user

Prerequisites
Must have Serverless instaled on your machine (verify with the command: serverless -v)
Must have default credentials in your .aws/credentials file with a user key and secret that has access to deploy Cloudformation to that account.

Once the repository has been cloned to your local directory

aws cloudformation create-stack --stack-name ir-test --template-body file://cloudformation_template.yml --capabilities CAPABILITY_NAMED_IAM
aws cloudformation update-stack --stack-name ir-test --template-body file://cloudformation_template.yml --capabilities CAPABILITY_NAMED_IAM