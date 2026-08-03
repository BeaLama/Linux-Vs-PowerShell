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
- [Resumen de equivalencias](#resumen-de-equivalencias)

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

### Buenas prácticas

- Revisa periódicamente las tareas programadas para eliminar aquellas que ya no sean necesarias.
- Comprueba que las rutas de los scripts siguen siendo válidas.
- Utiliza nombres descriptivos para identificar fácilmente cada tarea.
- Documenta las tareas críticas para facilitar su mantenimiento.

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

### Buenas prácticas

- Utiliza rutas absolutas para los scripts y ejecutables.
- Comprueba que el usuario tiene permisos para ejecutar la tarea.
- Añade comentarios en el `crontab` para documentar el propósito de cada tarea.
- Prueba el script manualmente antes de programarlo.
- Utiliza nombres descriptivos para identificar fácilmente las tareas en Windows.

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

### Buenas prácticas

- Revisa la sintaxis antes de guardar el archivo `crontab`.
- Comprueba que las rutas de los scripts siguen siendo válidas tras la modificación.
- Documenta los cambios realizados en tareas críticas.
- Prueba la tarea manualmente después de modificarla para verificar que sigue funcionando correctamente.

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

### Buenas prácticas

- Comprueba que la tarea ya no es necesaria antes de eliminarla.
- Realiza una copia del `crontab` antes de efectuar cambios importantes.
- Evita utilizar `crontab -r` salvo que realmente quieras eliminar todas las tareas programadas.
- Documenta la eliminación de tareas críticas en servidores de producción.

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

### Buenas prácticas

- Ejecuta siempre el script manualmente antes de programarlo.
- Comprueba que las rutas y permisos sean correctos.
- Revisa la salida del script para detectar posibles errores.
- Si la tarea genera registros (*logs*), verifica que se crean correctamente.

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

### Buenas prácticas

- Deshabilita una tarea antes de eliminarla si no estás seguro de que ya no será necesaria.
- Añade un comentario indicando el motivo cuando deshabilites una tarea en el `crontab`.
- Comprueba el estado de la tarea después de habilitarla o deshabilitarla.
- Evita eliminar tareas críticas si solo necesitas detener su ejecución temporalmente.

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

### Buenas prácticas

- Comprueba que el servicio **cron** está activo antes de investigar por qué una tarea no se ejecuta.
- Revisa periódicamente el resultado de las tareas críticas en Windows.
- Verifica que la próxima ejecución sea la esperada después de modificar una tarea.
- Si una tarea falla, consulta también los registros del sistema para obtener más información.

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

### Buenas prácticas

- Comprueba siempre que la expresión CRON sea correcta antes de guardar el `crontab`.
- Utiliza horarios fácilmente identificables para simplificar el mantenimiento.
- Evita programar varias tareas pesadas exactamente a la misma hora.
- Documenta el significado de expresiones complejas mediante comentarios.

---

### Comandos relacionados

- [Crear una tarea programada](#crear-una-tarea-programada)
- [Modificar una tarea programada](#modificar-una-tarea-programada)
- [Ejecutar una tarea manualmente](#ejecutar-una-tarea-manualmente)

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver las tareas programadas | `crontab -l` | `Get-ScheduledTask` |
| Crear una tarea programada | `crontab -e` | `Register-ScheduledTask` |
| Modificar una tarea programada | `crontab -e` | `Set-ScheduledTask` |
| Eliminar una tarea programada | `crontab -e` | `Unregister-ScheduledTask` |
| Eliminar todas las tareas | `crontab -r` | No existe un equivalente directo |
| Ejecutar una tarea manualmente | Ejecutar el comando o script | `Start-ScheduledTask` |
| Habilitar una tarea | Descomentar la línea del `crontab` | `Enable-ScheduledTask` |
| Deshabilitar una tarea | Comentar la línea del `crontab` | `Disable-ScheduledTask` |
| Consultar el estado de una tarea | `systemctl status cron` / `crontab -l` | `Get-ScheduledTaskInfo` |

---

### Buenas prácticas generales

- Prueba siempre el script manualmente antes de programarlo.
- Utiliza rutas absolutas para evitar errores durante la ejecución automática.
- Asigna nombres descriptivos a las tareas para facilitar su identificación.
- Documenta las tareas críticas indicando su finalidad y frecuencia de ejecución.
- Revisa periódicamente las tareas programadas para eliminar aquellas que ya no sean necesarias.
- Evita programar varias tareas intensivas exactamente a la misma hora.
- Comprueba regularmente los registros o *logs* para detectar posibles errores.

---

[⬆️ Volver al índice](#índice)