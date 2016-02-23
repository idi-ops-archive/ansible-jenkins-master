Ansible role: Jenkins
=====================

Installs a standalone Jenkins server using the internal database for authentication (matrix-based).

It can also .create administrator users and install additional plugins.

At the moment of installation, the hostname you pass through jenkins_hostname must be reachable and pointing to the server where Jenkins will be running (because some checks and operations are run against it during the installation).

Ideally, Jenkins should be listening only to localhost (127.0.0.1) while nginx or some other web server acts as a frontend.

The role uses the following [Ansible tags](http://docs.ansible.com/ansible/playbooks_tags.html) to control the provisioning process:

* ``install`` - installs Jenkins software using package managers and startup files if necessary
* ``configure`` - sets up Jenkins cli command, adds the ``deploy`` user to use with [Jenkins job builder] (http://docs.openstack.org/infra/jenkins-job-builder/), updates existing plugins and install the plugins listed in the variable ``jenkins_plugins`` and finally sets the permissions usign a Groovy script.
* ``deploy`` - enable and start a Systemd unit if a VM or physical machine is being used or in the case of Docker, add a Supervisor config
* ``test`` - check the application's HTTP endpoint for a response to confirm it is working and check if Jenkins is working pulling the list of plugins using Jenkins-cli.

Requirements
------------

* [Ansible facts](https://github.com/idi-ops/ansible-facts)

Role Variables
--------------

* ``jenkins_admins`` - List of administration credentials, it contains a list of pairs [ 'adminuser', 'password' ]

Please refer to the [defaults/main.yml](defaults/main.yml) file for a list of variables along with additional documentation.

Example Playbook
----------------

```
---


- name: Configure Jenkins test server
  hosts: localhost

  roles:
    - role: facts
    - role: jenkins
        jenkins_hostname: localhost
        jenkins_port: 8080
        jenkins_admins:
          - ['user1', 'password1']
          - ['user2', 'password2']
        jenkins_plugins:
          - git-client
          - git
          - publish-over-ssh
          - nodejs

```
License
-------

MIT

Author Information
------------------

* Inclusive Design Research Centre (OCAD University)
* Raising the floor - International

