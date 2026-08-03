# Planificación de tareas

## Introducción

La planificación de tareas permite automatizar la ejecución de programas, scripts y procesos en momentos determinados o cuando ocurre un evento específico. Gracias a esta funcionalidad es posible realizar tareas repetitivas sin intervención del usuario, mejorando la eficiencia, reduciendo errores y garantizando que determinadas operaciones se ejecuten siempre en el momento adecuado.

Tanto Windows como Linux incorporan herramientas para programar tareas de forma sencilla. En Windows destaca el **Programador de tareas (Task Scheduler)**, mientras que en Linux las herramientas más utilizadas son **cron** y **systemd timers**. Estas soluciones permiten automatizar desde copias de seguridad y actualizaciones hasta scripts de mantenimiento o monitorización.

## Índice

- [Concepto de planificación de tareas](#concepto-de-planificación-de-tareas)
- [Ventajas de automatizar tareas](#ventajas-de-automatizar-tareas)
- [Tipos de desencadenadores (Triggers)](#tipos-de-desencadenadores-triggers)
- [Acciones programadas](#acciones-programadas)
- [Condiciones y configuración de las tareas](#condiciones-y-configuración-de-las-tareas)
- [Programador de tareas en Windows](#programador-de-tareas-en-windows)
- [Administración mediante PowerShell](#administración-mediante-powershell)
- [Administración mediante schtasks](#administración-mediante-schtasks)
- [Cron en Linux](#cron-en-linux)
- [Systemd Timers](#systemd-timers)
- [Monitorización y resolución de problemas](#monitorización-y-resolución-de-problemas)

---

## Concepto de planificación de tareas

### ¿Qué es la planificación de tareas?

La planificación de tareas consiste en programar la ejecución automática de una acción cuando se cumple una condición determinada.

La condición puede ser, por ejemplo:

- Una fecha concreta.
- Una hora determinada.
- El inicio de un sistema.
- El inicio de sesión de un usuario.
- La aparición de un evento específico.

Cuando la condición se cumple, el sistema operativo ejecuta automáticamente la tarea configurada.

---

### ¿Para qué sirve?

La planificación de tareas permite automatizar numerosas operaciones administrativas.

Entre las más habituales se encuentran:

- Copias de seguridad.
- Actualizaciones automáticas.
- Limpieza de archivos temporales.
- Ejecución de scripts.
- Generación de informes.
- Reinicio de servicios.
- Monitorización de sistemas.
- Sincronización de archivos.
  
De esta forma se reduce el trabajo manual y se mejora la eficiencia.

---

### Funcionamiento básico

El funcionamiento de una tarea programada puede representarse de la siguiente manera:


```text
Se configura la tarea

↓

Se establece un desencadenador

↓

Llega el momento o se produce el evento

↓

El sistema ejecuta la tarea automáticamente

↓

Finaliza la ejecución
```

Todo el proceso se realiza sin necesidad de intervención del usuario.

---

### Elementos de una tarea programada

Una tarea programada suele estar formada por varios componentes:

- **Nombre**, que identifica la tarea.
- **Desencadenador (Trigger)**, que indica cuándo debe ejecutarse.
- **Acción**, que define qué debe hacer.
- **Condiciones**, que deter,inan cuándo puede ejecutarse.
- **Configuración adicional**, que establece el comportamiento de la tarea.

Estos elementos permiten adoptar la automatización a diferentes necesidades.

---

### Sistemas de planificación 

Los principales sistemas utilizados son:

#### Windows

- Programador de tareas.
- PowerShell.
- `schtasks`.

#### Linux

- Cron.
- Crontab.
- systemd Timers.

Cada uno ofrece herramientas para crear, modificar y administrar tareas programadas.

---

### Ejemplos de uso

Algunos ejemplos habituales de planificacion de tareas son:

- Ejecutar una copia de seguridad todos los días a las 02:00.
- Reiniciar un servicio cada domingo.
- Limpiar archivos temporales semanalmente.
- Ejecutar un script al iniciar el sistema.
- Enviar un informe automáticamente cada lunes.

Toda estas tareas pueden realizarse sin intervención del administrador una vez configuradas.

---

### Importancia de la planificación de tareas

La automatización aporta numerosas ventajas en la administración de sistemas.

Permite:

- Reducir errores humanos.
- Ahorrar tiempo.
- Garantizar la ejecución periódica de tareas.
- Mejorar el mantenimiento del sistema.
- Aumentar la disponibilidad de los servicios.

Por ello, la planifición de taeas es una herramienta imprescindible en cualquier entorno profesional.

---

[⬆️ Volver al índice](#índice)

## Ventajas de automatizar tareas.

### Ahorro de tiempo

Una de las principales ventakas consiste en eliminar la necesidad de ejecutar manualmente tareas repetitivas.

Por ejemplo:

- Copias de seguridad.
- Limpieza de archivos temporales.
- Actualizaciones.
- Generación de informes.
- Reinicio de servicios.

Una vez programadas, estas tareas se ejecutan automáticamente.

---

### Reducción de errores humanos

Las tareas realizadas manualmente pueden provocar errores como:

- Olvidar ejecutar un proceso.
- Introducir comandos incorrectos.
- Ejecutar acciones en un momento inadecuado.
- Ominit algún paso del procedimiento.

La automatización garantiza que siempre se siga el mismo proceso previamente configurado.

---

### Mayor productividad

Al automatizar las tareas rutinarias, los administradores pueden dedicar su tiempo a actividades de mayor valor, como:

- Resolver incidencias.
- Mejorar la infraestructura.
- Implementar nuevas soluciones.
- Analizar problemas de rendimiento.
- Incrementar la seguridad del sistema.

Esto aumenta la productividad tanto del personal como de la organización.

---

### Ejecución programada

Las tareas pueden ejecutarse exactamente cuando sea necesario.

Algunos ejemplos son:

- Todos los días a las 02:00.
- Cada domingo.
- El primer día de cada mes.
- Al iniciar el sistema.
- Al iniciar sesión un usuario.

Esto permite realizar operaciones en horarios de baja actividad sin afectar a los usuarios.

---

### Funcionamiento continuo

Las tareas programadas pueden ejecutarse incluso cuando ningún usuario ha iniciado sesión.

Esto resulta especialmente útil en:

- Servidores.
- Sistemas de monitorización.
- Equipos que permanecen encendidos de forma permanente.
  
De esta manera, la automatización funciona de forma continua e independiente del usuario.

---

### Mayor disponilidad

Muchas tareas de mantenimiento pueden ejecutarse automáticamente para mantener el sistema operativo en buen estado.

Por ejemplo:

- Libear espacio en disco.
- Reiniciar servicios.
- Eliminar archivos temporales.
- Comprobar el estado del sistema.

Esto contribuye a mejorar la disponiblidad y estabilidad del sistema.

---

### Estandarización de procesos

La automatización garantiza que una misma tarea siempre se ejecute siguiendo exactamente el mismo procedimiento.

Esto proporciona:

- Uniformidad.
- Consistencia.
- Facilidad para documentar procesos.
- Mayor calidad en la administración.

---

### Escalabilidad

En una organización pequeña puede se rposible realidad determinadas tareas manualmente.

Sin embargo, cuando existen docenas o cientos de equipos, la automatización permite administrar todos ellos de forma mucho más eficiente.

Por ello, es una práctica fundamental en entornos empresariales.

---

### Ejemplos de automatización

Algunas tareas que suelen automatizarse son:

- Copias de seguridad.
- Actualizaciones del sistema.
- Reinicio de servicios.
- Ejecución de scripts.
- Limpieza de registros.
- Sincronización de archivos.
- Envío de informes.
- Comprobación del estado del sistema.

Estas automatizaciones reducen considerablemente la carga de trabajo del administrador.

---

[⬆️ Volver al índice](#índice)

## Tipos de desencadenadores (Triggers)

### ¿Qué es un desencadenador? 

El desencadenador es el elemento que indica al sistema operativo el momento exacto en el que debe iniciarse una tarea.

Una misma tarea puede tener uno o varios desencadenadores asociados.

---

### Desencadenadores basados en el tiempo

Son los más utilizados y permiten ejecutar una tarea según una programación establecida.

Por ejemplos:

- Una única vez.
- Diariamente.
- Semanalmente.
- Mensualmente.
- Cada cierto número de horas o minutos.

Ejemplo: 

```text
Todos los días

↓

02:00

↓

Ejecutar copia de seguridad
```

---

### Desencadenadores al iniciar el sistema

Permiten ejecutar una tarea cuando el sistema operativo finaliza su proceso de arranque.

Se utilizan para:

- Iniciar scripts.
- Comprobar el estado del sistema.
- Reiniciar servicios.
- Ejecutar tareas de mantenimiento.

Este tipo de desencadenadores funciona aunque ningún usuario haya iniciado sesión.

---

### Desencadenadores al inciar sesión

La tarea se ejecuta cuando el usuario inicia sesión en el sistema.

Para configurarse para:

- Todos los usuarios.
- Un usuario concreto.

Algunos ejemplos de uso son:

- Ejecutar aplicaciones automáticamente.
- Configurar el entorno de trabajo.
- Sincronizar archivos.
- Conectar unidades de red.

---

### Desenadenadores por inactividad

Algunas tareas pueden ejecutarse cuando el equipo permanece inactivo durante un tiempo determinado.

Esto resulta útil para realizar tareas que consumen recursos, como:

- Desfragmentación de discos.
- Limpieza del sistema.
- Análisis antivirus.
- Copias de seguridad.

Así se evita afectar al rendimiento mientras el usuario está trabajando.

---

### Desencadenadores por eventos

También es posible iniciar una tarea cuando ocurre un determinado evento del sistema.

Por ejemplo:

- Error de un servicio.
- Instalación de una aplicación.
- Inicio o cierre de sesión.
- Aparición de un evento concreto en el registro del sistema.

Este tipo de automatización es muy útil para responder rápidamente ante incidencias.

---

### Múltiples desencadenadores

Una misma tarea puede disponer de varios desencadenadores.

Ejemplo:

```text
Tarea de copia de seguridad

├── Todos los días a las 22:00

└── Al iniciar el sistema
```

La tarea se ejecutará cuando se cumpla cualquiera de las condiciones configuradas.

---

### Desencadenadores en Windows

El Programador de tareas de Windows permite utilizar desencadenadores como:

- Según una programación.
- Al iniciar el sistema.
- Al iniciar sesión.
- Al bloquear o desbloquear el equipo.
- Cuando se produce un evento.
- Al crear o modificar una tarea.

Esta flexibilidad permite automatizar numerosas operaciones administrativas.

---

### Desencadenadores en Linux

En Linux, herramientas como **cron** y **systemd timers** utilizan principalmente desencadenadores relacionados con el tiempo.

Algunos ejemplos son:

- Cada hora.
- Cada día.
- Cada semana.
- Cada mes.
- En una fecha concreta.

Con **systemd** también es posible utilizar desencadenadores relacionados con el arranque del sistema y otros eventos.

---

[⬆️ Volver al índice](#índice)

## Acciones programadas

### ¿Qué es una acción?

Una **acción** es la operación que ejecutará una tarea programada cuando sea activada por uno de sus Triggers.

En otras palabras:

```text
Desencadenador

↓

Se cumple la condición

↓

Ejecutar acción
```

Sin una acción definida, la tarea no realizará ninguna operación.

---

### Tipos de acciones

Dependiendo del sistema operativo y de la herramienta utilizada, pueden ejecutarse diferentes tipos de accicones.

Las más habituales son:

- Ejecutar un programa.
- Ejecutar un script.
- Ejecutar un comando.
- Iniciar un servicio.
- Detener un servicio.
- Reiniciar un servicio.
- Ejecutar tareas de mantenimiento.

Estas acciones permiten automatizar prácticamente cualquier tarea administrativa.

---

### Ejecutar programas

Una de las acciones más comunes consiste en abrir una aplicación determinada.

Ejemplos:

- Bloc de notas.
- Calculadora.
- Navegador web.
- Aplicaciones corporativas.

Ejemplo: 

```text
08:00

↓

Abrir aplicación de gestión
```

---

### Ejecutar scripts

Las tareas programadas también pueden ejecutar scripts creados por el administrador.

Por ejemplo:

- Scripts de PowerShell.
- Archivos Batch (.bat).
- Scripts Bash (.sh).
- Scripts Python.

Esto permite automatizar procesos complejos mediante un único archivo.

---

### Ejecutar comandos

Otra posibilidad consiste en ejecutar directamente comandos del sistema operativo.

Ejemplos en Windows:

```cmd
ipconfig /flushdns
```

```cmd
gpupdate /force
```

Ejemplos en Linux:

```bash
apt update
```

```bash
systemctl restart apache2
```

Esta opción resulta especialmente útil para tareas de mantenimiento.

---

### Administrar servicios

Las tareas programadas pueden utilizarse para administrar servicios automáticamente.

Por ejemplo:

- Iniciar un servicio.
- Detener un servicio.
- Reiniciar un servicio.

Ejemplo:

```text
Domingos

↓

03:00

↓

Reiniciar servicio web
```

---

### Ejecutar copias de seguridad

Una de las aplicaciones más habituales consiste en automatizar las copias de seguridad.

Ejemplo:

```text
Todos los días

↓

02:00

↓

Ejecutar script de copia

↓

Guardar registro
```

De esta forma se garantiza que la copia se realiza siempre a la misma hora.

---

### Ejecutar tareas de mantenimiento

Muchas operaciones de mantenimiento pueden automatizarse.

Por ejemplo:

- Limpieza de archivos temporales.
- Eliminación de registros antiguos.
- Optimización del sistema.
- Actualización de aplicaciones.
- Comprobación del estado del disco.

Esto reduce considerablemente el trabajo manual del administrador.

---

### Acciones en Windows

En el Programador de tareas de Windows, la acción más habitual es:

- **Iniciar un programa**.

Desde esta opción pueden ejecutarse:

- Ejecutables (.exe).
- Scripts (.ps1, .bat, .cmd).
- Comandos del sistema.

También es posible indicar parámetros y el directorio de trabajo.

---

### Acciones en Linux

En Linux, las acciones suelen ejecutarse mediante:

- Cron.
- Systemd Timers.
- Scripts Bash.

Algunos ejemplos son:

```bash
/usr/local/scripts/backup.sh
```

```bash
python3 informe.py
```

```bash
systemctl restart nginx
```

Estas acciones se ejecutan automáticamente cuando llega el momento programado.

---

[⬆️ Volver al índice](#índice)

## Condiciones y configuración de las tareas

### ¿Qué son las condiciones?

Las **condiciones** son requisitos adicionales que deben cumplirse para que una tarea pueda ejecutarse.

Aunque el Trigger se active, la tarea solo comenzará si también se cumplen las condiciones establecidas.

Por ejemplo:

```text
Son las 02:00

↓

El equipo está funcionando

↓

Se cumplen las condiciones

↓

Se ejecuta la tarea
```

---

### Condición de inactividad

Una tarea puede configurarse para ejecutarse únicamente cuando el equipo permanezca inactivo durante un tiempo determinado.

Esto resulta útil para tareas que consumen muchos recursos, como:

- Copias de seguridad.
- Análisis antivirus.
- Limpieza del sistema.
- Optimización de discos.
  
Así se evita afectar el rendimiento mientras el susuario está trabajando.

---

### Condición de alimentación

En equipos portátiles es posible indicar que una tarea solo se ejecute cuando el dispositivo esté conectado a la corriente eléctrica.

Esta opción evita un consumo innecesario de batería durante tareas de larga duración.

También puede configurarse para detener la tarea si el equipo pasa a funcionar con batería.

---

### Condición de conexión de red

Algunas tareas requieren acceso a recursos de red o a Internet.

En estos casos puede establecerse que la tarea solo se ejecute cuando exista una conexión de red disponible.

Ejemplos:

- Sincronización de archivos.
- Copias de seguridad en servidores remotos.
- Descarga de actualizaciones.
- Envío de informes.

---

### Repetición de la tarea

Es posible indicar que una tarea se repita automáticamente dentro de un intervalo de tiempo.

Por ejemplo:

- Cada 15 minutos.
- Cada hora.
- Cada 6 horas.

Esto resulta útil para tareas de monitorización o supervisión continua.

---

### Tiempo máximo de ejecución

Puede establecerse un límite de tiempo para impedir que una tarea permanezca ejecutándose indefinidamente.

Si supera ese tiempo:

```text
Tiempo máximo alcanzado

↓

Finalizar tarea automáticamente
```

Esta opción ayuda a evitar procesos bloqueados o consumos excesivos de recursos.

---

### Comportamiento ante errores

Las tareas programadas pueden configurarse para actuar cuando se produce un error.

Algunas opciones habituales son:

- Reintentar la ejecución.
- Ejecutar la tarea lo antes posible si se perdió una ejecución.
- Finalizar la tarea si permanece bloqueada.
- Registrar el error para su revisión.

Estas configuraciones aumentan la fiabilidad de la automatización.

---

### Configuración en Windows

El Programador de tareas de Windows incluye varias pestañas para configurar una tarea.

Las principales son:

- General.
- Desencadenadores.
- Acciones.
- Condiciones.
- Configuración.

Desde ellas es posible controlar todos los aspectos relacionados con la ejecución de la tarea.

---

### Configuración en Linux

En Linux, herramientas como **cron** ofrecen una configuración más sencilla centrada en la programación temporal.

En cambio, **systemd timers** permiten añadir opciones más avanzadas relacionadas con:

- Dependencias.
- Reinicio automático.
- Tiempo máximo de ejecución.
- Condiciones de inicio.

Esto proporciona una mayor flexibilidad en entornos profesionales.

---

[⬆️ Volver al índice](#índice)

## Programador de tareas en Windows

Introducción

El **Programador de tareas** (*Task Scheduler*) es la herramienta integrada en Windows que permite crear, modificar y administrar tareas programadas. Gracias a ella es posible automatizar la ejecución de programas, scripts y tareas de mantenimiento sin necesidad de intervención del usuario.

Se trata de una herramienta fundamental para administradores de sistemas, ya que facilita la automatización de procesos repetitivos y la gestión eficiente de equipos y servidores.

---

### ¿Qué es el Programador de tareas?

El Programador de tareas es una consola de administración que permite programar la ejecución automática de tareas basadas en:

- Una fecha y hora.
- Un intervalo de tiempo.
- El inicio del sistema.
- El inicio de sesión de un usuario.
- Un evento del sistema.

Cada tarea queda almacenada en el sistema y se ejecuta automáticamente cuando se cumplen las condiciones configuradas.

---

### Abrir el Programador de tareas

Existen varias formas de acceder a esta herramienta.

Desde **Ejecutar**:

```text
taskschd.msc
```

O bien desde:

```text
Panel de control

↓

Herramientas de Windows

↓

Programador de tareas
```

También puede localizarse desde el menú Inicio buscando:

```text
Programador de tareas
```

---

### Interfaz principal

La consola se divide en varias zonas.

- **Panel izquierdo:** árbol de carpetas con las tareas.
- **Panel central:** listado de tareas y su información.
- **Panel derecho:** acciones disponibles.

Desde esta interfaz pueden administrarse tanto las tareas creadas por el usuario como las propias del sistema operativo.

---

### Crear una tarea básica

Windows ofrece un asistente para crear tareas sencillas.

Pasos generales:

```text
Acción

↓

Crear tarea básica

↓

Asignar nombre

↓

Elegir desencadenador

↓

Seleccionar acción

↓

Finalizar
```

Esta opción es recomendable para tareas simples.

---

### Crear una tarea avanzada

Para disponer de todas las opciones de configuración puede utilizarse:

```text
Acción

↓

Crear tarea
```

Esta modalidad permite configurar:

- General.
- Desencadenadores.
- Acciones.
- Condiciones.
- Configuración.

Es la opción más utilizada por los administradores.

---

### Administrar tareas existentes

Sobre una tarea ya creada pueden realizarse diferentes acciones.

Entre ellas:

- Ejecutar.
- Finalizar.
- Deshabilitar.
- Eliminar.
- Exportar.
- Ver propiedades.

Esto permite modificar fácilmente cualquier tarea cuando cambian las necesidades del sistema.

---

### Historial de tareas

El Programador de tareas puede registrar el historial de ejecución de cada tarea.

Desde este historial es posible consultar:

- Fecha de ejecución.
- Resultado.
- Errores producidos.
- Hora de inicio y finalización.

Esta información resulta muy útil para diagnosticar incidencias.

---

### Biblioteca del Programador de tareas

Todas las tareas creadas se almacenan en la **Biblioteca del Programador de tareas**.

En ella aparecen:

- Tareas del sistema.
- Tareas creadas por aplicaciones.
- Tareas creadas por el administrador.

Es recomendable organizar las tareas en carpetas cuando se administran numerosos procesos automatizados.

---

### Ejemplos de uso

El Programador de tareas suele utilizarse para:

- Ejecutar scripts de PowerShell.
- Ejecutar archivos Batch.
- Automatizar copias de seguridad.
- Reiniciar servicios.
- Ejecutar programas al iniciar sesión.
- Limpiar archivos temporales.
- Generar informes automáticamente.

Estas tareas ayudan a reducir la carga de trabajo del administrador.

---

### Ventajas del Programador de tareas

Entre sus principales ventajas destacan:

- Interfaz gráfica sencilla.
- Gran flexibilidad de configuración.
- Compatibilidad con scripts y aplicaciones.
- Registro del historial de ejecución.
- Integración con el sistema operativo.
- Posibilidad de automatizar prácticamente cualquier tarea.

Por ello es una herramienta ampliamente utilizada en entornos Windows.

---

[⬆️ Volver al índice](#índice)

## Administración mediante PowerShell

Introducción

PowerShell permite administrar tareas programadas desde la línea de comandos mediante una colección de cmdlets específicos. Esta funcionalidad resulta especialmente útil para automatizar la creación y gestión de tareas, administrar múltiples equipos o integrar la planificación de tareas dentro de scripts de administración.

Gracias a PowerShell es posible realizar prácticamente las mismas operaciones que desde el Programador de tareas, pero de forma mucho más rápida y automatizable.

---

### Obtener todas las tareas programadas

Para listar todas las tareas registradas en el sistema:

```powershell
Get-ScheduledTask
```

La información mostrada incluye:

- Nombre de la tarea.
- Estado.
- Ruta.
- Descripción.

Este cmdlet es el punto de partida para administrar tareas mediante PowerShell.

---

### Consultar una tarea concreta

Para obtener información sobre una tarea específica:

```powershell
Get-ScheduledTask -TaskName "Backup Diario"
```

También puede indicarse la carpeta donde se encuentra:

```powershell
Get-ScheduledTask -TaskPath "\Microsoft\Windows\"
```

---

### Consultar el estado de una tarea

Para conocer el estado de ejecución de una tarea:

```powershell
Get-ScheduledTaskInfo -TaskName "Backup Diario"
```

Entre la información mostrada se encuentra:

- Última ejecución.
- Próxima ejecución.
- Resultado de la última ejecución.
- Tiempo de ejecución.

---

### Ejecutar una tarea manualmente

Para iniciar una tarea sin esperar a que se active su desencadenador:

```powershell
Start-ScheduledTask -TaskName "Backup Diario"
```

Esta opción resulta útil para comprobar que la tarea funciona correctamente.

---

### Detener una tarea

Si una tarea está en ejecución y es necesario finalizarla:

```powershell
Stop-ScheduledTask -TaskName "Backup Diario"
```

Debe utilizarse únicamente cuando sea necesario interrumpir la ejecución.

---

### Deshabilitar una tarea

Para impedir temporalmente que una tarea se ejecute:

```powershell
Disable-ScheduledTask -TaskName "Backup Diario"
```

La tarea permanecerá registrada, pero no volverá a ejecutarse hasta ser habilitada de nuevo.

---

### Habilitar una tarea

Para volver a activar una tarea previamente deshabilitada:

```powershell
Enable-ScheduledTask -TaskName "Backup Diario"
```

Recuperará su funcionamiento normal según la programación establecida.

---

### Crear una tarea programada

PowerShell también permite crear tareas mediante scripts.

Ejemplo sencillo:

```powershell
$Action = New-ScheduledTaskAction -Execute "notepad.exe"

$Trigger = New-ScheduledTaskTrigger -Daily -At 09:00

Register-ScheduledTask -TaskName "Abrir Bloc de notas" -Action $Action -Trigger $Trigger
```

Este script crea una tarea que abrirá el Bloc de notas todos los días a las 09:00.

---

### Eliminar una tarea

Para eliminar una tarea existente:

```powershell
Unregister-ScheduledTask -TaskName "Backup Diario"
```

Si se desea evitar la confirmación:

```powershell
Unregister-ScheduledTask -TaskName "Backup Diario" -Confirm:$false
```

Una vez eliminada, la tarea dejará de existir en el sistema.

---

### Automatización mediante scripts

Una de las mayores ventajas de PowerShell es la posibilidad de administrar múltiples tareas de forma automática.

Por ejemplo:

```powershell
Get-ScheduledTask | Where-Object State -eq "Disabled"
```

Este comando muestra únicamente las tareas que se encuentran deshabilitadas.

También pueden combinarse cmdlets para crear informes o modificar varias tareas simultáneamente.

---

[⬆️ Volver al índice](#índice)

## Administración mediante shtasks

### ¿Qué es schtasks?

`schtasks` es un comando integrado en Windows que permite administrar tareas programadas desde el **Símbolo del sistema (CMD)**.

Su sintaxis general es:

```cmd
schtasks [operación] [parámetros]
```

Con este comando es posible:

- Crear carpetas.
- Consultar tareas existentes.
- Ejecutarlas manualmente.
- Modificarlas.
- Eliminarlas.

---

### Consultar tareas programadas

Para mostrar todas las tareas registradas:

```cmd
schtasks /query
```

La salida incluye información como:

- Nombre de la tarea.
- Estado.
- Próxima ejecución.

---

### Mostrar información detallada

Si se desea obtener más información:

```cmd
schtasks /query /v
```

También puede utilizarse el formato de lista:

```cmd
schtasks /query /fo LIST /v
```

Esta opción muestra información detallada sobre cada tarea programada.

---

### Crear una tarea

Para crear una tarea que abra el Bloc de notas todos los días a las 09:00:

```cmd
schtasks /create /tn "Abrir Bloc" /tr "notepad.exe" /sc daily /st 09:00
```

Los parámetros más utilizados son:

- `/tn` → Nombre de la tarea.
- `/tr` → Programa o comando que se ejecutará.
- `/sc` → Frecuencia de ejecución.
- `/st` → Hora de inicio.

---

### Ejecutar una tarea manualmente

Para iniciar una tarea sin esperar a su programación:

```cmd
schtasks /run /tn "Abrir Bloc"
```

Esta opción resulta útil para comprobar que la tarea funciona correctamente.

---

### Modificar una tarea

Es posible cambiar algunos parámetros de una tarea existente mediante:

```cmd
schtasks /change
```

Por ejemplo, modificar el usuario con el que se ejecuta:

```cmd
schtasks /change /tn "Abrir Bloc" /ru Administrador
```

No todos los parámetros pueden modificarse directamente; en algunos casos es necesario eliminar la tarea y volver a crearla.

---

### Eliminar una tarea

Para eliminar una tarea:

```cmd
schtasks /delete /tn "Abrir Bloc"
```

Si se desea evitar la confirmación:

```cmd
schtasks /delete /tn "Abrir Bloc" /f
```

Una vez eliminada, dejará de aparecer en el Programador de tareas.

---

### Frecuencias disponibles

El parámetro `/sc` permite definir diferentes tipos de programación.

Las opciones más habituales son:

- `once` → Una sola vez.
- `daily` → Diariamente.
- `weekly` → Semanalmente.
- `monthly` → Mensualmente.
- `onstart` → Al iniciar el sistema.
- `onlogon` → Al iniciar sesión.

Estas opciones permiten adaptar la programación a distintas necesidades.

---

### Ventajas de schtasks

Entre sus principales ventajas destacan:

- Disponible en todas las versiones modernas de Windows.
- Fácil integración en scripts Batch.
- Administración desde CMD.
- Posibilidad de gestionar tareas de forma remota.
- Compatibilidad con herramientas de automatización.

Por ello continúa siendo una herramienta muy utilizada.

---

[⬆️ Volver al índice](#índice)

## Cron en Linux

Introducción

**Cron** es el sistema tradicional de planificación de tareas en Linux y otros sistemas Unix. Permite ejecutar comandos, programas o scripts automáticamente en fechas y horas determinadas, siendo una de las herramientas más utilizadas para automatizar tareas administrativas en servidores.

Aunque actualmente muchas distribuciones incorporan **systemd timers**, Cron continúa siendo ampliamente utilizado por su sencillez, fiabilidad y compatibilidad.

---

### ¿Qué es Cron?

Cron es un servicio que permanece ejecutándose en segundo plano y comprueba continuamente si existe alguna tarea programada que deba ejecutarse.

Cuando llega la fecha y la hora configuradas, Cron ejecuta automáticamente el comando correspondiente.

Su funcionamiento puede representarse así:

```text
Cron

↓

Comprueba la programación

↓

Llega la hora indicada

↓

Ejecuta la tarea
```

---

### ¿Qué es Crontab?

Las tareas programadas se almacenan en un archivo denominado **crontab**.

Cada usuario puede disponer de su propio archivo de programación.

Para editar el crontab del usuario actual:

```bash
crontab -e
```

Para visualizar las tareas existentes:

```bash
crontab -l
```

Eliminar todas las tareas programadas del usuario:

```bash
crontab -r
```

### Sintaxis de Cron

Cada línea del archivo **crontab** representa una tarea programada.

Su estructura es:

```test
Minuto Hora Día Mes Día_semana Comando
```

Ejemplo:

```bash
30 2 * * * /home/admin/backup.sh
```

Este ejemplo ejecutará el script todos los días a las **02:30**.

---

### Significado de los campos

Cada campo representa una parte de la programación.

| Campo | Valores |
|--------|----------|
| Minuto | 0-59 |
| Hora | 0-23 |
| Día del mes | 1-31 |
| Mes | 1-12 |
| Día de la semana | 0-7 (0 y 7 = domingo) |

Después de estos cinco campos se escribe el comando o script que se ejecutará.

---

### Caracteres especiales

Cron permite utilizar varios caracteres para simplificar la programación.

Asterisco:

```text
*
```

Significa **todos los valores posibles**.

Ejemplo:

```bash
* * * * *
```

Ejecuta la tarea cada minuto.

---

Coma:

```text
,
```

Permite indicar varios valores.

Ejemplo:

```bash
0 8,16 * * *
```

Ejecuta la tarea a las 08:00 y a las 16:00.

---

Guion:

```text
-
```

Indica un rango.

Ejemplo:

```bash
0 9-17 * * *
```

Ejecuta la tarea cada hora desde las 09:00 hasta las 17:00.

---

Barra:

```text
/
```

Permite indicar intervalos.

Ejemplo:

```bash
*/15 * * * *
```

Ejecuta la tarea cada 15 minutos.

---

### Ejemplos de programación

Todos los días a las 03:00:

```bash
0 3 * * * /home/admin/backup.sh
```

Todos los lunes a las 08:00:

```bash
0 8 * * 1 /home/admin/informe.sh
```

El primer día de cada mes:

```bash
0 0 1 * * /home/admin/limpieza.sh
```

Cada 30 minutos:

```bash
*/30 * * * * /home/admin/script.sh
```

---

### Ubicación de los archivos

Además del crontab de cada usuario, Linux dispone de otros archivos relacionados con Cron.

Los más habituales son:

```text
/etc/crontab
```

```text
/etc/cron.daily/
```

```text
/etc/cron.weekly/
```

```text
/etc/cron.monthly/
```

Estas ubicaciones permiten organizar tareas de administración del sistema.

---

### Comprobar el servicio Cron

En sistemas con **systemd**, puede comprobarse el estado del servicio mediante:

```bash
systemctl status cron
```

En algunas distribuciones el servicio recibe el nombre:

```bash
systemctl status crond
```

Si el servicio no está funcionando, ninguna tarea programada se ejecutará.

---

[⬆️ Volver al índice](#índice)

## Systemd Timers

Introducción

Aunque **Cron** continúa siendo una herramienta muy utilizada para programar tareas en Linux, muchas distribuciones modernas utilizan **systemd timers** como alternativa. Los *timers* forman parte de **systemd** y permiten programar la ejecución automática de servicios con una integración mucho mayor con el sistema operativo.

Gracias a esta integración, ofrecen más opciones de configuración, un mejor control de las dependencias y una administración unificada junto con el resto de servicios del sistema.

---

### ¿Qué es un Systemd Timer?

Un **Systemd Timer** es una unidad de **systemd** que permite ejecutar automáticamente un servicio cuando se cumple una determinada condición temporal.

Su funcionamiento puede representarse de la siguiente forma:

```text
Timer

↓

Llega el momento programado

↓

Ejecutar servicio asociado
```

A diferencia de Cron, un timer no ejecuta directamente un comando, sino un **servicio (.service)**.

---

### Archivos utilizados

Para utilizar un timer normalmente se crean dos archivos:

- Un archivo **.service**, que define la tarea a ejecutar.
- Un archivo **.timer**, que define cuándo debe ejecutarse.

Ejemplo:

```text
backup.service
```

```text
backup.timer
```

Ambos archivos suelen almacenarse en:

```text
/etc/systemd/system/
```

---

### Estructura de un servicio

El archivo **.service** contiene la acción que realizará la tarea.

Ejemplo:

```ini
[Unit]
Description=Copia de seguridad

[Service]
Type=oneshot
ExecStart=/opt/scripts/backup.sh
```

En este ejemplo, el servicio ejecutará un script de copia de seguridad.

---

### Estructura de un timer

El archivo **.timer** define la programación.

Ejemplo:

```ini
[Unit]
Description=Ejecutar copia de seguridad diariamente

[Timer]
OnCalendar=daily

[Install]
WantedBy=timers.target
```

En este caso, el servicio se ejecutará una vez al día.

---

### Activar un timer

Una vez creados los archivos, el timer puede habilitarse mediante:

```bash
sudo systemctl enable backup.timer
```

Después puede iniciarse:

```bash
sudo systemctl start backup.timer
```

A partir de ese momento comenzará a controlar la ejecución automática del servicio.

---

### Consultar timers

Para visualizar todos los timers activos:

```bash
systemctl list-timers
```

La salida muestra información como:

- Próxima ejecución.
- Última ejecución.
- Servicio asociado.
- Estado.

Esto facilita comprobar si la programación es correcta.

---

### Consultar el estado

Para comprobar el estado de un timer:

```bash
systemctl status backup.timer
```

También puede consultarse el estado del servicio asociado:

```bash
systemctl status backup.service
```

---

### Deshabilitar un timer

Si se desea impedir que continúe ejecutándose automáticamente:

```bash
sudo systemctl disable backup.timer
```

Y para detenerlo inmediatamente:

```bash
sudo systemctl stop backup.timer
```

---

### Ventajas frente a Cron

Los **Systemd Timers** ofrecen varias ventajas respecto a Cron.

Entre ellas:

- Integración completa con systemd.
- Mejor control de dependencias.
- Gestión mediante `systemctl`.
- Registro automático mediante `journalctl`.
- Mayor flexibilidad de configuración.
- Mejor administración de servicios.

Por ello, muchas distribuciones modernas los utilizan como alternativa a Cron.

---

### Cron vs Systemd Timers

| Cron | Systemd Timers |
|------|----------------|
| Ejecuta comandos directamente. | Ejecuta servicios de systemd. |
| Configuración sencilla. | Configuración más avanzada. |
| Basado en crontab. | Basado en archivos `.service` y `.timer`. |
| Muy extendido. | Integrado con systemd. |
| Menor control sobre dependencias. | Mayor control y flexibilidad. |

---

[⬆️ Volver al índice](#índice)

## Monitorización y resolución de problemas

Introducción

Una vez que una tarea programada ha sido creada, es importante supervisar su funcionamiento para comprobar que se ejecuta correctamente y detectar posibles errores. Una tarea mal configurada o que no se ejecuta cuando corresponde puede provocar fallos en procesos críticos como copias de seguridad, actualizaciones o generación de informes.

La monitorización periódica y un procedimiento ordenado de resolución de problemas permiten garantizar el correcto funcionamiento de la automatización.

---

### ¿Por qué monitorizar las tareas programadas?

La supervisión de las tareas permite:

- Comprobar que se ejecutan correctamente.
- Detectar errores de ejecución.
- Verificar los tiempos de ejecución.
- Confirmar que la programación es correcta.
- Identificar tareas que ya no son necesarias.

Una revisión periódica evita que pequeños errores pasen desapercibidos durante largos periodos de tiempo.

---

### Problemas habituales

Las incidencias más frecuentes son:

- La tarea no se ejecuta.
- El script contiene errores.
- La programación es incorrecta.
- El usuario no tiene permisos suficientes.
- El archivo o programa ya no existe.
- El servicio de planificación está detenido.
- Existen errores en las rutas especificadas.

Identificar correctamente la causa facilita la resolución del problema.

---

### Monitorización en Windows

En Windows pueden utilizarse diferentes herramientas.

Las principales son:

- Programador de tareas.
- Historial de tareas.
- Visor de eventos.
- PowerShell.

Para consultar información mediante PowerShell:

```powershell
Get-ScheduledTaskInfo -TaskName "Backup Diario"
```

Este cmdlet muestra:

- Última ejecución.
- Próxima ejecución.
- Resultado.
- Duración.

---

### Historial del Programador de tareas

El Programador de tareas permite registrar todas las ejecuciones realizadas.

Desde el historial pueden consultarse:

- Inicio de la tarea.
- Finalización.
- Errores.
- Cancelaciones.
- Resultado de la ejecución.

Si el historial está deshabilitado, es recomendable activarlo para facilitar el diagnóstico de incidencias.

---

### Monitorización en Linux

En Linux la supervisión depende de la herramienta utilizada.

Para Cron:

Consultar el contenido del crontab:

```bash
crontab -l
```

Revisar los registros del sistema:

```bash
journalctl -u cron
```

o, en algunas distribuciones:

```bash
journalctl -u crond
```

Para Systemd Timers:

Consultar los timers:

```bash
systemctl list-timers
```

Consultar el estado:

```bash
systemctl status backup.timer
```

Consultar los registros:

```bash
journalctl -u backup.service
```

---

### Procedimiento de resolución de problemas

Cuando una tarea no funciona correctamente es recomendable seguir un proceso ordenado.

```text
Comprobar que la tarea existe

↓

Verificar programación

↓

Revisar permisos

↓

Comprobar rutas y archivos

↓

Consultar registros

↓

Ejecutar manualmente la tarea

↓

Verificar resultado
```

Este procedimiento permite localizar rápidamente el origen de la incidencia.

---

### Verificar scripts

Cuando una tarea ejecuta un script, conviene comprobar que este funciona correctamente por separado.

Por ejemplo:

```bash
./backup.sh
```

o en Windows:

```powershell
.\backup.ps1
```

Si el script falla manualmente, también fallará cuando se ejecute automáticamente.

---

### Comprobar permisos

Muchas incidencias están relacionadas con permisos insuficientes.

Debe comprobarse que:

- El usuario tiene permisos de ejecución.
- Puede acceder a los archivos necesarios.
- Dispone de permisos sobre las carpetas utilizadas.
- Puede acceder a recursos de red si son necesarios.

Una configuración incorrecta de permisos impedirá la ejecución de la tarea.

---

[⬆️ Volver al índice](#índice)