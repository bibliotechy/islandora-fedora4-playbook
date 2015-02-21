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
# using limit
ansible-playbook -i inventory-vagrant/hosts islandora.yml --limit=webserver --private-key=~/.vagrant.d/insecure_private_key

# using tags
ansible-playbook -i inventory-vagrant/hosts islandora.yml --tags=fuseki --private-key=~/.vagrant.d/insecure_private_key

# combined
ansible-playbook -i inventory-vagrant/hosts islandora.yml --limit=webserver --tags=drupal --private-key=~/.vagrant.d/insecure_private_key
```

Future
------

- Ignore roles directory contents and use requirements file to download them
- Integrate (example) using cloud provider (i.e. AWS)

---
