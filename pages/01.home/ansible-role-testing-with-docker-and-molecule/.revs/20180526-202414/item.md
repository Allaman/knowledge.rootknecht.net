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
    A[Ansible Role] --> B[Molecule]
    A --> C(Round Rect)
    B --> D{Rhombus}
   C --> D
[/mermaid]


## Flow