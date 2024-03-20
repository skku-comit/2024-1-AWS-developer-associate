# section4

## Ways to access AWS

1. AWS Management Console (Web): protected with pw + mfa
2. AWS CLI: protected with access keys (Web Console - CloudShell에서도 사용 가능!)
3. AWS SDK - embed within code

### AWS CLI configuration

1. AWS CLI 설치
2. terminal에 `aws configure` 입력
3. 발급받은 access key id, secret 입력

### AWS CloudShell

- 특정 region들에서만 가능
- AWS Web Console에서 CLI 창을 띄워주는 서비스
- 로컬 환경에서 cli 설치하고 설정할 필요 없이 그냥 웹으로 바로 사용 가능!

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

#### Multi Factor Authentication (MFA)

- want to protect 'at least' Root Accounts
- MFA = pw + security device you own
  - Google Authenticator
  - Authy
  - physical security key
