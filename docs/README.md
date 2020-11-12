# Primeros pasos

Esta sección busca explicar de manera simple, por lo tanto escapando algunos detalles técnicos, para dejar tu computadora lista para empezar a trabajar en un proyecto.

## Preparando entorno de trabajo

Más allá de los permisos de accesos y cuentas mails que se deben habilitar en el proceso. Se puede ir realizando la configuración del entorno de trabajo, instalar las herramientas necesarias, realizar algunas pruebas y tener todo preparado para ese momento.

### Instalar GNU/Linux

Para este proyecto procederemos a preparar nuestro entorno bajo un SO GNU/Linux, lo haremos partiendo desde una laptop con SO Windows.

### Crear Partición

Por lo general trea una herramienta llamada "Crear Partición", desde inicio-buscar la podremos conseguir, una vez encontrada la abrimos, nos aparece nuestro disco con sus distintas particiones, la idea es asignar una parte grande a un espacio vacío para ahí instalar GNU/Linux. Le damos a crear partición, con una de 100GB es suficiente.

### USB ejecutable

Procedemos a descargarnos alguna imagen GNU/Linux (Debian, Ubuntu, etc...).

[Descargar SO KDE Neon for Developers](https://neon.kde.org/download)

Ahora descargamos rufus, app para montar la imagen .iso en el USB y volverlo booteable.

[Descargar rufus](https://rufus.ie/)

### Instalar SO

Reiniciamos la compu.
Por lo general con f2, f8 entramos al menú de booteo donde configuramos que el equipo inicie leyendo el PenDrive antes que el Disco.
Le damos a instalar SO, preferiblemente con cable ethernet conectado.
Seleccionamos idioma, zona horaria, teclado.
En la partición creada desde Windows procedemos a instalar el SO, por lo general se crean 3 particiones dentro de la vacía:
* Una de 1GB para el "área de intercambio".
* Otra de 20GB para los archivos de sistema ("/", ext4).
* El resto para los archivos del usuario ("/home", ext4).
Se deben ver las 3 nuevas que creamos. Siguiente.
Le asignamos el nombre a la compu, usario y clave.
Al finalinalizar te pedirá que saques el pendrive y se reiniciará.

## Instalar Python

Para poder desplegar varias funciones de google cloud y ejecutar el backend, tendremos que tener las siguientes versiones de python:

```bash
wget https://www.python.org/ftp/python/2.7.17/Python-2.7.17.tgz
tar xzf Python-2.7.17.tgz
cd Python-2.7.17/
./configure --enable-optimizations
python2 --version
```

```bash
wget https://www.python.org/ftp/python/3.8.1/Python-3.8.1.tgz
tar xzf Python-3.8.1.tgz
cd Python-3.8.1/
./configure --enable-optimizations
python3 --version
```
## Crear archivo de alias

Para crear un archivo de alias con los comandos que más vamos a utilizar y si te acostumbras me lo agradecerás. Nos vamos a la carpeta raíz:
```bash
cd ~
```
Creamos o abrimos el archivo de los alias con vim y los especifiquemos:
```bash
vim .bash_aliases
```
Con la letra i podemos escribir, con ESC dejamos de escribir y :wq + Enter podemos guardar y salir, salir forzado es :q!
```bash
alias upg="sudo apt-get update && sudo apt-get upgrade"
alias db_proxy="cloud_sql_proxy -instances={proyecto}:{server}:{user}=tcp:{puerto}"
alias proyecto="cd ~/ruta/proyecto"
alias deploy="fga-cli.py deploy app --env dev -- --promote"
```

## Git & Deploy

### Deploy en dev

Creamos una rama a partir de master, por lo general comienza con dev, luego el cuarto del año en curso y un nombre (dev-Q4-informes)

```bash
git checkout -b dev-Q4-informes
```

Verificamos que estamos en la rama creada, la dev, aquí es donde hago mis modificaciones.

```bash
git branch
```

Verifico si tengo archivos por commitear en mi árbol local.
```bash
git status
```

Si los hay pues los levanto a mi espacio de trabajo local. El punto hace referencia a todos los modificados.
```bash
git add .
```

Hago el commit a mi repositorio local, le coloco un mensaje conciso.
```bash
git commit -m "Info contundente"
```

Me voy ahora a la rama master y comienzo la magia de los merge. Esto siguiendo la recete confiable de don Froylan.

```bash
git checkout master 
git pull
git checkout dev-Q4-avaya 
git merge master
git branch
git checkout master 
git merge dev-Q4-avaya 
git push
fga-cli.py deploy app --env dev -- --promote
```
Si eres inteligente y seguiste los pasos de la guía de Juan correctamente, es decir hiciste un login a fga-cli con la cuenta ...completa@dev.bbva.com todo debe salir bien.

::: warning Problemas iniciales con fga-cli
Si tienes problemas para descargar el fga en linux, recuerda bajarle la seguridad ssl a tu compu, /etc/ssl/ssl_config a nivel 1... google con eso.
:::

## Back local a BD

Don Froyd creó una apires flask, para que con el siguiente proxy, nos podamos conectar a la BD de manera local y podamos probar funciones back.

Recomendamos fuertemente que el comando  "db_proxy" lo agregues a tu lista de [alias](#crear-archivo-de-alias) en tu computadora(#Git)

```bash
sudo systemctl stop mysql.service   #Sólo si el puerto 3306 está ocupado sin necesidad
./restart.sh                        #Se corre la primera vez, para todas las instalaciones
db_proxy
. ../env/bin/activate
python runner.py
```