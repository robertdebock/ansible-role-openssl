# [openssl](#openssl)

Make openssl certificates.

|Travis|GitHub|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-openssl.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-openssl)|[![github](https://github.com/robertdebock/ansible-role-openssl/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-openssl/actions)|[![quality](https://img.shields.io/ansible/quality/48939)](https://galaxy.ansible.com/robertdebock/openssl)|[![downloads](https://img.shields.io/ansible/role/d/48939)](https://galaxy.ansible.com/robertdebock/openssl)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-openssl.svg)](https://github.com/robertdebock/ansible-role-openssl/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.openssl
      openssl_items:
        - name: my_openssl_key
          common_name: my.example.com
```

The machine may need to be prepared using `molecule/resources/prepare.yml`:
```yaml
---
- name: prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.buildtools
    - role: robertdebock.epel
    - role: robertdebock.python_pip
```

For verification `molecule/resources/verify.yml` runs after the role has been applied.
```yaml
---
- name: Verify
  hosts: all
  become: yes
  gather_facts: no

  tasks:
    - name: check if connection still works
      ping:
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for openssl

# You can pass a list of ssl key/csr/crt/p12's to generate:
# openssl_items:
#   - name: my_openssl_key
#     common_name: my.example.com

# You can change the paths where to store each type of object (key, csr, crt,
# p12 and pkcs12). This is not required, by default the distributions regular
# location is set in `vars/main.yml`.

# This directory stores sensitive objects. (key, p12 and pkcs12)
openssl_key_directory: "{{ _openssl_key_directory[ansible_os_family] | default(_openssl_key_directory['default']) }}"

# This directory stores public, non-persistent objects. (csr)
openssl_csr_directory: "{{ _openssl_csr_directory[ansible_os_family] | default(_openssl_csr_directory['default']) }}"

# This directory stores public, persistent objects. (crt)
openssl_crt_directory: "{{ _openssl_crt_directory[ansible_os_family] | default(_openssl_crt_directory['default']) }}"
```

## [Requirements](#requirements)

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.buildtools
- robertdebock.epel
- robertdebock.python_pip

```

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/openssl.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|alpine|all|
|el|7, 8|
|debian|buster, bullseye|
|fedora|31, 32|
|opensuse|all|
|ubuntu|focal, bionic, xenial|

The minimum version of Ansible required is 2.9, tests have been done to:

- The previous version.
- The current version.
- The development version.



## [Testing](#testing)

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-openssl) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-openssl/issues)

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

## [License](#license)

Apache-2.0


## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
