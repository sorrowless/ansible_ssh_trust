# sbog/ssh-trust

[![Ansible Role](https://img.shields.io/ansible/role/50937)](https://galaxy.ansible.com/sorrowless/ssh_trust)
[![Build Status](https://travis-ci.com/sorrowless/ansible_ssh_trust.svg?branch=master)](https://travis-ci.com/sorrowless/ansible_ssh_trust)
[![Ansible Quality Score](https://img.shields.io/ansible/quality/50937)](https://galaxy.ansible.com/sorrowless/ssh_trust)
[![Ansible Role](https://img.shields.io/ansible/role/d/50937)](https://galaxy.ansible.com/sorrowless/ssh_trust)
[![GitHub](https://img.shields.io/github/license/sorrowless/ansible_ssh_trust)](https://github.com/sorrowless/ansible_ssh_trust/blob/master/LICENSE)

Role to achieve SSH confidence between nodes. After some time of software
deployment I stuck with interesting problem. There are cases when you need to
deploy software to several nodes where one node will behave like master and
will go to other nodes and fetch some data from them by SSH protocol. For
example if you deploy a backup solution based on Rsnapshot, it will go from
backup node to all the nodes which are needed to be backuped and try to get
some data from them. Or in case of AutoSSH usage some nodes will go to other
nodes. In both of these cases to avoid password authentication you have to
generate and use SSH keys. And there you will stuck into the problem - if there
are many nodes then you'll have to do a bunch of manual work to generate keys,
place them to proper places and add SSH fingerprints also. With this role you
can achieve all of these automatically.

## Requirements

Ansible 2.4

## Role Variables

You can see all vars in `default/main.yml` vars file.

## Dependencies

None

## Example Playbook

```yaml
- name: Set the confidence between hosts
  hosts: ssh_trust_servers
  remote_user: root

  roles:
    - ssh_trust
```

Also you have to know that as you have masters and slaves in the root of this
then you have to place masters firt in your inventory to give them opportunity
to generate private keys and place them to proper places. So, your inventory
can look like this:

```
[ssh_trust_masters]
master_host_1
master_host_2

[ssh_trust_slaves]
slave_host_1
slave_host_2

[ssh_trust_servers:children]
ssh_trust_masters
ssh_trust_slaves
```

Beware that you don't have to have these group names as they are aren't used as
base to search public ssh key material.

## License

Apache 2.0

## Author Information

This role was created by [Stan Bogatkin](https://sbog.ru).
