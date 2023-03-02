# Ansible Role for Nomad

Install and configure Nomad with Ansible.

The [Contributing Guide](CONTRIBUTING.md) explains how to work with and
contribute to this repository.

## [Example Playbook](#example-playbook)

This example is taken from
[`molecule/default/converge.yml`](https://github.com/robertdebock/ansible-role-nomad/blob/master/molecule/default/converge.yml)
and is tested on each push, pull request and release.

```yaml
---
- name: converge
  hosts: all
  become: true
  gather_facts: true

  roles:
    - role: remerge.nomad
```

The machine needs to be prepared. In CI this is done using
[`molecule/default/prepare.yml`](https://github.com/robertdebock/ansible-role-nomad/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  gather_facts: false
  become: true

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.core_dependencies
    - role: robertdebock.hashicorp
```

Also see a [full explanation and
example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use
these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/robertdebock/ansible-role-nomad/blob/master/defaults/main.yml):

```yaml
---
# defaults file for nomad

# You can install nomad using a package in this role. If you have installed
# nomad manually, set this to `no`.
nomad_install_package: true

# Common configuration
nomad_name: "{{ inventory_hostname_short }}"
nomad_region: global
nomad_datacenter: dc1

nomad_config_dir: /etc/nomad.d
nomad_data_dir: /opt/nomad/data
nomad_log_level: INFO

nomad_bind_addr: "0.0.0.0"
nomad_advertise_addr: "{{ ansible_default_ipv4.address }}"

# ACL settings
nomad_acl_enabled: false

# Vault integration settings
nomad_vault_enabled: false
nomad_vault_url: "http://vault.service.consul:8200"

# Configuration for server nodes
nomad_server: false
nomad_server_bootstrap_expect: 1

# Configuration for client nodes
nomad_client: false
nomad_client_node_class: worker
nomad_client_host_volumes: []
nomad_client_host_networks: []
```
