Islandora / Fedora4 playbook
============================

A minimal playbook to install Islandora / Fedora4 as development progresses.

Requirements
------------

- Virtualbox
- Vagrant
- Ansible

Quickstart
----------

The vagrant configuration will install all components onto a single VM.

```
vagrant up
```

Running Ansible directly
------------------------

**Example:**

```
ansible-playbook -i inventory islandora.yml --tags=fuseki --private-key=~/.vagrant.d/insecure_private_key
```

---
