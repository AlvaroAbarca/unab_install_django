# Guía de instalación de Django & Vagrant

## Objetivos
El objetivo de la siguiente guía es entregar un listado de pasos que guían al usuario o alumno a instalar el ambiente de desarrollo para proyectos basados en pytho/django bajo un ambiente unificado utilizando Vagrant.

## Instalación
Como primera parte debemos tener instalado [Virtualbox](http://www.virtualbox.org) y [Vagrant](http://www.vagrantup.com) que los puedes descargar de sus respectivos sitios oficiales.

Una vez instalado Virtualbox y Vagrant procedemos a realizar los siguientes pasos.

***Nota: Este tutorial está escrito en ubuntu 16.04 pero debería funcionar sin problemas en windows. pero debes tener instalado el paquete de git-bash. Por lo que cuando se menciona abrir una terminal, para el caso de windows hace referencia a git bash***

## Instalando ambiente
Desde la terminal debes escribir 
```sh
mkdir vagrant_unab
```
Luego accedes al directorio creado con
```sh
cd vagrant_unab 
```

Desde el directorio debemos bajar nuestro box que nos permitirá montar nuestro ambiente Django y Python sobre nuestra maquina.
Para ello descargaremos el box utilizando el programa *wget* ejecutando la siguiente instrucción

```sh
wget http://phoenix.ewok.cl/vagrant_boxes/vagrant_unab.box
```
Con esto descargamos nuestro box por lo que ahora procedemos a su instalación.

Como estamos parados en el directorio *~/vagrant_unab* solo basta con ejecutar los siguientes pasos:
```sh
vagrant box add vagrant_unab vagrant_unab.box
```
Este comando instalará el box en nuestro sistema. tomará un poco de tiempo. También lo podríamos haber ejecutado directo desde internet a través del comando *vagrant box add vagrant_unab http://phoenix.ewok.cl/vagrant_boxes/vagrant_unab.box* pero prefiero verlo como procesos separados en esta primera entrega.

Luego de cargar el ambiente es necesario, inicializar nuestro ambiente vagrant. Para ello ejecutamos la siguiente instrucción:

```sh
vagrant init vagrant_unab
```

Esto generará un archivo de configuración llamado  `Vagrantfile` que luego editaremos para configurar nuestro ambiente.

Para probar si funciona el ambiente basta con ejecutar

 ```sh
 vagrant up
 ```
 
si les aparece algo similar a esta pantalla estaríamos okey con la instalación del ambiente
 
 // pegar foto de successfull

## Configurando Vagrant
El siguiente paso es configurar el forwarding de puertos para poder visualizar nuestro proyecto a través de la maquina local.

Para esto editamos el archivo *Vagrantfile* que se encuentra en la raiz de nuestro proyecto *~/vagrant_unab/Vagrantfile*

En este archivo debemos descomentar la siguiente línea. Es decirm buscar la línea
 ```sh
   # config.vm.network "forwarded_port", guest: 80, host: 8080
```
y dejarla así
 ```sh
 config.vm.network "forwarded_port", guest: 8080, host: 8080
 ```
 
 Guardamos el archivo y debemos reiciar nuestro vagrant para que aplique los cambios. Para hacer este proceso basta con ejecutar
 
  ```sh
  vagrant reload
   ```
Si todo sale bien debería aparecer algo similar a la siguiente foto

//pegar foto de vagrant reload

Ahora debemos acceder al vagrant a través del comando vagrant ssh
 
  ```sh
  vagrant ssh
   ```
   
Con esto nos conectamos a la maquina linux de nuestro vagrant. Acá vamos a instalar nuestro primer proyecto de Django.

Para el proyecto de Django usaremos [virtualenv](http://rukbottoland.com/blog/tutorial-de-python-virtualenv/), utilidad que nos permite aislar nuestros ambientes de desarrollo con el objetivo de evitar problemas de versiones de bibliotecas, configuraciones, dependencias, etc. 

Para ello crearemos un ambiente con virtualenv ejecutando la siguiente instrucción

```sh
virtualenv demo_unab
```
Con esto nos creará un ambiente para nuestro proyecto. Luego accedemos a él usando 
```sh
cd demo_unab/
```

desde ese directorio debemos activar nuestro ambiente virtual, esto se hace ejecutando la siguiente instrucción:
```sh
source bin/activate
```
Esto activa el ambiente. nos daremos cuenta de esto por que se mostrará el nombre del ambiente al lado derecho del prompt entre parentesis. Ejemplo
```sh
(demo_unab)vagrant@precise32:~/demo_unab$ 
```

Ahora que tenemos el ambiente activo podemos instalar django y crear nuestra primera aplicación.

## Instalando Django

Para la instalación de Django lo pimero que debemos hacer es instalar el paquete de django y esto se hace a través de:
```sh
 pip install django
```
```sh
mkdir src 
```
```sh
django-admin startproject demo .
```
```sh
python manage.py migrate
```

```sh
python manage.py runserver 0.0.0.0:8080
```
```sh
(demo_unab)vagrant@precise32:~/demo_unab/src$ python manage.py runserver 0.0.0.0:8080
Performing system checks...

System check identified no issues (0 silenced).
June 07, 2016 - 15:37:07
Django version 1.10a1, using settings 'demo.settings'
Starting development server at http://0.0.0.0:8080/
Quit the server with CONTROL-C.
```

## Compartiendo directorios
Para el desarrollo realizaremos una configuración que nos permita compartir directorios entre 


