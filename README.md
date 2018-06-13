# roles/matlab/README.md

[![Build Status](https://travis-ci.org/cjsteel/matlab.svg?branch=master)](https://travis-ci.org/cjsteel/matlab)
[![Travis CI](http://img.shields.io/travis/csteel/matlab/default.svg?style=flat)](http://travis-ci.org/csteel/matlab/default)
[![Platforms](http://img.shields.io/badge/platforms-debian%20/%20ubuntu-lightgrey.svg?style=flat)](#)

## Description

matlab is an Ansible role used to install **Matlab** to all requried users.  

[The MathWorks](http://www.mathworks.com/academia/)
 products are computational software environments, which perform a wide variety of computational tasks related to mathematics, science, 
engineering, finance, and so on.

**note**: at the stage, we can only copy over the installation package to remote machine and unarchive them for manual installation as installation needs 'matlab licence key'.

matlab_install_dir    : '/opt/matlab/{{ matlab_version }}'
matlab_install_archive_dir: '/var/tmp/archive'

## Resources

- [mathworks](https://www.mathworks.com/products/matlab.html) 
- [Mcgill_weblink](http://kb.mcgill.ca/kb/?ArticleId=1305&source=article&c=12&cid=2#tab:homeTab:crumb:8:artId:1305:src:article) - with details how to apply for license and installation precedure...

## Recommended

Running Ansible in a virtual environment allows for a lot of testing flexibility.

* [docs/ansible-setup](docs/ansible-setup.md)

## Requirements

* Ansible

## Dependencies

- matlab package needs to be mannully downloaded in localhost first;
- there is one role in /tasks/main.yml to create aceusers group, please comment it for real playbook as all users are in ldap, ldap playbook will be run first in order to have 'aceusers' group available on remote machine;

## Variables

A description of the settable variables for this role should go here, including any variables that are in

### defaults/main.yml

```sh
---
unzip_version: "6.0*"

matlab_package_state    : 'present'
matlab_version  : 'R2017b'
matlab_package     : 'matlab_{{ matlab_version }}_glnxa64.zip'
#matlab_runtime_package: 'MCR_{{ matlab_version }}_glnxa64_installer.zip'
#matlab_http_link: 'http://ssd.mathworks.com/supportfiles/downloads/{{ matlab_version }}/deployment_files/{{ matlab_version }}/installers/glnxa64/{{ matlab_runtime_package }}'

matlab_local_resource_dir   : '{{ matlab_controller_home }}/sw/ubuntu/{{ ansible_distribution_version }}/matlab'
#matlab_local_resource_dir   : '{{ matlab_controller_home }}/sw/{{ ansible_distribution }}/{{ ansible_distribution_version }}/matlab'
matlab_local_resource_path : '{{ matlab_local_resource_dir }}/{{ matlab_version }}'

matlab_deployment_resource_dir  : '{{ matlab_deployment_home }}/sw/ubuntu/{{ ansible_distribution_version }}/matlab'
#matlab_deployment_resource_dir  : '{{ matlab_deployment_home }}/sw/{{ ansible_distribution }}/{{ ansible_distribution_version }}/matlab'
matlab_deployment_resource_path    : '{{ matlab_deployment_resource_dir }}/{{ matlab_version }}'


matlab_install_dir: '/usr/local/matlab/{{ matlab_version }}'
matlab_install_archive_dir: '/var/tmp/archive'
```



## Example Playbook

### project_name/matlab.yml

* [example_playbook.yml](files/example_playbook.yml)

To install:

```shell
cd project_directory
cp roles/matlab/files/example_playbook.yml matlab.yml
# edit if required
nano matlab.yml
```

### project_name/site.yml

* [example_matlab.yml](files/example_site.yml)

From the projects main directory run the following:

```yaml
cp roles/matlab/files/example_playbook.yml matlab.yml
cat matlab.yml
```

### project/group_vars/all/project_defaults.yml

[files/group_vars/all/example_defaults.yml](files/group_vars/all/example_defaults.yml)

```yaml
cp roles/matlab/files/group_vars/all/example_defaults.yml group_vars/all/project_defaults.yml
cat group_vars/all/project_defaults.yml
```

## Testing

Move into the role directory and run vagrant:

```shell
cd roles/matlab
vagrant up
```

### Authors and license

- [Andy Teng](http://mcin-cnim.ca/) | [e-mail](mailto:xiaoqiu.teng@mcgill.ca)
- [Christopher Steel](http://mcin-cnim.ca/) | [e-mail](mailto:christopher.steel@mcgill.ca)

License: [MIT](https://tldrlegal.com/license/mit-license)

***
### Open Science

The Neuro has adopted the principles of Open Science. We are inspired by the likes of the Allen Institute for Brain Science, the National Institutes of Health's Human Connectome project, and the Human Genome project. For additional information please see [open science at the neuro](https://www.mcgill.ca/neuro/open-science-0).

![MCIN](imgs/mcin-logo-brain-140x116.png)          ![neuro](imgs/neuro-logo-160x116.png)  

* ansible-role-matlab generated using [galaxy-role-skeleton](https://github.com/cjsteel/galaxy-role-skeleton)

