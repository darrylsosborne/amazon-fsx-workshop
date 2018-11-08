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

**2.01.1.** Sign in to the [Amazon EC2 Console](https://console.aws.amazon.com/ec2/)

**2.01.2.** Select **Launch Instance**

**2.01.3.** Scroll down to **Microsoft Windows Server 2016 Base** and click **Select**

**2.01.4.** Scroll down and choose **c5.large** and click **Next: Configuration Instance Details**

**2.01.5.** Configure the instance with the following details:

> **Number of instances**: 1
> **Purchasing option**: leave **Request Spot instances** unchecked
> **Network**: 
> **Subnet**: 
> **Auto-assign Public IP**: 
> **Placement group**: 
> **Capacity Reservation**: 
> **Domain join directory**: 

**Network & Security** section

- **Virtual private cloud (VPC)**: select the VPC crated in the prerequisites section (to verify the VPC Id, view the output of the AWS CloudFormation stack)
- **Availability zone**: select any availability zone
- **Subnet**: select the subnet
- **VPC Security Groups**: select the default security group

**Windows Authentication** section

- **Microsoft Active Directory ID**: select the directory created in the prerequisites section (to verify the the Directory Id, view the output of the AWS CloudFormation stack)

**Encryption** section

- **Encryption key**: select the default aws/fsx key

**Maintenance preferences - optional** section
(expand the window)

- **Daily automatic backup window**: No preference
- **Automatic backup retention period**: 0 days (this disables automatic backups)
- **Weekly maintenance window**: No preference

**2.00.3.** Select **Review summary**

**2.00.4.** Review the file system attributes & estimated monthly costs

**2.00.5.** Select **Create file system**

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

