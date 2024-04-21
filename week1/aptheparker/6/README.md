# Section 6. EC2 Instance Storage

## EBS Volumes

- Network USB stick.
- Can only be mounted to one EC2 instance at a time.
- Bound to a specific AZ.

![EBS Volume](./images/ebs_volume.png)

# EBS Snapshots

- Point-in-time backup of EBS volumes.
- Stored in S3.
- Features:
  - EBS Snapshot Archive: Cross-region copy of snapshots.
  - Recycle Bin: Delete snapshots without deleting the data.
  - EBS Fast Snapshot Restore: Restore volumes faster.

# AMI (Amazon Machine Image)

- Customization of EC2 instances.
- Built for a specific region.
- Features:
  - Public AMIs: Shared with other AWS accounts.
  - Private AMIs: Owned by a specific AWS account.
  - Marketplace AMIs: Sold by third-party vendors.
- AMI Process:

  1. Launch an EC2 instance.
  2. Customize the instance.
  3. Create an AMI.
  4. Launch new instances from the AMI.

  # EC2 Instance Store

  - High-performance hardware disk.

  # EBS Volume Types

  - Characterized in size, throughput, and IOPS (Input/Output Operations Per Second).
  - gp (General Purpose SSD)
    - Cost-effective.
    - Low-latency.
  - piops (Provisioned IOPS SSD)
    - Sustainable IOPS performance.
    - Suitable for database workloads.
  - hdd (Hard Disk Drive)
    - Cannot be a boot volume.
    - Big data, data warehousing, log processing.

# EBS Multi-Attach

- Allows a single EBS volume to be attached to multiple EC2 instances.
- For high-availability and clustering applications.
- Up to 16 EC2 instances.

# EFS (Elastic File System)

- Managed NFS (Network File System).
- Can be mounted on many EC2 instances, scalable, pay-per-use, and multi-AZ.
- Performance Mode:
  - General Purpose: Latency-sensitive use cases.
  - Max I/O: Higher latency, higher throughput.
- Throughput Mode:
  - Bursting: General-purpose.
  - Provisioned: High throughput.
  - Elastic: Automatically adjusts throughput.
- Storage Classes:
  - Standard: Latency-sensitive use cases.
  - Infrequent Access (IA): Cost-optimized for infrequent access.
  - One Zone-IA: IA storage class in a single

# EBS vs. EFS

- Price
  - EFS is more expensive but has IA to save costs.
- Performance
  - EBS is faster than EFS.
- Use Case
  - EBS is for a single EC2 instance.
  - EFS is for multiple EC2 instances.
