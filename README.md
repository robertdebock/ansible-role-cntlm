zabbix
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-zabbix.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-zabbix)

Provides Zabbix for your system.

Context
-------
This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/robertdebock.github.io/artifacts/zabbix.png "Dependency")

Requirements
------------

Access to a repository containing packages, likely on the internet.
Access to Extra Packages for Enterprise Linux. (Hint: robertdebock.epel)
Apache HTTPD for a Zabbix web interface. (Hint: robertdebock.httpd)

Role Variables
--------------

None known

Dependencies
------------

Soft dependencies that prepare your system for Zabbix:

- robertdebock.bootstrap
- robertdebock.epel
- robertdebock.httpd (For a Zabbix web frontend.)

Download the dependencies by issuing this command:
```
ansible-galaxy install --role-file requirements.yml
```

Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.3|ansible 2.4|ansible 2.5|
|------------|-----------|-----------|-----------|
|alpine-3.6|yes|yes|yes|
|alpine-3.7|yes|yes|yes|
|archlinux|yes|yes|yes|
|centos-6|yes|yes|yes|
|centos-7|yes|yes|yes|
|debian-buster|no|no|no|
|debian-jessie|yes|yes|yes|
|debian-stretch|yes|yes|yes|
|debian-wheezy|yes|yes|yes|
|fedora-27|no|no|no|
|fedora-28|no|no|no|
|opensuse-42.2|no|no|no|
|opensuse-42.3|no|no|no|
|ubuntu-artful|no|no|no|
|ubuntu-bionic|no|no|no|
|ubuntu-trusty|yes|yes|yes|
|ubuntu-xenial|yes|yes|yes|

Example Playbook
----------------

To install an agent to all `servers`:
```
- hosts: servers
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.epel
    - role: robertdebock.zabbix
```

To install a Zabbix environment:
```
- hosts: databaseserver
  become: yes

  roles:
    - robertdebock.bootstrap
    - robertdebock.mysql

    tasks:
      - name: create database
        mysql_db:
          name: zabbix

      - name: create user
        mysql_user:
          name: zabbix
          password: zabbix
          priv: '*.*:ALL'

- hosts: zabbixserver
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.epel
    - role: robertdebock.zabbix
      zabbix_server: present
      zabbix_server_database_host: "{{ hostvars['databaseserver']['ansible_default_ipv4']['address'] }}"

- hosts: all
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.epel
    - role: robertdebock.
      zabbix_agent_server_address: ""{{ hostvars['zabbixserver']['ansible_default_ipv4']['address'] }}"


- hosts: zabbixwebserver

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.buildtools
    - role: robertdebock.epel
    - role: robertdebock.scl
    - role: robertdebock.httpd
    - role: robertdebock.php
    - role: robertdebock.zabbix
      zabbix_web: present
      zabbix_web_server: localhost
```

Install this role using `galaxy install robertdebock.zabbix`.

License
-------

Apache License, Version 2.0

Author Information
------------------

Robert de Bock <robert@meinit.nl>
