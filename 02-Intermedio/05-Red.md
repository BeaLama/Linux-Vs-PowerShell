# Red

## Introducción

La administración de red permite conocer el estado de las interfaces de red, comprobar la conectividad, diagnosticar problemas de comunicación y obtener información sobre la configuración del equipo.

Dominar estos comandos resulta fundamental para solucionar incidencias relacionadas con direcciones IP, DNS, puertas de enlace, rutas o conexiones entre equipos.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `ip addr` | `Get-NetIPAddress` |
| **Ejemplo** | `ip -4 addr` | `Get-NetIPAddress -AddressFamily IPv4` |

> 💡 **Diferencia clave** — 🐧 `ip addr` muestra toda la información de las interfaces de red. · 🪟 `Get-NetIPAddress` muestra únicamente las direcciones IP.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `ping <destino>` | `Test-Connection <destino>` |
| **Ejemplo** | `ping -c 4 google.com` | `Test-Connection google.com -Count 4` |

> 💡 **Diferencia clave** — 🐧 `ping` continúa enviando paquetes hasta detenerlo manualmente (`Ctrl + C`). · 🪟 `Test-Connection` envía cuatro solicitudes por defecto.

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

[⬆️ Volver al índice](#índice)

## Consultar la configuración DNS

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cat /etc/resolv.conf` | `Get-DnsClientServerAddress` |

**Ejemplo**
```bash
grep nameserver /etc/resolv.conf
```
```powershell
Get-DnsClientServerAddress `
-AddressFamily IPv4
```

> 💡 **Diferencia clave** — 🐧 La configuración suele encontrarse en `/etc/resolv.conf` o gestionarse mediante `systemd-resolved`. · 🪟 Cada adaptador mantiene su propia configuración DNS.

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

[⬆️ Volver al índice](#índice)

## Resolver nombres DNS

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `nslookup <dominio>` | `Resolve-DnsName <dominio>` |

**Ejemplo**
```bash
dig google.com MX
```
```powershell
Resolve-DnsName `
-Name google.com `
-Type MX
```

> 💡 **Diferencia clave** — 🐧 `nslookup` ofrece consultas básicas. · 🪟 `Resolve-DnsName` devuelve objetos con información detallada.

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

[⬆️ Volver al índice](#índice)

## Ver las conexiones de red activas

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `ss -tuln` | `Get-NetTCPConnection` |

**Ejemplo**
```bash
ss -tln
```
```powershell
Get-NetTCPConnection |
Where-Object {$_.State -eq "Listen"}
```

> 💡 **Diferencia clave** — 🐧 `ss` sustituye al antiguo `netstat` y ofrece un mejor rendimiento. · 🪟 `Get-NetTCPConnection` muestra únicamente conexiones TCP.

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

[⬆️ Volver al índice](#índice)

## Consultar la tabla de rutas

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `ip route` | `Get-NetRoute` |

**Ejemplo**
```bash
ip route | grep default
```
```powershell
Get-NetRoute `
| Where-Object {$_.DestinationPrefix -eq "0.0.0.0/0"}
```

> 💡 **Diferencia clave** — 🐧 `ip route` muestra la tabla de rutas gestionada por el kernel. · 🪟 `Get-NetRoute` consulta la tabla de rutas de Windows.

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

[⬆️ Volver al índice](#índice)

## Probar puertos de red

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `nc -zv <host> <puerto>` | `Test-NetConnection <host> -Port <puerto>` |

**Ejemplo**
```bash
nc -zv servidor.local 22
```
```powershell
Test-NetConnection `
servidor.local `
-Port 22
```

> 💡 **Diferencia clave** — 🐧 `nc` comprueba rápidamente si un puerto está abierto. · 🪟 `Test-NetConnection` muestra información mucho más detallada sobre la prueba.

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

[⬆️ Volver al índice](#índice)

## Ver la caché ARP

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `ip neigh` | `Get-NetNeighbor` |

**Ejemplo**
```bash
ip neigh | grep 192.168.1.1
```
```powershell
Get-NetNeighbor `
| Where-Object {$_.IPAddress -eq "192.168.1.1"}
```

> 💡 **Diferencia clave** — 🐧 `ip neigh` muestra la caché ARP gestionada por el kernel. · 🪟 `Get-NetNeighbor` consulta la tabla de vecinos de Windows.

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

[⬆️ Volver al índice](#índice)