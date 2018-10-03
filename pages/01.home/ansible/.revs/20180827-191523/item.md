---
title: Ansible
taxonomy:
    category:
        - DevOps
        - Ansible
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