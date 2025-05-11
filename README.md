# Molecule Debian Docker Image

This repository contains a Dockerfile for creating a Debian-based container with `systemd` support. It is designed for testing with Molecule and mimics the default setup of a Raspberry Pi's admin user.

## Features

- Based on `debian:bookworm-slim`.
- Includes `systemd`, `curl`, `openssh-server`, and `sudo`.
- Removes unnecessary services to allow `systemd` to run inside the container.
- Creates an `admin` user with:
  - Username: `admin`
  - Password: `1234`
  - Sudo privileges.
- Configures SSH with password authentication enabled.
- Exposes port `22` for SSH access.

## Usage

To build the Docker image:

```sh
docker build -t molecule-debian .
```

To run the container:

```sh
docker run --privileged -d -p 2222:22 -v "/sys/fs/cgroup:/sys/fs/cgroup:ro" molecule-debian
```

## Notes

- The `admin` user is configured with a weak password (`1234`) for testing purposes. **Do not use this image in production.**