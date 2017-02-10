#Apigee OPDK Playbook Maintenance Cassandra Replication Factor

This playbook uses the roles to modify the Cassandra Replication Factor using Zero Downtime .

## Usage
Use ```ansible-galaxy``` to download the required roles.

```ansible-galaxy install -r requirements.yml```

The ```replication_factor_update.yml``` requires that you specify the ```replication_factor```,
```opdk_region``` and the ```hosts```. 

```ansible-playbook replication_factor_update.yml -e hosts=dc-1-ds -e opdk_region=dc-1 -e replication_factor=3```

This playbook contains a convenience playbook that uses the ```replication_factor_update.yml```
 and requires that you specify only the ```replication_factor```.

```ansible-playbook update.yml -vv -b -e replication_factor=3```

### Tags
The tasks of this playbook have been partitioned work between datacenter