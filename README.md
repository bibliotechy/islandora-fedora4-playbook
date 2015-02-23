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

**Reapply configuration**

```
vagrant provision
```

**Rebuild and redeploy sync**

```
# runs if there are upstream changes
ansible-playbook -i inventory-vagrant/hosts islandora.yml \
  --limit=sync --private-key=~/.vagrant.d/insecure_private_key
```

**Reinstall islf4 site**

```
ansible-playbook -i inventory-vagrant/hosts drush-si.yml \
  --private-key=~/.vagrant.d/insecure_private_key
```

_See play file for options._

**Running Ansible directly**

```
# using limit
ansible-playbook -i inventory-vagrant/hosts islandora.yml \
  --limit=database,webserver --private-key=~/.vagrant.d/insecure_private_key

# using tags
ansible-playbook -i inventory-vagrant/hosts islandora.yml \
  --tags=fuseki --private-key=~/.vagrant.d/insecure_private_key

# combined
ansible-playbook -i inventory-vagrant/hosts islandora.yml \
  --limit=database,webserver --tags=drupal --private-key=~/.vagrant.d/insecure_private_key
```

Future
------

- Ignore roles directory contents and use requirements file to download them
- Integrate (example) using cloud provider (i.e. AWS)
- Placeholder for persistent storage solution (glusterfs)?
- Test `vagrant` folder symlinks to source directories

---
