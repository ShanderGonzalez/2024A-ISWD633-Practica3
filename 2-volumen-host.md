# VOLUMEN TIPO HOST
Un volumen host (o bind mount) es un tipo de volumen donde se monta un directorio o archivo específico del sistema de archivos del host en un contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```

### Crear un volumen tipo host con la imagen nginx:alpine, para la ruta carpeta host: directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html esta ruta se obtiene al revisar la documentación
![Volúmenes](imagenes/volumen-host.PNG)
```
docker run -d -P --name host-nginx -v .\nginx\html\:/usr/share/nginx/html nginx:alpine
```

### ¿Qué sucede al ingresar al servidor de nginx?
Aparece un error de 403 Forbidden el cual el sitio web no tiene permisos para acceder a los archivos de la carpeta especificada

### ¿Qué pasa con el archivo index.html del contenedor?
Al inicio cuando no se tiene creado el index.html muestra el error de 403, pero si se agrega el index.html a la ruta, se muestra el html generado correctamente

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de nginx/html
![image](https://github.com/ShanderGonzalez/2024A-ISWD633-Practica3/assets/94009521/3998c539-5eb7-4dda-bdf2-5e0329b10495)

### ¿Qué sucede al ingresar al servidor de nginx?
Se visualiza el template que se descargo, ya que se tiene el index.html

### Eliminar el contenedor
```
docker rm host-nginx
```

### ¿Qué sucede al crear nuevamente el mismo contenedor con volumen de tipo host a los directorios definidos anteriormente?
Al crear el mismo contendor, sigue apareciendo el mismo template que se descargo, por lo tanto se hace una referencia del mismo, eso que dentro de la ruta no se modifico nada

### ¿Qué hace el comando pwd?
El comando pwd (print working directory) muestra la ruta del directorio actual en el que te encuentras.
Si quieres incluir el comando pwd dentro de un comando de Docker, lo puedes hacer de diferentes maneras dependiendo del shell que estés utilizando.


### Volumen tipo host usando PWD y PowerShell
```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v ${PWD}/<ruta relativa>:<ruta absoluta> <nombre imagen>:<tag> 
```

### Volumen tipo host usando PWD (Git Bash)

```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v $(pwd -W)/html:/usr/share/nginx/html <nombre imagen>:<tag> 
```

### Volumen tipo host usando PWD (en Linux)

```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v $(pwd)/html:/usr/share/nginx/html <nombre imagen>:<tag> 
```

