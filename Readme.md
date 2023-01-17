![ImageODOO](https://www.uadin.com/wp-content/uploads/2020/10/odoo_logo.png)
![ImagePostgres](https://raw.githubusercontent.com/docker-library/docs/01c12653951b2fe592c1f93a13b4e289ada0e3a1/postgres/logo.png)
![ImagenDocker](https://cdn.iconscout.com/icon/free/png-256/docker-3050921-2538289.png)
---

# Odoo con PostgreSQL en Docker

---

### Como empezar:

Lo primero que tendremos que hacer será abrir el PyCharm (Es importante que sea la edición **Profesional**, no la **Community**). A continuacion creamos una carpeta nueva y la abrimos con PyCharm. Dentro, crearemos un nuevo archivo llamado **docker-compose.yml**. 
Este contendrá toda la informacion necesaria para poder ejecutar los servicios y que sean plenamente funcionales. El código del docker-compose lo encontrarás en este repositorio o en este enlace --> [Click aquí](https://github.com/Endermaiter/Odoo-Postgres/blob/master/docker-compose.yml)

---

### Explicación del Docker-compose:

Además del Readme.md, este repositorio contiene el archivo necesario para iniciar los contenedores necesarios para nuestro Odoo: el ***Docker Compose***. Este está compuesto por dos servicios:

- ***Servicio Database (Postgresql):*** Esta es la base de datos que usará el servicio web explicado más adelante:
  * **Imagen:** La imagen es lo que le damos al *docker-compose* para que sepa el servicio que queremos utilizar.
  * **Environment:** Aquí definimos las credenciales de acceso a la base de datos asi como el nombre de la database.
  * **Puertos:** Es necesario mapear los puertos para poder acceder al servicio. (En este caso -> *5432*)
  * **Volumen:** Aunqe no es necesario, podemos usar un volumen para poder acceder a la información del contenedor.
  
  Imagen correspondiente del docker-compose:

  ![DBImage](https://cdn.discordapp.com/attachments/830402260336508938/1064857753299992628/Servicio_DBODOO.png)
- ***Servicio Web (Odoo):*** Este es el servicio que nos permitirá acceder a la web. La estructura es muy similar pero con algunas diferencias. Es decir, también necesita una imagen y mapear los puertos pero puede no usar un environment. Además de eso, le añadimos un depends_on:
  * Depends_on: Apartado relativamente importante que hace que el servicio web dependa de que el servicio **db** esté funcionando. De lo contrario puede haber problemas o dar errores.
  
  Imagen correspondiente del docker-compose:

  ![WebImage](https://cdn.discordapp.com/attachments/830402260336508938/1064857752947654666/Servicio_WebODOO.png)
---

### Procedimiento de lanzamiento de contenedores:

Para lanzar los contenedores, debemos ejecutar el docker-compose previamente explicado. Lo haremos con el siguiente comando en la propia terminal del PyCharm:

```docker-compose up```

Esto solo lo haremos una vez, ya que después usaremos los comandos:

```docker-compose start``` y ```docker-compose stop```,respectivamente, para inicializarlos o detenerlos.

---
### ¿Qué ocurre si en el ordenador local el puerto 5432 está ocupado? ¿Cómo lo puedes solucionar?
En este caso, al intentar lanzar los contenedores, nos dara un error de que ya hay un proceso usando ese puerto, ya que
no es posible tener dos procesos usando el mismo puerto. Para solucionar el problema, tendremos varias opciones:
 
  - ***Opción 1:*** Podemos cambiar el puerto que estemos usando a otro que esté en desuso. (Ej: 5432 -> 5430)
  ####
  - ***Opción 2:*** Podemos detener el proceso que está usando el puerto que nosotros queremos utilizar. Para ello necesitaremos primeramente saber que servicios se están ejecutando a tiempo real. Lo sabemos con el siguiente comando:
    ####
    ```sudo netstat -putan```
    ####
    Este comando nos proporcionará el puerto, entre otras cosas, que están usando los servicios que están en activo en ese momento. Una vez identificado el servicio que está usando el puerto deseado (5432), procederemos a detenerlo con el siguiente comando:
    ####
    ```sudo service [nombre del servicio]* stop```
    ####
    *Se puede autocompletar el nombre del servicio con el tabulador.
    ####
  - ***Opción 3:*** Podemos desinstalar de cuajo el servicio que nos está dando problemas. **[Opción nada recomendable]**
---

### Conexión de PyCharm con Docker y PostgreSQL:

- ***Docker:***
  
  En este caso, en PyCharm tendremos que irnos abajo donde pone **Services**. Le damos al **+** que encontramos en la barra de herramientas superior de la ventana emergente y a **Docker Connection**. Sin tocar nada más, le damos a **OK** y ya nos debería salir todo lo referente a docker que tengamos (Contenedores, Volúmenes, Imágenes...etc)

  Tiene que quedar tal que así:

  ![DockerIDE](https://cdn.discordapp.com/attachments/830402260336508938/1064872187074453544/Captura_desde_2023-01-17_12-41-43.png)

- ***PostgreSQL:***

  Para esta conexión nos dirigimos a la parte derecha del IDE. Encontraremos una bara vertical donde, entre otras cosas, encontramos Database. Clickamos ahí y a continuacion le damos a **+**. Le damos a **Data Source** y seleccionamos PostgreSQL. Ahora nos saldrá la siguiente ventana:

  ![ImagenDBODOO](https://cdn.discordapp.com/attachments/830402260336508938/1064870687203921990/Captura_desde_2023-01-17_12-35-24.png)

  Es importante que escribamos exactamente las credenciales que hemos puesto en el docker compose además del puerto que es 5432 por defecto. No queda mas que darle a Aplicar y Aceptar y ya tendremos la conexion a la base de datos para trabajar con ella.