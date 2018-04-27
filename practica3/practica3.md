
# Practica 3 SWAP

## Instalacion y Puesta en Marcha de Software de Balanceo de Carga

En esta tercera practica de SWAP, se ha llevado a cabo la instlacion y puesta en marcha de dos sistemas de balanceo de carga de servidores en maquinas virtuales. Se ha utilizado tanto el software de NGINX como el de HAPROXY; a continuacion se explicara el proceso seguido.

#####Instalacion de NGINX desde linea de comandos
Se Instalara NGINX en una tercera maquina que atendara las peticiones de las 2 maquinas finales que componen la granja web. Dicho software balancera la carga a las maquinas finales segun la configuracion que establezcamos.

![](https://github.com/nachop97m/SWAP1718/blob/master/practica3/2.PNG)

![](https://github.com/nachop97m/SWAP1718/blob/master/practica3/3.PNG)

Configuracion de la interfaz de red con IP estatica (sera la IP que atendera las peticiones de nuestra granja web; desde aqui se enviaran las peticiones a las maquinas con IPs especificadas en el archivo de configuracion de NGINX, tal y como se acaba de mostrar

![](https://github.com/nachop97m/SWAP1718/blob/master/practica3/4.PNG)

Comentamos la siguiente linea para que nginx no utilice la configuracion de servidor final:

![](https://github.com/nachop97m/SWAP1718/blob/master/practica3/6.PNG)

A continuacion se muestra como una 4ª maquina realiza peticiones al balanceador, y obtiene las respuestas de manera alterna desde ambas maquinas servidoras finales (utilizando Round-Robin)

![](https://github.com/nachop97m/SWAP1718/blob/master/practica3/7.PNG)

Repetimos el proceso, pero en este caso, utilizando HAPROXY (/etc/haproxy/haproxy.cfg previa instalacion desde linea de comandos).

![](https://github.com/nachop97m/SWAP1718/blob/master/practica3/9.PNG)

En este caso, configuramos NGINX y HAPROXY para que el balanceo se haga por prioridad, dando una mayor prioridad a la primera de las 2 maquinas finales (suponemos que ésta es más potente). Simplemente volvemos a editar los archivos de configuracion, añadiendo a continuacion de las IPs finales: weight=x (nginx) y weight x (haproxy) siendo x el peso que asginamos a dicha maquina. Antes de utilizar uno de los 2 software de balanceo debemos asegurarnos de que el otro está detenido, de ésta forma no se "pisaran" puesto que ambos escuchan el mismo puerto (80).

![](https://github.com/nachop97m/SWAP1718/blob/master/practica3/10.PNG)

![](https://github.com/nachop97m/SWAP1718/blob/master/practica3/11.PNG)

Por ultimo, simulamos carga real con Apache Benkmark y vemos de forma grafica con htop como el balanceador está al 100% de capacidad, mientras que los servidores finales (arriba) tienen una carga proporcional a la establecida previamente.

![](https://github.com/nachop97m/SWAP1718/blob/master/practica3/12.PNG)

![](https://github.com/nachop97m/SWAP1718/blob/master/practica3/13.PNG)

![](https://github.com/nachop97m/SWAP1718/blob/master/practica3/14.PNG)

![](https://github.com/nachop97m/SWAP1718/blob/master/practica3/15.PNG)