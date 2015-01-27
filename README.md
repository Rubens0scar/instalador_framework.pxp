Instalador del Framework PXP
===============================

(Este Manual ha sido probado con CENTOS 6.3 y 6.5 version MINIMAL) 

Requisitos
-----------

* Configuracion de red y acceso a internet
* En caso se ser necesario los comandos yum y wget deben estar configurados para utilizar proxy

Instalacion
------------

* Primero instalamos fabric para ejecutar el instalador ya que no viene por defecto en centos

```sh
yum install gcc python-devel python-setuptools git -y
```
Si la conexion es por proxy hacer:

```sh
export http_proxy=http://1.1.1.1:8080
export https_proxy=https://1.1.1.1:8080
```
Luego instalar easy_install

```sh
sudo -E easy_install pip
```

```sh
pip install fabric paramiko==1.10 fexpect
```
Anadir (si la conexion es por proxy) :

```sh
--proxy=http://1.1.1.1:8080
```

* Luego ejecutamos en la carpeta donde se encuentra el instalador

```sh 
fab instalar_pxp
```

* Nos pedira la ip de la maquina a la cual instalar y su contrasena

* Ejecutamos la recuperacion de la base de datos entramos a 

```sh 
cd var/www/html/kerp/pxp/utilidades/restaurar_bd
```

y ahi dentro ejecutar 

```sh 
su postgres -
```

luego

```sh
./restaurar_todo.py
```

NOTAS
-------
* El puerto 22 (ssh) queda abierto para cualquier conexion
* El puerto 5432 (postgres) queda abierto para cualquier conexion
* El protocolo icmp (ping) queda abierto para cualquier conexion


TODO'S
-------

* Buscar solucion a herencia de usuario dbkerp_admin (Temporalmente el instalador le da permiso de superusuario)
* Realizar los cambios necesarios para instalar en dos servidores separados (web y bd)
* Revisar los permisos de usuario apache y postgres sobre las carpetas del framework
* Que el instaador pregunte el nombre del sistema y base de datos
* Una ves instaladas todas las depedencias, es necesario un utilitario para agregar nuevas instancias de sistemas con su propia base de datos,   algo como un SDK
* agregar yum -y install php-xml 
