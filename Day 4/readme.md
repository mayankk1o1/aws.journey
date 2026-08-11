# EC2 Instance Creation Using AWS CloudFormation

## Overview

Created an **AWS EC2 instance using a YAML CloudFormation template**. Used VS Code to create/edit the template.


## Key Points

* **CloudFormation** → Infrastructure as Code (IaC) service.
* **Resources** → Defines AWS resources to create.
* **AWS::EC2::Instance** → Creates an EC2 instance.
* **ImageId** → Specifies the AMI/OS. AMI is region-specific.
* **InstanceType** → Defines instance size, e.g. `t3.micro`.
* **Parameters** → Makes template values configurable.
* **!Ref** → References parameter values.
* **Tags** → Used to identify the EC2 instance.

## Basic Flow

```text
YAML Template → CloudFormation Stack → EC2 Instance
```

## Important Note

Always ensure the **AMI ID is available in the selected AWS region** and maintain correct YAML indentation.

Check the other YAML file for the exact template I used to create an EC2 instance! 