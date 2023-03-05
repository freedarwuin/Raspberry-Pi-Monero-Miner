#### Instalar dependencias
```
sudo apt-get install automake autoconf pkg-config libcurl4-openssl-dev libjansson-dev libssl-dev -y 
sudo apt-get update -y
sudo apt-get install git -y
sudo apt-get install -y --force-yes autoconf automake libtool
sudo apt-get install screen -y
sudo apt-get install build-essential -y
```

#### Instalación del minero
```
git clone https://github.com/freedarwuin/cpuminer-multi
cd cpuminer-multi
```

#### Construyendo el minero
```
./autogen.sh
./build.sh
```

#### Minería
```
screen ./cpuminer -a cryptonight -o stratum+tcp://teracycle.net:3333 -p x -u (wallet)  --api-bind 0
```

Raspbian uses dphys-swapfile, which is a swap-file based solution instead of the "standard" swap-partition based solution. 
It is much easier to change the size of the swap.

The configuration file is:
```
/etc/dphys-swapfile 
```

The content is very simple. By default my Raspbian has 100MB of swap:
```
CONF_SWAPSIZE=100
```
If you want to change the size, you need to modify the number and restart dphys-swapfile:
```
/etc/init.d/dphys-swapfile stop
/etc/init.d/dphys-swapfile start
```

Edit: On Raspbian the default location is /var/swap, which is (of course) located on the SD card. I think it is a bad idea, so I would like to point out, that the /etc/dphys-swapfile can have the following option too: ```CONF_SWAPFILE=/media/btsync/swapfile```

I only problem with it, the usb storage is automounted, so a potential race here (automount vs. swapon)

#### Ejecución automática
```
sudo nano /etc/rc.local
```
