# Programación WEB (electiva)

## Maquina Virtual

La maquina virtual tiene instalado [Lubuntu Linux 18.04](http://lubuntu.net/), es la distribución más liviana de Ubuntu. Se puede descargar desde [aquí](https://www.dropbox.com/s/yvcvni643i8h68u/WEB2018-lubuntu18.04.7z?dl=0)

### Requerimientos para el correcto funcionamiento de la maquina virtual

Para que funcione la maquina virtual es necesario tener instalado lo siguiente:

* Sistema Operativo de 64bits.

* para poder descomprimir el archivo es necesario tener instalado 7zip, se puede descargar desde [la web oficial de 7zip](http://www.7-zip.org/download.html)

* Vmware Workstation Player [se puede descargar desde la web oficial de VmWare](https://my.vmware.com/en/web/vmware/free#desktop_end_user_computing/vmware_workstation_player/14_0)

<!-- o VirtualBox [se puede descargar desde la web oficial de VirtualBox](https://www.virtualbox.org/wiki/Downloads) -->

* 10GB de espacio libre en un disco.

### Pasos a seguir para iniciar la maquina Virtual

1. Descargar el archivo de la maquina virtual desde [aquí](https://www.dropbox.com/s/yvcvni643i8h68u/WEB2018-lubuntu18.04.7z?dl=0)
1. Descomprimir el archivo en un disco Local.

<!--
1. Abrir la aplicación  de virtualización ( VmWare o VirtualBox), seleccionar el menu importar, abrirá el asistente donde tendremos que seleccionar dentro de la carpeta descomprimida el archivo **lubuntu17.04_web.ovf** y luego seguir el asistente, el proceso de importación va a demorar unos minutos, y luego quedará disponible la maquina virtual para iniciar.
-->

## Instalar todo el software que usaremos

en caso de no poder ejecutar la maquina virtual se puede seguir los siguientes pasos para instalar todo el software que usaremos en una pc con ubuntu recién Instalado.

### 1. Actualizar la base de datos local de paquetes

**sudo** permite ejecutar un comando con privilegios de super usuario **root**
**apt**  es el nuevo gestor de paquetes de ubuntu pasando el parámetro **update** actualiza la base de datos de paquetes disponibles para ubuntu desde los repositorios que tenga configurado.

```bash
sudo apt update
```

### 2. Actualizar los paquetes

**apt upgrade** actualiza los paquetes instalados actualmente en el sistemas con el parámetro adicional **-y** indicamos que no pida confirmación para actualizar

```bash
sudo apt upgrade -y
```

### 3. Opcional (Si la maquina es Virtual es recomendable instalar open-vm-tools open-vm-tools-desktop)

si la maquina que tiene instalado ubuntu es **virtual**, es recomendable instalar las tools para maquinas virtuales, para tener compatibilidad con la resolución de pantalla, permitir el uso del porta papeles entre la maquina virtual y el host, etc.

```bash
sudo apt install open-vm-tools open-vm-tools-desktop
```

### 4. Instalar Google Chrome y Visual Studio Code

**Visual Studio Code** y **Google Chrome** lamentable mente no están en los repositorios oficiales por lo que es necesario instalar desde el sitio web oficial de cada uno, una vez instalado, se actualizan la fuentes de paquetes para que en el futuro cuando intentes actualizar el software puedas hacerlo directamente desde **apt**.

#### 4.1 [Descargar **visual estudio code** desde la web oficial](https://code.visualstudio.com/download)

#### 4.2 [Descargar **google chrome** desde desde la web oficial](https://www.google.com/chrome/index.html)

#### 4.3 abrir una terminal

#### 4.4 ir al directorio de Descargas

el comando **cd** nos sirve para cambiarnos de directorio, por defecto cuando se abre una terminal el directorio en el que se está parado es el directorio home del usuario **/home/usuario** y dentro de ese directorio se encuentra el directorio **Descargas** que es donde se descargan los archivos por defecto.

```bash
cd Descargas/
```

#### 4.5 Instalar todos los paquetes con extensión **deb** que estén en el directorio Descargas

**dpkg** también es un gestor de paquetes de debian linux, con el parámetro **-i** se indica que se va a instalar paquetes ***.deb** es una expresión regular que busca todos los archivos con extensión **deb** que es la extensión que usan las distribuciones basadas en debian linux para paquetes de instalación.

```bash
sudo dpkg -i *.deb
```

#### 4.6 instalar las dependencias que faltan para que funcione chrome y visual studio code

cuando se usa **dpkg** para instalar paquetes no se descargan las dependencias del software, por eso es necesario usar nuevamente **apt** con los parámetros
**--fix-broken** para que descargue las dependencias necesarias

```bash
sudo apt --fix-broken install
```

#### 4.7 actualizar nuevamente la base de datos local de paquetes

```bash
sudo apt update -y
```

#### 4.8 actualizar los paquetes

```bash
sudo apt upgrade -y
```

### 5 instalar utilidades

```bash
sudo apt install -y vim curl git git-flow git-gui
```

* **vim** es un editor de texto que funciona en la terminal de linux.
* **curl** es una herramienta para transferencia de archivos en la terminal de linux.
* **git** es la herramienta para control de versiones de archivos más utilizada en la actualidad.
* **git-flow** es un plugin para administrar el flujo de trabajo en **git**.
* **git-gui**  es una interfaz gráfica para **git**.

### 6 instalar MYSQL y el Workbench

Va a pedirles una **nueva contraseña para el usuario root de MySQL**, el usuario root de mysql no tiene nada que ver con el usuario del sistema operativo.

```bash
sudo apt install -y mysql-server mysql-workbench
```

### 7 Instalar NODEJS

#### 7.1 [instalar nodejs preferentemente con **nvm**](https://github.com/creationix/nvm)

```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
# cerrar y volver a abrir la terminal
```

#### 7.2 instalar nodejs desde nvm

```bash
nvm install node
```

#### 7.3 utilidades en nodejs

```bash
npm i -g json-server
npm i -g eslint
```

### 8 Apache, PHP y Composer

```bash
sudo apt install -y apache2 php php-mysql php-mbstring php-token-stream php-xml
```

#### 8.1 [instalar composer según la web oficial](https://getcomposer.org/download/)

```bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

#### 8.2 habilitar composer para todos los usuarios

```bash
sudo mv composer.phar /usr/bin/composer
```

#### 8.3 crear un proyecto de prueba en laravel

##### 8.3.1 crear un proyecto con la ultima versión de laravel

```bash
composer create-project --prefer-dist laravel/laravel lara01
```

##### 8.3.2 crear un proyecto con un versión especifica de laravel

si necesitamos crear una aplicación web con una versión especifica de laravel se agrega al final la versión como podemos observar en el siguiente ejemplo:

```bash
composer create-project --prefer-dist laravel/laravel lara01  '5.5.*'
```

podemos apreciar **'5.5.*'** representa la ultima versión LTS al día de hoy [Aquí podemos ver las versiones de laravel](https://laravel.com/docs/releases).
y como la versión traducida al castellano de la documentación oficial de laravel es la **5.5** ( [podemos encontrar la documentación de laravel traducida aquí](https://docs.laraveles.com/docs/5.5) ) es recomendable usar está versión en este momento.

#### 8.4 verificar el funcionamiento de la nueva aplicación laravel

```bash
cd lara01
php artisan serve
```