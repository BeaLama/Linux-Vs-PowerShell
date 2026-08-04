# Planificación de tareas

## Introducción

La planificación de tareas permite automatizar la ejecución de programas, scripts y procesos en momentos determinados o cuando ocurre un evento específico.

## Índice

- [Concepto de planificación de tareas](#concepto-de-planificación-de-tareas)
- [Ventajas de automatizar tareas.](#ventajas-de-automatizar-tareas)
- [Tipos de desencadenadores (Triggers)](#tipos-de-desencadenadores-triggers)
- [Acciones programadas](#acciones-programadas)
- [Condiciones y configuración de las tareas](#condiciones-y-configuración-de-las-tareas)
- [Programador de tareas en Windows](#programador-de-tareas-en-windows)
- [Administración mediante PowerShell](#administración-mediante-powershell)
- [Administración mediante shtasks](#administración-mediante-shtasks)
- [Cron en Linux](#cron-en-linux)
- [Systemd Timers](#systemd-timers)
- [Monitorización y resolución de problemas](#monitorización-y-resolución-de-problemas)

---

## Concepto de planificación de tareas

**Conceptos clave:**

- **¿Qué es la planificación de tareas?:** La planificación de tareas consiste en programar la ejecución automática de una acción cuando se cumple una condición determinada.
- **¿Para qué sirve?:** La planificación de tareas permite automatizar numerosas operaciones administrativas.
- **Funcionamiento básico:** El funcionamiento de una tarea programada puede representarse de la siguiente manera.
- **Elementos de una tarea programada:** Una tarea programada suele estar formada por varios componentes: Nombre, que identifica la tarea.
- **Sistemas de planificación:** Los principales sistemas utilizados son: Programador de tareas.
- **Ejemplos de uso:** Algunos ejemplos habituales de planificacion de tareas son: Ejecutar una copia de seguridad todos los días a las 02:00.
- **Importancia de la planificación de tareas:** La automatización aporta numerosas ventajas en la administración de sistemas.

## Ventajas de automatizar tareas.

**Conceptos clave:**

- **Ahorro de tiempo:** Una de las principales ventakas consiste en eliminar la necesidad de ejecutar manualmente tareas repetitivas.
- **Reducción de errores humanos:** Las tareas realizadas manualmente pueden provocar errores como: Olvidar ejecutar un proceso.
- **Mayor productividad:** Al automatizar las tareas rutinarias, los administradores pueden dedicar su tiempo a actividades de mayor valor, como: Resolver incidencias.
- **Ejecución programada:** Las tareas pueden ejecutarse exactamente cuando sea necesario.
- **Funcionamiento continuo:** Las tareas programadas pueden ejecutarse incluso cuando ningún usuario ha iniciado sesión.
- **Mayor disponilidad:** Muchas tareas de mantenimiento pueden ejecutarse automáticamente para mantener el sistema operativo en buen estado.
- **Estandarización de procesos:** La automatización garantiza que una misma tarea siempre se ejecute siguiendo exactamente el mismo procedimiento.
- **Escalabilidad:** En una organización pequeña puede se rposible realidad determinadas tareas manualmente.
- **Ejemplos de automatización:** Algunas tareas que suelen automatizarse son: Copias de seguridad.

---

## Tipos de desencadenadores (Triggers)

**Conceptos clave:**

- **¿Qué es un desencadenador?:** El desencadenador es el elemento que indica al sistema operativo el momento exacto en el que debe iniciarse una tarea.
- **Desencadenadores basados en el tiempo:** Son los más utilizados y permiten ejecutar una tarea según una programación establecida.
- **Desencadenadores al iniciar el sistema:** Permiten ejecutar una tarea cuando el sistema operativo finaliza su proceso de arranque.
- **Desencadenadores al inciar sesión:** La tarea se ejecuta cuando el usuario inicia sesión en el sistema.
- **Desenadenadores por inactividad:** Algunas tareas pueden ejecutarse cuando el equipo permanece inactivo durante un tiempo determinado.
- **Desencadenadores por eventos:** También es posible iniciar una tarea cuando ocurre un determinado evento del sistema.
- **Múltiples desencadenadores:** Una misma tarea puede disponer de varios desencadenadores.
- **Desencadenadores en Windows:** El Programador de tareas de Windows permite utilizar desencadenadores como: Según una programación.
- **Desencadenadores en Linux:** En Linux, herramientas como cron y systemd timers utilizan principalmente desencadenadores relacionados con el tiempo.

---

## Acciones programadas

**Conceptos clave:**

- **¿Qué es una acción?:** Una acción es la operación que ejecutará una tarea programada cuando sea activada por uno de sus Triggers.
- **Tipos de acciones:** Dependiendo del sistema operativo y de la herramienta utilizada, pueden ejecutarse diferentes tipos de accicones.
- **Ejecutar programas:** Una de las acciones más comunes consiste en abrir una aplicación determinada.
- **Ejecutar scripts:** Las tareas programadas también pueden ejecutar scripts creados por el administrador.

### Ejecutar comandos

*Otra posibilidad consiste en ejecutar directamente comandos del sistema operativo.*

```bash
apt update
```
```bash
systemctl restart apache2
```

---

**Conceptos clave:**

- **Administrar servicios:** Las tareas programadas pueden utilizarse para administrar servicios automáticamente.
- **Ejecutar copias de seguridad:** Una de las aplicaciones más habituales consiste en automatizar las copias de seguridad.
- **Ejecutar tareas de mantenimiento:** Muchas operaciones de mantenimiento pueden automatizarse.
- **Acciones en Windows:** En el Programador de tareas de Windows, la acción más habitual es: Iniciar un programa.

### Acciones en Linux

*En Linux, las acciones suelen ejecutarse mediante: Cron.*

```bash
/usr/local/scripts/backup.sh
```
```bash
python3 informe.py
```

---

## Condiciones y configuración de las tareas

**Conceptos clave:**

- **¿Qué son las condiciones?:** Las condiciones son requisitos adicionales que deben cumplirse para que una tarea pueda ejecutarse.
- **Condición de inactividad:** Una tarea puede configurarse para ejecutarse únicamente cuando el equipo permanezca inactivo durante un tiempo determinado.
- **Condición de alimentación:** En equipos portátiles es posible indicar que una tarea solo se ejecute cuando el dispositivo esté conectado a la corriente eléctrica.
- **Condición de conexión de red:** Algunas tareas requieren acceso a recursos de red o a Internet.
- **Repetición de la tarea:** Es posible indicar que una tarea se repita automáticamente dentro de un intervalo de tiempo.
- **Tiempo máximo de ejecución:** Puede establecerse un límite de tiempo para impedir que una tarea permanezca ejecutándose indefinidamente.
- **Comportamiento ante errores:** Las tareas programadas pueden configurarse para actuar cuando se produce un error.
- **Configuración en Windows:** El Programador de tareas de Windows incluye varias pestañas para configurar una tarea.
- **Configuración en Linux:** En Linux, herramientas como cron ofrecen una configuración más sencilla centrada en la programación temporal.

---

## Programador de tareas en Windows

*El Programador de tareas (*Task Scheduler*) es la herramienta integrada en Windows que permite crear, modificar y administrar tareas programadas.*

**Conceptos clave:**

- **¿Qué es el Programador de tareas?:** El Programador de tareas es una consola de administración que permite programar la ejecución automática de tareas basadas en: Una fecha y hora.
- **Abrir el Programador de tareas:** Existen varias formas de acceder a esta herramienta.
- **Interfaz principal:** La consola se divide en varias zonas.
- **Crear una tarea básica:** Windows ofrece un asistente para crear tareas sencillas.
- **Crear una tarea avanzada:** Para disponer de todas las opciones de configuración puede utilizarse.
- **Administrar tareas existentes:** Sobre una tarea ya creada pueden realizarse diferentes acciones.
- **Historial de tareas:** El Programador de tareas puede registrar el historial de ejecución de cada tarea.
- **Biblioteca del Programador de tareas:** Todas las tareas creadas se almacenan en la Biblioteca del Programador de tareas.
- **Ejemplos de uso:** El Programador de tareas suele utilizarse para: Ejecutar scripts de PowerShell.
- **Ventajas del Programador de tareas:** Entre sus principales ventajas destacan: Interfaz gráfica sencilla.

---

## Administración mediante PowerShell

*PowerShell permite administrar tareas programadas desde la línea de comandos mediante una colección de cmdlets específicos.*

### Obtener todas las tareas programadas

*Para listar todas las tareas registradas en el sistema.*

```powershell
Get-ScheduledTask
```

---

### Consultar una tarea concreta

*Para obtener información sobre una tarea específica.*

```powershell
Get-ScheduledTask -TaskName "Backup Diario"
```
```powershell
Get-ScheduledTask -TaskPath "\Microsoft\Windows\"
```

---

### Consultar el estado de una tarea

*Para conocer el estado de ejecución de una tarea.*

```powershell
Get-ScheduledTaskInfo -TaskName "Backup Diario"
```

---

### Ejecutar una tarea manualmente

*Para iniciar una tarea sin esperar a que se active su desencadenador.*

```powershell
Start-ScheduledTask -TaskName "Backup Diario"
```

---

### Detener una tarea

*Si una tarea está en ejecución y es necesario finalizarla.*

```powershell
Stop-ScheduledTask -TaskName "Backup Diario"
```

---

### Deshabilitar una tarea

*Para impedir temporalmente que una tarea se ejecute.*

```powershell
Disable-ScheduledTask -TaskName "Backup Diario"
```

---

### Habilitar una tarea

*Para volver a activar una tarea previamente deshabilitada.*

```powershell
Enable-ScheduledTask -TaskName "Backup Diario"
```

---

### Crear una tarea programada

*PowerShell también permite crear tareas mediante scripts.*

```powershell
$Action = New-ScheduledTaskAction -Execute "notepad.exe"

$Trigger = New-ScheduledTaskTrigger -Daily -At 09:00

Register-ScheduledTask -TaskName "Abrir Bloc de notas" -Action $Action -Trigger $Trigger
```

---

### Eliminar una tarea

*Para eliminar una tarea existente.*

```powershell
Unregister-ScheduledTask -TaskName "Backup Diario"
```
```powershell
Unregister-ScheduledTask -TaskName "Backup Diario" -Confirm:$false
```

---

### Automatización mediante scripts

*Una de las mayores ventajas de PowerShell es la posibilidad de administrar múltiples tareas de forma automática.*

```powershell
Get-ScheduledTask | Where-Object State -eq "Disabled"
```

---

## Administración mediante shtasks

**Conceptos clave:**

- **¿Qué es schtasks?:** `schtasks` es un comando integrado en Windows que permite administrar tareas programadas desde el Símbolo del sistema (CMD).
- **Consultar tareas programadas:** Para mostrar todas las tareas registradas.
- **Mostrar información detallada:** Si se desea obtener más información.
- **Crear una tarea:** Para crear una tarea que abra el Bloc de notas todos los días a las 09:00.
- **Ejecutar una tarea manualmente:** Para iniciar una tarea sin esperar a su programación.
- **Modificar una tarea:** Es posible cambiar algunos parámetros de una tarea existente mediante.
- **Eliminar una tarea:** Para eliminar una tarea.
- **Frecuencias disponibles:** El parámetro `/sc` permite definir diferentes tipos de programación.
- **Ventajas de schtasks:** Entre sus principales ventajas destacan: Disponible en todas las versiones modernas de Windows.

---

## Cron en Linux

*Cron es el sistema tradicional de planificación de tareas en Linux y otros sistemas Unix.*

**Conceptos clave:**

- **¿Qué es Cron?:** Cron es un servicio que permanece ejecutándose en segundo plano y comprueba continuamente si existe alguna tarea programada que deba ejecutarse.

### ¿Qué es Crontab?

*Las tareas programadas se almacenan en un archivo denominado crontab.*

```bash
crontab -e
```
```bash
crontab -l
```

---

### Sintaxis de Cron

*Cada línea del archivo crontab representa una tarea programada.*

```bash
30 2 * * * /home/admin/backup.sh
```

---

### Significado de los campos

*Cada campo representa una parte de la programación.*

| Campo | Valores |
|--------|----------|
| Minuto | 0-59 |
| Hora | 0-23 |
| Día del mes | 1-31 |
| Mes | 1-12 |
| Día de la semana | 0-7 (0 y 7 = domingo) |

---

### Caracteres especiales

*Cron permite utilizar varios caracteres para simplificar la programación.*

```bash
* * * * *
```
```bash
0 8,16 * * *
```

---

### Ejemplos de programación

*Todos los días a las 03:00.*

```bash
0 3 * * * /home/admin/backup.sh
```
```bash
0 8 * * 1 /home/admin/informe.sh
```

---

**Conceptos clave:**

- **Ubicación de los archivos:** Además del crontab de cada usuario, Linux dispone de otros archivos relacionados con Cron.

### Comprobar el servicio Cron

*En sistemas con systemd, puede comprobarse el estado del servicio mediante.*

```bash
systemctl status cron
```
```bash
systemctl status crond
```

---

## Systemd Timers

*Aunque Cron continúa siendo una herramienta muy utilizada para programar tareas en Linux, muchas distribuciones modernas utilizan systemd timers como alternativa.*

**Conceptos clave:**

- **¿Qué es un Systemd Timer?:** Un Systemd Timer es una unidad de systemd que permite ejecutar automáticamente un servicio cuando se cumple una determinada condición temporal.
- **Archivos utilizados:** Para utilizar un timer normalmente se crean dos archivos: Un archivo.
- **Estructura de un servicio:** El archivo .service contiene la acción que realizará la tarea.
- **Estructura de un timer:** El archivo .timer define la programación.

### Activar un timer

*Una vez creados los archivos, el timer puede habilitarse mediante.*

```bash
sudo systemctl enable backup.timer
```
```bash
sudo systemctl start backup.timer
```

---

### Consultar timers

*Para visualizar todos los timers activos.*

```bash
systemctl list-timers
```

---

### Consultar el estado

*Para comprobar el estado de un timer.*

```bash
systemctl status backup.timer
```
```bash
systemctl status backup.service
```

---

### Deshabilitar un timer

*Si se desea impedir que continúe ejecutándose automáticamente.*

```bash
sudo systemctl disable backup.timer
```
```bash
sudo systemctl stop backup.timer
```

---

**Conceptos clave:**

- **Ventajas frente a Cron:** Los Systemd Timers ofrecen varias ventajas respecto a Cron.

### Cron vs Systemd Timers

| Cron | Systemd Timers |
|------|----------------|
| Ejecuta comandos directamente. | Ejecuta servicios de systemd. |
| Configuración sencilla. | Configuración más avanzada. |
| Basado en crontab. | Basado en archivos `.service` y `.timer`. |
| Muy extendido. | Integrado con systemd. |
| Menor control sobre dependencias. | Mayor control y flexibilidad. |

---

## Monitorización y resolución de problemas

*Una vez que una tarea programada ha sido creada, es importante supervisar su funcionamiento para comprobar que se ejecuta correctamente y detectar posibles errores.*

**Conceptos clave:**

- **¿Por qué monitorizar las tareas programadas?:** La supervisión de las tareas permite: Comprobar que se ejecutan correctamente.
- **Problemas habituales:** Las incidencias más frecuentes son: La tarea no se ejecuta.

### Monitorización en Windows

*En Windows pueden utilizarse diferentes herramientas.*

```powershell
Get-ScheduledTaskInfo -TaskName "Backup Diario"
```

---

**Conceptos clave:**

- **Historial del Programador de tareas:** El Programador de tareas permite registrar todas las ejecuciones realizadas.

### Monitorización en Linux

*En Linux la supervisión depende de la herramienta utilizada.*

```bash
crontab -l
```
```bash
journalctl -u cron
```

---

**Conceptos clave:**

- **Procedimiento de resolución de problemas:** Cuando una tarea no funciona correctamente es recomendable seguir un proceso ordenado.

### Verificar scripts

*Cuando una tarea ejecuta un script, conviene comprobar que este funciona correctamente por separado.*

```bash
./backup.sh
```
```powershell
.\backup.ps1
```

---

**Conceptos clave:**

- **Comprobar permisos:** Muchas incidencias están relacionadas con permisos insuficientes.

---

[⬆️ Volver al índice](#índice)
