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

Rules and values applied
------------------------
The following scap rules and values are enforced :
* System Settings
  * Account and Access Control
    * Protect Accounts by Configuring PAM
      * xccdf_org.ssgproject.content_rule_display_login_attempts
      * Set Password Quality Requirements
        * Set Password Quality Requirements with pam_pwquality
          * xccdf_org.ssgproject.content_value_var_password_pam_dcredit: 1
          * xccdf_org.ssgproject.content_rule_accounts_password_pam_dcredit
          * xccdf_org.ssgproject.content_value_var_password_pam_difok: 4
          * xccdf_org.ssgproject.content_rule_accounts_password_pam_difok
          * xccdf_org.ssgproject.content_value_var_password_pam_ucredit: 1
          * xccdf_org.ssgproject.content_rule_accounts_password_pam_ucredit
          * xccdf_org.ssgproject.content_value_var_password_pam_ocredit: 1
          * xccdf_org.ssgproject.content_rule_accounts_password_pam_ocredit
          * xccdf_org.ssgproject.content_value_var_password_pam_lcredit: 1
          * xccdf_org.ssgproject.content_rule_accounts_password_pam_lcredit
    * Protect Physical Console Access
      * xccdf_org.ssgproject.content_rule_require_singleuser_auth
      * xccdf_org.ssgproject.content_rule_grub2_disable_interactive_boot
    * Protect Accounts by Restricting Password-Based Login
      * Set Password Expiration Parameters
        * xccdf_org.ssgproject.content_value_var_accounts_maximum_age_login_defs: 60
        * xccdf_org.ssgproject.content_rule_accounts_maximum_age_login_defs
        * xccdf_org.ssgproject.content_value_var_accounts_minimum_age_login_defs: 1
        * xccdf_org.ssgproject.content_rule_accounts_minimum_age_login_defs
        * xccdf_org.ssgproject.content_value_var_accounts_password_minlen_login_defs: 14
        * xccdf_org.ssgproject.content_rule_accounts_password_minlen_login_defs
      * Restrict Root Logins
        * xccdf_org.ssgproject.content_rule_securetty_root_login_console_only
      * Set Account Expiration Parameters
        * xccdf_org.ssgproject.content_value_var_account_disable_post_pw_expiration: 35
        * xccdf_org.ssgproject.content_rule_account_disable_post_pw_expiration
    * Secure Session Configuration Files for Login Accounts
      * xccdf_org.ssgproject.content_value_var_accounts_max_concurrent_login_sessions: 10
      * xccdf_org.ssgproject.content_rule_accounts_max_concurrent_login_sessions
  * System Accounting with auditd
    * xccdf_org.ssgproject.content_rule_grub2_audit_argument
    * Configure Auditd Rules for Comprehensive Auditing
      * xccdf_org.ssgproject.content_rule_audit_rules_mac_modification
      * xccdf_org.ssgproject.content_rule_audit_rules_sysadmin_actions
      * xccdf_org.ssgproject.content_rule_audit_rules_usergroup_modification
      * Record Unauthorized Access Attempts Events to Files (unsuccessful)
        * xccdf_org.ssgproject.content_rule_audit_rules_unsuccessful_file_modification
      * Record Information on Kernel Modules Loading and Unlodaing
        * xccdf_org.ssgproject.content_rule_audit_rules_kernel_module_loading
      * Record Events that Modify Date and Time Information
        * xccdf_org.ssgproject.content_rule_audit_rules_time_adjtimex
        * xccdf_org.ssgproject.content_rule_audit_rules_time_clock_settime
        * xccdf_org.ssgproject.content_rule_audit_rules_time_settimeofday
        * xccdf_org.ssgproject.content_rule_audit_rules_time_watch_localtime
    * Network Configuration and Firewalls
      * Uncommon Network Protocols
        * xccdf_org.ssgproject.content_rule_kernel_module_dccp_disabled
        * xccdf_org.ssgproject.content_rule_kernel_module_sctp_disabled
      * IPv6
        * Configure IPv6 Settings if Necessary
          * xccdf_org.ssgproject.content_value_sysctl_net_ipv6_conf_default_accept_redirects: 0
          * xccdf_org.ssgproject.content_rule_sysctl_net_ipv6_conf_default_accept_redirects
      * Kernel Parameters Which Affect Networking
        * Network Parameters for Hosts Only
          * xccdf_org.ssgproject.content_rule_sysctl_net_ipv4_conf_all_send_redirects
          * xccdf_org.ssgproject.content_rule_sysctl_net_ipv4_conf_default_send_redirects
        * Network Related Kernel Runtime Parameters for Hosts and Routers
            * xccdf_org.ssgproject.content_value_sysctl_net_ipv4_icmp_ignore_bogus_error_responses_value: 1
            * xccdf_org.ssgproject.content_rule_sysctl_net_ipv4_icmp_ignore_bogus_error_responses
            * xccdf_org.ssgproject.content_value_sysctl_net_ipv4_conf_default_accept_redirects_value: 0
            * xccdf_org.ssgproject.content_rule_sysctl_net_ipv4_conf_default_accept_redirects
            * xccdf_org.ssgproject.content_value_sysctl_net_ipv4_conf_all_accept_redirects_value: 0
            * xccdf_org.ssgproject.content_rule_sysctl_net_ipv4_conf_all_accept_redirects
            * xccdf_org.ssgproject.content_value_sysctl_net_ipv4_conf_all_rp_filter_value: 1
            * xccdf_org.ssgproject.content_rule_sysctl_net_ipv4_conf_all_rp_filter
            * xccdf_org.ssgproject.content_value_sysctl_net_ipv4_conf_default_secure_redirects_value: 0
            * xccdf_org.ssgproject.content_rule_sysctl_net_ipv4_conf_default_secure_redirects
            * xccdf_org.ssgproject.content_value_sysctl_net_ipv4_conf_all_secure_redirects_value: 0
            * xccdf_org.ssgproject.content_rule_sysctl_net_ipv4_conf_all_secure_redirects
            * xccdf_org.ssgproject.content_value_sysctl_net_ipv4_conf_all_accept_source_route_value: 0
            * xccdf_org.ssgproject.content_rule_sysctl_net_ipv4_conf_all_accept_source_route
            * xccdf_org.ssgproject.content_value_sysctl_net_ipv4_conf_all_log_martians_value: 1
            * xccdf_org.ssgproject.content_rule_sysctl_net_ipv4_conf_all_log_martians
            * xccdf_org.ssgproject.content_value_sysctl_net_ipv4_icmp_echo_ignore_broadcasts_value: 1
            * xccdf_org.ssgproject.content_rule_sysctl_net_ipv4_icmp_echo_ignore_broadcasts
    * File Permissions and Masks
      * Restrict Programs from Dangerous Execution Patterns
        * Disable Core Dumps
          * xccdf_org.ssgproject.content_rule_disable_users_coredumps
      * Restrict Dynamic Mounting and Unmounting of...
        * xccdf_org.ssgproject.content_rule_service_autofs_disabled
* Services
  * Cron and At Daemons
    * xccdf_org.ssgproject.content_rule_service_atd_disabled
  * SSH Server
  * xccdf_org.ssgproject.content_value_sshd_idle_timeout_value: 900
    * Configure OpenSSH Server if Necessary
      * xccdf_org.ssgproject.content_rule_sshd_set_keepalive
      * xccdf_org.ssgproject.content_rule_sshd_do_not_permit_user_env
      * xccdf_org.ssgproject.content_rule_sshd_disable_empty_passwords
      * xccdf_org.ssgproject.content_rule_sshd_use_approved_ciphers
      * xccdf_org.ssgproject.content_rule_sshd_set_idle_timeout


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
