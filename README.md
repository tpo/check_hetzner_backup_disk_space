check-hetzner-backup-disk-space
===============================

This is a check for Nagios/Icinga to report back remaining (free) disk space on the backup service that Hetzner is providing.

It assumes that there's a /usr/local/bin/backup-df script, which executes the actual 'df' on Hetzner's backup server. The actual checking is separated from the check_ script, to keep privileges split:

 - the check_script is running as the user 'nagios' and doesn't require much rights
 - in contrast the backup-df script is usually running as root, because it needs access to the ssh keys that are required to access the Hetzner backup server since these are the same keys, that are used to do the backup, and the backup is usually done as root.
 
Made for Sourcepole.com by Tomáš Pospíšek <tpo_deb@sourcepole.ch>
