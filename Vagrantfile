# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
  config.vm.define 'master' do |c|
    c.vm.host_name = 'master.vm'
    c.vm.network :hostonly, "10.50.60.2"

    c.vm.box = "centos-58-64bit"
    c.vm.box_url = "https://s3.amazonaws.com/kbarber-puppetlabs-firewall/vagrant/centos-58-64bit.box"

    c.vm.forward_port 22, 22200


    c.vm.provision :puppet do |p|
      p.manifests_path = "manifests"
      p.manifest_file = "site.pp"
      p.module_path = "modules"
    end
  end

  config.vm.define 'centos-58-64bit' do |c|
    c.vm.host_name = 'centos-58-64bit.vm'
    c.vm.network :hostonly, "10.50.60.3"

    c.vm.box = "centos-58-64bit"
    c.vm.box_url = "https://s3.amazonaws.com/kbarber-puppetlabs-firewall/vagrant/centos-58-64bit.box"

    c.vm.forward_port 22, 22201

    c.vm.provision :puppet do |p|
      p.manifests_path = "manifests"
      p.manifest_file = "site.pp"
      p.module_path = "modules"
    end
  end

  config.vm.define 'debian-605-64bit' do |c|
    c.vm.host_name = 'debian-605-64bit.vm'
    c.vm.network :hostonly, "10.50.60.4"

    c.vm.box = "debian-605-64bit"
    c.vm.box_url = "https://s3.amazonaws.com/kbarber-puppetlabs-firewall/vagrant/debian-605-64bit.box"

    c.vm.forward_port 22, 22202

    c.vm.provision :puppet do |p|
      p.manifests_path = "manifests"
      p.manifest_file = "site.pp"
      p.module_path = "modules"
    end
  end

  config.vm.define 'ubuntu-1104-64bit' do |c|
    c.vm.host_name = 'ubuntu-1104-64bit.vm'
    c.vm.network :hostonly, "10.50.60.5"

    c.vm.box = "ubuntu-1104-64bit"
    c.vm.box_url = "https://s3.amazonaws.com/kbarber-puppetlabs-firewall/vagrant/ubuntu-1104-64bit.box"

    c.vm.forward_port 22, 22203

    c.vm.provision :puppet do |p|
      p.manifests_path = "manifests"
      p.manifest_file = "site.pp"
      p.module_path = "modules"
    end
  end

  config.vm.define 'centos-63-64bit' do |c|
    c.vm.host_name = 'centos-63-64bit.vm'
    c.vm.network :hostonly, "10.50.60.6"

    c.vm.box = "centos-63-64bit"
    c.vm.box_url = "https://s3.amazonaws.com/kbarber-puppetlabs-firewall/vagrant/centos-63-64bit.box"

    c.vm.forward_port 22, 22204

    c.vm.provision :puppet do |p|
      p.manifests_path = "manifests"
      p.manifest_file = "site.pp"
      p.module_path = "modules"
    end
  end
end
