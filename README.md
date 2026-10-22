# Phansible Role: Solr

[![CI](https://github.com/phansible/role-solr/actions/workflows/ci.yml/badge.svg)](https://github.com/phansible/role-solr/actions/workflows/ci.yml)

An Ansible Role that installs [Solr](https://solr.apache.org/) on Ubuntu and Debian specifically created with [Phansible](http://phansible.com/) in mind.

## Requirements

- Ubuntu 22.04, 24.04, 26.04 or Debian 12, 13 (x86_64)
- Ansible >= 2.15

Solr is installed from the official Apache release tarball (verified against its published SHA-512) and runs on the distro's default OpenJDK as a systemd service.

## Role Variables

| Variable | Default | Description |
| --- | --- | --- |
| `solr_version` | `9.11.0` | Solr release to install. |
| `solr_filename` | `solr-{{ solr_version }}` | Release archive name, also the directory created under `/opt`. |
| `solr_filename_extension` | `.tgz` | Release archive extension. |
| `solr_path` | `/opt/solr` | Symlink pointing at the installed release. |
| `solr_user` | `solr` | System user that owns and runs Solr. |
| `solr_url` | `https://archive.apache.org/dist/solr/solr/{{ solr_version }}` | Where the archive and its `.sha512` are downloaded from. |
| `solr_var_path` | `/var/solr` | Holds `solr.in.sh`; Solr home is `{{ solr_var_path }}/data`. |
| `solr_port` | `'8983'` | HTTP port. |
| `solr_cloud_mode` | `'0'` | Set to `'1'` to start in SolrCloud mode against ZooKeeper on `localhost:2181`. |

Logs go to `/var/log/solr`. Solr 9 listens on `127.0.0.1` only by default; set `SOLR_JETTY_HOST` in `{{ solr_var_path }}/solr.in.sh` to expose it.

## Dependencies

None. For SolrCloud mode, run ZooKeeper on the same host, for example with [role-zookeeper](https://github.com/phansible/role-zookeeper).

## Example Playbook

```yaml
- hosts: search
  become: yes
  roles:
    - role-solr
```

## License

This role is released under the terms of the license specified in the repository or if not specified, under the [MIT license](https://raw.githubusercontent.com/phansible/role-solr/master/LICENSE).

## Author Information

This role was created in 2015 by [The Phansible Team & Contributors](https://github.com/phansible/role-solr/graphs/contributors), credits go also to [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/) and source of inspiration.
