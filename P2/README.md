# Práctica 2 - Configuración de concesión y renovación

Para realizar esta práctica, partimos del estado en el que se queda el servidor al terminar la práctica anterior.

## Configuración del servidor DHCP

En el fichero `/etc/dhcp/dhcpd.conf` volvemos a añadir las nuevas opcciones. En el rango (dentro de la subnet) que ya teníamos creado, añadimos nuevas configuraciones.

Todas las nuevas líneas se derivan directamente de lo pedido en el enunciado, con la consideración de que debemos pasar los tiempos a segundos.

## Aplicando la configuración

_Igual que en la P1_

Una vez más, reiniciamos el servicio:

> `sudo systemctl restar isc-dhcp-server`

Comprobamos que el servicio se haya levantada correctamente con:

> `sudo systemctl status isc-dhcp-server`

Si todo hubiera ido bien, nos mostrará un status correcto. En caso de fallo en alguno de los ficheros anteriores, deberemos consultar `/var/log/syslog` buscando información sobre los mismos.

## Comprobaciones

Podemos comprobar que la práctica se ha realizado correctamente aplicando lo mismo que se cuenta en la [P1](../P1/instrucciones.md).

Además, podemos utilizar el comando 

> `sudo dhcp-lease-list`

para ver el tiempo de concesión.