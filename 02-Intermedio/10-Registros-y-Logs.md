# Registros y Logs

## Introducción

Los registros (logs) almacenan información sobre la actividad del sistema, los servicios, las aplicaciones y los usuarios.

Son una herramienta fundamental para:

- Diagnosticar errores.
- Investigar incidentes.
- Auditar la actividad del sistema.
- Supervisar servicios.
- Detectar problemas de seguridad.

En Linux, los registros suelen gestionarse mediante **systemd-journald** y archivos ubicados en **/var/log**, mientras que Windows utiliza principalmente el **Visor de eventos**, accesible desde PowerShell mediante cmdlets específicos.

---

## Índice

- [Ver los registros del sistema](#ver-los-registros-del-sistema)
- [Consultar los registros de un servicio](#consultar-los-registros-de-un-servicio)
- [Ver las últimas líneas de un registro](#ver-las-últimas-líneas-de-un-registro)
- [Buscar información dentro de un registro](#buscar-información-dentro-de-un-registro)
- [Consultar registros por fecha](#consultar-registros-por-fecha)
- [Exportar registros](#exportar-registros)
- [Limpiar registros](#limpiar-registros)
- [Ubicación de los registros](#ubicación-de-los-registros)

---

## Ver los registros del sistema

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `journalctl` | `Get-WinEvent` |

**Ejemplo**
```bash
journalctl -b
```
```powershell
Get-WinEvent `
-LogName System `
-MaxEvents 200
```

> 💡 **Diferencia clave** — 🐧 `journalctl` consulta el registro de **systemd-journald**. · 🪟 `Get-WinEvent` consulta el Visor de eventos de Windows.

---

### Comandos relacionados

- [Consultar los registros de un servicio](#consultar-los-registros-de-un-servicio)
- [Consultar registros por fecha](#consultar-registros-por-fecha)
- [Buscar información dentro de un registro](#buscar-información-dentro-de-un-registro)

---

[⬆️ Volver al índice](#índice)

## Consultar los registros de un servicio

**Sintaxis**
```bash
journalctl -u <servicio>
```
```powershell
Get-WinEvent `
-LogName <registro>
```

> 💡 **Diferencia clave** — 🐧 Los registros pueden filtrarse directamente por el nombre del servicio. · 🪟 Normalmente se filtran por el registro o por el proveedor del evento.

---

### Comandos relacionados

- [Ver los registros del sistema](#ver-los-registros-del-sistema)
- [Consultar registros por fecha](#consultar-registros-por-fecha)
- [Buscar información dentro de un registro](#buscar-información-dentro-de-un-registro)

---

[⬆️ Volver al índice](#índice)

## Ver las últimas líneas de un registro

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `tail <archivo.log>` | `Get-Content <archivo.log> -Tail <número>` |

**Ejemplo**
```bash
tail -f /var/log/syslog
```
```powershell
Get-Content `
"C:\Logs\aplicacion.log" `
-Tail 20 `
-Wait
```

> 💡 **Diferencia clave** — 🐧 `tail` está diseñado específicamente para trabajar con archivos de texto y logs. · 🪟 `Get-Content` puede utilizarse con cualquier archivo de texto.

---

### Comandos relacionados

- [Buscar información dentro de un registro](#buscar-información-dentro-de-un-registro)
- [Consultar los registros de un servicio](#consultar-los-registros-de-un-servicio)
- [Consultar registros por fecha](#consultar-registros-por-fecha)

---

[⬆️ Volver al índice](#índice)

## Buscar información dentro de un registro

**Sintaxis**
```bash
grep <texto> <archivo.log>
```
```powershell
Select-String `
-Path <archivo.log> `
-Pattern <texto>
```

> 💡 **Diferencia clave** — 🐧 `grep` trabaja principalmente con texto plano. · 🪟 `Select-String` devuelve objetos con información adicional.

---

### Comandos relacionados

- [Ver las últimas líneas de un registro](#ver-las-últimas-líneas-de-un-registro)
- [Consultar registros por fecha](#consultar-registros-por-fecha)
- [Consultar los registros de un servicio](#consultar-los-registros-de-un-servicio)

---

[⬆️ Volver al índice](#índice)

## Consultar registros por fecha

**Sintaxis**
```bash
journalctl --since "<fecha>"
```
```powershell
Get-WinEvent `
-FilterHashtable @{
    LogName = "System"
    StartTime = <fecha>
}
```

> 💡 **Diferencia clave** — 🐧 Utiliza los parámetros `--since` y `--until`. · 🪟 Utiliza `StartTime` y `EndTime` dentro de `-FilterHashtable`.

---

### Comandos relacionados

- [Ver los registros del sistema](#ver-los-registros-del-sistema)
- [Buscar información dentro de un registro](#buscar-información-dentro-de-un-registro)
- [Consultar los registros de un servicio](#consultar-los-registros-de-un-servicio)

---

[⬆️ Volver al índice](#índice)

## Exportar registros

**Sintaxis**
```bash
journalctl > registros.txt
```
```powershell
Get-WinEvent `
-LogName System |
Out-File "C:\Logs\System.log"
```

> 💡 **Diferencia clave** — 🐧 Utiliza la redirección (`>`) o `tee` para guardar la salida. · 🪟 Utiliza cmdlets específicos como `Out-File`, `Export-Csv` o `Tee-Object`.

---

### Comandos relacionados

- [Ver los registros del sistema](#ver-los-registros-del-sistema)
- [Buscar información dentro de un registro](#buscar-información-dentro-de-un-registro)
- [Limpiar registros](#limpiar-registros)

---

[⬆️ Volver al índice](#índice)

## Limpiar registros

**Sintaxis**
```bash
sudo journalctl --vacuum-time=7d
```
```powershell
Clear-EventLog `
-LogName Application
```

> 💡 **Diferencia clave** — 🐧 Normalmente se eliminan registros antiguos según tiempo, tamaño o número de archivos. · 🪟 Habitualmente se vacía un registro completo.

---

### Comandos relacionados

- [Exportar registros](#exportar-registros)
- [Consultar registros por fecha](#consultar-registros-por-fecha)
- [Ver los registros del sistema](#ver-los-registros-del-sistema)

---

[⬆️ Volver al índice](#índice)

## Ubicación de los registros

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | *(no aplica)* | `Get-WinEvent` |
| **Ejemplo** | *(no aplica)* | *(no aplica)* |

> 💡 **Diferencia clave** — 🐧 Los registros suelen almacenarse como archivos de texto o en el *journal*. · 🪟 Los registros se almacenan en archivos binarios `.evtx`.

---

### Comandos relacionados

- [Ver los registros del sistema](#ver-los-registros-del-sistema)
- [Consultar los registros de un servicio](#consultar-los-registros-de-un-servicio)
- [Exportar registros](#exportar-registros)

---

[⬆️ Volver al índice](#índice)