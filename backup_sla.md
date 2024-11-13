# Backup SLA

## Coverage

We back up services that satisfy at least one of these criteria:
 - are primary source of truth for particular data
 - contain customer and/or client data
 - are not feasible (or very costly) to restore by other means

Services that are backed up:
 - Ansible Git Repository
 - MySQL
 - InfluxDB


## Schedule

Ansible Git Repository backups are created every 24h; it takes up to 1 min to create and store the backup.

MySQL backups are created every 24h; it takes up to 1 min to create and store the backup.

InfluxDB backups are created every 24h; it takes up to 1 min to create and store the backup.

All backups are started automatically by 01:00 UTC+2.

Backup RPO (recovery point objective) is:
 - 24h for MySQL
 - 24h for InfluxDB
 - 24h for Ansible Git Repository


## Storage

MySQL and InfluxDB backups are uploaded to the backup server.

Ansible Git Repository is mirrored to the internal Git server.

Backup data from both servers will be synchronized to encrypted AWS S3 bucket in future (work in progress).


## Retention

Ansible Git Repository backups are stored for 30 days; all versions (recovery points) are available to restore.

InfluxDB backups are stored for 30 days; 29 versions are available to restore.

MySQL backups are stored for 30 days; 29 versions are available to restore.


## Usability checks

MySQL backups are verified every sunday by Innar Viinamäe.

InfluxDB backups are verified every sunday by Innar Viinamäe.

_____ backups are verified every _____ by _____.


## Restore process

Service is recovered from the backup in case of an incident, and when service cannot be restored in any other way.

RTO (recovery time objective) is:
 - 5 min for MySQL
 - 5 min for InfluxDB
 - _____ for _____

Detailed backup restore procedure is documented in the [backup_restore.md](./backup_restore.md).