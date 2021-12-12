# Instalación de k0s:
## En Este archivo mostraré como instalé k0s:

Para instalar K0s en el servidor remoto de Clouding realicé los siguientes pasos, todos muy sencillos.

## 1. Descargamos k0s con el comando k0s y le aplicamos el sh para ejecutarlo en el mismo comando.
```
curl -sSLF https://get.k0s.sh |sh
```

![i1](https://github.com/mloparj10/Proyecto-k0s/blob/main/images/instalacionk0s/i1.JPG)

Nos muestra un mensaje indicandonos que la herramienta k0s ya es ejecutable en el sistema.
## 2. Instalación como servicio del sistema en el host local. Indicamos con el praámetro "controller --single" indicamos que será de 1 solo nodo
```
k0s install controller --single
```
![i1](https://github.com/mloparj10/Proyecto-k0s/blob/main/images/instalacionk0s/i2.JPG)


## 3. Iniciamos k0s con un sencillo comando.
```
k0s start
k0s status
```
![i1](https://github.com/mloparj10/Proyecto-k0s/blob/main/images/instalacionk0s/i3.JPG)

Con el segundo comando "status" vemos la version y que el proceso corre perfectamente.

## 4. Una vez teniendo iniciado k0s, vamos a utilizar la herrmaienta kubectl (que ya viene dentro del servicio) para ver los nodos disponibles y que servicios están funcionando

```
k0s kubectl get nodes
k0s kubectl get all
```
![i1](https://github.com/mloparj10/Proyecto-k0s/blob/main/images/instalacionk0s/i4.JPG)

Al realizar el comando "get nodes" observamos que solo hay un nodo funcionando, que es nuestro servidor. Y utilizando "get all" nos muestra que el cluster de Kubernetes esta funcionando sin problemas.
