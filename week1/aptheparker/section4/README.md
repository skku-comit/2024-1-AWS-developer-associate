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
