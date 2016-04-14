# ExtendedCloudWatchScripts

Extension to Amazon Cloud Watch Scripts that adds logical volume metrics.

Adds the following metrics:
* lv-space-util
* lv-space-used
* lv-space-avail

NOTE: These metrics requires the script to be run by root or a user with lvdisplay permissions.
