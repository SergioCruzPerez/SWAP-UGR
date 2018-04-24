Práctica3

En esta práctica configuraremos una red entre varias máquinas de forma que
tengamos un balanceador que reparta la carga entre varios servidores finales.
El problema a solucionar es la sobrecarga de los servidores. Se puede balancear
cualquier protocolo, pero dado que esta asignatura se centra en las tecnologías web,
balancearemos los servidores HTTP que tenemos configurados.
De esta forma conseguiremos una infraestructura redundante y de alta disponibilidad.

La dirección de red en la que están todas las máquinas es: 192.168.1.0.

SWAP1: 192.168.1.50
SWAP2: 192.168.1.100
balanceador: 192.168.1.105
peticiones: 192.168.1.110

Balancear la carga usando Nginx.

LO instalamos en la máquina balanceador
sudo apt-get install nginx

Una vez que lo tenemos instalado, iniciamos el servicio y comprobamos que lo tenemos funcionando.

Tenemos que modificar el siguiente fichero /etc/nginx/conf.d/default.conf  ya que la configuración que viene por defecto no es útil.

Para que nginx deje de funcionar como servidor y funcione como balanceador hay que tocar el siguiente archivo /etc/nginx/nginx.conf y habría que comentar la siguiente la línea 
include /etc/nginx/sites-enabled/*;


