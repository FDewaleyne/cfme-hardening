Role Name
=========

cfme-hardening is a role meant to offer an alternative to appliance_console. It is an adaptation of the scap_rules.yml that is used with the linuxadmin gem by appliance_console and is heavily based on remediation snippets from https://static.open-scap.org/ (I try to put sources in each task file)

Requirements
------------

This is meant to be used on a CloudForms 5.0.11 (cfme-5.11.11) to replicate openscap hardening as done through appliance_config.

Role Variables
--------------

WIP
A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

WIP
A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

WIP
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

GPL V2

Author Information
------------------

For issues go to https://github.com/FDewaleyne/cfme-hardening/issues 
