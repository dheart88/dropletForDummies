# dropletForDummies
A guide to create a droplet on Digital Ocean with LEMP Stack + Laravel project for Ubuntu User, assuming a droplet has been deployed and you know how to do ssh :) . I have some experiences with Fedora and CentOS but this is my first time installing LEMP stack on ubuntu machine.

## Optional : Create Sudo User
Taken from https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-ubuntu-quickstart, I strongly believe you shouldn't use your root account for everything :) so let's create a user account

## Optional : Change SSH port
After you managed to connect to your droplet, you should change port number of ssh, because port 22 is very obvious.
you could look at this link https://www.cyberciti.biz/faq/howto-change-ssh-port-on-linux-or-unix-server/

Find sshd config file

`$ find / -name "sshd_config" 2>/dev/null`

I personally prefer to use nano for editing, but vi/vim is also doable, on recent ubuntu droplet nano is already installed. But if you dont have it and you want to install:

`sudo apt install nano`

change the settings

`sudo nano /etc/ssh/sshd_config`

![SSHD](images/sshd.jpg)


change port 22 to any number higher than 1024 and below 65535, I changed it to 5115

There is no need to configure the firewall because it is inactive, but if you are curious you can do this

`sudo ufw status`

All you have to do is to restart the ssh service

`sudo systemctl restart ssh`

and to logout from current ssh connection you can do 
`logout`

![Done](images/sshdone.jpg)

Don't forget to set your firewall.. I think on default there is no firewall (uh.. i forgot what was it like at first time), but you to make sure that you have firewall configured properly on your digital ocean control panel

![firewall](images/firewall.jpg)


## Step 1 : Install Nginx
I took this link for references, I was too busy to look at the whole documentation so I just google a bit to find references, and I found this.. https://websiteforstudents.com/how-to-install-lemp-on-ubuntu-16-04-18-04-18-10/ , lets try it out


`sudo apt update && sudo apt dist-upgrade && sudo apt autoremove`

I believe && is part of chaining in bash/shell, so it consists 3 different instruction. the command above should update packages and second command should update the distro (ubuntu itself) and third command should remove unneccessary packages

```
sudo apt install nginx
sudo systemctl enable nginx
```

it should install nginx for you, and second part to enable it, so it will run as service and should be autostart after you restart your instance


