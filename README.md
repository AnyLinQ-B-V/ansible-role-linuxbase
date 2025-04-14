# Ansible Role: Linux Base

[![CI](https://github.com/AnyLinQ-B-V/ansible-role-linuxbase/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/AnyLinQ-B-V/ansible-role-linuxbase/actions/workflows/ci.yml)
[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)

An Ansible role to configure base system settings for Linux servers. This role handles common system configurations including:

- Python interpreter setup
- System timezone configuration
- Hostname management
- Package repository configuration
- Base package installation
- Virtualization support packages
- System updates
- SSH server configuration
- User and group management
- Distribution-specific configurations

## Requirements

- Ansible 2.10 or higher
- Python 3.x on target hosts
- Root or sudo access on target hosts

## Supported Platforms

- Debian 12 (Bookworm)
- Debian 13 (Trixie)
- Ubuntu 22.04 LTS (Jammy)
- Ubuntu 24.04 LTS (Noble)
- RHEL/Rocky Linux 9

## Role Variables

```yaml
# Python interpreter configuration
check_python_interpreter:
  debian:
    other: '/usr/bin/python3'
  ubuntu:
    other: '/usr/bin/python3'
  redhat:
    other: '/usr/bin/python3'

# SSH Configuration
ssh:
  configure: true
  port: "{{ ansible_port }}"
  allow_root: false
  auth_pwd: true
  auth_pubkey: true

# Repository Configuration
repo:
  provider: 'debian.org'  # alternatives: 'hetzner.com'
  security_updates: true
```

See [defaults/main.yml](defaults/main.yml) for all available variables.

## Dependencies

- `ansibleguy.linux_users` (for user and group management)

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: anylinq.linuxbase
      vars:
        hostname: "webserver01"
        timezone: "Europe/Amsterdam"
        ssh:
          configure: true
          port: 22
          allow_root: false
```

## Tags

- `always`: Tasks that should always run
- `system`: System configuration tasks
- `timezone`: Timezone configuration
- `hostname`: Hostname configuration
- `packages`: Package management tasks
- `repositories`: Repository configuration
- `virtualization`: VM-specific package installation
- `updates`: System update tasks
- `ssh`: SSH configuration
- `security`: Security-related tasks
- `users`: User management tasks
- `groups`: Group management tasks
- `auth`: Authentication configuration
- `config`: Distribution-specific configurations

## Testing

```bash
# Test the role using molecule
molecule test

# Test specific distribution
MOLECULE_DISTRO=debian12 molecule test
```

## License

MIT

## Changelog

See [CHANGELOG.md](https://github.com/AnyLinQ-B-V/ansible-role-linuxbase/blob/main/CHANGELOG.md) for a list of all notable changes to this project.

## Security

Please see our [Security Policy](https://github.com/AnyLinQ-B-V/ansible-role-linuxbase/blob/main/SECURITY.md) for reporting vulnerabilities.

## Contributing

Please read our [Contributing Guide](https://github.com/AnyLinQ-B-V/ansible-role-linuxbase/blob/main/CONTRIBUTING.md) and our [Code of Conduct](https://github.com/AnyLinQ-B-V/ansible-role-linuxbase/blob/main/CODE_OF_CONDUCT.md) before submitting a Pull Request.

---

<div align="center">
Created and maintained by <a href="https://www.anylinq.com">AnyLinQ B.V.</a><br/><br/>
<a href="https://www.anylinq.com"><img src="https://anylinq.com/hubfs/AnyLinQ%20transparant.png" width="120" alt="AnyLinQ Logo"/></a>
</div>