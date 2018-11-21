![](https://s3.amazonaws.com/aws-us-east-1/tutorial/AWS_logo_PMS_300x180.png)

![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_available.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_ingergration.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_ecryption-lock.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_fully-managed.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_lowcost-affordable.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_performance.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_scalable.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_storage.png)
# **Amazon FSx for Windows File Server**

## Create a file system

### Version fsx-w-1.0.0

---

© 2018 Amazon Web Services, Inc. and its affiliates. All rights reserved. This work may not be  reproduced or redistributed, in whole or in part, without prior written permission from Amazon Web Services, Inc. Commercial copying, lending, or selling is prohibited.

Errors or corrections? Email us at [darrylo@amazon.com](mailto:darrylo@amazon.com).

---
### Prerequisites

* An AWS account with administrative level access
* An Amazon EC2 key pair

If a key pair has not been previously created in your account, please refer to [Creating a Key Pair Using Amazon EC2](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#having-ec2-create-your-key-pair) from the AWS EC2 User's Guide.  

Verify that the key pair is created in the same AWS region you will use for the tutorial.

WARNING!! This tutorial environment will exceed your free-usage tier. You will incur charges as a result of building this environment and executing the scripts included in this tutorial. Delete all files on the EFS file system that were created during this tutorial and delete the  stack so you don’t continue to incur additional compute and storage charges.

### Create Amazon Virtual Private Clouds (Amazon VPC)

Click on the link below in the desired AWS region to create the AWS Cloudformation stack that will create two Amazon VPCs in your AWS account. These VPCs will host Amazon EFS file systems and the other AWS resources created in this workshop. Use the following parameters and the screenshot below as a guide to enter the appropriate AWS CloudFormation parameter values.

#### Parameters

- Select two unique CIDR blocks, one per VPC (default recommended)

- Select two (2) Availability Zones per VPC

![](./images/efs_workshop_prerequisites_parameters.png)

---

Click on the link below in the desired AWS region to create the AWS Cloudformation stack that will create an Amazon VPC, AWS Manageed Microsoft AD (enterprise), and two Windows EC2 instances with the Distributed File System role.

| AWS Region Code | Region Name |
| :--- | :--- 
| us-east-1 | [US East (N. Virginia)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=efs-workshop-prerequisites&templateURL=https://s3.amazonaws.com/aws-us-east-1/fsx-workshop/windows/current/templates/FSx_StackMaster_DFSn.yaml) |
| us-east-2 | [US East (Ohio)](https://console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/new?stackName=efs-workshop-prerequisites&templateURL=https://s3.amazonaws.com/aws-us-east-1/fsx-workshop/windows/current/templates/FSx_StackMaster_DFSn.yaml) |
| us-west-2 | [US West (Oregon)](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=efs-workshop-prerequisites&templateURL=https://s3.amazonaws.com/aws-us-east-1/fsx-workshop/windows/current/templates/FSx_StackMaster_DFSn.yaml) |
| eu-west-1 | [EU East (Ireland)](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/new?stackName=efs-workshop-prerequisites&templateURL=https://s3.amazonaws.com/aws-us-east-1/fsx-workshop/windows/current/templates/FSx_StackMaster_DFSn.yaml) |

---
## Next section
### Click on the link below to go to the next section

| [**Create file system**](workshop/1_create_file_system) |
| :---
---

For feedback, suggestions, or corrections, please email me at [darrylo@amazon.com](mailto:darrylo@amazon.com).

## License

This library is licensed under the Amazon Software License.
