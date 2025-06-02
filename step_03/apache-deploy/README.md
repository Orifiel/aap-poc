Role Name
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).

Para criação do execution environment 

1 - Crie arquivo pip.conf com o conteudo:
[global]
index=https://artifactory.py.example.com/artifactory/api/pypi/pypi-remote/pypi
index-url=https://artifactory.py.example.com/artifactory/api/pypi/pypi-remote/simple
trusted-host=artifactory.py.example.com

2 - Crie a pasta context, e resida o arquivo pip.conf nele.

3 - Obtenha as imagens de container abaixo
# podman pull registry.redhat.io/ansible-automation-platform-23/ansible-builder-rhel8:latest
# podman pull registry.redhat.io/ansible-automation-platform-23/ee-29-rhel8:latest

4 - Crie o execution-environment.yml fora da pasta context/
---
version: 3
images:
  base_image:
    name: 'registry.redhat.io/ansible-automation-platform-23/ee-minimal-rhel8:latest'
dependencies:
  galaxy: requirements.yml
  python: requirements.txt

5 - Crie o arquivo requirements.yaml (indicando quais são as collections)
---
collections:
  - name: ansible.posix
  - name: ansible.utils
  - name: community.general

6 - Execute o comando 
$ ansible-builder create

7 - Execute o comando
$ podman build -f context/Containerfile -t custom:latest context
