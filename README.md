# role_le-nginx

Ansible Playbook for nginx and letsencrypt


Wichtig: Definiere folgende variable:

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
 + Fedora 29 Server (needs [se_firewalld](https://github.com/DO1JLR/role_se_firewalld) role for SELINUX Policy)

 Variables:
------------
| variable | default value | function |
| -------- | ------------- | -------- |
| dns_name | - | used domain name for config and certificate |
| letsencrypt_email | ``info@{{ ansible_hostname }}`` | Lets Encrypt notify mail |
| gen_letsencrypt_certificate | ``false`` | Generate Letsencrypt or self signed cert |
| reverse_proxy | ``true`` | host files or be a reverse proxy |
| reverse_proxy_destination | ``http://127.0.0.1:3000`` | Where should the proxy point to? |
| nginx_default_server | ``false`` | Is this the default nginx site? (Use only once per server) |
| nginx_aliases | ``""`` | String with aditional vhost names |
| nginx_php | false | allow php |

 Example:
----------
You can use this role multiple times for different destinations:

```
- name: nginx server for example.com
  hosts: webserver01.example.com
  roles:
    - le-nginx
  tags:
   - web
   - config
  vars:
   - dns_name: "example.com"
   - gen_letsencrypt_certificate: false
   - reverse_proxy_destination: http://127.0.0.1:9001
```

