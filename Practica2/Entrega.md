# Práctica2

En esta práctica el objetivo es configurar las máquinas virtuales para trabajar en modo
espejo, consiguiendo que una máquina secundaria mantenga siempre actualizada la
información que hay en la máquina servidora principal.
Hay que llevar a cabo las siguientes tareas:
1. probar el funcionamiento de la copia de archivos por ssh
2. clonado de una carpeta entre las dos máquinas
3. configuración de ssh para acceder sin que solicite contraseña
4. establecer una tarea en cron que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos máquinas

**Probar el funcionamiento de la copia de archivos por ssh**

Comprobamos que ambas máquinas se ven entre sí, usando el comando *ping* seguido de la **ip_de_cada_máquina**
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica2/fotos/Captura%20de%20pantalla%20de%202018-04-03%2017-44-52.png)
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica2/fotos/Captura%20de%20pantalla%20de%202018-04-03%2017-45-17.png)


Primero, hacemos que el usuario sea dueño de la carpeta /var/www mediante la orden *chown* tanto en una máquina como en otra para que al ejecutar la orden
**rsync** no proporcione ningún tipo de error y se lleve a cabo correctamente.
Se ilustra para la máquina 1, pero se procedera de la misma forma para la máquina 2.
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica2/fotos/Captura%20de%20pantalla%20de%202018-04-03%2018-28-51.png)

Y ya mediante la herramienta **rsync** cumplimos el primer objetivo del apartado 1.
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica2/fotos/Captura%20de%20pantalla%20de%202018-04-03%2018-29-23.png)

Cabe destacar que rsync hace uso de distintas opciones para llevar a cabo la copia de una manera o de otra como bien se señala en el guión de prácticas.
Además como bien se señala en el guión, bastaría con haber usado la orden tar y mediante un **'|'** mandar la salida a *ssh*.

**Acceso sin contraseña para ssh**

**ssh-keygen -b 4096 -t rsa** Lo ejecutams en SWAP2, que es la máquina que vamos a usar para almacenar copias de seguridad peridicas etc.

![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica2/fotos/Captura%20de%20pantalla%20de%202018-04-04%2017-00-05.png)

Una vez generada la clave ejecutamos el comando **ssh-copy-id** para copiar la clave en la máquina 1 de forma elegante.
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica2/fotos/Captura%20de%20pantalla%20de%202018-04-04%2017-06-13.png)

Cabe destacar que si quisiéramos ejecutar comandos en la máquina a la cual nos conectamos mediante ssh, bastaría con añadir el comando
al final de la orden ssh seguida de la ip de la máquina a la cual deseamos conectarnos.
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica2/fotos/Captura%20de%20pantalla%20de%202018-04-04%2017-07-48.png)

Teniendo preparado el acceso por **ssh sin contraseña**, podemos hacer uso del *rsync* desde scripts que se ejecuten automáticamente con el cron.

**Programar tareas con crontab**

Establecer una tarea en cron que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos máquinas.
Lo que vamos a hacer es mantener actualizado el contenido de /var/www/ en la máquina 2 con respecto a máquina 1.
Bastara con acceder al fichero /etc/crontab de la máquina 2 y añadir la siguiente línea.

![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica2/fotos/Captura%20de%20pantalla%20de%202018-04-04%2017-20-19.png)

![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica2/fotos/Captura%20de%20pantalla%20de%202018-04-04%2017-20-09.png)
