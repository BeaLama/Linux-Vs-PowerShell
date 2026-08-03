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
- [Resumen de equivalencias](#resumen-de-equivalencias)

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

### Buenas prácticas

- Comprueba periódicamente qué servicios se encuentran en ejecución.
- Identifica los servicios detenidos antes de iniciar uno manualmente.
- No detengas servicios críticos del sistema sin conocer su función.
- Utiliza filtros para localizar rápidamente la información necesaria.

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

### Buenas prácticas

- Utiliza el nombre exacto del servicio siempre que sea posible.
- Si desconoces el nombre completo, realiza una búsqueda parcial.
- Comprueba el estado del servicio antes de iniciarlo o detenerlo.
- Utiliza `DisplayName` cuando conozcas el nombre visible del servicio pero no su nombre interno.

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

### Buenas prácticas

- Comprueba siempre el estado del servicio antes de iniciarlo o detenerlo.
- Si un servicio no se inicia correctamente, revisa la información mostrada por `systemctl status`.
- En PowerShell, consulta también el tipo de inicio cuando un servicio no arranque automáticamente.
- Si un servicio falla repetidamente, revisa los registros del sistema para identificar la causa.

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

### Buenas prácticas

- Comprueba que el servicio está detenido antes de iniciarlo.
- Verifica que el servicio ha arrancado correctamente después de ejecutarlo.
- Si el servicio no inicia, consulta su estado y los registros del sistema para identificar el problema.
- Evita iniciar servicios innecesarios que puedan consumir recursos o aumentar la superficie de ataque.

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

### Buenas prácticas

- Comprueba que el servicio está en ejecución antes de detenerlo.
- Verifica que otros servicios o aplicaciones no dependan de él.
- Comprueba el estado del servicio después de detenerlo para confirmar que la operación se ha realizado correctamente.
- Evita detener servicios críticos del sistema, ya que pueden afectar al funcionamiento del equipo o de la red.

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

### Buenas prácticas

- Utiliza `reload` cuando el servicio lo admita y solo sea necesario aplicar cambios de configuración.
- Reinicia un servicio únicamente cuando sea necesario, ya que puede interrumpir temporalmente su funcionamiento.
- Comprueba el estado del servicio después del reinicio para confirmar que se ha iniciado correctamente.
- Si el servicio no vuelve a iniciarse, revisa los registros del sistema antes de volver a intentarlo.

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

### Buenas prácticas

- Configura como automáticos únicamente los servicios necesarios.
- Deshabilita los servicios que no vayan a utilizarse para reducir el consumo de recursos y la superficie de ataque.
- Antes de deshabilitar un servicio, comprueba que ninguna aplicación dependa de él.
- Verifica el tipo de inicio después de realizar cualquier cambio.

---

### Comandos relacionados

- [Iniciar un servicio](#iniciar-un-servicio)
- [Detener un servicio](#detener-un-servicio)
- [Reiniciar un servicio](#reiniciar-un-servicio)

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|--------|--------|------------|
| Listar servicios | `systemctl list-units --type=service` | `Get-Service` |
| Buscar un servicio | `systemctl \| grep` | `Get-Service` / `Where-Object` |
| Consultar el estado de un servicio | `systemctl status` | `Get-Service` |
| Iniciar un servicio | `systemctl start` | `Start-Service` |
| Detener un servicio | `systemctl stop` | `Stop-Service` |
| Reiniciar un servicio | `systemctl restart` | `Restart-Service` |
| Recargar la configuración de un servicio | `systemctl reload` | No existe un equivalente directo |
| Habilitar el inicio automático | `systemctl enable` | `Set-Service -StartupType Automatic` |
| Deshabilitar el inicio automático | `systemctl disable` | `Set-Service -StartupType Disabled` |

---

### Buenas prácticas generales

- Comprueba siempre el estado del servicio antes de iniciarlo, detenerlo o reiniciarlo.
- Evita detener servicios críticos del sistema sin conocer su función.
- Configura como automáticos únicamente los servicios necesarios.
- Revisa periódicamente los servicios que se inician durante el arranque del sistema.
- Utiliza `reload` en lugar de `restart` cuando solo necesites aplicar cambios de configuración y el servicio lo permita.
- Después de cualquier modificación, verifica que el servicio ha quedado en el estado esperado.

---

### Comandos más utilizados

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Listar servicios | `systemctl list-units --type=service` | `Get-Service` |
| Ver el estado de un servicio | `systemctl status ssh` | `Get-Service sshd` |
| Iniciar un servicio | `systemctl start ssh` | `Start-Service sshd` |
| Detener un servicio | `systemctl stop ssh` | `Stop-Service sshd` |
| Reiniciar un servicio | `systemctl restart ssh` | `Restart-Service sshd` |
| Habilitar inicio automático | `systemctl enable ssh` | `Set-Service -Name sshd -StartupType Automatic` |

---

[⬆️ Volver al índice](#índice)