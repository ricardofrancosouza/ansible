Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/bionic64"


    config.vm.define "mysqlserver" do |mysqlserver|
        mysqlserver.vm.network "public_network", ip: "192.168.56.16"
        mysqlserver.vm.provision "shell",
            inline: "cat /vagrant/configs/id_ansible.pub >> .ssh/authorized_keys"
    end

        config.vm.define "ansible" do |ansible|
        ansible.vm.network "public_network", ip: "192.168.56.15"   
        ansible.vm.provision "shell", inline: "cp /vagrant/id_ansible /home/vagrant && \
         chmod 600 /home/vagrant/id_ansible && \
         chown vagrant:vagrant /home/vagrant/id_ansible"
        
        ansible.vm.provision "shell",  
            inline: "apt-get update && \
            apt-get install -y software-properties-common && \
            apt-add-repository --yes --update ppa:ansible/ansible && \
            apt-get install -y ansible"
        ansible.vm.provision "shell",
            inline: "ansible-playbook -i /vagrant/configs/ansible/hosts /vagrant/configs/ansible/playbook.yml"    
  
       
    end

  
   
end