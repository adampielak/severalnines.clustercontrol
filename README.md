# Ansible Role: ClusterControl

Installs and configures Severalnines ClusterControl on RHEL/CentOS or Debian/Ubuntu servers. 

## Overview

Installs ClusterControl for your new database node/cluster deployment or on top of your existing database node/cluster. ClusterControl is a management and automation software for database clusters. It helps deploy, monitor, manage and scale your database cluster.

Supported database clusters:

 - Galera Cluster for MySQL
 - Percona XtraDB Cluster
 - MariaDB Galera Cluster
 - MySQL Replication
 - MySQL single instance
 - MySQL Cluster (NDB)
 - MongoDB Replica Set
 - MongoDB Sharded Cluster
 - TokuMX Cluster
 - PostgreSQL single instance

More details at [Severalnines](http://www.severalnines.com) website.

## Requirements

Make sure you meet following criteria prior to the deployment:

 - ClusterControl node must run on a clean dedicated host with internet connection.
 - If you are running as non-root user, make sure the user is able to escalate to root with sudo command.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    mysql_user_home: /root

The home directory inside which Python MySQL settings will be stored, which Ansible will use when connecting to MySQL. This should be the home directory of the user which runs this Ansible role.

    mysql_root_password: password

The MySQL root user account password.

    mysql_root_username: root

The MySQL super user account username. It's recommended to keep the default.

    cmon_mysql_password: cmon

The MySQL password for user 'cmon'.

    cmon_mysql_port: 3306

ClusterControl will install MySQL/MariaDB server to listen on this port, and ClusterControl applications will be configured accordingly.

## Example Playbook

The simplest playbook would be:

    - hosts: clustercontrol-server
      roles:
        - { role: severalnines.clustercontrol }

If you would like to specify custom configuration values as explained above, create a file called `vars/main.yml` and include it inside the playbook:
    - hosts: 192.168.10.15
      vars:
        - vars/main.yml
      roles:
        - { role: severalnines.clustercontrol }

*Inside `vars/main.yml`*:

    mysql_root_username: admin
    mysql_root_password: super-user-password
    cmon_mysql_password: super-cmon-password
    cmon_mysql_port: 3307

If you are running as another user, ensure the user has ability to escalate as super user via sudo. Example playbook for Ubuntu 12.04 with sudo password enabled:

    - hosts: ubuntu@192.168.10.100
      become: yes
      become_user: root
      roles:
        - { role: severalnines.clustercontrol }

Then, execute the command with --ask-become-pass flag.

## Limitations

This playbook is built on top of Ansible v1.9.4 and has been tested on following platforms:
 - Debian 8.x (jessie)
 - Ubuntu 12.04 LTS (precise)
 - RHEL/CentOS 6/7

## Author Information

This role was created in 2016 by Ashraf Sharif from [Severalnines AB](http://severalnines.com/).
