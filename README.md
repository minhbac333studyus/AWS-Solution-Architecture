# AWS-Solution-Architecture
## Contents
- [EC2](#ec2)
- [EBS](#ebs)
- [S3](#s3)

1.Install FileZilla Client\
2.Go to Edit/Settings/ choose SFTP and set the private key from AWS for the instance EC2\
3.Go to File/Site Manager

## Intall Java on Amazon Linux 2 by  Wget Command
`get --no-check-certificate -c --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/11.0.2+9/f51449fcd52f4d52b93a989c5c56ed3c/jdk-11.0.2_linux-x64_bin.rpm`\


## Install Java on Amazon Linux 2 by SUDO COMMAND
Step 1 – Install Java on Amazon Linux
The OpenJDK 8 is available under default yum repositories and OpenJDK 11 is available under Amazon Linux 2 extras repositories. You can simply install Java 11 or Java 8 on the Amazon Linux system using the following commands.

Run below commands to install Java 11 on Amazon Linux:\
`
sudo amazon-linux-extras install java-openjdk11
`\
Run below commands to install Java 8 on Amazon Linux:\
`
sudo yum install java-1.8.0-openjdk
`\
Step 2 – Check Active Java Version\
After successfully installing Java on Amazon Linux using the above steps, Let’s verify the installed version using the following command.\

java -version

`openjdk version "1.8.0_222"`\
`OpenJDK Runtime Environment (build 1.8.0_222-8u222-b10-1ubuntu1~18.04.1-b10)`\
`OpenJDK 64-Bit Server VM (build 25.222-b10, mixed mode)`\
Step 3 – Switch Java Version
Use alternatives command-line utility to switch active Java version on your Amazon Linux system. Run below command from the command line and select the appropriate Java version to make it default.\
`
alternatives --config java
`\
Install Java on Amazon Linux

After switching let’s check again active Java version:\
 
`java -version`\
`openjdk version "11.0.7" 2020-04-14 LTS`\
`OpenJDK Runtime Environment 18.9 (build 11.0.7+10-LTS)`\
`OpenJDK 64-Bit Server VM 18.9 (build 11.0.7+10-LTS, mixed mode, sharing)`\

/var/www/html/index.html


## EC2
1. Convert .pem to .ppk by puttygen\
2. Get the instance ssh `ec2-18-222-55-120.us-east-2.compute.amazonaws.com`\
3. In category **Connection/Data**, type `ec2-user` in Auto-login username\  
4. In category **Connection/SSH/Auth**, choose private key file .ppk from step 1
5. Connect to server

## EBS
1. run: `lsblk`\
**`Assumming that it showed as below: `**\
`NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT`\
`xvda    202:0    0   8G  0 disk\`\
`└─xvda1 202:1    0   8G  0 part /`\
`xvdf    202:80   0   1G  0 disk `\
`xvdm    202:192  0   2G  0 disk `
2. Mount xvdf disk block to 
```
mke2fs /dev/xvdf
sudo !!
mount /dev/xvdf /yourMountFileName
```
3. Go into yourMountFileName\
```
cd yourMountFileName
vim newFile.txt
```
3.1 Type something in vim file\
`:wq` \
`mkdir Home` \
4. Move newFile.txt to Home \


## S3
Source reference: https://gsviec.com/blog/amazon-s3-la-gi-va-tai-sao-ban-nen-dung-no/
1. Create an role in **IAM** \
1.1 Give access to **AmazonS3FullAcess**\
1.2 Give a name for the role: For example: **ec2-s3-fullAccess**
1.3 **NOTE**::Make sure your instance EC2 have this IAM role


2. Go to `S3 on AWS`
3. Create a bucket then naming for it
4. Upload a file from instance EC2 to bucket by CLI - linux
```
touch demo.txt
vim demo.txt
```
Press **`i`** to edit your demo file, when you finish press **`Esc`** and type: **`:wq`**

```
cp demo.txt 
aws s3 cp demo.txt s3://adam.test.buckket/hello.txt
```
Use the following command to copy an object from Amazon S3 to your instance.

`[ec2-user ~]$` **`aws s3 cp`** **`s3://my_bucket/my_folder/my_file.ext`** **`my_copied_file.ext`**\
\
Use the following command to copy an object from your instance back into Amazon S3.
 
`[ec2-user ~]$` **`aws s3 cp`** **`my_copied_file.ext`** **`s3://my_bucket/my_folder/my_file.ext`**
 
NOTE: If we want to make our bucket be **public** then add this rule to policy
```
{
    "Version": "2008-10-17",
    "Statement": [
        {
            "Sid": "AllowPublicRead",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::your-bucket-name/*"
        }
    ]
}
```

One more example from amazon
The following example bucket policy shows the preceding policy elements.\
The policy allows Dave, a user in account Account-ID, **s3:GetObject**, **s3:GetBucketLocation**, and **s3:ListBucket** Amazon S3 permissions on the awsexamplebucket1 bucket.
```
{
    "Version": "2012-10-17",
    "Id": "ExamplePolicy01",
    "Statement": [
        {
            "Sid": "ExampleStatement01",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::123456789012:user/Dave"
            },
            "Action": [
                "s3:GetObject",
                "s3:GetBucketLocation",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::awsexamplebucket1/*",
                "arn:aws:s3:::awsexamplebucket1"
            ]
        }
    ]
}
```
