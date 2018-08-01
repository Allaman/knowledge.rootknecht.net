---
title: 'Ansible role testing with Docker and Molecule'
taxonomy:
    category:
        - Ansible
        - DevOps
        - Docker
    author:
        - Knecht
---

## Requirements

1. Ansible
1. Docker
3. pip install molecule, docker-py, testinfra

## Big Picture

[mermaid]
graph LR
    A[Ansible Role] --> B((Molecule))
        click A "https://www.ansible.com/" "Ansible Homepage"
        click B "https://github.com/metacloud/molecule" "Molecule Homepage"
    B --> C[Docker Container]
        click B "https://www.docker.com/" "Docker Homepage"
    B --> D[Play Playbook]
    B --> E[Testinfra]
       click B "https://github.com/philpep/testinfra" "Testinfra Homepage"
    B --> F[Clean up]
[/mermaid]


## Flow