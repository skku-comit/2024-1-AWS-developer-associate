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
