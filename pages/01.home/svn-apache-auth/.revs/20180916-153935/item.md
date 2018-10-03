---
title: SVN+Apache+Auth
taxonomy:
    category:
        - Application
---

Setup SVN accessable through Apache with local + ldap authentication and user based authorization

## Create svn repo
```bash
svnadmin create path/to/repo
chown -R www-data:www-data path/to/repo # adjust apache user if needed
# optionally dump and import existing repo
svnadmin dump file:///path/to/exisitngt > repo.dump
svnadmin load /path/to/repo < repo.dump
```

## Setup Apache
Install/enable `mod_dav_svn`, `mod_authz_svn`, and `mod_authnz_ldap`

Add location to your `apache.conf`:
```ini
 <Location /repo>
        Options                    Includes Indexes FollowSymLinks ExecCGI
        AllowOverride              None
        Order                      allow,deny
        Allow                      from all
        AuthType                   basic
        AuthName                   "SVN Repo Auth"
        AuthzSVNAccessFile         /path/to/authz
        require                    valid-user
        DAV                        svn
        SVNPath                    /path/to/repo
        SVNReposName               "SVN Repo"
        SVNAllowBulkUpdates        on
        SVNCacheRevProps           on

        AuthBasicAuthoritative     off
        AuthBasicProvider          ldap file # provide multiple auth provider
        AuthUserFile               /path/to/passwd
        AuthzLDAPAuthoritative     off
        AuthLDAPDereferenceAliases never
        AuthLDAPBindDN             "CN=svn_user,OU=svn,DC=example,DC=com"
        AuthLDAPBindPassword       "password"
        AuthLDAPURL                "ldap://ldap.example.com/OU=svn users,DC=example,DC=com?sAMAccountName?sub?(&(objectClass=user))"
    </Location>
```

## Setup local users

```bash
htpasswd -c /path/to/passwd USER
```

## Setup authorization

Edit ` /path/to/authz` according to the following scheme:

```ini
[aliases]
TMU     = muellet
MHU     = hummelm
MGO     = gomezm

[groups]
ADM     = &TMU,&MHU
MGO     = &MGO

[/]
@ADM    = rw
*       = r

[/all.md]
@FK     = rw
@ADM    = rw
*       =

[/ADM]
@ADM    = rw
*       =
[/MGO]
@ADM    = rw
@MGO    = rw
*       =
```

