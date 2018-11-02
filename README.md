postfix
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-postfix.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-postfix)

Installs and configures postfix on your system. This role can be used for any type of SMTP server:
- relayhost
- endpoint
- locally accepting


Example Playbook
----------------

This example is taken from `molecule/default/playbook.yml`:
```
---
- name: Converge
  hosts: all
  become: true
  gather_facts: false

  roles:
    - robertdebock.bootstrap
    - robertdebock.postfix

```

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```
---
# defaults file for postfix

# These settings are required in postfix.
postfix_myhostname: "{{ ansible_fqdn }}"
postfix_mydomain: "{{ ansible_domain | default ('localdomain', true) }}"
postfix_myorigin: "{{ ansible_domain | default ('localdomain', true) }}"

# To "listen" on public interfaces, set inet_interfaces to something like
# "all" or the name of the interface, such as "eth0".
postfix_inet_inferfaces: "loopback-only"

# The distination tells Postfix what mails to accept mail for.
postfix_mydestination: $mydomain, $myhostname, localhost.$mydomain, localhost

# To accept email from other machines, set the mynetworks to something like
# "192.168.0.0/24".
postfix_mynetworks: "127.0.0.0/8"

# These settings change the role of the postfix server to a relay host.
# postfix_relay_domains: "$mydestination"

# If you want to forward emails to another central relay server, set relayhost.
# use brackets to sent to the A-record of the relayhost.
# postfix_relayhost: [relay.example.com]

# Set the restrictions for receiving mails.
postfix_smtpd_recipient_restrictions:
  - permit_mynetworks
  - permit_sasl_authenticated
  - reject_unauth_destination
  - reject_invalid_hostname
  - reject_non_fqdn_hostname
  - reject_non_fqdn_sender
  - reject_non_fqdn_recipient
  - reject_unknown_sender_domain
  - reject_unknown_recipient_domain
  - reject_rbl_client sbl.spamhaus.org
  - reject_rbl_client cbl.abuseat.org
  - reject_rbl_client dul.dnsbl.sorbs.net
  - permit

# To enable spamassassin, ensure spamassassin is installed,
# (hint: role: robertdebock.spamassassin) and set these two variables:
# postfix_spamassassin: enabled
# postfix_spamassassin_user: spamd

# To enable clamav, ensure clamav is installed,
# (hint: role: robertdebock.clamav) and set this variable:
# postfix_clamav: enabled

# To update all packages installed by this roles, set `postfix_package_state` to `latest`.
postfix_package_state: present

```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the last 3 release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

---
- robertdebock.bootstrap


Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/postfix.png "Dependency")


Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.4|ansible 2.5|ansible 2.6|ansible 2.7|ansible devel|
|------------|-----------|-----------|-----------|-----------|-------------|
|alpine-edge*|yes|yes|yes|yes|yes*|
|alpine-latest|yes|yes|yes|yes|yes*|
|archlinux|yes|yes|yes|yes|yes*|
|centos-6|yes|yes|yes|yes|yes*|
|centos-latest|yes|yes|yes|yes|yes*|
|debian-latest|yes|yes|yes|yes|yes*|
|debian-stable|yes|yes|yes|yes|yes*|
|debian-unstable*|yes|yes|yes|yes|yes*|
|fedora-latest|yes|yes|yes|yes|yes*|
|fedora-rawhide*|yes|yes|yes|yes|yes*|
|opensuse-leap|yes|yes|yes|yes|yes*|
|opensuse-tumbleweed|yes|yes|yes|yes|yes*|
|ubuntu-artful|yes|yes|yes|yes|yes*|
|ubuntu-devel*|yes|yes|yes|yes|yes*|
|ubuntu-latest|yes|yes|yes|yes|yes*|

A single star means the build may fail, it's marked as an experimental build.

Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-postfix) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-postfix/issues)

To test this role locally please use [Molecule](https://github.com/metacloud/molecule):
```
pip install molecule
molecule test
```
There are many specific scenarios available, please have a look in the `molecule/` directory.


License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
