# tower-openstack
> A set of playbooks for deploying and managing OpenStack with Ansible Tower.

The intent of this repo is to make it possible to drive installation and management of OpenStack with Ansible. Making actions performed by the [`openstack/openstack-ansible/scripts`](https://github.com/openstack/openstack-ansible/tree/master/scripts) bash scripts available via Ansible playbooks means that we can use them in Ansible Tower. The goal is to be able to provide a self-service portal that allows users to create their own OpenStack environments and then work with them, also using the operational playbooks provided by `openstack/openstack-ansible`.

## Usage
The `openstack.yml` playbook will deploy OpenStack using the official [`openstack-ansible`](https://github.com/openstack/openstack-ansible) playbooks. It simply clones a specified version of those playbooks and uses them to perform an install. The motivation behind this is to allow a tool like Ansible Tower to drive management activities for an OpenStack deployment.

1. create an inventory with the following host groups:
  - deploy-host
    - the host performing the deployment (set to localhost when using Tower)
  - target-hosts
    - the hosts OpenStack is being deployed to
    - these hosts will also be in other host groups, depending on which type of OpenStack node they are
2. override any role variables as desired
3. run `ansible-playbook -i inventory openstack.yml` or configure to run via Tower job template

## Goals
- never require a fork of `openstack/openstack-ansible`
- no *wrapping* of `openstack/openstack-ansible` playbooks
  - include them directly in `openstack.yml`
- `openstack.yml` should replace installation scripts
