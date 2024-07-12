# Ansible role [backup](https://galaxy.ansible.com/ui/standalone/roles/buluma/backup/documentation)

The purpose of this role is to make backups of your system.

|GitHub|Version|Issues|Pull Requests|Downloads|
|------|-------|------|-------------|---------|
|[![github](https://github.com/buluma/ansible-role-backup/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-backup/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-backup.svg)](https://github.com/buluma/ansible-role-backup/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-backup.svg)](https://github.com/buluma/ansible-role-backup/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-backup.svg)](https://github.com/buluma/ansible-role-backup/pulls/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/backup)](https://galaxy.ansible.com/ui/standalone/roles/buluma/backup/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-backup/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true

  roles:
    - role: buluma.backup
      backup_cleanup: false
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-backup/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  gather_facts: false
  become: true

  roles:
    - role: buluma.bootstrap
    - role: buluma.mysql
      mysql_databases:
        - name: test_db
          encoding: utf8
          collation: utf8_bin
    - role: buluma.buildtools
    - role: buluma.epel
    - role: buluma.python_pip
    - role: buluma.postgres
      postgres_databases:
        - name: test_db
          state: present
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-backup/blob/master/defaults/main.yml):

```yaml
---
# defaults file for backup

# The directory on the Ansible controller where to store backups.
backup_directory: backups

# The directory on the Ansible managed node where to temporarily store backups.
backup_remote_directory: /tmp

# Cleanup files created on the {{ backup_remote_directory }} when done?
backup_cleanup: true

# What timestamp format to use when saving files.
backup_timestamp: "{{ ansible_date_time.date }}"

# What compression type to use, choose from bz2, tar, xz or zip
backup_format: zip

backup_objects:
  - name: varspool
    type: directory
    source: /var/spool
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-backup/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | Version |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Ansible Molecule](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-bootstrap.svg)](https://github.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.mysql](https://galaxy.ansible.com/buluma/mysql)|[![Ansible Molecule](https://github.com/buluma/ansible-role-mysql/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-mysql/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-mysql.svg)](https://github.com/shadowwalker/ansible-role-mysql)|
|[buluma.buildtools](https://galaxy.ansible.com/buluma/buildtools)|[![Ansible Molecule](https://github.com/buluma/ansible-role-buildtools/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-buildtools/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-buildtools.svg)](https://github.com/shadowwalker/ansible-role-buildtools)|
|[buluma.epel](https://galaxy.ansible.com/buluma/epel)|[![Ansible Molecule](https://github.com/buluma/ansible-role-epel/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-epel/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-epel.svg)](https://github.com/shadowwalker/ansible-role-epel)|
|[buluma.python_pip](https://galaxy.ansible.com/buluma/python_pip)|[![Ansible Molecule](https://github.com/buluma/ansible-role-python_pip/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-python_pip/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-python_pip.svg)](https://github.com/shadowwalker/ansible-role-python_pip)|
|[buluma.postgres](https://galaxy.ansible.com/buluma/postgres)|[![Ansible Molecule](https://github.com/buluma/ansible-role-postgres/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-postgres/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-postgres.svg)](https://github.com/shadowwalker/ansible-role-postgres)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-backup/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/r/buluma/enterpriselinux)|8|
|[Fedora](https://hub.docker.com/r/buluma/fedora)|39, 40|
|[opensuse](https://hub.docker.com/r/buluma/opensuse)|all|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-backup/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-backup/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-backup/blob/master/LICENSE)

## [Author Information](#author-information)

[Shadow Walker](https://buluma.github.io/)
