[![Build Status](https://travis-ci.org/infrastructr/ansible-role-rancher-cluster.svg?branch=master)](https://travis-ci.org/infrastructr/ansible-role-rancher-cluster)
[![Ansible Galaxy](https://img.shields.io/badge/role-infrastructr.rancher_cluster-blue.svg)](https://galaxy.ansible.com/infrastructr/rancher_cluster/)
[![GitHub tag (latest by date)](https://img.shields.io/github/v/tag/infrastructr/ansible-role-rancher-cluster)](https://galaxy.ansible.com/infrastructr/rancher_cluster)
[![Ansible Galaxy Downloads](https://img.shields.io/ansible/role/d/49672.svg?color=blue)](https://galaxy.ansible.com/infrastructr/rancher_cluster/)

# Ansible Role: Rancher Cluster

An Ansible Role that manages setup and configuration of [Rancher](https://rancher.com/docs/rancher/v2.x/en/installation/) clusters.

## Role Variables

Available variables listed below, along with default values (see `defaults/main.yml`):

    rancher_cluster_base_group: paas

Inventory group for all Rancher hosts.    
    
    rancher_cluster_master_group: paas_master

Inventory group for the Rancher master hosts.

    rancher_clusters:
      - name: cluster1
        group: cluster1
        network_provider: weave

Clusters to create with corresponding configuration and related groups.

    rancher_cluster_master_host: "{{ hostvars[groups[rancher_cluster_master_group][0]]['ansible_host'] }}"
    
Rancher API host.    
    
    rancher_cluster_master_url: "https://{{ rancher_cluster_master_host }}"
    
Rancher API URL.    
    
    rancher_cluster_validate_certs: no
  
Enable/disable SSL certificate validation when communicating with the Rancher API.

    rancher_cluster_network_provider_default: weave
    
Default network provider.

## Dependencies

- [geerlingguy.pip](https://galaxy.ansible.com/geerlingguy/pip)
- [geerlingguy.docker](https://galaxy.ansible.com/geerlingguy/docker)

## Example Playbook

    - hosts: all
      vars:
        pip_package: python3-pip
        pip_install_packages:
          - name: docker    
      roles:
        - geerlingguy.pip
        - geerlingguy.docker 
        
    - hosts: paas_master
      roles:
        - infrastructr.rancher_master
        - infrastructr.rancher_cluster

## Development

Use [docker-molecule](https://github.com/infrastructr/docker-molecule) following the instructions to run [Molecule](https://molecule.readthedocs.io/en/stable/)
or install [Molecule](https://molecule.readthedocs.io/en/stable/) locally (not recommended, version conflicts might appear).

Provide Hetzner Cloud token:

    export HCLOUD_TOKEN=123abc456efg

Use following to run tests:

    molecule test --all

## Maintainers

- [build-failure](https://github.com/build-failure)

## License

See the [LICENSE.md](LICENSE.md) file for details.

## Author Information

This role was created in 2020 by [infrastructr](https://github.com/infrastructr) team.
