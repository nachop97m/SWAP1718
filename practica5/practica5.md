
# Practica 5 SWAP

## Replicación de bases de datos MySQL

Creación de una Base de Datos, así como de una copia de seguridad en una segunda máquina, quedando ésta actualizada en todo momento. El proceso de actualización lo lleva a cabo un demonio en la máquina principal.

#####Crear BD

Se crea la BD contactos con MySql en la máquina Server1. 

![](https://github.com/nachop97m/SWAP1718/blob/master/practica5/Captura1.PNG)

----------------------------------------------------------

![](https://github.com/nachop97m/SWAP1718/blob/master/practica5/Captura2.PNG)


A continuación, se replica la base de datos con mysqldump y se copia a la máquina 2 con SCP mediante ssh. Una vez copiada, la creamos con MySql en dicha máquina y volcamos el archivo copiado a la base de datos.

![](https://github.com/nachop97m/SWAP1718/blob/master/practica5/Captura3.PNG)

----------------------------------------------------------

![](https://github.com/nachop97m/SWAP1718/blob/master/practica5/Captura4.PNG)

Se edita el archivo /etc/mysql/mysql.conf.d/mysqld.cnf en ambas máquinas, modificando la bind-address (para que escuche al servidor local), el archivo log de errores, así como el bin para la información de actualizaciones de la BD, y el server id, que deberá ser distinto en ambas máquinas.

![](https://github.com/nachop97m/SWAP1718/blob/master/practica5/Captura5.PNG)

----------------------------------------------------------

![](https://github.com/nachop97m/SWAP1718/blob/master/practica5/Captura6.PNG)

Se reinician ambos MySql, y se comprueban los datos de la base de datos maestra para su posterior "selección" desde la máquina 2. En la segunda máquina (backup), se añaden los datos de la BD maestra para que tome los datos de ésta (copia de seguridad).

![](https://github.com/nachop97m/SWAP1718/blob/master/practica5/Captura7.PNG)

----------------------------------------------------------

![](https://github.com/nachop97m/SWAP1718/blob/master/practica5/Captura8.PNG)

Se comprueba con el comando SHOW SLAVE STATUS\G que todo funciona correctamente, pero obtenemos un error (seconds behind master = null)

![](https://github.com/nachop97m/SWAP1718/blob/master/practica5/Captura9.PNG)

El problema: se configuraron por error las 2 máquinas con el mismo server id. Cambiamos el de la segunda máquina y listo.

![](https://github.com/nachop97m/SWAP1718/blob/master/practica5/Captura10.PNG)

----------------------------------------------------------

![](https://github.com/nachop97m/SWAP1718/blob/master/practica5/Captura11.PNG)

Ahora si, todo funciona correctamente, y los cambios en la BD maestra son actualizados al momento por el demonio.

![](https://github.com/nachop97m/SWAP1718/blob/master/practica5/Captura12.PNG)

----------------------------------------------------------

![](https://github.com/nachop97m/SWAP1718/blob/master/practica5/Captura13.PNG)