# How to mount S3 bucket on EC2 Linux Instance using AWS Credentials

Hi All,
 
In this blog will explain how we can mount s3 bucket as a mount point to Linux instance

I am assuming that you have a running Linux EC2 instance on AWS and also you created s3 bucket in AWS which we can mount on our Linux EC2 instance.

Then login to EC2 instance with root privileges

# The following steps you need to perform on Linux EC2 Instance to mount s3bucket

Step 1: Create AWS IAM User in AWS with S3 permissions (Full Access)

Step 2: Download the IAM User Credentials file in your local system later will add it in EC2 Linux instance

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
Step 6: To check whether s3fs is configured or not we need run below command
```
which s3fs
```
Step 7: You need access-key and secret key for s3buket IAM user , store key details in /etc/passwd-s3fs

Create a file passwd-s3fs and save access and secret key of the user
```
vi /etc/passwd-s3fs
```
Step 8: Replace access-key-id and secret-access-key with your keys

ex: hghjhsut9t57huo45592840:jhighuahdguhugigigi!#45678ihu9
```
Your_accesskey:Your_secretkey
```
save and exit

Step 9: change permissions
```
chmod 640 /etc/passwd-s3fs
```
Step 10: Now create a directory or provide the path of an existing directory and mount S3bucket in it.
```
mkdir /demobucket
```
Step 11: Mount the bucket
```
s3fs awsbucketname /demobucket -o use_cache=/tmp -o allow_other  -o nonempty -o uid=1001 -o mp_umask=002 -o multireq_max=5 -o use_path_request_style -o url=https://s3.console.aws.amazon.com/s3/home?region=ap-south-1
```
Step 12: Now it will mount this bucket as a directory to check that you can use the below command
```
df -h
```
Step 13: when we reboot this instance it will unmount the bucket.

For this we make an entry in /etc/fstab
```
vi /etc/fstab
```
ex: awsbucketname /demobucket fuse.s3fs _netdev,allow_other 0 0
```
awsbucketname /demobucket fuse.s3fs _netdev,allow_other 0 0
```
```
mount -a
```
Step 14: To confirm
```
df -h
```
Hope you have mounted the s3Bucket on your Linux ec2 Instance

#### Happy Learning
