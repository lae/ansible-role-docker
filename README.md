[![Build Status](https://travis-ci.org/lae/ansible-role-docker.svg?branch=master)](https://travis-ci.org/lae/ansible-role-docker)
[![Galaxy Role](https://img.shields.io/badge/ansible--galaxy-docker-blue.svg)](https://galaxy.ansible.com/lae/docker/)

lae.docker
==========

Installs/upgrades and configures Docker Community Edition.

Notes
-----

This role should also work on Fedora, but Fedora tests are not passing on LXC.
Debian 8/9, Ubuntu 16 and CentOS 7 are.

Role Variables
--------------

`docker_config` is a dumped as (human-readable) JSON format into
`/etc/docker/daemon.json`, e.g. the following default:

```
docker_config:
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

`docker_restart_on_upgrade` will restart the docker service if this role
upgrades the `docker-ce` package.

To install `docker-compose`, set `docker_compose_install` to `True` or `yes`.
This will install `docker-compose` via PyPI, as well as pull the `docker` Python
library. To only install the `docker` library, set `docker_python_install` to
`True` or `yes`. You will likely need to ensure a recent version of `pip` is
installed, as the `docker` library depends on a version of `requests` that is
incompatible with the `pip` package in most distributions. For testing, this
role uses [azavea.pip](https://galaxy.ansible.com/azavea/pip/).

Example Playbook
----------------

```
- hosts: all
  become: True
  roles:
    - azavea.pip
    - lae.docker
  vars:
    docker_restart_on_upgrade: no
    docker_compose_install: yes
```

Testing
-------

If you are attempting to use this role in Travis CI's environment in conjunction
with LXC containers, please note you will need to mount the correct cgroups as
Ubuntu 14.04 does not have the correct mappings for its LXC templates. Please
refer to the [`install.yml`](`tests/install.yml`) in this repo.
