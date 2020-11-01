# Preparando entorno de trabajo

Más allá de los permisos de accesos y cuentas mails que se deben habilitar en el proceso. Se puede ir realizando la configuración del entorno de trabajo, instalar las herramientas necesarias, realizar algunas pruebas y tener todo preparado para ese momento.

# Instalar GNU/Linux

Para este proyecto procederemos a preparar nuestro entorno bajo un SO GNU/Linux, lo haremos partiendo desde una laptop con SO Windows.

## Crear Partición

Por lo general trea una herramienta llamada "Crear Partición", desde inicio-buscar la podremos conseguir, una vez encontrada la abrimos, nos aparece nuestro disco con sus distintas particiones, la idea es asignar una parte grande a un espacio vacío para ahí instalar GNU/Linux. Le damos a crear partición, con una de 100GB es suficiente.

## USB ejecutable

Procedemos a descargarnos alguna imagen GNU/Linux (Debian, Ubuntu, etc...).

[Descargar SO KDE Neon for Developers](https://neon.kde.org/download)

Ahora descargamos rufus, app para montar la imagen .iso en el USB y volverlo booteable.

[Descargar rufus](https://rufus.ie/)

## Instalar SO

Reiniciamos la compu.
Por lo general con f2, f8 entramos al menú de booteo donde configuramos que el equipo inicie leyendo el PenDrive antes que el Disco.
Le damos a instalar SO, preferiblemente con cable ethernet conectado.
Seleccionamos idioma, zona horaria, teclado.
En la partición creada desde Windows procedemos a instalar el SO, por lo general se crean 3 particiones dentro de la vacía:
- Una de 1GB para el "área de intercambio".
- Otra de 20GB para los archivos de sistema ("/", ext4).
- El resto para los archivos del usuario ("/home", ext4).
Si todo está bien, queda la partición de Windows y las 3 nuevas que creamos.
Se le esigna el nombre a la compu, tu usario, clave.
Al finalinalizar te pedirá que saques el pendrive y se reiniciará.

# Instalar Python

Para poder desplegar varias funciones de google cloud y ejecutar el backend, tendremos que tener las siguientes versiones de python:

<code-group>
<code-block title="Version 2.7.17">
```bash
wget https://www.python.org/ftp/python/2.7.17/Python-2.7.17.tgz
tar xzf Python-2.7.17.tgz
cd Python-2.7.17/
./configure --enable-optimizations
python2 --version
```
</code-block>

<code-block title="Version 3.8.">
```bash
wget https://www.python.org/ftp/python/3.8.1/Python-3.8.1.tgz
tar xzf Python-3.8.1.tgz
cd Python-3.8.1/
./configure --enable-optimizations
python2 --version
```
</code-block>
</code-group>