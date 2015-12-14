Ansible role: Jenkins
=====================

Installs a standalone Jenkins server using the internal database for authentication (matrix-based).

It can also .create administrator users and install additional plugins.

At the moment of installation, the hostname you pass through jenkins_hostname must be reachable and pointing to the server where Jenkins will be running (because some checks and operations are run against it during the installation).

Ideally, Jenkins should be listening only to localhost (127.0.0.1) while nginx or some other web server acts as a frontend.

Requirements
------------

None

Role Variables
--------------

    jenkins_listen_address: 127.0.0.1
    jenkins_hostname: localhost
    jenkins_port: 8080
    
    jenkins_handler_max: 100
    jenkins_handler_idle: 20
    
    jenkins_allow_signups: false
    
    jenkins_admins:         # format: [ username, password ]
      - ['admin','admin']
    
    jenkins_cli_jar: /opt/jenkins/jenkins-cli.jar
    jenkins_home: /var/lib/jenkins
    jenkins_java_cmd: ''
    jenkins_user: jenkins
    jenkins_java_options: "-Djava.awt.headless=true"
    jenkins_debug_level: 5
    jenkins_access_log: no
    jenkins_args: ''
    
    jenkins_conn_retries: 60
    jenkins_conn_delay: 10
    
    jenkins_plugins:
      - git-client 
      - git

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

Created by [Giovanni Tirloni](http://gtirloni.com)

