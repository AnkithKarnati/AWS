# Install Cloudwatch unified agent on EC2 instance. To Gather Custom Metrics of Memory Utlilization using Amazon Linux AMI
Hi All,

In this Blog i will explain how to install Cloudwatch agent on EC2 instance. Gather Custom Metrics using Amazon Linux AMI
First We need to create required IAM role for the EC2 instances to be able to send metrics information to cloudwatch.

In policies while creating IAM Role for EC2 Instance, Select the **CloudWatchAgentServerPolicy**.

I am assuming that you have created an ec2 Linux instance and it is in running state.

SSH into the instance

Find the cloudwatch agent download link here: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/download-cloudwatch-agent-commandline.html

Download the Cloudwatch Unified Agent. Find the right agent link for your OS by visiiting the above link

```
wget https://s3.amazonaws.com/amazoncloudwatch-agent/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm
```
Install the Cloudwatch Agent

```
sudo rpm -U ./amazon-cloudwatch-agent.rpm
```

Configure the Cloudwatch agent with the help of a setup wizard:

```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
```

Choose all the default option except don't install statd and collectd. Select YES when asked to collect Memory Utilization metric. 

Select NO when asked if you want to monitor log files.

Start the agent

```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
```

You should be set! We'll explore the collected metrics now.

View the collected cloudwatch custom metrics

we configured the cloudwatch Unified agent. 

Now let's look at the metrics collected by the agent.

Remember: RAM/Memory metrics are not collected by Cloudwatch by default. 

Cloudwatch agent enables us to collect those metrics not collected by default.

In the config wizard we selected to collect Metrics like Ram etc.

Congratulations! you just collected and graphed EC2 Custom metrics using the Cloudwatch Unified Agent
