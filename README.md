# SWGEmu Development Environment setup

****************************************************************************************************************
Special Thanks to lordkator for the initial FastTrack VM Image and the scripts that this repository is based on.
****************************************************************************************************************

## Install Debian 9.x 64bit

## Tested with debian 9.8 with cinnamon desktop

## Blank MtG Server Debian 9.8 v2.0 VM Image can be downloaded from [HERE.](https://drive.google.com/open?id=1UrUAlKTqypyXA8kub4GwZsMOjTEUrnKc)

Install a new VM in VirtualBox (or download the above link).

##Impotant Note!!
Please ensure you run `sudo apt-get update` and `sudo apt-get upgrade` BEFORE running the following scripts if using the MtG Base Image.

Once complete

For this exercise, use the following passwords:

root: 12345678

And setup the user to be:

swgemu

password: 123456

## Import scripts

Copy this series of commands into a terminal: Installs git, downloads scripts and installs them. ## DO NOT LOGIN AS ROOT!!!!

And just to make sure you don't ignore it and do it anyway!!

## DO NOT LOGIN AS ROOT!!!!
YOU WILL BREAK THE INSTALL IF YOU DO THIS AS ROOT!!

So..

Copy this long series of commands into your console..


```
sudo apt-get update && sudo apt-get install -y -q git && git clone https://github.com/ModTheGalaxy/DevEnv.git && cp -i ~/DevEnv/README.md ~/Documents && mkdir setup && mkdir run && cp -r ~/DevEnv/run/* ~/run/ && chmod -v +x ~/DevEnv/bin/* && cat ~/DevEnv/bin/pathto &>> ~/.bashrc
```

## Run scripts

Once the above has completed, run the following from the command line.

1. cd ~/DevEnv/bin

2. ./reqd - Installs required packages and programs including Lua, BerkelyDB, etc.

3. ./setup - Setup of development environment follows these steps:
   * Clone repos and checkout a local branch of mtgserver/master
   * Server configuration
   * For MySQL databases, passwords are [sudo]123456, then 123456 for the two DB's
   * Tre files (They will need to be copied or moved)
   * Asks if you want to build and run the server.
   
4. Will build the server. However if it fails, use the following:

5. cd ~/workspace/Core3/MMOCoreORB

6. build server with `make -j8`

7. While the server is building, is a good time to copy your tre files to the server. There is a shared folder set up in the VM.

8. On your host computers C drive, create a folder called c:\vmshare

9. Copy your tre files to this folder, **YOU WILL CURRENTLY HAVE TO RENAME YOUR TRE FOLDER "TRE" AS IT IS CURRENTLY CALLED NIL **


10. Open a new terminal and press the up arrow until you see this command: Then hit Enter.

```sudo mount -t vboxsf vmshare ~/share/```

11. The folder should now be available in the Debian file explorer, you should be able now, to drag the files actross to /tre

12. Once the build process has finished, it should immediately launch the server. If it does not, then:

13. cd ~/workspace/Core3/MMOCoreORB/bin

14. Run server with `./core3`

9. you can run the "latest" script to update code and engine submodule as you wish. It will do a quick git-stash, git-pull, and git-stash-apply so you can get to the latest code w/o losing local work.

## Setup MySQL

You will need to manually setup MySQL workbench. Easiest way is to set it up from the command line.

From command line run:

`sudo mysql -u root`

`use mysql;`

`update user set password=PASSWORD("12345678") where User='root';`

`UPDATE user SET plugin='mysql_native_password' WHERE User='root';`

`FLUSH PRIVILEGES;`

`exit;`

Now open workbench from start/programming.

Log in as root uping p/w 12345678

open galaxy table and edit IP address to your VM's address (default is localhost 127.0.0.1), save, apply, exit, reboot.

****************************************************************************************************************
