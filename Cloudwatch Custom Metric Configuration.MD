Install Cloudwatch unified agent on EC2 instance

1)  Create required IAM role with **CloudWatchAgentServerPolicy**.

2) Launch an EC2 instance and associate the created policy.

3) Login to the instance

4) Find the required cloudwatch agent download link:

https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/download-cloudwatch-agent-commandline.html

5) Download the Cloudwatch Unified Agent. Find the right agent link for your OS by visiiting the above link
```console
wget https://s3.amazonaws.com/amazoncloudwatch-agent/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm
```


6) Install the Cloudwatch Agent
```console
sudo rpm -U ./amazon-cloudwatch-agent.rpm
```

7) Configure the Cloudwatch agent with the help of a setup wizard:

```console
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
```

Choose all the default option except don't install statd and collectd. Selecy **YES** when asked to collect Memory Utilization metric.  Select **NO** when asked if you want to monitor log files.

8) Start the agent


```console
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
```

9) We have configured the cloudwatch metrics now.
