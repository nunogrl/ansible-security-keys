Ansible Security Keys
=====================

Performs linux hardening and deploy the user keys as required.


Test
----

run vagrant with:

    vagrant up

and test another user with:

    ansible-playbook -i hosts.txt tests.yml


Handling users
--------------

There are 2 configurations for users, the `main_users` and the `serverusers`.

`main_users` are the ones you want to aknowledge their existence,
but you don't want to mess with them.

Examples of this are "ec2-user","git", etc

    main_users:
      - git
      - ansible
      - vagrant

`serverusers` are the users and keys you want to maintain: update and delete.

    serverusers:
      - donald
      - mickey

This will grab the keys from the files with the same name stored on the "users"
folder.

Notes:

- if the list is not provided, it creates a list from the all the users list.
- if there's no matching file for a user, the playbook will fail to execute.



Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should
be mentioned here. For instance, if the role uses the EC2 module, it may be
a good idea to mention in this section that the boto package is required.

Role Variables
--------------

SSH_PORT

    the ssh port. If not provided, it will remain 22


root_password

    the password to attempt if the user fails to login


main_users

    users to keep regardless the keys are present or absent


serverusers

    users to maintain

Dependencies
------------

none

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables
passed in as parameters) is always nice for users too:

    - hosts: servers
      become: yes
      become_method: sudo
      gather_facts: False
      vars:
        main_users:
          - ec2-user
          - git
        serverusers:
          - mickey
          - goofy
        hostname: tests
        SSH_PORT: 22
        root_password: "PleaseDontPutAnClearTextPasswordHere"
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information,
or a website (HTML is not allowed).
