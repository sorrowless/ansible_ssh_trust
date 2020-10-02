# sbog/ssh-trust

[![Build Status](https://travis-ci.com/sorrowless/ansible_ssh_trust.svg?branch=master)](https://travis-ci.com/sorrowless/ansible_ssh_trust)
[![Ansible Role](https://img.shields.io/ansible/role/50937)](https://galaxy.ansible.com/sorrowless/ssh_trust)
[![Ansible Quality Score](https://img.shields.io/ansible/quality/50937)](https://galaxy.ansible.com/sorrowless/ssh_trust)
[![Ansible Role](https://img.shields.io/ansible/role/d/50937)](https://galaxy.ansible.com/sorrowless/ssh_trust)
[![GitHub](https://img.shields.io/github/license/sorrowless/ansible_ssh_trust)](https://github.com/sorrowless/ansible_ssh_trust/blob/master/LICENSE)

Role to achieve SSH confidence between nodes. After setup new nodes one of
which should reach other one, you get problem cause you have to go to the first
node and manually try to reach second one. You have to do that cause SSH daemon
will ask you to confirm target node fingerprint. In case you do not want to do
that manually, this role can help. You can just specify primary and secondary
nodes and run this role. For specified users on masters known_hosts will be
created automatically. This helps especially if you have many primary nodes or
have several groups of primary/secondary nodes.

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
