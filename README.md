# AWS-Solution-Architecture
# MENU
## EBS
1. run: `lsblk`\
**`Assumming that it showed as below: `**\
`NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT`\
`xvda    202:0    0   8G  0 disk\`\
`└─xvda1 202:1    0   8G  0 part /`\
`xvdf    202:80   0   1G  0 disk `\
`xvdm    202:192  0   2G  0 disk `\
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
