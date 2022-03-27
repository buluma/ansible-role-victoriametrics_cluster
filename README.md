# [victoriametrics_cluster](#victoriametrics_cluster)

Ansible role for installing and configuring victoriametrics cluster

|GitHub|GitLab|Quality|Downloads|Version|Issues|Pull Requests|
|------|------|-------|---------|-------|------|-------------|
|[![github](https://github.com/buluma/ansible-role-victoriametrics_cluster/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-victoriametrics_cluster/actions)|[![gitlab](https://gitlab.com/buluma/ansible-role-victoriametrics_cluster/badges/master/pipeline.svg)](https://gitlab.com/buluma/ansible-role-victoriametrics_cluster)|[![quality](https://img.shields.io/ansible/quality/58578)](https://galaxy.ansible.com/buluma/victoriametrics_cluster)|[![downloads](https://img.shields.io/ansible/role/d/58578)](https://galaxy.ansible.com/buluma/victoriametrics_cluster)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-victoriametrics_cluster.svg)](https://github.com/buluma/ansible-role-victoriametrics_cluster/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-victoriametrics_cluster.svg)](https://github.com/buluma/ansible-role-victoriametrics_cluster/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-victoriametrics_cluster.svg)](https://github.com/buluma/ansible-role-victoriametrics_cluster/pulls/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: true

  pre_tasks:
    - name: Update apt cache.
      apt: update_cache=yes cache_valid_time=600
      when: ansible_os_family == 'Debian'
      changed_when: false

  roles:
    - role: apps_victoriametrics
```

The machine needs to be prepared. In CI this is done using `molecule/default/prepare.yml`:
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: true
  pre_tasks:
    - name: Update apt cache.
      apt: update_cache=yes cache_valid_time=600
      when: ansible_os_family == 'Debian'
      changed_when: false
```


## [Role Variables](#role-variables)

The default values for the variables are set in `defaults/main.yml`:
```yaml
---
debug_exec: true
# Install options
victoriametrics_install_standalone: true
victoriametrics_install_cluster: false  # todo
victoriametrics_install_vmutils: true

victoriametrics_cluster_role: [vminsert, vmselect, vmstorage]
victoriametrics_version: "1.67.0"
victoriametrics_vmutils_version: "1.67.0"
victoriametrics_cluster_version: "1.67.0"

victoriametrics_system_user: "victoriametrics"
victoriametrics_system_group: "{{ victoriametrics_system_user }}"

# Systemd options
victoriametrics_data_dir: "/var/lib/victoria-metrics/"
victoriametrics_retention_period: "12"
victoriametrics_service_args:
  storageDataPath: "{{ victoriametrics_data_dir }}"
  retentionPeriod: "{{ victoriametrics_retention_period }}"
victoriametrics_max_open_files: 2097152
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-victoriametrics_cluster/blob/main/requirements.txt).


## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.co.ke/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-victoriametrics_cluster/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|ubuntu|all|
|debian|all|
|el|all|

The minimum version of Ansible required is 2.8, tests have been done to:

- The previous version.
- The current version.
- The development version.



If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-victoriametrics_cluster/issues)

## [License](#license)

Apache License, Version 2.0

## [Author Information](#author-information)

[Michael Buluma](https://buluma.github.io/)
