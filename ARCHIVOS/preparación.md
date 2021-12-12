# Preparación del Servidor Linux.
## Antes de ponernos con la instalación de K0s, vamos a investigar un poco nuestro servidor y a dejarlo listo para ello. 

## 1. Lo primero que vamos a hacer es actualizar el servidor para tenerlo todo preparado:

```
apt update
apt upgrade
```


## 2. Vamos a ver las interfaces y la ip de nuestro servidor:
```
ip a
```

![p1](https://github.com/mloparj10/Proyecto-k0s/blob/main/images/preparacion/p1.JPG)

Como podemos observar tiene una tarjeta de red física, la eth0.


## 3. Vemos el archivo resolv.conf para los DNS
```
cat /etc/resolv.conf
```

![p2](https://github.com/mloparj10/Proyecto-k0s/blob/main/images/preparacion/p2.JPG)

El servidor tiene los DNS de Google. Nada fuera de lo normal


## 4. Con la herramienta ScreenFetch nos da información basica del sistema. Si no la tenemos la instalamos en un momento. y para ejecutarla escribimos screenfetch.
```
apt install screenfetch
screenfetch
```

![p3](https://github.com/mloparj10/Proyecto-k0s/blob/main/images/preparacion/p4.JPG)

Así en resumen, tenemos un Daebian 11, con un disco de 5 GB, y 9 Gb de Ram. El kernel de linux es 5.10.0-6-amd64

