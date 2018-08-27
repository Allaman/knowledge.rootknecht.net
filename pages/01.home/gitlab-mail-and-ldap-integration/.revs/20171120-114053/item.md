---
title: 'Gitlab Mail and LDAP Integration'
taxonomy:
    category:
        - Others
---

`gitlab.rb`

```ruby
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "<SMTP Host>"
gitlab_rails['smtp_port'] = "587"
gitlab_rails['smtp_user_name'] = "<user>"
gitlab_rails['smtp_password'] = "<password>"
gitlab_rails['smtp_authentication'] = "login"
gitlab_rails['smtp_enable_starttls_auto'] = true
gitlab_rails['smtp_openssl_verify_mode'] = 'none' # change if there are valid certificates
gitlab_rails['gitlab_email_from'] = "<MAIL FROM>"
gitlab_rails['gitlab_email_reply_to'] = "<REPLY TO>"

gitlab_rails['ldap_enabled'] = true

gitlab_rails['ldap_servers'] = {
'main' => {
  'label' => 'Description',
  'host' =>  '<LDAP-HOST',
  'port' => 389, # 636 for secured connection
  'uid' => 'sAMAccountName',
  'verify_certificates' => true,
  'bind_dn' => '<can be full bind or username>',
  'password' => '<password>',
  'method' => 'plain', # change for enrypted connections
  'base' => '<BASE DN>',
  'active_directory' => true, # true only for Microsoft AD
  'allow_username_or_email_login' => true,
  'user_filter' => '(&(objectCategory=Person)(sAMAccountName=*))'
  }
}
```