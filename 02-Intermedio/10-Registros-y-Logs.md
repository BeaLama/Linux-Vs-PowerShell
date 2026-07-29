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

### Linux

```bash
journalctl
```

También puede utilizarse:

```bash
dmesg
```

para consultar los mensajes del núcleo (*kernel*).

**Descripción**

Permite consultar los registros almacenados por **systemd-journald**, que recopila información sobre:

- Arranque del sistema.
- Servicios.
- Errores.
- Eventos del sistema.
- Mensajes del kernel.
- Aplicaciones.

Por defecto, `journalctl` muestra todos los registros disponibles en orden cronológico.

---

### PowerShell

```powershell
Get-WinEvent
```

También puede utilizarse:

```powershell
Get-EventLog
```

> **Nota:** `Get-EventLog` está obsoleto y solo funciona con registros clásicos. Se recomienda utilizar `Get-WinEvent`.

**Descripción**

Permite consultar los registros almacenados por el **Visor de eventos de Windows**.

Los registros más habituales son:

- **Application**
- **System**
- **Security**
- **Setup**

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver los registros del sistema | `journalctl` | `Get-WinEvent` |
| Ver mensajes del kernel | `dmesg` | `Get-WinEvent -LogName System` |

---

### Ejemplos

**Mostrar todos los registros**

Linux

```bash
journalctl
```

PowerShell

```powershell
Get-WinEvent `
-LogName System
```

---

**Mostrar únicamente los registros del arranque actual**

Linux

```bash
journalctl -b
```

PowerShell

```powershell
Get-WinEvent `
-LogName System `
-MaxEvents 200
```

---

**Mostrar los mensajes del kernel**

Linux

```bash
dmesg
```

PowerShell

```powershell
Get-WinEvent `
-LogName System
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `journalctl` consulta el registro de **systemd-journald**. | `Get-WinEvent` consulta el Visor de eventos de Windows. |
| `dmesg` muestra únicamente mensajes del kernel. | Los eventos del sistema se encuentran principalmente en el registro **System**. |
| Los registros suelen almacenarse en el journal y/o en archivos de `/var/log`. | Los registros se almacenan en el Visor de eventos. |

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

> **💡 Consejo:** Tanto `journalctl` como `Get-WinEvent` pueden mostrar miles de eventos. En la práctica, lo habitual es combinar estos comandos con filtros (por servicio, fecha, nivel o palabra clave) para localizar rápidamente la información relevante.

---

[⬆️ Volver al índice](#índice)

## Consultar los registros de un servicio

### Linux

```bash
journalctl -u <servicio>
```

También puede utilizarse:

```bash
systemctl status <servicio>
```

para consultar el estado del servicio y los últimos registros asociados.

**Descripción**

Permite mostrar únicamente los registros generados por un servicio concreto gestionado por **systemd**.

Es especialmente útil para diagnosticar errores relacionados con servicios como:

- Apache
- Nginx
- SSH
- MySQL
- Docker

---

### PowerShell

```powershell
Get-WinEvent `
-LogName <registro>
```

También puede filtrarse por el proveedor del evento:

```powershell
Get-WinEvent `
-ProviderName <proveedor>
```

**Descripción**

Permite consultar los eventos generados por un registro o por un proveedor específico del Visor de eventos.

Muchos servicios y aplicaciones registran sus eventos utilizando un proveedor propio.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Consultar los registros de un servicio | `journalctl -u` | `Get-WinEvent -ProviderName` |
| Consultar el estado y últimos registros | `systemctl status` | `Get-WinEvent` |

---

### Ejemplos

**Consultar los registros del servicio SSH**

Linux

```bash
journalctl -u ssh
```

PowerShell

```powershell
Get-WinEvent `
-ProviderName OpenSSH
```

---

**Consultar los registros de Apache**

Linux

```bash
journalctl -u apache2
```

PowerShell

```powershell
Get-WinEvent `
-ProviderName IIS-W3SVC
```

---

**Consultar el estado del servicio Nginx**

Linux

```bash
systemctl status nginx
```

PowerShell

```powershell
Get-WinEvent `
-LogName Application
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Los registros pueden filtrarse directamente por el nombre del servicio. | Normalmente se filtran por el registro o por el proveedor del evento. |
| `systemctl status` muestra el estado del servicio junto con los últimos registros. | El estado del servicio suele consultarse con `Get-Service`, mientras que los eventos se consultan con `Get-WinEvent`. |
| Los registros proceden de **systemd-journald**. | Los registros proceden del Visor de eventos de Windows. |

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

> **💡 Consejo:** Cuando un servicio falla al iniciarse, el comando **`systemctl status`** suele ser el primer paso en Linux, ya que muestra tanto el estado del servicio como los últimos mensajes registrados. Si necesitas más detalle, utiliza **`journalctl -u`** para consultar todo su historial de eventos.

---

[⬆️ Volver al índice](#índice)

## Ver las últimas líneas de un registro

### Linux

```bash
tail <archivo.log>
```

También puede utilizarse:

```bash
tail -n <número> <archivo.log>
```

o, para seguir el registro en tiempo real:

```bash
tail -f <archivo.log>
```

**Descripción**

Permite visualizar las últimas líneas de un archivo de registro.

Es una de las herramientas más utilizadas para supervisar logs mientras un servicio está en funcionamiento o para comprobar errores recientes.

La opción `-f` mantiene el comando abierto y muestra automáticamente las nuevas entradas conforme se escriben en el archivo.

---

### PowerShell

```powershell
Get-Content <archivo.log> -Tail <número>
```

Para seguir el registro en tiempo real:

```powershell
Get-Content <archivo.log> `
-Tail <número> `
-Wait
```

**Descripción**

Permite mostrar las últimas líneas de un archivo de texto o registro.

Con el parámetro `-Wait`, PowerShell permanece a la espera de nuevas entradas, funcionando de forma similar a `tail -f` en Linux.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver las últimas líneas de un registro | `tail` | `Get-Content -Tail` |
| Seguir un registro en tiempo real | `tail -f` | `Get-Content -Wait` |

---

### Ejemplos

**Mostrar las últimas 20 líneas**

Linux

```bash
tail -n 20 /var/log/syslog
```

PowerShell

```powershell
Get-Content `
"C:\Logs\aplicacion.log" `
-Tail 20
```

---

**Seguir un registro en tiempo real**

Linux

```bash
tail -f /var/log/syslog
```

PowerShell

```powershell
Get-Content `
"C:\Logs\aplicacion.log" `
-Tail 20 `
-Wait
```

---

**Consultar el registro de autenticación**

Linux

```bash
tail /var/log/auth.log
```

PowerShell

```powershell
Get-Content `
"C:\Logs\auth.log" `
-Tail 10
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `tail` está diseñado específicamente para trabajar con archivos de texto y logs. | `Get-Content` puede utilizarse con cualquier archivo de texto. |
| `tail -f` muestra nuevas líneas en tiempo real. | `Get-Content -Wait` ofrece un comportamiento equivalente. |
| Muy utilizado para monitorizar servicios en ejecución. | Muy útil para supervisar archivos de log generados por aplicaciones o scripts. |

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

> **💡 Consejo:** `tail -f` (Linux) y `Get-Content -Wait` (PowerShell) son herramientas muy útiles durante tareas de diagnóstico. Permiten observar los registros en tiempo real mientras reinicias un servicio, ejecutas una aplicación o reproduces un error.

---

[⬆️ Volver al índice](#índice)

## Buscar información dentro de un registro

### Linux

```bash
grep <texto> <archivo.log>
```

También puede utilizarse:

```bash
grep -i <texto> <archivo.log>
```

o

```bash
grep -n <texto> <archivo.log>
```

**Descripción**

Permite buscar palabras, frases o patrones dentro de un archivo de registro.

Opciones habituales:

- `-i` → Ignora mayúsculas y minúsculas.
- `-n` → Muestra el número de línea donde aparece la coincidencia.
- `-r` → Busca de forma recursiva dentro de directorios.

---

### PowerShell

```powershell
Select-String `
-Path <archivo.log> `
-Pattern <texto>
```

También puede utilizarse:

```powershell
Select-String `
-Path <archivo.log> `
-Pattern <texto> `
-CaseSensitive
```

**Descripción**

Permite buscar texto o expresiones regulares dentro de uno o varios archivos.

Por defecto, `Select-String` no distingue entre mayúsculas y minúsculas.

Además de la línea encontrada, devuelve información adicional como:

- Archivo.
- Número de línea.
- Texto coincidente.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar texto en un registro | `grep` | `Select-String` |
| Ignorar mayúsculas/minúsculas | `grep -i` | Comportamiento predeterminado |
| Mostrar número de línea | `grep -n` | Propiedad `LineNumber` |

---

### Ejemplos

**Buscar la palabra "error"**

Linux

```bash
grep error /var/log/syslog
```

PowerShell

```powershell
Select-String `
-Path "C:\Logs\aplicacion.log" `
-Pattern "error"
```

---

**Buscar sin distinguir mayúsculas**

Linux

```bash
grep -i failed /var/log/auth.log
```

PowerShell

```powershell
Select-String `
-Path "C:\Logs\auth.log" `
-Pattern "failed"
```

---

**Mostrar el número de línea donde aparece una coincidencia**

Linux

```bash
grep -n ssh /var/log/auth.log
```

PowerShell

```powershell
Select-String `
-Path "C:\Logs\auth.log" `
-Pattern "ssh"
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `grep` trabaja principalmente con texto plano. | `Select-String` devuelve objetos con información adicional. |
| Las opciones se especifican mediante parámetros cortos (`-i`, `-n`, etc.). | Utiliza parámetros descriptivos (`-Pattern`, `-Path`, etc.). |
| Muy utilizado junto con tuberías (`\|`). | Se integra fácilmente con el resto del pipeline de PowerShell. |

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

> **💡 Consejo:** En la mayoría de incidencias, no es necesario leer un registro completo. Buscar palabras como **`error`**, **`failed`**, **`timeout`**, **`denied`** o **`warning`** suele ser el punto de partida más rápido para localizar la causa del problema.

---

[⬆️ Volver al índice](#índice)

## Consultar registros por fecha

### Linux

```bash
journalctl --since "<fecha>"
```

También puede utilizarse:

```bash
journalctl --since "<fecha>" --until "<fecha>"
```

**Descripción**

Permite filtrar los registros almacenados por **systemd-journald** según un intervalo de fechas y horas.

Es especialmente útil para investigar incidencias ocurridas en un momento concreto.

El formato de fecha admite distintas opciones, por ejemplo:

- `"today"`
- `"yesterday"`
- `"1 hour ago"`
- `"2026-07-29 08:00:00"`

---

### PowerShell

```powershell
Get-WinEvent `
-FilterHashtable @{
    LogName = "System"
    StartTime = <fecha>
}
```

También puede utilizarse un rango de fechas:

```powershell
Get-WinEvent `
-FilterHashtable @{
    LogName = "System"
    StartTime = <fecha_inicio>
    EndTime = <fecha_fin>
}
```

**Descripción**

Permite recuperar únicamente los eventos registrados dentro de un intervalo de tiempo.

El uso de `-FilterHashtable` es el método recomendado porque resulta mucho más eficiente que recuperar todos los eventos y filtrarlos posteriormente.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Consultar registros desde una fecha | `journalctl --since` | `Get-WinEvent -FilterHashtable` |
| Consultar registros entre dos fechas | `journalctl --since --until` | `Get-WinEvent -FilterHashtable` |

---

### Ejemplos

**Mostrar los registros de la última hora**

Linux

```bash
journalctl --since "1 hour ago"
```

PowerShell

```powershell
Get-WinEvent `
-FilterHashtable @{
    LogName = "System"
    StartTime = (Get-Date).AddHours(-1)
}
```

---

**Mostrar los registros de hoy**

Linux

```bash
journalctl --since today
```

PowerShell

```powershell
Get-WinEvent `
-FilterHashtable @{
    LogName = "System"
    StartTime = (Get-Date).Date
}
```

---

**Consultar un intervalo concreto**

Linux

```bash
journalctl `
--since "2026-07-29 08:00:00" `
--until "2026-07-29 10:00:00"
```

PowerShell

```powershell
Get-WinEvent `
-FilterHashtable @{
    LogName = "System"
    StartTime = Get-Date "2026-07-29 08:00"
    EndTime = Get-Date "2026-07-29 10:00"
}
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Utiliza los parámetros `--since` y `--until`. | Utiliza `StartTime` y `EndTime` dentro de `-FilterHashtable`. |
| Acepta expresiones naturales como `"today"` o `"1 hour ago"`. | Normalmente utiliza objetos `DateTime` obtenidos mediante `Get-Date`. |
| El filtrado lo realiza directamente `journalctl`. | El filtrado se realiza mediante el Visor de eventos utilizando `FilterHashtable`. |

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

> **💡 Consejo:** Cuando investigues una incidencia, empieza filtrando los registros por el intervalo de tiempo en el que ocurrió el problema. Reducir miles de eventos a unos pocos minutos suele ahorrar mucho tiempo durante el diagnóstico.

---

[⬆️ Volver al índice](#índice)

## Exportar registros

### Linux

Los registros pueden exportarse utilizando la redirección de salida (`>`) o herramientas como `tee`.

```bash
journalctl > registros.txt
```

También puede exportarse un registro concreto:

```bash
journalctl -u ssh > ssh.log
```

O guardar la salida mientras se muestra por pantalla:

```bash
journalctl | tee registros.txt
```

**Descripción**

Permite guardar los registros del sistema en un archivo para su posterior análisis, archivado o envío a otros administradores.

---

### PowerShell

```powershell
Get-WinEvent `
-LogName System |
Out-File "C:\Logs\System.log"
```

También puede exportarse en formato CSV:

```powershell
Get-WinEvent `
-LogName System |
Export-Csv "C:\Logs\System.csv" `
-NoTypeInformation
```

**Descripción**

Permite guardar los eventos del Visor de eventos en distintos formatos.

Los más habituales son:

- **TXT** (`Out-File`)
- **CSV** (`Export-Csv`)

El formato CSV resulta especialmente útil para analizar los eventos con Excel u otras herramientas de tratamiento de datos.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Exportar registros a un archivo de texto | `>` / `tee` | `Out-File` |
| Exportar registros a CSV | Mediante herramientas externas | `Export-Csv` |

---

### Ejemplos

**Exportar todos los registros**

Linux

```bash
journalctl > registros.txt
```

PowerShell

```powershell
Get-WinEvent `
-LogName System |
Out-File "C:\Logs\System.log"
```

---

**Exportar los registros de un servicio**

Linux

```bash
journalctl -u ssh > ssh.log
```

PowerShell

```powershell
Get-WinEvent `
-ProviderName OpenSSH |
Export-Csv "C:\Logs\OpenSSH.csv" `
-NoTypeInformation
```

---

**Guardar los registros mientras se muestran por pantalla**

Linux

```bash
journalctl | tee registros.txt
```

PowerShell

```powershell
Get-WinEvent `
-LogName System |
Tee-Object `
-FilePath "C:\Logs\System.log"
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Utiliza la redirección (`>`) o `tee` para guardar la salida. | Utiliza cmdlets específicos como `Out-File`, `Export-Csv` o `Tee-Object`. |
| La salida suele almacenarse como texto plano. | Puede exportarse fácilmente a TXT, CSV u otros formatos. |
| Muy utilizado para generar informes rápidos. | Muy útil para automatizar informes y análisis posteriores. |

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

> **💡 Consejo:** Antes de limpiar o rotar registros, exporta una copia si pueden ser necesarios para auditorías o investigaciones. Una vez eliminados, normalmente no podrán recuperarse.

---

[⬆️ Volver al índice](#índice)

## Limpiar registros

### Linux

Para reducir el tamaño del *journal* gestionado por **systemd-journald** pueden utilizarse los siguientes comandos:

```bash
sudo journalctl --vacuum-time=7d
```

o

```bash
sudo journalctl --vacuum-size=500M
```

También puede eliminarse todo el contenido del *journal* archivado:

```bash
sudo journalctl --vacuum-files=1
```

**Descripción**

Permite eliminar registros antiguos para liberar espacio en disco.

Las opciones más habituales son:

- `--vacuum-time` → Conserva únicamente los registros de un periodo determinado.
- `--vacuum-size` → Limita el tamaño máximo del *journal*.
- `--vacuum-files` → Conserva únicamente un número determinado de archivos de registro.

> **Importante:** Estos comandos solo afectan a los registros gestionados por **systemd-journald**.

---

### PowerShell

Para los registros clásicos:

```powershell
Clear-EventLog `
-LogName Application
```

También puede utilizarse la utilidad integrada de Windows:

```powershell
wevtutil cl System
```

**Descripción**

Permite eliminar el contenido de un registro del Visor de eventos.

- `Clear-EventLog` funciona únicamente con registros clásicos.
- `wevtutil` permite limpiar tanto registros clásicos como modernos.

> **⚠️ Advertencia:** Una vez eliminados, los eventos no pueden recuperarse salvo que exista una copia de seguridad.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Reducir el tamaño de los registros | `journalctl --vacuum-*` | No existe un equivalente directo |
| Limpiar un registro | No existe un único comando para todos los logs | `Clear-EventLog` / `wevtutil cl` |

---

### Ejemplos

**Conservar únicamente los registros de los últimos 7 días**

Linux

```bash
sudo journalctl --vacuum-time=7d
```

PowerShell

```powershell
# No existe un equivalente directo.
```

---

**Limitar el journal a 500 MB**

Linux

```bash
sudo journalctl --vacuum-size=500M
```

PowerShell

```powershell
# No existe un equivalente directo.
```

---

**Vaciar el registro del sistema**

Linux

```bash
# No existe un comando equivalente para todos los registros.
```

PowerShell

```powershell
wevtutil cl System
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Normalmente se eliminan registros antiguos según tiempo, tamaño o número de archivos. | Habitualmente se vacía un registro completo. |
| El *journal* puede gestionarse automáticamente mediante políticas de retención. | Cada registro debe limpiarse individualmente. |
| Los parámetros `--vacuum-*` permiten conservar parte del historial. | Al limpiar un registro se eliminan todos sus eventos. |

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

> **💡 Consejo:** En la mayoría de los sistemas no es recomendable eliminar los registros de forma habitual. Es preferible configurar una **política de retención** que elimine automáticamente los eventos más antiguos y conserve un historial suficiente para tareas de diagnóstico y auditoría.

---

[⬆️ Volver al índice](#índice)

## Ubicación de los registros

### Linux

En Linux, los registros del sistema suelen almacenarse en el directorio:

```text
/var/log
```

Dependiendo de la distribución y del servicio utilizado, los archivos de registro pueden variar.

Los registros gestionados por **systemd-journald** pueden consultarse mediante `journalctl`, aunque también pueden almacenarse de forma persistente en:

```text
/var/log/journal/
```

---

### PowerShell

Windows no almacena los registros como archivos de texto independientes.

La mayoría de los eventos se guardan en el **Visor de eventos** (*Event Viewer*), cuyos archivos se encuentran normalmente en:

```text
C:\Windows\System32\winevt\Logs\
```

Los registros utilizan el formato:

```text
.evtx
```

Estos archivos pueden consultarse mediante:

```powershell
Get-WinEvent
```

o desde la consola **Visor de eventos**.

---

### Archivos de registro más importantes en Linux

| Archivo o directorio | Descripción |
|----------------------|-------------|
| `/var/log/syslog` | Registro general del sistema (Debian/Ubuntu). |
| `/var/log/messages` | Registro general del sistema (RHEL/CentOS). |
| `/var/log/auth.log` | Autenticación e inicios de sesión (Debian/Ubuntu). |
| `/var/log/secure` | Autenticación e inicios de sesión (RHEL/CentOS). |
| `/var/log/kern.log` | Mensajes del kernel. |
| `/var/log/dmesg` | Mensajes generados durante el arranque. |
| `/var/log/boot.log` | Registro del proceso de arranque. |
| `/var/log/apache2/` | Registros del servidor Apache. |
| `/var/log/nginx/` | Registros del servidor Nginx. |
| `/var/log/mysql/` | Registros del servidor MySQL/MariaDB. |
| `/var/log/journal/` | Journal persistente de systemd (si está habilitado). |

---

### Registros más importantes en Windows

| Registro | Descripción |
|----------|-------------|
| **Application** | Eventos generados por aplicaciones instaladas. |
| **System** | Eventos del sistema operativo, controladores y servicios. |
| **Security** | Eventos de autenticación, permisos y auditoría. |
| **Setup** | Instalaciones, actualizaciones y configuración del sistema. |
| **Forwarded Events** | Eventos recibidos desde otros equipos. |
| **Windows PowerShell** | Ejecución de scripts y cmdlets de PowerShell. |

---

### Equivalencia

| Linux | PowerShell |
|--------|------------|
| `/var/log` | `C:\Windows\System32\winevt\Logs\` |
| Archivos `.log` | Archivos `.evtx` |
| `journalctl` | `Get-WinEvent` |

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Los registros suelen almacenarse como archivos de texto o en el *journal*. | Los registros se almacenan en archivos binarios `.evtx`. |
| Pueden consultarse directamente con herramientas como `cat`, `less` o `tail`. | Deben consultarse mediante el Visor de eventos o `Get-WinEvent`. |
| Cada servicio puede generar sus propios archivos de log. | La mayoría de los eventos se centralizan en el Visor de eventos. |

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

> **💡 Consejo:** Uno de los errores más comunes al buscar un problema es consultar el registro equivocado. Antes de empezar a analizar eventos, identifica si la incidencia está relacionada con el sistema, una aplicación, un servicio o la autenticación del usuario. Esto reducirá enormemente el tiempo de diagnóstico.

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

### Comandos más utilizados

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver registros | `journalctl` | `Get-WinEvent` |
| Ver registros de un servicio | `journalctl -u` | `Get-WinEvent -ProviderName` |
| Ver las últimas líneas | `tail` | `Get-Content -Tail` |
| Monitorizar un log en tiempo real | `tail -f` | `Get-Content -Wait` |
| Buscar texto | `grep` | `Select-String` |
| Filtrar por fecha | `journalctl --since` | `Get-WinEvent -FilterHashtable` |
| Exportar registros | `>` / `tee` | `Out-File` / `Export-Csv` |
| Limpiar registros | `journalctl --vacuum-*` | `wevtutil cl` |

---

### Flujo de trabajo recomendado

Cuando necesites investigar una incidencia, el procedimiento habitual suele ser:

1. Identificar el servicio o componente afectado.
2. Consultar los registros correspondientes.
3. Filtrar los eventos por fecha, servicio o palabra clave.
4. Revisar los errores o advertencias relacionados con la incidencia.
5. Exportar los registros si es necesario compartirlos o archivarlos.
6. Aplicar la solución y comprobar nuevamente los registros para verificar que el problema ha desaparecido.

---

### Diferencias clave

| Linux | Windows / PowerShell |
|--------|----------------------|
| Los registros pueden almacenarse en archivos de texto y en el *journal* de systemd. | Los eventos se almacenan principalmente en archivos binarios `.evtx`. |
| Herramientas como `journalctl`, `grep` y `tail` permiten analizar rápidamente los registros. | `Get-WinEvent` ofrece acceso estructurado a los eventos del Visor de eventos. |
| Cada servicio puede disponer de sus propios archivos de log en `/var/log`. | La mayoría de los eventos se centralizan en registros como **Application**, **System** y **Security**. |
| Es muy habitual combinar varios comandos mediante tuberías (`|`). | Los cmdlets devuelven objetos que pueden filtrarse y procesarse fácilmente mediante el pipeline de PowerShell. |

---

[⬆️ Volver al índice](#índice)