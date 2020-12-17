# [vault](#vault)

Install Hashicorp Vault on your system.

|Travis|GitHub|GitLab|Quality|Downloads|Version|
|------|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-vault.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-vault)|[![github](https://github.com/robertdebock/ansible-role-vault/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-vault/actions)|[![gitlab](https://gitlab.com/robertdebock/ansible-role-vault/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-vault)|[![quality](https://img.shields.io/ansible/quality/50255)](https://galaxy.ansible.com/robertdebock/vault)|[![downloads](https://img.shields.io/ansible/role/d/50255)](https://galaxy.ansible.com/robertdebock/vault)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-vault.svg)](https://github.com/robertdebock/ansible-role-vault/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.vault
      vault_show_unseal_information: yes
      vault_make_backup: yes
```

The machine needs to be prepared in CI this is done using `molecule/resources/prepare.yml`:
```yaml
---
- name: prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.core_dependencies
    - role: robertdebock.hashicorp
      hashicorp_products:
        - name: vault
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for vault

# Configure clustering.
vault_disable_clustering: "false"

# The leader to use, please use a fqdn, i.e. `vault.example.com`
# This variable is not required for single-node installations, where the
# variabel `vault_disable_clustering` is set to `"True"`.
# vault_leader: centos-7

# The URL where cluster members can find the leader.
vault_cluster_addr: "http://{{ vault_leader | default('localhost') }}:8201"

# The URL where the API will be served. This is the API of a local instance.
vault_api_addr: "http://127.0.0.1:8200"

# The plugin plugin directory.
vault_plugin_directory: /usr/local/lib/vault/plugins

# The storage backend(s) to configure.
vault_storages:
  - name: raft
    path: /vault/data
    node_id: "{{ inventory_hostname_short }}"

# Where vault should listen on.
vault_listeners:
  - name: tcp
    address: 127.0.0.1:8200
    cluster_address: 127.0.0.1:8201
    tls_disable: "true"

# Have the web ui be made available.
vault_ui: "true"

# The amount of unseal keys to hand out.
vault_key_shares: 5
# The amount of unseal keys to require.
vault_key_threshold: 3

# If you want to see the (sensitive) output of `vault operator init`, set
# this parameter to `yes`
vault_show_unseal_information: no

# To reduce disk io, mlock can be disabled.
vault_disable_mlock: "true"

# You can unseal vault using unseal keys that are know. For new installations
# you do not need to specify these.
# vault_unseal_keys:
#   - KeY-oNe
#   - KeY-tWo
#   - KeY-tHrEe

# You can use this role to make a backup of Vault.
vault_make_backup: no

# Where should backups be saved? A full path, including file, for example:
# vault_backup_path: /tmp/my_backup.yml
vault_backup_path: "/root/vault-raft_{{ ansible_date_time.date}}-{{ ansible_date_time.hour }}{{ ansible_date_time.minute }}.snapshot"
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-vault/blob/master/requirements.txt).

## [Status of requirements](#status-of-requirements)

The following roles are used to prepare a system. You may choose to prepare your system in another way, I have tested these roles as well.

| Requirement | Travis | GitHub |
|-------------|--------|--------|
| [robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-bootstrap.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-bootstrap) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions) |
| [robertdebock.core_dependencies](https://galaxy.ansible.com/robertdebock/core_dependencies) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-core_dependencies.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-core_dependencies) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-core_dependencies/actions) |
| [robertdebock.hashicorp](https://galaxy.ansible.com/robertdebock/hashicorp) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-hashicorp.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-hashicorp) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-hashicorp/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-hashicorp/actions) |
| [robertdebock.vault](https://galaxy.ansible.com/robertdebock/vault) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-vault.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-vault) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-vault/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-vault/actions) |

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/vault.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|el|7, 8|
|debian|buster|
|fedora|32, 33|
|ubuntu|bionic, focal|

The minimum version of Ansible required is 2.9, tests have been done to:

- The previous version.
- The current version.
- The development version.



## [Testing](#testing)

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-vault) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-vault/issues)

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
