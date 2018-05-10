
# Practica 4 SWAP

## Asegurar la Granja Web

En esta tercera practica de SWAP, se ha llevado a cabo la creacion de un certificado SSL propio, la configuración de apache y nginx para aceptar peticiones HTTPS y la configuración del cortafuegos mediante iptables.

#####Crear certificado y añadirlo en el archivo de configuracion de apache

Tal y como se muestra, se pueden realizar peticiones a la maquina en cuestion tanto por HTTPs como por HTTP

![](https://github.com/nachop97m/SWAP1718/blob/master/practica4/Captura1.PNG)

![](https://github.com/nachop97m/SWAP1718/blob/master/practica4/Captura2.PNG)

![](https://github.com/nachop97m/SWAP1718/blob/master/practica4/Captura3.PNG)

![](https://github.com/nachop97m/SWAP1718/blob/master/practica4/Captura4.PNG)

Enviamos los certificados a las demas maquinas y configuramos apache y nginx (segunda foto)

![](https://github.com/nachop97m/SWAP1718/blob/master/practica4/Captura5.PNG)

![](https://github.com/nachop97m/SWAP1718/blob/master/practica4/Captura7.PNG)

Por ultimo, creamos un script con las instrucciones para que el cortafuegos se resetee al inicio y, posteriormente, bloquee todos los puertos excepto el 22 (conexion por ssh), 80 y 443 (HTTP y HTTPs)

![](https://github.com/nachop97m/SWAP1718/blob/master/practica4/Captura6.PNG)


A continuacion se muestra el funcionamiento final: La maquina 4 (abajo izquierda) realiza peticiones HTTPs al balanceador nginx (abajo derecha), que reparte la carga entre las maquinas 1 y 2 (arriba) de manera proporcional.

![](https://github.com/nachop97m/SWAP1718/blob/master/practica4/Captura8.PNG)