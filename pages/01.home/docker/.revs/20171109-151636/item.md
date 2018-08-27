---
title: 'Docker Tricks'
taxonomy:
    category:
        - Docker
---

## Prevent a container from exiting
After starting a service via docker-compose Docker will shut it down if there is no process running. To prevent that you can call a "dummy" endless command - in this case by overriding the entrypoint with a simple ping.
```yaml
entrypoint: ping localhost
```