# Section 5. EC2 Fundamentals

## EC2 (Elastic Compute Cloud)

- Infrastructure as a Service (IaaS).
- Consists in the capability of:
  - Renting virtual machines (EC2 instances).
  - Storing data on virtual drives (EBS).
  - Distributing load across machines (ELB).
  - Scaling the services using an auto-scaling group (ASG).

## Security Groups

- Firewalls that control traffic at the instance level.
- Regulate:
  - Access to ports.
  - Authorised IP ranges - IPv4 and IPv6.
  - Control of inbound & outbound network (can be different).

## SSH (Secure Shell Protocol)

- Used to connect to EC2 instances.
- EC2 Instance Connect
  - Browser-based SSH connection to EC2 instances using the AWS Management Console.
  - No need to use a key file.
  - Port 22 must be open in the security group.

## EC2 Instances Purchasing Options

- On-Demand: Pay fixed rate by the hour (or second) with no commitment.
- Reserved: Capacity reservation, significant discount on hourly charge.
- Savings Plans: Commit to a consistent amount of usage (measured in $/hour) for a 1 or 3 year term.
- Spot Instances: Bid for unused capacity, can get a significant discount.
- Dedicated Hosts: Physical EC2 server dedicated for your use, can help reduce costs by allowing you to use your existing server-bound software licenses.
- Dedicated Hosts: Physical EC2 server dedicated for your use, can help reduce costs by allowing you to use your existing server-bound software licenses.
- Dedicated Instances: Instances running on hardware that's dedicated to a single customer.
- Capacity Reservations: Reserve capacity for your EC2 instances in a specific Availability Zone for any duration.
