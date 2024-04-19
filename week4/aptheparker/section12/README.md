# Section 12. AWS CLI, SDK, IAM Roles & Policies

## EC2 Instance Metadata (IMDS)

- Allows EC2 instances to learn about themselves without using an IAM role for that purpose.
- Can retrieve IAM Role name but not the IAM Policy.
- IMDSv1 vs. IMDSv2
  - IMDSv1: access http://169.254.169.254/latest/meta-data directly.
  - IMDSv2: more secure, requires token to access metadata.
    1. Get Session Token (STS): `curl -X PUT " http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"`
    2. Use Session Token: `curl http://169.254.169.254/latest/meta-data/profile -H "X-aws-ec2-metadata-token: $TOKEN`

## MFA with CLI

- Must use temporary credentials (STS GetSessionToken) to use MFA.
  - `aws sts get-session-token --serial-number arn:aws:iam::123456789012:mfa/aptheparker --token-code 123456`

## AWS SDK

- AWS SDKs are available in multiple languages.
- To perform actions on AWS services from code. (Ex. use SDK when coding against DynamoDB)

## AWS Limits (Quotas)

- API Rate Limits: how many API calls you can make per second.
  - Exponential Backoff: retry mechanism when you hit the rate limit. (wait 2^x seconds)
- Service Quotas: how many resources you can create in your account.

## AWS CLI Credentials Provider Chain

1. Command Line Options: `--region`, `--output`, `--profile`
2. Environment Variables: `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_SESSION_TOKEN`
3. CLI Credentials File: `~/.aws/credentials`
4. CLI Configuration File: `~/.aws/config`
5. Container Credentials: ECS Task Role
6. Instance Profile Credentials: EC2 Instance Profile

**Credentials Best Practices**: use IAM Roles for EC2 instances when possible & use environment variables for local development.

## Signing AWS API Requests

- AWS API requests must be signed to authenticate.
- Using SDK and CLI automatically signs requests.
- Should sign requests using Signature v4.
- 2 ways to sign requests:
  1. HTTP Header (signature in 'Authorization header')
  2. Query Parameters (signature in 'X-Amz-Signature')
