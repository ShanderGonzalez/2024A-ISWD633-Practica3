## Esquema para el ejercicio
![Imagen](imagenes/esquema-ejercicio3.PNG)

### Crear red net-wp
```
docker network create net-wp
```

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
La informacion es almacenada en  ```/var/lib/mysql``` dentro del contenedor. Por lo que al montar un volumen sus datos no se perderan asegurando la persistencia
En el esquema del ejercicio la carpeta contenedor (a) es (/var/lib/mysql)
Ruta carpeta host: C:\Users\shander\Desktop\2024A-ISWD633-Practica3\ejercicio3\db

### ¿Qué contiene la carpeta db del host?
Por ahora no contiene nada, pero luego de crear el volumen contendria toda la informacion que esta en ```/var/lib/mysql```

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
```
docker run -P -d --name mysql --env-file=${PWD}/ejercicio3/varMySQL.env -v ${PWD}/ejercicio3/db:/var/lib/mysql --network net-wp mysql:8
```

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
Ahora la carpeta db contiene toda la informacion(archivos y directorios) que esta presente en el contenedor mysql creado en base al directorio ```/var/lib/mysql```

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta contenedor (b) es (/var/www/html)
Ruta carpeta host: C:\Users\shander\Desktop\2024A-ISWD633-Practica3\ejercicio3\www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
```
docker run -P -d --name wordpress --env-file=${PWD}/ejercicio3/varWordPress.env -v ${PWD}/ejercicio3/www:/var/www/html --network net-wp wordpress
```

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?

Cuando se elimina y recrea el contenedor, las configuraciones y contenidos previamente añadidos se mantienen, ya que están almacenados en un volumen conectado desde el servidor principal. Esto garantiza que cualquier modificación hecha en WordPress se conserve, incluso si el contenedor se borra y se vuelve a crear.



