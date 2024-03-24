# section6

## EBS

- Elastic Block Store Volume: a network drive you can attach to your instances while they run
- allows your instances to persist data, **even after their termination**
- can be mounted to one instance at a time (also has 'multi-attach' feature)
- bound to a specific AZ
- ~= network USB stick

### EBS Volume

- network drive (not a physical drive)
    - use network to communicate the instance -> a bit of latency exists
    - can be detached and attached to another quickly (within same AZ)
- locked to an AZ
    - to move a volume across AZs, first need to snapshot it
- have provisioned capacity (in GBs, and IOPS)

### Delete on Termination attribute

- true by default for root volume (of an instance)
- false by default for new volumes

### EBS Snapshots

- make a backup of your EBS volume at a point in time
- can copy snapshots across AZ

#### Features

- EBS Snapshopt Archive
    - Move a snapshot to "archive tier": 75% cheaper
    - Takes 24-72 hours for restoring! (reason why it's cheaper)
- Recycle Bin
    - retain deleted snapshots for specific retension (from 1 day to 1 year) for recovery from accidental deletion
    - need to set rule in advance
- Fast Snapshot Restore
    - Force full initialization of snapshot to have no latency on the first use
    - expensive!

### EBS Volume Types

- 6 types: differs by size, throughput, IOPS(I/O Ops Per Sec)
- **Only gp2/gp3, io1/io2 block express can be used as boot volumes**

#### General Purpose SSD(gp2/gp3)

- cost effective, low-latency
- gp3: can set volume size, throughput, IOPS independently
- gp2: **volume size and IOPS are linked**
- TODO: need to check exact size and IOPS limit

#### Provisioned IOPS (PIOPS) SSD (io1/io2)

- critical business applications with sustained IOPS performance, or **> 16,000 IOPS required**
- great for **DB workloads**
- io1
    - 4GiB - 16TiB
    - max 64000 PIOPS for Nitro EC2 instances, 32000 for others
    - can increase PIOPS independently from storage size
- io2
    - 4GiB - 64TiB
    - sub-ms latency
    - max 256000 with IOPS:GiB ratio of 1000:1 (PIOS, storage size are linked)
- support EBS multi-attach!

#### HDD

- cannot be a boot volume
- 125GiB - 16TiB
- st1 (Throughput Optimized)
    - Big Data, Log Processing, Data Warehouses
    - Max throughput 500MiB/s, IOPS 500
- sc1 (cold HDD)
    - lowest cost
    - Max throughput 250MiB/s, IOPS 250

### EBS Multi-Attach - io1/io2 only

- Attach same EBS volume to multiple EC2 instances *in the same AZ*
- each instance has full read & write permissions
- use case:
    - higher application availability in clustered Linux applications (ex: Teradata)
    - applications must manage concurrent write operations
- *Up to **16** EC2 instances at a time*

## AMI

- AMI = Amazon Machine Image
- customization of an EC2 instance
    - you can add your own SW, config, OS, monitoring, ...
    - faster boot / config time since all your SW is **pre-packaged**
- you can build AMI for a **specific region(not AZ)** (and can be copied across regions)
- you can launch EC2 instances from a public AMI, or your own custom AMI
- you can buy or sell AMI at AWS marketplace

### how to make AMI from an EC2 instance

1. Start EC2 instance, customize it
2. Stop the instance, and build an AMI (this will also create EBS snapshots)

### 그럼 AMI와 snapshot의 차이가 무엇일까?

- 우선 AMI의 usgae 및 장점: 특정 패키지의 설치를 user script에 작성하는 대신, AMI로 pre-package하여 instance의 boot 속도를 빠르게 할 수 있음!
- 그냥 EBS snapshot을 찍고 매번 통으로 restore하는 것이랑 어떤 차이가 있을까?: [stackoverflow](https://stackoverflow.com/a/54157492)

## Local EC2 Instance Store

- EBS volumes are 'network drives' == good but still 'limited' performance
- EC2 Instance Store: high-performance HW disk
- Better I/O, but *ephemeral*: lose if they're stopped
- good for buffer / cache / temporary content
- risk of data loss if HW fails
- backups & replications is your responsibility

## Amazon EFS - Elastic File System

- Managed NFS (Network File System) that can be mounted on many EC2
- EFS works with EC2 instances in **multi-AZ**
- Highly available, scalable, expensive, pay per use
- use cases: content management, web serving, data sharing, Wordpress
- use NFSv4.1 protocol internally
- use 'security group' to control access to EFS
- **compatible with Linux based AMI, not Windows**
- Encryption at rest using KMS
- POSIX file system that has a standard file API
- scales automatically, pay-per-use, no capacity planning!

### Performance

- EFS Scale
    - 1000s of concurrent NFS clients, 10GB+/s throughput
    - grow to Petabyte-scale automatically
- Performance Mode (set at EFS creation time)
    1. General Purpose (default): latency-sensitive use cases (web server, CMS, ...)
    2. Max I/O: higher latency, throughput, highly parallel (big data, media processing)
- Throughput Mode
    1. Bursting: 1TB = 50MiB/s + burst of up to 100MiB/s
    2. Provisioned: set throughput regardless of storage size. ex: 1 GiB/s for 1TB storage
    3. Elastic: automatically scales throughput up or down based on workloads - up to 3GiB/s reads, 1GiB/s writes

### Storage Classes

- Storage Tiers (lifecycle management feature - move file from standard tier to IA tier after N days)
    - standard: for frequently accessed files
    - infrequent access (EFS-IA): cost to retrieve files, but lower price
- Availability and durability
    - standard: multi-AZ, great for production
    - one zone: one-AZ, great for development, backup enabled by default, compatible with IA
- over 90% cost savings!

## EBS vs EFS

### EBS

- can be attached to one instance (except io1/io2)
- locked to one AZ
- to migrate across AZ, need to take snapshot and restore to another AZ
- root EBS volumes of instances: terminate when EC2 is terminated (by default)

### EFS

- can mount 100s of instances *across AZ*
- EFS share website files (WordPress)
- Only Linux Instances
- higher price than EBS
- can leverage EFS-IA(Infrequent Access) for cost savings

## 기억할 내용

- EFS vs EBS vs local instance store 비교!
- region-scope vs AZ-scope
