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
- [Resumen de equivalencias](#resumen-de-equivalencias)

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

### Buenas prácticas

- Consulta primero los registros del sistema cuando investigues un problema.
- Revisa los mensajes del kernel tras errores de hardware o controladores.
- Filtra los registros para reducir la cantidad de información mostrada.
- Conserva los registros importantes antes de realizar tareas de mantenimiento.

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

### Buenas prácticas

- Consulta primero los registros del servicio antes de reiniciarlo.
- Si un servicio no inicia correctamente, revisa los últimos eventos registrados.
- Combina la consulta de registros con la comprobación del estado del servicio.
- Filtra únicamente el servicio que estás investigando para reducir la cantidad de información mostrada.

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

### Buenas prácticas

- Consulta únicamente las últimas líneas cuando investigues un problema reciente.
- Utiliza el modo en tiempo real para supervisar servicios mientras realizas pruebas.
- Evita abrir archivos de registro muy grandes completos si solo necesitas los eventos más recientes.
- Combina este comando con herramientas de búsqueda cuando necesites localizar errores específicos.

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

### Buenas prácticas

- Utiliza palabras clave concretas para reducir el número de resultados.
- Busca términos como `error`, `failed`, `warning` o `critical` al investigar incidencias.
- Combina las búsquedas con filtros por fecha o servicio para localizar problemas más rápidamente.
- Si el registro es muy grande, limita previamente el contenido antes de realizar la búsqueda.

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

### Buenas prácticas

- Filtra siempre los registros por fecha cuando investigues una incidencia concreta.
- Utiliza intervalos lo más reducidos posible para facilitar el análisis.
- Combina el filtro por fecha con filtros por servicio o por texto cuando sea necesario.
- Comprueba la hora del sistema antes de analizar los registros para evitar confusiones.

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

### Buenas prácticas

- Exporta los registros antes de realizar cambios importantes en el sistema.
- Utiliza nombres descriptivos para identificar fácilmente los archivos generados.
- Si los registros contienen información sensible, almacénalos en ubicaciones seguras.
- El formato CSV facilita el análisis y filtrado de grandes cantidades de eventos.

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

### Buenas prácticas

- Exporta los registros importantes antes de eliminarlos.
- Evita limpiar los registros durante una investigación o auditoría.
- Configura políticas de retención para evitar que los registros ocupen demasiado espacio.
- Conserva los registros de seguridad durante el tiempo establecido por la política de la organización.

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

### Buenas prácticas

- Familiarízate con la ubicación de los registros más utilizados de tu sistema.
- Consulta primero el registro adecuado según el tipo de incidencia (autenticación, sistema, aplicación, etc.).
- Evita modificar manualmente los archivos de registro.
- Controla el espacio ocupado por los logs, especialmente en servidores con alta actividad.

---

### Comandos relacionados

- [Ver los registros del sistema](#ver-los-registros-del-sistema)
- [Consultar los registros de un servicio](#consultar-los-registros-de-un-servicio)
- [Exportar registros](#exportar-registros)

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver los registros del sistema | `journalctl` | `Get-WinEvent` |
| Ver mensajes del kernel | `dmesg` | `Get-WinEvent -LogName System` |
| Consultar los registros de un servicio | `journalctl -u` | `Get-WinEvent -ProviderName` |
| Ver las últimas líneas de un registro | `tail` | `Get-Content -Tail` |
| Seguir un registro en tiempo real | `tail -f` | `Get-Content -Wait` |
| Buscar información dentro de un registro | `grep` | `Select-String` |
| Consultar registros por fecha | `journalctl --since --until` | `Get-WinEvent -FilterHashtable` |
| Exportar registros | `>` / `tee` | `Out-File` / `Export-Csv` |
| Limpiar registros | `journalctl --vacuum-*` | `Clear-EventLog` / `wevtutil cl` |

---

### Buenas prácticas generales

- Consulta siempre los registros antes de reiniciar un servicio o realizar cambios en el sistema.
- Filtra los registros por servicio, fecha o palabra clave para reducir la cantidad de información.
- Exporta los registros importantes antes de eliminarlos o realizar tareas de mantenimiento.
- Conserva un historial suficiente para facilitar auditorías e investigaciones.
- Supervisa periódicamente el tamaño de los registros para evitar problemas de espacio en disco.
- Documenta cualquier incidencia relevante junto con los registros asociados.

---

[⬆️ Volver al índice](#índice)