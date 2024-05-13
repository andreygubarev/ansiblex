# `getansible.sh` - self-contained, standalone, and reproducible Ansible installation

## Getting Started

You can use `install.sh` to download and execute `getansible.sh`:
```bash
curl -sL https://getansible.sh/ | bash
```

Additionally, you can specify the Ansible release to install (e.g. `9.0`):
```bash
curl -sL https://getansible.sh/ | ANSIBLE_RELEASE=9.0 bash
```

Or, you can execute Ansible commands using curl piping:
```bash
curl -sL https://getansible.sh/ | bash -s -- ansible-playbook playbook.yml
```

Also, you can specify `--link` to create system-wide symlinks:
```bash
curl -sL https://getansible.sh/ | bash -s -- install --link
```

After linking, you can execute Ansible commands:
```bash
ansible-playbook playbook.yml
```

Alternatively, you can download distribution of `getansible.sh` from the [releases page](https://github.com/andreygubarev/getansible/releases):
```bash
curl -fsSL https://github.com/andreygubarev/getansible/releases/download/v0.3.5/getansible-9.0-amd64.sh -o /usr/local/bin/getansible.sh
chmod +x /usr/local/bin/getansible.sh
```

Then, you can execute Ansible commands:
```bash
getansible.sh -- ansible-playbook playbook.yml
```

### Prerequisites

`getansible.sh` requires `bash`, `sed` and `tar` to be installed on the system.

Additionally, if you are using curl piping, you need:
- `curl` to download the script, and CA certificates to verify the download


### Configuration

You can configure the following environment variables:

`GETANSIBLE_PATH` - Path to install `getansible.sh` (default: `/usr/local/bin/getansible.sh`):
```bash
curl -sL https://getansible.sh/ | GETANSIBLE_PATH=/opt/getansible.sh bash
```

`ANSIBLE_RELEASE` - Ansible release to install (default: `9.0`):
```bash
curl -sL https://getansible.sh/ | ANSIBLE_RELEASE=9.0 bash
```

`TMPDIR` - Temporary directory to extract Ansible (default: `/tmp`):
```bash
curl -sL https://getansible.sh/ | TMPDIR=/opt/ bash
```
`getansible.sh` requires at least 1GB of free space in the temporary directory. You may need to change default `TMPDIR` if you have limited space in `/tmp`.

## Overview

`getansible.sh` is a shell script that contains a self-extracting archive of Ansible (including dependencies) and Python interpreter. It is designed to be executed on any Linux machine without the need to install packages or dependencies.

Supported Ansible Versions:

| Release | Ansible | Ansible Core | Python |
|---------|---------|--------------|--------|
| 3.0     | 3.4.0   | 2.10.17      | 3.8.19 |
| 4.0     | 4.10.0  | 2.11.12      | 3.8.19 |
| 5.0     | 5.10.0  | 2.12.10      | 3.8.19 |
| 6.0     | 6.7.0   | 2.13.13      | 3.8.19 |
| 7.0     | 7.7.0   | 2.14.16      | 3.11.9 |
| 8.0     | 8.7.0   | 2.15.11      | 3.11.9 |
| 9.0     | 9.5.1   | 2.16.6       | 3.11.9 |

Supported Linux with GLIBC 2.17 or later:

- `Debian` starting from `8` (`jessie`)
- `Ubuntu` starting from `14.04` (`trusty`)
- `Fedora` starting from `21`
- `openSUSE` starting from `13.2`
- `RHEL` or `CentOS` starting from `7`

Note: Linux distributions with MUSL (e.g. Alpine) are not supported.

Supported Platforms:

- `amd64`
- `arm64`

## Motivation

Author always wanted Ansible to be distributed as a single binary, so it can be easily executed on any Linux machine without the need to install packages or dependencies.

Setting up Ansible using package manager means sticking to the version provided by the OS, which always lags behind the latest release. Setting up Ansible using Python package manager means relying on the PYPI repository, which may be down.

Thus, `getansible.sh` was created to provide a self-contained, standalone (isolated and portable), and reproducible Ansible installation.

### Criticism of Curl Piping

- https://0x46.net/thoughts/2019/04/27/piping-curl-to-shell/
- https://gnu.moe/wallofshame.md

Author believes that curl piping is acceptable for downloading and executing scripts, as long as the script is open-source and the source code is available for review. In this case, transparency is sufficient to ensure good faith.

For those who are still concerned (and rightfully so), `getansible.sh` can be downloaded directly from the [releases page](https://github.com/andreygubarev/getansible/releases) and executed locally.

# Reference

The project is possible only because of the following tools:

- [Ansible](https://www.ansible.com/)
- [Makeself](https://makeself.io/)
- [python-build-standalone](https://github.com/indygreg/python-build-standalone)

Additional references:

- [Ansible Releases Explained](https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html)
- [Linux Support Explained](https://gregoryszorc.com/docs/python-build-standalone/20220227/running.html#linux)
- [Python Lifecycle](https://devguide.python.org/versions/#versions)
