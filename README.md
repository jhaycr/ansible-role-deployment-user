Ansible Role: Deployment User
=========

An Ansible role that installs a deployment user, by default 'ansible', for further Ansible interactions to use rather than the existing user.

The 'deployment-user-create' tasks can be used with the 'root' account to:
(1) create an SSH key for the deployment user on the local machine.
(2) create the deployment user on the remote machine.
(3) push the SSH key to the remote machine.
(4) add the deployment user to the remote machine's sudoers group.

The 'deployment-user-destroy' tasks can be used to reverse actions 2-4 on the remote machine.

Requirements
------------

None

Role Variables
--------------

See `defaults/main.yml`.


Dependencies
------------

Relies on Ansible community collections:
* community.crypto.openssh_keypair
* community.general.sudoers

Example Playbook
----------------

### bootstrap-deployment-user-create.yml

```
---
- name: Create deployment user for ansible
  hosts: all

  roles:
    - role: jhaycr.deployment_user

  vars:
    deployment_user_state: present
    deployment_user_name: ansible
    deployment_user_sudo: true
    deployment_user_sudo_passwordless: true
    deployment_user_public_key_files:
      - ~/.ssh/ansible.pub
    ansible_ssh_user: root 
```


### bootstrap-deployment-user-destroy.yml

```
---
- name: Remove deployment user for ansible
  hosts: all

  roles:
    - role: jhaycr.deployment_user

  vars:
    deployment_user_state: absent
    deployment_user_name: ansible
    ansible_ssh_user: root 
```


License
-------

MIT

Author Information
------------------

Josh Haycraft