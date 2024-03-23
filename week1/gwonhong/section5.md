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
