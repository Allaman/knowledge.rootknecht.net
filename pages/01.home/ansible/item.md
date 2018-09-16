---
title: Ansible
metadata:
    refresh: 30
    generator: 'Grav'
    description: 'Some useful Ansible tips and trikcs'
    keywords: 'Ansible, Linux, Server, Configuration, SSH, Automation'
    author: 'Allaman'
taxonomy:
    category:
        - DevOps
        - Linux
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