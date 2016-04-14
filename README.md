# ExtendedCloudWatchScripts

Extension to Amazon Cloud Watch Scripts that adds logical volume metrics found here: [http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/mon-scripts.html](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/mon-scripts.html)

This addresses the issue of not being able to create metrics for Logical Volumes.
Using these scripts you now gain:

* `lv-space-util` [Shows percentage free space in a Logical Volume]
* `lv-space-used` [Shows gigabytes used space in a Logical Volume]
* `lv-space-avail` [Shows gigabytes free space in a Logical Volume]

Which can be used to set up metrics and alarms in CloudWatch.

Note:
* These scripts does not currently check if the Logical Volume can grow inside the Logical Group, hence it might show less space free than there actually is available to the volume if it's expanded in the Logical Group.
* These metrics requires the script to be run by root or a user with `lvdisplay` permissions.
