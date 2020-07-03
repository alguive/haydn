# Vagrant [CentOS] - Ansible [LEMP]

Simple Vagrant + Ansible LEMP setup with **Nginx**, **PHP7** and **MariaDB** on a **CentOS 7** Box (From the official CentOS).


## Requirements
 * VirtualBox
 * Ansible
 * Vagrant

## Installation

1. ```git clone https://github.com/alvarogv7/haydn.git```
2. ```cd haydn```
3. Follow ***Configuration*** steps
4. ```Vagrant up```
5. ```cd ansible```
6. ```ansible-galaxy install -r requirements.yml || ansible-galaxy install -r requirements.yml --force```
7. ```ansible-playbook -i hosts playbook.yml```

If after following the steps, the machine doesn't get up, maybe you will need to execute: ***vagrant reload --provision***.


## Configuration

### Vagrantfile
The hostname will be the URL to your project.

```
  config.vm.hostname = "haydn.test"
```

The network IP to your project.

```
  config.vm.network "private_network", ip: "10.10.30.40"
```

The server directory to your ./src folder.

```
  config.vm.synced_folder "./src", "/var/www/haydn"
```

### Hosts files
You will need to add your hostname to you hosts file: ***/private/etc/hosts***. [In MacOS].

Also you will need to change the **hosts** file inside the ansible directory with your **IP** and optionally with a custom ***user*** and ***vagrant***.

```
dev ansible_host=10.10.30.40 ansible_user=vagrant ansible_password=vagrant
```

### Playbook file

You will need to change the **mysql_users** and **mysql_databases** params, **server_name**, **root** and the **include** route from **extra_parameters** param to those you have set before. ***[haydn]***

```
mysql_users:
  - name: haydn
    password: haydn
mysql_databases:
  - name: haydn

server_name: "haydn.test"
root: /var/www/haydn
extra_parameters: |
  include /var/www/haydn/nginx.conf;
```

--
