# auto-deploy
using git Action + git secret + ansible(in git-actions)

## For deploy to work to your changes 
### create a git secret name: VPS_SSH_KEY
contains your private key to connect to the remote server.
steps: 
1- your repository
2- settings --> secrets and variables --> actions
3- new repository secret --> name it:  VPS_SSH_KEY --> copy the ssh private key --> save

### update ansible/inventory.ini
modify: 
  - ansible_host=<ip@ or DNS>
  - ansible_user=<ssh remote user to connect to>
### update ansible\template\conf\static-site-config
default configuration is this as you please:
--- log
server {
    listen 80;
    server_name rabbeh.giize.com;

    location / {
        alias /var/www/html/flutter/;
        index index.html;
    }
}
---
### update ansible\playbook.yaml  paths if necessary
paths as your static-site-config :
path_dest_data: /var/www/html/flutter  #change this as you please on respect to static-site-config
otherpaths: update if you need to based on your use case.
---
##
