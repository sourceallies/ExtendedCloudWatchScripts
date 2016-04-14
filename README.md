# ExtendedCloudWatchScripts

Extension to Amazon Cloud Watch Scripts that adds logical volume metrics found here: [http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/mon-scripts.html](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/mon-scripts.html)

## Features
This addresses the issue of not being able to create metrics for Logical Volumes.
Using these scripts you now gain:

* `lv-space-util` [Shows percentage free space in a Logical Volume]
* `lv-space-used` [Shows gigabytes used space in a Logical Volume]
* `lv-space-avail` [Shows gigabytes free space in a Logical Volume]

Which can be used to set up metrics and alarms in CloudWatch.

## Usage example
This could be used with the [Amazon ECS Optimized AMI](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs-optimized_AMI.html) by running the following scripts. It could be added to the User Data in an AWS EC2 Launch Configuration to make sure it is performed on all instances.
```
#!/bin/bash
yum -y install perl-Switch perl-DateTime perl-Sys-Syslog perl-LWP-Protocol-https perl-Digest-SHA.x86_64
curl -L https://github.com/alexanderbh/ExtendedCloudWatchScripts/archive/1.0.0.tar.gz -O
tar -zxvf 1.0.0.tar.gz -C /
(crontab -l ; echo "*/5 * * * * /ExtendedCloudWatchScripts-1.0.0/mon-put-instance-data.pl --lv-space-util --lv-space-avail --lv-space-used --auto-scaling --from-cron")| crontab -
```

This will install the required perl tools, download the extended scripts and extract them, and lastly add the scripts to crontab to run every 5 minutes.

This requires the EC2 instance to have an IAM role with at least the following permissions
* cloudwatch:PutMetricData
* cloudwatch:GetMetricStatistics
* cloudwatch:ListMetrics
* ec2:DescribeTags

If not you will have to provide the AWS credentials to the scripts as per the original guide linked above.

## Note
* These scripts does not currently check if the Logical Volume can grow inside the Logical Group, hence it might show less space free than there actually is available to the volume if it's expanded in the Logical Group.
* These metrics requires the script to be run by root or a user with `lvdisplay` permissions.
 

## License
Licensed under the Apache License, Version 2.0

Copyright 2016 Alexander Hansen
