##Ejercicio T4.2##
Buscar información sobre precio y características de
balanceadores hardware específicos. Compara las
prestaciones que ofrecen unos y otros. 
KEMP LM-5400 que rondaría unos 19000 dólares y luego por otro lado Citrix MPX-8005 que rondaría los 24000 dólares.En cuánto a características tendríamos lo siguiente:
-Número de fuentes de alimentación: Citrix(1) y KEMP(2).
-Consumo(medido en W): Citrix(184.5) y KEMP(185). Sería muy similar
-Memoria RAM:Citrix(32GB) y KEMP(8GB)

##Ejercicio T4.3##
Buscar información sobre los métodos de balanceo que implementan los dispositivos recogidos en el ejercicio 4.2.
KEMP LM-5400 implementa los algoritmos de Round Robin, Round Robin con pesos, el menor número de conexiones, menor número de conexiones con pesos, reparto mediante un sistema agente que estudia la carga del servidor, source o ip-hash, switching según el contenido de la capa 6 y usar un servidor por defecto y usar otro cuando haya mucha demanda.
Citrix sobre todo emplea Round Robin o Least Connection.

##Ejercicio T4.7##
Buscar información sobre métodos y herramientas para
implementar GSLB. 
Deberíamos colocar dos servidores en zonas distintas, a ser posible en continentes distintos, ya que si no este método no tiene ningún sentido. Una vez hecho esto, crearíamos una VPN para conectar de manera segura ambos servidores previamente instalados. Posteriormente no tendría más que configurarlo para que sea capaz de detectar la posición geográfica del usuario que accede al servicio para balancear la carga hacia un lado u otro.

