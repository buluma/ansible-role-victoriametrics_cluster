# ansible-apps_victoriametrics

## Description

[![Galaxy Role](https://img.shields.io/badge/galaxy-apps_victoriametrics-purple?style=flat)](https://galaxy.ansible.com/lotusnoir/apps_victoriametrics)
[![Version](https://img.shields.io/github/release/lotusnoir/ansible-apps_victoriametrics.svg)](https://github.com/lotusnoir/ansible-apps_victoriametrics/releases/latest)
![GitHub repo size](https://img.shields.io/github/repo-size/lotusnoir/ansible-apps_victoriametrics?color=orange&style=flat)
[![downloads](https://img.shields.io/ansible/role/d/56106)](https://galaxy.ansible.com/lotusnoir/apps_victoriametrics)
![Ansible Quality Score](https://img.shields.io/ansible/quality/56106)
[![License](https://img.shields.io/badge/license-Apache--2.0-brightgreen?style=flat)](https://opensource.org/licenses/Apache-2.0)

Deploy [victoriametrics](https://victoriametrics.com/) monitoring system.

## Requirements

none

## Role variables

See [variables](/defaults/main.yml) for more details.

## Examples

        ---
        - hosts: apps_victoriametrics
          become: true
          become_method: sudo
          gather_facts: true
          roles:
            - role: ansible-apps_victoriametrics


## License

This project is licensed under Apache License. See [LICENSE](/LICENSE) for more details.

