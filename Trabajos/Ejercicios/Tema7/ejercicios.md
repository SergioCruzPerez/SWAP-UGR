## Ejercicio T7.1 ##
¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 0 a partir de dos discos de 100 GB y 100 GB? 200GB sumando ambos discos.
¿Qué tamaño de unidad de unidad RAID se obtendrá al
configurar un RAID 0 a partir de tres discos de 200 GB
cada uno? 600GB al existir 3 discos.

## Ejercicio T7.2 ##
¿Qué tamaño de unidad de unidad RAID se obtendrá al
configurar un RAID 1 a partir de dos discos de 100 GB y
100 GB? 100GB porque RAID1 solamente duplica los datos, no el espacio.
¿Qué tamaño de unidad de unidad RAID se obtendrá al
configurar un RAID 1 a partir de tres discos de 200 GB
cada uno? 200GB,mismo caso que apartado anterior.

## Ejercicio T7.4 ##
Buscar información sobre los sistemas de ficheros en red más
utilizados en la actualidad y comparar sus características. Hacer
una lista de ventajas e inconvenientes de todos ellos, así como
grandes sistemas en los que se utilicen. 

-**SMB/CIFSEs** el sistema nativo de Windows.Permite navegar por los recursos ofrecidos y está orientado al funcionamiento en LAN
-**NFS**: Es el sistema nativo de Unix. No está pensado para navegar por los recursos y funciona en WAN
-**Coda**: El cliente guarda de forma local los ficheros de trabajo, para asegurar la disponibilidad cuando no existe conexión de red
-**Intermezzo**: Inspirado en Coda pero diseñado de nuevo
-**Lustre**: Nuevo desarrollo destinado a supercomputación. Para grandes clusters o procesadores masivamente paralelos (MPP)

**NFS** es enrutable, de manera que el servidor y el cliente pueden estar en diferentes redes comunicadas por un conjunto de routers.
**SMB/CIFS** permite compartir sistemas de archivos e impresoras.
Permite explorar la red para descubrir máquinas y recursos compartidos
**Coda / Intermezzo / Lustre** Los sistemas de ficheros en red Coda e InterMezzo intentan dar soporte a dispositivos móviles que se conectan/desconectan con frecuencia de la red. Para permitir el funcionamiento de los clientes durante las desconexiones de red, estos guardan una copia local (caché) del sistema de archivos remoto.
El sistema de archivos en red Lustre es el nuevo proyecto en el que participan los desarrolladores de InterMezzo, está destinado a la supercomputación y tiene por objetivo conseguir un gran rendimiento al tiempo que resuelve las necesidades de almacenamieno de grandes clusters o máquinas masivamente paralelas.
