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

### Linux

```bash
crontab -l
```

También puede utilizarse:

```bash
sudo crontab -l
```

para visualizar las tareas programadas del usuario **root**.

**Descripción**

Permite mostrar todas las tareas programadas del usuario actual mediante **cron**.

Cada línea representa una tarea programada e incluye:

- Fecha y hora de ejecución.
- Comando o script que se ejecutará.

Si el usuario no tiene tareas programadas, se mostrará un mensaje indicándolo.

---

### PowerShell

```powershell
Get-ScheduledTask
```

**Descripción**

Permite mostrar todas las tareas registradas en el Programador de tareas de Windows.

La información incluye, entre otros datos:

- Nombre de la tarea.
- Ruta.
- Estado.
- Desencadenadores (Triggers).
- Acción que ejecuta.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver las tareas programadas | `crontab -l` | `Get-ScheduledTask` |

---

### Ejemplos

**Mostrar las tareas del usuario actual**

Linux

```bash
crontab -l
```

PowerShell

```powershell
Get-ScheduledTask
```

---

**Mostrar las tareas del usuario root**

Linux

```bash
sudo crontab -l
```

PowerShell

```powershell
Get-ScheduledTask `
-TaskPath "\"
```

---

**Buscar una tarea concreta**

Linux

```bash
crontab -l | grep backup
```

PowerShell

```powershell
Get-ScheduledTask |
Where-Object TaskName -like "*backup*"
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `crontab -l` muestra únicamente las tareas del usuario seleccionado. | `Get-ScheduledTask` muestra todas las tareas registradas a las que el usuario tiene acceso. |
| Cada línea representa una tarea programada. | Cada tarea es un objeto con múltiples propiedades. |
| La salida es texto plano. | La salida son objetos que pueden filtrarse o exportarse fácilmente. |

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

> **💡 Consejo:** En Linux, `crontab -l` solo muestra las tareas del usuario actual (o del usuario indicado con `sudo`). En Windows, `Get-ScheduledTask` permite consultar todas las tareas registradas, lo que resulta especialmente útil para administrar servidores con numerosas tareas automáticas.

---

[⬆️ Volver al índice](#índice)

## Crear una tarea programada

### Linux

```bash
crontab -e
```

**Descripción**

Permite crear o editar las tareas programadas del usuario mediante **cron**.

Al ejecutar el comando se abre el archivo **crontab**, donde cada línea representa una tarea programada siguiendo la sintaxis:

```text
* * * * * comando
```

Los cinco primeros campos indican cuándo debe ejecutarse la tarea:

```text
┌──────── Minuto (0-59)
│ ┌────── Hora (0-23)
│ │ ┌──── Día del mes (1-31)
│ │ │ ┌── Mes (1-12)
│ │ │ │ ┌ Día de la semana (0-7)
│ │ │ │ │
* * * * * comando
```

---

### PowerShell

```powershell
Register-ScheduledTask
```

**Descripción**

Permite crear una nueva tarea en el Programador de tareas de Windows.

Una tarea suele componerse de:

- Una acción (qué ejecutar).
- Un desencadenador (*Trigger*).
- Un usuario.
- Opciones adicionales (ejecutar con privilegios elevados, repetir, etc.).

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Crear una tarea programada | `crontab -e` | `Register-ScheduledTask` |

---

### Ejemplos

**Ejecutar un script todos los días a las 08:00**

Linux

```text
0 8 * * * /home/usuario/scripts/backup.sh
```

PowerShell

```powershell
$Action = New-ScheduledTaskAction `
-Execute "powershell.exe" `
-Argument "-File C:\Scripts\backup.ps1"

$Trigger = New-ScheduledTaskTrigger `
-Daily `
-At 08:00

Register-ScheduledTask `
-TaskName "Backup diario" `
-Action $Action `
-Trigger $Trigger
```

---

**Ejecutar una tarea cada hora**

Linux

```text
0 * * * * /home/usuario/scripts/script.sh
```

PowerShell

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

---

**Ejecutar una tarea al iniciar el sistema**

Linux

```text
@reboot /home/usuario/scripts/inicio.sh
```

PowerShell

```powershell
$Action = New-ScheduledTaskAction `
-Execute "powershell.exe" `
-Argument "-File C:\Scripts\inicio.ps1"

$Trigger = New-ScheduledTaskTrigger `
-AtStartup

Register-ScheduledTask `
-TaskName "Inicio del sistema" `
-Action $Action `
-Trigger $Trigger
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Las tareas se definen mediante expresiones CRON. | Las tareas se crean mediante acciones y desencadenadores (*Triggers*). |
| Todas las tareas se almacenan en el archivo `crontab`. | Cada tarea se registra de forma independiente en el Programador de tareas. |
| La configuración es sencilla y basada en texto. | Ofrece muchas más opciones de configuración y condiciones de ejecución. |

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

> **💡 Consejo:** Aunque `crontab` parece mucho más simple, **las expresiones CRON son muy potentes** y permiten programar prácticamente cualquier tipo de ejecución periódica. En Windows se consigue el mismo resultado mediante **Triggers**, que ofrecen una configuración más visual y flexible.

---

[⬆️ Volver al índice](#índice)

## Modificar una tarea programada

### Linux

```bash
crontab -e
```

**Descripción**

En Linux no existe un comando específico para modificar una tarea programada.

Las tareas se editan utilizando `crontab -e`, modificando directamente la línea correspondiente y guardando los cambios.

Al guardar el archivo, **cron** aplica automáticamente la nueva configuración.

---

### PowerShell

```powershell
Set-ScheduledTask
```

**Descripción**

Permite modificar una tarea ya registrada en el Programador de tareas.

Pueden modificarse distintos elementos de la tarea, como:

- Acciones.
- Desencadenadores (*Triggers*).
- Configuración.
- Usuario que la ejecuta.
- Opciones de ejecución.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Modificar una tarea programada | `crontab -e` | `Set-ScheduledTask` |

---

### Ejemplos

**Cambiar la hora de ejecución**

Linux

Antes:

```text
0 8 * * * /home/usuario/scripts/backup.sh
```

Después:

```text
0 10 * * * /home/usuario/scripts/backup.sh
```

PowerShell

```powershell
$Trigger = New-ScheduledTaskTrigger `
-Daily `
-At 10:00

Set-ScheduledTask `
-TaskName "Backup diario" `
-Trigger $Trigger
```

---

**Cambiar el script que ejecuta la tarea**

Linux

Antes:

```text
0 8 * * * /home/usuario/scripts/backup.sh
```

Después:

```text
0 8 * * * /home/usuario/scripts/backup2.sh
```

PowerShell

```powershell
$Action = New-ScheduledTaskAction `
-Execute "powershell.exe" `
-Argument "-File C:\Scripts\backup2.ps1"

Set-ScheduledTask `
-TaskName "Backup diario" `
-Action $Action
```

---

**Modificar varios parámetros**

Linux

Editar el archivo mediante:

```bash
crontab -e
```

PowerShell

```powershell
Set-ScheduledTask `
-TaskName "Backup diario" `
-Action $Action `
-Trigger $Trigger
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| La modificación consiste en editar manualmente el archivo `crontab`. | Permite modificar propiedades concretas mediante parámetros del cmdlet. |
| Cada cambio requiere editar la línea correspondiente. | Puede modificarse únicamente la propiedad necesaria sin recrear toda la tarea. |
| Los cambios se aplican al guardar el archivo. | Los cambios se aplican inmediatamente tras ejecutar el cmdlet. |

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

> **💡 Consejo:** En Linux no es necesario reiniciar el servicio **cron** después de modificar el `crontab`. Los cambios se aplican automáticamente al guardar el archivo. En Windows, las modificaciones realizadas con `Set-ScheduledTask` también tienen efecto inmediatamente.

---

[⬆️ Volver al índice](#índice)

## Eliminar una tarea programada

### Linux

```bash
crontab -e
```

También puede utilizarse:

```bash
crontab -r
```

**Descripción**

En Linux existen dos formas de eliminar tareas programadas:

- `crontab -e` → Permite eliminar únicamente la línea correspondiente a la tarea.
- `crontab -r` → Elimina **todas** las tareas programadas del usuario.

> **⚠️ Advertencia:** `crontab -r` elimina el archivo `crontab` completo y no solicita confirmación en muchas distribuciones.

---

### PowerShell

```powershell
Unregister-ScheduledTask
```

**Descripción**

Permite eliminar una tarea registrada en el Programador de tareas de Windows.

Puede eliminarse una tarea concreta indicando su nombre o su ruta.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Eliminar una tarea programada | `crontab -e` | `Unregister-ScheduledTask` |
| Eliminar todas las tareas | `crontab -r` | No existe un equivalente directo |

---

### Ejemplos

**Eliminar una única tarea**

Linux

Editar el archivo:

```bash
crontab -e
```

Y eliminar la línea correspondiente:

```text
0 8 * * * /home/usuario/scripts/backup.sh
```

PowerShell

```powershell
Unregister-ScheduledTask `
-TaskName "Backup diario"
```

---

**Eliminar una tarea sin solicitar confirmación**

PowerShell

```powershell
Unregister-ScheduledTask `
-TaskName "Backup diario" `
-Confirm:$false
```

---

**Eliminar todas las tareas del usuario**

Linux

```bash
crontab -r
```

PowerShell

```powershell
# No existe un comando equivalente.
# Las tareas deben eliminarse individualmente.
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Para eliminar una única tarea es necesario editar el `crontab`. | Cada tarea puede eliminarse individualmente mediante su nombre. |
| `crontab -r` elimina todas las tareas del usuario. | No existe un cmdlet para eliminar todas las tareas programadas de una sola vez. |
| La configuración se basa en un único archivo de texto. | Cada tarea se administra como un objeto independiente. |

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

> **💡 Consejo:** Si únicamente deseas eliminar una tarea en Linux, utiliza **`crontab -e`** y borra la línea correspondiente. **`crontab -r`** debe utilizarse con mucha precaución, ya que elimina todas las tareas programadas del usuario.

---

[⬆️ Volver al índice](#índice)

## Ejecutar una tarea manualmente

### Linux

```bash
<comando_o_script>
```

También puede utilizarse:

```bash
bash <script.sh>
```

o, si el script tiene permisos de ejecución:

```bash
./script.sh
```

**Descripción**

En Linux no existe un comando específico para ejecutar manualmente una tarea definida en **cron**.

Para comprobar su funcionamiento, simplemente se ejecuta el mismo comando o script que aparece en el `crontab`.

Esto permite verificar que la tarea funciona correctamente antes de esperar a que cron la ejecute automáticamente.

---

### PowerShell

```powershell
Start-ScheduledTask
```

**Descripción**

Permite ejecutar inmediatamente una tarea registrada en el Programador de tareas, sin esperar a que se cumpla el desencadenador (*Trigger*).

La tarea se ejecutará utilizando exactamente la misma configuración con la que fue creada.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ejecutar una tarea manualmente | Ejecutar el comando o script | `Start-ScheduledTask` |

---

### Ejemplos

**Ejecutar un script de copia de seguridad**

Linux

```bash
/home/usuario/scripts/backup.sh
```

o

```bash
bash /home/usuario/scripts/backup.sh
```

PowerShell

```powershell
Start-ScheduledTask `
-TaskName "Backup diario"
```

---

**Ejecutar un script de PowerShell**

Linux

```bash
pwsh script.ps1
```

PowerShell

```powershell
Start-ScheduledTask `
-TaskName "Script PowerShell"
```

---

**Ejecutar un script ubicado en el directorio actual**

Linux

```bash
./script.sh
```

PowerShell

```powershell
Start-ScheduledTask `
-TaskName "Mi tarea"
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Se ejecuta directamente el comando o script definido en el `crontab`. | Se ejecuta la tarea registrada completa, respetando toda su configuración. |
| No interviene el servicio **cron**. | La ejecución la gestiona el Programador de tareas. |
| Permite comprobar rápidamente el funcionamiento del script. | Permite probar exactamente el mismo comportamiento que tendrá la tarea programada. |

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

> **💡 Consejo:** Una de las causas más habituales de fallo en tareas programadas es que **el script nunca se ha probado manualmente**. Si funciona correctamente al ejecutarlo de forma manual, será mucho más sencillo localizar problemas relacionados con permisos, variables de entorno o configuración del programador.

---

[⬆️ Volver al índice](#índice)

## Habilitar y deshabilitar tareas

### Linux

En **cron** no existe un comando específico para habilitar o deshabilitar una tarea.

Lo habitual es comentar o descomentar la línea correspondiente en el archivo `crontab`.

Para editar el archivo:

```bash
crontab -e
```

**Descripción**

Una tarea puede deshabilitarse añadiendo el carácter `#`al inciio de la línea.

Cuando una línea está comentada, **cron la ignora** y no volverá a ejecutarse hasta que se elimine el comentario.

---

### PowerShell

```powershell
Disable-ScheduledTask
```

Para volver a habilitarla:

```powershell
Enable-ScheduledTask
```

**Descripción**

Permite deshabilitar o habilitar una tarea registrada en el Programador de tareas sin necesidad de eliminarla.

Una tarea deshabilitada permanece registrada, pero no se ejecutará hasta que vuelva a habilitarse.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Deshabilitar una tarea | Comentar la línea en `crontab` | `Disable-ScheduledTask` |
| Habilitar una tarea | Descomentar la línea | `Enable-ScheduledTask` |

---

### Ejemplos

**Deshabilitar una tarea**

Linux

Antes:

```text
0 8 * * * /home/usuario/scripts/backup.sh
```

Después:

```text
# 0 8 * * * /home/usuario/scripts/backup.sh
```

PowerShell

```powershell
Disable-ScheduledTask `
-TaskName "Backup diario"
```

---

**Volver a habilitar una tarea**

Linux

Antes:

```text
# 0 8 * * * /home/usuario/scripts/backup.sh
```

Después:

```text
0 8 * * * /home/usuario/scripts/backup.sh
```

PowerShell

```powershell
Enable-ScheduledTask `
-TaskName "Backup diario"
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Las tareas se habilitan o deshabilitan modificando el archivo `crontab`. | Existen cmdlets específicos para habilitar y deshabilitar tareas. |
| La tarea permanece en el archivo, pero comentada. | La tarea permanece registrada con un estado de habilitada o deshabilitada. |
| La modificación requiere editar manualmente el archivo. | La operación se realiza mediante un único comando. |

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

> **💡 Consejo:** Siempre que una tarea pueda volver a utilizarse en el futuro, es preferible **deshabilitarla en lugar de eliminarla**. Así conservarás su configuración y podrás reactivarla rápidamente cuando sea necesario.

---

[⬆️ Volver al índice](#índice)

## Consultar el estado de una tarea

### Linux

```bash
systemctl status cron
```

También puede utilizarse:

```bash
systemctl status crond
```

(según la distribución utilizada).

Para comprobar las tareas programadas del usuario:

```bash
crontab -l
```

**Descripción**

En Linux, el estado de una tarea depende de dos aspectos:

- Que el servicio **cron** esté en ejecución.
- Que la tarea exista en el archivo `crontab`.

A diferencia de Windows, **cron no mantiene un estado individual para cada tarea** (como "Lista", "En ejecución" o "Deshabilitada").

---

### PowerShell

```powershell
Get-ScheduledTaskInfo
```

**Descripción**

Permite consultar información sobre el estado de ejecución de una tarea registrada en el Programador de tareas.

Entre la información disponible se encuentra:

- Última ejecución.
- Resultado de la última ejecución.
- Próxima ejecución.
- Número de ejecuciones.
- Estado actual.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Consultar el estado del programador | `systemctl status cron` | `Get-ScheduledTaskInfo` |
| Consultar las tareas configuradas | `crontab -l` | `Get-ScheduledTask` |

---

### Ejemplos

**Comprobar si cron está funcionando**

Linux

```bash
systemctl status cron
```

PowerShell

```powershell
Get-ScheduledTaskInfo `
-TaskName "Backup diario"
```

---

**Consultar las tareas programadas**

Linux

```bash
crontab -l
```

PowerShell

```powershell
Get-ScheduledTask
```

---

**Consultar la información de una tarea concreta**

Linux

```bash
crontab -l | grep backup
```

PowerShell

```powershell
Get-ScheduledTaskInfo `
-TaskName "Backup diario"
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Cron únicamente ejecuta las tareas definidas en el `crontab`. | Cada tarea mantiene información detallada sobre su ejecución. |
| No existe un estado individual para cada tarea. | Es posible conocer la última ejecución, el resultado y la próxima ejecución de cada tarea. |
| El estado del servicio se consulta mediante `systemctl`. | El estado se consulta mediante `Get-ScheduledTaskInfo`. |

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

> **💡 Consejo:** Una diferencia importante entre ambos sistemas es que **Windows registra el historial y el resultado de cada ejecución**, mientras que **cron simplemente lanza el comando en la fecha y hora indicadas**. Si necesitas comprobar por qué una tarea de Linux ha fallado, normalmente tendrás que revisar los registros del sistema o los *logs* generados por el propio script.

---

[⬆️ Volver al índice](#índice)

## Expresiones CRON

### Linux

Las tareas programadas en **cron** se definen mediante expresiones CRON.

Cada expresión indica el momento exacto en el que debe ejecutarse un comando o script.

Su estructura es la siguiente:

```text
┌──────── Minuto (0-59)
│ ┌────── Hora (0-23)
│ │ ┌──── Día del mes (1-31)
│ │ │ ┌── Mes (1-12)
│ │ │ │ ┌ Día de la semana (0-7)
│ │ │ │ │
* * * * * comando
```

Cada uno de los cinco campos puede contener valores concretos, rangos, listas o caracteres especiales.

---

### PowerShell

Windows **no utiliza expresiones CRON**.

Las tareas programadas se configuran mediante **Triggers** (desencadenadores), indicando la frecuencia de ejecución mediante cmdlets como:

```powershell
New-ScheduledTaskTrigger
```

Los *Triggers* pueden configurarse para ejecutarse:

- Una sola vez.
- Cada día.
- Cada semana.
- Cada mes.
- Al iniciar el sistema.
- Al iniciar sesión.
- Ante determinados eventos.

---

### Equivalencia

| Expresión CRON | Significado | Trigger equivalente |
|---------------|-------------|---------------------|
| `* * * * *` | Cada minuto | Repetición cada minuto |
| `0 * * * *` | Cada hora | Repetición cada hora |
| `0 8 * * *` | Todos los días a las 08:00 | `-Daily -At 08:00` |
| `0 8 * * 1-5` | De lunes a viernes a las 08:00 | `-Weekly` |
| `@reboot` | Al iniciar el sistema | `-AtStartup` |

---

### Caracteres especiales

| Símbolo | Significado | Ejemplo |
|---------|-------------|---------|
| `*` | Todos los valores posibles | `* * * * *` |
| `,` | Lista de valores | `1,15,30` |
| `-` | Rango | `1-5` |
| `/` | Intervalo | `*/10` |

---

### Expresiones más utilizadas

| Expresión | Significado |
|-----------|-------------|
| `* * * * *` | Cada minuto |
| `*/5 * * * *` | Cada 5 minutos |
| `*/10 * * * *` | Cada 10 minutos |
| `0 * * * *` | Cada hora |
| `0 */2 * * *` | Cada 2 horas |
| `0 0 * * *` | Todos los días a las 00:00 |
| `0 8 * * *` | Todos los días a las 08:00 |
| `30 18 * * *` | Todos los días a las 18:30 |
| `0 8 * * 1-5` | De lunes a viernes a las 08:00 |
| `0 9 * * 6,0` | Sábados y domingos a las 09:00 |
| `0 0 1 * *` | El día 1 de cada mes |
| `0 0 1 1 *` | El 1 de enero |
| `@reboot` | Al iniciar el sistema |

---

### Ejemplos

**Ejecutar un script cada día a las 08:00**

Linux

```text
0 8 * * * /home/usuario/scripts/backup.sh
```

PowerShell

```powershell
New-ScheduledTaskTrigger `
-Daily `
-At 08:00
```

---

**Ejecutar un script cada 15 minutos**

Linux

```text
*/15 * * * * /home/usuario/scripts/script.sh
```

PowerShell

```powershell
New-ScheduledTaskTrigger `
-Once `
-At (Get-Date) `
-RepetitionInterval (New-TimeSpan -Minutes 15)
```

---

**Ejecutar una tarea al iniciar el sistema**

Linux

```text
@reboot /home/usuario/scripts/inicio.sh
```

PowerShell

```powershell
New-ScheduledTaskTrigger `
-AtStartup
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Utiliza expresiones CRON para definir la programación. | Utiliza *Triggers* independientes para definir cuándo se ejecuta una tarea. |
| Una única línea contiene toda la programación. | La programación se configura mediante propiedades del desencadenador. |
| Muy compacto y potente. | Más descriptivo y sencillo de interpretar. |

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

> **💡 Consejo:** Si solo vas a memorizar una parte de **cron**, aprende la estructura de los cinco campos (`minuto hora día mes día_semana`) y las expresiones más habituales (`*/5`, `0 * * * *`, `0 8 * * *` y `@reboot`). Con ellas podrás crear la mayoría de tareas programadas sin necesidad de consultar documentación.

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

### Comandos más utilizados

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver tareas | `crontab -l` | `Get-ScheduledTask` |
| Crear tarea | `crontab -e` | `Register-ScheduledTask` |
| Modificar tarea | `crontab -e` | `Set-ScheduledTask` |
| Ejecutar tarea | Ejecutar el script | `Start-ScheduledTask` |
| Eliminar tarea | `crontab -e` | `Unregister-ScheduledTask` |
| Consultar estado | `systemctl status cron` | `Get-ScheduledTaskInfo` |

---

### Flujo de trabajo recomendado

Cuando necesites automatizar una tarea, el proceso habitual suele ser:

1. Crear y probar el script manualmente.
2. Crear la tarea programada.
3. Verificar que la programación es correcta.
4. Ejecutarla manualmente para comprobar su funcionamiento.
5. Revisar periódicamente su estado y los registros generados.
6. Modificarla o eliminarla cuando deje de ser necesaria.

---

### Diferencias clave

| Linux (cron) | Windows (Programador de tareas) |
|---------------|---------------------------------|
| Utiliza expresiones CRON para definir la programación. | Utiliza desencadenadores (*Triggers*) configurables. |
| Todas las tareas del usuario se almacenan en un único archivo (`crontab`). | Cada tarea es un objeto independiente. |
| Configuración sencilla basada en texto. | Configuración más flexible con numerosas opciones adicionales. |
| No mantiene un historial detallado de cada ejecución. | Registra información sobre la última ejecución, el resultado y la próxima ejecución. |

---

[⬆️ Volver al índice](#índice)