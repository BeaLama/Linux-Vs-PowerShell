# Gestión de procesos

## Introducción

Los procesos son la base del funcionamiento de cualquier sistema operativo.

## Índice

- [Concepto de proceso](#concepto-de-proceso)
- [Estados de un proceso](#estados-de-un-proceso)
- [Proceso e hilos (Threads)](#proceso-e-hilos-threads)
- [Planificación de procesos](#planificación-de-procesos)
- [Prioridad dinámica](#prioridad-dinámica)
- [Consultar prioridad](#consultar-prioridad)
- [Iniciar un proceso con prioridad distinta](#iniciar-un-proceso-con-prioridad-distinta)
- [Modificar la prioridad de un proceso](#modificar-la-prioridad-de-un-proceso)
- [Mostrar procesos](#mostrar-procesos)
- [Buscar un proceso](#buscar-un-proceso)
- [Finalizar un proceso](#finalizar-un-proceso)
- [Ordenar procesos por consumo de memoria](#ordenar-procesos-por-consumo-de-memoria)
- [Mostrar los procesos que más CPU consumen](#mostrar-los-procesos-que-más-cpu-consumen)
- [Gestión de procesos en Linux](#gestión-de-procesos-en-linux)
- [kill](#kill)
- [Forzar la finalización](#forzar-la-finalización)
- [killall](#killall)
- [pkill](#pkill)
- [Deshabilitado](#deshabilitado)
- [top](#top)
- [htop](#htop)
- [free](#free)
- [df](#df)
- [vmstat](#vmstat)
- [iostat](#iostat)
- [sar](#sar)
- [Procesos bloqueados y finalización de procesos](#procesos-bloqueados-y-finalización-de-procesos)
- [kill](#kill)
- [kill -9](#kill--9)
- [killall](#killall)
- [pkill](#pkill)
- [Procesos en segundo plano](#procesos-en-segundo-plano)
- [Automatización y tareas programadas](#automatización-y-tareas-programadas)
- [Auditoría y registros de procesos](#auditoría-y-registros-de-procesos)
- [Procedimiento](#procedimiento)
- [Procedimiento](#procedimiento)
- [Procedimiento](#procedimiento)
- [Procedimiento](#procedimiento)
- [Procedimiento](#procedimiento)
- [Procedimiento](#procedimiento)
- [Solución en Windows](#solución-en-windows)
- [Solución en Linux](#solución-en-linux)

---

## Concepto de proceso

*Aunque suelen confundirse, un programa y un proceso no son lo mismo.*

| Programa | Proceso |
|----------|----------|
| Conjunto de instrucciones almacenadas en disco. | Programa que se está ejecutando en memoria. |
| Es un elemento pasivo. | Es un elemento activo. |
| No consume recursos mientras no se ejecuta. | Consume CPU, memoria y otros recursos del sistema. |

---

**Conceptos clave:**

- **Procesos del sistema:** Son iniciados por el sistema operativo y permiten su correcto funcionamiento.
- **Procesos de usuario:** Son iniciados por los usuarios o por las aplicaciones.

## Estados de un proceso

*De forma simplificada, un proceso pasa por los siguientes estados.*

| Código | Significado |
|---------|-------------|
| R | Running (En ejecución) |
| S | Sleeping (Esperando) |
| D | Espera ininterrumpida (normalmente E/S) |
| T | Detenido |
| Z | Zombie |

```bash
ps aux
```

---

## Proceso e hilos (Threads)

*Un hilo (Thread) es la unidad básica de ejecución dentro de un proceso.*

| Proceso | Hilo (Thread) |
|----------|---------------|
| Programa en ejecución. | Unidad de ejecución dentro de un proceso. |
| Tiene memoria y recursos propios. | Comparte los recursos del proceso. |
| Puede contener varios hilos. | Pertenece siempre a un único proceso. |

```bash
ps -ef
```
```bash
ps -T -p PID
```

---

## Planificación de procesos

**Conceptos clave:**

- **¿Qué es el planificador de procesos?:** El planificador de procesos es el componente del sistema operativo responsable de administrar el acceso a la CPU.
- **FIFO (First In, First Out):** Los procesos se ejecutan en el mismo orden en el que llegan.
- **Round Robin:** Cada proceso recibe un pequeño intervalo de tiempo (quantum).
- **Planificación por prioridades:** Cada proceso dispone de una prioridad.
- **Prioridad de procesos:** No todos los procesos tienen la misma importancia para el sistema operativo.
- **Prioridad estática:** Es una prioridad fija establecida por el sistema o por el administrador.

## Prioridad dinámica

*El sistema operativo modifica automáticamente la prioridad según el comportamiento del proceso.*

| Prioridad | Uso habitual |
|-----------|--------------|
| Tiempo real | Procesos extremadamente críticos |
| Alta | Aplicaciones importantes |
| Superior a la normal | Aplicaciones exigentes |
| Normal | Mayoría de aplicaciones |
| Inferior a la normal | Procesos secundarios |
| Baja | Procesos en segundo plano |

---

## Consultar prioridad

*Ejemplo.*

```bash
ps -el
```
```bash
top
```

---

## Iniciar un proceso con prioridad distinta

*Ejemplo.*

```bash
nice -n 10 programa
```

---

## Modificar la prioridad de un proceso

*Ejemplo.*

```bash
renice 5 -p 3218
```

---

**Conceptos clave:**

- **Gestión de procesos en Windows:** Windows proporciona diversas herramientas para visualizar, supervisar y administrar los procesos que se ejecutan en el sistema.
- **Mostrar procesos:** ```cmd tasklist ``` Ejemplo.
- **Finalizar un proceso:** Por nombre.

## Mostrar procesos

```powershell
Get-Process
```

---

## Buscar un proceso

```powershell
Get-Process chrome
```

---

## Finalizar un proceso

```powershell
Stop-Process -Name chrome
```
```powershell
Stop-Process -Id 3456
```

---

## Ordenar procesos por consumo de memoria

```powershell
Get-Process | Sort-Object WorkingSet -Descending
```

---

## Mostrar los procesos que más CPU consumen

```powershell
Get-Process | Sort-Object CPU -Descending
```

---

## Gestión de procesos en Linux

*Linux ofrece un amplio conjunto de herramientas para visualizar, administrar y controlar los procesos del sistema.*

```bash
ps
```
```bash
ps -ef
```

---

## kill

*Finaliza un proceso utilizando su PID.*

```bash
kill 2487
```

---

## Forzar la finalización

*Si el proceso no responde.*

```bash
kill -9 2487
```

---

## killall

*Permite finalizar procesos por nombre.*

```bash
killall firefox
```

---

## pkill

*Permite finalizar procesos utilizando parte del nombre.*

```bash
pkill chrome
```
```bash
top
```

---

**Conceptos clave:**

- **Servicios del sistema:** Además de los procesos iniciados por los usuarios, los sistemas operativos ejecutan numerosos servicios del sistema, encargados de realizar tareas esenciales en segundo plano sin necesidad de interacción directa.
- **Automático:** El servicio se inicia durante el arranque del sistema.
- **Automático (inicio retrasado):** El servicio se inicia automáticamente unos segundos después del arranque.
- **Manual:** El servicio únicamente se inicia cuando una aplicación o un usuario lo solicita.

## Deshabilitado

*El servicio no puede iniciarse hasta que su configuración sea modificada.*

**Conceptos clave:**

- **Windows:** - Print Spooler - Windows Update - Windows Defender - DHCP Client - DNS Client - Remote Desktop Services
- **Linux:** - ssh - apache2 - nginx - mysql - docker - cron --- Una mala configuración puede provocar: Consumo excesivo de recursos.
- **Monitorización del rendimiento:** La monitorización del rendimiento consiste en supervisar el estado y el consumo de los recursos del sistema para garantizar un funcionamiento eficiente y detectar posibles problemas antes de que afecten a los usuarios.
- **Administrador de tareas:** Permite consultar: CPU.
- **Monitor de recursos:** Puede abrirse mediante.
- **Monitor de rendimiento:** Puede iniciarse mediante.

## top

```bash
top
```

---

## htop

```bash
htop
```

---

## free

*Consultar memoria.*

```bash
free -h
```

---

## df

*Consultar espacio en disco.*

```bash
df -h
```

---

## vmstat

*Consultar información del sistema.*

```bash
vmstat
```

---

## iostat

*Analizar el rendimiento del almacenamiento.*

```bash
iostat
```

---

## sar

*Obtener estadísticas históricas.*

| Recurso | Indicador |
|----------|------------|
| CPU | % de utilización |
| RAM | Memoria utilizada |
| Disco | Tiempo de respuesta |
| Red | Tráfico enviado y recibido |
| Procesos | Consumo de CPU y memoria |

```bash
sar
```

---

## Procesos bloqueados y finalización de procesos

*Durante el funcionamiento de un sistema operativo, es posible que algunos procesos dejen de responder correctamente debido a errores de programación, falta de recursos o conflictos con otros procesos.*

```powershell
Get-Process
```
```powershell
Stop-Process -Name notepad
```

---

## kill

*Finaliza un proceso utilizando su PID.*

```bash
kill 3456
```

---

## kill -9

*Si el proceso no responde.*

```bash
kill -9 3456
```

---

## killall

*Finaliza todos los procesos con un mismo nombre.*

```bash
killall firefox
```

---

## pkill

*Permite finalizar procesos utilizando parte de su nombre.*

| Señal | Nombre | Descripción |
|--------|---------|-------------|
| 15 | SIGTERM | Finalización normal |
| 9 | SIGKILL | Finalización inmediata |
| 2 | SIGINT | Interrupción (Ctrl + C) |
| 19 | SIGSTOP | Detener proceso |
| 18 | SIGCONT | Reanudar proceso |

```bash
pkill chrome
```

---

## Procesos en segundo plano

*No todos los procesos requieren la interacción directa del usuario.*

| Primer plano | Segundo plano |
|---------------|---------------|
| Interacción directa con el usuario. | Sin interacción directa. |
| Normalmente muestra una ventana. | Habitualmente no muestra interfaz gráfica. |
| El usuario controla su ejecución. | El sistema o la aplicación la controlan automáticamente. |

```bash
ps -ef
```
```bash
top
```

---

## Automatización y tareas programadas

*En la administración de sistemas es habitual que determinadas tareas deban ejecutarse de forma periódica o automática, sin necesidad de la intervención de un usuario.*

```bash
crontab -e
```
```powershell
Get-Process
```
```bash
crontab -l
```
```powershell
Get-Process > procesos.txt
```

---

## Auditoría y registros de procesos

*La auditoría de procesos consiste en registrar y analizar la información relacionada con la creación, ejecución y finalización de los procesos del sistema.*

**Conceptos clave:**

- **Windows:** - Visor de eventos.

### Linux

*- journalctl.*

```bash
journalctl -u nombre_del_servicio
```

---

## Procedimiento

```bash
top
```
```bash
htop
```

---

**Conceptos clave:**

- **Situación:** El sistema comienza a utilizar memoria virtual y las aplicaciones responden lentamente.

## Procedimiento

*Windows.*

```bash
free -h
```
```bash
top
```

---

**Conceptos clave:**

- **Situación:** Un servidor web deja de responder a las peticiones de los usuarios.

## Procedimiento

*Windows.*

```bash
systemctl status apache2
```
```powershell
Get-Service
```
```bash
sudo systemctl restart apache2
```
```powershell
Restart-Service NombreServicio
```

---

**Conceptos clave:**

- **Situación:** Aparece un proceso desconocido consumiendo recursos del sistema.

## Procedimiento

```bash
ps -ef
```
```bash
which nombre_proceso
```

---

**Conceptos clave:**

- **Situación:** Windows informa de que una aplicación impide el apagado del sistema.
- **Procedimiento:** ```text Identificar aplicación ↓ Guardar información ↓ Cerrar correctamente ↓ Si continúa bloqueada ↓ Finalizar tarea ``` Forzar el cierre únicamente cuando sea imprescindible.
- **Situación:** Se desea obtener información sobre los procesos que más memoria consumen.

## Procedimiento

```powershell
Get-Process | Sort-Object WorkingSet -Descending
```
```powershell
Get-Process | Sort-Object WorkingSet -Descending | Select-Object -First 10
```

---

**Conceptos clave:**

- **Situación:** Un proceso ha dejado de responder.

## Procedimiento

*Localizar el PID.*

```bash
ps -ef
```
```bash
kill PID
```

---

**Conceptos clave:**

- **Situación:** El administrador desea generar diariamente un listado de procesos en ejecución.

## Solución en Windows

*Crear un script de PowerShell.*

```powershell
Get-Process > C:\Informes\procesos.txt
```

---

## Solución en Linux

*Crear un script Bash.*

```bash
ps -ef > /home/admin/procesos.txt
```

---

[⬆️ Volver al índice](#índice)
