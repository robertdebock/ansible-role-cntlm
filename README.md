cntlm
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-cntlm.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-cntlm)

Provides cntlm for your system.

Context
-------
This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/cntlm.png "Dependency")

Requirements
------------

Access to a repository containing packages, likely on the internet.

Role Variables
--------------

cntlm_version: The version of cntlm to install.
cntlm_release: The release to install.
cntlm_download_mirror: Where to download cntlm from.

cntlm_username: The username to connect to a corporate proxy.
cntlm_password: The password to connect to a corporate proxy.
cntlm_domain: The domain to authenticate with.
cntlm_proxy: The (existing) corporate proxy to connect to.
cntlm_listen: The port of that proxy.
cntlm_passntlmv2: The generated hash.
cntlm_noproxy: What domains not to proxy to the corporate proxy.

Dependencies
------------

Soft dependencies that prepare your system for cntlm:

- [robertdebock.bootstrap](https://travis-ci.org/robertdebock/ansible-role-bootstrap)

Download the dependencies by issuing this command:
```
ansible-galaxy install --role-file requirements.yml
```

Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.4|ansible 2.5|ansible 2.6|
|------------|-----------|-----------|-----------|
|alpine-edge|no|no|no|
|alpine-latest|no|no|no|
|archlinux|no|no|no|
|centos-6|yes|yes|yes|
|centos-latest|yes|yes|yes|
|debian-latest|yes|yes|yes|
|debian-stable|yes|yes|yes|
|fedora-latest|yes|yes|yes|
|fedora-rawhide|yes|yes|yes|
|opensuse-leap|no|no|no|
|opensuse-tumbleweed|no|no|no|
|ubuntu-artful|yes|yes|yes|
|ubuntu-latest|yes|yes|yes|

Example Playbook
----------------

```
- hosts: servers
  become: yes

  roles:
    - robertdebock.bootstrap
    - robertdebock.cntlm
      cntlm_username: myusername
      cntlm_password: somestring
```

Install this role using `galaxy install robertdebock.cntlm`.

License
-------

Apache License, Version 2.0

Author Information
------------------

Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
