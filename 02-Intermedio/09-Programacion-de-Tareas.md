# Programación de tareas

## Introducción

La programación de tareas permite ejecutar comandos, scripts o aplicaciones de forma automática en momentos determinados o como respuesta a eventos específicos.

En Linux, esta funcionalidad se gestiona principalmente mediante **cron** y **crontab**, mientras que en Windows se utiliza el **Programador de tareas**, que puede administrarse desde PowerShell mediante los cmdlets del módulo **ScheduledTasks**.

---

## Índice

- [Ver las tareas programadas](#ver-las-tareas-programadas)
- [Crear una tarea programada](#crear-una-tarea-programada)
- [Modificar una tarea programada](#modificar-una-tarea-programada)
- [Eliminar una tarea programada](#eliminar-una-tarea-programada)
- [Ejecutar una tarea manualmente](#ejecutar-una-tarea-manualmente)
- [Habilitar y deshabilitar tareas](#habilitar-y-deshabilitar-tareas)
- [Consultar el estado de una tarea](#consultar-el-estado-de-una-tarea)
- [Expresiones CRON](#expresiones-cron)

---

## Ver las tareas programadas

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `crontab -l` | `Get-ScheduledTask` |

**Ejemplo**
```bash
sudo crontab -l
```
```powershell
Get-ScheduledTask `
-TaskPath "\"
```

> 💡 **Diferencia clave** — 🐧 `crontab -l` muestra únicamente las tareas del usuario seleccionado. · 🪟 `Get-ScheduledTask` muestra todas las tareas registradas a las que el usuario tiene acceso.

---

### Comandos relacionados

- [Crear una tarea programada](#crear-una-tarea-programada)
- [Consultar el estado de una tarea](#consultar-el-estado-de-una-tarea)
- [Eliminar una tarea programada](#eliminar-una-tarea-programada)

---

[⬆️ Volver al índice](#índice)

## Crear una tarea programada

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `crontab -e` | `Register-ScheduledTask` |

**Ejemplo**
```bash

```
```powershell
$Action = New-ScheduledTaskAction `
-Execute "powershell.exe" `
-Argument "-File C:\Scripts\script.ps1"

$Trigger = New-ScheduledTaskTrigger `
-Once `
-At (Get-Date) `
-RepetitionInterval (New-TimeSpan -Hours 1)

Register-ScheduledTask `
-TaskName "Script horario" `
-Action $Action `
-Trigger $Trigger
```

> 💡 **Diferencia clave** — 🐧 Las tareas se definen mediante expresiones CRON. · 🪟 Las tareas se crean mediante acciones y desencadenadores (*Triggers*).

---

### Comandos relacionados

- [Ver las tareas programadas](#ver-las-tareas-programadas)
- [Modificar una tarea programada](#modificar-una-tarea-programada)
- [Expresiones CRON](#expresiones-cron)

---

[⬆️ Volver al índice](#índice)

## Modificar una tarea programada

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `crontab -e` | `Set-ScheduledTask` |

**Ejemplo**
```bash

```
```powershell
$Action = New-ScheduledTaskAction `
-Execute "powershell.exe" `
-Argument "-File C:\Scripts\backup2.ps1"

Set-ScheduledTask `
-TaskName "Backup diario" `
-Action $Action
```

> 💡 **Diferencia clave** — 🐧 La modificación consiste en editar manualmente el archivo `crontab`. · 🪟 Permite modificar propiedades concretas mediante parámetros del cmdlet.

---

### Comandos relacionados

- [Crear una tarea programada](#crear-una-tarea-programada)
- [Ejecutar una tarea manualmente](#ejecutar-una-tarea-manualmente)
- [Consultar el estado de una tarea](#consultar-el-estado-de-una-tarea)

---

[⬆️ Volver al índice](#índice)

## Eliminar una tarea programada

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `crontab -e` | `Unregister-ScheduledTask` |

**Ejemplo**
```bash

```
```powershell
Unregister-ScheduledTask `
-TaskName "Backup diario" `
-Confirm:$false
```

> 💡 **Diferencia clave** — 🐧 Para eliminar una única tarea es necesario editar el `crontab`. · 🪟 Cada tarea puede eliminarse individualmente mediante su nombre.

---

### Comandos relacionados

- [Ver las tareas programadas](#ver-las-tareas-programadas)
- [Modificar una tarea programada](#modificar-una-tarea-programada)
- [Crear una tarea programada](#crear-una-tarea-programada)

---

[⬆️ Volver al índice](#índice)

## Ejecutar una tarea manualmente

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `<comando_o_script>` | `Start-ScheduledTask` |

**Ejemplo**
```bash
pwsh script.ps1
```
```powershell
Start-ScheduledTask `
-TaskName "Script PowerShell"
```

> 💡 **Diferencia clave** — 🐧 Se ejecuta directamente el comando o script definido en el `crontab`. · 🪟 Se ejecuta la tarea registrada completa, respetando toda su configuración.

---

### Comandos relacionados

- [Crear una tarea programada](#crear-una-tarea-programada)
- [Consultar el estado de una tarea](#consultar-el-estado-de-una-tarea)
- [Ver las tareas programadas](#ver-las-tareas-programadas)

---

[⬆️ Volver al índice](#índice)

## Habilitar y deshabilitar tareas

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `crontab -e` | `Disable-ScheduledTask` |

**Ejemplo**
```bash

```
```powershell
Enable-ScheduledTask `
-TaskName "Backup diario"
```

> 💡 **Diferencia clave** — 🐧 Las tareas se habilitan o deshabilitan modificando el archivo `crontab`. · 🪟 Existen cmdlets específicos para habilitar y deshabilitar tareas.

---

### Comandos relacionados

- [Ver las tareas programadas](#ver-las-tareas-programadas)
- [Consultar el estado de una tarea](#consultar-el-estado-de-una-tarea)
- [Eliminar una tarea programada](#eliminar-una-tarea-programada)

---

[⬆️ Volver al índice](#índice)

## Consultar el estado de una tarea

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `systemctl status cron` | `Get-ScheduledTaskInfo` |
| **Ejemplo** | `crontab -l` | `Get-ScheduledTask` |

> 💡 **Diferencia clave** — 🐧 Cron únicamente ejecuta las tareas definidas en el `crontab`. · 🪟 Cada tarea mantiene información detallada sobre su ejecución.|

---

### Comandos relacionados

- [Ver las tareas programadas](#ver-las-tareas-programadas)
- [Ejecutar una tarea manualmente](#ejecutar-una-tarea-manualmente)
- [Habilitar y deshabilitar tareas](#habilitar-y-deshabilitar-tareas)

---

[⬆️ Volver al índice](#índice)

## Expresiones CRON

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | *(no aplica)* | `New-ScheduledTaskTrigger` |

**Ejemplo**
```bash

```
```powershell
New-ScheduledTaskTrigger `
-Once `
-At (Get-Date) `
-RepetitionInterval (New-TimeSpan -Minutes 15)
```

> 💡 **Diferencia clave** — 🐧 Utiliza expresiones CRON para definir la programación. · 🪟 Utiliza *Triggers* independientes para definir cuándo se ejecuta una tarea.

---

### Comandos relacionados

- [Crear una tarea programada](#crear-una-tarea-programada)
- [Modificar una tarea programada](#modificar-una-tarea-programada)
- [Ejecutar una tarea manualmente](#ejecutar-una-tarea-manualmente)

---

[⬆️ Volver al índice](#índice)