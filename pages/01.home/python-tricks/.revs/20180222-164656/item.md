---
title: 'Python Tricks'
---

## Read file
```python
try:
	content = open(file, 'r').read()
	lines = open(file, 'r').readline()
except IOError as err:
    print(err)
    sys.exit()
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

json.load(open(file.json, 'r'))
json.loads('{"hello": "world}')
```