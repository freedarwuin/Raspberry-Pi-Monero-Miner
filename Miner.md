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

Raspbian utiliza dphys-swapfile, que es una solución basada en archivos de intercambio en lugar de la solución basada en particiones de intercambio "estándar".
Es mucho más fácil cambiar el tamaño del intercambio.

El archivo de configuración es:
```
/etc/dphys-swapfile 
```

El contenido es muy simple. Por defecto, mi Raspbian tiene 100 MB de intercambio:
```
CONF_SWAPSIZE=100
```
Si desea cambiar el tamaño, debe modificar el número y reiniciar dphys-swapfile:
```
/etc/init.d/dphys-swapfile stop
/etc/init.d/dphys-swapfile start
```

Editar: en Raspbian, la ubicación predeterminada es /var/swap, que (por supuesto) se encuentra en la tarjeta SD. Creo que es una mala idea, por lo que me gustaría señalar que /etc/dphys-swapfile también puede tener la siguiente opción: ```CONF_SWAPFILE=/media/btsync/swapfile```

Solo tengo un problema con eso, el almacenamiento USB es de montaje automático, por lo que una carrera potencial aquí (montaje automático vs. swapon)

#### Ejecución automática
```
sudo nano /etc/rc.local
```
