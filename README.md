Ansible role: Jenkins
=====================

Installs a standalone Jenkins server using the internal database for authentication (matrix-based).

It can also .create administrator users and install additional plugins.

At the moment of installation, the hostname you pass through jenkins_hostname must be reachable and pointing to the server where Jenkins will be running (because some checks and operations are run against it during the installation).

Ideally, Jenkins should be listening only to localhost (127.0.0.1) while nginx or some other web server acts as a frontend.

The role uses the following [Ansible tags](http://docs.ansible.com/ansible/playbooks_tags.html) to control the provisioning process:

* ``install`` - install software using package managers and (not recommended) using source 
* ``configure`` - add user accounts, groups, make filesystem related changes, clone git repositories, run application commands, etc.
* ``deploy`` - enable and restart a Systemd unit if a VM or physical machine is being used or in the case of Docker, add a Supervisor config
* ``test`` - check the application's HTTP endpoint for a response to confirm it is working

Requirements
------------

None

Role Variables
--------------

Please refer to the [defaults/main.yml](defaults/main.yml) file for a list of variables along with additional documentation.

Example Playbook
----------------

    ---
    - name: Configure Jenkins servers
      hosts: localhost
      become: yes

      roles:

        - role: jenkins
          jenkins_hostname: ci.example.com
          jenkins_admins:
            - ['user1','password']
            - ['user2','password2']
          jenkins_plugins:
            - git-client
            - git
            - publish-over-ssh
            - nodejs

License
-------

MIT

Author Information
------------------

* Created by [Giovanni Tirloni](http://gtirloni.com)
* Some changes by [Alfredo Matas](http://www.alfredomatas.es)

