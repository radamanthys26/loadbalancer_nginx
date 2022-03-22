# Criado por Bruno Lima (radamanthys@outlook.com)

# Exemplo de load balance usando Vagrant / VirtualBox/ Nginx / Linux CentOS,
# totalmente automatizado, utilizando os servidores Master 192.168.33.20,
# e slave1 192.168.33.21 e 192.168.33.2.

# São 3 blocos de configuração, sendo:
# Bloco 1 - Configuração do servidor de balanceamento do nginx (master);
# Blocos 2 e 3 - Configuração dos servidores web (slave1,slave2)

# Bloco 1
Vagrant.configure("2") do |config|

# Servidor nginx com balanceamento de carga
    config.vm.define "master" do |master|
      master.vm.box = "centos/7"
      master.vm.hostname = 'master'
      master.vm.box_url = "centos/7"

     master.vm.network :private_network, ip: "192.168.33.20"

     master.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--memory", 1024]
        v.customize ["modifyvm", :id, "--name", "master"]

      master.vm.provision :shell, inline: <<-SHELL
        yum install -y epel-release
        yum install -y nginx nano
        systemctl enable nginx && systemctl start nginx
        ttt='upstream nodes { server 192.168.33.21; server 192.168.33.22; } server { listen 80; server_name 192.168.33.20; location / { proxy_pass http://nodes; } }' && sudo bash -c "echo '$ttt' > /etc/nginx/conf.d/balanceador.conf" && systemctl restart nginx

      SHELL
        end
          end

# Bloco 2
# Maquina virtual slave 1 com o site azul
    config.vm.define "slave1" do |slave1|
      slave1.vm.box = "centos/7"
      slave1.vm.hostname = 'slave1'
      slave1.vm.box_url = "centos/7"

    slave1.vm.network :private_network, ip: "192.168.33.21"

    slave1.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--memory", 1024]
        v.customize ["modifyvm", :id, "--name", "slave1"]

    slave1.vm.provision :shell, inline: <<-SHELL
      yum install -y epel-release
      yum install -y nginx nano
      systemctl enable nginx && systemctl start nginx
      mv /usr/share/nginx/html/index.html /usr/share/nginx/html/index.html.bak
      ttt='<html> <body style="background-color:blue;"> </body> </html>' && sudo bash -c "echo '$ttt' > /usr/share/nginx/html/index.html"
   SHELL
      end
        end

#Bloco 3
# Maquina virtual slave 2 com o site vermelho
    config.vm.define "slave2" do |slave2|
      slave2.vm.box = "centos/7"
      slave2.vm.hostname = 'slave2'
      slave2.vm.box_url = "centos/7"

    slave2.vm.network :private_network, ip: "192.168.33.22"

    slave2.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--name", "slave2"]

    slave2.vm.provision :shell, inline: <<-SHELL
      yum install -y epel-release
      yum install -y nginx nano
      systemctl enable nginx && systemctl start nginx
      mv /usr/share/nginx/html/index.html /usr/share/nginx/html/index.html.bak
      ttt='<html> <body style="background-color:red;"> </body> </html>' && sudo bash -c "echo '$ttt' > /usr/share/nginx/html/index.html"
   SHELL
      end
    end


end
