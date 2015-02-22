# -*- mode: ruby -*-
# vi: set ft=ruby :

$islf4 = {
  hostname: "islandora",
  box: "ubuntu/trusty64",
  ram: 2048,
  ip_address: "10.11.12.15",
  ports: [
    { guest: 80, host: 8000 },   # apache
    { guest: 3030, host: 3030 }, # fuseki
    { guest: 3306, host: 3306 }, # mysql
    { guest: 5432, host: 5432 }, # postgres
    { guest: 8080, host: 8080 }, # tomcat
    { guest: 8181, host: 8181 }, # karaf
  ],
}

Vagrant.configure("2") do |config|

  config.vm.hostname = $islf4[:hostname]
  config.vm.box = $islf4[:box]

  config.vm.network :private_network, ip: $islf4[:ip_address]
  $islf4[:ports].each { |p| config.vm.network :forwarded_port, guest: p[:guest], host: p[:host] }

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", $islf4[:ram]]

    # attempt to determine cpu count according to platform
    if not RUBY_PLATFORM.downcase.include?("mswin")
      v.customize [ "modifyvm", :id, "--cpus",
        `awk "/^processor/ {++n} END {print n}" /proc/cpuinfo 2> /dev/null || \
        sh -c 'sysctl hw.logicalcpu 2> /dev/null || \
        echo ": 2"' | awk \'{print \$2}\' `.chomp ]
    end
  end

  config.vm.provision :ansible do |ansible|
    ansible.host_key_checking = false
    ansible.playbook = "islandora.yml"
    ansible.inventory_path = "inventory-vagrant/hosts"
    ansible.limit = 'all'
  end

end
