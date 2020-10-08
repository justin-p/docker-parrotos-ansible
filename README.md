# Parrot OS Ansible Test Image

[![Github Actions](https://img.shields.io/github/workflow/status/justin-p/docker-parrotos-ansible/CI?label=Github%20Actions&logo=github&style=flat-square)](https://github.com/justin-p/docker-parrotos-ansible/actions)
[![Docker Pulls](https://img.shields.io/docker/pulls/jperdok/docker-parrotos-ansible?logo=docker&style=flat-square)](https://hub.docker.com/r/jperdok/docker-parrotos-ansible)
[![Docker Size](https://img.shields.io/docker/image-size/jperdok/docker-parrotos-ansible?logo=docker&sort=date&style=flat-square)](https://hub.docker.com/r/jperdok/docker-parrotos-ansible)
[![Docker Stars](https://img.shields.io/docker/stars/jperdok/docker-parrotos-ansible?logo=docker&style=flat-square)](https://hub.docker.com/r/jperdok/docker-parrotos-ansible)
[![Docker Tag](https://img.shields.io/docker/v/jperdok/docker-parrotos-ansible?logo=docker&sort=date&style=flat-square)](https://hub.docker.com/r/jperdok/docker-parrotos-ansible)

Parrot OS Core Docker container for Ansible playbook and role testing. This is heavily based of the work done by [geerlingguy](https://github.com/geerlingguy).

## Tags

- `latest`: Latest stable version of Ansible, with Python 3.x.

## How to Build

This image is built on Docker Hub automatically any time the upstream OS container is rebuilt, and any time a commit is made or merged to the `master` branch. But if you need to build the image on your own locally, do the following:

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. `cd` into this directory.
  3. Run `docker build -t parrotos-ansible .`

## How to Use

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. Pull this image from Docker Hub: `docker pull URL HERE` (or use the image you built earlier, e.g. `parrotos-ansible`).
  3. Run a container from the image: `docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro URL HERE` (to test my Ansible roles, I add in a volume mounted from the current working directory with ``--volume=`pwd`:/etc/ansible/roles/role_under_test:ro``).
  4. Use Ansible inside the container:
    a. `docker exec --tty [container_id] env TERM=xterm ansible --version`
    b. `docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/ansible/playbook.yml --syntax-check`

## Notes

I use Docker to test my Ansible roles and playbooks on multiple OSes using CI tools like Github Actions and Molecule. This container allows me to test roles and playbooks using Ansible running locally inside the container.

> **Important Note**: I use this image for testing in an isolated environment—not for production—and the settings and configuration used may not be suitable for a secure and performant production environment. Use on production servers/in the wild at your own risk!
