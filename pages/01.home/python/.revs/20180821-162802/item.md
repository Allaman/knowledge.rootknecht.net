---
title: Python
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

## Upgrade all pip packages
```bash
sudo pip freeze --local | grep -v '"'"'^\-e'"'"' | cut -d = -f 1  | xargs -n1 sudo pip install -U
```

## pip proxy
Windows `%APPDATA%\pip\pip.ini` /  Linux pip.conf
```ini
[global]
    proxy = http://[domain name]%5C[username]:[password]@[proxy address]:[proxy port]
```

## pip certificate validation

**pip**
```bash
pip install [--index-url=http://pypi.org/simple/] --trusted-host pypi.org
```
or in pip.ini (windowns) / pip.conf (linux)
```ini
[global]
trusted-host = pypi.python.org
               pypi.org
               files.pythonhosted.org
```
or provide certificate (in pem format) with `pip3 --cert path/to/cert install PACAKGE`

**conda**
```bash
conda config --set ssl_verify false
```

## LDAP testing
```python
#!/usr/bin/env python

from ldap3 import Server, Connection, ALL

def ldap_initialize(server, port, user, password):
    """
    Simple ldap conncection test function
        :param server: mail server address
        :param port: mail server port
        :param user: user to auth
        :param password: password to auth
    """

    s = Server(server, port, get_info=ALL)
    # define the connection
    c = Connection(s, user, password, auto_bind='NONE', version=3, authentication='SIMPLE', \
    client_strategy='SYNC', auto_referrals=True, check_names=True, read_only=True, lazy=False, raise_exceptions=False)
    # perform the Bind operation
    if not c.bind():
        print('error in bind', c.result)
```

## SMTP testing

```python
import smtplib

from email.mime.text import MIMEText

def send_mail(host, me, you, user, password):
    """
   Send a test mail containing a simple ASCII message
        :param host: mail server + port
        :param me: sender address
        :param you: receiver mail address
        :param user: user to auth
        :param password: password to auth
    """
    msg = MIMEText("Hello World!")
    msg['Subject'] = 'Test mail from Python'
    msg['From'] = me
    msg['To'] = you

    s = smtplib.SMTP(host)
    s.set_debuglevel(True)
    s.login(user, password)
    s.sendmail(me, [you], msg.as_string())
    s.quit()
```

## Generate sha1 password
For example for Jupyter notebooks credentials
```python
In [1]: from IPython.lib import passwd
In [2]: passwd()
```
