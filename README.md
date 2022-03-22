# Projeto de balanceamento de carga com Nginx no CentOS
### Sobre o projeto

O objetivo deste projeto é demonstrar de maneira simples o funcionamento do balanceamento de carga com o webserver Nginx. Foi utilizado o Vagrant para criar 3 servidores CentOS no VirtualBox. 1 master, 2 slaves. Ao carregar o servidor master, o nginx irá direcionar a abertura do site balanceando entre os servidores slave1 e slave1. 

## Como testar

- Instale o Virtualbox e o Vagrant;
- Baixe os arquivo ou faça um git clone;
- No terminal, digite o comando $ vagrant up
- Após o término, basta acessar pelo navegador de seu pc o endereço http:// 192.168.33.20
- Ao pressionar a tecla F5 o nginx irá direcionar para um dos servidores abrindo um site azul ou vermellho.

OBS: Há diversas formas de balanceamento, o utilizado neste projeto, alterna de maneira padrão entre os servidores.
