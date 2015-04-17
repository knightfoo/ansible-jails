# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

FIX_BOX = <<SCRIPT
echo "Fixing python symlinks"
ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
ln -sf /usr/local/bin/pydoc2.7 /usr/local/bin/pydoc
echo '193.190.67.98 ftp.belnet.be' >> /etc/hosts
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "freebsd"
  config.vm.box_check_update = false
  # disable default shared folder, we don't need it with ansible
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provision "shell", inline: FIX_BOX

  # config.vm.provider "virtualbox" do |vb|
  #   # Don't boot with headless mode
  #   vb.gui = true
  #
  #   # Use VBoxManage to customize the VM. For example to change memory:
  #   vb.customize ["modifyvm", :id, "--memory", "1024"]
  # end
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.extra_vars = {
      ansible_python_interpreter: "/usr/local/bin/python",
      jails_zfs_pool: "tank",
      jails_dir: "/jails",
      remote_user: "vagrant"
    }
  end
end
