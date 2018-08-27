---
title: 'Ansible role testing with Docker and Molecule'
taxonomy:
    category:
        - Ansible
        - DevOps
        - Docker
---

## Requirements

1. Ansible
1. Docker
3. pip install molecule, docker-py, testinfra

## Big Picture

[mermaid]
graph LR
    A[Ansible Role] --> B(Molecule)
    B --> C[Docker Container]
    B --> C[Play Playbook]
    B --> C[Testinfra]
    B --> C[Clean up]
[/mermaid]


## Flow