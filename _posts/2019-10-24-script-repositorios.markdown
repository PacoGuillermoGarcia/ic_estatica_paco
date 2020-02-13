---
layout: post
title: "Script en bash para comprobar los paquetes de un repositorio"
date: 2019-10-24 16:57:30 +0530
categories: Debian
published: true
---
### Realiza un script que introduciéndolo como parámetro el nombre de un repositorio, muestre como salida los paquetes de ese repositorio que están instalados en la máquina.
```
#Este script sirve para saber los paquetes que estan instalados desde un repositorio que le ponemos nosotros como parametro a la hora de ejecutarlo

#Ejemplos de parametros: http://deb.debian.org/debian

#!/bin/bash

#Guardo el repositorio
repo=$1
#Filtro el comando "dpkg -l" para que me de todos los paquetes que estan instalados y luego con cut me quedo con el nombre
#Hago un bucle para que por cada paquete que este instalado se quede solo con el repositorio del que se ha instalado y lo igualo al repositorio que he guardado al principio que era un parametro 
#Por ultimo muestro el paquete si los dos repositorios son iguales 
for paquete in $(dpkg -l | grep '^ii' | cut -d ' ' -f 3); do
    if [ $repo = $(apt-cache policy $paquete | egrep '\*\*\*' -A1 | tail -1 | awk '{print $2}') ]; then
        echo $paquete
    fi
done
```
