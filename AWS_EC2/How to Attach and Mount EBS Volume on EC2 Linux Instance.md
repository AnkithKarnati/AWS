# How to Attach and Mount EBS volume to EC2 Linux 
Hi All,  

I am assuming that you have already created an EC2 Linux instance with root volume of (X GB) and it is in running state. 
Now you want to add more volume to your Instance then go to EC2 service and select EBS volumes and create a new volume. 

Example: - Create Volume

Volume Type: General purpose SSD

Size: 20GB

Availability Zone: us-east-1a

So, under EBS volumes you have created a new volume with 20GB it is in available state. that needs to be attached with your EC2 Linux instance for that right click on that selected EBS volume and attach volume to instance ID of Linux machine and then click on attach. Now state it is changed from available to in use state.

Then login to EC2 instance with root privileges 

# Follow below commands
For xfs or ext4 file system you can use same cmds by replacing ext4 or xfs filesystem type

To check volumes

```
df -h
```

To list all the block devices in the Linux machine
```
lsblk
```

If you see data as output then you need to setup the filesystem for this block device
```
file -s /dev/xvdf 
```
To make xfs filesystem then use below cmd to create a filesystem 
```
mkfs -t xfs /dev/xvdf 
```
To make ext4 filesystem then then use below cmd to to create a filesystem 
```
mkfs -t ext4 /dev/xvdf 
```
create a mount directory 
```
mkdir -p /volume
```
To mount the device to that directory
```
mount /dev/xvdf /volume 
```
To check the UUID
```
blkid
```
copy the UUID of the mount filesystem

To attach that device permanently when it reboot also you need to edit the etc/fstab file
```
vi /etc/fstab
```
Add this below line to mount permanently and save it
```
#example UUID=bc0b1xxxx-2bec-41df-56789642-1e4e82d1d512 /volume xfs defaults 0 0
```
To confirm that everything is working fine just run again below cmd 
```
mount -a
```
To check volumes
```
df -hT
```
