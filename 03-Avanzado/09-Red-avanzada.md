# 09 - Red avanzada

## Introducción

Las redes son uno de los pilares fundamentales de cualquier infraestructura informática. En niveles anteriores se han visto conceptos básicos como direccionamiento IP, configuración de interfaces o resolución DNS.

---

## Índice

- [Arquitectura y modelos de red](#arquitectura-y-modelos-de-red)
- [Protocolos de red avanzados](#protocolos-de-red-avanzados)
- [Switching y VLAN](#switching-y-vlan)
- [Routing y enrutamiento avanzado](#routing-y-enrutamiento-avanzado)
- [Alta disponibilidad y redundancia](#alta-disponibilidad-y-redundancia)
- [Seguridad en redes](#seguridad-en-redes)
- [Monitorización y diagnóstico](#monitorización-y-diagnóstico)

---

## Arquitectura y modelos de red

Las redes modernas están formadas por numerosos dispositivos que trabajan conjuntamente para permitir la comunicación entre equipos, servidores, aplicaciones y usuarios.

Comprender la arquitectura de una red facilita su diseño, administración y resolución de incidencias, ya que permite identificar cómo viajan los datos y qué función desempeña cada componente.

En entornos empresariales, una correcta arquitectura de red es fundamental para garantizar el rendimiento, la disponibilidad y la seguridad de los servicios.

---

### ¿Qué es una arquitectura de red?

La arquitectura de red define la organización de todos los elementos que intervienen en la comunicación entre dispositivos.

Incluye:

- Equipos cliente.
- Servidores.
- Switches.
- Routers.
- Firewalls.
- Puntos de acceso.
- Protocolos de comunicación.
- Medios de transmisión.

Su diseño determina cómo circula la información dentro de la infraestructura.

---

### Componentes principales

Una red empresarial suele estar formada por:

```text
Cliente

↓

Switch

↓

Router

↓

Firewall

↓

Internet
```

Además pueden existir:

- Servidores.
- NAS.
- SAN.
- Balanceadores de carga.
- VPN.
- Sistemas de monitorización.

Cada dispositivo cumple una función específica dentro de la infraestructura.

---

### Topologías de red

La topología describe cómo están conectados físicamente o lógicamente los dispositivos.

Las más habituales son:

#### Topología en estrella

```text
      Switch
     /  |  \
   PC1 PC2 PC3
```

**Ventajas:**

- Fácil administración.
- Fácil ampliación.
- Aislamiento de fallos.

Es la más utilizada actualmente.

---

#### Topología en bus

```text
PC ─── PC ─── PC ─── PC
```

Todos los equipos comparten el mismo medio de transmisión.

Actualmente apenas se utiliza.

---

#### Topología en anillo

```text
PC ─ PC
|      |
PC ─ PC
```

Cada equipo se conecta con el siguiente formando un circuito cerrado.

Fue habitual en tecnologías como Token Ring.

---

#### Topología en malla

```text
Todos los equipos
conectados entre sí
```

Ofrece:

- Máxima redundancia.
- Alta disponibilidad.

Su coste es elevado.

---

### Tipos de red según el alcance

Las redes también pueden clasificarse según su tamaño.

#### LAN (Local Area Network)

Red local.

Ejemplos:

- Oficina.
- Empresa.
- Vivienda.

---

#### MAN (Metropolitan Area Network)

Conecta distintas sedes dentro de una ciudad.

---

#### WAN (Wide Area Network)

Interconecta redes situadas en diferentes ubicaciones geográficas.

Internet es el mayor ejemplo de WAN.

---

### Modelos de comunicación

Existen dos modelos principales para describir el funcionamiento de una red.

- Modelo OSI.
- Modelo TCP/IP.

Ambos representan el proceso de comunicación por capas.

---

### Modelo OSI

El modelo **OSI (Open Systems Interconnection)** divide la comunicación en siete capas.

| Capa | Función |
|------|----------|
| 7 | Aplicación |
| 6 | Presentación |
| 5 | Sesión |
| 4 | Transporte |
| 3 | Red |
| 2 | Enlace de datos |
| 1 | Física |

Cada capa ofrece servicios a la superior y utiliza los de la inferior.

---

### Función de cada capa OSI

#### Capa 1 – Física

Gestiona:

- Cableado.
- Fibra óptica.
- Señales eléctricas.
- Conectores.

Ejemplos:

- RJ45.
- Cable UTP.
- Fibra óptica.

---

#### Capa 2 – Enlace de datos

Gestiona:

- Direcciones MAC.
- Switches.
- VLAN.
- Tramas Ethernet.

---

#### Capa 3 – Red

Gestiona:

- Direcciones IP.
- Routing.
- Routers.

Protocolos:

- IPv4.
- IPv6.
- ICMP.

---

#### Capa 4 – Transporte

Garantiza la comunicación entre aplicaciones.

Protocolos:

- TCP.
- UDP.

---

#### Capas 5, 6 y 7

Se encargan de:

- Sesiones.
- Formato de los datos.
- Aplicaciones.

Ejemplos:

- HTTP.
- HTTPS.
- FTP.
- DNS.
- SMTP.

---

### Modelo TCP/IP

Es el modelo utilizado realmente en Internet.

Consta de cuatro capas.

| TCP/IP | Equivalencia OSI |
|---------|------------------|
| Aplicación | 5-7 |
| Transporte | 4 |
| Internet | 3 |
| Acceso a red | 1-2 |

Es más sencillo y práctico que el modelo OSI.

---

### Encapsulación

Cuando una aplicación envía información, los datos atraviesan todas las capas.

Proceso:

```text
Aplicación

↓

TCP

↓

IP

↓

Ethernet

↓

Cable o Wi-Fi
```

Cada capa añade su propia información antes de transmitir los datos.

---

### Desencapsulación

En el equipo receptor ocurre el proceso inverso.

```text
Cable

↓

Ethernet

↓

IP

↓

TCP

↓

Aplicación
```

Cada capa elimina la información añadida por su equivalente en el equipo emisor.

---

### Direccionamiento en la comunicación

Durante la transmisión intervienen distintos identificadores.

- Dirección MAC.
- Dirección IP.
- Puerto TCP o UDP.
- Nombre DNS.

Cada uno opera en una capa distinta del modelo de comunicación.

---

### Flujo de una comunicación

Cuando un usuario accede a una página web:

```text
Navegador

↓

DNS

↓

Dirección IP

↓

Router

↓

Internet

↓

Servidor web

↓

Respuesta
```

Todo este proceso suele completarse en pocos milisegundos.

---

### Arquitectura de una red empresarial

Una infraestructura moderna suele organizarse en distintos niveles.

```text
Internet

↓

Firewall

↓

Router

↓

Switch principal

↓

Switches de acceso

↓

Equipos
```

Además pueden existir:

- Servidores.
- NAS.
- Wi-Fi.
- Sistemas de monitorización.
- VPN.

Esta organización facilita el crecimiento y la administración de la red.

---

### Comparativa

| Modelo | Uso |
|---------|-----|
| OSI | Modelo teórico y educativo |
| TCP/IP | Modelo real utilizado en Internet |

---

[⬆️ Volver al índice](#índice)

## Protocolos de red avanzados

Los protocolos de red son el conjunto de normas que permiten que los dispositivos intercambien información de forma correcta.

En niveles anteriores se han estudiado protocolos básicos como **TCP**, **UDP**, **HTTP**, **DNS** o **DHCP**. En este apartado se profundiza en otros protocolos ampliamente utilizados en redes empresariales para tareas de enrutamiento, administración, seguridad, sincronización y monitorización.

Comprender estos protocolos permite diseñar infraestructuras más eficientes y resolver incidencias con mayor rapidez.

---

### ¿Qué es un protocolo de red?

Un protocolo define cómo debe producirse una comunicación entre dos o más dispositivos.

Especifica aspectos como:

- Formato de los datos.
- Orden de transmisión.
- Control de errores.
- Autenticación.
- Confirmación de recepción.

Todos los equipos de una red deben utilizar los mismos protocolos para poder comunicarse correctamente.

---

### Clasificación de protocolos

Los protocolos pueden agruparse según su función.

Los más habituales son:

- Protocolos de transporte.
- Protocolos de direccionamiento.
- Protocolos de enrutamiento.
- Protocolos de administración.
- Protocolos de sincronización.
- Protocolos de seguridad.
- Protocolos de monitorización.

Cada uno trabaja en distintas capas del modelo TCP/IP.

---

### ICMP (Internet Control Message Protocol)

ICMP se utiliza para intercambiar mensajes de control y diagnóstico.

No transporta información de usuario.

Permite:

- Comprobar conectividad.
- Informar de errores.
- Medir tiempos de respuesta.

Herramientas que utilizan ICMP:

- `ping`
- `traceroute` (parcialmente)

Es uno de los protocolos más utilizados durante la resolución de incidencias.

---

### ARP (Address Resolution Protocol)

ARP permite conocer la dirección MAC correspondiente a una dirección IP dentro de una red local.

Proceso:

```text
Dirección IP

↓

Consulta ARP

↓

Dirección MAC
```

Sin ARP, un equipo no podría comunicarse mediante Ethernet.

---

### NDP (Neighbor Discovery Protocol)

En redes IPv6, ARP es sustituido por **NDP**.

Además de resolver direcciones, permite:

- Descubrimiento de vecinos.
- Autoconfiguración.
- Detección de routers.
- Comprobación de accesibilidad.

Es un protocolo fundamental en redes IPv6.

---

### RIP (Routing Information Protocol)

RIP es uno de los protocolos de enrutamiento dinámico más antiguos.

Características:

- Fácil configuración.
- Utiliza número de saltos como métrica.
- Máximo de 15 saltos.
- Actualizaciones periódicas.

Actualmente su uso es reducido debido a sus limitaciones.

---

### OSPF (Open Shortest Path First)

OSPF es uno de los protocolos de enrutamiento dinámico más utilizados en redes empresariales.

Características:

- Alta velocidad de convergencia.
- Escalable.
- Basado en el algoritmo SPF.
- Organización mediante áreas.
- Muy utilizado en grandes infraestructuras.

Es el protocolo interno (IGP) más habitual en empresas.

---

### BGP (Border Gateway Protocol)

BGP es el protocolo responsable del intercambio de rutas entre sistemas autónomos.

Se utiliza principalmente:

- Entre proveedores de Internet.
- Grandes operadores.
- Organizaciones con múltiples conexiones WAN.

Internet funciona gracias a BGP.

Su configuración es considerablemente más compleja que la de otros protocolos de enrutamiento.

---

### HSRP

**HSRP (Hot Standby Router Protocol)** proporciona alta disponibilidad para routers.

Funcionamiento:

```text
Router activo

↓

Fallo

↓

Router de respaldo
```

Los usuarios continúan utilizando la misma puerta de enlace sin percibir el cambio.

Es una tecnología desarrollada por Cisco.

---

### VRRP

**VRRP (Virtual Router Redundancy Protocol)** ofrece una funcionalidad similar a HSRP.

Características:

- Estándar abierto.
- Compatible con múltiples fabricantes.
- Alta disponibilidad de gateways.

Actualmente es muy utilizado en entornos heterogéneos.

---

### LACP (Link Aggregation Control Protocol)

LACP permite agrupar varios enlaces físicos en uno solo.

Ventajas:

- Mayor ancho de banda.
- Redundancia.
- Balanceo de carga.

Ejemplo:

```text
4 enlaces físicos

↓

LACP

↓

1 enlace lógico
```

Es habitual entre switches y servidores.

---

### SNMP (Simple Network Management Protocol)

SNMP permite supervisar dispositivos de red de forma remota.

Puede monitorizar:

- Routers.
- Switches.
- Firewalls.
- Servidores.
- Impresoras.
- NAS.

La información suele almacenarse en una **MIB (Management Information Base)**.

Es uno de los protocolos más utilizados en plataformas de monitorización.

---

### NTP (Network Time Protocol)

NTP sincroniza la hora de todos los dispositivos de la red.

Proceso:

```text
Servidor NTP

↓

Clientes

↓

Hora sincronizada
```

Una sincronización correcta es esencial para:

- Logs.
- Autenticación.
- Certificados.
- Auditorías.

---

### LDAP (Lightweight Directory Access Protocol)

LDAP permite consultar y administrar servicios de directorio.

Se utiliza habitualmente con:

- Active Directory.
- OpenLDAP.

Permite:

- Buscar usuarios.
- Consultar grupos.
- Autenticar equipos.
- Centralizar identidades.

---

### Kerberos

Kerberos es un protocolo de autenticación basado en tickets.

Características:

- Autenticación segura.
- Evita enviar contraseñas continuamente.
- Muy utilizado en Active Directory.

Es uno de los pilares de la autenticación en redes Windows.

---

### SSH (Secure Shell)

SSH permite administrar equipos de forma remota utilizando conexiones cifradas.

Permite:

- Consola remota.
- Transferencia segura de archivos (SCP y SFTP).
- Túneles seguros.

Ha sustituido prácticamente por completo a Telnet.

---

### Telnet

Telnet proporciona acceso remoto sin cifrado.

Actualmente se considera inseguro porque:

- Transmite credenciales en texto plano.
- Puede ser interceptado fácilmente.

Su uso únicamente está justificado en entornos de laboratorio o con equipos muy antiguos.

---

### Syslog

Syslog permite centralizar los registros de eventos de múltiples dispositivos.

Ejemplo:

```text
Router

↓

Servidor Syslog
```

```text
Firewall

↓

Servidor Syslog
```

Centralizar los logs facilita enormemente la administración y el análisis de incidencias.

---

### Protocolos de monitorización

Además de SNMP, existen otros mecanismos ampliamente utilizados.

Entre ellos:

- NetFlow.
- sFlow.
- IPFIX.

Permiten conocer:

- Tráfico generado.
- Consumo de ancho de banda.
- Aplicaciones utilizadas.
- Equipos más activos.

Son muy utilizados en redes empresariales.

---

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

[⬆️ Volver al índice](#índice)

## Switching y VLAN

Los switches constituyen el núcleo de la mayoría de redes locales modernas. Son los dispositivos encargados de interconectar equipos dentro de una LAN, permitiendo que la comunicación se realice de forma eficiente y reduciendo las colisiones que existían en tecnologías más antiguas como los hubs.

En entornos empresariales, el switching suele complementarse con **VLAN**, enlaces troncales, protocolos de prevención de bucles y mecanismos de agregación de enlaces para construir redes escalables, seguras y altamente disponibles.

---

### ¿Qué es un switch?

Un **switch** es un dispositivo de red que opera principalmente en la **capa 2 (Enlace de datos)** del modelo OSI.

Su función consiste en reenviar las tramas únicamente al puerto donde se encuentra el dispositivo destinatario.

```text
PC1

↓

Switch

↓

PC2
```

Gracias a ello se optimiza el tráfico y se mejora el rendimiento de la red.

---

### Funcionamiento de un switch

Cada vez que un equipo transmite información, el switch aprende automáticamente la dirección MAC del dispositivo.

Este proceso permite construir una tabla interna.

```text
MAC

↓

Puerto

↓

Tabla CAM
```

Cuando recibe una nueva trama:

- Consulta la tabla.
- Localiza el puerto correspondiente.
- Reenvía únicamente la información necesaria.

---

### Tabla CAM

La **CAM (Content Addressable Memory)** almacena la relación entre direcciones MAC y puertos físicos.

Ejemplo:

| Dirección MAC | Puerto |
|---------------|--------|
| AA:BB:CC:11:22:33 | Fa0/1 |
| DD:EE:FF:44:55:66 | Fa0/2 |

Esto evita enviar tráfico innecesario al resto de equipos.

---

### Dominios de colisión

Cada puerto de un switch constituye un dominio de colisión independiente.

```text
PC

↓

Puerto independiente

↓

Switch
```

Como consecuencia:

- Se eliminan prácticamente las colisiones.
- Se mejora el rendimiento.
- Todos los equipos pueden transmitir simultáneamente.

---

### Dominios de broadcast

Aunque un switch separa los dominios de colisión, todos los equipos pertenecen inicialmente al mismo dominio de broadcast.

```text
Broadcast

↓

Todos los puertos
```

Para dividir este dominio se utilizan las VLAN.

---

### ¿Qué es una VLAN?

Una **VLAN (Virtual Local Area Network)** permite dividir una red física en varias redes lógicas independientes.

Cada VLAN funciona como si fuese una red completamente separada.

Ejemplo:

```text
Switch

↓

VLAN 10

↓

Administración
```

```text
↓

VLAN 20

↓

Ventas
```

Aunque ambos departamentos utilicen el mismo switch, permanecerán aislados entre sí.

---

### Ventajas de las VLAN

Las VLAN ofrecen numerosas ventajas.

Entre ellas:

- Mayor seguridad.
- Reducción del tráfico broadcast.
- Mejor organización de la red.
- Aislamiento entre departamentos.
- Administración más sencilla.

Son una de las tecnologías más utilizadas en redes empresariales.

---

### Identificador de VLAN

Cada VLAN posee un identificador numérico.

Ejemplos habituales:

| VLAN | Uso |
|------|-----|
| 1 | VLAN por defecto |
| 10 | Administración |
| 20 | Ventas |
| 30 | Recursos Humanos |
| 40 | Invitados |

El identificador recibe el nombre de **VLAN ID**.

---

### Puertos Access

Un **puerto Access** pertenece únicamente a una VLAN.

Ejemplo:

```text
PC

↓

Puerto Access

↓

VLAN 20
```

Es el tipo de puerto utilizado para conectar:

- Equipos.
- Impresoras.
- Teléfonos IP.
- Cámaras.

---

### Puertos Trunk

Un **puerto Trunk** permite transportar varias VLAN simultáneamente.

Ejemplo:

```text
Switch

↓

Puerto Trunk

↓

Switch
```

Las tramas incluyen una etiqueta que identifica la VLAN mediante el estándar **IEEE 802.1Q**.

---

### Etiquetado 802.1Q

Cuando una trama atraviesa un enlace Trunk, incorpora información adicional.

```text
Ethernet

↓

Etiqueta VLAN

↓

Datos
```

Gracias a esta etiqueta los switches conocen a qué VLAN pertenece cada trama.

---

### VLAN nativa

En un enlace Trunk existe una **VLAN nativa**.

Las tramas pertenecientes a dicha VLAN viajan sin etiquetar.

Por motivos de seguridad, muchas organizaciones modifican la VLAN nativa por defecto.

---

### Comunicación entre VLAN

Las VLAN están completamente aisladas.

Para que dos VLAN diferentes puedan comunicarse es necesario un dispositivo de capa 3.

Puede ser:

- Router.
- Switch multicapa (Layer 3 Switch).

Proceso:

```text
VLAN 10

↓

Router

↓

VLAN 20
```

Este proceso recibe el nombre de **Inter-VLAN Routing**.

---

### STP (Spanning Tree Protocol)

Cuando existen varios caminos entre switches pueden aparecer bucles de red.

STP evita este problema bloqueando automáticamente algunos enlaces.

```text
Switch

↘   ↙

Switch

↓

Enlace bloqueado
```

Gracias a ello se evita el colapso de la red.

---

### RSTP (Rapid Spanning Tree Protocol)

RSTP es una evolución de STP.

Sus ventajas principales son:

- Recuperación mucho más rápida.
- Menor tiempo de convergencia.
- Mayor disponibilidad.

Actualmente es la versión más utilizada.

---

### LACP

LACP permite agrupar varios enlaces físicos formando un único enlace lógico.

```text
4 enlaces

↓

LACP

↓

1 enlace lógico
```

Ventajas:

- Mayor ancho de banda.
- Redundancia.
- Balanceo de carga.

---

### Switch multicapa

Un **Layer 3 Switch** combina funciones de switch y router.

Permite:

- Routing entre VLAN.
- Mayor rendimiento.
- Menor latencia.

Es muy habitual en el núcleo de las redes empresariales.

---

### Seguridad en switching

Existen diferentes mecanismos para proteger los switches.

Los más utilizados son:

- Port Security.
- Deshabilitar puertos no utilizados.
- Cambiar la VLAN nativa.
- Desactivar DTP cuando no sea necesario.
- Limitar direcciones MAC.

Estas medidas reducen considerablemente la superficie de ataque.

---

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

[⬆️ Volver al índice](#índice)

## Routing y enrutamiento avanzado

El **routing** es el proceso mediante el cual los datos son enviados desde una red de origen hasta una red de destino utilizando uno o varios dispositivos intermedios denominados **routers**.

En redes pequeñas puede bastar con unas pocas rutas configuradas manualmente, pero en infraestructuras empresariales es necesario utilizar protocolos de enrutamiento dinámico que permitan intercambiar información automáticamente y adaptarse a los cambios de la red.

El conocimiento del routing resulta esencial para conectar distintas sedes, segmentar redes mediante VLAN o proporcionar acceso a Internet de forma eficiente y segura.

---

### ¿Qué es el routing?

El routing consiste en determinar el mejor camino para que un paquete IP llegue hasta su destino.

Proceso:

```text
Equipo origen

↓

Router

↓

Red

↓

Router

↓

Equipo destino
```

Cada router toma decisiones basándose en su tabla de rutas.

---

### ¿Qué es un router?

Un **router** es un dispositivo de **capa 3 (Red)** del modelo OSI.

Su función principal es:

- Interconectar redes distintas.
- Encaminar paquetes IP.
- Separar dominios de broadcast.
- Aplicar políticas de seguridad.
- Proporcionar acceso a Internet.

Sin routers, únicamente podrían comunicarse equipos pertenecientes a la misma red.

---

### Tabla de enrutamiento

Cada router mantiene una **tabla de rutas** donde almacena información sobre las redes conocidas.

Una entrada típica contiene:

- Red de destino.
- Máscara.
- Siguiente salto (Next Hop).
- Interfaz de salida.
- Métrica.

Ejemplo:

| Red destino | Next Hop | Interfaz |
|--------------|----------|----------|
| 192.168.1.0/24 | Directa | Gig0/0 |
| 10.0.0.0/24 | 192.168.1.1 | Gig0/1 |
| 0.0.0.0/0 | ISP | Gig0/2 |

---

### Rutas conectadas

Las rutas conectadas aparecen automáticamente cuando una interfaz del router pertenece a una red.

Ejemplo:

```text
Gig0/0

↓

192.168.1.1/24

↓

Ruta conectada
```

No requieren configuración adicional.

---

### Rutas estáticas

Las **rutas estáticas** son configuradas manualmente por el administrador.

Ventajas:

- Simplicidad.
- Bajo consumo de recursos.
- Control total del tráfico.

Inconvenientes:

- No se adaptan automáticamente a los cambios.
- Requieren mantenimiento manual.

Son recomendables en redes pequeñas o para rutas muy concretas.

---

### Ruta por defecto

La **ruta por defecto** se utiliza cuando el router desconoce el destino de un paquete.

Se representa como:

```text
0.0.0.0/0
```

Habitualmente apunta hacia:

- El proveedor de Internet.
- Otro router principal.

Es una de las rutas más importantes de cualquier infraestructura.

---

### Enrutamiento dinámico

En redes grandes resulta inviable configurar todas las rutas manualmente.

Los routers pueden intercambiar información automáticamente mediante protocolos de enrutamiento.

Ventajas:

- Adaptación automática.
- Alta disponibilidad.
- Escalabilidad.
- Menor administración manual.

---

### Protocolos de enrutamiento

Los protocolos más utilizados son:

| Protocolo | Tipo |
|------------|------|
| RIP | IGP |
| OSPF | IGP |
| EIGRP | IGP |
| IS-IS | IGP |
| BGP | EGP |

Cada uno está diseñado para escenarios diferentes.

---

### RIP

**RIP (Routing Information Protocol)** es uno de los protocolos dinámicos más sencillos.

Características:

- Métrica basada en saltos.
- Máximo de 15 saltos.
- Actualizaciones periódicas.
- Fácil configuración.

Actualmente se utiliza principalmente con fines didácticos.

---

### OSPF

**OSPF (Open Shortest Path First)** es el protocolo dinámico más utilizado en redes empresariales.

Características:

- Alta velocidad.
- Escalable.
- Basado en áreas.
- Algoritmo SPF.
- Baja convergencia.

Es adecuado para infraestructuras medianas y grandes.

---

### EIGRP

**EIGRP (Enhanced Interior Gateway Routing Protocol)** fue desarrollado por Cisco.

Características:

- Muy rápido.
- Bajo consumo.
- Excelente convergencia.
- Fácil administración.

Aunque inicialmente era propietario, actualmente puede utilizarse en otros fabricantes compatibles.

---

### BGP

**BGP (Border Gateway Protocol)** se utiliza para comunicar sistemas autónomos diferentes.

Es el protocolo responsable del funcionamiento de Internet.

Características:

- Muy escalable.
- Basado en políticas.
- Complejo de administrar.
- Utilizado por operadores y grandes organizaciones.

---

### Métricas de enrutamiento

Cuando existen varias rutas posibles, el router utiliza una métrica para elegir la mejor.

Dependiendo del protocolo, la métrica puede basarse en:

- Número de saltos.
- Ancho de banda.
- Retardo.
- Coste.
- Fiabilidad.
- Carga.

La ruta con mejor métrica será la seleccionada.

---

### Next Hop

El **Next Hop** representa el siguiente router al que debe enviarse un paquete.

Ejemplo:

```text
Router A

↓

Next Hop

↓

Router B

↓

Destino
```

Cada router únicamente necesita conocer el siguiente salto, no el camino completo.

---

### Inter-VLAN Routing

Cuando existen varias VLAN, un router o un switch multicapa permite que puedan comunicarse.

Proceso:

```text
VLAN 10

↓

Router

↓

VLAN 20
```

Esta técnica es imprescindible en la mayoría de redes empresariales.

---

### NAT (Network Address Translation)

NAT permite traducir direcciones IP privadas a direcciones públicas.

Ejemplo:

```text
192.168.1.25

↓

NAT

↓

80.45.10.20
```

Ventajas:

- Ahorro de direcciones IPv4.
- Mayor seguridad.
- Acceso compartido a Internet.

---

### PAT (Port Address Translation)

PAT es una variante de NAT.

Permite que múltiples equipos compartan una única dirección IP pública.

Ejemplo:

```text
PC1

↓

192.168.1.10
```

```text
PC2

↓

192.168.1.20
```

↓

```text
Una única IP pública
```

Es la configuración más habitual en empresas.

---

### Balanceo de carga

Cuando existen varias rutas equivalentes, algunos protocolos permiten repartir el tráfico.

Ventajas:

- Mejor aprovechamiento del ancho de banda.
- Mayor disponibilidad.
- Reducción de cuellos de botella.

---

### Redundancia

Las redes empresariales suelen disponer de rutas alternativas.

```text
Router principal

↓

Fallo

↓

Router secundario
```

Los protocolos dinámicos detectan automáticamente el cambio y recalculan las rutas.

---

### Resolución de incidencias

Durante el diagnóstico del routing suelen utilizarse herramientas como:

Comprobar conectividad:

```bash
ping
```

Mostrar el recorrido:

```bash
traceroute
```

En Windows:

```powershell
tracert
```

Consultar la tabla de rutas:

Linux:

```bash
ip route
```

Windows:

```powershell
route print
```

---

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

[⬆️ Volver al índice](#índice)

## Alta disponibilidad y redundancia

En una infraestructura empresarial es fundamental garantizar que los servicios continúen funcionando incluso cuando se produce un fallo de hardware, software o comunicaciones.

La **alta disponibilidad (High Availability o HA)** engloba el conjunto de técnicas destinadas a minimizar el tiempo de inactividad de un sistema, mientras que la **redundancia** consiste en duplicar componentes críticos para evitar puntos únicos de fallo.

Ambos conceptos son esenciales en servidores, redes, almacenamiento y centros de datos.

---

### ¿Qué es la alta disponibilidad?

La alta disponibilidad consiste en diseñar sistemas capaces de seguir prestando servicio ante la aparición de incidencias.

Su objetivo principal es:

- Reducir interrupciones.
- Garantizar la continuidad del negocio.
- Minimizar el tiempo de recuperación.
- Evitar pérdidas económicas.

En muchas organizaciones, unos pocos minutos de inactividad pueden tener un impacto importante.

---

### ¿Qué es la redundancia?

La redundancia consiste en disponer de componentes adicionales preparados para sustituir a los principales en caso de fallo.

Ejemplo:

```text
Servidor principal

↓

Fallo

↓

Servidor secundario
```

El usuario continúa utilizando el servicio sin apenas interrupciones.

---

### Punto único de fallo (SPOF)

Un **SPOF (Single Point Of Failure)** es cualquier elemento cuya avería provoca la caída completa del servicio.

Ejemplos:

- Un único router.
- Un único switch.
- Un único servidor.
- Una única fuente de alimentación.
- Un único enlace de red.

Eliminar los SPOF es uno de los principales objetivos del diseño de infraestructuras.

---

### Redundancia de red

Las redes empresariales suelen disponer de varios caminos entre dispositivos.

Ejemplo:

```text
Switch principal

↙        ↘

Switch A  Switch B
```

Si uno de los enlaces deja de funcionar, el tráfico puede utilizar el otro camino disponible.

Esto aumenta considerablemente la disponibilidad.

---

### Redundancia de routers

Puede configurarse más de un router como puerta de enlace.

```text
Router activo

↓

Fallo

↓

Router de respaldo
```

Protocolos como:

- HSRP.
- VRRP.

Permiten realizar el cambio automáticamente.

---

### Redundancia de switches

Los switches también pueden configurarse de forma redundante.

Es habitual disponer de:

- Dos switches principales.
- Enlaces duplicados.
- Agregación mediante LACP.
- STP o RSTP para evitar bucles.

Así, el fallo de un switch no implica la pérdida de conectividad.

---

### Agregación de enlaces (LACP)

**LACP (Link Aggregation Control Protocol)** permite agrupar varios enlaces físicos en uno solo.

```text
4 enlaces

↓

LACP

↓

1 enlace lógico
```

Ventajas:

- Mayor ancho de banda.
- Redundancia.
- Balanceo de carga.

Si uno de los enlaces falla, el resto continúa funcionando.

---

### Alta disponibilidad en servidores

Los servidores críticos suelen configurarse en clústeres.

Ejemplo:

```text
Servidor A

↓

Clúster

↓

Servidor B
```

Si el servidor principal deja de responder, el secundario asume automáticamente el servicio.

---

### Clústeres

Un **clúster** es un conjunto de servidores que trabajan conjuntamente.

Dependiendo de su función pueden ser:

- Clúster de alta disponibilidad.
- Clúster de balanceo de carga.
- Clúster de almacenamiento.
- Clúster de bases de datos.

Su objetivo es mejorar tanto la disponibilidad como el rendimiento.

---

### Balanceo de carga

El balanceo distribuye las peticiones entre varios servidores.

```text
Usuarios

↓

Balanceador

↓

Servidor A
```

```text
↓

Servidor B
```

```text
↓

Servidor C
```

Ventajas:

- Mayor rendimiento.
- Mejor reparto de carga.
- Alta disponibilidad.

---

### Balanceadores de carga

Los balanceadores pueden ser:

**Hardware**

- F5 BIG-IP.
- Citrix ADC.

**Software**

- HAProxy.
- NGINX.
- Traefik.

Estos dispositivos deciden qué servidor atenderá cada petición.

---

### Redundancia del almacenamiento

El almacenamiento suele protegerse mediante:

- RAID.
- Cabinas duplicadas.
- Replicación.
- Snapshots.
- NAS redundantes.
- SAN con múltiples controladoras.

Así se evita la pérdida del servicio ante fallos físicos.

---

### Replicación

La replicación mantiene una copia sincronizada de los datos en otro sistema.

```text
Servidor principal

↓

Replicación

↓

Servidor secundario
```

Puede realizarse:

- En tiempo real.
- De forma periódica.

Es una de las bases de los planes de recuperación ante desastres.

---

### Redundancia eléctrica

También conviene proteger la alimentación eléctrica.

Es habitual disponer de:

- Dos fuentes de alimentación.
- Dos líneas eléctricas.
- Sistemas UPS (SAI).
- Generadores.

Esto permite mantener el servicio incluso durante cortes de suministro.

---

### Failover

El **Failover** consiste en transferir automáticamente un servicio desde un sistema averiado hacia otro disponible.

Proceso:

```text
Servidor principal

↓

Fallo

↓

Servidor secundario

↓

Servicio operativo
```

El cambio puede producirse de forma automática o manual.

---

### Failback

Cuando el sistema principal vuelve a estar disponible puede recuperarse el funcionamiento habitual.

```text
Servidor secundario

↓

Principal recuperado

↓

Failback

↓

Servicio principal
```

No todos los sistemas realizan este proceso automáticamente.

---

### Disponibilidad

La disponibilidad suele expresarse como porcentaje.

Ejemplos:

| Disponibilidad | Tiempo máximo de caída al año |
|----------------|-------------------------------|
| 99 % | ~3,6 días |
| 99,9 % | ~8,8 horas |
| 99,99 % | ~53 minutos |
| 99,999 % | ~5 minutos |

Cuantos más "nueves" tenga la disponibilidad, menor será el tiempo permitido de inactividad.

---

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

[⬆️ Volver al índice](#índice)

## Seguridad en redes

La seguridad en redes engloba el conjunto de medidas destinadas a proteger la infraestructura de comunicaciones frente a accesos no autorizados, ataques, fugas de información y cualquier otra amenaza que pueda comprometer la confidencialidad, integridad o disponibilidad de los datos.

En una red empresarial no basta con conectar dispositivos entre sí; es necesario controlar quién puede acceder, qué recursos puede utilizar y cómo se supervisa la actividad de la red.

Una estrategia de seguridad adecuada combina tecnologías, procedimientos y políticas para reducir al máximo los riesgos.

---

### Objetivos de la seguridad en redes

Las medidas de seguridad persiguen principalmente:

- Proteger la información.
- Evitar accesos no autorizados.
- Detectar actividades sospechosas.
- Garantizar la disponibilidad de los servicios.
- Limitar el impacto de posibles ataques.

Estos objetivos forman parte de la denominada **tríada CIA**:

- **Confidencialidad**.
- **Integridad**.
- **Disponibilidad**.

---

### Principales amenazas

Una infraestructura de red puede verse afectada por múltiples amenazas.

Entre las más habituales se encuentran:

- Malware.
- Ransomware.
- Ataques DDoS.
- Phishing.
- Suplantación de identidad.
- Escaneo de puertos.
- Fuerza bruta.
- Ataques Man-in-the-Middle.
- ARP Spoofing.
- DNS Spoofing.

Cada una requiere medidas de protección específicas.

---

### Firewalls

El **firewall** constituye la primera línea de defensa de una red.

Su función consiste en controlar el tráfico que entra y sale de la infraestructura mediante reglas previamente definidas.

Ejemplo:

```text
Internet

↓

Firewall

↓

Red interna
```

El firewall puede permitir o bloquear conexiones según distintos criterios.

---

### Tipos de firewall

Los principales tipos son:

#### Firewall de filtrado de paquetes

Analiza:

- Dirección IP.
- Puerto.
- Protocolo.

Es el modelo más sencillo.

---

#### Firewall con estado (Stateful)

Además de analizar los paquetes, mantiene información sobre las conexiones activas.

Esto permite tomar decisiones más precisas y seguras.

Es el tipo más utilizado actualmente.

---

#### Firewall de nueva generación (NGFW)

Los **Next Generation Firewall** incorporan funciones avanzadas como:

- Inspección profunda de paquetes.
- Control de aplicaciones.
- IDS/IPS integrado.
- Filtrado web.
- Detección de malware.

Son habituales en entornos empresariales.

---

### ACL (Access Control List)

Las **ACL** permiten controlar qué tráfico está permitido o bloqueado.

Una ACL puede basarse en:

- Dirección IP.
- Puerto.
- Protocolo.
- Red origen.
- Red destino.

Ejemplo:

```text
Red invitados

↓

Sin acceso

↓

Servidores internos
```

Las ACL suelen configurarse en routers, switches multicapa y firewalls.

---

### Segmentación de red

Una de las mejores medidas de seguridad consiste en dividir la red en diferentes segmentos.

Puede realizarse mediante:

- VLAN.
- Firewalls internos.
- Redes independientes.

Ejemplo:

```text
Administración

↓

VLAN 10
```

```text
Producción

↓

VLAN 20
```

```text
Invitados

↓

VLAN 30
```

La segmentación limita la propagación de ataques.

---

### DMZ (Zona desmilitarizada)

Una **DMZ** es una red intermedia destinada a alojar servicios accesibles desde Internet.

Ejemplo:

```text
Internet

↓

Firewall

↓

DMZ

↓

Servidor Web
```

```text
↓

Firewall

↓

Red interna
```

Si un servidor de la DMZ resulta comprometido, la red interna permanece protegida.

---

### IDS

Un **IDS (Intrusion Detection System)** detecta actividades sospechosas dentro de la red.

Su función consiste en:

- Analizar el tráfico.
- Detectar ataques.
- Generar alertas.

No bloquea el tráfico.

Ejemplos:

- Snort.
- Suricata.

---

### IPS

Un **IPS (Intrusion Prevention System)** va un paso más allá.

Además de detectar amenazas:

- Bloquea automáticamente conexiones maliciosas.
- Detiene ataques conocidos.
- Reduce el impacto de las intrusiones.

Muchos firewalls NGFW incorporan IPS integrado.

---

### VPN

Las **VPN (Virtual Private Network)** permiten establecer conexiones seguras a través de Internet.

Proceso:

```text
Usuario remoto

↓

VPN cifrada

↓

Empresa
```

Ventajas:

- Cifrado.
- Acceso remoto seguro.
- Protección de la información.

Son imprescindibles para el teletrabajo y el acceso remoto.

---

### Port Security

**Port Security** es una función de los switches que limita qué dispositivos pueden conectarse a un puerto.

Puede configurarse para:

- Permitir únicamente determinadas direcciones MAC.
- Limitar el número de dispositivos.
- Bloquear el puerto ante una infracción.

Ayuda a evitar conexiones no autorizadas.

---

### 802.1X

El estándar **IEEE 802.1X** proporciona autenticación antes de permitir el acceso a la red.

Proceso:

```text
Usuario

↓

Autenticación

↓

Acceso a la red
```

Suele integrarse con:

- Active Directory.
- Servidores RADIUS.

Es muy habitual en redes corporativas.

---

### WPA2 y WPA3

En redes inalámbricas se utilizan protocolos de cifrado.

Los más habituales son:

- WPA2.
- WPA3.

Actualmente se recomienda utilizar **WPA3** siempre que sea posible debido a sus mejoras de seguridad.

---

### RADIUS

**RADIUS (Remote Authentication Dial-In User Service)** centraliza la autenticación de usuarios.

Permite gestionar el acceso a:

- Redes Wi-Fi.
- VPN.
- Equipos de red.
- 802.1X.

De esta forma, la administración de credenciales resulta mucho más sencilla.

---

### Registro de eventos

Todos los dispositivos de red deberían registrar su actividad.

Habitualmente se centralizan mediante:

- Syslog.
- SIEM.
- Servidores de monitorización.

Los registros permiten:

- Detectar ataques.
- Investigar incidencias.
- Cumplir requisitos de auditoría.

---

### Actualizaciones

Mantener actualizado el software de los dispositivos es una medida básica de seguridad.

Conviene actualizar:

- Firewalls.
- Routers.
- Switches.
- Puntos de acceso.
- Sistemas operativos.
- Firmware.

Las actualizaciones corrigen vulnerabilidades conocidas.

---

### Principio de mínimo privilegio

Los usuarios y dispositivos deben disponer únicamente de los permisos necesarios para realizar su trabajo.

Esto reduce el impacto de:

- Errores.
- Malware.
- Ataques internos.

Es uno de los principios fundamentales de la ciberseguridad.

---

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

[⬆️ Volver al índice](#índice)

## Monitorización y diagnóstico

La monitorización de una red consiste en supervisar de forma continua el estado de los dispositivos, el tráfico y los servicios para detectar incidencias antes de que afecten a los usuarios.

Por su parte, el diagnóstico comprende el conjunto de técnicas utilizadas para localizar y resolver problemas de conectividad, rendimiento o disponibilidad.

Una buena estrategia de monitorización reduce el tiempo de respuesta ante incidencias y permite mantener una infraestructura estable, segura y eficiente.

---

### Objetivos de la monitorización

La monitorización permite:

- Detectar fallos rápidamente.
- Supervisar el rendimiento de la red.
- Anticiparse a posibles incidencias.
- Analizar tendencias de uso.
- Generar alertas automáticas.
- Facilitar el diagnóstico de problemas.

Cuanto antes se detecte una anomalía, menor será su impacto.

---

### ¿Qué debe monitorizarse?

En una red empresarial conviene supervisar:

- Routers.
- Switches.
- Firewalls.
- Servidores.
- Puntos de acceso Wi-Fi.
- Balanceadores de carga.
- Enlaces WAN.
- VPN.
- Servicios críticos.

Todos estos elementos forman parte de la infraestructura de comunicaciones.

---

### Parámetros importantes

Los indicadores más habituales son:

- Disponibilidad.
- Latencia.
- Ancho de banda.
- Uso de CPU.
- Uso de memoria.
- Estado de interfaces.
- Errores de red.
- Pérdida de paquetes.
- Tráfico generado.

Analizar estos parámetros permite detectar cuellos de botella y degradaciones del servicio.

---

### Disponibilidad

La disponibilidad indica si un dispositivo responde correctamente.

Ejemplo:

```text
Switch

↓

Respuesta

↓

Activo
```

Si deja de responder:

```text
Switch

↓

Sin respuesta

↓

Alerta
```

Es uno de los primeros indicadores supervisados por cualquier sistema de monitorización.

---

### Latencia

La latencia representa el tiempo que tarda un paquete en llegar desde un origen hasta un destino.

Una latencia elevada puede provocar:

- Lentitud.
- Problemas en VoIP.
- Cortes en videoconferencias.
- Mal rendimiento de aplicaciones.

Se suele medir en milisegundos (ms).

---

### Pérdida de paquetes

La pérdida de paquetes indica que parte del tráfico nunca alcanza su destino.

Puede deberse a:

- Saturación.
- Fallos de hardware.
- Problemas de cableado.
- Interferencias Wi-Fi.
- Configuraciones incorrectas.

Una pérdida elevada suele afectar notablemente a la calidad de la comunicación.

---

### Uso del ancho de banda

También resulta importante conocer cuánto tráfico circula por cada enlace.

Esto permite detectar:

- Saturaciones.
- Usuarios con elevado consumo.
- Aplicaciones que generan demasiado tráfico.
- Necesidad de ampliar la capacidad.

---

### SNMP

Uno de los protocolos más utilizados para monitorizar dispositivos es **SNMP (Simple Network Management Protocol)**.

Permite obtener información sobre:

- Interfaces.
- CPU.
- Memoria.
- Temperatura.
- Estado de los dispositivos.

Muchos programas de monitorización utilizan SNMP como fuente principal de información.

---

### NetFlow

**NetFlow** recopila información detallada sobre el tráfico que atraviesa un dispositivo.

Permite conocer:

- Equipos que más tráfico generan.
- Aplicaciones utilizadas.
- Protocolos.
- Consumo de ancho de banda.
- Conversaciones entre equipos.

Es especialmente útil para detectar anomalías y planificar la capacidad de la red.

---

### Syslog

**Syslog** centraliza los registros de eventos de múltiples dispositivos.

Ejemplo:

```text
Router

↓

Servidor Syslog
```

```text
Firewall

↓

Servidor Syslog
```

Centralizar los registros facilita la investigación de incidencias y auditorías.

---

### Herramientas de monitorización

Algunas de las soluciones más utilizadas son:

- Zabbix.
- PRTG Network Monitor.
- Nagios.
- Centreon.
- Prometheus.
- Grafana.
- SolarWinds.
- LibreNMS.

Estas herramientas permiten supervisar miles de dispositivos desde una única consola.

---

### Herramientas de diagnóstico

Cuando aparece una incidencia, existen diversas utilidades para localizar el problema.

Las más habituales son:

- ping
- traceroute
- tracert
- nslookup
- dig
- ipconfig
- ifconfig
- ip
- arp
- route
- netstat
- tcpdump
- Wireshark

Cada una proporciona información diferente sobre la comunicación de red.

---

### Ping

Comprueba si un equipo responde mediante ICMP.

Linux:

```bash
ping 192.168.1.1
```

Windows:

```powershell
ping 192.168.1.1
```

Permite verificar:

- Conectividad.
- Latencia.
- Pérdida de paquetes.

---

### Traceroute

Muestra todos los routers por los que pasa un paquete hasta llegar a su destino.

Linux:

```bash
traceroute 8.8.8.8
```

Windows:

```powershell
tracert 8.8.8.8
```

Es muy útil para localizar el punto donde se produce un problema de comunicación.

---

### Nslookup y Dig

Permiten comprobar la resolución DNS.

Windows:

```powershell
nslookup ejemplo.com
```

Linux:

```bash
dig ejemplo.com
```

Sirven para verificar:

- Resolución de nombres.
- Servidores DNS.
- Registros DNS.

---

### Netstat

Permite consultar las conexiones de red activas.

Ejemplos:

```bash
netstat
```

o

```powershell
netstat -ano
```

Proporciona información sobre:

- Conexiones abiertas.
- Puertos.
- Procesos asociados.

---

### Tcpdump

**tcpdump** captura paquetes directamente desde la interfaz de red.

Ejemplo:

```bash
tcpdump -i eth0
```

Es una herramienta muy utilizada en servidores Linux.

---

### Wireshark

**Wireshark** es el analizador de protocolos más utilizado.

Permite:

- Capturar tráfico.
- Analizar protocolos.
- Detectar errores.
- Investigar incidencias.
- Analizar ataques.

Puede mostrar el contenido de miles de protocolos diferentes.

---

### Diagnóstico por capas

Una forma habitual de resolver incidencias consiste en seguir el modelo OSI.

Proceso:

```text
Capa Física

↓

Enlace

↓

Red

↓

Transporte

↓

Aplicación
```

Este método permite localizar el origen del problema de forma sistemática.

---

### Alertas

Los sistemas de monitorización suelen generar alertas cuando detectan:

- Equipo caído.
- Enlace inactivo.
- CPU elevada.
- Memoria alta.
- Poco espacio libre.
- Latencia excesiva.
- Pérdida de paquetes.

Las alertas pueden enviarse mediante:

- Correo electrónico.
- SMS.
- Aplicaciones de mensajería.
- Integración con plataformas ITSM.

---

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