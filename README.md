
- [Distancias Administrativa Routing](#distancia-administrativa-routing)

- [Routing Linux](#routing-linux)

- [Autonomous Systems BGP](#autonomous-systems-bgp)

- [Simulador de red GNS3](./routing-instalacion-gns3.md)  

  - [Instalación de GNS3 en Ubuntu 20.04 LTS](./routing-instalacion-gns3.md)       
 
  - [Ejercicio Core MPLS sobre GNS3](./routing-ejercicio-mpls-sobre-gns3.md)        

***

# Distancia Administrativa Routing

| Protocolo	                  | Distancia administrativa |
|-----------------------------|--------------------------|
| Directamente conectados	    | 0 |
| Ruta estática	              | 1 |
| Ruta EIGRP sumarizada	      | 5 |
| BGP externa	                | 20 |
| EIGRP interna	              | 90 |
| IGRP	                      | 100 |
| OSPF	                      | 110 |
| IS-IS	                      | 115 |
| RIP	                        | 120 |
| EGP	                        | 140 |
| ODR	                        | 160 |
| EIGRP externa	              | 170 |
| BGP interna	                | 200 |
| Desconocida	                | 255 |

# Autonomous Systems BGP

Hasta el 2007, los números AS estaban definidos como un entero de 16-bits, lo que permite un número máximo de 65.536.

IANA controla los números AS. Y estos son asignados de la siguiente forma:

| Number | Description |
|--------|-------------|
| 0 | reserved. |
| 1-64.495 | public AS numbers. |
| 64.496 – 64.511 | reserved to use in documentation. |
| 64.512 – 65.534 | private AS numbers. |
| 65.535 | reserved. |

Desde el 2007 los ASN son de 32-bits.

| Number | Bits | Description	|
|--------|------|-------------|
| 0 | 16 | Reserved for RPKI unallocated space invalidation[11] |
| 1 - 23455	| 16 | Public ASNs. |
| 23456 | 16 | Reserved for AS Pool Transition. |
| 23457 - 64495 | 16 |  Public ASNs. |
| 64496 - 64511	| 16 | Reserved for use in documentation/sample code. |
| 64512 - 65534	| 16 | Reserved for private use. |
| 65535 | 16 | Reserved. |
| 65536 - 65551 | 32 | Reserved for use in documentation and sample code. |
| 65552 - 131071 | 32 | Reserved. |
| 131072 - 4199999999 | 32 | Public 32-bit ASNs. |
| 4200000000 - 4294967294 | 32 |   Reserved for private use. |
| 4294967295 | 32 |    Reserved. |



# Routing linux

Para activar el routing con multi-homing. Hay que activar el forwarding:

    # echo 1 > /proc/sys/net/ipv4/ip_forwarding

Para que en caso de reinicio del linux quede activado, modificaremos el fichero /etc/sysctl.conf añadiendo la siguiente línea.

    # vi /etc/sysctl.conf
    net.ipv4.ip_forward = 1

Y con el siguiente cambio aplicaremos el cambio:

    # sysctl -p


***

# URLs referencia:
- https://www.cyberciti.biz/tips/linux-how-to-setup-multi-homing-networking.html
- https://en.wikipedia.org/wiki/Autonomous_system_(Internet)
- https://www.geeksforgeeks.org/difference-between-ebgp-and-ibgp/
- https://www.bgp.us/ibgp-and-ebgp/


