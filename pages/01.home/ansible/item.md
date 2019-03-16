---
title: Ansible
metadata:
    refresh: '30'
    generator: Grav
    description: 'Some useful Ansible tips and trikcs'
    keywords: 'Ansible, Linux, Server, Configuration, SSH, Automation'
    author: Allaman
taxonomy:
    category:
        - Linux
        - DevOps
---

## Run playbook without inventory file

```bash
ansible-playbook -i xxx.xxx.xxx.xxx, playbook.yml # be aware of the comma
```

## Get a list of facts

```bash
ansible -m setup localhost | sed '1c {' | jq '.ansible_facts | keys'
# alternatively | python -mjson.tool
```

## Ansible playbook waiting for reboot of target

! UPDATE: Since Ansible 2.7 there is a [reboot module](https://docs.ansible.com/ansible/devel/modules/reboot_module.html)

Sometimes a reboot of a machine during Ansible operation is required. Reboot results in a lost ssh connection.

Here is a way how to properly tell Ansible to handle a machines reboot in the middle of its operation without failing.

The following playbook snippet reconfigures the network (especially the IP), performs a reboot of the server while wating for it to come back with its new IP address. `host_name` and `ip_address` must be provided from a external call.

```yaml
---
- name: Configure interface
  template:
    src: etc/interfaces.j2
    dest: /etc/network/interfaces
    owner: root
    group: root
    mode: "u=rw,g=r,o=r"

- name: Set hostname
  hostname:
    name: '{{ host_name }}'
  tags: [hostname]

- name: Reboot Machine
  shell: sleep 2 && shutdown -r now "Ansible reboot"
  async: 1
  poll: 0
  ignore_errors: true

- name: Wait for the remote network interface to come back up
  local_action:
    module: wait_for
    host: "{{ ip_address }}"
    port: 22
    delay: 30
    timeout: 300
    state: started
  become: false
  register: wait_result

- name: Change ansible_ssh_host to new ip for further connections
  set_fact:
    ansible_ssh_host: "{{ ip_address }}"

- name: Interface configuration finished
  debug:
    msg: "Interface configuration finished"
  when: wait_result|succeeded
```