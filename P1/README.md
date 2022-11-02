# Práctica 1 - Configuación inicial del DHCP

## Configuración red del servidor

Modificamos el fichero `/etc/netplan/00-installer-config.yaml` para establecer una IP fija.

Reiniciamos la red:

> `sudo netplan apply`

Y comprobamos que se hayan aplicado los cambios correctamente con:

> `ip addr`

## Configuración del servidor DHCP

Empezamos instalando el servidor DHCP:

> `sudo apt update && sudo apt install -y isc-dhcp-server`

Debemos modificar dos ficheros:

1. `/etc/defaults/isc-dhcp-server `: Indicamos por qué interfaces escucharemos peticiones.
2. `/etc/dhcp/dhcpd.conf`: Fichero que incluye la configuración dle propio servicio.

Modificados los ficheros, reiniciamos el servicio:

> `sudo systemctl restar isc-dhcp-server`

Comprobamos que el servicio se haya levantada correctamente con:

> `sudo systemctl status isc-dhcp-server`

Si todo hubiera ido bien, nos mostrará un status correcto. En caso de fallo en alguno de los ficheros anteriores, deberemos consultar `/var/log/syslog` buscando información sobre los mismos.

## Comprobaciones

Para comprobar que ha sido correctamente realizado, debemos levantar una máquina virtual que haga de cliente.

En dicha máquina cliente, también deberemos modificar el fichero `/etc/netplan/00-installer-config.yaml`, especificando que vamos a recibir la IP por DHCP.

Se reinicia la máquina (o se reinicia aplican las modificaciones con `netplan apply`) y se comprueba si se ha obtenido una IP dentro del rango.

Es importante comprobar que la máquina cliente y la máquina servidor tienen configuradas interfaces de red que permitan la comunicación entre ellas (como "red interna").

Por último, también es posible comprobar los mensajes enviados por el servidor leyendo el contenido de `/var/log/syslog`, pues en dicho fichero quedan registrados.