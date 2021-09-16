# How to Set Root Password in EC2 Linux Instance
Hi All,
 
In this blog will explain how we can to Set Root Password in EC2 Linux Instance

I am assuming that you have a running Linux EC2 instance on AWS

Then login to EC2 instance with root privileges 

# Follow below commands
```
passwd root
```
Enter new password and retype password
```
ex: UIJYH@iujk20
```
After setting up new password need to modify in sshd_config file.
```
Path : vi /etc/ssh/sshd_config
```
uncomment/Modify below details and save it
```
PermitRootLogin yes
PasswordAuthentication no
```
After saving need to restart the sshd service
```
systemctl restart sshd
systemctl status sshd
```

# Setup Hostname For Linux Machine

Login to EC2 instance with root privileges 

Run following cmd
```
hostnamectl set-hostname SERVERNAME
```

# Happy Learning
