![](https://s3.amazonaws.com/aws-us-east-1/tutorial/AWS_logo_PMS_300x180.png)

![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_available.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_ingergration.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_ecryption-lock.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_fully-managed.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_lowcost-affordable.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_performance.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_scalable.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_storage.png)

# **Amazon FSx for Windows File Server**

## Map file share

### Version 2018.11

fsx.w.wrkshp.2018.11

---

© 2018 Amazon Web Services, Inc. and its affiliates. All rights reserved. This work may not be  reproduced or redistributed, in whole or in part, without prior written permission from Amazon Web Services, Inc. Commercial copying, lending, or selling is prohibited.

Errors or corrections? Email us at [darrylo@amazon.com](mailto:darrylo@amazon.com).

---

### Map file share

You must first complete [**Prerequisites**](../0-prerequisites) and the previous step [**Create a file system**](../2-launch-clients)

WARNING!! This workshop environment will exceed your free-usage tier. You will incur charges as a result of building this environment and completing the steps below.

### Step 3.1: Log on to the Windows EC2 instance

- From the Amazon EC2 Console, copy the **Public DNS (IPv4)** name of the **Windows Server 2016 - FSx Workshop** instance
- Launch your remote desktop application to log on to the Windows EC2 instance you created in the previous workshop
- Log on to the **Windows Server 2016 - FSx Workshop** instance using following AD credentials

| Username | Password |
| :--- | :--- 
| admin@<<directory>> (e.g. admin@example.com) | The Microsoft Active Directory (MAD) password you entered as a parameter when you launched the prerequisites CloudFormation stack|

### Step 3.2: Copy the DNS name of the FSx for Windows file system

- From the Amazon FSx Console select the file system you created in the **Create a file system** section.
- Click the **Network & Security** tab.
- Copy the **DNS name** of the file system

### Step 3.3: Map the file system's default share

> Complete the following steps when logged on to the **Windows Server 2016 - FSx Workshop** instance

- Open **File Explorer**
- Context-click **This PC** and click **Map network drive...**
- Map the file share using the following information, 

| Configuraiton detail | Value 
| :--- | :--- 
| Drive | Z:
| Folder | UNC path of the file system's default file share using the DNS name you copied above - **\\\\<file system's DNS name>>\share** - (e.g. **\\\fs-0123456789abcdef.example.com\share**)
| Reconnect at sign-in | Leave **checked**
| Connect using different credentials | Leave **unchecked**

### Step 3.3: Access a file share

> Complete the following steps when logged on to the **Windows Server 2016 - FSx Workshop** instance

- In the **File Explorer** window of the **Z:\**

---
## Next section
### Click on the link below to go to the next section

| [**Map file share**](../3-map-file-share) |
| :---
---

For feedback, suggestions, or corrections, please email me at [darrylo@amazon.com](mailto:darrylo@amazon.com).

## License

This library is licensed under the Amazon Software License.
