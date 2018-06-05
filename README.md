# Couchbase Cluster Role for Ansible

An Ansible Role for setting up Couchbase

## Organising hosts

This module requires 3 hosts groups: `couchbase`, `couchbase-server` and `couchbase-client`:

* All Couchbase servers should belong under the `couchbase` group.
* The master Couchbase servers should belong under `couchbase-master` group
* Any nodes should belong under `couchbase-node`


### Example Hosts file

```
[couchbase:children]
couchbase-master
couchbase-node

[couchbase-master]
cb01.example.com

[couchbase-node]
cb02.example.com
```

## Variables

Here is an example variables file

```
---
couchbase:
  adapter: ansible_eth0
  port: 8091
  clustername: Couchbase
  clusteraddr: localhost:8091
  clusterram: 512
  clusterindexram: 512
  username: Administrator
  password: Administrator
  datapath: /data/couchbase/
```

**Note: Hostnames must be resolvable or cluster rebalance will fail! If you would rather use IP addresses you can override this on a per host basis:**

```
couchbase:
  hostname: <IP ADDRESS>
```

## Example Task with role

```
- name: Couchbase | Cluster Setup
  hosts: couchbase
  roles:
    - edr.couchbase
```
