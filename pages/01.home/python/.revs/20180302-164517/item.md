---
title: 'Python Tricks'
---

[TOC]

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

loggers = {}

def mylogger(name):
    global loggers

    if loggers.get(name):
        return loggers.get(name)
    else:
        logger = logging.getLogger(name)
        logger.setLevel(logging.DEBUG)
        handler = logging.StreamHandler()
        formatter = logging.Formatter(
            '%(asctime)s %(levelname)s %(module)s %(message)s')
        handler.setFormatter(formatter)
        logger.addHandler(handler)
        loggers.update(dict(name=logger))

        return logger
```
```python
from log import mylogger
logger = mylogger(__name__)
logger.info("TEXT")
logger.debug("!!!!")
```

## JSON
```python
import json

json.load(open(file.json, 'r'))
json.loads('{"hello": "world}')
```

## pip proxy
Windows `%APPDATA%\pip\pip.ini` (for use with pipenv)
```ini
[global]
    trusted-host = pypi.python.org
    proxy = http://[domain name]%5C[username]:[password]@[proxy address]:[proxy port]
```