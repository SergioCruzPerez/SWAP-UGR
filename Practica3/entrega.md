# Práctica3:Balanceo de carga #

En esta práctica configuraremos una red entre varias máquinas de forma que
tengamos un balanceador que reparta la carga entre varios servidores finales.
El problema a solucionar es la sobrecarga de los servidores. Se puede balancear
cualquier protocolo, pero dado que esta asignatura se centra en las tecnologías web,
balancearemos los servidores HTTP que tenemos configurados.
De esta forma conseguiremos una infraestructura redundante y de alta disponibilidad.

La **dirección de red** en la que están todas las máquinas es: **192.168.1.0**.

SWAP1: 192.168.1.50
SWAP2: 192.168.1.100
balanceador: 192.168.1.105
peticiones: 192.168.1.110
balanceador-haproxy: 192.168.1.120

## Balancear la carga usando Nginx. ##

Lo instalamos en la máquina balanceador mediante *sudo apt-get install nginx*

Una vez que lo tenemos instalado, iniciamos el servicio y comprobamos que lo tenemos funcionando.
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica3/fotos/Captura%20de%20pantalla%20de%202018-04-19%2017-06-21.png)

Tenemos que modificar el siguiente fichero /etc/nginx/conf.d/default.conf  ya que la configuración que viene por defecto no no es útil para lo que queremos realizar. ![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica3/fotos/Captura%20de%20pantalla%20de%202018-04-19%2017-15-11.png)

Para que nginx deje de funcionar como servidor y funcione como balanceador hay que tocar el siguiente archivo /etc/nginx/nginx.conf y habría que comentar la siguiente la línea 
*include /etc/nginx/sites-enabled/*;*
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica3/fotos/Captura%20de%20pantalla%20de%202018-04-19%2017-18-40.png)

### Tipos de funcionamiento de Nginx ###

Primero adjunto una captura de funcionamiento de Nginx mediante algoritmo de Round-Robin.
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica3/fotos/Captura%20de%20pantalla%20de%202018-04-24%2011-54-48.png)
Para configurar Nginx para que funcione mediante balanceo ponderado tenemos que añadir en */etc/nginx/conf.d/default.conf* para cada servidor un peso "weight", en mi caso 2 para el servidor 1 y 1 para el servidor 2 y el funcionamiento sería el siguiente
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica3/fotos/Captura%20de%20pantalla%20de%202018-04-24%2011-56-39.png)

## Balancear la carga usando haproxy ##

Lo instalamos en la máquina balanceador-haproxy mediante *sudo apt-get install haproxy*

Una vez que lo tenemos instalado, iniciamos el servicio y comprobamos que lo tenemos funcionando.
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica3/fotos/Captura%20de%20pantalla%20de%202018-04-24%2012-18-46.png)

Modificamos el fichero /etc/haproxy/haproxy.cfg añadiendo a la configuración de haproxy lo siguiente, para indicar que dos máquinas van a ser mis servidores
global
    daemon
    maxconn 256
    
defaults
    mode http
    contimeout 4000
    clitimeout 42000
    srvtimeout 43000
    
frontend http-in
    bind *:80
    default_backend servers
    
backend servers
    server    m1 172.16.168.130:80 maxconn 32
    server    m2 172.16.168.131:80 maxconn 32

Para lanzar haproxy una vez hemos cambiando su configuración ejecutamos el siguiente comando sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg y comprobamos que funciona
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica3/fotos/Captura%20de%20pantalla%20de%202018-04-24%2012-36-23.png)

## Someter a una alta carga la granja web ##
### Nginx ###

Para probar nuestra granja web con un balanceador nginx, vamos a lanzar 90000 peticiones de 10 en 10 con apache benchmark a nuestro balanceador, pidiendo la página hola.html

ab -n 90000 -c 10 http://192.168.1.105/hola.html

#### Htop ####
Me es imposible adjuntar captura de esta parte de la práctica, ya que en cuanto ejecutaba htop en dos máquinas virutales, mi pc se me bloqueaba y me era imposible continuar con la práctica

#### Resultado ####
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica3/fotos/Captura%20de%20pantalla%20de%202018-04-24%2013-58-25.png)

Ha tardado en atender 90000 peticiones unos 66.249 segundos, y ha habido peticiones fallidas cuyo motivo reside en la configuración(anfitrión, software de virtualización, máquinas, sistemas operativos virtualizados...) por lo tanto no podemos afirmar que el servidor no esté saturado.

Podemos ver como ha atendido unas 1358,51 peticiones por segundo, ha dedicado unos 7,261 ms por petición y ha tenido una velocidad media de transferencia de 450,18 kb/s.

### Haproxy ###

Para probar nuestra granja web con un balanceador nginx, vamos a lanzar 90000 peticiones de 10 en 10 con apache benchmark a nuestro balanceador, pidiendo la página hola.html

ab -n 90000 -c 10 http://192.168.1.120/hola.html

#### Htop ####
Me es imposible adjuntar captura de esta parte de la práctica, ya que en cuanto ejecutaba htop en dos máquinas virutales, mi pc se me bloqueaba y me era imposible continuar con la práctica

#### Resultado ####
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica3/fotos/Captura%20de%20pantalla%20de%202018-04-24%2014-05-27.png)

Ha tardado en atender 90000 peticiones unos 54,01 segundos, y ha habido peticiones fallidas cuyo motivo reside en la configuración(anfitrión, software de virtualización, máquinas, sistemas operativos virtualizados...) por lo tanto no podemos afirmar que el servidor no esté saturado.

Podemos ver como ha atendido unas 1665,08 peticiones por segundo, ha dedicado unos 6,006 ms por petición y ha tenido una velocidad media de transferencia de 553,67 kb/s.

## Comparación de balanceadores ##

Ninguno de los dos balanceadores no se ha saturado ya que ambos han dejado peticiones sin atender. Se puede observar que Nginx atiende más peticiones que Haproxy, pero éste segundo tiene mayor velocidad de transferencia y atiende más peticiones por segundo, dedicando menos tiempo que Nginx a atender a cada una individualmente.
**Haproxy** es mejor.


