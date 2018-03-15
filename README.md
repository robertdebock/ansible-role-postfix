postfix
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-postfix.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-postfix)

Provides Postfix for your system.

Context
--------
This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/robertdebock.github.io/artifacts/postfix.png "Dependency")

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

Basic configuration, using all defaults (See defaults/main.yml).
```
- hosts: servers

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.postfix
```

To configure postfix to relay all its email to a relayhost:
```
- hosts: servers

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.postfix
      postfix_relayhost: "[relay.example.com]"
```


To configure postfix to receive all mail for example.com:
```
- hosts: mailserver

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.postfix
      postfix_mydestination: "example.com, $mydomain, $myhostname, localhost.$mydomain, localhost"
```

To configure postfix to use spamassassin and clamav:
```
- hosts: mailserver

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.postfix
      postfix_mydestination: "example.com, $mydomain, $myhostname, localhost.$mydomain, localhost"
      postfix_spamassassin: enabled
      postfix_clamav: enabled
```

Install this role using `galaxy install robertdebock.postfix`.

License
-------

Apache License, Version 2.0

Author Information
------------------

Robert de Bock <robert@meinit.nl>
