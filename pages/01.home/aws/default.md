---
title: AWS
---

[TOC]

## Tooling

- [awless](https://github.com/wallix/awless)
- [bash-my-aws](https://github.com/bash-my-aws/bash-my-aws)
- [commandeer](https://getcommandeer.com/)

## RDS instance

```
# create snapshot
aws rds create-db-snapshot --db-instance-identifier <INSTANCE_IDENTIFIER> --db-snapshot-identifier <SNAPSHOT_IDENTIFIER>
# verify snapshot
aws rds describe-db-snapshots --db-snapshot-identifier <SNAPSHOT_IDENTIFIER>
# create encrypted snapshot by copying
aws rds copy-db-snapshot --source-db-snapshot-identifier <SNAPSHOT_IDENTIFIER> --target-db-snapshot-identifier <ENCRYPTED_SNAPSHOT_IDENTIFIER> --kms-key-id <KEY_ID>
# delete instance
aws rds delete-db-instance --db-instance-identifier <INSTANCE_IDENTIFIER> --skip-final-snapshot --no-delete-automated-backup
```

## AMI

```
# create 
aws ec2 create-image --no-reboot --instance-id <INSTANCE_ID> --name "FOO" --description "BAR"
# verify
aws ec2 describe-images --image-ids <AMI_ID>
```

## Volumes

```
# stop instance
# for ASG change min=0 desired=0 and set instance to standby
aws ec2 stop-instances --instance-ids <INSTANCE_ID>
# detach volume from instance
aws ec2 detach-volume --volume-id <VOLUME_ID>
# create snapshot
aws ec2 create-snapshot --volume-id <VOLUME_ID> --description "FOO"
# verify vol
aws ec2 describe-snapshots --snapshot-ids <SNAPSHOT_ID>
# create encrypted vol
aws ec2 create-volume --snapshot-id <SNAPSHOT_ID> --volume-type gp2 --encrypted --availability-zone us-east-1a
# reattach vol
aws ec2 attach-volume --volume-id <NEW_SNAPSHOT_ID>--instance-id <INSTANCE_ID> --device /dev/sda1
```