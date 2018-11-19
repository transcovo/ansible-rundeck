# Ansible Rundeck Role

This is an [Ansible](http://www.ansible.com/) role to install, configure and ensure sure rundeck is running.
Feedback, bug-reports, requests are welcomed and can be done via [github issues](https://github.com/New-Edge-Engineering/ansible-rundeck/issues).

## Execution Requirements
- Tested on Mac OS X with Ansible 1.7.

## Role Variables

The following variables can be overridden:

 * `rundeck_version`: Package version to install, default to latest available.
 * `rundeck_protocol`: Defaults to http but should be set to the protocol the web application with accessed by.
 * `rundeck_domain`: Defaults to localhost:4440 but should be set to the host name web application with accessed by.
 * `rundeck_ssl_terminated_proxy`: Default: False. Is Rundeck running behind a transparent SSL-enabled reverse proxy? See [Using an SSL Terminated Proxy](http://rundeck.org/docs/administration/configuring-ssl.html#using-an-ssl-terminated-proxy)
 * `rundeck_database_type`: Defaults to hsqldb but can be set to postgresql or mysql to use those databases. Users and databases are not automatically created.
 * `rundeck_database_host`: Defaults to localhost and only needs to be set if using an externally hosted database.
 * `rundeck_database_port`: Defaults to None and must be set if using a different database than the default hsqldb.
 * `rundeck_database_name`: Defaults to rundeck but allows you to use a different rundeck database name.
 * `rundeck_database_user`: Defaults to rundeck but allows you to use a different username to accesses the rundeck database.
 * `rundeck_database_pass`: Defaults to rundeck but allows you to use a different password for the user access to the rundeck database.
 * `rundeck_users`: A list of dictionaries of name, password ([hashed](http://rundeck.org/docs/administration/authenticating-users.html#propertyfileloginmodule)) and a list of roles (One must be an admin). If empty the default admin is not removed.
 * `rundeck_plugins`: A list of plugin urls that are downloaded and installed into the rundeck libext, default is none.
 * `rundeck_generate_ssh`: Automatically generate ssh key, default `True` set to `False` to stop this action.
 * `rundeck_ssh_key_type`: Default: 'rsa'. Available SSH key types will depend on implementation present on target host.
 * `rundeck_ldap`: Determine if LDAP authentication should be used, overrides rundeck_users. Default is False. The LDAP server must have a `user` group to provide access to rundeck web interface.
 * `rundeck_ldap_url`: The location of the LDAP server, i.e. ldap://localhost:389
 * `rundeck_ldap_bind_user`: The DN to access the LDAP server, i.e. cn=Manager,dc=example,dc=com
 * `rundeck_ldap_bind_pass`: The DN user password o access the LDAP server, secrent
 * `rundeck_ldap_google`: Default: False. Install stunnel to use Google Secure LDAP
 * `rundeck_ldap_google_crt`: Certificate to authenticate to  Google Secure LDAP
 * `rundeck_ldap_google_key`: Key to authenticate to  Google Secure LDAP
 * `rundeck_ldap_user_dn`: The DN of the users, i.e. ou=People,dc=test1,dc=example,dc=com
 * `rundeck_ldap_user_rdn_attr`: The attribute that identifies the username, i.e. uid
 * `rundeck_ldap_user_id_attr`: The attribute that identifies the username, i.e. uid
 * `rundeck_ldap_bindinglogin`: Default: false. If true, bind as the user that is authenticating, otherwise bind as the manager and perform a search to verify user password
 * `rundeck_ldap_bindingLoginUseRootContextForRoles`: Default: false. If true and forceBindingLogin is true, then role membership searches will be performed in the root context, rather than in the bound user context.
 * `rundeck_ldap_user_pass_attr`: The attribute that identifies the user password, i.e. userPassword
 * `rundeck_ldap_user_filter`: The objectClass that is used to find user, i.e. account
 * `rundeck_ldap_role_dn`: The DN of the roles, i.e. ou=Groups,dc=test1,dc=example,dc=com
 * `rundeck_ldap_role_name_attr`: The attribute name of the role, i.e. cn
 * `rundeck_ldap_role_username_attr`: This overrides the `rundeck_ldap_role_member_attr` determine user membership of roles, i.e. uid
 * `rundeck_ldap_role_member_attr`: Used to determine user membership of roles, i.e. member
 * `rundeck_ldap_role_filter`: The objectClass that is used to find role, i.e. groupOfNames
 * `rundeck_ldap_netsted_groups`: Default: false. If true, will resolve all nested groups for authenticated users
 * `rundeck_ldap_debug`: Default: false. Enable/Disable ldap debuging
 * `rundeck_multiauth`: Default: false. Enable/Disable multiauthentication (LDAP and using realm.properties file)
 * `rundeck_security_authorization_preauthenticated_enabled`: ""
 * `rundeck_security_authorization_preauthenticated_attributename`: ""
 * `rundeck_security_authorization_preauthenticated_delimiter`: ""
 * `rundeck_security_authorization_preauthenticated_usernameheader`: ""
 * `rundeck_security_authorization_preauthenticated_userrolesheader`: ""
 * `rundeck_security_authorization_preauthenticated_redirectlogout`: ""
 * `rundeck_security_authorization_preauthenticated_redirecturl`: ""

## Dependencies
This role does not have a hard dependency on any other role to deploy but rundeck does require java to be installed (decoupled on the communities request). smola's [ansible-java-role](https://github.com/smola/ansible-java-role) is a good choice with the
following configuration:

 * **Debian:** Ensure java_packages has a debian java package in it, i.e. openjdk-7-jre-headless
 * **RedHat:** Ensure java_packages has a debian java package in it, i.e. java-1.7.0-openjdk, had to adjust role to include RedHat.yml in main.yml to work.

If you choose to use a database then please ensure it is installed before executing this role. The following roles have been used to create databases:

 * **Ubuntu 12.04 & 14.04/PostgreSQL:** [postgresql](https://galaxy.ansible.com/list#/roles/512)
 * **Centos 6.5 & 7.0/PostgreSQL:** [postgresql-on-el6](https://galaxy.ansible.com/list#/roles/766) (with tweeks, watch this space for updates)

## License

Licensed under the MIT License. See the LICENSE file for details.
