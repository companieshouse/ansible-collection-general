# Ansible Role: systemd-journald 

An [Ansible Galaxy](https://galaxy.ansible.com/) role for configuring systemd-journald.

## Table of contents

* [Configuration][1]
* [Example Requirements File][2]
* [Example Playbook][3]
* [License][4]

[1]: #configuration
[2]: #example-requirements-file
[3]: #example-playbook
[4]: #license

## Configuration

All configuration is managed through group/host variables. The following variables should be defined to override defaults where necessary:

| Name           | Default             | Description                                                                           |
|----------------|---------------------|---------------------------------------------------------------------------------------|
| `systemd_journald_storage_mode` | `persistent` | Controls where to store journal data. One of `volatile`, `persistent`, `auto` and `none`. See `journald.conf(5)` for more information. |

## Example Requirements File

```yml
- src: https://github.com/companieshouse/ansible-role-systemd-journald
  name: systemd-journald
  version: "n.n.n"
```

## Example Playbook

```yml
    - hosts: servers
      roles:
        - systemd-journald
```

## License

This project is subject to the terms of the [MIT License](/LICENSE).
