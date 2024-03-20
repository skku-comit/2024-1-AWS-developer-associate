# section4

## IAM

### Users & Groups

- Root acount
- Users: can belong to many groups (even no group)
- Groups: only contain users, not other groups

### Permissions

- JSON으로 유저 별 규칙을 정의

### Policies inheritance

- group에 적용된 policy는은 그 그룹에 속한 유저들에게도 상속됨
- user에게 직접 **inline** policy 또한 부여 가능

### Policies (JSON) structure

- Version
- Id
- Satement
  - Sid
  - Effect (allow, deny)
  - principal: applied to the account or user or role
  - action
  - resource
  - condition

### Defense Mechanisms

#### Password Policy

- min length
- require specific char types
- allow IAM change their own pw
- require to change pw after some time
- prevent pw re-use

### Multi Factor Authentication (MFA)

- want to protect 'at least' Root Accounts
- MFA = pw + security device you own
  - Google Authenticator
  - Authy
  - physical security key
  