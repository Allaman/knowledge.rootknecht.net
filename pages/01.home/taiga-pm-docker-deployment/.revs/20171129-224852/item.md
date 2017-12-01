---
title: 'Taiga PM Docker Deployment'
published: false
taxonomy:
    category:
        - Applications
    author:
        - Knecht
---

docker exec -it taigadocker_taigaback_1 bash
apt-get install vim
vim settings/common.py
MEDIA_URL = "http://project.rootknecht.net:8000/media/"
STATIC_URL = "http://project.rootknecht.net:8000/static/"
sh regenerate.sh

frontend/conf.json
api domain

admin url http://project.rootknecht.net:8080/admin/
