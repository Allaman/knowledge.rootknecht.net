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
graph TD
    A[Ansible Role] <-- B(Molecule)
    B --> C[Docker Container]
    C --> D
    B --> D[Play Playbook]
    D --> E
    B --> E[Testinfra]
    E --> F
    B --> F[Clean up]
[/mermaid]


## Flow