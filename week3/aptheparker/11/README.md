# Section 11. S3

## S3 Basics

- **S3**: Simple Storage Service
- Use cases:
  - Backup and restore
  - Disaster recovery
  - Archive
  - Big Data analytics
  - Hybrid cloud storage
  - Application hosting
- **Bucket**: Container for objects
- **Object**: File (up to 5TB)
  - Metadata: key-value pairs
  - Tags: key-value pairs
  - Version ID

## S3 Security

- User-based
  - IAM policies
- Resource-based
  - Bucket policies
  - Object Access Control Lists (ACLs)
  - Bucket Access Control Lists (ACLs)
- Encryption: encrypt objects in S3 using encryption keys

## S3 Bucket Policies

- JSON-based
- Resources: buckets and objects
- Actions: set of API calls
- Effect: Allow/Deny
- Principal: account/user/role that policy applies to

## Static Website Hosting

- S3 can host static websites & have them accessible on the internet
- Website URL: `http://<bucket-name>.s3-website-<region>.amazonaws.com`

## S3 Versioning

- Stores all versions of an object (including all writes and even deletes)
- Enabled at the bucket level

## S3 Replication (CRR & SRR)

- **Cross-Region Replication (CRR)**: for compliance, lower latency
- **Same-Region Replication (SRR)**: for log aggregation, live replication

## S3 Storage Classes

- **S3 Standard**: For frequently accessed data, low latency.
- **S3 IA (Infrequent Access)**: For data accessed less frequently, but requires rapid access when needed. Lower fee than S3 Standard.
- **S3 One Zone-IA**: Storing secondary backup copies.
- **S3 Glacier**: Low-cost storage class for archiving or backup.
  - Glacier Instant Retrieval: Data available within a few milliseconds.
  - Glacier Flexible Retrieval: Data available within 1-5 minutes.
  - Glacier Deep Archive: Data available within 12 (Standard) - 48 (Bulk) hours.
- **S3 Intelligent Tiering**: Automatically moves objects between two access tiers based on changing access patterns.
