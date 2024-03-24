# section5

## billing and cost management

- budgets 탭에서 말 그대로 예산을 정할 수 있다.
- 기본 template 중 'zero spend budget'이 있다. 말 그대로 요금이 부과될 것 같으면, 이를 알려주는 것이다. (실제로는 1달러가 임계값)
- x 달러를 임계값으로 정하고, 실제 사용량 or forecasted spend가 임계값의 n%에 도달하면 알려주는 'notification'들을 추가할 수 있다.

## EC2

- EC2 = Elastic Compute Cloud = Infrastructure as a Service

1. EC2: rent virtual machines
2. EBS: store data in virtual drives
3. ELB: distribute load across machines
4. ASG: scale services using auto-scaling group

### sizing & config options

1. OS: Linux, Windows, Mac OS
2. CPU, RAM
3. Storage:
    1. Network-attached: EBS, EFS
    2. HW: EC2 Instance Store
4. Network card: speed of the card, public IP address
5. Firewall rules: security group
6. Bootstrap script: EC2 User Data

### EC2 User Data

- EC2 user data script: run once at the instance 'first start'
- example:
    - install updates, softwares
    - download files, ...
- runs with root user (sudo)

### EC2 instance types

#### example

- t2.micro: 1 cpu, 1GB mem, EBS-only storage, network performance: low, ...
- t2.xlarge: 4cpu, 16GB mem, ...

#### overview

- <https://aws.amazon.com/ec2/instance-types/>
- naming convention: `m5.2xlarge`
    - m: instance class
    - 5: generation
    - 2xlarge: size within the instance class

#### General Purpose

- balance between: compute, memory, networking

#### Compute Optimized

- great for: batch processing workloads, machine learning, dedicated gaming servers, ...
- class `C`(Compute)

#### Memory Optimized

- great for: high performance, in-memory databases, distributed cache stores, real-time processing of big unstructured data, ...
- class `R`(RAM), `X`, `Z`, ...

#### Storage Optimized

- great for: SQL, noSQL db, data warehousing applications, distributed file systems, ...
- class `I`, `D`, ...

#### `ec2instances.info`

## Security Groups

### overview

- control how traffic is allowed into or out of our EC2 instances
- only 'allow' rules
- security groups can reference by IP or by security group

### deeper dive

- act as "firewall"
- regulate
    - access to ports
    - authroized IP ranges
    - control of inbound(between instances) and outbound(instance - internet) network

### Good to know

- can be attached to multiple instances
- locked down to a region/VPC combination
- live 'outside' EC2: even if traffic is blocked, EC2 won't notice it
- good to maintain one separate security group for SSH access
- **if application is not accessible (time out) - security group issue** (most common case)
- if application gives 'connection refused' - then application error or not launched
- all inbound: blocked by default
- all outbound: allowed by default

### referencing other security groups

- for example, `security group 1` has rule `inbound: authorize security group 1`
- by this, instances within `security group 1` can communicate to each other!

### classic ports

- 22: SSH
- 21: FTP - upload files
- 22: SFTP - upload files using SSH
- 80: HTTP
- 443: HTTPS
- 3389: RDP - log into a Windows instance

### CLI

#### connect via SSH

- way to connect to server for maintanence using CLI
- `ssh -i {security-key-file-path} ec2-user@{public-ip-address-of-the-ec2-instance}`
- `ec2-user`가 해당 ec2 instance의 default user이다. IAM user랑은 아예 별개이다.

#### connect via EC2 Instance Connect

- AWS web console에서 바로 EC2 Instance와 연결된 terminal을 띄워줌. 
- 목록에서 연결을 원하는 instance 클릭 - (우측 상단)connect - EC2 Instance Connect - user name은 (Amazon Linux의 경우)기본적으로 `ec2-user`
- 결국 SSH를 이용하는 것으로, SSH port (22번)을 허용하지 않으면 이것도 작동하지 않으므로 주의!

#### tips

- never enter access key (with `aws configure`) of (admin) user to ec2 instance! - ec2 instance에 접근 가능한 모든 유저에게 해당 (admin) 유저의 권한이 오픈 되기 때문.
- 대신,(필요하다면) 'IAM role'을 instance에 부여해서 해당 instance에게 직접 권한을 부여하기!

### Purchasing Options

1. On-Demand: per second
2. Reserved: 1, 3 years - as the name says!
3. Saving Plans: 1, 3 years - discount for specific amount of usage per month for specific duration, beyond is charged as on-demand
4. Spot Instances: most cheapest, short, less reliable - suitable for distributed workloads
5. Dedicated Hosts: reserve entire physical server - most expensive, useful for using server-bound SW licenses
6. Dedicated Instances: no other customers will share your HW (reserve specific HW)
7. Capacity Reservation: reserve **On-Demand** instances capacity in a 'specific AZ(Availability Zone)' for any duration - suitable for short-term, uninterrupted workloads that needs to be in specific AZ
