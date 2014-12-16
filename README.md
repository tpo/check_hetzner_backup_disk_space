check_hetzner_backup_disk_space
===============================

This is a check for Nagios/Icinga to report back remaining (free) disk space on the backup service that Hetzner is providing.

It assumes that there's a /usr/local/bin/backup-df script, which executes the actual 'df' on Hetzner's backup server. The path of the backup-df script can be changed, by changing the respective line in the check_backup_df script.

The actual checking is separated from the check_ script, to keep privileges split:

 - the check_script is running as the user 'nagios' and doesn't require much rights
 - in contrast the backup-df script is usually running as root, because it needs access to the ssh keys that are required to access the Hetzner backup server since these are the same keys, that are used to do the backup, and the backup is usually done as root.
 
You'll need to allow the check_script to run backup-df via sudo. From the /etc/sudoers file:

    nagios ALL=NOPASSWD: /usr/local/bin/backup-df -h

The check thresholds can be configured:

    $ ./check_backup_df --help
    Usage: ./check_backup_df -w warn -c crit
    
      'warn' and 'crit' are integers between 0 and 100 (percent)
    
      check free disk space on Hetzner backup
    
      Example: ./check_backup_df -w 20 -c 5


Made for Sourcepole.com by Tomáš Pospíšek <tpo_deb@sourcepole.ch>
