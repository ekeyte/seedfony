# seedfony
Vagrant box for seeding Symfony projects

## Setup
The goal for this project is to provide a very simple and fast way for you to configure a Symfony project, using Vagrant and Ansible to setup your virtual machine and provision it with all the Symfony goodness you'll need.

First you will need to add an entry to your HOSTS file:
```
172.16.0.16     {projectname.vm}
```

Then, specify 