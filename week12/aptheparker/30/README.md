# Section 30.Security: KMS, Encryption SDK, SSM Parameter Store, IAM & STS

## Encryption

- `Encryption in flight (SSL/TLS)`

  - Data is encrypted before sending and decrypted after receiving.
  - Ensures no MITM (man in the middle attack).
    ![Encryption in flight](./images/encryption-in-flight.png)

<hr>

- `Server-side encryption at rest`

  - Data is encrypted after being received by the server and decrypted before being sent.
  - Stored in an encrypted form thanks to a key.
    ![Server-side encryption at rest](./images/server-side-encryption-at-rest.png)

<hr>

- `Client-side encryption`
  - Data is encrypted by the client and never decrypted by the server.
  - The server only stores the encrypted data and does not have access to the encryption keys.
    ![Client-side encryption](./images/client-side-encryption.png)

## KMS (Key Management Service)

- AWS Manages encryption keys for us.
- Fully integrated with IAM for authorization.
- Seamlessly integrated into most AWS services. (EBS, S3, RDS, etc.)

<hr/>

- KMS Keys Types:

  - `Symmetric (AES-256)`: Single key to encrypt and decrypt.
  - `Asymmetric (RSA & ECC - Elliptic Curve Cryptography)`: Public and private key pair. Public key encrypts data, private key decrypts data.

<hr>

- KMS Workflow (Server-side encryption):
  ![KMS Workflow](./images/kms-workflow.png)

- Envelope Encryption (Client-side encryption):

  - Encrypt > 4KB.
  - GenerateDataKey API.
  - Envelope Encryption:
    ![Envelope Encryption](./images/envelope-encryption.png)
  - Decrypt Envelope Data:
    ![Decrypt Envelope Data](./images/decrypt-envelope-data.png)

<hr>

- KMS Request Quotas:
  - Throttling Exceptions when you exceed the request rate.
  - Solution:
    - Exponential backoff.
    - DEK caching from the Encryption SDK.
    - Request a Request Quotas increase through API or AWS support.

<hr>

- S3 Bucket Key for SSE-KMS encryption
  - Decrease number of KMS calls from S3 by 99%.
  - Decrease cost of KMS calls from S3 by 99%.
    ![S3 Bucket Key](./images/s3-bucket-key.png)

## CloudHSM

- Cloud Hardware Security Module.
- Hardware security module (HSM) for key storage and cryptographic operations.
- Users manage their own keys entirely. (Not AWS).
- No free tier.
  ![CloudHSM](./images/cloudhsm.png)

<hr>

- High Availability:
  - Multiple HSMs in multiple AZs.
    ![High Availability](./images/high-availability.png)

## SSM Parameter Store

- Secure storage for configuration and secrets.

![SSM Parameter Store](./images/ssm-parameter-store.png)

<hr>

- SSM Parameter Store Hierarchy:
  ![SSM Parameter Store Hierarchy](./images/ssm-parameter-store-hierarchy.png)

## Secrets Manager

- Rotate, manage and retrieve secrets from the AWS console.
- Secrets are encrypted using KMS.

<hr>

- Multi-Region Secrets:
  - Replicate Secrets across multiple AWS Regions.
    ![Multi-Region Secrets](./images/multi-region-secrets.png)

<hr>

- Secrets Manager vs SSM Parameter Store:
<table>
  <tr>
    <th>SSM Parameter Store</th>
    <th>Secrets Manager</th>
  </tr>
  <tr>
    <td>No secret rotation</td>
    <td>Automatic rotation of secrets with AWS Lambda</td>
  </tr>
  <tr>
    <td>Cheap</td>
    <td>Expensive</td>
  </tr>
  <tr>
    <td>KMS encryption is optional</td>
    <td>KMS encryption is mandatory</td>
  </tr>
</table>

<hr>

- SSM Parameter Store vs. Secrets Manager Rotation
  ![SSM Parameter Store vs. Secrets Manager Rotation](./images/ssm-parameter-store-vs-secrets-manager-rotation.png)

## Cloudformation - Dynamic References

- Reference external values stored in Systems Manager Parameter Store and Secrets Manager within CloudFormation templates.
- CloudFormation retrieves the value of the specified reference during create/update/delete operations.
  ![Cloudformation - Dynamic References](./images/cloudformation-dynamic-references.png)

<hr>

- Option 1: ManageMasterUserPassword

  - creates admin secret implicitly.
    ![ManageMasterUserPassword](./images/manage-master-user-password.png)

- Option 2: Dynamic Reference
  ![Dynamic Reference](./images/dynamic-reference.png)
