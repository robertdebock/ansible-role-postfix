postfix
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-postfix.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-postfix)

Provides Postfix for your system.

Context
--------
This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Requirements
------------

Access to a repository containing packages, likely on the internet.

Role Variables
--------------

See defaults/main.yml

Dependencies
------------

You can use this role to prepare your system.

- robertdebock.bootstrap

Download the dependencies by issuing this command:
```
ansible-galaxy install --role-file requirements.yml
```

Example Playbook
----------------

```
- hosts: servers

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.postfix
```

Install this role using `galaxy install robertdebock.postfix`.

License
-------

Apache License, Version 2.0

Author Information
------------------

Robert de Bock <robert@meinit.nl>
