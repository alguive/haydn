# Vagrant [CentOS] - Ansible [LEMP]

Simple Vagrant + Ansible LEMP setup with **Nginx**, **PHP7** and **MariaDB** on a **CentOS 7** Box (From the official CentOS).


## Requirements
 * VirtualBox
 * Ansible
 * Vagrant

 
## Configuration

### Vagrantfile
The hostname will be the URL to your project.

```
  config.vm.hostname = "haydn.test"
```

The network IP to your project

```
  config.vm.network "private_network", ip: "10.10.30.40"
```

The server directory to your ./src folder

```
  config.vm.synced_folder "./src", "/var/www/haydn",
```

### Hosts file
You will need to add your hostname to you hosts file: ***/private/etc/hosts***. [This is in MacOS]

### Playbook file

You will need to change the **server_name** and **root** params to those you have set before.

```
server_name: "haydn.test"
root: /var/www/haydn
```