# [victoriametrics_cluster](#victoriametrics_cluster)

Ansible role for installing and configuring victoriametrics cluster

|GitHub|GitLab|Quality|Downloads|Version|Issues|Pull Requests|
|------|------|-------|---------|-------|------|-------------|
|[![github](https://github.com/buluma/ansible-role-victoriametrics_cluster/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-victoriametrics_cluster/actions)|[![gitlab](https://gitlab.com/buluma/ansible-role-victoriametrics_cluster/badges/master/pipeline.svg)](https://gitlab.com/buluma/ansible-role-victoriametrics_cluster)|[![quality](https://img.shields.io/ansible/quality/)](https://galaxy.ansible.com/buluma/victoriametrics_cluster)|[![downloads](https://img.shields.io/ansible/role/d/)](https://galaxy.ansible.com/buluma/victoriametrics_cluster)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-victoriametrics_cluster.svg)](https://github.com/buluma/ansible-role-victoriametrics_cluster/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-victoriametrics_cluster.svg)](https://github.com/buluma/ansible-role-victoriametrics_cluster/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-victoriametrics_cluster.svg)](https://github.com/buluma/ansible-role-victoriametrics_cluster/pulls/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: ensure docker
  become: true
  hosts: all
  roles: [ docker ]

- name: ensure victoria_storage
  become: true
  hosts: all
  roles: [ victoria_cluster ]
  vars: 
    vm_role: victoria-storage
    if_name: enp0s8
  tags: [ 'vm_storage', 'victoria_cluster' ]

- name: ensure victoria_select
  become: true
  hosts: all
  roles: [ victoria_cluster ]
  vars: 
    vm_role: victoria-select
    if_name: enp0s8
  tags: [ 'vm_select', 'victoria_cluster' ]

- name: ensure victoria_insert
  become: true
  hosts: all
  roles: [ victoria_cluster ]
  vars: 
    vm_role: victoria-insert
    if_name: enp0s8
  tags: [ 'vm_insert', 'victoria_cluster' ]
```


## [Role Variables](#role-variables)

The default values for the variables are set in `defaults/main.yml`:
```yaml
---
# Docker images defaults
vm_docker_image_tag: latest
vminsert_docker_repository: victoriametrics/vminsert
vmselect_docker_repository: victoriametrics/vmselect
vmstorage_docker_repository: victoriametrics/vmstorage
## docker image overrides for particular components
# vmstorage_docker_version: ""
# vminsert_docker_version: ""
# vmselect_docker_version: ""

# Systemd settings
environment_file_path: "/etc/default"
systemd_environment_file: ""
exec_stop: ""
## ExecStop overrides for particular components
# vmstorage_exec_stop: ""
# vminsert_exec_stop: ""
# vmselect_exec_stop: ""
exec_start_post: ""
## ExecStartPost overrides for particular components
# vmstorage_exec_start_post: ""
# vminsert_exec_start_post: ""
# vmselect_exec_start_post: ""

# Group of servers with victoria metrics storage role. Used to collect ip addresses for vmselect and vminsert
vmstorage_group: victoria_cluster

# host defaults
vmstorage_host_path: /var/lib/victoriametrics
vm_conf_host_path: /etc/victoriametrics

########################
##### PARAMS BLOCK #####
########################
# Current limitations:
# 1) do not pass storageNode param anywhere. it is generated automatically.
# 2) u cannot use set environment usage per component. variable defines behavior for all components.

# possible values: true, false, both
use_environment: false

# VM storage defaults
vmstorage_params: []

# VM insert defaults
vminsert_params:
- param: replicationFactor
  value: 1

# VM select defaults
vmselect_params:
- param: dedup.minScrapeInterval
  value: "1ms"

# interface to gather ip address
if_name: "{{ vars['ansible_default_ipv4'].interface }}"
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
|debian|all|
|fedora|all|
|el|all|
|ubuntu|focal, bionic|

The minimum version of Ansible required is 2.9, tests have been done to:

- The previous version.
- The current version.
- The development version.



If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-victoriametrics_cluster/issues)

## [License](#license)

Apache-2.0

## [Author Information](#author-information)

[Michael Buluma](https://buluma.github.io/)
