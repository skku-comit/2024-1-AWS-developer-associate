# Section 4. IAM & AWS CLI

- User, Group, Policy

  - Policy: JSON document that defines permissions.
  - IAM Policy Elements: Version, ID, Statement, Sid, Effect, Principal, Action, Resource, Condition.

- MFA (Multi-Factor Authentication)

  - Virtual MFA device: Google Authenticator, Authy.
  - Hardware MFA device: YubiKey, Gemalto.

- Methods to access AWS

  - AWS Management Console: protected by passwords and MFA.
  - AWS Command Line Interface (CLI): protected by access keys.
  - AWS Software Development Kit (SDK): protected by access keys.
    - SDK: Language-specific APIs to interact with AWS services using code.

- IAM Roles

  - Permissions to AWS services.

- IAM Security Tools

  - IAM Credentials Report: CSV file with all users and their various credentials. (account-level)
  - IAM Access Advisor: Shows service permissions granted to users and when those services were last accessed. (user-level)

- IAM Best Practices

  - Don't use root account.
  - Use groups to assign permissions.
  - Use roles to delegate permissions.
  - Use strong password policy and MFA.
  - Use Access Keys for programmatic access.
  - Audit permissions with IAM Credential Report and Access Advisor.
  - Never share IAM users and access keys.

- Shared Responsibility Model

  - AWS: Security of the cloud.
    - Physical security of data centers.
    - Network and infrastructure security.
  - Customer: Security in the cloud.
    - Data encryption.
    - Access management.
    - Application security.
