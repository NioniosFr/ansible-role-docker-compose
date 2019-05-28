Ansible Role: Docker Compose
=========

An ansible role to install [docker-compose](https://github.com/docker/compose) from GitHub Releases in a Linux x86_64 based system.

Requirements
------------

The role targets Debian and RHEL based systems build on the `x86_64` architecture.

The role is intended to run on the remote machine, which means that internet connectivity on remote is required.

The [docker](https://www.docker.com/) engine has to be installed on the target machine for `docker-compose` to function correctly.

Role Variables
--------------

Default:

```yaml
docker_compose_version: "1.24.0" # The version to install

docker_compose_user: "docker" # The owner of the binary (should match the docker user)
docker_compose_group: "docker" # The group owning the binary (should match the docker group)
docker_compose_dest: "/usr/local/bin" # The location to place the binary
docker_compose_cmd_name: "docker-compose" # The name of the command (in case you need multiple parallerl docker-compose versions installed!?)

docker_compose_configure_system_path: false # Whether the `docker_compose_dest` directory should be added to the system `PATH`
docker_compose_system_path_prepend: false # Whether to append or prepend the `docker_compose_dest` directory into the `PATH`, IF (docker_compose_configure_system_path is True).
```

Dependencies
------------

The role has no dependencies but, `docker-compose` is dependent on the [docker](https://www.docker.com/) engine.

Suggested role for installing docker on RHEL based systems: [nioniosfr.docker_ce](https://galaxy.ansible.com/nioniosfr/docker_ce).

Example Playbook
----------------

```yaml
    - hosts: localhost
      roles:
        - role: nioniosfr.docker_compose # Installs the default configured version

        - role: nioniosfr.docker_compose # Install a RC version
          vars:
            docker_compose_version: "1.25.0-rc1"

        - role: nioniosfr.docker_compose # Installs the default configured version in '/opt/docker-compose' and sets a `profile.d` file to setup the system path
          vars:
            docker_compose_version: "1.22.0"
            docker_compose_name: "docker-compose-122"
            docker_compose_binary_dest: "/opt/docker-compose"
            docker_compose_configure_system_path: true
```

License
-------

MIT

Author Information
------------------

[NioniosFr](https://github.com/NioniosFr)
