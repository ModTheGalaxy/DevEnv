# SWGEmu Development Environment setup

****************************************************************************************************************
Special Thanks to lordkator for the initial FastTrack VM Image and the scripts that this repository is based on.
****************************************************************************************************************

## Install Debian 9.x 64bit or Ubuntu 16.x

## Tested with debian 9.5 with cinnamon desktop

Install to a new VM and ensure you run `sudo apt-get update` and `sudo apt-get upgrade` BEFORE running the following scripts.

## Import scripts

Copy this series of commands into a terminal: Installs git, downloads scripts and installs them. ## DO NOT LOGIN AS ROOT!!!!

```
sudo apt-get update && sudo apt-get install -y -q git && git clone https://bitbucket.org/lasko2112/DevEnv.git && cp -i ~/DevEnv/README.md ~/Documents && mkdir setup && mkdir run && cp -r ~/DevEnv/run/* ~/run/ && chmod -v +x ~/DevEnv/bin/* && cat ~/DevEnv/bin/pathto &>> ~/.bashrc
```

## Run scripts

Once the above has completed, run the following from the command line.

1. cd ~/DevEnv/bin

2. ./reqd - Installs required packages and programs including Lua, BerkelyDB, etc.

3. ./setup - Setup of development environment follows these steps:
   * Clone repos and checkout a local branch of Core3 origin/unstable
   * Server configuration
   * Tre files (They will need to be copied or moved)
   * Asks if you want to build and run the server. - Currently will fail
   
4. cd ~/workspace/Core3/MMOCoreORB

5. build server with `make -j8`

6. cd ~/workspace/Core3/MMOCoreORB/bin

7. Run server with `./core3`

8. you can run the "latest" script to update as you wish. It will do a quick git-stash, git-pull, and git-stash-apply so you can get to the latest code w/o loosing local work.

## Setup MySQL

You will need to edit the SQL database with workbench. Easiest way is to set it up from the command line.

From command line run:

`sudo mysql -u root

use mysql;

update user set password=PASSWORD("12345678") where User='root';

UPDATE user SET plugin='mysql_native_password' WHERE User='root';

FLUSH PRIVILEGES;

exit;`

Now open workbench from start/programming.

Log in as root uping p/w 12345678

open galaxy table and edit IP address to your VM's address (default is localhost 127.0.0.1), save, apply, exit, reboot.

****************************************************************************************************************
