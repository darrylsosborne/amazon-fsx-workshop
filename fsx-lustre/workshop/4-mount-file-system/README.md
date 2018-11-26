![](https://s3.amazonaws.com/aws-us-east-1/tutorial/AWS_logo_PMS_300x180.png)

![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_available.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_ingergration.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_ecryption-lock.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_fully-managed.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_lowcost-affordable.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_performance.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_scalable.png)![](https://s3.amazonaws.com/aws-us-east-1/tutorial/100x100_benefit_storage.png)

# **Amazon FSx for Lustre**

## Mount file system

### Version 2018.11

fsx.l.wrkshp.2018.11

---

© 2018 Amazon Web Services, Inc. and its affiliates. All rights reserved. This work may not be  reproduced or redistributed, in whole or in part, without prior written permission from Amazon Web Services, Inc. Commercial copying, lending, or selling is prohibited.

Errors or corrections? Email us at [darrylo@amazon.com](mailto:darrylo@amazon.com).

---

### Mount file system

You must first complete [**Prerequisites**](../0-prerequisites) and the previous step [**Launch clients**](../3-launch_clients).

You must wait for the file system you created in section 1 **Create file system** to have a **Lifecycle** of **Available**. You can verify the file system's lifecycle or status by viewing the status using FSx Console or the lifecycle using the CLI command below, substituting the appropriate region parameter based on your environment.

```sh
aws fsx describe-file-systems --output json --region <region>
```

WARNING!! This workshop environment will exceed your free-usage tier. You will incur charges as a result of building this environment and completing the steps below.

### Step 4.1: Log on to the Linux EC2 instance

- From the Amazon EC2 Console, select the **Lustre client - FSx Workshop** instance
- Click **Connect**
- Use the connection information to SSH to the instance using your laptop's terminal application

### Step 4.2: Install linux applications

> Complete the following steps SSH'd in to the **Lustre client - FSx Workshop** instance

- Run the following script

```sh
# update
sudo yum update -y

# install utilities
sudo yum install -y tree git wget
sudo yum install -y --enablerepo=epel nload ioping

# install parallel
(wget -O - pi.dk/3 || curl pi.dk/3/ || fetch -o - http://pi.dk/3) | bash

# install smallfile
git clone https://github.com/bengland2/smallfile.git

# install fio
sudo yum groupinstall -y "Development Tools"
sudo yum install -y libaio-devel
git clone git://git.kernel.dk/fio.git
cd fio
./configure
make
sudo make install
cd

# install ior
sudo yum groupinstall -y "Development Tools"
sudo yum install -y openmpi openmpi-devel
git clone https://github.com/hpc/ior.git
export PATH=$PATH:/usr/lib64/openmpi/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib64/openmpi/lib/
cd ior
./bootstrap
./configure
make
sudo cp src/ior /usr/local/bin
cd

```

### Step 4.3: Verify applications were installed correctly

> Complete the following steps SSH'd in to the **Lustre client - FSx Workshop** instance

#### Verify parallel

- Run the following command

```sh
parallel --will-cite --version
```

- The output should be similar to this:

```sh
GNU parallel 20160722
Copyright (C) 2007,2008,2009,2010,2011,2012,2013,2014,2015,2016
Ole Tange and Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
GNU parallel comes with no warranty.

Web site: http://www.gnu.org/software/parallel

When using programs that use GNU Parallel to process data for publication
please cite as described in 'parallel --citation'.
```

#### Verify smallfile

- Run the following command

```sh
python ~/smallfile/smallfile_cli.py
```

- The output should be similar to this:


```sh
                                 version : 3.1
                           hosts in test : None
                   top test directory(s) : ['/var/tmp/smf']
                               operation : cleanup
                            files/thread : 200
                                 threads : 2
           record size (KB, 0 = maximum) : 0
                          file size (KB) : 64
                  file size distribution : fixed
                           files per dir : 100
                            dirs per dir : 10
              threads share directories? : N
                         filename prefix :
                         filename suffix :
             hash file number into dir.? : N
                     fsync after modify? : N
          pause between files (microsec) : 0
             minimum directories per sec : 50
                    finish all requests? : Y
                              stonewall? : Y
                 measure response times? : N
                            verify read? : Y
                                verbose? : False
                          log to stderr? : False
                           ext.attr.size : 0
                          ext.attr.count : 0
host = ip-172-31-21-162,thr = 00,elapsed = 0.604281,files = 200,records = 0,status = ok
host = ip-172-31-21-162,thr = 01,elapsed = 0.604252,files = 200,records = 0,status = ok
total threads = 2
total files = 400
total IOPS = 0
100.00% of requested files processed, minimum is  70.00
elapsed time =     0.604
files/sec = 661.943755
```

#### Verify fio

- Run the following command

```sh
fio --version
```
- The output should be similar to this:

```sh
fio-3.12-19-g41dd
```


#### Verify ior

- Run the following command

```sh
ior
```

- The output should be similar to this:

```sh
IOR-3.2.0: MPI Coordinated Test of Parallel I/O
Began               : Mon Nov 19 02:02:51 2018
Command line        : ior
Machine             : Linux ip-172-31-21-162
TestID              : 0
StartTime           : Mon Nov 19 02:02:51 2018
Path                : /home/ec2-user
FS                  : 7.7 GiB   Used FS: 23.8%   Inodes: 0.5 Mi   Used Inodes: 13.6%

Options:
api                 : POSIX
apiVersion          :
test filename       : testFile
access              : single-shared-file
type                : independent
segments            : 1
ordering in a file  : sequential
ordering inter file : no tasks offsets
tasks               : 1
clients per node    : 1
repetitions         : 1
xfersize            : 262144 bytes
blocksize           : 1 MiB
aggregate filesize  : 1 MiB

Results:

access    bw(MiB/s)  block(KiB) xfer(KiB)  open(s)    wr/rd(s)   close(s)   total(s)   iter
------    ---------  ---------- ---------  --------   --------   --------   --------   ----
write     2004.51    1024.00    256.00     0.000014   0.000483   0.000002   0.000499   0
read      13588      1024.00    256.00     0.000002   0.000070   0.000001   0.000074   0
remove    -          -          -          -          -          -          0.000136   0
Max Write: 2004.51 MiB/sec (2101.88 MB/sec)
Max Read:  13587.69 MiB/sec (14247.73 MB/sec)

Summary of all tests:
Operation   Max(MiB)   Min(MiB)  Mean(MiB)     StdDev   Max(OPs)   Min(OPs)  Mean(OPs)     StdDev    Mean(s) Test# #Tasks tPN reps fPP reord reordoff reordrand seed segcnt   blksiz    xsize aggs(MiB)   API RefNum
write        2004.51    2004.51    2004.51       0.00    8018.02    8018.02    8018.02       0.00    0.00050     0      1   1    1   0     0        1         0    0      1  1048576   262144       1.0 POSIX      0
read        13587.69   13587.69   13587.69       0.00   54350.78   54350.78   54350.78       0.00    0.00007     0      1   1    1   0     0        1         0    0      1  1048576   262144       1.0 POSIX      0
Finished            : Mon Nov 19 02:02:51 2018
```



### Step 4.4: Install Lustre client

> Complete the following steps SSH'd in to the **Amazon Linux - FSx Workshop** instance

- There are separate instructions for each Linux distribution. Following the appropriate instructions based on the Linux distribution you used to launch the EC2 instance in the previous section.





### Step 4.5: Mount the file system

> Complete the following steps SSH'd in to the **Amazon Linux - FSx Workshop** instance

- Run the following script to create a local mount point and mount the file system

- Replace <file-system-dns-name> and <region> with values specific to your environment. You can find the file system's DNS name by viewing it on the **Network & Security** tab of the FSx Console or using the CLI command below, substituting the appropriate <region> parameter based on your environment.


```sh
aws fsx describe-file-systems --output json --region <region>
```

```sh
sudo mkdir -p /mnt/fsx
# for example: sudo mount -t cifs //fs-0123456789abcdef.example.com/share /mnt/fsx/share --verbose -o vers=2.0,user=admin@example.com
sudo mount -t lustre <file-system-dns-name>@tcp:/fsx /mnt/fsx
```

- Run **df** to verify mount

```sh
df
```

### Step 4.6: Examine the file system's metadata loaded from the linked S3 bucket






time find /mnt/fsx/*.las -type f | parallel --will-cite -j ${threads} sudo lfs hsm_restore {} &

time lfs find /mnt/fsx --type f --name *.nc | parallel --will-cite -j ${threads} sudo lfs hsm_restore {} &


time lfs find /mnt/fsx --type f --name *.nc | wc -l


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


- Run the **smallfile** test below to write a large number of small files

```sh
job_name=$(echo $(uuidgen)| grep -o ".\{6\}$")
prefix=$(echo $(uuidgen)| grep -o ".\{6\}$")
path=/mnt/fsx/share/${job_name}
sudo mkdir -p ${path}

threads=16
file_size=1024
file_count=1024
operation=create
same_dir=N

sudo python ~/smallfile/smallfile_cli.py \
--operation ${operation} \
--threads ${threads} \
--file-size ${file_size} \
--files ${file_count} \
--same-dir ${same_dir} \
--hash-into-dirs Y \
--prefix ${prefix} \
--dirs-per-dir ${file_count} \
--files-per-dir ${file_count} \
--top ${path} &

```

- While the script above is running, press the return/enter key a few times to return a prompt. Run the **nload** command below for 30-40 seconds to monitor network throughput in real time.
- Exit **nload** by pressing **Control+z**
- How long did it take to generate 32 GiB of data across 16 threads?
- What was the average throughput of this test?


- Run the **smallfile** test below to read the files generated above

```sh
operation=read

sudo python ~/smallfile/smallfile_cli.py \
--operation ${operation} \
--threads ${threads} \
--file-size ${file_size} \
--files ${file_count} \
--same-dir ${same_dir} \
--hash-into-dirs Y \
--prefix ${prefix} \
--dirs-per-dir ${file_count} \
--files-per-dir ${file_count} \
--top ${path} &
```

- Run the **smallfile** test below to stat the files generated above

```sh
operation=stat

sudo python ~/smallfile/smallfile_cli.py \
--operation ${operation} \
--threads ${threads} \
--file-size ${file_size} \
--files ${file_count} \
--same-dir ${same_dir} \
--hash-into-dirs Y \
--prefix ${prefix} \
--dirs-per-dir ${file_count} \
--files-per-dir ${file_count} \
--top ${path} &
```

- Run the **smallfile** test below to append to the files generated above

```sh
operation=append
file_size=128

sudo python ~/smallfile/smallfile_cli.py \
--operation ${operation} \
--threads ${threads} \
--file-size ${file_size} \
--files ${file_count} \
--same-dir ${same_dir} \
--hash-into-dirs Y \
--prefix ${prefix} \
--dirs-per-dir ${file_count} \
--files-per-dir ${file_count} \
--top ${path} &
```

- Run the **smallfile** test below to rename to the files generated above

```sh
operation=rename

sudo python ~/smallfile/smallfile_cli.py \
--operation ${operation} \
--threads ${threads} \
--file-size ${file_size} \
--files ${file_count} \
--same-dir ${same_dir} \
--hash-into-dirs Y \
--prefix ${prefix} \
--dirs-per-dir ${file_count} \
--files-per-dir ${file_count} \
--top ${path} &
```

- Run the **smallfile** test below to rename to the files generated above

```sh
operation=delete-renamed

sudo python ~/smallfile/smallfile_cli.py \
--operation ${operation} \
--threads ${threads} \
--file-size ${file_size} \
--files ${file_count} \
--same-dir ${same_dir} \
--hash-into-dirs Y \
--prefix ${prefix} \
--dirs-per-dir ${file_count} \
--files-per-dir ${file_count} \
--top ${path} &
```


---
## Next section
### Click on the link below to go to the next section

| [**Restore backup**](../7-restore-backup) |
| :---
---

For feedback, suggestions, or corrections, please email me at [darrylo@amazon.com](mailto:darrylo@amazon.com).

## License

This library is licensed under the Amazon Software License.

