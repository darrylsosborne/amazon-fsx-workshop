![](https://s3.amazonaws.com/aws-us-east-1/tutorial/AWS_logo_PMS_300x180.png)

![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_available.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_ingergration.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_ecryption-lock.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_fully-managed.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_lowcost-affordable.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_performance.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_scalable.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_storage.png)


# **Amazon FSx for Windows File Server**

## Workshop

### Version 2018.11

fsx.w.wrkshp.2018.11

---

© 2018 Amazon Web Services, Inc. and its affiliates. All rights reserved. This work may not be  reproduced or redistributed, in whole or in part, without prior written permission from Amazon Web Services, Inc. Commercial copying, lending, or selling is prohibited.

---

## Workshop Overview

### Overview

This will show solutions architects how to take advantage of a fully-managed Windows native file system for various application workloads like home directories, web serving & content management, enterprise applications, analytics, and media & entertainment.

This workshop will cover how to create and initiate an incremental file-system-consistent backup of a file system, as well as how to access the file system from a broad range of clients from Windows and Linux EC2 instances to Amazon WorkSpaces and AppStream 2.0. We will also restore a backup as a new file system and setup Microsoft Distributed File System (DFS) Replication between two file systems across Availability Zones. For those of you who want to consolidate multiple file systems under a single namespace, we'll spend time setting up DFS Namespaces with two file systems to achieve double the capacity and throughput.

### Informational

You will be using your own AWS account for all workshop activities.
WARNING!! This workshop will exceed your free-usage tier. You will incur charges as a result of stepping through this workshop. Terminate all resources that were created during this workshop so you don’t continue to incur ongoing charges.

### The Workshop

This workshop is divided into two sections with the second section dependent on the first. The first section creates all the workshop prerequisites, like an Amazon VPC, an AWS Managed Microsoft AD, mulitple Amazon EC2 instances, Amazon WorkSpaces, and an AppStream 2.0 stack. The second section depends on the resources created in the first. In this section you will create the FSx for Windows file system and complete various administrative tasks and run a few performance tests against the file system.

### Section 1: Prerequisites

Click on the link below to go to the Amazon FSx for Windows File Server prerequisites section. Start this section at the start of the workshop, as soon as you sit down. The referenced Amazon CloudFormation template will create a stack that contains all the prerequisites for the next section of the workshop and it will take 20-30 minutes for the CloudFormation stack to  automatically build out the environment. You must complete this section before moving to **Section 2: The Workshop**.

| Step | The Prerequisites |
| --- | :--- |
| 1.00 | [Prerequisites](./1.00-prerequisites) |


### Section 2: The Workshop

Click on the links below to go to the FSx for Windows worshop steps. You must first complete **Section 1: Prerequisites** above before moving on to the steps in**Section 2: The Workshop** below.

| Step | The Workshop |
| --- | :--- |
| 2.00 | [Create a file system](./2.00-create-file-system)
| 2.01 | [Launch a few clients](./2.01-launch-clients)
| 2.02 | [Map a file share on Windows and test](./2.02-map-fileshare-and-test)
| 2.03 | [Create new shares and test](./2.03-create-new-shares-and-test)
| 2.04 | [Backup the file system](./2.04-backup-file-system)
| 2.05 | [Mount a file system on Linux and test](./2.05-mount-filesystem-and-test)
| 2.06 | [Restore a backup](./2.06-restore-backup)
| 2.07 | [Setup and test DFS Replication](./2.07-setup-and-test-dfsr)
| 2.08 | [Setup and test DFS Namespaces](./2.08-setup-and-test-dfsn)
| 2.09 | [Delete the resources](./2.09-delete-resources)


## License

This library is licensed under the Amazon Software License.