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

---

## Ver la configuración de red

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `ip addr` | `Get-NetIPAddress` |
| **Ejemplo** | `ip -4 addr` | `Get-NetIPAddress -AddressFamily IPv4` |

> 💡 **Diferencia clave** — 🐧 `ip addr` muestra toda la información de las interfaces de red. · 🪟 `Get-NetIPAddress` muestra únicamente las direcciones IP.

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

### Comandos relacionados

- [Ver la configuración de red](#ver-la-configuración-de-red)
- [Comprobar la conectividad (Ping)](#comprobar-la-conectividad-ping)
- [Ver las conexiones de red activas](#ver-las-conexiones-de-red-activas)

---

[⬆️ Volver al índice](#índice)