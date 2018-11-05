cntlm
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-cntlm.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-cntlm)

The purpose of this role is to install and configure cntlm on your system.

Example Playbook
----------------

This example is taken from `molecule/default/playbook.yml`:
```
---
- name: Converge
  hosts: all
  become: true
  gather_facts: false

  roles:
    - robertdebock.bootstrap
    - robertdebock.cntlm

```

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```
---
# defaults file for cntlm

# The version of CNTLM to install.
cntlm_version: 0.92.3

# What release to install.
cntlm_release: 1

# Where to download CNTLM from.
cntlm_download_mirror: netcologne.dl.sourceforge.net

# CNTLM authenticate to the proxy, set a username, password and domain.
cntlm_username: changeme
cntlm_password: changeme
cntlm_domain: example.com
cntlm_proxy: changeme.example.com

# To what port should CNTLM listen?
cntlm_listen: 3128

# When you've got a password hash, you may fill it in here.
cntlm_passntlmv2: 1234567890abcdef

# What hosts to omit in the proxy.
cntlm_noproxy: localhost

# To update all packages installed by this roles, set `cntlm_package_state` to `latest`.
cntlm_package_state: present

```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the last 3 release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

---
- robertdebock.bootstrap
- robertdebock.buildtools


Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/cntlm.png "Dependency")


Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.4|ansible 2.5|ansible 2.6|ansible 2.7|ansible devel|
|------------|-----------|-----------|-----------|-----------|-------------|
|alpine-edge*|yes|yes|yes|yes|yes*|
|alpine-latest|yes|yes|yes|yes|yes*|
|archlinux|yes|yes|yes|yes|yes*|
|centos-6|yes|yes|yes|yes|yes*|
|centos-latest|yes|yes|yes|yes|yes*|
|debian-latest|yes|yes|yes|yes|yes*|
|debian-stable|yes|yes|yes|yes|yes*|
|debian-unstable*|yes|yes|yes|yes|yes*|
|fedora-latest|yes|yes|yes|yes|yes*|
|fedora-rawhide*|yes|yes|yes|yes|yes*|
|opensuse-leap|yes|yes|yes|yes|yes*|
|opensuse-tumbleweed|yes|yes|yes|yes|yes*|
|ubuntu-artful|yes|yes|yes|yes|yes*|
|ubuntu-devel*|yes|yes|yes|yes|yes*|
|ubuntu-latest|yes|yes|yes|yes|yes*|

A single star means the build may fail, it's marked as an experimental build.

Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-cntlm) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-cntlm/issues)

To test this role locally please use [Molecule](https://github.com/metacloud/molecule):
```
pip install molecule
molecule test
```
There are many specific scenarios available, please have a look in the `molecule/` directory.


License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
