# NFS role

An [Ansible Galaxy](https://galaxy.ansible.com/) role for configuring persistent NFS filesystem mounts.

## Table of contents

* [NFS Configuration][1]
* [Role variable configuration][2]
* [Hashicorp Vault configuration][3]
* [Example Requirements File][4]
* [Example Playbook][5]
* [License][6]

[1]: #nfs-configuration
[2]: #role-variable-configuration
[3]: #hashicorp-vault-configuration
[4]: #example-requirements-file
[5]: #example-playbook
[6]: #license

## NFS Configuration

NFS filesystem mounts are configured in one of two ways using the variables `nfs_mounts_config` or `nfs_mounts_vault_path` and configuration will be sourced from the role variable itself or a Hashicorp Vault secret respectively. The sections that follow describe the use of these variables in more detail.

### Role variable configuration

> [!NOTE]
> The optional `nfs_mounts_config` variable described here is mutually exlusive with the `nfs_mounts_vault_path` variable.

Use the optional `nfs_mounts_config` variable to configure the NFS filesystems for this role via a group/host variable. If set, the `nfs_mounts_config` variable should be defined as a list of dictionaries and each dictionary supports the following parameters:

| Name          | Default             | Description                                                                           |
|---------------|---------------------|---------------------------------------------------------------------------------------|
| `path`        |                     | The path on the remote system being provisioned which will be used as the mount point for the NFS filesystem. |
| `src`         |                     | The source of the NFS filesystem in the form of the hostname or IP address of the NFS server and the directory being exported (e.g. `1.2.3.4:/exported`). |
| `opts`        | `hard,bg,nfsvers=4` | _Optional_. Any options for the NFS filesystem to be added to the filesystem table configuration file (i.e. `/etc/fstab`) in the form of a single comma-separated string. |
| `symlink`     |                     | _Optional_. An optional path to a symbolic link that will be created and which will point to the `path` specified. |

### Hashicorp Vault configuration

> [!NOTE]
> The `nfs_mounts_vault_path` variable described here is mutually exlusive with the `nfs_mounts_config` variable.

Use the optional `nfs_mounts_vault_path` variable to configure the NFS filesystems for this role via a Hashicorp Vault secret. If set, the `nfs_mounts_vault_path` variable should contain the path to a Hashicorp Vault secret containing a JSON object of the following format:

```json
{
  "nfs_mounts": [
    {
      "opts": "<filesystem-options>",
      "path": "<mount-path>",
      "src": "<nfs-source>",
      "symlink": "<symbolic-link-path>"
    }
  ]
}
```

The `nfs_mounts` attribute should contain an array with zero or more objects whose key names correspond to those documented in the in the [Role variable configuration][2] section above.

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

- name: Provision NFS mounts
  hosts: all
  roles:
    - role: companieshouse.general.nfs_mounts
```

## License

This project is subject to the terms of the [MIT License](LICENSE).
