# Ansible Role: systemd-tmpfiles 

An [Ansible Galaxy](https://galaxy.ansible.com/) role for configuring `systemd-tmpfiles(8)` cleanup of files and directories in `/tmp`.

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

| Name                        | Default             | Description                                                                           |
|-----------------------------|---------------------|---------------------------------------------------------------------------------------|
| `systemd_tmpfiles_age`      | `1d`                | Used to decide what files to delete from `/tmp` when cleaning. If a file or directory is older than the current time minus the age value, it is deleted. |
| `systemd_tmpfiles_filename` | `tmp.conf`          | The name of the configuration file to create in `/etc/tmpfiles.d`. This should be the same name as the configuration files installed by vendor packages in `/usr/lib/tmpfiles.d` or `/run/tmpfiles.d` containing an entry for the `/tmp` directory to be overridden. |
| `systemd_tmpfiles_type`     | `v`                 | The type consists of a single letter and optionally one or more modifier characters: a plus sign ("+"), exclamation mark ("!"), minus sign ("-"), equals sign ("="), tilde character ("~") and/or caret ("^"). See `tmpfiles.d(5)` for more information. |

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

- name: Provision systemd-tmpfiles age
  hosts: all
  roles:
    - role: companieshouse.general.systemd_tmpfiles
```

## License

This project is subject to the terms of the [MIT License](LICENSE).
