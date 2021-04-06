DangerPool 

install Kudaraidee's Repo Yiimp

Create a Swap File - Low Ram Servers

 sudo fallocate -l 1G /swapfile
 
 sudo chmod 600 /swapfile
 
 sudo mkswap /swapfile
 
 sudo swapon /swapfile
 
 sudo nano /etc/fstab

Add to fstab file

/swapfile   none    swap    sw    0   0

    apt update
    apt upgrade
    reboot
    adduser pool (pool it's just an example...)
    adduser pool sudo
    su - pool
    sudo apt-get install curl mc nano git pwgen libkrb5-dev apt-transport-https software-properties-common
    git clone -b Kudaraidee https://github.com/xavatar/yiimp_install_scrypt.git
    cd yiimp_install_scrypt/
    bash install.sh (DO NOT RUN THE SCRIPT AS ROOT or SUDO)
    At the end, you MUST REBOOT to finalize installation...

Finish !

Edit files:

/home/danger/yiimp_install_scrypt/utils/screen-stratum.sh

/var/web/serverconfig.php

/var/web/yaamp/modules/site/index.php

/var/web/yaamp/core/backend/payment.php

/home/danger/yiimp-install-only-do-not-run-commands-from-this-folder/stratum/coinbase.cpp

/var/web/yaamp/modules/api/ApiController.php

utils/screen-stratum.sh

add lyra2z

var/web/serverconfig.php

fees mining 0.1

payments freq 1*60*60

payments min 0.01

1032 ... lyra2z

crontab -e

@reboot sleep 35 && /etc/screen-scrypt.sh

@reboot sleep 35 && /etc/screen-stratum.sh

@reboot sleep 2 && /home/danger/dngrcoind -daemon -txindex

//copyed /utils/screen-stratum.sh to /etc/screen-stratum.sh

sudo cp -r /home/pool/yiimp_install_scrypt/utils/screen-stratum.sh /etc/

sudo chmod +x /etc/screen-stratum.sh

reboot

for payout to work

/var/web/yaamp/core/backend/payment.php

line 57 add 'DNGR'

edit var/web/yaamp/modules/site/index.php

Rename domain to Danger Pool

<option value="92.38.163.183">World</option>

<option value="pool.dangercoin.org">World2</option> 

result += coin.options[coin.selectedIndex].dataset.algo + ' -o stratum+tcp://';

result += stratum.value + ':';

sudo ufw allow 80 443 4553 49002

cd yiimp_install_scrypt/utils/

bash delcoin.sh

to change coinbase name from yiimp to something else. 

sudo nano ~/yiimp-install-only-do-not-run-commands-from-this-folder/stratum/coinbase.cpp

char script2[32] = "7969696d7000"; // "yiimp\0" in hex ascii

to char script2[32] = "44616e676572506f6f6c00"; // "DangerPool" in hex ascii

 compile stratum
 
cd ~/yiimp-install-only-do-not-run-commands-from-this-folder/stratum

sudo make

replace the new stratum you just compiled

 sudo cp -r stratum /var/stratum
 

install dngrcoind:

wget https://raw.githubusercontent.com/dngrcoin/dngrcoin/master/DNGRinstall.sh

bash DNGRinstall.sh

Go to http://xxx.xxx.xxx.xxx/AdminPanel or https://xxx.xxx.xxx.xxx/AdminPanel to access Panel Admin

Go to the wallets tab

click at the bottom CREATE COIN of the page

go to GENERAL

Name DangerCoin

Symbol  DNGR

Algo  lyra2z

go to SETTINGS

Put a tick: Enable, AutoReady, Visible, Installed, Masternodes

go to DAEMON

Process name dngrcoind

Conf folder .dngrcoin

RPC host 127.0.0.1

RPC port 49003

click at the bottom CREATE

click at the DangerCoin

click at the tab SET AUTO

click at the tab COIN PROPERTIES

click at the tab DAEMON

Copy sample config from coin properties/daemon to .dngrcoin/dngrcoin.conf

--------------------------

for example:

rpcuser=yiimprpc

rpcpassword=eLcIr4MWBJvZ93J5tswC4g

rpcport=49003

rpcthreads=8

rpcallowip=127.0.0.1

maxconnections=12

daemon=1

gen=0

alertnotify=echo %s | mail -s "DangerCoin alert!" al456643@gog.tr

blocknotify=/var/stratum/blocknotify dngrpool.99:4553 1425 %s

---------------------------
sudo reboot

