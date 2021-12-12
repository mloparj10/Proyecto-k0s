# Comprobación de nuestro kubernetes
Para comprobar que funciona todo bien, voy a desplegar un pod de Nginx con una página web, simple, con un mensaje personalizado, así vemos que se han aplicado los cambios hechos por mí de manera correcta. Explicaré el proceso que he seguido:

## 1. Realizamos un "get all" para ver si está todo limpio. 
```
k0s kubectl get all 
```
*Nota importante: recuerda siempre poner delante "k0s" ya que la herramienta kubectl, como antes he explicado, viene dentro del servicio. Si no te dará error.*

![c2](https://github.com/mloparj10/Proyecto-k0s/blob/main/images/comprobaciones/c1.JPG)

No hay nada exytraño en el, simplemente el servicio de kubernetes. Podemos continuar.

## 2. Vamos ha lanzar un pod con la imagen de Nginx.
Yo le he llamado "pod-nginx-mario" pero puedes llamarlo como quieras. Podríamos crear un archivo .yaml con todas las configuraciones, pero vamos a utilzar este comando que es mucho más rapido:
```
k0s kubectl run pod-nginx-mario --image=nginx
```

![c2](https://github.com/mloparj10/Proyecto-k0s/blob/main/images/comprobaciones/c2.JPG)

## 3. Comprobamos que está funcionando nuestro pod. Volvemos a ejecutar un "get all"

![c3](https://github.com/mloparj10/Proyecto-k0s/blob/main/images/comprobaciones/c3.JPG)

El pod ya está cargado. En apartado STATUS indica que está "runnning" (corriendo). Hasta que en ese apartado no ponga "running" el pod no estará funcionando.

## 4. Vamos a acceder al pod con una terminal interactiva. 

Para introducirnos en el pod e interactuar con el realizaremos el siguiente comando:
```
k0s kubectl exec pod/pod-nginx-mario -i -- /bin/bash
```

Lo ejecutaremos y estaremos dentro. Podemos darnos cuenta de eso al ver que el prompt ha cambiado. Es una consola bash como otra cualquiera, un pequeño sistema linux sin ningún misterio, asi que podemos navegar tranquilamente por sus directorios.
Nos vamos a ir al directorio donde se encuentra el index.html de Nginx, para editarlo y poner un mensaje personalizado con el comando echo.
```
cd /usr/share/nginx/html
echo "mensaje personalizado" > index.html
```

![c4](https://github.com/mloparj10/Proyecto-k0s/blob/main/images/comprobaciones/c4.JPG)

Y estaría listo el index. Ahora nos vamos a salir de la terminal del pod. Basta con ejecutar un "exit"

## 5. Acceso a la aplicación web Nginx

Vamos a necesitar 2 terminales simultáneas. Para ello nos ayudaremos de la herramienta "tmux". Si no la tienes instalada:
```
apt install tmux
```
Para ejecutarla escribimos "tmux" Y se nos abrirá una terminal limpia, con una barra en la parte inferior. 
Para tener dos consolas, pulsamos CTRL + B y soltamos, después SHITF +  2. Se nos dividirá la terminal en 2, de manera horizontal. Si queremos cambiar entre ellas: CTRL + B y soltamos, después pulsamos flecha hacia arriba o flecha hacia abajo.

Una vez preparada esta "doble consola", nos situamos en la de arriba. Vamos a crear una pasarela por un puerto al pod. Tendremos que utilizar un puerto que esté libre. En este caso he utilizado el 8081, y con dos puntos, indicamos el puerto por el cual corre la aplicación (Nginx), en este caso es el 80.
```
k0s kubectl port-forward pod/pod-nginx-mario 8081:80
```

Empezará a mostrarnos un mensaje que dicre "Forwarding from..." . Eso quiere decir que ahora la aplicación esta corriendo por el puerto 8081. Sin realizar un CTRL + C para cancelar, nos pasamos a la terminal de abajo. y ejecutamos el siguiente comando:
```
curl localhost:8081
```
 Lo que hace la herramienta curl no es solo descargar archivos de internet. Si no que también puede extraer el código html de una página web. Le indicamos que llame a la pagina "localhost" (nuestro servidor donde nos encontramos) y el puerto 8081(puerto por el que hemos hecho que se lance la aplicación previamente). Si al ejecutar el comando muestra el mensaje personalizado que escribimos anteriormente en el index.html, quiere decir que nuestro k0s funciona a la perfección.
 
![c5](https://github.com/mloparj10/Proyecto-k0s/blob/main/images/comprobaciones/c5.JPG)


