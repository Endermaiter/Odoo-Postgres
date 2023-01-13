# Odoo con Postgresql

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

