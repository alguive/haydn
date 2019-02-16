Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.hostname = "haydn.test"
  config.vm.box_check_update = false

  config.vm.network "private_network", ip: "10.10.30.40"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder "./src", "/var/www/haydn",
    type: "nfs",
    nfs_version: 3,
    nfs_udp: false,
    mount_options: ['actimeo=2']

  config.vm.provision "shell", inline: <<-SHELL
    sudo sed -i 's|[#]*PasswordAuthentication no|PasswordAuthentication yes|g' /etc/ssh/sshd_config
    sudo systemctl reload sshd

    setenforce 0
    sed -i 's/SELINUX=\(enforcing\|permissive\)/SELINUX=disabled/g' /etc/selinux/config
  SHELL
end
