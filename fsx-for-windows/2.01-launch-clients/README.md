![](https://s3.amazonaws.com/aws-us-east-1/tutorial/AWS_logo_PMS_300x180.png)

![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_available.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_ingergration.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_ecryption-lock.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_fully-managed.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_lowcost-affordable.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_performance.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_scalable.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_storage.png)
# **Amazon FSx for Windows File Server**

## Workshop 2.01 - Launch a few clients

### Version fsx-w-1.0.0

---

© 2018 Amazon Web Services, Inc. and its affiliates. All rights reserved. This work may not be  reproduced or redistributed, in whole or in part, without prior written permission from Amazon Web Services, Inc. Commercial copying, lending, or selling is prohibited.

Errors or corrections? Email us at [darrylo@amazon.com](mailto:darrylo@amazon.com).

---

### Prerequisites

You must first complete [**Section 1: Prerequisites**](../README.md) and the previous steps in [**Section 2: The Workshop**](../README.md).

WARNING!! This workshop environment will exceed your free-usage tier. You will incur charges as a result of building this environment and completing the steps below.

## Workshop

### Step 2.01: Launch a few clients

> This step involves launching two Amazon EC2 instances (Windows & Linux), and two Amazon WorkSpaces (Windows & Linux)

#### Launch an Amazon EC2 Windows instance

**2.01.1.** Sign in to the [Amazon EC2 Console](https://console.aws.amazon.com/ec2/)

**2.01.2.** Select **Launch Instance**

**2.01.3.** Scroll down to **Microsoft Windows Server 2016 Base** and click **Select**

**2.01.4.** Scroll down and choose **c5.large** and click **Next: Configuration Instance Details**

**2.01.5.** Configure the instance with the following details:

| Detail | Value |
| :--- | :--- |
| Number of instances | 1 |
| Purchasing option | Request Spot instances unchecked |
| Network | Select the VPC created in the prerequisites section |
| Subnet | Select any subnet |
| Auto-assign Public IP | Use subnet setting (Enable) |
| Placement group | Add instance to placement group unchecked |
| Capacity Reservation | Open |
| Domain join directory | Select the directory created in the prerequisites section |
| IAM role | Select fsx-workshop-AmazonEC2RoleForSSM |
| CPU options | Specify CPU options unchecked |
| Shutdown behavior | Stop |
| Enable termination protection | Protect against accidental termination unchecked |
| Monitoring | Enable CloudWatch detailed monitoring |
| Subnet | Enable CloudWatch detailed monitoring unchecked |
| EBS-optimized instance | N/A |
| Tenancy | Shared - Run a shared hardware instance |
| Elastic GPU | Add GPU unchecked |

**2.01.6.** Select **Next: Add Storage**

**2.01.7.** Select **Next: Add tags**

**2.01.8.** Select **Add Tag**

> Enter the following key/value pair

| Key | Value |
| :--- | :--- |
| Name | Windows Server 2016 - FSx Workshop |

**2.01.9.** Select **Next: Configure Security Group**

**2.01.10.** Select the default VPC security group

**2.01.11.** Select **Review and Launch**

**2.01.12.** Select **Launch**

**2.01.13.** Choose an existing key pair and click the check box. Make sure you select a key pair that you have access to. If you need to create a new key pair, select **Create a new key pair** and follow the instructions.

**2.01.14.** Select **Launch Instances**

#### Launch an Amazon EC2 Windows instance

**2.01.15.** Sign in to the [Amazon EC2 Console](https://console.aws.amazon.com/ec2/)

**2.01.16.** Select **Launch Instance**

**2.01.17.** Scroll down to **Microsoft Windows Server 2016 Base** and click **Select**

**2.01.18.** Scroll down and choose **c5.large** and click **Next: Configuration Instance Details**

**2.01.19.** Configure the instance with the following details:

| Detail | Value |
| :--- | :--- |
| Number of instances | 1 |
| Purchasing option | Request Spot instances unchecked |
| Network | Select the VPC created in the prerequisites section |
| Subnet | Select any subnet |
| Auto-assign Public IP | Use subnet setting (Enable) |
| Placement group | Add instance to placement group unchecked |
| Capacity Reservation | Open |
| Domain join directory | Select the directory created in the prerequisites section |
| IAM role | Select fsx-workshop-AmazonEC2RoleForSSM |
| CPU options | Specify CPU options unchecked |
| Shutdown behavior | Stop |
| Enable termination protection | Protect against accidental termination unchecked |
| Monitoring | Enable CloudWatch detailed monitoring |
| Subnet | Enable CloudWatch detailed monitoring unchecked |
| EBS-optimized instance | N/A |
| Tenancy | Shared - Run a shared hardware instance |
| Elastic GPU | Add GPU unchecked |

**2.01.6.** Select **Next: Add Storage**

**2.01.7.** Select **Next: Add tags**

**2.01.8.** Select **Add Tag**

> Enter the following key/value pair

| Key | Value |
| :--- | :--- |
| Name | Windows Server 2016 - FSx Workshop |

**2.01.9.** Select **Next: Configure Security Group**

**2.01.10.** Select the default VPC security group

**2.01.11.** Select **Review and Launch**

**2.01.12.** Select **Launch**

**2.01.13.** Choose an existing key pair and click the check box. Make sure you select a key pair that you have access to. If you need to create a new key pair, select **Create a new key pair** and follow the instructions.

**2.01.14.** Select **Launch Instances**


---
## Next step
### Click on the link below to go to the next step

| Step | The Workshop |
| --- | :--- |
| 2.02 | [Map a file share on Windows and test](./2.02-map-fileshare-and-test)


## Troubleshooting
For feedback, suggestions, or corrections, please email me at [darrylo@amazon.com](mailto:darrylo@amazon.com).

## License
This library is licensed under the Amazon Software License.

