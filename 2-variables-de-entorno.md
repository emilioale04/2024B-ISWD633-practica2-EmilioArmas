# Variables de Entorno
### ¿Qué son las variables de entorno
# COMPLETAR

### Para crear un contenedor con variables de entorno?

```
docker run -d --name <nombre contenedor> -e <nombre variable1>=<valor1> -e <nombre variable2>=<valor2>
```

### Crear un contenedor a partir de la imagen de nginx:alpine con las siguientes variables de entorno: username y role. Para la variable de entorno rol asignar el valor admin.

```
docker run -d --name srv-nginx -e username=emilio -e role=admin nginx:alpine

docker exec -it srv-nginx sh

/ # echo $username
/ # echo $role
```

# CAPTURA CON LA COMPROBACIÓN DE LA CREACIÓN DE LAS VARIABLES DE ENTORNO DEL CONTENEDOR ANTERIOR

![nginx_variables_entorno](screenshots/nginx_env_var.png)

### Crear un contenedor con mysql:8 , mapear todos los puertos

```
docker run -d --name mysql-cont --publish published=3306,target=3306 mysql:8
```

### ¿El contenedor se está ejecutando?

No, únicamente se creó el contenedor.

### Identificar el problema

Falta especificar variables de entorno para la contraseña.

![mysql_logs](screenshots/mysql_error_logs.png)

### Eliminar el contenedor creado con mysql:8 
```
docker rm mysql-cont
```

### Para crear un contenedor con variables de entorno especificadas
- Portabilidad: Las aplicaciones se vuelven más portátiles y pueden ser desplegadas en diferentes entornos (desarrollo, pruebas, producción) simplemente cambiando el archivo de variables de entorno.
- Centralización: Todas las configuraciones importantes se centralizan en un solo lugar, lo que facilita la gestión y auditoría de las configuraciones.
- Consistencia: Asegura que todos los miembros del equipo de desarrollo o los entornos de despliegue utilicen las mismas configuraciones.
- Evitar Exposición en el Código: Mantener variables sensibles como contraseñas, claves API, y tokens fuera del código fuente reduce el riesgo de exposición accidental a través del control de versiones.
- Control de Acceso: Los archivos de variables de entorno pueden ser gestionados con permisos específicos, limitando quién puede ver o modificar la configuración sensible.

Previo a esto es necesario crear el archivo y colocar las variables en un archivo, **.env** se ha convertido en una convención estándar, pero también es posible usar cualquier extensión como **.txt**.
```
docker run -d --name <nombre contenedor> --env-file=<nombreArchivo>.<extensión> <nombre imagen>
```
**Considerar**
Es necesario especificar la ruta absoluta del archivo si este se encuentra en una ubicación diferente a la que estás ejecutando el comando docker run.

### Crear un contenedor con mysql:8 , mapear todos los puertos y configurar las variables de entorno mediante un archivo

```
docker run -d --name mysql-cont --env-file=./mysql_docker_config.env mysql:8
```
![mysql_run](screenshots/mysql_run_env_file.png)

# CAPTURA CON LA COMPROBACIÓN DE LA CREACIÓN DE LAS VARIABLES DE ENTORNO DEL CONTENEDOR ANTERIOR 

![mysql_env_var](screenshots/mysql_env_var.png)

### ¿Qué bases de datos existen en el contenedor creado?

```
docker exec -it mysql-cont bash

bash# mysql -u root -p

mysql> show databases;
```


![mysql_databases](screenshots/mysql_db.png)
