# Red

## Introducción

La administración de red permite conocer el estado de las interfaces de red, comprobar la conectividad, diagnosticar problemas de comunicación y obtener información sobre la configuración del equipo.

Dominar estos comandos resulta fundamental para solucionar incidencias relacionadas con direcciones IP, DNS, puertas de enlace, rutas o conexiones entre equipos.

En este capítulo aprenderás a consultar la configuración de red, comprobar la conectividad y obtener información sobre las conexiones activas tanto en Linux como en PowerShell.

---

## Índice

- [Ver la configuración de red](#ver-la-configuración-de-red)
- [Comprobar la conectividad (Ping)](#comprobar-la-conectividad-ping)
- [Consultar la configuración DNS](#consultar-la-configuración-dns)
- [Resolver nombres DNS](#resolver-nombres-dns)
- [Ver las conexiones de red activas](#ver-las-conexiones-de-red-activas)
- [Consultar la tabla de rutas](#consultar-la-tabla-de-rutas)
- [Probar puertos de red](#probar-puertos-de-red)
- [Ver la caché ARP](#ver-la-caché-arp)
- [Resumen de equivalencias](#resumen-de-equivalencias)

---

## Ver la configuración de red

### Linux

```bash
ip addr
```

También puede utilizarse:

```bash
ip address
```

**Descripción**

Muestra la configuración de todas las interfaces de red del sistema.

La información incluye:

- Nombre de la interfaz.
- Estado de la interfaz.
- Dirección IPv4.
- Dirección IPv6.
- Dirección MAC.
- Máscara de red.

---

### PowerShell

```powershell
Get-NetIPAddress
```

También puede utilizarse:

```powershell
Get-NetIPConfiguration
```

**Descripción**

Permite consultar la configuración de red del equipo.

La información mostrada puede incluir:

- Dirección IPv4.
- Dirección IPv6.
- Máscara de subred.
- Puerta de enlace.
- Adaptador de red.
- Configuración DNS.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver la configuración de red | `ip addr` | `Get-NetIPAddress` / `Get-NetIPConfiguration` |

---

### Ejemplos

**Mostrar toda la configuración de red**

Linux

```bash
ip addr
```

PowerShell

```powershell
Get-NetIPConfiguration
```

---

**Mostrar únicamente las direcciones IPv4**

Linux

```bash
ip -4 addr
```

PowerShell

```powershell
Get-NetIPAddress -AddressFamily IPv4
```

---

**Mostrar únicamente las direcciones IPv6**

Linux

```bash
ip -6 addr
```

PowerShell

```powershell
Get-NetIPAddress -AddressFamily IPv6
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `ip addr` muestra toda la información de las interfaces de red. | `Get-NetIPAddress` muestra únicamente las direcciones IP. |
| Puede filtrarse por IPv4 o IPv6 mediante opciones del comando. | Puede filtrarse utilizando el parámetro `-AddressFamily`. |
| La salida es texto estructurado. | La salida son objetos que pueden filtrarse y procesarse mediante la tubería. |

---

### Buenas prácticas

- Comprueba que la interfaz de red se encuentra activa antes de diagnosticar problemas de conectividad.
- Verifica que la dirección IP pertenece a la red correcta.
- Revisa la configuración IPv4 e IPv6 cuando existan problemas de comunicación.
- Comprueba que únicamente las interfaces necesarias se encuentran habilitadas.

---

### Comandos relacionados

- [Comprobar la conectividad (Ping)](#comprobar-la-conectividad-ping)
- [Consultar la configuración DNS](#consultar-la-configuración-dns)
- [Consultar la tabla de rutas](#consultar-la-tabla-de-rutas)

---

[⬆️ Volver al índice](#índice)

## Comprobar la conectividad (Ping)

### Linux

```bash
ping <destino>
```

También puede utilizarse:

```bash
ping -c 4 <destino>
```

**Descripción**

Permite comprobar si existe conectividad entre el equipo local y otro dispositivo de la red.

El comando envía paquetes **ICMP Echo Request** al destino y espera una respuesta (**ICMP Echo Reply**).

La información obtenida incluye:

- Tiempo de respuesta (latencia).
- Número de paquetes enviados y recibidos.
- Pérdida de paquetes.

---

### PowerShell

```powershell
Test-Connection <destino>
```

También puede utilizarse:

```powershell
Test-Connection <destino> -Count 4
```

**Descripción**

Comprueba la conectividad con otro equipo utilizando ICMP, mostrando información sobre el tiempo de respuesta y el resultado de cada intento.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Comprobar conectividad | `ping` | `Test-Connection` |

---

### Ejemplos

**Comprobar la conectividad con Google**

Linux

```bash
ping google.com
```

PowerShell

```powershell
Test-Connection google.com
```

---

**Enviar únicamente cuatro paquetes**

Linux

```bash
ping -c 4 google.com
```

PowerShell

```powershell
Test-Connection google.com -Count 4
```

---

**Comprobar la conectividad con una dirección IP**

Linux

```bash
ping 8.8.8.8
```

PowerShell

```powershell
Test-Connection 8.8.8.8
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `ping` continúa enviando paquetes hasta detenerlo manualmente (`Ctrl + C`). | `Test-Connection` envía cuatro solicitudes por defecto. |
| Para limitar el número de paquetes se utiliza `-c`. | Para indicar el número de intentos se utiliza `-Count`. |
| La salida es texto estructurado. | La salida son objetos que pueden filtrarse y procesarse mediante la tubería. |

---

### Buenas prácticas

- Comprueba primero la conectividad con la puerta de enlace antes de probar servidores externos.
- Si una dirección IP responde pero un nombre de dominio no, es probable que exista un problema de DNS.
- Una respuesta lenta o con pérdida de paquetes puede indicar problemas de red.
- Recuerda que algunos dispositivos bloquean las respuestas ICMP por motivos de seguridad.

---

### Comandos relacionados

- [Consultar la configuración DNS](#consultar-la-configuración-dns)
- [Resolver nombres DNS](#resolver-nombres-dns)
- [Probar puertos de red](#probar-puertos-de-red)

---

> **💡 Consejo:** Si `ping 8.8.8.8` funciona pero `ping google.com` no, la conectividad a Internet probablemente existe y el problema suele estar relacionado con la resolución DNS.

---

[⬆️ Volver al índice](#índice)

## Consultar la configuración DNS

### Linux

```bash
cat /etc/resolv.conf
```

También puede utilizarse:

```bash
resolvectl status
```

(en sistemas con **systemd-resolved**)

**Descripción**

Permite consultar la configuración de los servidores DNS utilizados por el sistema.

La información puede incluir:

- Servidores DNS configurados.
- Dominio de búsqueda.
- Configuración de resolución de nombres.

---

### PowerShell

```powershell
Get-DnsClientServerAddress
```

**Descripción**

Muestra los servidores DNS configurados para cada adaptador de red del equipo.

La salida incluye información como:

- Nombre de la interfaz.
- Direcciones de los servidores DNS.
- Familia de direcciones (IPv4 o IPv6).

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Consultar la configuración DNS | `cat /etc/resolv.conf` / `resolvectl status` | `Get-DnsClientServerAddress` |

---

### Ejemplos

**Mostrar la configuración DNS**

Linux

```bash
cat /etc/resolv.conf
```

PowerShell

```powershell
Get-DnsClientServerAddress
```

---

**Mostrar únicamente los servidores DNS IPv4**

Linux

```bash
grep nameserver /etc/resolv.conf
```

PowerShell

```powershell
Get-DnsClientServerAddress `
-AddressFamily IPv4
```

---

**Consultar la configuración DNS de una interfaz concreta**

Linux

```bash
resolvectl status eth0
```

PowerShell

```powershell
Get-DnsClientServerAddress `
-InterfaceAlias "Ethernet"
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| La configuración suele encontrarse en `/etc/resolv.conf` o gestionarse mediante `systemd-resolved`. | Cada adaptador mantiene su propia configuración DNS. |
| Puede existir uno o varios servidores DNS configurados. | Es posible consultar la configuración por interfaz o por familia de direcciones. |
| La salida es texto estructurado. | La salida son objetos que pueden filtrarse y procesarse mediante la tubería. |

---

### Buenas prácticas

- Comprueba que los servidores DNS configurados sean accesibles y correctos.
- Configura al menos dos servidores DNS cuando sea posible para disponer de redundancia.
- Si existen problemas de resolución de nombres, verifica primero la configuración DNS antes de realizar otras comprobaciones.
- Revisa la configuración de cada interfaz de red, especialmente en equipos con varias conexiones.

---

### Comandos relacionados

- [Resolver nombres DNS](#resolver-nombres-dns)
- [Comprobar la conectividad (Ping)](#comprobar-la-conectividad-ping)
- [Ver la configuración de red](#ver-la-configuración-de-red)

---

> **💡 Consejo:** Si el equipo tiene conexión a Internet pero no puede acceder a páginas web por su nombre, revisa primero la configuración de los servidores DNS. En muchos casos, el problema no está en la red, sino en la resolución de nombres.

---

[⬆️ Volver al índice](#índice)

## Resolver nombres DNS

### Linux

```bash
nslookup <dominio>
```

También puede utilizarse:

```bash
dig <dominio>
```

(si está instalado)

**Descripción**

Permite consultar los registros DNS asociados a un nombre de dominio.

Puede utilizarse para comprobar si un nombre de dominio se resuelve correctamente y obtener información como:

- Dirección IP.
- Servidor DNS utilizado.
- Tiempo de respuesta.
- Registros DNS (A, AAAA, MX, NS, TXT, etc., mediante `dig`).

---

### PowerShell

```powershell
Resolve-DnsName <dominio>
```

También puede utilizarse:

```powershell
nslookup <dominio>
```

**Descripción**

Resuelve un nombre de dominio mediante los servidores DNS configurados en el sistema.

`Resolve-DnsName` devuelve información detallada sobre los registros DNS encontrados.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Resolver un nombre DNS | `nslookup` / `dig` | `Resolve-DnsName` |

---

### Ejemplos

**Resolver un dominio**

Linux

```bash
nslookup google.com
```

PowerShell

```powershell
Resolve-DnsName google.com
```

---

**Consultar un registro MX**

Linux

```bash
dig google.com MX
```

PowerShell

```powershell
Resolve-DnsName `
-Name google.com `
-Type MX
```

---

**Consultar un registro TXT**

Linux

```bash
dig google.com TXT
```

PowerShell

```powershell
Resolve-DnsName `
-Name google.com `
-Type TXT
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `nslookup` ofrece consultas básicas. | `Resolve-DnsName` devuelve objetos con información detallada. |
| `dig` permite consultar prácticamente cualquier tipo de registro DNS. | El tipo de registro se especifica mediante el parámetro `-Type`. |
| La salida es texto estructurado. | La salida son objetos que pueden filtrarse y procesarse mediante la tubería. |

---

### Buenas prácticas

- Comprueba que el dominio resuelve correctamente antes de investigar otros problemas de red.
- Verifica distintos tipos de registros (A, AAAA, MX, TXT, NS) cuando sea necesario.
- Si un dominio no resuelve, comprueba primero la configuración DNS del equipo.
- Utiliza `Resolve-DnsName` o `dig` cuando necesites información más detallada que la proporcionada por `ping`.

---

### Comandos relacionados

- [Consultar la configuración DNS](#consultar-la-configuración-dns)
- [Comprobar la conectividad (Ping)](#comprobar-la-conectividad-ping)
- [Probar puertos de red](#probar-puertos-de-red)

---

> **💡 Consejo:** Un dominio puede resolverse correctamente mediante DNS y, aun así, el servidor no estar disponible. La resolución de nombres únicamente confirma que el DNS funciona; no garantiza que el servicio esté accesible.

---

[⬆️ Volver al índice](#índice)

## Ver las conexiones de red activas

### Linux

```bash
ss -tuln
```

También puede utilizarse:

```bash
ss -tunap
```

**Descripción**

Permite consultar las conexiones de red activas y los puertos que se encuentran en escucha.

La información puede incluir:

- Protocolo (TCP o UDP).
- Dirección local.
- Dirección remota.
- Puerto.
- Estado de la conexión.
- Proceso asociado (con `-p`).

---

### PowerShell

```powershell
Get-NetTCPConnection
```

También puede utilizarse:

```powershell
Get-NetUDPEndpoint
```

**Descripción**

Permite consultar las conexiones TCP activas y los puertos abiertos del equipo.

La salida incluye información como:

- Dirección local.
- Dirección remota.
- Puerto local.
- Puerto remoto.
- Estado de la conexión.
- Proceso propietario (PID).

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver conexiones TCP | `ss -tuln` | `Get-NetTCPConnection` |
| Ver conexiones UDP | `ss -u` | `Get-NetUDPEndpoint` |

---

### Ejemplos

**Mostrar todas las conexiones y puertos en escucha**

Linux

```bash
ss -tuln
```

PowerShell

```powershell
Get-NetTCPConnection
```

---

**Mostrar únicamente los puertos en escucha**

Linux

```bash
ss -tln
```

PowerShell

```powershell
Get-NetTCPConnection |
Where-Object {$_.State -eq "Listen"}
```

---

**Mostrar el proceso asociado a cada conexión**

Linux

```bash
sudo ss -tunap
```

PowerShell

```powershell
Get-NetTCPConnection |
Select-Object LocalAddress,
              LocalPort,
              RemoteAddress,
              RemotePort,
              State,
              OwningProcess
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `ss` sustituye al antiguo `netstat` y ofrece un mejor rendimiento. | `Get-NetTCPConnection` muestra únicamente conexiones TCP. |
| Con `-p` puede mostrarse el proceso asociado a cada conexión. | El proceso se identifica mediante el PID (`OwningProcess`). |
| La salida es texto estructurado. | La salida son objetos que pueden filtrarse y procesarse mediante la tubería. |

---

### Buenas prácticas

- Revisa periódicamente qué puertos se encuentran en escucha.
- Comprueba que únicamente existan conexiones esperadas.
- Identifica el proceso propietario cuando detectes un puerto desconocido.
- Si un puerto está ocupado inesperadamente, investiga qué aplicación lo está utilizando antes de detener el proceso.

---

### Comandos relacionados

- [Probar puertos de red](#probar-puertos-de-red)
- [Consultar la tabla de rutas](#consultar-la-tabla-de-rutas)
- [Ver la caché ARP](#ver-la-caché-arp)

---

> **💡 Consejo:** Si necesitas saber qué programa está utilizando un puerto concreto, identifica primero el **PID** y después consulta el proceso correspondiente (`ps` en Linux o `Get-Process` en PowerShell).

---

[⬆️ Volver al índice](#índice)

## Consultar la tabla de rutas

### Linux

```bash
ip route
```

También puede utilizarse:

```bash
ip r
```

**Descripción**

Permite mostrar la tabla de rutas del sistema.

La tabla de rutas indica cómo decide el sistema operativo enviar los paquetes hacia otras redes.

La información incluye:

- Red de destino.
- Puerta de enlace (Gateway).
- Interfaz utilizada.
- Métrica de la ruta.

---

### PowerShell

```powershell
Get-NetRoute
```

**Descripción**

Muestra la tabla de rutas configurada en el equipo.

La salida incluye información como:

- Red de destino.
- Prefijo de red.
- Puerta de enlace.
- Interfaz de salida.
- Métrica.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Consultar la tabla de rutas | `ip route` | `Get-NetRoute` |

---

### Ejemplos

**Mostrar toda la tabla de rutas**

Linux

```bash
ip route
```

PowerShell

```powershell
Get-NetRoute
```

---

**Mostrar la puerta de enlace predeterminada**

Linux

```bash
ip route | grep default
```

PowerShell

```powershell
Get-NetRoute `
| Where-Object {$_.DestinationPrefix -eq "0.0.0.0/0"}
```

---

**Mostrar únicamente las rutas IPv4**

Linux

```bash
ip -4 route
```

PowerShell

```powershell
Get-NetRoute `
-AddressFamily IPv4
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `ip route` muestra la tabla de rutas gestionada por el kernel. | `Get-NetRoute` consulta la tabla de rutas de Windows. |
| Puede filtrarse fácilmente mediante `grep`. | Puede filtrarse mediante `Where-Object` o utilizando parámetros del cmdlet. |
| La salida es texto estructurado. | La salida son objetos que pueden procesarse mediante la tubería. |

---

### Buenas prácticas

- Comprueba siempre que exista una ruta predeterminada (`default` o `0.0.0.0/0`) cuando un equipo no tenga acceso a Internet.
- Verifica que la puerta de enlace sea correcta para la red utilizada.
- Revisa la métrica cuando existan varias rutas hacia el mismo destino.
- Después de modificar la configuración de red, comprueba que la tabla de rutas se haya actualizado correctamente.

---

### Comandos relacionados

- [Ver la configuración de red](#ver-la-configuración-de-red)
- [Comprobar la conectividad (Ping)](#comprobar-la-conectividad-ping)
- [Ver las conexiones de red activas](#ver-las-conexiones-de-red-activas)

---

> **💡 Consejo:** Si un equipo puede comunicarse con otros dispositivos de su red local pero no con redes externas, uno de los primeros aspectos que debes comprobar es la **ruta predeterminada**. Una puerta de enlace incorrecta suele ser una causa frecuente de este tipo de problemas.

---

[⬆️ Volver al índice](#índice)

## Probar puertos de red

### Linux

```bash
nc -zv <host> <puerto>
```

También puede utilizarse:

```bash
telnet <host> <puerto>
```

(si está instalado)

**Descripción**

Permite comprobar si un puerto TCP remoto se encuentra accesible.

Es una herramienta muy utilizada para verificar si un servicio está escuchando correctamente o si existe algún problema de conectividad o filtrado por firewall.

- `nc` (Netcat) es la opción recomendada.
- `telnet` sigue utilizándose en algunos entornos, aunque está prácticamente en desuso para este tipo de comprobaciones.

---

### PowerShell

```powershell
Test-NetConnection <host> -Port <puerto>
```

**Descripción**

Comprueba si un puerto TCP remoto está abierto y accesible.

Además del resultado de la prueba, muestra información adicional como:

- Dirección IP del destino.
- Resolución DNS.
- Interfaz utilizada.
- Estado de la conexión TCP.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Probar un puerto TCP | `nc -zv` | `Test-NetConnection -Port` |

---

### Ejemplos

**Comprobar el puerto HTTPS (443)**

Linux

```bash
nc -zv google.com 443
```

PowerShell

```powershell
Test-NetConnection `
google.com `
-Port 443
```

---

**Comprobar el puerto SSH (22)**

Linux

```bash
nc -zv servidor.local 22
```

PowerShell

```powershell
Test-NetConnection `
servidor.local `
-Port 22
```

---

**Comprobar el puerto RDP (3389)**

Linux

```bash
nc -zv servidor.local 3389
```

PowerShell

```powershell
Test-NetConnection `
servidor.local `
-Port 3389
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `nc` comprueba rápidamente si un puerto está abierto. | `Test-NetConnection` muestra información mucho más detallada sobre la prueba. |
| También puede utilizarse `telnet`, aunque está obsoleto para este uso. | El cmdlet integra resolución DNS, conectividad ICMP y prueba TCP en un único comando. |
| La salida es texto estructurado. | La salida son objetos que pueden filtrarse y procesarse mediante la tubería. |

---

### Buenas prácticas

- Comprueba primero que el equipo responde al ping antes de probar un puerto.
- Verifica que el servicio correspondiente esté iniciado si el puerto aparece cerrado.
- Ten en cuenta que un firewall puede bloquear el acceso al puerto aunque el servicio esté funcionando.
- Utiliza este comando para comprobar servicios como SSH (22), HTTP (80), HTTPS (443), RDP (3389) o SMB (445).

---

### Comandos relacionados

- [Comprobar la conectividad (Ping)](#comprobar-la-conectividad-ping)
- [Ver las conexiones de red activas](#ver-las-conexiones-de-red-activas)
- [Resolver nombres DNS](#resolver-nombres-dns)

---

> **💡 Consejo:** Si el ping funciona pero `Test-NetConnection` o `nc` indican que el puerto está cerrado, normalmente el problema se encuentra en el servicio remoto o en un firewall, no en la conectividad de red.

---

[⬆️ Volver al índice](#índice)

## Ver la caché ARP

### Linux

```bash
ip neigh
```

También puede utilizarse:

```bash
arp -a
```

(si está instalado)

**Descripción**

Permite mostrar la caché ARP (Address Resolution Protocol) del sistema.

La caché ARP relaciona las direcciones IP con sus correspondientes direcciones MAC dentro de la red local.

La información mostrada incluye:

- Dirección IP.
- Dirección MAC.
- Interfaz de red.
- Estado de la entrada.

---

### PowerShell

```powershell
Get-NetNeighbor
```

**Descripción**

Muestra la tabla de vecinos del sistema (Neighbor Cache), que contiene las asociaciones entre direcciones IP y direcciones MAC.

La salida incluye información como:

- Dirección IP.
- Dirección MAC.
- Interfaz de red.
- Estado de la entrada.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver la caché ARP | `ip neigh` | `Get-NetNeighbor` |

---

### Ejemplos

**Mostrar toda la caché ARP**

Linux

```bash
ip neigh
```

PowerShell

```powershell
Get-NetNeighbor
```

---

**Buscar una dirección IP concreta**

Linux

```bash
ip neigh | grep 192.168.1.1
```

PowerShell

```powershell
Get-NetNeighbor `
| Where-Object {$_.IPAddress -eq "192.168.1.1"}
```

---

**Mostrar únicamente las entradas alcanzables**

Linux

```bash
ip neigh | grep REACHABLE
```

PowerShell

```powershell
Get-NetNeighbor `
| Where-Object {$_.State -eq "Reachable"}
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `ip neigh` muestra la caché ARP gestionada por el kernel. | `Get-NetNeighbor` consulta la tabla de vecinos de Windows. |
| También pueden mostrarse estados como `STALE`, `DELAY` o `FAILED`. | Los estados aparecen con nombres similares (`Reachable`, `Stale`, `Unreachable`, etc.). |
| La salida es texto estructurado. | La salida son objetos que pueden filtrarse y procesarse mediante la tubería. |

---

### Buenas prácticas

- Comprueba que la dirección MAC asociada a una IP coincide con el dispositivo esperado.
- Si una entrada presenta un estado incorrecto o desactualizado, vuelve a comprobar la conectividad con el dispositivo.
- Utiliza la caché ARP para detectar posibles conflictos de red o problemas de comunicación en la red local.
- Recuerda que ARP únicamente funciona en redes IPv4; para IPv6 se utiliza el protocolo **NDP (Neighbor Discovery Protocol)**.

---

### Comandos relacionados

- [Ver la configuración de red](#ver-la-configuración-de-red)
- [Comprobar la conectividad (Ping)](#comprobar-la-conectividad-ping)
- [Ver las conexiones de red activas](#ver-las-conexiones-de-red-activas)

---

> **💡 Consejo:** Si un equipo responde al `ping` pero aparece con una dirección MAC diferente de la esperada, podría tratarse de un cambio de hardware, una configuración incorrecta o, en casos poco frecuentes, un intento de **ARP Spoofing**.

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|--------|--------|------------|
| Ver la configuración de red | `ip addr` | `Get-NetIPConfiguration` / `Get-NetIPAddress` |
| Comprobar la conectividad | `ping` | `Test-Connection` |
| Consultar la configuración DNS | `cat /etc/resolv.conf` / `resolvectl status` | `Get-DnsClientServerAddress` |
| Resolver nombres DNS | `dig` / `nslookup` | `Resolve-DnsName` |
| Ver las conexiones de red activas | `ss` | `Get-NetTCPConnection` |
| Consultar la tabla de rutas | `ip route` | `Get-NetRoute` |
| Probar puertos de red | `nc` | `Test-NetConnection` |
| Ver la caché ARP | `ip neigh` | `Get-NetNeighbor` |

---

### Buenas prácticas generales

- Comprueba primero la configuración IP antes de diagnosticar problemas de red.
- Si existe conectividad por IP pero no por nombre, revisa la configuración DNS.
- Utiliza `Test-NetConnection` o `nc` para comprobar servicios concretos, no solo `ping`.
- Revisa periódicamente los puertos en escucha y las conexiones activas.
- Comprueba la tabla de rutas cuando existan problemas para acceder a otras redes.
- Verifica la caché ARP si sospechas de problemas de comunicación dentro de la red local.
- Documenta siempre la configuración IP, DNS y puerta de enlace antes de realizar cambios.

---

### Comandos más utilizados

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver configuración IP | `ip addr` | `Get-NetIPConfiguration` |
| Comprobar conectividad | `ping google.com` | `Test-Connection google.com` |
| Ver DNS | `cat /etc/resolv.conf` | `Get-DnsClientServerAddress` |
| Resolver un dominio | `dig google.com` | `Resolve-DnsName google.com` |
| Ver conexiones | `ss -tuln` | `Get-NetTCPConnection` |
| Ver rutas | `ip route` | `Get-NetRoute` |
| Probar un puerto | `nc -zv servidor 443` | `Test-NetConnection servidor -Port 443` |
| Ver caché ARP | `ip neigh` | `Get-NetNeighbor` |

---

### Siguiente capítulo

➡️ **06-Procesos-de-Red.md** *(o el nombre que hayas decidido para el siguiente tema)*

En el siguiente capítulo aprenderás a capturar tráfico, analizar conexiones y utilizar herramientas de diagnóstico más avanzadas para investigar problemas de red y comunicaciones entre equipos.

---

[⬆️ Volver al índice](#índice)