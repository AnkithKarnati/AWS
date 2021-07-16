# How to Unmount EBS volume of EC2 Linux Instance
Hi All,
 
In this blog will explain how we can unmount volume in Linux Instance

I am assuming that you have a running Linux EC2 instance on AWS  we want to unmount particular volume in our Linux EC2 instance.

Then login to EC2 instance with root privileges 

# Follow below commands
To check volumes
```
df -h
```
To list all the block devices in the Linux machine
```
lsblk
```
Run cmd to unmount the extra volume
```
unmount /dev/xvdf 
```
Then go to the EC2 Service under volumes select the extra volume and detach that volume that’s it done.

check again whether it is detach or not in Linux machine by running cmd
```
lsblk
```

# Happy Learning
