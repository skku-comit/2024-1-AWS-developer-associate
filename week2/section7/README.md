# section7

## Scalability & High Availability

### Scalability

- Scalability: application / system can handle greater loads by adapting
    - Vertical Scalability
    - Horizontal Scalability (== elasticity)
- **Scalability != High Availalability**, but both are linked

#### Vertical Scalability

- increasing the size of the instance
- common for non distributed systems, such as a database
- there's a limit to how much you can vertically scale (HW limit)

#### Horizontal Scalability

- increase the number of instances / systems for your application
- horizontal scale is available at distributed systems: common for web applicadtions, modern applications
- very easy to horizontally scale with cloud offerings such as EC2

### High Availability

- goes hand in hand with horizontal scaling
- goal of high availability == survive a data center loss (== make application to be available 24 hrs / day as possible)
- can be passive (RDS Multi AZ) or active (horizontal scaling)

### High Availability & Scalability for EC2

- Vertical Scaling: Increasing instance size (scale up / down)
- Horizontal Scaling: Increasing number of instances (scale out / in)
- High Availability: Run instances for the same application across multi AZ
    - Auto Scaling Group multi AZ
    - Load Balancer multi AZ
