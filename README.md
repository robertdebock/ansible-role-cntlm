cntlm
=========

<img src="https://docs.ansible.com/ansible-tower/3.2.4/html_ja/installandreference/_static/images/logo_invert.png" width="10%" height="10%" alt="Ansible logo" align="right"/>
<a href="https://travis-ci.org/robertdebock/ansible-role-cntlm"> <img src="https://travis-ci.org/robertdebock/ansible-role-cntlm.svg?branch=master" alt="Build status"/></a> <img src="https://img.shields.io/ansible/role/d/25457"/> <img src="https://img.shields.io/ansible/quality/25457"/>

Install and configure cntlm on your system.

Example Playbook
----------------

This example is taken from `molecule/resources/playbook.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - robertdebock.cntlm
```

The machine you are running this on, may need to be prepared, I use this playbook to ensure everything is in place to let the role work.
```yaml
---
- name: Prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - robertdebock.bootstrap
    - robertdebock.buildtools
```


Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```yaml
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
cntlm_proxy: changeme.example.com:3128

# To what port should CNTLM listen?
cntlm_listen: 3128

# When you've got a password hash, you may fill it in here.
cntlm_passntlmv2: 1234567890abcdef

# What hosts to omit in the proxy.
cntlm_noproxy: localhost

# Where to install temporary files
cntlm_tmp: /root

# Which IPs or CIDR subnets CNTLM is accessible from.  Items other than 127.0.0.1 are only effective if gateway_enabled
# is yes
cntlm_allows:
  - 127.0.0.1

# By default ("0/0"), CNTLM is inaccessible from all other IP addresses.
cntlm_denies:
  - 0/0

# If yes, access to CNTLM is possible from outside of the local host, subject to cntlm_allows and cntlm_denies:
gateway_enabled: "no"
```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.buildtools
- robertdebock.service

```

Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/cntlm.png "Dependency")


Compatibility
-------------

This role has been tested on these [container images](https://hub.docker.com/):

|container|tags|
|---------|----|
|amazon|Candidate|
|archlinux|all|
|debian|all|
|el|7, 8|
|fedora|all|
|ubuntu|trusty, artful|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.

Exceptions
----------

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| EL | No package matching 'bison' found available, installed or updated |
| Alpine | Cannot make the task 'start and enable cntlm' idempotent. |

Included version(s)
-------------------

This role [refers to a version](https://github.com/robertdebock/ansible-role-cntlm/blob/master/defaults/main.yml) released by Mavey on SOURCEFORGE. Check the released version(s) here:
- [cntlm](https://sourceforge.net/projects/cntlm/files/).

This version reference means a role may get outdated. Monthly tests occur to see if [bit-rot](https://en.wikipedia.org/wiki/Software_rot) occured. If you however find a problem, please create an issue, I'll get on it as soon as possible.
Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-cntlm) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-cntlm/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/)
