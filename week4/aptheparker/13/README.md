# Section 13. S3 - Advanced

## Moving between Storage Classes

- Move to Standard IA: infrequent access.
- Move to Glacier: don't need fast retrieval.
- Moving objects can be automated with S3 Lifecycle Policies.

## S3 Lifecycle Rules

- Transition actions: move objects to different storage classes.
- Expiration actions: delete objects after a certain period.
- _Rules can be created for a prefix or tag._

## S3 Analytics

- Help decide when to transition objects to different storage classes.
- Recommendations for Standard & IA storage classes (Does not work for One Zone-IA or Glacier).

## Event Notifications

- Send notifications when objects are uploaded, deleted, etc.
- With EventBridge, can send to other AWS services (Lambda, SNS, SQS, etc.).
  - Advanced filtering options: JSON rules.
  - Multiple Destinations: send to multiple services.
  - EventBridge Capacity: Archive, Replay events.

## S3 Baseline Performance

- Can archive at least 3,500 PUT/COPY/POST/DELETE and 5,500 GET/HEAD requests per second.
- No limit to the number of prefixes in a bucket.

## S3 Performance

- Multi-part upload: upload parts in parallel.
- S3 Transfer Acceleration: use CloudFront edge locations to upload files.

## S3 Byte-Range Fetches

- Download part of an object.
- Parallelize GETs to download parts of an object in parallel.
- Can be used to speed up downloads or retrieve a specific part of an object (Ex. Head of a file).

## S3 Select & Glacier Select

- Retrieve only the data you need from an object by performing SQL queries.

## S3 User-Defined Metadata & S3 Object Tags

- Metadata: key-value pairs to store additional information.
- Tags: key-value pairs to manage objects.
- _Cannot search the object metadata or tags (shoud use an external database such as DynamoDB)._
