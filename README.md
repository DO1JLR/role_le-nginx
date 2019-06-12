 Ansible role le-nginx
==========================
[![Build Status](https://travis-ci.org/DO1JLR/role_le-nginx.svg?branch=master)](https://travis-ci.org/DO1JLR/role_le-nginx)
Ansible Playbook for nginx and letsencrypt

```
WARNING

THIS ROLE IS  A LITTLE BIT OUTDATED.
PLEASE  BE CAREFULLY  BY  USING  IT.
IT  IS  HIGHLY RECOMENDED  TO USE  A
BETTER NGINX CONFIGURATION ROLE THAN
THESE HERE!  REALLY!!!  DO  NOT  USE
```

### Wichtig: Definiere folgende variable:

```yaml
dns_name
```

 What it currently does:
------------------------

+ Update System
+ Install needed packages like nginx or some python modules 
+ Generate self signed SSL-Certificate or LE-Certificate
+ configure nginx to forward http to https
+ configure nginx to make a reverseproxy to Port 3000 (e.g. used for gitea)
+ Generate DHPARAMS (improved TLS Entropie) 

 Tested on:
-----------
 + Fedora 29 Server (may need [se_firewalld](https://github.com/DO1JLR/role_se_firewalld) role for SELINUX Policy)
 + Debian 9 (no dependencies)

For the PHP part of this playbook I used [this](https://github.com/DO1JLR/role_se_php) ansible role.

 Variables:
------------
| variable          | default value | function |
| --------          | ------------- | -------- |
| dns_name          | -  | used domain name for config and certificate |
| letsencrypt_email | ``info@{{ ansible_hostname }}`` | Lets Encrypt notify mail |
| gen_letsencrypt_certificate | ``false`` | Generate Letsencrypt or self signed cert |
| copy_own_certificate        | ``false`` | Copy your own custom certificate to the webserver |
| skip_dhaparam     | ``true`` | Should we skip generating good crypto? **NOT RECOMENDED** |
| reverse_proxy     | ``true`` | host files or be a reverse proxy |
| reverse_proxy_destination | ``http://127.0.0.1:3000`` | Where should the proxy point to? |
| nginx_default_server | ``false`` | Is this the default nginx site? (Use only once per server) |
| nginx_aliases     | ``""`` | String with aditional vhost names |
| nginx_php         | ``false`` | enable php config |
| nginx_dokuwiki    | ``false`` | enable custom dokuwiki config |
| basic_auth        | ``false`` | authentification via basic auth? |
| htpasswd.name     | ``alice`` | default basic auth name |
| htpasswd.pw       | - | basic auth password |
| le_custom_certificate | - | The Path where your custom certificate is located. This file may include the intermediate certificate too! |
| le_custom_privatekey  | - | The Path where your custom private cert is  located |

 Example:
----------
Hint: You can use this role multiple times for different destinations on the same host:

```yaml
- name: nginx server for example.com
  hosts: webserver01.example.com
  roles:
    - le-nginx
  tags:
   - web
   - config
   - nginx
   - le-nginx
  vars:
   - dns_name: "example.com"
   - nginx_default_server: false
   - gen_letsencrypt_certificate: false
   - skip_dhparam: false
   - reverse_proxy_destination: http://127.0.0.1:8443
   - copy_own_certificate: false
```

