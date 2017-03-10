# Apigee OPDK Playbook Maintenance - Cassandra Replication Factor Change Runbook

This is an Ansible playbook that performs a modification of Cassandra replication factor on Apigee
components with Zero Downtime. 

## Requirements and Usage

This playbook uses ansible-galaxy to download roles that are used by this playbook. Once roles are 
downloaded the playbook and be invoked in several ways. The playbook can be invoked in its entirety, 
a tag can be used to invoke a subset of playbook services or the playbook may be run manually. These
ways of invoking the playbook are described below. 

## Download Roles

The playbook roles and their location is found in the  ```requirements.yml``` file. This file is 
provided to ```ansible-galaxy``` so that the roles may be downloaded.

### ansible-galaxy usage

```ansible-galaxy install -r requirements.yml```

### Usage: replication_factor_update.yml 

The ```replication_factor_update.yml``` requires that you specify the ```replication_factor```,
```opdk_region``` and the ```hosts```. 

```ansible-playbook replication_factor_update.yml -e hosts=dc-1-ds -e opdk_region=dc-1 -e replication_factor=3```

### Usage: update.yml 
This playbook contains a convenience playbook that uses the ```replication_factor_update.yml```
 and requires that you specify only the ```replication_factor```.

```ansible-playbook update.yml -vv -b -e replication_factor=3```

### Defined Tags 
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
