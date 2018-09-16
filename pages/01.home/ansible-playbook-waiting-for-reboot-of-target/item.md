---
title: 'Ansible playbook waiting for reboot of target'
taxonomy:
    category:
        - DevOps
        - Linux
---

Sometimes a reboot of a machine during Ansible operation is required, e.g. when altering the network config (I am aware of the possibility of restarting the network service but I have made bad experiences regarding the reliability of this method). Nevertheless, reboot and restart of the network results in a lost ssh connection.

Here is a way how to properly tell Ansible to handle a machines reboot in the middle of its operation without failing.

The following playbook snippet reconfigures the network, performs a reboot of the server while wating for it to come back with its new IP address. `host_name` and `ip_address` must be provided from external call.

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

