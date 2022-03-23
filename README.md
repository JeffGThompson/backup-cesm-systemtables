# Ansible: basic server setup

[![Platform](https://img.shields.io/badge/platform-CentOS%206-lightgrey.svg?style=plastic)](#)
[![Platform](https://img.shields.io/badge/platform-RHEL%206-lightgrey.svg?style=plastic)](#)
[![Platform](https://img.shields.io/badge/platform-CentOS%207-lightgrey.svg?style=plastic)](#)
[![Platform](https://img.shields.io/badge/platform-RHEL%207-lightgrey.svg?style=plastic)](#)

This Ansible playbook backups system tables for CESMs and copies them over to the server you run the playbook on.

# Roles
This playbook consists of the following Ansible roles:

1. common
    - Runs the system table backup commands and retrieves the file.

# Prerequisites

Ansible v2.0 or above is required to use this repo. To install Ansible, see [here](https://docs.ansible.com/ansible/intro_installation.html#installing-the-control-machine).

# Usage

**Note:** this playbook uses [Ansible-Vault](http://docs.ansible.com/ansible/playbooks_vault.html) to encrypt the following files which contain sensitive variables such as passwords for the CORR-engine:
  * `group_vars/client1`
  * `group_vars/client2`
  
  To edit these files, you will need to open them using ansible-vault: 

    $ ansible-vault edit group_vars/[Client CESM]

The password to Ansible Vault can be found in the password safe.

## Deploying the playbook

1. clone this repo: 

2. The IP address of the CESM(s) are in the file `inventory` under the correct group

3. Remove # on the left side of the IP address you wish to run the playbook on.

4. 
    A) Run the playbook as your adm account for CESMs connected to Active Directory:

    `$ ansible-playbook site.yml -i inventory -u jeffthompson -k -K  --ask-vault-pass`
    
    B) Run the playbook as the root user for CESMs not connected to Active Directory: 
   
    `$ ansible-playbook site.yml -i inventory -u root -k -K  --ask-vault-pass`

## Expected Outcome

See build status for what a successful execution of this playbook looks like. 


## Playbook Variables

A brief description of the variables used by this playbook.

The following variables are defined in `group_vars/all` with pre-set defaults that can be overridden:

| Variable | Explanation 
| -------- | -------- | 
| tmp_folder   | Used in case folder used to perform the backup of the system table changes in different versions of Arcsight.
| password | The password used for the CORR-Engine. This can be found on Password Manager as well.
