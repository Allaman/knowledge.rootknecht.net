---
title: Terraform
taxonomy:
    category:
        - Programming
        - DevOps
---

## TF exclude targets

Terraform allows to specify target modules by the `--target` option. Unfortunately, there is no option to apply everything but a certain module. The following script iterates through the directory and filters all modules. From this result a string is constructed to perform a Terraform command that excludes some target modules.

```python
#!/usr/bin/env python3
"""
This script walks recursively through a given directory (default './')
and reads all .tf files looking for 'module "FOO"' lines.
From these results and the given module names to be excluded a target string
to be used for Terraform commands printed to stdout
"""
__version__ = "1.0.0"

import argparse
import os
import re


def main(args):
    """ entry point """
    m = re.compile(r'^module "(.*?)"')
    modules = set()
    for root, dirs, files in os.walk(args.path):
        files[:] = [f for f in files if f.endswith('.tf')]
        for file in files:
            with open(os.path.join(root, file), 'r') as f:
                content = f.read()
                if m.match(content):
                    modules.add(m.match(content).group(1))
    excludes = set(args.modules)
    print(' '.join(['--target module.' + t for t in (modules-excludes)]))


if __name__ == "__main__":
    """ Executed from the commandline"""
    parser = argparse.ArgumentParser(
        description='Generate --target string from excluded modules')
    parser.add_argument('-p',
                        '--path',
                        action='store',
                        default="./",
                        help='Path of your TF root')
    parser.add_argument(
        '-v',
        action='version',
        version='%(prog)s (version {version})'.format(version=__version__))
    parser.add_argument('modules', metavar='M', type=str, nargs='+',
                        help='Name of the modules to be exlcuded')
    args = parser.parse_args()
    main(args)
```