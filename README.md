# aws_cloud_formation_build_lambda

This CloudFormation Template creates the Lambda Function to enable Termination Protection in the account along with the Role and Policies needed 
to read and modify resources: EC2, ELB, RDS

## Setup

1) Create an internal load balancer to store the lambda function: Lambda-EnableTerminationProtection.py.zip

2) Modify bucket name on line 100: s3-bucket-lambda-function

3) Run CloudFormation template: (No input parameters are needed)

4) Open the Lambda function and create a test event as follow:

{
"TopicArn": "arn:aws:sns:eu-central-1:AccountNumber:TopicName",
"AccountDescription": "AccountName"
}

5) Run the Lambda function

## Lambda Function

- AWSLambdaEnableTerminationProtection: can be run to enable Termination Protection on the missing resources

## IAM Role and Policies

- Role Name: AWSLambdaEnableTerminationProtection 
- Policy 1 Name: Ec2-AWSLambdaEnableTerminationProtection
    - DecribeInstances
    - DecribeInstanceStatus
    - DescribeInstanceAttribute
    - ModifyInstanceAttribute

- Policy 2 Name: SNS-AWSEnableTerminationProtection
    - SNS Publish

- Policy 3 Name: ELB-AWSLambdaEnableTerminationProtection
    - DescribeLoadBalancers
    - DescribeLoadBalancerAttributes
    - ModifyLoadBalancerAttributes

- Policy 4 Name: RDS-AWSLambdaEnableTerminationProtection
    - DescribeDBInstances
    - ModifyDBInstance

N.B. you can find the Lambda function Code in repository https://github.com/DanielePaganoDritto/aws_lambda_enable_termination_protection
