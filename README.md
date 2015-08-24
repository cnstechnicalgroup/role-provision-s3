Role: cns.provision-s3
========

Provision S3 and create / attach Bucket Policy to enable administrative account access.

Requirements
------------

Nothing, it runs out of the box.

Role Variables
--------------

In the current version, you can specify the following variables:

| Name               | Default |                                      |
|--------------------|---------|--------------------------------------|
| owner |   ---   | The client name for the project. |
| site_prefix |   ---   | Project short name (super-widgets.com = superwidgets) |
| mgmt_account |   ---   | The management AWS Account ID to enable cross account access |



Dependencies
------------

This package has no dependencies.

License
-------

GPLv2

Author Information
------------------

Created by [Sam Morrison](https://www.twitter.com/samcns)

Examples
--------

```yaml
---
- name: cns.provision-s3 example
  hosts: all
  roles:
    - cns.provision-s3
```
```yaml
# An S3 Bucket Policy is generated for modes (enviornment) defined in vars/main.yml
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "List Access",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::1234567890:root"
      },
      "Action": [
        "s3:ListBucket",
        "s3:GetBucketLocation"
      ],
      "Resource": "arn:aws:s3:::superwidgets-prod"
    },
    {
      "Sid": "Get Object Read Only",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::1234567890:root"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::superwidgets-prod/*"
    }
  ]
}
``
