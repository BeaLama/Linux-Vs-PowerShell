# Procesos avanzados

## Introducción

Los procesos son la unidad básica de ejecución de un sistema operativo. En niveles anteriores se han visto las operaciones más habituales, como listar procesos, consultar su consumo de recursos o finalizarlos.

---

## Índice

- [Arquitectura de un proceso](#arquitectura-de-un-proceso)
- [Estados de un proceso](#estados-de-un-proceso)
- [Prioridad y planificación](#prioridad-y-planificación)
- [Afinidad de CPU](#afinidad-de-cpu)
- [Procesos en Linux](#procesos-en-linux)
- [Procesos en Windows](#procesos-en-windows)
- [Señales y finalización de procesos](#señales-y-finalización-de-procesos)
- [Monitorización y depuración](#monitorización-y-depuración)

---

## Arquitectura de un proceso

Un proceso es una instancia de un programa en ejecución.

| 🐧 Linux | 🪟 PowerShell |
|---|---|
| `pstree` | *(no aplica)* |

Cuando un usuario ejecuta una aplicación, el sistema operativo crea un proceso y le asigna los recursos necesarios para que pueda funcionar de forma independiente.

---

### Programa vs proceso

Aunque suelen utilizarse como sinónimos, no significan lo mismo.

#### Programa

Es un conjunto de instrucciones almacenadas en un archivo.

Ejemplos:

```text
notepad.exe
```

Un programa no consume CPU ni memoria hasta que se ejecuta.

---

#### Proceso

Es un programa que ya está ejecutándose.

Ejemplo:

```text
Usuario

↓

Ejecuta Firefox

↓

Se crea un proceso
```

Un mismo programa puede generar varios procesos independientes.

---

[⬆️ Volver al índice](#índice)

## Estados de un proceso

Un proceso no permanece siempre ejecutándose.

| 🐧 Linux | 🪟 PowerShell |
|---|---|
| `ps aux` | *(no aplica)* |

Durante su ciclo de vida puede pasar por distintos **estados**, dependiendo de si está utilizando la CPU, esperando un recurso o ha finalizado su ejecución.

---

### Ciclo de vida de un proceso

De forma simplificada, un proceso pasa por los siguientes estados:

```text
Nuevo

↓

Preparado

↓

Ejecución

↓

Espera

↓

Preparado

↓

Ejecución

↓

Finalizado
```

Un proceso puede alternar varias veces entre **Preparado**, **Ejecución** y **Espera** antes de finalizar.

---

### Estados en Linux

En Linux los procesos muestran una letra que indica su estado.

Las más habituales son:

| Estado | Significado |
|---------|-------------|
| R | Running (ejecutándose o listo para ejecutarse). |
| S | Sleeping (espera interrumpible). |
| D | Espera no interrumpible (normalmente E/S). |
| T | Detenido o trazado. |
| Z | Zombie. |

Consultar procesos:

```bash
ps aux
```

---

### Estado Zombie

Un **Zombie** es un proceso que ya ha terminado, pero cuyo proceso padre todavía no ha recogido su estado de finalización.

Características:

- No ejecuta código.
- No utiliza CPU.
- Conserva su PID.
- Permanece en la tabla de procesos.

En Linux aparece con el estado:

```text
Z
```

Un número elevado de procesos Zombie puede indicar errores de programación.

---

### Estado Huérfano (Orphan)

Un proceso huérfano es aquel cuyo proceso padre finaliza antes que él.

En Linux, estos procesos son adoptados automáticamente por:

```text
init
```

o, en sistemas modernos:

```text
systemd
```

De esta forma pueden finalizar correctamente sin quedar abandonados.

---

### Estados en Windows

Windows no muestra exactamente los mismos estados que Linux, pero internamente también distingue situaciones como:

- Inicialización.
- Preparado.
- En ejecución.
- Espera.
- Suspendido.
- Finalizado.

Herramientas como **Process Explorer** permiten visualizar información mucho más detallada que el Administrador de tareas.

---

[⬆️ Volver al índice](#índice)

## Prioridad y planificación

En un sistema operativo moderno pueden ejecutarse cientos o incluso miles de procesos simultáneamente.

| Linux | Windows |
|--------|----------|
| Nice (-20 a 19) | Clases de prioridad |
| `nice` | Administrador de tareas |
| `renice` | PowerShell |
| Prioridad dinámica | Prioridad dinámica |
| Scheduler CFS (habitualmente) | Scheduler propio de Windows |

---

### Consultar prioridades

Mostrar procesos:

```bash
ps -el
```

O:

```bash
top
```

La columna **NI** indica el valor Nice.

---

### Ejecutar con otra prioridad

Ejecutar un proceso con prioridad baja:

```bash
nice -n 10 comando
```

Ejecutar con prioridad alta (requiere permisos):

```bash
nice -n -10 comando
```

---

### Modificar un proceso existente

Cambiar la prioridad:

```bash
renice 5 -p 1234
```

Ejemplo:

```bash
renice -10 -p 1234
```

---

### Prioridades en Windows

Windows utiliza distintas clases de prioridad.

Las principales son:

- Idle
- Below Normal
- Normal
- Above Normal
- High
- Realtime

La prioridad **Realtime** debe utilizarse únicamente en situaciones muy concretas, ya que puede impedir que otros procesos críticos obtengan tiempo de CPU.

---

### Cambiar prioridad

Administrador de tareas:

```text
Procesos

↓

Detalles

↓

Botón derecho

↓

Establecer prioridad
```

PowerShell:

```powershell
(Get-Process notepad).PriorityClass
```

Modificar prioridad:

```powershell
(Get-Process notepad).PriorityClass = "High"
```

---

[⬆️ Volver al índice](#índice)

## Afinidad de CPU

La **afinidad de CPU** (*CPU Affinity*) permite controlar en qué núcleo o núcleos del procesador puede ejecutarse un proceso.

| Linux | Windows |
|--------|----------|
| `taskset` | Administrador de tareas |
| `ps -o psr` | Establecer afinidad |
| Máscara de CPU | Máscara de CPU |
| Configuración por proceso | Configuración por proceso |

---

### Afinidad en Linux

Consultar el procesador donde se ejecuta un proceso:

```bash
ps -o pid,psr,comm
```

La columna **PSR** indica el núcleo utilizado en ese momento.

---

### Consultar afinidad

```bash
taskset -p PID
```

Ejemplo:

```bash
taskset -p 1234
```

---

### Establecer afinidad

Ejecutar un programa únicamente en el núcleo 0:

```bash
taskset -c 0 comando
```

Ejecutarlo en varios núcleos:

```bash
taskset -c 0,1,2 comando
```

Modificar la afinidad de un proceso existente:

```bash
taskset -cp 0,1 1234
```

---

### Afinidad en Windows

Windows permite modificar la afinidad desde el Administrador de tareas.

Ruta:

```text
Administrador de tareas

↓

Detalles

↓

Botón derecho

↓

Establecer afinidad
```

Se mostrará una lista con todos los procesadores disponibles.

Ejemplo:

```text
☑ CPU 0

☑ CPU 1

☐ CPU 2

☐ CPU 3
```

---

### PowerShell

Consultar un proceso:

```powershell
Get-Process notepad
```

---

[⬆️ Volver al índice](#índice)

## Procesos en Linux

Linux proporciona un amplio conjunto de herramientas para administrar, supervisar y controlar procesos desde la línea de comandos.

---

### Listar procesos

La herramienta más utilizada es:

```bash
ps
```

Mostrar todos los procesos:

```bash
ps aux
```

---

### top

`top` muestra el estado del sistema en tiempo real.

Ejecutar:

```bash
top
```

---

### htop

Versión mejorada de `top`.

Ejecutar:

```bash
htop
```

---

### Buscar procesos

Buscar procesos por nombre:

```bash
pgrep firefox
```

Mostrar información completa:

```bash
ps aux | grep firefox
```

---

### Árbol de procesos

Visualizar relaciones entre procesos:

```bash
pstree
```

---

### Finalizar procesos

Finalizar mediante PID:

```bash
kill 1234
```

---

### Prioridad

Consultar prioridad:

```bash
ps -el
```

---

### Afinidad

Consultar afinidad:

```bash
taskset -p 1234
```

Asignar núcleos:

```bash
taskset -c 0,1 comando
```

Modificar un proceso existente:

```bash
taskset -cp 0,1 1234
```

---

### Información detallada

Consultar información de un proceso:

```bash
cat /proc/1234/status
```

O visualizar todo su directorio:

```bash
ls /proc/1234
```

---

### Archivos abiertos

Consultar archivos utilizados por un proceso:

```bash
lsof -p 1234
```

---

### Conexiones de red

Consultar conexiones abiertas por un proceso:

```bash
ss -tulpn
```

---

### Procesos en segundo plano

Ejecutar una aplicación en segundo plano:

```bash
comando &
```

---

### nohup

Permite que un proceso continúe ejecutándose incluso después de cerrar la sesión.

Ejemplo:

```bash
nohup comando &
```

Muy útil para procesos largos.

---

### screen

`screen` permite mantener sesiones persistentes.

Crear sesión:

```bash
screen
```

---

### tmux

Alternativa moderna a `screen`.

Crear sesión:

```bash
tmux
```

---

### Depuración

Seguir llamadas al sistema:

```bash
strace -p 1234
```

Seguir llamadas a bibliotecas:

```bash
ltrace comando
```

Estas herramientas ayudan a diagnosticar bloqueos y errores complejos.

---

### Consumo de recursos

Procesos con mayor uso de CPU:

```bash
ps aux --sort=-%cpu
```

Procesos con mayor uso de memoria:

```bash
ps aux --sort=-%mem
```

---

[⬆️ Volver al índice](#índice)

## Procesos en Windows

Windows dispone de numerosas herramientas para administrar y supervisar procesos, tanto mediante interfaces gráficas como desde PowerShell y la línea de comandos.

---

### Administrador de tareas

Es la herramienta más utilizada para gestionar procesos.

Abrir:

```text
Ctrl + Shift + Esc
```

Permite:

- Ver procesos activos.
- Finalizar aplicaciones.
- Consultar CPU.
- Consultar memoria.
- Consultar disco.
- Consultar red.
- Cambiar prioridad.
- Configurar afinidad.

Resulta ideal para un diagnóstico rápido.

---

### Pestaña Procesos

Muestra todas las aplicaciones y procesos en ejecución.

Información disponible:

- Nombre.
- Uso de CPU.
- Memoria.
- Disco.
- Red.
- GPU.
- Consumo energético.

Los procesos pueden ordenarse por cualquiera de estas columnas.

---

### Pestaña Detalles

Ofrece información más técnica.

Incluye:

- PID.
- Estado.
- Usuario.
- Prioridad.
- Afinidad.
- Arquitectura.

Desde esta pestaña también es posible:

- Finalizar procesos.
- Cambiar prioridad.
- Cambiar afinidad.
- Analizar cadenas de espera.

---

### PowerShell

PowerShell proporciona una forma muy flexible de administrar procesos.

Mostrar todos los procesos:

```powershell
Get-Process
```

---

### Ordenar procesos

Mayor consumo de CPU:

```powershell
Get-Process |
Sort-Object CPU -Descending
```

Mayor consumo de memoria:

```powershell
Get-Process |
Sort-Object WorkingSet -Descending
```

---

### Finalizar procesos

Finalizar mediante nombre:

```powershell
Stop-Process -Name notepad
```

Finalizar mediante PID:

```powershell
Stop-Process -Id 1234
```

---

### Iniciar procesos

Ejecutar una aplicación:

```powershell
Start-Process notepad.exe
```

---

### Prioridad

Consultar prioridad:

```powershell
(Get-Process notepad).PriorityClass
```

Modificar prioridad:

```powershell
(Get-Process notepad).PriorityClass = "High"
```

---

[⬆️ Volver al índice](#índice)

## Señales y finalización de procesos

| Linux | Windows |
|--------|----------|
| `kill` | `Stop-Process` |
| `killall` | `taskkill` |
| `pkill` | Administrador de tareas |
| Señales | Finalización directa |
| SIGTERM | Cierre normal |
| SIGKILL | Finalización forzada |

---

### SIGTERM

Es la señal recomendada para finalizar un proceso.

```text
Proceso

↓

SIGTERM

↓

Libera recursos

↓

Guarda datos

↓

Finaliza correctamente
```

Permite que la aplicación cierre conexiones, guarde información y libere memoria antes de finalizar.

Enviar la señal:

```bash
kill 1234
```

ya que `SIGTERM` es la señal utilizada por defecto.

---

### SIGKILL

Finaliza inmediatamente el proceso.

```text
Proceso

↓

SIGKILL

↓

Finalización inmediata
```

El proceso **no puede interceptar ni ignorar** esta señal.

Ejemplo:

```bash
kill -9 1234
```

Debe utilizarse únicamente cuando el proceso no responde a `SIGTERM`.

---

### SIGINT

Se genera normalmente al pulsar:

```text
Ctrl + C
```

La mayoría de aplicaciones interpretan esta señal como una solicitud de finalización.

---

### SIGHUP

Originalmente indicaba que se había perdido la conexión del terminal.

Actualmente suele utilizarse para indicar a un servicio que vuelva a leer su archivo de configuración sin necesidad de reiniciarse.

Ejemplo:

```bash
kill -HUP 1234
```

Es habitual en servicios como:

- Nginx.
- Apache.
- SSH.

---

### SIGSTOP y SIGCONT

Permiten pausar y reanudar procesos.

Pausar:

```bash
kill -STOP 1234
```

Reanudar:

```bash
kill -CONT 1234
```

Resulta útil para tareas de administración y depuración.

---

### kill

Enviar una señal mediante PID:

```bash
kill PID
```

Especificar una señal concreta:

```bash
kill -9 PID
```

Consultar todas las señales disponibles:

```bash
kill -l
```

---

### killall

Permite finalizar procesos utilizando su nombre.

Ejemplo:

```bash
killall firefox
```

Finalizará todas las instancias del proceso indicado.

---

### pkill

Busca procesos por nombre o patrón y les envía una señal.

Ejemplo:

```bash
pkill firefox
```

También permite utilizar expresiones regulares y filtros más avanzados.

---

### Finalización en Windows

Windows no utiliza señales como Linux.

Administrador de tareas:

```text
Finalizar tarea
```

PowerShell:

```powershell
Stop-Process -Id 1234
```

CMD:

```cmd
taskkill /PID 1234
```

Finalización forzada:

```cmd
taskkill /F /PID 1234
```

O mediante PowerShell:

```powershell
Stop-Process -Id 1234 -Force
```

---

### taskkill

Ejemplos:

Finalizar por PID:

```cmd
taskkill /PID 1234
```

Finalizar por nombre:

```cmd
taskkill /IM notepad.exe
```

Forzar finalización:

```cmd
taskkill /F /IM notepad.exe
```

---

[⬆️ Volver al índice](#índice)

## Monitorización y depuración

Además de administrar procesos, un administrador de sistemas debe ser capaz de **analizar su comportamiento**, detectar problemas de rendimiento y diagnosticar errores.

---

### Monitorización en Linux

Las herramientas más habituales son:

| Herramienta | Función |
|-------------|---------|
| `top` | Procesos en tiempo real |
| `htop` | Monitor interactivo |
| `ps` | Información de procesos |
| `pidstat` | Estadísticas por proceso |
| `vmstat` | Memoria y CPU |
| `iostat` | Rendimiento de discos |
| `sar` | Estadísticas históricas |

Estas utilidades permiten obtener una visión global del estado del sistema.

---

### Monitorización en Windows

Las herramientas principales son:

- Administrador de tareas.
- Monitor de recursos.
- Monitor de rendimiento (PerfMon).
- Process Explorer.
- Process Monitor.

Cada una ofrece distintos niveles de detalle según el tipo de análisis necesario.

---

### strace

En Linux, `strace` permite observar las llamadas al sistema realizadas por un proceso.

Ejemplo:

```bash
strace -p 1234
```

Muestra operaciones como:

- Apertura de archivos.
- Lectura y escritura.
- Creación de procesos.
- Acceso a memoria.
- Operaciones de red.

Es una herramienta muy útil para detectar dónde queda bloqueado un proceso.

---

### ltrace

Mientras que `strace` muestra llamadas al sistema, `ltrace` permite observar las llamadas a bibliotecas compartidas.

Ejemplo:

```bash
ltrace programa
```

Resulta útil para analizar aplicaciones que utilizan bibliotecas dinámicas.

---

### gdb

**GNU Debugger (gdb)** es el depurador estándar de Linux.

Permite:

- Ejecutar programas paso a paso.
- Establecer puntos de interrupción (*breakpoints*).
- Examinar variables.
- Analizar la pila de llamadas.
- Investigar bloqueos.

Ejemplo:

```bash
gdb programa
```

Está orientado principalmente a desarrolladores, aunque también puede utilizarse para analizar fallos complejos en servidores.

---

### Registros del sistema

Muchas incidencias pueden diagnosticarse revisando los registros.

En Linux:

```bash
journalctl
```

o:

```bash
dmesg
```

En Windows:

- Visor de eventos.

Estos registros suelen contener información muy útil sobre errores de procesos y servicios.

---

[⬆️ Volver al índice](#índice)