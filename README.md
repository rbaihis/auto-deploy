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
this simply build your flutter code on push request in flutter<br>
==> genrates web build <br>
==> test ssh connection to your server <br>
==> install ansible in gitaction <br>
==> execute the ansible playbook for remote deployment to your nginx


## For deploy to work to your changes 
### create a git secret name: VPS_SSH_KEY
contains your private key to connect to the remote server.<br>
steps: <br>
  1- your repository<br>
  2- settings --> secrets and variables --> actions<br>
  3- new repository secret --> name it:  VPS_SSH_KEY --> copy the ssh private key --> save<br>

### update ansible/inventory.ini
modify: 
  - ansible_host=\<ip@ or DNS\>
  - ansible_user=\<remote userSSH to connect to\>
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
  otherpaths: update if you need to based on your use case.<br>

---
## update .github\workflows\ci.yml
if necessary update some paths  or working directories since this project DEMO have this structure:<br>
``` log
auto-deploy
├───.github
│   └───workflows
|        └───ci.yaml
├───ansible
│   └───template
│       ├───conf
│       └───webflutter(build will be saved here at runtime when building flutter)
└───flutter
    └─── contains flutter code not the build
```
