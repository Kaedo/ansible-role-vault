# [vault](#vault)

Install Hashicorp Vault, either a package or a binary.

|GitHub|GitLab|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![github](https://github.com/robertdebock/ansible-role-vault/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-vault/actions)|[![gitlab](https://gitlab.com/robertdebock-iac/ansible-role-vault/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-vault)|[![quality](https://img.shields.io/ansible/quality/50255)](https://galaxy.ansible.com/robertdebock/vault)|[![downloads](https://img.shields.io/ansible/role/d/50255)](https://galaxy.ansible.com/robertdebock/vault)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-vault.svg)](https://github.com/robertdebock/ansible-role-vault/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/robertdebock/ansible-role-vault/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.vault
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/robertdebock/ansible-role-vault/blob/master/molecule/default/prepare.yml):

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
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/robertdebock/ansible-role-vault/blob/master/defaults/main.yml):

```yaml
---
# defaults file for vault

# Select the type of Vault to install. Either "oss", "ent" or "hsm".
# `oss` means Open Source.
# `ent` means Enterprise.
# `hsm` means Enterprise with HSM support.
vault_type: oss

# Set the version of the package to install.
vault_version: "1.12.3"

# For package installations, a "release" is required. The package would for example be called `vault-1.12.2-1`.
vault_package_release: "1"

# Select the way to intall Vault. Either "package" or "binary".
vault_installation_method: "package"

# When `vault_installation_method` is set to "binary", set the path where to (temporarily) download Vault.
vault_download_path: "/tmp/vault-{{ vault_version }}"

# When `vault_installation_method` is set to "binary", set the (base) path where to install Vault. This can be "" or "/opt" for example.
vault_path: ""

# When `vault_installation_method` is set to "binary", set the user Vault will run under. The user "root" is not allowed.
vault_user: vault

# When `vault_installation_method` is set to "binary", set the group Vault will run under. The group "root" is not allowed.
vault_group: vault

# When `vault_installation_method` is set to "binary", set the shell for the vault_user.
vault_user_shell: /bin/false

# Where to store data. That's Raft data and TLS material.
vault_data_directory: /opt/vault
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-vault/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-bootstrap)|
|[robertdebock.core_dependencies](https://galaxy.ansible.com/robertdebock/core_dependencies)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-core_dependencies/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-core_dependencies/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-core_dependencies)|
|[robertdebock.hashicorp](https://galaxy.ansible.com/robertdebock/hashicorp)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-hashicorp/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-hashicorp/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-hashicorp/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-hashicorp)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/ansible-role-vault/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|[Amazon](https://hub.docker.com/repository/docker/robertdebock/amazonlinux/general)|Candidate|
|[Debian](https://hub.docker.com/repository/docker/robertdebock/debian/general)|all|
|[EL](https://hub.docker.com/repository/docker/robertdebock/enterpriselinux/general)|all|
|[Fedora](https://hub.docker.com/repository/docker/robertdebock/fedora/general)|36, 37|
|[Ubuntu](https://hub.docker.com/repository/docker/robertdebock/ubuntu/general)|all|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-vault/issues)

## [License](#license)

[Apache-2.0](https://github.com/robertdebock/ansible-role-vault/blob/master/LICENSE).

## [Author Information](#author-information)

[robertdebock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
