#Práctica 1
~~~
Primero conectamos ambas máquinas internamente mediante la red **solo-anfitrión** llamada vboxnet0.
Primero lo haríamos con la **máquina 1(SWAP 1)** y luego con la **máquina 2 (SWAP 2)**.

![Captura de pantalla](~/SWAP-UGR/Practica1/fotos/a.png)
![Captura de pantalla](~/SWAP-UGR/Practica1/fotos/b.png)
~~~

~~~
Una vez realizado lo anterior al ejecutar el comando **ifconfig**,veremos claramente como ya ambas máquinas detectan **vboxnet0** creada.
![Captura de pantalla](~/SWAP-UGR/Practica1/fotos/c.png)
![Captura de pantalla](~/SWAP-UGR/Practica1/fotos/d.png)

Trabajaremos,entonces, con las ips siguientes(*asignadas anteriormente*):
**Para SWAP1: 192.168.1.50**
**Para SWAP1: 192.168.1.100**
~~~

~~~
Ya solamente queda demostrar que podemos acceder por **ssh** de una máquina a otra:
![Captura de pantalla](~/SWAP-UGR/Practica1/fotos/e.png)
Aquí mostramos que podemos acceder con **ssh** desde SWAP1 (*192.168.1.50*) a SWAP2 (*192.168.1.100*) (A la inversa también se puede, solo que nada más lo mostramos el funcionamiento en una dirección)
~~~

~~~
Por último demostramos que es posible acceder mediante la herramienta curl desde una máquina a la otra
![Captura de pantalla](~/SWAP-UGR/Practica1/fotos/f.png)
~~~

~~~
Probamos a ejecutar hola.html en **SWAP1** desde **SWAP2** y la captura muestra el correcto funcionamiento.
A la inversa también es posible.
~~~
