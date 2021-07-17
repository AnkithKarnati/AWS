# How to Mount S3 Bucket on EC2 Linux Instance Using IAM Role
Hi All,
 
In this blog will explain how we can mount s3 bucket as a mount point to Linux Instance

I am assuming that you have a running Linux EC2 instance on AWS and also you created s3 bucket in AWS which we can mount on our Linux EC2 instance.

Then login to EC2 instance with root privileges

# The following steps you need to perform on Linux EC2 Instance to mount s3bucket

Step 1: Create IAM Role in AWS with S3 permissions (Full Access)

Step 2:  Attach that IAM role to the EC2 Linux Machine in AWS
Step 3: We need to install required dependencies packages on system by using below following commands
```
yum install automake fuse fuse-devel gcc-c++ git libcurl-devel libxml2-devel make openssl-devel
```
Step 4: We need to take Clone s3fs code from GitHub
```
git clone https://github.com/s3fs-fuse/s3fs-fuse.git
```
Step 5: we need to run the code in our system 
```
cd s3fs-fuse

./autogen.sh

./configure --prefix=/usr --with-openssl

make

make install
```
Step 6:  To check whether s3fs is configured or not we need run below command
```
which s3fs
```
Step 7: Now create a directory or provide the path of an existing directory and mount S3bucket in it.
```
mkdir /demobucket
```
Step 8:We need to Add the below entry in fstab
```
vi  /etc/fstab
```
```
s3fs#yourbucketname /demobucket fuse _netdev,allow_other,uid=1002,gid=1002,iam_role=your-iam-role,use_cache=/tmp,url=https://s3.ap-south-1.amazonaws.com 0 0
```
```
mount -a
```
Step 9: Now it will mount this bucket as a directory to check that you can use the below command
```
df -h
```
Hope you have mounted the s3Bucket on your Linux ec2 Instance

#### Happy Learning
