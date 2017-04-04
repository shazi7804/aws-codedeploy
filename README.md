# CodeDeploy generate permissions on AWS
This example provides all the permissions to build Codedeploy on AWS

## Note
In this example you will create the following permissions：

- A S3 bucket

- A IAM USER for Travis CI

    - attach policy: AWSCodeDeployDeployerAccess

    - user policy
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "Stmt1487528506000",
                "Effect": "Allow",
                "Action": [
                    "s3:*"
                ],
                "Resource": [
                    "arn:aws:s3:::codedeploy-*"
                ]
            }
        ]
    }
    ```

- A IAM Role for EC2 (default: Role-EC2-CodeDeploy)

    - trust role 

        ```json
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                "Effect": "Allow",
                "Principal": {
                    "Service": "ec2.amazonaws.com"
                },
                "Action": "sts:AssumeRole"
                }
            ]
        }
        ```

    - role policy

        ```json
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Sid": "Stmt1487527978000",
                    "Effect": "Allow",
                    "Action": [
                        "s3:GetObject",
                        "s3:GetObjectVersion",
                        "s3:ListBucket"
                    ],
                    "Resource": [
                        "arn:aws:s3:::codedeploy-*"
                    ]
                }
            ]
        }
        ```
- A IAM Role for CodeDeploy service (default: Role-CodeDeploy)

    - attach policy: AWSCodeDeployRole

- CodeDeploy application (default: $projectname)

    - Deployment config: CodeDeployDefault.AllAtOnce (default)
    - Deployment Group: dev, stage, prod

## Auto Install

    $ chmod +x install
    $ ./install

## Config

### Customize

- ProjectName = Set your project name.

### Global
- Region = AWS region

### S3
- BucketName = Set you S3 bucket name

### IAM group

- IAMGROUP = Set IAM group name

## Other 
You can without auto install.

### Create S3 bucket.

    $ ./s3bucket

### Create IAM user(TravisCI) to provide Travis CI deploy.

    $ ./iamuser-travis

### Create IAM Role to provide EC2 access S3, CodeDeploy.

    $ ./iamrole-ec2

### Create IAM Role to provide CodeDeploy service.

    $ ./iamrole-codedeploy

### Create CodeDeploy application, deployment_group

    $ ./codedeploy    