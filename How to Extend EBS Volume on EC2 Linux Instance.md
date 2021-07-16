# How to Extend Root Volume of EC2 Linux Instance
Hi All,
 
In this blog will explain how to extend EBS volume in EC2 Linux instance

I am assuming that you have created an ec2 Linux instance with root volume of (X amount of GB) and it is in running state. 

Now you want to increase the root volume of your Instance 

Go to EC2 service and select EBS volumes click on the EBS volume and modify the volume with extra Y amount of GB and modify it.

Then login to EC2 instance with root privileges

# Follow below commands

To check volumes
```
df -h
```
To check which type of filesystem whether it is xfs or ext4
```
cat /etc/fstab
```
For XFS filesystem use the cmd to increase volume 
```
xfs_growfs -d /volume1
```
For ext4 filesystem use the cmd to increase volume 
```
resize2fs /volume1
```
To check volumes
```
df -h
```
