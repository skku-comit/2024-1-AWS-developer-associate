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

- group에 적용된 policy는 그 그룹에 속한 유저들에게도 상속됨
- user에게 직접 **inline** policy 또한 부여 가능

### Policies (JSON) structure

- Version
- Id
- Statement
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

### Roles

- permissions for AWS services instead of user!
- EC2 Instance - IAM Role - AWS services

### IAM Security (monitoring?) Tools

1. IAM Credentials Report (account-level): report of all accounts
2. IAM Access Advisor (per-user-level): shows all permissions granted to a specific user, and when last accessed

### IAM best practices

- do not use root account except for intial setup!
- one physical user = one AWS user
- assign permissions to groups, and assign users to groups, not directly to users.
- create strong password policy
- enforce MFA
- use Roles to grant permissions for AWS services
- use Access Keys for CLI or SDK
- audit permissions of your account using IAM credentials report & access advisor
- Never share IAM users & access keys

### Shared Responsibility Model for IAM

1. AWS: take care of infrastructure
  - Infrastructure
  - Configuration and vulnerability analysis
  - Compliance validation (규정 준수 검증)
2. Me: take care of how to use it (infrastructure)
  - Users, Groups, Roles, Policies management and monitoring
  - security of all accounts (MFA, access key rotation)
  - permission management
  - analyze access patterns & review permissions

### Account vs User

- 로그인할 때 account ID (또는 alias), user name, password 이렇게 세 가지를 입력해야 한다. 단 `https://{account ID or alias}.signin.aws.amazon.com/console`와 같은 주소로 로그인을 시도하면, account ID는 자동으로 채워짐을 알 수 있다.
- (내피셜) account ID란, root account의 ID를 의미하며, user는 그 root account에 딸려있는 관계인 것이다.
- [AWS Organizations terminology and concepts](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_getting-started_concepts.html) 참고할만한 링크 같아서 달아뒀다.
