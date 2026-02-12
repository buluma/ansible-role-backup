# [Ansible role backup](#ansible-role-backup)

The purpose of this role is to make backups of your system.

|GitHub|GitLab|Downloads|Version|
|------|------|---------|-------|
|[![github](https://github.com/buluma/ansible-role-backup/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-backup/actions)|[![gitlab](https://gitlab.com/shadowwalker/ansible-role-backup/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-backup)|[![downloads](https://img.shields.io/ansible/role/d/buluma/backup)](https://galaxy.ansible.com/buluma/backup)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-backup.svg)](https://github.com/buluma/ansible-role-backup/releases/)|

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

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.mysql](https://galaxy.ansible.com/buluma/mysql)|[![Build Status GitHub](https://github.com/buluma/ansible-role-mysql/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-mysql/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-mysql/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-mysql)|
|[buluma.buildtools](https://galaxy.ansible.com/buluma/buildtools)|[![Build Status GitHub](https://github.com/buluma/ansible-role-buildtools/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-buildtools/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-buildtools/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-buildtools)|
|[buluma.epel](https://galaxy.ansible.com/buluma/epel)|[![Build Status GitHub](https://github.com/buluma/ansible-role-epel/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-epel/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-epel/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-epel)|
|[buluma.python_pip](https://galaxy.ansible.com/buluma/python_pip)|[![Build Status GitHub](https://github.com/buluma/ansible-role-python_pip/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-python_pip/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-python_pip/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-python_pip)|
|[buluma.postgres](https://galaxy.ansible.com/buluma/postgres)|[![Build Status GitHub](https://github.com/buluma/ansible-role-postgres/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-postgres/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-postgres/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-postgres)|

## [Context](#context)

This role is part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-backup/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/r/buluma/enterpriselinux)|all|
|[Fedora](https://hub.docker.com/r/buluma/fedora)|all|
|[opensuse](https://hub.docker.com/r/buluma/opensuse)|all|

The minimum version of Ansible required is 2.12, tests have been done on:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them on [GitHub](https://github.com/buluma/ansible-role-backup/issues).

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-backup/blob/master/LICENSE).

## [Author Information](#author-information)

[Michael Buluma](https://buluma.github.io/)

