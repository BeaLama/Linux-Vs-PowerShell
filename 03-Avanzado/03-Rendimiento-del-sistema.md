# Rendimiento del sistema

## Introducción

El rendimiento del sistema hace referencia a la capacidad de un equipo o servidor para ejecutar tareas de forma eficiente utilizando los recursos disponibles.

---

## Índice

- [Conceptos básicos](#conceptos-básicos)
- [Uso de CPU](#uso-de-cpu)
- [Uso de memoria RAM](#uso-de-memoria-ram)
- [Rendimiento del disco](#rendimiento-del-disco)
- [Rendimiento de red](#rendimiento-de-red)
- [Monitorización en Linux](#monitorización-en-linux)
- [Monitorización en Windows](#monitorización-en-windows)
- [Optimización del rendimiento](#optimización-del-rendimiento)

---

## Conceptos básicos

Antes de analizar el rendimiento de un sistema es importante comprender qué recursos intervienen y cómo afectan al funcionamiento del equipo.

| Linux | Windows |
|--------|----------|
| `top`, `htop`, `vmstat`, `free` | Administrador de tareas |
| `iostat`, `iotop` | Monitor de recursos |
| `sar`, `pidstat` | Monitor de rendimiento (PerfMon) |
| `iftop`, `ss`, `nload` | PowerShell (`Get-Counter`, `Get-Process`) |

---

[⬆️ Volver al índice](#índice)

## Uso de CPU

La **CPU (Central Processing Unit)** es el componente encargado de ejecutar las instrucciones del sistema operativo y de las aplicaciones.

| Linux | Windows |
|--------|----------|
| `top` | Administrador de tareas |
| `htop` | Monitor de recursos |
| `ps` | PowerShell (`Get-Process`) |
| `uptime` | PerfMon |
| `lscpu` | `Get-CimInstance Win32_Processor` |

---

### Conceptos importantes

Al analizar el procesador suelen revisarse los siguientes indicadores:

| Indicador | Descripción |
|-----------|-------------|
| Uso de CPU (%) | Porcentaje de utilización del procesador. |
| Núcleos | Número de unidades de procesamiento disponibles. |
| Hilos (Threads) | Procesos de ejecución simultánea soportados por la CPU. |
| Frecuencia | Velocidad de funcionamiento del procesador (GHz). |
| Carga media (*Load Average*) | Número de procesos esperando para ejecutarse (Linux). |
| Tiempo de usuario | Tiempo dedicado a ejecutar aplicaciones. |
| Tiempo de sistema | Tiempo utilizado por el kernel del sistema operativo. |
| Tiempo inactivo | Tiempo durante el que la CPU no está realizando trabajo. |

---

### Analizar la CPU en Linux

#### Ver uso en tiempo real

La herramienta más utilizada es:

```bash
top
```

---

#### Versión mejorada: `htop`

Si está instalada:

```bash
htop
```

---

#### Ver la carga del sistema

```bash
uptime
```

---

#### Información del procesador

```bash
lscpu
```
---

#### Mostrar procesos ordenados por CPU

```bash
ps aux --sort=-%cpu
```

Ejemplo:

```bash
ps aux --sort=-%cpu | head
```

Permite identificar rápidamente los procesos que más CPU están consumiendo.

---

### Analizar la CPU en Windows

#### Administrador de tareas

Abrir:

```text
Ctrl + Shift + Esc
```

Pestaña:

```text
Rendimiento

↓

CPU
```

---

#### Monitor de recursos

Abrir:

```text
resmon
```

Pestaña:

```text
CPU
```

---

#### Monitor de rendimiento

Abrir:

```text
perfmon
```

Permite crear contadores personalizados para supervisar la CPU durante largos periodos de tiempo.

Muy utilizado en servidores Windows.

---

[⬆️ Volver al índice](#índice)

## Uso de memoria RAM

La **memoria RAM (Random Access Memory)** es el espacio de almacenamiento temporal utilizado por el sistema operativo y las aplicaciones mientras se encuentran en ejecución.

| Linux | Windows |
|--------|----------|
| `free -h` | Administrador de tareas |
| `top` | Monitor de recursos |
| `htop` | PerfMon |
| `vmstat` | PowerShell |
| `ps aux --sort=-%mem` | `Get-Process` |

---

### Conceptos importantes

Al analizar la memoria RAM conviene conocer los siguientes términos:

| Concepto | Descripción |
|----------|-------------|
| Memoria total | Cantidad total de memoria RAM instalada. |
| Memoria utilizada | RAM ocupada por el sistema y las aplicaciones. |
| Memoria libre | RAM completamente disponible. |
| Memoria disponible | Memoria que puede utilizarse inmediatamente, incluyendo parte de la memoria en caché. |
| Caché | Datos almacenados temporalmente para acelerar accesos futuros. |
| Buffer | Memoria utilizada para operaciones de entrada y salida. |
| Swap / Memoria virtual | Espacio en disco utilizado cuando la RAM es insuficiente. |

---

### Analizar la memoria en Linux

#### Ver memoria disponible

```bash
free -h
```

Ejemplo:

```text
               total   used   free  shared  buff/cache  available
Mem:            15Gi   6Gi    2Gi     500Mi      7Gi         8Gi
Swap:            2Gi   0Gi    2Gi
```

---

#### Monitorización en tiempo real

```bash
top
```

o

```bash
htop
```

---

#### Mostrar procesos por consumo de memoria

```bash
ps aux --sort=-%mem
```

Los diez primeros:

```bash
ps aux --sort=-%mem | head
```

---

#### Información detallada

```bash
vmstat
```

---

### Analizar la memoria en Windows

#### Administrador de tareas

Abrir:

```text
Ctrl + Shift + Esc
```

Pestaña:

```text
Rendimiento

↓

Memoria
```

---

#### Monitor de recursos

Abrir:

```text
resmon
```

Pestaña:

```text
Memoria
```

---

### PowerShell

Consultar la memoria física instalada:

```powershell
Get-CimInstance Win32_PhysicalMemory
```

Consultar el sistema operativo:

```powershell
Get-CimInstance Win32_OperatingSystem
```

---

[⬆️ Volver al índice](#índice)

## Rendimiento del disco

El almacenamiento es uno de los recursos que más influye en el rendimiento de un sistema.

| Linux | Windows |
|--------|----------|
| `df` | Explorador de archivos |
| `du` | Propiedades de la unidad |
| `iostat` | Administrador de tareas |
| `iotop` | Monitor de recursos |
| `lsblk` | `Get-PhysicalDisk` |
| `df -h` | `Get-Volume` |

| Linux | Windows |
|--------|----------|
| `ip addr` | `Get-NetIPAddress` |
| `ip -s link` | `Get-NetAdapterStatistics` |
| `ss` | `Get-NetTCPConnection` |
| `iftop` | Monitor de recursos |
| `nload` | Administrador de tareas |
| `ping` | `Test-Connection` |

---

### Analizar el disco en Linux

#### Espacio disponible

```bash
df -h
```

Ejemplo:

```text
Filesystem      Size  Used Avail Use%
/dev/sda2       100G   62G   38G  62%
```

---

#### Uso de directorios

```bash
du -sh carpeta
```

Ejemplo:

```bash
du -sh /var/log
```

Para listar el tamaño de los subdirectorios:

```bash
du -sh *
```

---

#### Actividad del disco

```bash
iostat
```

Ejemplo:

```bash
iostat -x 2
```

Muestra información como:

- Lecturas por segundo.
- Escrituras por segundo.
- Tiempo de espera.
- Utilización del dispositivo.

> **Nota:** `iostat` forma parte normalmente del paquete **sysstat**.

---

#### Procesos que utilizan el disco

```bash
iotop
```

Permite identificar qué procesos están realizando más operaciones de lectura y escritura.

> **Nota:** `iotop` puede requerir permisos de administrador.

---

#### Información de los dispositivos

```bash
lsblk
```

Muestra:

- Discos.
- Particiones.
- Tamaño.
- Punto de montaje.

---

### Analizar el disco en Windows

#### Administrador de tareas

Abrir:

```text
Ctrl + Shift + Esc
```

Pestaña:

```text
Rendimiento

↓

Disco
```

---

#### Monitor de recursos

Abrir:

```text
resmon
```

Pestaña:

```text
Disco
```

---

### PowerShell

Consultar los discos físicos:

```powershell
Get-PhysicalDisk
```

Consultar las unidades disponibles:

```powershell
Get-Volume
```

---

[⬆️ Volver al índice](#índice)

### Rendimiento de red

La red es uno de los recursos más importantes en cualquier sistema conectado.

Para diagnosticar estos problemas es necesario analizar tanto la configuración como el tráfico y el estado de la conexión.

---

### Conceptos importantes

Los principales indicadores de rendimiento de red son:

| Indicador | Descripción |
|-----------|-------------|
| Ancho de banda | Cantidad máxima de datos que puede transmitir una conexión. |
| Velocidad de transferencia | Cantidad real de datos transmitidos por segundo. |
| Latencia | Tiempo que tarda un paquete en llegar a su destino y volver. |
| Jitter | Variación en la latencia entre paquetes consecutivos. |
| Pérdida de paquetes | Porcentaje de paquetes que no llegan a su destino. |
| Errores | Paquetes dañados o descartados durante la transmisión. |
| Conexiones activas | Número de conexiones abiertas en un momento determinado. |

---

### Analizar la red en Linux

#### Configuración de interfaces

```bash
ip addr
```

---

#### Estadísticas de red

```bash
ip -s link
```

---

#### Conexiones activas

```bash
ss -tuln
```

---

#### Tráfico en tiempo real

```bash
iftop
```

---

#### Monitor sencillo

```bash
nload
```

---

#### Comprobar conectividad

```bash
ping 8.8.8.8
```

---

#### Analizar la ruta

```bash
traceroute google.com
```

---

### Analizar la red en Windows

#### Administrador de tareas

Abrir:

```text
Ctrl + Shift + Esc
```

Pestaña:

```text
Rendimiento

↓

Ethernet o Wi-Fi
```

---

#### Monitor de recursos

Abrir:

```text
resmon
```

Pestaña:

```text
Red
```

---

### PowerShell

Consultar los adaptadores de red:

```powershell
Get-NetAdapter
```

Consultar la configuración IP:

```powershell
Get-NetIPAddress
```

Consultar estadísticas:

```powershell
Get-NetAdapterStatistics
```

---

#### Comprobar conectividad

```powershell
Test-Connection google.com
```

También puede utilizarse:

```powershell
ping google.com
```

---

#### Conexiones abiertas

```powershell
Get-NetTCPConnection
```

---

[⬆️ Volver al índice](#índice)

## Monitorización en Linux

La monitorización consiste en observar el estado del sistema de forma continua para detectar problemas de rendimiento antes de que afecten a los usuarios o a los servicios.

---

### top

`top` es una de las herramientas más conocidas para monitorizar el sistema en tiempo real.

Ejecutar:

```bash
top
```

Controles útiles:

| Tecla | Acción |
|--------|--------|
| `P` | Ordenar por uso de CPU. |
| `M` | Ordenar por uso de memoria. |
| `k` | Finalizar un proceso. |
| `q` | Salir. |

---

### htop

`htop` es una versión mejorada de `top`.

Ejecutar:

```bash
htop
```

Ejemplo:

```bash
sudo apt install htop
```

---

### free

Consultar el estado de la memoria:

```bash
free -h
```

---

### vmstat

Consultar estadísticas generales:

```bash
vmstat
```

Actualizar cada segundo:

```bash
vmstat 1
```

---

### iostat

Analizar el rendimiento del almacenamiento:

```bash
iostat -x 2
```

---

### iotop

Monitorizar la actividad de entrada y salida por proceso:

```bash
sudo iotop
```

---

### sar

`sar` permite analizar el rendimiento del sistema utilizando datos históricos.

Ejemplos:

Uso de CPU:

```bash
sar -u
```

Memoria:

```bash
sar -r
```

Disco:

```bash
sar -d
```

Red:

```bash
sar -n DEV
```

---

[⬆️ Volver al índice](#índice)

## Monitorización en Windows

Windows incorpora diversas herramientas para supervisar el estado del sistema y analizar el consumo de recursos en tiempo real.

---

### Administrador de tareas

El **Administrador de tareas** es la herramienta de monitorización más utilizada.

Abrir:

```text
Ctrl + Shift + Esc
```

O:

```text
Ctrl + Alt + Supr

↓

Administrador de tareas
```

---

### Monitor de recursos

Abrir:

```text
resmon
```

O buscar:

```text
Monitor de recursos
```

---

### PowerShell

PowerShell permite obtener información de rendimiento mediante diferentes cmdlets.

---

#### Procesos

Mostrar procesos ordenados por CPU:

```powershell
Get-Process |
Sort-Object CPU -Descending
```

Mostrar procesos ordenados por memoria:

```powershell
Get-Process |
Sort-Object WorkingSet -Descending
```

---

#### Rendimiento mediante Get-Counter

Consultar el uso de CPU:

```powershell
Get-Counter '\Processor(_Total)\% Processor Time'
```

Consultar memoria disponible:

```powershell
Get-Counter '\Memory\Available MBytes'
```

Consultar actividad del disco:

```powershell
Get-Counter '\PhysicalDisk(_Total)\Disk Transfers/sec'
```

Consultar tráfico de red:

```powershell
Get-Counter '\Network Interface(*)\Bytes Total/sec'
```

---

#### Información general

```powershell
Get-ComputerInfo
```

---

[⬆️ Volver al índice](#índice)

## Optimización del rendimiento

Optimizar el rendimiento consiste en mejorar el funcionamiento del sistema utilizando de forma más eficiente los recursos disponibles.

| 🐧 Linux | 🪟 PowerShell |
|---|---|
| `top` | `Get-Process \|<br>Sort-Object CPU -Descending` |

---

### Optimización en Linux

Algunas acciones habituales son:

Consultar procesos:

```bash
top
```

Liberar memoria caché (solo en casos concretos y con conocimiento del impacto):

```bash
sudo sync

echo 3 | sudo tee /proc/sys/vm/drop_caches
```

Comprobar espacio disponible:

```bash
df -h
```

Identificar procesos que consumen más memoria:

```bash
ps aux --sort=-%mem
```

---

### Optimización en Windows

Herramientas útiles:

Administrador de tareas:

```text
Ctrl + Shift + Esc
```

Liberador de espacio:

```text
cleanmgr
```

Optimización de unidades:

```text
dfrgui
```

Configuración de programas de inicio:

```text
Administrador de tareas

↓

Inicio
```

PowerShell:

Consultar procesos con mayor consumo:

```powershell
Get-Process |
Sort-Object CPU -Descending
```

---

[⬆️ Volver al índice](#índice)