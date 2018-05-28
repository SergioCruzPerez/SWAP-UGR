## Ejercicio5.1 ##
Buscar información sobre cómo calcular el número de conexiones por segundo.
En Linux bastaría con ejecutar el siguiente comando: netstat | grep http | wc -l, el cual nos responde con un entero que representa cada cliente que posee sockets para atender diferentes peticiones.
Si queremos realizarlo con la herramienta Nginx bastaría con abrir el fichero nginx.conf, editar unas líneas,guardar la configuración,reiniciar el servicio y en el navegador insertar la siguiente URL http://ip.address.here/nginx_status, la cual nos mostrará una información con la que podemos obtener lo deseado en este ejercicio realizando una serie de cuentas muy sencillas.
También hay otras aplicaciones de gran utilidad como pueden ser ipstate o apache2ctl,además de la mencionada anteriormente netstat.s

## Ejercicio 5.3 ##
Buscar información sobre características, disponibilidad para diversos SO, etc de herramientas para monitorizar las
prestaciones de un servidor.
-Pandora FMS: Versión libre capaz de monitorizar más de 10,000 nodos y cubre (sin limitaciones) una monitorización de red, de servidores (basados en agentes o de forma remota) y de aplicaciones. Con funcionalidades completas de informes, alertas, integraciones con terceros via API.
Destacamos también su integración con dispositivos móviles, no sólo para acceder a la consola sino también para monitorizarlos gracias a su sistema de geolocalización.
-Zabbix: Fácil configuración y potente interfaz gráfico. Empieza a caer su rendimiento cuando se empiezan a monitorizar muchos nodos. Destaca el servicio de monitorización sin necesidad de instalar agentes. La experiencia nos dice que se pueden monitorizar hasta 10,000 nodos sin problemas de rendimiento.
-GroudWork: Es complicada la integración de sus diferentes módulos. Además, no posee muchos plugins desarrollados. Para grandes entornos se queda pequeño. No muestra un histórico extenso cuando monitorizamos muchos nodos y no soporta plataformas como HP-UX, FreeBSD.
-Zenoss: Monitorizar almacenamiento, redes, servidores, aplicaciones y servidores virtuales. Destaca su monitorización sin necesidad de utilizar agentes. Tiene una versión “Community” con funcionalidades muy reducidas y una versión comercial con todas las funcionalidades. Capaz de monitorizar multiples plataformas.
