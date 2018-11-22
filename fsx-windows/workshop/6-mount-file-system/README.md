![](https://s3.amazonaws.com/aws-us-east-1/tutorial/AWS_logo_PMS_300x180.png)

![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_available.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_ingergration.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_ecryption-lock.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_fully-managed.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_lowcost-affordable.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_performance.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_scalable.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_storage.png)

# **Amazon FSx for Windows File Server**

## Mount file system

### Version 2018.11

fsx.w.wrkshp.2018.11

---

© 2018 Amazon Web Services, Inc. and its affiliates. All rights reserved. This work may not be  reproduced or redistributed, in whole or in part, without prior written permission from Amazon Web Services, Inc. Commercial copying, lending, or selling is prohibited.

Errors or corrections? Email us at [darrylo@amazon.com](mailto:darrylo@amazon.com).

---

### Mount file system

You must first complete [**Prerequisites**](../0-prerequisites) and the previous step [**Backup file system**](../5-backup-file-system)

WARNING!! This workshop environment will exceed your free-usage tier. You will incur charges as a result of building this environment and completing the steps below.

### Step 6.1: Log on to the Linux EC2 instance

- From the Amazon EC2 Console, select the **Amazon Linux - FSx Workshop** instance
- Click **Connect**
- Use the connection information to SSH to the instance using your laptop's terminal application

### Step 6.2: Install linux applications

> Complete the following steps SSH'd in to the **Amazon Linux - FSx Workshop** instance

- Run the following script
- **cifs-utils** is the only utility needed to mount the FSX for Windows file system on Amazon Linux, the other utilites will be used for testing and monitoring performance

```sh
sudo yum update -y
sudo yum install -y parallel tree git cifs-utils
sudo yum install -y --enablerepo=epel nload ioping
git clone https://github.com/bengland2/smallfile.git

```

### Step 6.3: Mount the file system's default file share

> Complete the following steps SSH'd in to the **Amazon Linux - FSx Workshop** instance

- Run the following script to create a local mount point and mount the file system
- You will be prompted to enter the password of the AD user **admin** (e.g. admin@example.com)

```sh
sudo mkdir -p /mnt/fsx/share
# for example: sudo mount -t cifs //fs-0123456789abcdef.example.com/share /mnt/fsx/share --verbose -o vers=2.0,user=admin@example.com
sudo mount -t cifs //<file-system-dns-name>/share /mnt/fsx/share --verbose -o vers=2.0,user=admin@<domain>
```

- Run **df** to verfify the file share has been mounted correctly

```sh
df
```

- Experiment and mount the file shares you created in the previous section. Use the following table to mount each share to a different local mount point. Remember to create the local mount point first before mounting the file share.

| Local mount point | File share |
| :--- | :--- |
| /mnt/fsx/data | data |
| /mnt/fsx/finance | finance |
| /mnt/fsx/sales | sales |
| /mnt/fsx/marketing | marketing |

- Were you able to mount all file shares?
- Why not?

- Run **df** to verfify all file shares have been mounted correctly

```sh
df
```

- Can you mount a single file share and gain access all the sub-shares?
- Try this

```sh
sudo mkdir -p /mnt/fsx
# for example: sudo mount -t cifs //fs-0123456789abcdef.example.com/share /mnt/fsx/share --verbose -o vers=2.0,user=admin@example.com
sudo mount -t cifs //<file-system-dns-name>/d$ /mnt/fsx --verbose -o vers=2.0,user=admin@<domain>
```

- Run a simple touch command to write to the /share file share.

```sh
touch amazon_linux_test.txt
```

- What two things can you do to write to these shares?

```sh
sudo touch amazon_linux_test.txt
```

```sh
sudo chown ec2-user:ec2-user /mnt/fsx/share
touch amazon_linux_test.txt
```


### Step 6.4: Run performance tests

> Complete the following steps SSH'd in to the **Amazon Linux - FSx Workshop** instance

- Run scripts below to evaluate file share performance. Change the path to access any of the file shares you've created (e.g. of=/mnt/fsx/share, of=/mnt/fsx/data, of=/mnt/fsx/marketing, etc.)

```sh
time sudo dd if=/dev/zero of=/mnt/fsx/share/2G-fsx-dd-$(date +%Y%m%d%H%M%S.%3N) bs=1M count=2048 status=progress conv=fsync
```
```sh
time sudo dd if=/dev/zero of=/mnt/fsx/share/2G-fsx-dd-$(date +%Y%m%d%H%M%S.%3N) bs=1M count=2048 status=progress oflag=sync
```
```sh
job_name=$(echo $(uuidgen)| grep -o ".\{6\}$")
bs=1024K
count=256
sync=oflag=sync
threads=128

sudo mkdir -p /mnt/fsx/share/${job_name}/{1..128}

time seq 1 ${threads} | sudo parallel --will-cite -j ${threads} dd if=/dev/zero of=/mnt/fsx/share/${job_name}/{}/dd-$(date +%Y%m%d%H%M%S.%3N) bs=${bs} count=${count} ${sync} &
```

- While the parallel dd command is running, run the **nload** command below for 10-20 seconds to monitor network throughput in real time
- Exit **nload** by pressing **Control+z**
- How long did it take to generate 32 GiB of data across 128 files?
- What was the average throughput of this test?

```sh
job_name=$(echo $(uuidgen)| grep -o ".\{6\}$")
sudo mkdir -p /mnt/fsx/share/${job_name}
threads=16
file_size=1024
file_count=1024
sudo python ~/smallfile/smallfile_cli.py \
--operation create \
--threads ${threads} \
--file-size ${file_size} \
--files ${file_count} \
--same-dir N \
--dirs-per-dir ${file_count} \
--hash-into-dirs Y \
--files-per-dir ${file_count} \
--prefix $(echo $(uuidgen)| grep -o ".\{6\}$") \
--top /mnt/fsx/share/${job_name} &


```





- If you adjust the share permissions from the **Windows Server 2016 - FSx Workshop** instance, can you get

- Open **File Explorer**
- Context-click **This PC** and click **Map network drive...**
- Map the file share using the following information, 

| Configuraiton detail | Value 
| :--- | :--- 
| Drive | Z:
| Folder | UNC path of the file system's default file share using the DNS name you copied above - **\\\\<file system's DNS name>\share** - (e.g. **\\\\fs-0123456789abcdef.example.com\share**)
| Reconnect at sign-in | Leave **checked**
| Connect using different credentials | Leave **unchecked**

### Step 3.3: Access a file share

> Complete the following steps logged on to the **Windows Server 2016 - FSx Workshop** instance

- In the **File Explorer** window of the **Z:**
- Create new empty files on the **Z:** drive
- Context-click >> **New** >> **Text Document**
- Create a few different types of files

### Step 3.3: Test the performance of the new file share

> Complete the following steps logged on to the **Windows Server 2016 - FSx Workshop** instance

- Open a **PowerShell** window as an **Administrator**
- Install DiskSpeed using the script below. Copy >> Paste >> Execute the script in the PowerShell window

```sh
$path = "C:\Tools\DiskSpd-2.0.21a"
$url = "https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62/file/199535/2/DiskSpd-2.0.21a.zip"
$destination = "C:\Tools\DiskSpd-2.0.21a.zip"
$download = New-Object -Typename System.Net.WebClient
New-Item -Type Directory -Path $path
$download.DownloadFile($url,$destination)

$extract = New-Object -ComObject Shell.Application
$files = $extract.Namespace($destination).Items()
$extract.NameSpace($path).CopyHere($files)

```

- Open a new **PowerShell** window **NOT** as **Administrator**
- Run the DiskSpeed script below to test write performance of the mapped **Z:** drive

```sh
C:\Tools\DiskSpd-2.0.21a\amd64\DiskSpd.exe -b16K -c4G -o4 -t8 -w25 -r -L -d30 -Z1G Z:\${env:computername}.dat
```

- While the script is running, open **Task Explorer** and monitor network performance (e.g. Task Explorer >> Performance (tab) >> Ethernet)

- What was the peak write throughput you achieved?
- What was the peak read throughput you achieved?
- What was the P99 (99th %-tile) of your test?


- Experiment with different DiskSpd parameter settings. Use the table below was a guide. Test with different block sizes (-b), file sizes (-c), number of outstanding I/O requests (-o), number of threads per file (-t), and read/write ratio (-w).

| Parameter | Description 
| :--- | :--- 
| `-b<size>[K\|M\|G]` | Block size in bytes or KiB, MiB, or GiB (default = 64K). |
| `-c<size>[K\|M\|G\|b]` | Create files of the specified size. Size can be stated in bytes or KiBs, MiBs, GiBs, or blocks. |
| `-o<count>` | Number of outstanding I/O requests per-target per-thread. (1 = synchronous I/O, unless more than one thread is specified with by using `-F`.) (default = 2) |
| `-t<count>` | Number of threads per target. Conflicts with `-F`, which specifies the total number of threads. |
| `-w<percentage>` | Percentage of write requests to issue (default = 0, 100% read). The following are equivalent and result in a 100% read-only workload: omitting `-w`, specifying `-w` with no percentage and `-w0`. **CAUTION**: A write test will destroy existing data without issuing a warning. |

- What different parameters did you test?
- How did the different parameter options alter the results?

---
## Next section
### Click on the link below to go to the next section

| [**Create new shares**](../4-creat-new-shares) |
| :---
---

For feedback, suggestions, or corrections, please email me at [darrylo@amazon.com](mailto:darrylo@amazon.com).

## License

This library is licensed under the Amazon Software License.

