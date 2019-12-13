# High-Availability-WebApp-Project

An AWS Cloudformation script that deploys the infrastructure for a high availability web application as specified by [Udacity](https://www,udacity.com) for Cloud DevOps Engineer - project 2. 

## Specifications

Specifications as per Udacity course requirements can be found [here](./documentation/project_specifications.md).

## Infrastructure Diagram

![Infrastructure Diagram](./documentation/High-Availability-WebApp-Project.svg)

## Prerequisites & Assumptions

- AWS account and appropriate credentials to deploy the script in its entirety. 
    - This script was developed and tested with the AdministratorAccess policy
- The AWS Cli installed and configured for your AWS account. 
    - This script was developed and tested with aws-cli v1.16.290.
- The setup scripts target AWS regions us-west2 by default and it is the recommendation region for deployment testing. Other regions may not have all the required AWS features.
- A BASH terminal to use the provided helper scripts. If using windows simply run the aws cli command manually. 

## Deployment

### Download Project Repo

Clone or download the project GIT repo to your AWS CLI workstation. 

### Setup S3 Bucket and Parameter Store

The UserData for the configured instances expects the web app source files to be located in a site.zip file stored in the root dir of an S3 bucket that is part of the same AWS account. The name of the S3 bucket is stored in Parameter store. This parameter store key is then passed to the script as part of its parameters. The script will also create an appropriate role giving the EC2 instances permission to the s3 bucket. 

**Steps**

1. Create an S3 bucket in the target AWS account region US-WEST2. Make note of the bucket name. 
2. Upload /website/site.zip to the root of the newly created S3 bucket. 
3. In AWS Systems Manager - Parameter Store, create a new "standard" tier parameter of type "string" with the name of your choice (Script default name is "HAWP-Source").
4. For the value of the parameter enter the S3 bucket name and save. 

### Modify Parameters as Required

A parameters file has been provided as hawp.json. Here you can set the Parameter Store containing the S3 Bucket name (default "HAWP-Source"),  the environment name, VPC and Subnet IP's, instance type (default t3.medium), instance ami (default Ubuntu Server 18.04 LTS).

The create.sh and update.sh helper scripts provided in the repo target AWS Region us-west-2 by default. You can edit these scripts to change the region if you wish however the Cloudformation script has only been tested on us-west-2.

### Deploy the CloudFormation Stack

Deploy the CloudFormation stack by running the create.sh helper script from the project directory. 

```./create.sh MyStackName hawp.yml hawp.json```

Replace `MyStackName` as desired.

TODO: Deployment Instructions  
TODO: Usage Instructions  
TODO: Access instructions  
TODO: Testing instructions
