# auto-deploy
this demo flutter app has this structure:
``` log
auto-deploy
├───.github(git action pipeline for build and run ansible deploy on nginx)
│
├───ansible(contains the ansible script for executing the tasks of deploiment in nginx)
│   
└───flutter(contains flutter code  that we will build)
```
this simply build your flutter code on push request in flutter 
==> genrates web build 
==> test ssh connection to your server 
==> install ansible in gitaction 
==> execute the ansible playbook for remote deployment to your nginx


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
```log
server {
    listen 80;
    server_name rabbeh.giize.com;

    location / {
        alias /var/www/html/flutter/;
        index index.html;
    }
}
```

### update ansible\playbook.yaml  paths if necessary
some paths are on respect to  static-site-config :</br>
  path_dest_data: /var/www/html/flutter  #change this as you please on respect to static-site-config<br>
  otherpaths: update if you need to based on your use case.

---
## update .github\workflows\ci.yml
if necessary update some paths  or working directories since this project DEMO have this structure:
``` log
auto-deploy
├───.github
│   └───workflows
|        └───ci.yaml
├───ansible
│   └───template
│       ├───conf
│       └───webflutter
└───flutter
    └─── contains flutter code (not just the build)
```
