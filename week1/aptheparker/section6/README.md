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
