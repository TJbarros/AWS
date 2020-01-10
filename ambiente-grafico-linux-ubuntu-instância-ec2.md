# Instalação ambiente gráfico linux instância ec2 ubuntu14.04 acesso via VNC
## Instancia: ubuntu/images/hvm-ssd/ubuntu-trusty-14.04-amd64-server-20190514 (ami-0e2e39cc84e09ff83).

1. Conectar a instancia ec2 via SSH.
2. Executar o comando **`sudo -s`** para privilegio de Super Usuário.
3. Executar o comando **`apt-get update`** para atualização da lista de pacotes.
4. Apos isso fazer o Reboot da maquina antes de instalar os pacotes.
5. Digite os seguintes comandos para instalar o ambiente gráfico e o vncserver:
**`sudo apt-get install ubuntu-desktop`**
**`sudo apt-get install vnc4server`**
**`sudo apt-get install gnome-panel`**
6. Digite o comando **`vncserver `** para iniciar o serviço.
7. Depois mate a sessão do vncserver digitando o comando **`vncserver -kill :1`**
8. Alterar o arquivo xstartup gerado apos a execução do passo anterior **`vi .vnc/xstartup`**, depois teclar **` i `**, modificando da seguinte forma:
```
#!/bin/sh
# Uncomment the following two lines for normal desktop:
unset SESSION_MANAGER
# exec /etc/X11/xinit/xinitrc
gnome-session –session=gnome-classic &
gnome-panel&
[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
vncconfig -iconic &
x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &
x-window-manager &
```
9. Pressionar **ESC** depois **:wq** e **ENTER** para salvar e sair do arquivo.
10. Adicione a porta 5901 ao security group da instancia ec2.
11. Digitar o comando **`vncserver `** novamente para iniciar o serviço.
12. Acessar remotamente utilizando o **public_ip::5901** .
