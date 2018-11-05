<a href='https://travis-ci.org/shinken-monitoring/mod-auth-active-directory'><img src='https://api.travis-ci.org/shinken-monitoring/mod-auth-active-directory.svg?branch=master' alt='Travis Build'></a>
mod-auth-active-directory
=========================

Shinken module for UI authentification with Active Directory or OpenLDAP

### Disclaimer
This documentation is taken from [shinken-webui-wiki](https://github.com/shinken-monitoring/mod-webui/wiki)

## How to use

This module allows to lookup passwords into both Active Directory or OpenLDAP entries.

How to install:
```
$ shinken install auth-active-directory
```

How to configure:
```
$ cat /etc/shinken/modules/auth_active_directory.cfg
[...]

## Module:      auth-active-directory
## Loaded by:   WebUI
## Usage:       Uncomment and set your value in ldap_uri
# Check authentification for WebUI using an Active Directory server.
define module {
    module_name     auth-active-directory
    module_type     ad_webui
    #ldap_uri        ldaps://myserver
    username        user
    password        password
    basedn          DC=google,DC=com

    # For mode you can switch between ad (active dir)
    # and openldap
    mode            ad
}
```

Change “adserver” by your own dc server, and set the “user/password” to an account with read access on the basedn for searching the user entries.

Change “mode” from “ad” to “openldap” to make the module ready to authenticate against an OpenLDAP directory service.

WARNING : Be aware that you'll also need a contact file in order for your auth to work.

For example, if you have on your AD or LDAP the following credentials :
```
login : corentin
password : secret
```

Then you'll need to have a contact card like the following :
```
define contact{
    use             generic-contact
    contact_name    corentin
    contactgroups   admin,users
    email           shinken@localhost
    pager           0000000000  ; contact phone number
    is_admin        1
    expert      1
}
```
