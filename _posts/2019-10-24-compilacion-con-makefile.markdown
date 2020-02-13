---
layout: post
title: "Compilación de un programa en C utilizando un Makefile"
date: 2019-10-24 16:57:30 +0530
categories: Debian
published: true
---
### Elige el programa escrito en C que prefieras y comprueba en las fuentes que exista un fichero Makefile para compilarlo.
### Realiza los pasos necesarios para compilarlo e instálalo en tu equipo en un directorio que no interfiera con tu sistema de paquetes (/opt, /usr/local, etc.)


El paquete que he elegido es emacs voy a compilar la versión 26.3

* Descargo el paquete del repositorio del proyecto gnu:

<http://ftp.gnu.org/gnu/emacs/>

* Creo una carpeta en mi directorio personal, voy a esa carpeta y descomprimo el archivo tar.gz
```
mkdir emacs
cd emacs
tar xvfz ../Descargas/emacs-26.3.tar.gz
```
* Miramos el *Makefile* para ver donde instalara el paquete, el mio por ejemplo tiene las siguientes lineas para cambiar ese *prefix* tendríamos que pasarle un parámetro en la ejecución del script de configuración, ejemplo *./configure --prefix=/opt* y tendríamos que añadir esa ruta al *PATH* para poder ejecutarlo 
```
# The default location for installation.  Everything is placed in
# subdirectories of this directory.  The default values for many of
# the variables below are expressed in terms of this one, so you may
# not need to change them.  This defaults to /usr/local.
prefix=/usr/local
```

* Ahora vamos ejecutamos el script de configuración e instalamos el programa. Es probable que cuando ejecutemos el script de configuración nos de errores o advertencias de ciertas dependencias, yo las he instalado con apt, algunas de las dependencias que yo he tenido que instalar son *libgnutls, xorg-dev, libtiff-dev*
```
paco@Ra:~/emacs/emacs-26.3$ ./configure
paco@Ra:~/emacs/emacs-26.3$ make
paco@Ra:~/emacs/emacs-26.3$ sudo make install
```

* Esperamos a que termine y vemos donde se nos ha instalado el paquete
```
paco@Ra:~/emacs/emacs-26.3$ which emacs
/usr/local/bin/emacs
```

* Para desinstalar el programa en mi caso se puede hacer con:
```
make unistall
```

* Para limpiar los ficheros creados durante la compilación en mi caso en el fichero *Makefile* nos da varias opciones de clean
```
make distclean
```
