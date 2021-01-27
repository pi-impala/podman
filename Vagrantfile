# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.https://vagrantcloud.com/generic/fedora33
Vagrant.configure("2") do |config|
#   config.vagrant.plugins = "vagrant-sshfs"
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "fedora/33-cloud-base"
  config.vm.box_version = "33.20201019.0"

  config.vm.define "fedora33-podman-dev"

  config.vm.provider "libvirt" do |libvirt, override|
    libvirt.memory = 4096
    libvirt.cpus = 4
    libvirt.storage :file,
        :type => 'qcow2'

    # override.vm.synced_folder ".", "/vagrant", type: "sshfs"
    # config.vm.synced_folder ".", "/home/vagrant/sync", disabled: true
    # config.vm.synced_folder ".", "/home/vagrant/libpod", type: "rsync", rsync__exclude: ["_output"]
  end

  config.vm.provision "shell", inline: <<-SHELL
  sudo yum update -y
  sudo yum install -y \
    btrfs-progs-devel \
    conmon \
    containernetworking-cni \
    device-mapper-devel \
    git \
    glib2-devel \
    glibc-devel \
    glibc-static \
    go \
    golang-github-cpuguy83-md2man \
    gpgme-devel \
    iptables \
    libassuan-devel \
    libgpg-error-devel \
    libseccomp-devel \
    libselinux-devel \
    make \
    pkgconfig \
    runc \
    containers-common

    systemctl daemon-reload

    git clone https://github.com/containers/podman/
    cd podman
    make BUILDTAGS="selinux seccomp"
    sudo make install PREFIX=/usr

  SHELL

end
