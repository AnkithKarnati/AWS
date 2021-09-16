# How to Setup Key Base Authentication from one server to another server using SSH
Hi All,
 
In this blog will explain how can we Setup Key Base Authentication from one server to another server using SSH

I am assuming that you have a  two running Linux EC2 instance on AWS

Then login to EC2 instance with root privileges 

# In server one Follow below commands

Switch to root user go to ssh path
```
Path : cd .ssh
```
After that need to generate key by running the below cmd you can gernerate key
```
ssh-keygen -t rsa
```
After generating key you will get private key and public (id_rsa.pub, id_rsa)

You need to copy id_rsa.pub using cat cmd and copy the key.

```
cat id_rsa.pub
```
The file that ends with ‘.pub’ is your public key. This key needs to be in the computer you want to connect to (the server) inside a file called authorized_keys there you need to paste the public key.
```
vi authorized_keys
```
After saving file try to connect from server1 and access server 2 using SSH
```
ex: ssh -i id_rsa root@172.31.1.2
```

simple and secure way to manage your remote connections.

To copy files from server1 to server 2
```
scp /root/foldername/filename root@secondserverIP: /root/server-1-datafolder/
ex: scp /root/backupfile.txt root@172.31.15.161: /root/transferfile/
```

# Happy Learning
