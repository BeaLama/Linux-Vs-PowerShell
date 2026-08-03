# Servicios

## Introducción

Un servicio es un programa que se ejecuta en segundo plano para proporcionar una función al sistema operativo o a otras aplicaciones.

A diferencia de los procesos interactivos, los servicios pueden iniciarse automáticamente durante el arranque del sistema y continuar funcionando sin intervención del usuario.

La administración de servicios es una tarea fundamental para mantener la disponibilidad y el correcto funcionamiento de servidores y equipos.

---

## Índice

- [Listar servicios](#listar-servicios)
- [Buscar un servicio](#buscar-un-servicio)
- [Consultar el estado de un servicio](#consultar-el-estado-de-un-servicio)
- [Iniciar un servicio](#iniciar-un-servicio)
- [Detener un servicio](#detener-un-servicio)
- [Reiniciar un servicio](#reiniciar-un-servicio)
- [Configurar el inicio automático](#configurar-el-inicio-automático)

---

## Listar servicios

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `systemctl list-units --type=service` | `Get-Service` |

**Ejemplo**
```bash
systemctl list-units --type=service --state=running
```
```powershell
Get-Service |
Where-Object {$_.Status -eq "Running"}
```

> 💡 **Diferencia clave** — 🐧 `systemctl` administra los servicios mediante **systemd**. · 🪟 `Get-Service` consulta el Administrador de Control de Servicios (SCM) de Windows.

---

### Comandos relacionados

- [Buscar un servicio](#buscar-un-servicio)
- [Consultar el estado de un servicio](#consultar-el-estado-de-un-servicio)
- [Iniciar un servicio](#iniciar-un-servicio)

---

[⬆️ Volver al índice](#índice)

## Buscar un servicio

**Sintaxis**
```bash
systemctl list-units --type=service | grep <servicio>
```
```powershell
Get-Service <servicio>
```

> 💡 **Diferencia clave** — 🐧 Utiliza `grep` para filtrar la salida de `systemctl`. · 🪟 Puede buscar directamente por nombre mediante `Get-Service`.

---

### Comandos relacionados

- [Listar servicios](#listar-servicios)
- [Consultar el estado de un servicio](#consultar-el-estado-de-un-servicio)
- [Iniciar un servicio](#iniciar-un-servicio)

---

[⬆️ Volver al índice](#índice)

## Consultar el estado de un servicio

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `systemctl status <servicio>` | `Get-Service <servicio>` |
| **Ejemplo** | `systemctl status cups` | `Get-Service Spooler` |

> 💡 **Diferencia clave** — 🐧 `systemctl status` muestra información muy detallada del servicio. · 🪟 `Get-Service` muestra información básica del servicio.

---

### Comandos relacionados

- [Buscar un servicio](#buscar-un-servicio)
- [Iniciar un servicio](#iniciar-un-servicio)
- [Detener un servicio](#detener-un-servicio)

---

[⬆️ Volver al índice](#índice)

## Iniciar un servicio

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo systemctl start <servicio>` | `Start-Service <servicio>` |
| **Ejemplo** | `sudo systemctl start cups` | `Start-Service Spooler` |

> 💡 **Diferencia clave** — 🐧 `systemctl start` inicia el servicio mediante **systemd**. · 🪟 `Start-Service` solicita al Administrador de Control de Servicios (SCM) que inicie el servicio.

---

### Comandos relacionados

- [Consultar el estado de un servicio](#consultar-el-estado-de-un-servicio)
- [Detener un servicio](#detener-un-servicio)
- [Reiniciar un servicio](#reiniciar-un-servicio)

---

[⬆️ Volver al índice](#índice)

## Detener un servicio

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo systemctl stop <servicio>` | `Stop-Service <servicio>` |
| **Ejemplo** | `sudo systemctl stop cups` | `Stop-Service Spooler` |

> 💡 **Diferencia clave** — 🐧 `systemctl stop` detiene el servicio mediante **systemd**. · 🪟 `Stop-Service` solicita al Administrador de Control de Servicios (SCM) que detenga el servicio.

---

### Comandos relacionados

- [Consultar el estado de un servicio](#consultar-el-estado-de-un-servicio)
- [Iniciar un servicio](#iniciar-un-servicio)
- [Reiniciar un servicio](#reiniciar-un-servicio)

---

[⬆️ Volver al índice](#índice)

## Reiniciar un servicio

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo systemctl restart <servicio>` | `Restart-Service <servicio>` |
| **Ejemplo** | `sudo systemctl restart cups` | `Restart-Service Spooler` |

> 💡 **Diferencia clave** — 🐧 `restart` reinicia completamente el servicio. · 🪟 `Restart-Service` detiene e inicia nuevamente el servicio.

---

### Comandos relacionados

- [Consultar el estado de un servicio](#consultar-el-estado-de-un-servicio)
- [Iniciar un servicio](#iniciar-un-servicio)
- [Detener un servicio](#detener-un-servicio)

---

[⬆️ Volver al índice](#índice)

## Configurar el inicio automático

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo systemctl enable <servicio>` | `Set-Service -Name <servicio> -StartupType Automatic` |
| **Ejemplo** | `sudo systemctl disable cups` | `Set-Service -Name Spooler -StartupType Disabled` |

> 💡 **Diferencia clave** — 🐧 `enable` y `disable` controlan el inicio automático del servicio. · 🪟 `Set-Service` permite configurar varios tipos de inicio.

---

### Comandos relacionados

- [Iniciar un servicio](#iniciar-un-servicio)
- [Detener un servicio](#detener-un-servicio)
- [Reiniciar un servicio](#reiniciar-un-servicio)

---

[⬆️ Volver al índice](#índice)
