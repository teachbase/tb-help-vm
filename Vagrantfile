Vagrant.configure("2") do |config|
  config.vm.box       = "ubuntu/trusty64"

  config.vm.provision "ansible" do |ansible|
    ENV["ANSIBLE_CONFIG"] = "ansible/ansible.cfg"
    ansible.playbook = "dev.yml"
    ansible.inventory_path = "dev_hosts"
    ansible.tags = ENV["TAGS"]
    ansible.skip_tags = ENV["SKIP_TAGS"]
    ansible.verbose = 'v'
    ansible.limit = "all"
  end

  config.vm.network :forwarded_port, host: 2210, guest: 22 
  config.vm.network :forwarded_port, host: 3100, guest: 80 

  config.vm.network "private_network", ip: "192.168.50.131"

  config.vm.synced_folder ".", "/vagrant", :disabled => true
  config.vm.synced_folder "src/", "/webapps/help.teachbase", create: true, id: "vagrant-root",
    owner: "vagrant",
    group: "www-data",
    mount_options: ["dmode=775,fmode=774"]
end