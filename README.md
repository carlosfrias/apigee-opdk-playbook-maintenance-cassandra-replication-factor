## Apigee OPDK Playbook Maintenance - Cassandra Replication Factor Change Runbook

This is an Ansible playbook that performs a modification of the Cassandra replication factor used 
with Apigee components with zero downtime in a two data center topology. 

## Requirements and Usage Overview

This playbook uses ansible-galaxy to download roles that are used by this playbook. Once roles are 
downloaded the playbook and be invoked in several ways. The playbook can be invoked in its entirety, 
a tag can be used to invoke a subset of playbook services or the playbook may be run manually. These
ways of invoking the playbook are described below. 

## Description: Download Roles 

The playbook roles and their location is found in the  ```requirements.yml``` file. This file is 
provided to ```ansible-galaxy``` so that the roles may be downloaded.

## Usage: Ansible Galaxy 

Ansible galaxy will download the required roles when invoked with the install action and the 
requirements file. This is accomplished in the following way:

```ansible-galaxy install -r requirements.yml```

## Update Replication Factor Overview
 
The ```update-replication-factor.yml``` script performs the update of the Cassandra replication 
factor for keyspaces in a Cassandra ring. This playbook assumes that you are changing Cassandra 
replication on a planet that is composed of two regions or two data centers. 

This script expects you to provide the ```replication_factor``` setting you wish to use when the 
script is invoked at the command line. 

## Usage: Full Playbook Invocation
 
The full playbook invocation is performed in the following way: 

    ansible-playbook update-replication-factor -e replication_factor=6 -vvv -b 
    
## Usage: Manaul Playbook Invocation

This playbook enables tasks to be invoked manually. Manual invocation of this playbook is 
accomplished in the following way: 
 
    ansible-playbook update-replication-factor -e replication_factor=6 -vvv --step
    
During manual invocation the playbook will stop before every task. The user is prompted on each task  
for permission to execute, stop execution or continue execution to the first task of the next play. 
The prompt accepts ```y``` to execute; ```n``` to stop execution or ```c``` to continue execution 
and stop on the first task of the next play. 

## Usage: Playbook Invocation with Tags

    ansible-playbook update-replication-factor -e replication_factor=6 -vvv --tags={{ tag name}}
    
## Usage: Manual Playbook Invocation with Tags    

    ansible-playbook update-replication-factor -e replication_factor=6 -vvv --tags={{ tag name}} --step
    
## Defined Tags 

Playbook Name | Tag Name | Description | Usage |
--- | --- | --- | --- | --- |
update-replication-factor.yml | cache | Update local cache apigee attributes | --tags=cache
update-replication-factor.yml | backup | Backup zookeeper and cassandra | --tags=backup
update-replication-factor.yml | two | Set the consistency level to TWO for RMPs and MSs | --tags=two 
update-replication-factor.yml | local-quorum | Set the consistency level to LOCAL_QUORUM for RMPs and MSs  | --tags=local-quorum
update-replication-factor.yml | repair | Perform nodetool repair | --tags=repair
update-replication-factor.yml | restart | Restart all apigee components for nodes with C*/ZK, RMPs and MSs | --tags=restart
update-replication-factor.yml | stop | Stop all apigee components for nodes with C*/ZK, RMPs and MSs | --tags=stop
update-replication-factor.yml | start | Start all apigee components for nodes with C*/ZK, RMPs and MSs | --tags=start
update-replication-factor.yml | update-replication-factor | Update the replication factor | --tags=update-replication-factor
update-replication-factor.yml | logs | Download Apigee logs from servers | --tags=logs
<!-- BEGIN Google Required Disclaimer -->

# Not Google Product Clause

This is not an officially supported Google product.
<!-- END Google Required Disclaimer -->
