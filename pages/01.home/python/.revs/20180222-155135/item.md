---
title: 'Python Tricks'
---

## Read file
```python
content = open(file, 'r').read()
lines = open(file, 'r').readline()
```

## Logging
```python
import logging

logging.basicConfig(level=logging.DEBUG)
logger = logging.getLogger(__name__)

logger.info("TEXT")
logger.debug("!!!!")
```

## JSON
```python
import json

json.load(open(path, 'r'))
json.loads('{"hello": "world}')
```