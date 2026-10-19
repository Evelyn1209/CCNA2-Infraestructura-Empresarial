# Infraestructura empresarial: enrutamiento estático, EIGRP y seguridad de red

Proyecto final del curso CCNA 2 (Switching, Routing, and Wireless Essentials), Universidad Castro Carazo. Desarrollado en Cisco Packet Tracer.

![Topología](topologia.png)

## Descripción

Red de una empresa con tres sedes: un sitio principal (MDF) y dos sucursales remotas (IDF-1 e IDF-2). El sitio principal usa enrutamiento estático, las sucursales usan EIGRP, y un router central integra ambos segmentos mediante redistribución.

## Qué incluye

- Segmentación con VLAN (Administración, Ventas, TI, Nativa y Servidor)
- Direccionamiento IPv4 con VLSM
- Enrutamiento entre VLAN con SVI (switches de Capa 3) y router-on-a-stick (sucursales)
- Enrutamiento estático y ruta por defecto en el MDF
- EIGRP (AS 100) en el segmento remoto y redistribución de rutas estáticas
- DHCP centralizado con DHCP Relay (`ip helper-address`)
- Seguridad de acceso: Port Security (sticky, modo restrict), DHCP Snooping, PortFast y BPDU Guard
- Acceso remoto seguro por SSH, con Telnet deshabilitado

## Direccionamiento

| Sitio | VLAN | Red |
|-------|------|-----|
| MDF | 10 – Administración | 172.16.10.0 /27 |
| MDF | 20 – Ventas | 172.16.20.0 /27 |
| MDF | 30 – TI | 172.16.30.0 /27 |
| MDF | 99 – Nativa | 172.16.99.0 /28 |
| IDF-1 | 10 / 20 / 30 | 172.16.40.0 /28, 172.16.50.0 /28, 172.16.60.0 /28 |
| IDF-1 | 99 – Nativa | 172.16.199.0 /28 |
| IDF-2 | 10 / 20 / 30 | 172.16.70.0 /28, 172.16.80.0 /28, 172.16.90.0 /28 |
| IDF-2 | 99 – Nativa | 172.16.190.0 /28 |
| IDF-2 | 100 – Servidor | 172.16.100.0 /28 |

## Problemas encontrados y cómo se resolvieron

- Falta de comunicación entre los switches de Capa 3 del MDF: se añadió una SVI de gestión y rutas estáticas cruzadas.
- Enlaces seriales sin sincronización: faltaba `clock rate` en el extremo DCE.
- Servidor en la VLAN nativa: se movió a una VLAN dedicada (100) para evitar riesgos de VLAN hopping.
- DHCP Snooping bloqueaba el relay en una cadena de dos switches: se marcó como `trust` también el puerto de bajada.

## Archivos

- `packet-tracer/`: archivo `.pkt` de la simulación
- `configuraciones/`: configuración de cada dispositivo (`show running-config`)

## Herramientas

Cisco Packet Tracer · Cisco IOS

## Autora

Evelyn Castro Vega
