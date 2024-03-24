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

### EBS Snapshots

- make a backup of your EBS volume at a point in time
- can copy snapshots across AZ

#### Features

- EBS Snapshopt Archive
    - Move a snapshot to "archive tier": 75% cheaper
    - Takes 24-72 hours for restoring! (reason why it's cheaper)
- Recycle Bin
    - retain deleted snapshots for specific retension (from 1 day to 1 year) for recovery from accidental deletion
    - need to set rule in advance
- Fast Snapshot Restore
    - Force full initialization of snapshot to have no latency on the first use
    - expensive!
