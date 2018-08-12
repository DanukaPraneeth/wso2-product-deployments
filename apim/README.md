# Ansible automation of Internal Gateway ( v3.0.0 ) deployement

This is an ansile project to automate downloading the internal gateway products on servers, creating databases, configuring the product changes and start the pack. Products are deployed on four servers as follows.

---
* server 1 - database server ( contain all the databases )
---


## Prerequisits for deployment.

There are some prerequisits in the newly created servers to deploy the products ( eg: ansible, mysql. Java, Python, unzip etc ). These will be automatically installed during the execution of the playbooks.

But there are some prerequisits in the server on which the playbooks are being executed. Those needs to be fulfilled before executing the playbooks.
  
  1. Ansible
  --- 
     sudo apt install ansible
  ---
  2. Python boto
  ---
     sudo apt-get install python-pip 
     sodo pip install -U boto
  --- 
  3. sudo apt-get install sshpass


## Project layout

The product is deployed using three main playbooks and configurations are done in several roles to increase the flexibility.


**play1.yml** - 1 roles
-  install_servers_prerequisits_n_update_ip_addresses ( install ansible on servers and update corresponding host variables in other roles )

**play2.yml** - Download and configure products on newly created servers

1.  Database server - 3 roles
 - download_prerequisites - install java, mysql, unzip and python on the server
 - import_products - import required databases scripts
 - create_DB - create databases and run the database scripts ( database server will identify AM server, MIG server and DAS server using it's IP address, unique username and password. So If username or password of the server needs to be changed, the corresponding variable in each and every role should be updated before running the playbook, play2.yml.

## Important facts

1. Before executing the play1.yml, you should update the host file with corresponding IPs and all the variables in the var file in the role "install_servers_prerequisits_n_update_ip_addresses".

2. Before executing the play2.yml, log into the servers and update the hosts and hostname file in each server with correct host names and IPs of other related servers.

3. Update the hostnames of servers correctly in the var file of the role "install_servers_prerequisits_n_update_ip_addresses" before executing play1.yml

4. Use the same variable values in the var folder of each interrelated roles.

