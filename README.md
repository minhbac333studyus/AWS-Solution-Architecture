# AWS-Solution-Architecture
# MENU
## EBS
1. run: `lsblk`\
**`Assumming that it showed as below: `**\
`NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT`\
`xvda    202:0    0   8G  0 disk\`\
`└─xvda1 202:1    0   8G  0 part /`\
`xvdf    202:80   0   1G  0 disk `\
`xvdm    202:192  0   2G  0 disk `
2. Mount xvdf disk block to 
`mke2fs /dev/xvdf`\
`sudo !!`\
`mount /dev/xvdf /yourMountFileName`\
3. Go into yourMountFileName\
`cd yourMountFileName`\
`vim newFile.txt`\
3.1 Type something in vim file\
`:wq` \
`mkdir Home` \
4. Move newFile.txt to Home \


## S3
Source reference: https://gsviec.com/blog/amazon-s3-la-gi-va-tai-sao-ban-nen-dung-no/


1. Go to `S3 on AWS`
2. Create a bucket then naming for it
3. Upload a file from instance to bucket by CLI - linux
```
touch demo.txt
vim demo.txt
```
Press **`i`** to edit your demo file, when you finish press **`Esc`** and type: **`:wq`**

```
cp demo.txt 
aws s3 cp demo.txt s
```
Use the following command to copy an object from Amazon S3 to your instance.
```
[ec2-user ~]$ aws s3 cp s3://my_bucket/my_folder/my_file.ext my_copied_file.ext
```
Use the following command to copy an object from your instance back into Amazon S3.
```
[ec2-user ~]$ aws s3 cp my_copied_file.ext s3://my_bucket/my_folder/my_file.ext
```
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
            "Resource": "arn:aws:s3:::&lt;tên-bucket-của ban&gt;/*"
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
