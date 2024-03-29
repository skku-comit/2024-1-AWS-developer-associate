# Section 8. RDS + Aurora + ElastiCache

## RDS (Relational Database Service)

- **Managed database service** for DBs like MySQL, PostgreSQL, Oracle, SQL Server, etc.
- **Automated backups**, **software patching**, **scaling**, **replication**, etc.
- **Storage Auto-scaling**: Automatically scales storage capacity.

## RDS Read Replicas for Read Scalability

- Read-only copies of the master DB.
- **Asynchronous replication**: Data is copied from the master DB to the read replicas.
- Free for same region / charged for cross-region.
- Different from Multi-AZ (Disaster Recovery).
  - Multi-AZ: Synchronous replication for failover.
  - Read Replicas: Asynchronous replication for read scalability.
    ![RDS Multi AZ](./images/rds-multi-az.png)

## Aurora

- **MySQL** and **PostgreSQL**-compatible.
- **5x performance** of MySQL, 3x of PostgreSQL.
- **Automatic failover** and **high availability** and **read scaling**.
- 1 primary instance and 15 read replicas.
- Cross-region replication.

## RDS & Aurora Security

- **At-rest encryption**: Encrypts data using KMS.
- **Inflight encryption**: SSL certificates to encrypt data to and from the DB.
- **IAM Authentication**: Authenticate using IAM user / role.
- **Security Groups**: Control inbound and outbound traffic to the DB.
- **No SSH access** to the DB.

## RDS Proxy

- To pool and share DB connections established with the database.
- Improve database efficiency by reducing database load.
- Serverless, auto-scaling, and highly available.
- Enforce IAM Authentication for DB connections and securely store credentials in Secrets Manager.
- RDS Proxy is only accessible within the VPC.
  ![RDS Proxy](./images/rds-proxy.png)
