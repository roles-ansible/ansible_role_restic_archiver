 ansible_role_restic_archiver
======================

ansible role to "archive" restic backups.

The scenario for this role is:
- You have the restic rest server running in write-only mode
- you send backups from other servers to your restic backup server

Now you don't want to store all backups indefinitely, but only for the last days a daily backup and otherwise weekly, monthly, yearly a few... just like you do it.

Of course you don't want to give access to others, so you solve the whole thing with a local cronjob. And this cronjob is built with this Ansible role.

As a bonus feature, you can optionally transfer the backups to another disk (even with a different password). Which is also a very charming backup concept from a security point of view.

this role does not install restic. For that, we recommend [this ansible role](https://github.com/arillso/ansible.restic.git).
We have had good experience with this role for the [restic rest server](https://github.com/donat-b/ansible-restic-rest.git).

 Variables:
---------
```yml
---
# which repos should we cleanup by default
restic_archiver__repos: {}
#  - name: example_server:
#    location: /srv/restic/example_server_repo
#    password: securepassword4eXaMpleSserver
#  - name: other_server
#    location: /srv/restic/other_server_repo
#    password: xtrasecuredifferentpassword4other
#    archive: true
#    archive_location: /mnt/archive/other_server_repo
#    archive_password: archive4other_server_password
#    archive_cleanup: true
#    keep_last: 5
#    keep_hourly: 4
#    keep_daily: 1
#    keep_weekly: 1
#    keep_monthly: 1
#    keep_yearly: 1
#    keep_within: 1

# how long should we store all backups by default
restic_archiver__keep: 9
restic_archiver__keep_hourly: 28
restic_archiver__keep_daily: 26
restic_archiver__keep_weekly: 8
restic_archiver__keep_monthly: 13
restic_archiver__keep_yearly: 12

# owner and user of all restic stuff
restic_archiver__owner: 'root'
restic_archiver__group: 'root'

# shedule restic cronjob
restic_archiver__hour: '3'
restic_archiver__minute: '32'

# validate if disk is mounted
restic_archiver__mount_required: false
# which disk have to be mounted
restic_archiver__mount_disk: '/mnt/'
# umount after use?
restic_archiver__umount_after_usage: false

# required packages
restic_archiver__package:
  - cron

# version check for this playbook (true is recomended)
submodules_versioncheck: false
```

