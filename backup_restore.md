Install and configure infrastructure with Ansible:

    ansible-playbook infra.yaml

Restore MySQL data from the backup:

    <On controller node>

    ssh ubuntu@193.40.156.67 -p <Port of host with MySQL master>

    <Now on managed host with MySQL master>

    sudo -i
    sudo -u backup duplicity --no-encryption restore rsync://1nnu@backup.pingix.ttu/mysql /home/backup/restore/mysql
    sudo mysql agama < /home/backup/restore/mysql/agama.sql

    <Backup should be successful, now to check>

    mysql -e 'SHOW DATABASES'

Restore InfluxDB data from the backup:

    <On controller node>

    ssh ubuntu@193.40.156.67 -p <Port of host with InfluxDB>

    <Now on managed host>

    sudo -i
    sudo -u backup duplicity --no-encryption restore rsync://1nnu@backup.pingix.ttu/influxdb /home/backup/restore/influxdb
    service telegraf stop
    influx -execute 'DROP DATABASE telegraf'
    influxd restore -portable -db telegraf /home/backup/restore/influxdb

    <Backup should be successful, now to check>
    influx -execute 'show databases'

    <Post backup restoration>
    service telegraf start
