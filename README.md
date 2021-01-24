# ImageResizer
Image resizer lambda function


# Installation
  - dotnet new -i Amazon.Lambda.Templates
  - dotnet new | Select-String -SimpleMatch 'lambda'


# Create Source Bucket in AWS S3
  - aws s3 mb s3://<source bucket> --region us-west-2


# Create Destination Bucket in AWS S3
  - aws s3 mb s3://<destination bucket> --region us-west-2


# Create PutObject Policy
  - aws iam create-policy --policy-name <policy document> --policy-document file://<filename>.json

  Sample policy document (<filename>.json):
  {
  "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Action": "s3:PutObject",
        "Resource": "arn:aws:s3:::<destination bucket>/*"
      }
    ]
 }


# Create IAM Role
  - image-resizer-role
  - AWSLambdaBasicExecutionRole
  - AmazonS3ReadOnlyAccess


# Add function-role to aws-lambda-tools-default.json
  - "function-role": "arn:aws:iam::<account>:role/image-resizer-role"


# Create Empty Lambda Function
  - dotnet new lambda.EmptyFunction --name ImageResizer --profile default --region us-west-2


# Install Packages
  - dotnet add package AWSSDK.S3
  - dotnet add package Magick.NET-Q16-AnyCPU --version 7.21.1


# Deploy Lambda Function
  - dotnet lambda deploy-function ImageResizer


# Add Trigger to ImageResizer Lambda Function
  - use <source bucket> as the source bucket


# Get Function Config
  - dotnet lambda get-function-config ImageResizer


# Update Function Config
  - dotnet lambda update-function-config


# References
  - https://devblogs.microsoft.com/dotnet/net-core-image-processing/
  - https://adamtheautomator.com/aws-lambda-example/#How_does_a_Lambda_function_work
