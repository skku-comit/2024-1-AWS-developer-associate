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

## AMI

- AMI = Amazon Machine Image
- customization of an EC2 instance
    - you can add your own SW, config, OS, monitoring, ...
    - faster boot / config time since all your SW is **pre-packaged**
- you can build AMI for a **specific region** (and can be copied across regions)
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
