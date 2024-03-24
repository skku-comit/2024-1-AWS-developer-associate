# section6

## EBS

- Elastic Block Store Volume: a network drive you can attach to your instances while they run
- allows your instances to persist data, **even after their termination**
- can be mounted to one instance at a time (also has 'multi-attach' feature)
- bound to a specific AZ
- ~= network USB stick

### EBS Volume

- network drive (not a physical drive)
    - use network to communicate the instance -> a bit of latency exists
    - can be detached and attached to another quickly (within same AZ)
- locked to an AZ
    - to move a volume across AZs, first need to snapshot it
- have provisioned capacity (in GBs, and IOPS)

### Delete on Termination attribute

- true by default for root volume (of an instance)
- false by default for new volumes

