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
Si todo está bien, queda la partición de Windows y las 3 nuevas que creamos.
Se le esigna el nombre a la compu, tu usario, clave.
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
python2 --version
```

## Git & Deploy

### Deploy en dev

Creamos una rama a partir del master, por lo general comienza con dev, luego el cuarto del año en curso y el nombre (dev-Q4-nombre)

```bash
git checkout -b dev-Q4-plataforma-abogados
```

Hago mis modificaciones sobre esa rama. Para verificar en qué rama estoy.

```bash
git branch
```

Verifico si tengo archivos por commitear en mi árbol local.
```bash
git status
```

Agrego todos mis archivos modificados a mi espacio de trabajo local.
```bash
git add .
```

Hago el commit a mi repositorio local, les coloco un mensaje que en corto explique mucho
```bash
git commit -m "Informes Avaya Opciones"
```

Me voy a master o seguro en un futuro main, actualizo mi main local trayéndome todos los cambios que hayan arriba en el repositorio compartido, luego mezclo esos cambios a mi rama (Consejos de Froylan), de ahí me voy a master y le hago un merge de la mezcla que tengo en la rama. Hago el gran push al repositorio online.
```bash
git status
git checkout master 
git pull
git checkout dev-Q4-avaya 
git merge master
git branch
git checkout master 
git merge dev-Q4-avaya 
git push
```
Si eres inteligente y seguiste los pasos de la guía de Juan como se debe, es decir hiciste un login bla@dev.bbva.com en el fga-cli.py (Si tienes problemas para descargar no es 404, es bajarle la seguridad ssl a tu compu, /etc/ssl/ssl_config a nivel 1... google con eso).

Te vas a la carpeta del proyecto y corres

```bash
fga-cli.py deploy app --env dev -- --promote
```

### Deploy en producción

¿Del 1 al 10 que tan seguro estás?