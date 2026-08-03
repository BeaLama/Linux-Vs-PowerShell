# 09 - Red avanzada — Linux vs PowerShell

Las redes son uno de los pilares fundamentales de cualquier infraestructura informática.

## Índice

- [Arquitectura y modelos de red](#arquitectura-y-modelos-de-red)
- [Protocolos de red avanzados](#protocolos-de-red-avanzados)
- [Switching y VLAN](#switching-y-vlan)
- [Routing y enrutamiento avanzado](#routing-y-enrutamiento-avanzado)
- [Alta disponibilidad y redundancia](#alta-disponibilidad-y-redundancia)
- [Seguridad en redes](#seguridad-en-redes)
- [Monitorización y diagnóstico](#monitorizacion-y-diagnostico)

---

## Arquitectura y modelos de red

*Las redes modernas están formadas por numerosos dispositivos que trabajan conjuntamente para permitir la comunicación entre equipos, servidores, aplicaciones y usuarios.*

### Modelo OSI

*El modelo OSI (Open Systems Interconnection) divide la comunicación en siete capas.*

| Capa | Función |
|------|----------|
| 7 | Aplicación |
| 6 | Presentación |
| 5 | Sesión |
| 4 | Transporte |
| 3 | Red |
| 2 | Enlace de datos |
| 1 | Física |

### Modelo TCP/IP

*Es el modelo utilizado realmente en Internet.*

| TCP/IP | Equivalencia OSI |
|---------|------------------|
| Aplicación | 5-7 |
| Transporte | 4 |
| Internet | 3 |
| Acceso a red | 1-2 |

### Comparativa

| Modelo | Uso |
|---------|-----|
| OSI | Modelo teórico y educativo |
| TCP/IP | Modelo real utilizado en Internet |

---

## Protocolos de red avanzados

*Los protocolos de red son el conjunto de normas que permiten que los dispositivos intercambien información de forma correcta.*

### Comparativa

| Protocolo | Función |
|-----------|----------|
| ICMP | Diagnóstico |
| ARP | Resolución IP → MAC |
| NDP | Resolución IPv6 |
| RIP | Enrutamiento básico |
| OSPF | Enrutamiento empresarial |
| BGP | Enrutamiento en Internet |
| HSRP | Alta disponibilidad |
| VRRP | Alta disponibilidad estándar |
| LACP | Agregación de enlaces |
| SNMP | Monitorización |
| NTP | Sincronización horaria |
| LDAP | Directorio |
| Kerberos | Autenticación |
| SSH | Administración remota segura |
| Syslog | Centralización de eventos |

---

## Switching y VLAN

*Los switches constituyen el núcleo de la mayoría de redes locales modernas.*

### Tabla CAM

*La CAM (Content Addressable Memory) almacena la relación entre direcciones MAC y puertos físicos.*

| Dirección MAC | Puerto |
|---------------|--------|
| AA:BB:CC:11:22:33 | Fa0/1 |
| DD:EE:FF:44:55:66 | Fa0/2 |

### Identificador de VLAN

*Cada VLAN posee un identificador numérico.*

| VLAN | Uso |
|------|-----|
| 1 | VLAN por defecto |
| 10 | Administración |
| 20 | Ventas |
| 30 | Recursos Humanos |
| 40 | Invitados |

### Comparativa

| Elemento | Función |
|-----------|----------|
| Switch | Conmutación de tramas |
| VLAN | Segmentación lógica |
| Access | Una única VLAN |
| Trunk | Varias VLAN |
| STP | Evita bucles |
| RSTP | STP rápido |
| LACP | Agregación de enlaces |
| Layer 3 Switch | Routing entre VLAN |

---

## Routing y enrutamiento avanzado

*El routing es el proceso mediante el cual los datos son enviados desde una red de origen hasta una red de destino utilizando uno o varios dispositivos intermedios denominados routers.*

### Tabla de enrutamiento

*Cada router mantiene una tabla de rutas donde almacena información sobre las redes conocidas.*

| Red destino | Next Hop | Interfaz |
|--------------|----------|----------|
| 192.168.1.0/24 | Directa | Gig0/0 |
| 10.0.0.0/24 | 192.168.1.1 | Gig0/1 |
| 0.0.0.0/0 | ISP | Gig0/2 |

- Red de destino.
- Máscara.
- Siguiente salto (Next Hop).
- Interfaz de salida.
- Métrica.

### Protocolos de enrutamiento

*Los protocolos más utilizados son.*

| Protocolo | Tipo |
|------------|------|
| RIP | IGP |
| OSPF | IGP |
| EIGRP | IGP |
| IS-IS | IGP |
| BGP | EGP |

### Resolución de incidencias

*Durante el diagnóstico del routing suelen utilizarse herramientas como.*

```bash
ping
```
```powershell
tracert
```

### Comparativa

| Tipo | Característica |
|------|----------------|
| Ruta conectada | Automática |
| Ruta estática | Configuración manual |
| RIP | Sencillo |
| OSPF | Escalable |
| EIGRP | Muy rápido |
| BGP | Internet |
| NAT | Traducción de IP |
| PAT | Varias IP privadas → una IP pública |

---

## Alta disponibilidad y redundancia

*En una infraestructura empresarial es fundamental garantizar que los servicios continúen funcionando incluso cuando se produce un fallo de hardware, software o comunicaciones.*

### Disponibilidad

*La disponibilidad suele expresarse como porcentaje.*

| Disponibilidad | Tiempo máximo de caída al año |
|----------------|-------------------------------|
| 99 % | ~3,6 días |
| 99,9 % | ~8,8 horas |
| 99,99 % | ~53 minutos |
| 99,999 % | ~5 minutos |

### Comparativa

| Tecnología | Función |
|------------|----------|
| HSRP / VRRP | Redundancia de routers |
| STP / RSTP | Prevención de bucles |
| LACP | Agregación de enlaces |
| Clúster | Alta disponibilidad de servidores |
| Balanceador | Reparto de carga |
| RAID | Redundancia del almacenamiento |
| Replicación | Copia sincronizada de datos |
| UPS | Protección eléctrica |

---

## Seguridad en redes

### Comparativa

| Tecnología | Función |
|------------|----------|
| Firewall | Filtrado de tráfico |
| ACL | Control de acceso |
| VLAN | Segmentación |
| DMZ | Aislamiento de servicios públicos |
| IDS | Detección de intrusiones |
| IPS | Prevención de intrusiones |
| VPN | Acceso remoto seguro |
| Port Security | Control de dispositivos |
| 802.1X | Autenticación de acceso |
| RADIUS | Autenticación centralizada |

---

## Monitorización y diagnóstico

*La monitorización de una red consiste en supervisar de forma continua el estado de los dispositivos, el tráfico y los servicios para detectar incidencias antes de que afecten a los usuarios.*

### Ping

*Comprueba si un equipo responde mediante ICMP.*

```bash
ping 192.168.1.1
```
```powershell
ping 192.168.1.1
```

- Conectividad.
- Latencia.
- Pérdida de paquetes.

### Traceroute

*Muestra todos los routers por los que pasa un paquete hasta llegar a su destino.*

```bash
traceroute 8.8.8.8
```
```powershell
tracert 8.8.8.8
```

### Nslookup y Dig

*Permiten comprobar la resolución DNS.*

```bash
dig ejemplo.com
```
```powershell
nslookup ejemplo.com
```

- Resolución de nombres.
- Servidores DNS.
- Registros DNS.

### Netstat

*Permite consultar las conexiones de red activas.*

```bash
netstat
```
```powershell
netstat -ano
```

- Conexiones abiertas.
- Puertos.
- Procesos asociados.

### Tcpdump

*tcpdump captura paquetes directamente desde la interfaz de red.*

```bash
tcpdump -i eth0
```

### Comparativa

| Herramienta | Función |
|-------------|----------|
| ping | Comprobar conectividad |
| traceroute / tracert | Mostrar el recorrido de los paquetes |
| nslookup / dig | Consultar DNS |
| netstat | Ver conexiones activas |
| tcpdump | Capturar tráfico |
| Wireshark | Analizar paquetes |
| SNMP | Monitorización |
| NetFlow | Análisis de tráfico |
| Syslog | Centralización de eventos |

---

[⬆️ Volver al índice](#índice)