[![Build Status](https://travis-ci.org/lae/ansible-role-docker-ce.svg?branch=master)](https://travis-ci.org/lae/ansible-role-docker-ce)
[![Galaxy Role](https://img.shields.io/badge/ansible--galaxy-docker-ce-blue.svg)](https://galaxy.ansible.com/lae/docker-ce/)

lae.docker-ce
=========

Installs/upgrades and configures Docker Community Edition.

Notes
-----

This role should also work on Fedora 25, but Fedora is currently not tested.
Debian 8, Ubuntu 16 and CentOS 7 are.

Role Variables
--------------

`docker_ce_config` is a dumped as (human-readable) JSON format into
`/etc/docker/daemon.json`, e.g. the following default:

```
docker_ce_config:
  live-restore: true
  log-level: "info"
```

will turn into the following `/etc/docker/daemon.json`:

```
{
    "live-restore": true,
    "log-level": "info"
}
```

`docker_ce_restart_on_upgrade` will restart the docker service if this role
upgrades the `docker-ce` package.


Example Playbook
----------------

```
- hosts: all
  become: True
  roles:
    - lae.docker-ce
  vars:
    docker_ce_restart_on_upgrade: no
```
