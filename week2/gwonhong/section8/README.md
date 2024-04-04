# section8: RDS + Aurora + ElastiCache

## RDS

![1](images/1.jpg)

- Relational Database Service
- managed DB service for SQL DB
- allows you to create databases in the cloud that are managed by AWS
  - Postgres
  - MySQL
  - MariaDB
  - Oracle
  - MS SQL Server
  - IBM DB2
  - Aurora (AWS Proprietary db)

### Advantages over EC2

- managed service:
  - automated provisioning, OS patching
  - continuous backup & restore
  - monitoring dashboards
  - read replicas for improved read performance
  - multi AZ setup for Disaster Recovery
  - maintenance windows for upgrades -> ?
  - scaling capability (vertical & horizontal)
  - storage backed by EBS (gp2 or io1)
- but, you can't SSH into your instances

### Storage Auto Scaling

- when RDS detects not enough free db stroage, it scales automatically
- no need of manual scaling
- you have to set Maximum Storage Threshold
- automatically modify storage if:
  - free storage < 10%
  - low-storage lasts at least 5 minutes
  - 6 hours passed since last modification
- useful for applications with *unpredictable workloads*
