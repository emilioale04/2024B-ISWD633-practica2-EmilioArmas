## Esquema para el ejercicio
![Imagen](img/esquema-ejercicio5.PNG)

### Crear la red
```
docker network create net-wp -d bridge
```

### Crear el contenedor mysql a partir de la imagen mysql:8, configurar las variables de entorno necesarias
```
docker run -d --name contenedor-mysql -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=wordpressdb --network net-wp mysql:8
```

### Crear el contenedor wordpress a partir de la imagen: wordpress, configurar las variables de entorno necesarias
```
docker run -d --name contenedor-wordpress -p 9300:80 --network net-wp wordpress
```

De acuerdo con el trabajo realizado, en el esquema de ejercicio el puerto a es **9300**


Ingresar desde el navegador al wordpress y finalizar la configuración de instalación.

### Dirección Contenedor MySQL

![net-wp_inspect](screenshots/mysql_ip.png)

### Configuración Wordpress

![wordpress_config](screenshots/wordpress_config.png)

Desde el panel de admin: cambiar el tema y crear una nueva publicación.
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress
# COLOCAR UNA CAPTURA DEL SITO EN DONDE SEA VISIBLE LA PUBLICACIÓN.

![wordpress_publicacion](screenshots/wordpress_publicacion.png)


### Eliminar el contenedor wordpress
```
docker stop contenedor-wordpress

docker rm contenedor-wordpress
```

### Crear nuevamente el contenedor wordpress
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress

![wordpress_rm](screenshots/wordpress_rm.png)

### ¿Qué ha sucedido, qué puede observar?

Se borró la configuración anterior del anterior contenedor de wordpress

![new_container_wordpress](screenshots/wordpress_new.png)