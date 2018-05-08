# Practica 4 #

1. Objetivos de la práctica

El objetivo de esta práctica es llevar a cabo la configuración de seguridad de la granja
web. Para ello, llevaremos a cabo las siguientes tareas:
• Instalar un certificado SSL para configurar el acceso HTTPS a los servidores.

• Configurar las reglas del cortafuegos para proteger la granja web.

## Instalar un certificado SSL autofirmado para configurar el acceso por HTTPS ##

Lo he realizado desde la máquina 2, con **ip** 192.168.1.100 y he realizado lo siguiente:

-Se activan una serie de módulos: a2enmod ssl

-Reiniciamos el servicio de apache2 : service apache2 restart

-Creamos la carpeta donde guardaremos nuestro certificado SSL: mkdir /etc/apache2/ssl

-Generamos el certificado SSL : **openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt** 

Y rellenamos los campos que se nos pide tal y como se adjunta en el guión de la práctica 4.

![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica4/fotos/imagen1)

A continuación tenemos que editar el archivo de configuración de nuestro servidor para añadir nuestro certificado creado para que pueda ser creado.

**sudo nano /etc/apache2/sites-available/default-ssl.conf**

Y añadimos las siguientes líneas:
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica4/fotos/imagen2)

Una vez modificadas estas líneas, hacemos el procedimiento anterior, activamos el sitio y reiniciamos apache.

![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica4/fotos/imagen3)

Y para comprobar que funciona todo según lo previsto, hacemos peticiones mediante la herramienta curl, y comprobamos también que si no se especifica la opción -k no funciona.

![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica4/fotos/imagen4)

## Configuración del cortafuegos ##
En primer lugar para ver el estado del cortafuegos ejecutamos: **iptables -L -n -v**
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica4/fotos/imagen5)
Podemos ver como se acepta todo tipo de tráfico,tanto de entrada como de salida, debido a que todavía no hemos aplicado ninguna regla.

### IPTABLES ###
Iptables es una herramienta de cortafuegos, de espacio de usuario, con la que el superusuario define reglas de filtrado de paquetes, de traducción de direcciones de red, y mantiene registros de log.
Se basa en establecer una lista de reglas con las que definir qué acciones hacer con cada paquete en función de la información que incluye.

Ilustramos el funcionamiento de algunas de estas reglas mencionadas anteriormente:

Para bloquear el tráfico de entrada, podemos hacer:
**iptables -P INPUT DROP**
**iptables -P FORWARD DROP**
**iptables -P OUTPUT ACCEPT**
**iptables -A INPUT -m state --state NEW,ESTABLISHED -j ACCEPT**
**iptables –L –n -v**
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica4/fotos/imagen6)

Si queremos bloquear trafico ICMP para evitar ataques mediante ping:
**iptables -A INPUT -p icmp --icmp-type echo-request -j DROP**
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica4/fotos/imagen7)

Si queremos permitir el acceso por SSH, abriendo el puerto 22:
**iptables -A INPUT -p tcp --dport 22 -j ACCEPT**
**iptables -A OUTPUT -p udp --sport22 -j ACCEPT**
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica4/fotos/imagen8)

Si queremos permitir el acceso a DNS, abriendo el puerto 53:
**iptables -A INPUT -m state --state NEW -p udp --dport 53 -j ACCEPT**
**iptables -A INPUT -m state --state NEW -p tcp --dport 53 -j ACCEPT**
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica4/fotos/imagen9)

Si queremos bloquear todo el tráfico de entrada o salida desde una IP:
**iptables -I INPUT -s 192.168.1.50 -j DROP**
**iptables -I OUTPUT -s 192.168.1.50 -j DROP**
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica4/fotos/imagen10)

Ahora procedemos a comprobar el funcionamiento del cortafuegos ejecutando la siguiente orden:
**netstat -tulpn**
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica4/fotos/imagen11)

## SCRIPT ##
Script que realizaría lo pedido en la práctica, más otras funcionalidades.
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica4/fotos/imagen12)

Para que se ejecute con el arranque de la máquina, nada más bastaría añadir lo siguiente en el crontab
![img](https://github.com/SergioCruzPerez/SWAP-UGR/blob/master/Practica4/fotos/imagen13)





