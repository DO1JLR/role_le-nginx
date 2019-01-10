# role_le-nginx

Ansible Playbook for nginx and letsencrypt


Wichtig: Definiere folgende variable:

```yaml
dns_name
```

 What it currently does:
------------------------

+ Update System
+ 
+ Generate self signed SSL-Certificate or LE-Certificate
+ configure nginx to forward http to https
+ configure nginx to make a reverseproxy to Port 3000 (e.g. used for gitea)


 Tested on:
-----------
 + Fedora 29 Server (needs [se_firewalld](https://github.com/DO1JLR/role_se_firewalld) role for SELINUX Policy)

