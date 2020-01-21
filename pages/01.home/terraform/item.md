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

## Manage AWS security groups

! Terraform &ge; 0.12 required due to `for_each` functionality

```
locals {
  cidr_to_sg_rules = {
    icmp_ping = {
      type        = "ingress"
      protocol    = "icmp"
      from_port   = -1
      to_port     = -1
      cidr_blocks = [var.ping_cidr]
    }
    icmp_pong = {
      type        = "egress"
      protocol    = "icmp"
      from_port   = -1
      to_port     = -1
      cidr_blocks = [var.egress_cidr]
    }
    http_out = {
      type        = "egress"
      protocol    = "tcp"
      from_port   = 80
      to_port     = 80
      cidr_blocks = [var.egress_cidr]
    }
    https_out = {
      type        = "egress"
      protocol    = "tcp"
      from_port   = 443
      to_port     = 443
      cidr_blocks = [var.egress_cidr]
    }
  }
  sg_to_sg_rules = { for id in var.ssh_security_group_ids :
    id => {
      type         = "ingress"
      protocol     = "tcp"
      from_port    = 22
      to_port      = 22
      source_sg_id = id
    }
  }
}

resource "aws_security_group_rule" "cidr_to_sg" {
  for_each          = local.cidr_to_sg_rules
  type              = each.value["type"]
  protocol          = each.value["protocol"]
  from_port         = each.value["from_port"]
  to_port           = each.value["to_port"]
  cidr_blocks       = each.value["cidr_blocks"]
  security_group_id = module.foo.security_group_id
}

resource "aws_security_group_rule" "sg_to_sg" {
  for_each                 = local.sg_to_sg_rules
  type                     = each.value["type"]
  protocol                 = each.value["protocol"]
  from_port                = each.value["from_port"]
  to_port                  = each.value["to_port"]
  source_security_group_id = each.value["source_sg_id"]
  security_group_id        = module.foo.security_group_id
}
```

## Using for_each

! Terraform &ge; 0.12 required

```
operators =   {
  "Max_Mustermann" = "system:masters",
  "Michaela_Musterfrau" = "system:masters"
}
```

```
resource "aws_iam_user" "operators" {
  for_each = var.operators
  name  = each.key
  path  = "/${var.cluster_name}/"

  tags = {
    "group" = each.value
  }
}
```

```
data "external" "operator_map" {
  for_each = var.operators
  program = ["python", "${path.module}/map.py"]

  query = {
    user_arn = aws_iam_user.operators[each.key].arn
    username = aws_iam_user.operators[each.key].name
    group    = each.value
  }
}
```

```
output "users" {
  value = [for value in data.external.operator_map: value.result]
}
```