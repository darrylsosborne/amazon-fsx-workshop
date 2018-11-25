
![](https://s3.amazonaws.com/aws-us-east-1/tutorial/AWS_logo_PMS_300x180.png)

![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_available.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_ingergration.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_ecryption-lock.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_fully-managed.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_lowcost-affordable.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_performance.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_scalable.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_storage.png)


# **Amazon FSx for Lustre**

## Workshop

### Version 2018.11

fsx.l.wrkshp.2018.11

---

© 2018 Amazon Web Services, Inc. and its affiliates. All rights reserved. This work may not be  reproduced or redistributed, in whole or in part, without prior written permission from Amazon Web Services, Inc. Commercial copying, lending, or selling is prohibited.

---

## Workshop Overview

### Overview

This will show solutions architects how to take advantage of a fully-managed Lustre file system with Amazon S3 integration that links the file system to an existing data repository.

This workshop will cover how to create a file system and load metadata from an Amazon S3 bucket. Learn how to lazy load objects from Amazon S3 to an FSx for Lustre file system or review some sample scripts to bulk load all objects with a single operation.  FSx for Lustre file systems are designed for compute-intense workloads and can achieve high levels of iops and throughput. Test read and write performance as you walk through these step-by-step instructions and monitor how hard your tests are driving the file system by creating an Amazon CloudWatch dashboard for your file system.

### Informational

You will be using your own AWS account for all workshop activities.
WARNING!! This workshop will exceed your free-usage tier. You will incur charges as a result of stepping through this workshop. Terminate all resources that were created during this workshop so you don’t continue to incur ongoing charges.

### Prerequisites

Click on the link below to go to the Amazon FSx for Windows File Server prerequisites section. Start this section at the start of the workshop, as soon as you sit down. The referenced Amazon CloudFormation template will create a stack that contains all the prerequisites for the next section of the workshop and it will take 20-30 minutes for the CloudFormation stack to  automatically build out the environment. You must complete this section before moving to **The Workshop**.

| Step | Workshop |
| :--- | :---
| 0 | [Prerequisites](workshop/0-prerequisites) |

### The Workshop

Click on the links below to go to the FSx for Windows workshop. You must first complete **Prerequisites** above before moving on to the steps in**The Workshop** below. These steps must be completed in order.


| Step | Workshop |
| :--- | :---
| 1 | [Create a file system](workshop/1-create-file-system) |
| 2 | [Create a CloudWatch dashboard](workshop/2-create-dashboard) |
| 3 | [Launch a few clients](workshop/3-launch-clients) |
| 4 | [Mount a file system on Linux](workshop/4-mount-file-system) |
| 5 | [Lazy load files](workshop/5-lazy-load) |
| 6 | [Bulk load files](workshop/6-bulk-load) |
| 7 | [Run IOPS tests](workshop/7-iops-tests) |
| 8 | [Run throughput tests](workshop/8-throughput-tests) |



## License

This library is licensed under the Amazon Software License.
