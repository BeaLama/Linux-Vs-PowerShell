# Servicios

## Introducción

Un servicio es un programa que se ejecuta en segundo plano para proporcionar una función al sistema operativo o a otras aplicaciones.

A diferencia de los procesos interactivos, los servicios pueden iniciarse automáticamente durante el arranque del sistema y continuar funcionando sin intervención del usuario.

La administración de servicios es una tarea fundamental para mantener la disponibilidad y el correcto funcionamiento de servidores y equipos.

En este capítulo aprenderás a consultar, iniciar, detener, reiniciar y administrar servicios tanto en Linux como en PowerShell.

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

### Linux

```bash
systemctl list-units --type=service
```

También puede utilizarse:

```bash
systemctl --type=service
```

**Descripción**

Muestra todos los servicios gestionados por **systemd** que se encuentran cargados en el sistema.

La salida incluye información como:

- Nombre del servicio.
- Estado de carga.
- Estado de ejecución.
- Descripción.

---

### PowerShell

```powershell
Get-Service
```

**Descripción**

Muestra todos los servicios instalados en el sistema, indicando información como:

- Nombre del servicio.
- Nombre para mostrar.
- Estado.
- Tipo de inicio.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Listar servicios | `systemctl list-units --type=service` | `Get-Service` |

---

### Ejemplos

**Mostrar todos los servicios**

Linux

```bash
systemctl list-units --type=service
```

PowerShell

```powershell
Get-Service
```

---

**Mostrar únicamente los servicios en ejecución**

Linux

```bash
systemctl list-units --type=service --state=running
```

PowerShell

```powershell
Get-Service |
Where-Object {$_.Status -eq "Running"}
```

---

**Mostrar únicamente los servicios detenidos**

Linux

```bash
systemctl list-units --type=service --state=inactive
```

PowerShell

```powershell
Get-Service |
Where-Object {$_.Status -eq "Stopped"}
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `systemctl` administra los servicios mediante **systemd**. | `Get-Service` consulta el Administrador de Control de Servicios (SCM) de Windows. |
| Puede filtrar directamente por estado utilizando `--state`. | Habitualmente se utiliza `Where-Object` para filtrar resultados. |
| La salida es texto estructurado. | La salida son objetos que pueden procesarse mediante la tubería. |

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

### Linux

```bash
systemctl list-units --type=service | grep <servicio>
```

También puede utilizarse:

```bash
systemctl | grep <servicio>
```

**Descripción**

Permite localizar uno o varios servicios cuyo nombre coincida con el texto especificado.

Generalmente se utiliza junto con `grep` para filtrar la salida de `systemctl`.

---

### PowerShell

```powershell
Get-Service <servicio>
```

También puede utilizarse:

```powershell
Get-Service | Where-Object {$_.Name -like "*<servicio>*"}
```

o

```powershell
Get-Service | Where-Object {$_.DisplayName -like "*<servicio>*"}
```

**Descripción**

Permite buscar servicios por su nombre interno (`Name`) o por su nombre descriptivo (`DisplayName`).

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar un servicio | `systemctl \| grep` | `Get-Service` / `Where-Object` |

---

### Ejemplos

**Buscar el servicio SSH**

Linux

```bash
systemctl list-units --type=service | grep ssh
```

PowerShell

```powershell
Get-Service sshd
```

---

**Buscar el servicio de impresión**

Linux

```bash
systemctl list-units --type=service | grep cups
```

PowerShell

```powershell
Get-Service Spooler
```

---

**Buscar todos los servicios relacionados con SQL**

Linux

```bash
systemctl list-units --type=service | grep sql
```

PowerShell

```powershell
Get-Service |
Where-Object {$_.DisplayName -like "*SQL*"}
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Utiliza `grep` para filtrar la salida de `systemctl`. | Puede buscar directamente por nombre mediante `Get-Service`. |
| La búsqueda se realiza sobre texto. | La búsqueda puede realizarse sobre las propiedades `Name` o `DisplayName`. |
| La salida continúa siendo texto. | La salida son objetos que pueden seguir procesándose mediante la tubería. |

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

### Linux

```bash
systemctl status <servicio>
```

**Descripción**

Muestra información detallada sobre un servicio concreto, incluyendo:

- Estado actual.
- Si está activo o detenido.
- Fecha y hora del último inicio.
- PID principal.
- Consumo de recursos.
- Mensajes recientes del registro relacionados con el servicio.

---

### PowerShell

```powershell
Get-Service <servicio>
```

También puede utilizarse:

```powershell
Get-Service <servicio> | Select-Object Name, Status, StartType
```

**Descripción**

Permite consultar el estado actual de un servicio.

La información más habitual incluye:

- Nombre del servicio.
- Estado (`Running`, `Stopped`, etc.).
- Tipo de inicio.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Consultar el estado de un servicio | `systemctl status` | `Get-Service` |

---

### Ejemplos

**Consultar el estado del servicio SSH**

Linux

```bash
systemctl status ssh
```

PowerShell

```powershell
Get-Service sshd
```

---

**Consultar el estado del servicio de impresión**

Linux

```bash
systemctl status cups
```

PowerShell

```powershell
Get-Service Spooler
```

---

**Mostrar únicamente el estado y el tipo de inicio**

Linux

```bash
systemctl status ssh
```

PowerShell

```powershell
Get-Service Spooler |
Select-Object Name, Status, StartType
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `systemctl status` muestra información muy detallada del servicio. | `Get-Service` muestra información básica del servicio. |
| Incluye registros recientes del servicio. | Para obtener más información suele combinarse con otros cmdlets como `Get-CimInstance`. |
| Permite comprobar rápidamente si el servicio está funcionando correctamente. | Devuelve un objeto que puede utilizarse en otros comandos. |

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

### Linux

```bash
sudo systemctl start <servicio>
```

**Descripción**

Inicia un servicio que se encuentra detenido.

Si el servicio ya está en ejecución, el comando no produce ningún cambio.

---

### PowerShell

```powershell
Start-Service <servicio>
```

**Descripción**

Inicia un servicio detenido.

Si el servicio ya está iniciado, PowerShell mostrará un mensaje indicando que el servicio ya se encuentra en ejecución.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Iniciar un servicio | `systemctl start` | `Start-Service` |

---

### Ejemplos

**Iniciar el servicio SSH**

Linux

```bash
sudo systemctl start ssh
```

PowerShell

```powershell
Start-Service sshd
```

---

**Iniciar el servicio de impresión**

Linux

```bash
sudo systemctl start cups
```

PowerShell

```powershell
Start-Service Spooler
```

---

**Comprobar que el servicio se ha iniciado correctamente**

Linux

```bash
systemctl status ssh
```

PowerShell

```powershell
Get-Service sshd
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `systemctl start` inicia el servicio mediante **systemd**. | `Start-Service` solicita al Administrador de Control de Servicios (SCM) que inicie el servicio. |
| Generalmente requiere privilegios de administrador (`sudo`). | Normalmente requiere ejecutar PowerShell como administrador. |
| Es habitual comprobar el resultado con `systemctl status`. | Es habitual comprobar el resultado con `Get-Service`. |

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

### Linux

```bash
sudo systemctl stop <servicio>
```

**Descripción**

Detiene un servicio que se encuentra en ejecución.

Si el servicio ya está detenido, el comando no produce ningún cambio.

---

### PowerShell

```powershell
Stop-Service <servicio>
```

**Descripción**

Detiene un servicio en ejecución.

Si el servicio ya está detenido, PowerShell mostrará un mensaje indicando que el servicio no está en ejecución.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Detener un servicio | `systemctl stop` | `Stop-Service` |

---

### Ejemplos

**Detener el servicio SSH**

Linux

```bash
sudo systemctl stop ssh
```

PowerShell

```powershell
Stop-Service sshd
```

---

**Detener el servicio de impresión**

Linux

```bash
sudo systemctl stop cups
```

PowerShell

```powershell
Stop-Service Spooler
```

---

**Comprobar que el servicio se ha detenido correctamente**

Linux

```bash
systemctl status ssh
```

PowerShell

```powershell
Get-Service sshd
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `systemctl stop` detiene el servicio mediante **systemd**. | `Stop-Service` solicita al Administrador de Control de Servicios (SCM) que detenga el servicio. |
| Generalmente requiere privilegios de administrador (`sudo`). | Normalmente requiere ejecutar PowerShell como administrador. |
| Es habitual comprobar el resultado con `systemctl status`. | Es habitual comprobar el resultado con `Get-Service`. |

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

> **⚠️ Advertencia:** Detener un servicio puede interrumpir aplicaciones, conexiones de red o funciones del sistema que dependan de él. Asegúrate de conocer el impacto antes de ejecutar el comando.

---

[⬆️ Volver al índice](#índice)

## Reiniciar un servicio

### Linux

```bash
sudo systemctl restart <servicio>
```

También puede utilizarse:

```bash
sudo systemctl reload <servicio>
```

**Descripción**

Permite reiniciar un servicio para que vuelva a cargarse desde cero.

- `restart` detiene el servicio y lo inicia de nuevo.
- `reload` recarga la configuración del servicio sin detener completamente su ejecución (solo si el servicio lo admite).

---

### PowerShell

```powershell
Restart-Service <servicio>
```

**Descripción**

Detiene e inicia nuevamente un servicio.

Es útil cuando un servicio deja de responder o cuando se han realizado cambios en su configuración.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Reiniciar un servicio | `systemctl restart` | `Restart-Service` |
| Recargar configuración | `systemctl reload` | No existe un equivalente directo |

---

### Ejemplos

**Reiniciar el servicio SSH**

Linux

```bash
sudo systemctl restart ssh
```

PowerShell

```powershell
Restart-Service sshd
```

---

**Reiniciar el servicio de impresión**

Linux

```bash
sudo systemctl restart cups
```

PowerShell

```powershell
Restart-Service Spooler
```

---

**Recargar la configuración de un servicio**

Linux

```bash
sudo systemctl reload ssh
```

PowerShell

No existe un comando equivalente.

En la mayoría de los casos es necesario reiniciar el servicio:

```powershell
Restart-Service sshd
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `restart` reinicia completamente el servicio. | `Restart-Service` detiene e inicia nuevamente el servicio. |
| Algunos servicios permiten utilizar `reload` para aplicar cambios sin reiniciar completamente. | No existe un cmdlet equivalente a `reload`; normalmente es necesario reiniciar el servicio. |
| Generalmente requiere privilegios de administrador (`sudo`). | Normalmente requiere ejecutar PowerShell como administrador. |

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

### Linux

```bash
sudo systemctl enable <servicio>
```

También puede utilizarse:

```bash
sudo systemctl disable <servicio>
```

**Descripción**

Permite configurar si un servicio debe iniciarse automáticamente durante el arranque del sistema.

- `enable` habilita el inicio automático.
- `disable` deshabilita el inicio automático.

---

### PowerShell

```powershell
Set-Service -Name <servicio> -StartupType Automatic
```

También puede utilizarse:

```powershell
Set-Service -Name <servicio> -StartupType Disabled
```

o

```powershell
Set-Service -Name <servicio> -StartupType Manual
```

**Descripción**

Permite modificar el tipo de inicio de un servicio.

Los tipos de inicio más habituales son:

- `Automatic` → Se inicia automáticamente al arrancar Windows.
- `Manual` → Se inicia únicamente cuando es necesario.
- `Disabled` → El servicio no puede iniciarse hasta volver a habilitarlo.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Habilitar inicio automático | `systemctl enable` | `Set-Service -StartupType Automatic` |
| Deshabilitar inicio automático | `systemctl disable` | `Set-Service -StartupType Disabled` |

---

### Ejemplos

**Configurar el inicio automático del servicio SSH**

Linux

```bash
sudo systemctl enable ssh
```

PowerShell

```powershell
Set-Service -Name sshd -StartupType Automatic
```

---

**Deshabilitar el inicio automático del servicio de impresión**

Linux

```bash
sudo systemctl disable cups
```

PowerShell

```powershell
Set-Service -Name Spooler -StartupType Disabled
```

---

**Configurar un servicio para iniciarlo manualmente**

Linux

No existe un equivalente directo mediante `systemctl`.

Para impedir el inicio automático basta con:

```bash
sudo systemctl disable ssh
```

PowerShell

```powershell
Set-Service -Name sshd -StartupType Manual
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `enable` y `disable` controlan el inicio automático del servicio. | `Set-Service` permite configurar varios tipos de inicio. |
| Un servicio deshabilitado puede iniciarse manualmente mediante `systemctl start` (salvo que esté enmascarado con `mask`). | Un servicio con inicio `Manual` puede iniciarse cuando sea necesario; uno `Disabled` no puede iniciarse hasta volver a habilitarlo. |
| La configuración se realiza mediante **systemd**. | La configuración se almacena en el Administrador de Control de Servicios (SCM). |

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

### Siguiente capítulo

➡️ **04-Usuarios-y-Grupos.md**

En el siguiente capítulo aprenderás a crear, modificar y administrar usuarios y grupos, asignar pertenencias y gestionar permisos básicos tanto en **Linux** como en **PowerShell**.

---

[⬆️ Volver al índice](#índice)