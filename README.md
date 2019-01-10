# role_le-nginx

Ansible Playbook for nginx and letsencrypt


Wichtig: Definiere folgende variable:

```yaml
dns_name
```

 What it currently does:
------------------------

+ Generate self signed SSL-Certificate or LE-Certificate
+ configure nginx to forward http to https
+ configure nginx to make a reverseproxy to Port 3000 (e.g. used for gitea)

