# Práctica 5: Replicación de bases de datos MySQL #
Cabe destacar en esta práctica que el usuario de ambas máquinas es el mismo porque he decidido clonar la máuinq 2 en máquina 1 y cambiarle la ip debido a la existencia de un problema con MySql, el cual me era imposible solucionar.
Los objetivos de la práctica 5 son: clonar manualmente una base de datos entre máquinas y configurar la estructura maestro-esclavo entre dos máquinas para realizar el clonado automáticamente de la información.

## Creación de una base de datos e inserción de datos ##
Usamos la interfaz de línea de comandos de mysql: **mysql -uroot -p**

Creamos una base de datos con el nombre de contactos, y dentro de ella creamos una tabla para poder operar y mostrar el funcionamiento.
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica5/fotos/imagen2)

Insertamos valores, para tener algo que copiar ya que si no, no tendría sentido copiar absolutamente nada.
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica5/fotos/imagen3)

## Replicar una base de datos con mysqldump ##
Debemos de bloquear la base de datos mientras se está haciendo el volcado con mysqldump para evitar que surjan problemas, por ejemplo de seguridad.

Dentro de la interfaz de la línea de comandos, ejecutaríamos **FLUSH TABLES WITH READ LOCK;**
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica5/fotos/imagen4)

Realizado esto, iríamos a la máquina 1 para copiar el archivo ejemplo.sql con los datos salvados.

![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica5/fotos/imagen5)

Es necesario crear la base de datos correspondiente en la máquina 1 porque mysqldump no incluye la opción para indicar que cree la base de datos.
Para ello primero creamos la base de datos y luego restauramos los datos contenidos en la base de datos creada.

![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica5/fotos/imagen6)

## Replicación de BD mediante una configuración maestro-esclavo. ##
Consiste en demonizar lo realizado anteriormente para que todo cambio en maestro(máquina 2) se refleje en esclavo(máquina 2).

En el archivo /etc/mysql/mysql.conf.d/mysqld.conf los siguientes cambios:
-Comentar la línea **bin_address**

-Indicarle el fichero para almacenar errores: línea **log_error**

-Descomentar las líneas de **server-id** y **log_bin**

![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica5/fotos/imagen7)
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica5/fotos/imagen8)

Reiniciamos el servicio 

![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica5/fotos/imagen9)

Hacemos la misma configuración en el esclavo con la única diferencia que en el server-id le indicamos un 2. Y reiniciamos el servicio.

Procedemos a crear un usuario en el maestro que tenga permisos para la replicación.

![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica5/fotos/imagen10)

Ahora en el esclavo indicamos los datos del maestro y posteriormente lo iniciamos.

![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica5/fotos/imagen11)

En maestro volvemos a activar las tablas.

![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica5/fotos/imagen12)

Comprobamos si está todo correcto con la orden **SHOW SLAVE STATUS\G** y si, funciona todo correctamente poeque el campo *Seconds_behind_master* tiene el valor 0.

![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica5/fotos/Captura%20de%20pantalla%20de%202018-05-23%2013-33-46.png)

De primeras no me funcionaba debido a que las máquinas estaban clonadas y tenían el mismo server UUID para MySQL y lo he arreglado mediante **rm /var/lib/mysql/auto.cnf**
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica5/fotos/imagen13)



