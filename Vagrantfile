# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", ip: "192.168.33.13"

  # NFS shared folders for speed.
  # @see https://gist.github.com/ziadoz/241be0ed516d9204fe9f
  sync_opts = { nfs: true }
  # Options for host exportfs and /etc/exports (on Linux).
  nfs_exports = ["rw", "async", "insecure", "no_subtree_check", "all_squash"]
  # Options for mount within VM.
  sync_opts[:mount_options] = ["rw", "noac", "actimeo=0", "intr", "async", "noacl", "lookupcache=none"]

  if (RUBY_PLATFORM =~ /darwin/)
    nfs_exports << "maproot=0:0"
    sync_opts[:bsd__nfs_options] = nfs_exports
  elsif (RUBY_PLATFORM =~ /linux/)
    nfs_exports << "no_root_squash"
    sync_opts[:linux__nfs_options] = nfs_exports
  else
    raise "Cannot recognize platform #{RUBY_PLATFORM}"
  end

  # All synced folders go here with the same options.
  config.vm.synced_folder "..", "/vagrant", sync_opts

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "provisioning/playbook.yml"
  end

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

end
