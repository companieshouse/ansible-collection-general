# Ansible Role: systemd-journald 

An [Ansible Galaxy](https://galaxy.ansible.com/) role for configuring `systemd-journald` service storage mode.

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

All configuration is managed through group/host variables. The following variables can be defined to override the default values when necessary:

| Name           | Default             | Description                                                                           |
|----------------|---------------------|---------------------------------------------------------------------------------------|
| `systemd_journald_storage_mode` | `persistent` | Controls where to store journal data. One of `volatile`, `persistent`, `auto` and `none`. See `journald.conf(5)` for more information. |

## Example Requirements File

```yml
---

collections:
  - name: companieshouse.general
    version: "1.0.0"
```

## Example Playbook

```yml
---

- name: Provision systemd-journald configuration storage mode
  hosts: all
  roles:
    - role: companieshouse.general.systemd_journald
```

## License

This project is subject to the terms of the [MIT License](LICENSE).
