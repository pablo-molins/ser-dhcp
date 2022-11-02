# P3 - Configuración de una IP fija vía DHCP

Una vez más, partimos del estado en el que hemos dejado la máquina virtual con el servidor.

## [Opcional pero recomendado] Clonar la máquina cliente

Para comprobar del todo que hemos logrado asignar por DHCP de forma fija y dinámica, combiene duplicar la máquina en VirtualBox para probar ambos métodos en simultáneo.

Si duplicamos la máquina, deberemos marcar la opción de generar nuevas direcciones MAC en nuestras tarjetas de red virtuales para evitar problemas. En la nueva máquina, deberemos apuntarnos cuál es su ip. 

## Conocer la MAC de la máquina cliente 

Para hacer la asignación estática necesitaremos la MAC del cliente. Para ello, en la nueva máquina de cliente, podemos ejecutar:

> `sudo ip addr`

Para el resto de la práctica, supondremos que  **00:11:22:33:44:55** es la MAC de nuestra máquina cliente fija.

## Configuración del servidor DHCP

Una vez más, modificamos el fichero `/etc/dhcp/dhcpd.conf`. Dejamos lo mismo que en su [versión de la P2](../P2/etc/dhcp/dhcpd.conf), pero ahora añadimos nuevas secciones:

- Las opciones generales (las `option`, `default-lease-time` y `max-lease-time`) las ponemos como configuración global.
- En la subred dejamos la línea que define el rango.
- Creamos una nueva sección de host en la que especificado que para nuestra MAC irá la IP solicitada.

## Reiniciamos el servicio

Hacemos igual que en [P1](../P1/README.md) o en [P2](../P2/README.md).

## Comprobando el servicio en los clientes

En la máquina de cliente de rango fijo deberíamos tener todo funcionando igual que antes.

En la nueva máquina, debemos comprobar que al hacer el `ip addr` nos muestra 192.168.1.200 como la IP.

## Comprobando en el servidor

Si hemos ejecutado la máquina cliente nueva y luego hemos actualizado la configuración, deberemos ver en el servidor ese cambio en la tabla ARP. Para consultarla, podemos hacer:

> `sudo arp -a`

Y ver cómo las IP están asociadas a las MAC correspondientes.