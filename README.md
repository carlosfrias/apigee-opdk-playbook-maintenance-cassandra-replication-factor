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
Playbook Name | Tag Name | Description 
--- | --- | ----
update.yml | dc-1 | All tasks on dc-1 only
update.yml | dc-2 | All tasks on dc-2 only
update.yml | restart | Restart apigee components other than ds profile components
replication_factor_update.yml | cache | Update ansible cache, includes apigee specific attributes
replication_factor_update.yml | update | Update replication factor
replication_factor_update.yml | repair | Perform nodetool repair
replication_factor_update.yml | restart | Restart all apigee components on the node
replication_factor_update.yml | stop | Stop all apigee components on the node
replication_factor_update.yml | start | Start all apigee components on the node
