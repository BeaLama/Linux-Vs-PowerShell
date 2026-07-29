# Rendimiento del sistema

## Introducción

El rendimiento del sistema hace referencia a la capacidad de un equipo o servidor para ejecutar tareas de forma eficiente utilizando los recursos disponibles.

Una degradación del rendimiento puede provocar:

- Lentitud en aplicaciones.
- Mayor tiempo de respuesta.
- Bloqueos.
- Consumo excesivo de recursos.
- Interrupciones en los servicios.

El objetivo del administrador de sistemas es identificar rápidamente los cuellos de botella y determinar qué recurso está limitando el rendimiento del sistema.

Los principales recursos que deben supervisarse son:

- Procesador (CPU).
- Memoria RAM.
- Almacenamiento (discos).
- Red.
- Procesos y servicios.

Tanto Linux como Windows incorporan herramientas que permiten monitorizar estos recursos en tiempo real y detectar posibles problemas de rendimiento.

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
- [Buenas prácticas](#buenas-prácticas)

---

## Conceptos básicos

Antes de analizar el rendimiento de un sistema es importante comprender qué recursos intervienen y cómo afectan al funcionamiento del equipo.

El rendimiento depende del equilibrio entre varios componentes de hardware y software. Un único recurso saturado puede convertirse en un **cuello de botella**, limitando el rendimiento general aunque el resto de recursos tengan una utilización baja.

---

# Recursos principales

Los recursos que más influyen en el rendimiento son:

- Procesador (CPU).
- Memoria RAM.
- Almacenamiento.
- Red.
- Procesos y servicios.

Cada uno cumple una función específica y debe analizarse de forma independiente.

---

# CPU

El procesador ejecuta las instrucciones de los programas y del sistema operativo.

Una CPU con un uso elevado durante periodos prolongados puede provocar:

- Lentitud general.
- Mayor tiempo de respuesta.
- Retrasos en aplicaciones.
- Incremento de la temperatura.
- Mayor consumo energético.

Un uso alto de CPU no siempre indica un problema; puede deberse a tareas intensivas como compilaciones, máquinas virtuales o procesos de análisis.

---

# Memoria RAM

La memoria RAM almacena temporalmente la información que necesitan el sistema operativo y las aplicaciones mientras se están ejecutando.

Cuando la memoria disponible se agota:

- El sistema comienza a utilizar memoria virtual o archivo de paginación.
- El acceso a disco aumenta considerablemente.
- El rendimiento disminuye de forma notable.

No siempre es necesario mantener un gran porcentaje de memoria libre; muchos sistemas operativos utilizan la RAM disponible para mejorar el rendimiento mediante caché.

---

# Almacenamiento

El rendimiento del almacenamiento depende de varios factores:

- Tipo de unidad (HDD o SSD).
- Velocidad de lectura y escritura.
- Tiempo de acceso.
- Número de operaciones de entrada/salida (IOPS).
- Cola de operaciones pendientes.

Un disco muy ocupado puede afectar al rendimiento incluso aunque la CPU y la memoria apenas estén siendo utilizadas.

---

# Red

La red puede convertirse en un factor limitante cuando existe:

- Saturación del ancho de banda.
- Alta latencia.
- Pérdida de paquetes.
- Errores de transmisión.

Los problemas de red suelen reflejarse en:

- Aplicaciones lentas.
- Copias de archivos muy lentas.
- Accesos remotos con retraso.
- Problemas en servicios web.

---

# Procesos

Cada aplicación que se ejecuta crea uno o varios procesos.

Algunos procesos pueden consumir recursos de forma excesiva debido a:

- Errores de programación.
- Bucles infinitos.
- Fugas de memoria (*memory leaks*).
- Alta carga de trabajo.

Identificar el proceso responsable suele ser el primer paso para resolver un problema de rendimiento.

---

# Servicios

Muchos servicios del sistema permanecen ejecutándose continuamente en segundo plano.

Un servicio mal configurado puede provocar:

- Consumo elevado de CPU.
- Uso excesivo de memoria.
- Acceso continuo al disco.
- Consumo innecesario de red.

Por este motivo es recomendable revisar periódicamente los servicios activos.

---

# Cuello de botella

Se denomina **cuello de botella** al recurso que limita el rendimiento del sistema.

Ejemplo:

```text
CPU      → 15 %

RAM      → 40 %

Red      → 10 %

Disco    → 100 %
```

Aunque la CPU apenas esté trabajando, el disco está completamente ocupado.

En este caso, el almacenamiento constituye el cuello de botella.

---

# Monitorización

Monitorizar consiste en observar el estado de los recursos del sistema para detectar problemas antes de que afecten a los usuarios.

La monitorización permite conocer:

- Utilización de CPU.
- Consumo de memoria.
- Actividad del disco.
- Tráfico de red.
- Procesos más exigentes.
- Estado general del sistema.

Puede realizarse:

- En tiempo real.
- De forma periódica.
- Mediante herramientas automáticas.

---

# Indicadores habituales

Al analizar el rendimiento suelen revisarse indicadores como:

| Recurso | Indicadores |
|----------|-------------|
| CPU | Porcentaje de uso, carga media, tiempo de usuario y sistema |
| Memoria | RAM utilizada, memoria libre, memoria caché, swap |
| Disco | Lecturas/escrituras por segundo, tiempo de respuesta, IOPS |
| Red | Velocidad, latencia, ancho de banda, paquetes enviados y recibidos |
| Procesos | Consumo de CPU, memoria, tiempo de ejecución |

---

# Comparativa

| Linux | Windows |
|--------|----------|
| `top`, `htop`, `vmstat`, `free` | Administrador de tareas |
| `iostat`, `iotop` | Monitor de recursos |
| `sar`, `pidstat` | Monitor de rendimiento (PerfMon) |
| `iftop`, `ss`, `nload` | PowerShell (`Get-Counter`, `Get-Process`) |

---

# Buenas prácticas

- Analiza siempre varios recursos antes de identificar un problema.
- No te centres únicamente en el porcentaje de CPU.
- Revisa la memoria, el disco y la red conjuntamente.
- Compara el rendimiento con valores habituales del sistema.
- Identifica el recurso que actúa como cuello de botella antes de aplicar cambios.
- Utiliza herramientas de monitorización para obtener datos objetivos y evitar conclusiones basadas únicamente en la percepción de lentitud.

---

[⬆️ Volver al índice](#índice)

## Uso de CPU

La **CPU (Central Processing Unit)** es el componente encargado de ejecutar las instrucciones del sistema operativo y de las aplicaciones.

Un uso elevado de CPU puede provocar:

- Lentitud general del sistema.
- Retrasos en la apertura de aplicaciones.
- Mayor tiempo de respuesta.
- Incremento de la temperatura del equipo.
- Mayor consumo energético.

No obstante, una CPU al **100 %** no siempre indica un problema. Puede ser completamente normal durante tareas intensivas como:

- Compresión de archivos.
- Copias de seguridad.
- Compilación de código.
- Renderizado de vídeo.
- Ejecución de máquinas virtuales.

Lo importante es identificar **qué proceso** está utilizando la CPU y durante cuánto tiempo.

---

# Conceptos importantes

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

# Analizar la CPU en Linux

## Ver uso en tiempo real

La herramienta más utilizada es:

```bash
top
```

Muestra:

- Uso de CPU.
- Consumo de memoria.
- Procesos activos.
- Tiempo de actividad del sistema.

---

## Versión mejorada: `htop`

Si está instalada:

```bash
htop
```

Ventajas:

- Interfaz más clara.
- Uso de colores.
- Visualización por núcleo.
- Búsqueda de procesos.
- Finalización de procesos desde la propia herramienta.

---

## Ver la carga del sistema

```bash
uptime
```

Ejemplo:

```text
load average: 0.35, 0.42, 0.50
```

Los tres valores representan la carga media durante:

- 1 minuto.
- 5 minutos.
- 15 minutos.

Como referencia:

- Un valor cercano al número de núcleos suele ser normal.
- Valores muy superiores pueden indicar saturación.

---

## Información del procesador

```bash
lscpu
```

Muestra información como:

- Modelo.
- Arquitectura.
- Núcleos.
- Hilos.
- Frecuencia.
- Caché.

---

## Mostrar procesos ordenados por CPU

```bash
ps aux --sort=-%cpu
```

Ejemplo:

```bash
ps aux --sort=-%cpu | head
```

Permite identificar rápidamente los procesos que más CPU están consumiendo.

---

# Analizar la CPU en Windows

## Administrador de tareas

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

Se muestra información como:

- Uso de CPU.
- Velocidad actual.
- Procesos.
- Núcleos.
- Procesadores lógicos.
- Tiempo activo.

---

## Monitor de recursos

Abrir:

```text
resmon
```

Pestaña:

```text
CPU
```

Permite observar:

- Uso por proceso.
- Uso por servicio.
- Hilos.
- Procesos asociados.

---

## Monitor de rendimiento

Abrir:

```text
perfmon
```

Permite crear contadores personalizados para supervisar la CPU durante largos periodos de tiempo.

Muy utilizado en servidores Windows.

---

## PowerShell

Consultar procesos ordenados por consumo de CPU:

```powershell
Get-Process | Sort-Object CPU -Descending
```

Mostrar los diez primeros:

```powershell
Get-Process |
Sort-Object CPU -Descending |
Select-Object -First 10
```

---

## Información del procesador

```powershell
Get-CimInstance Win32_Processor
```

Muestra:

- Modelo.
- Fabricante.
- Número de núcleos.
- Procesadores lógicos.
- Velocidad máxima.

---

# Interpretación del uso de CPU

| Situación | Interpretación |
|------------|----------------|
| Uso bajo y estable | Funcionamiento normal. |
| Picos breves | Habitual durante tareas intensivas. |
| Uso elevado constante | Posible cuello de botella o proceso problemático. |
| Uso cercano al 100 % durante mucho tiempo | Requiere investigación. |

---

# Diagnóstico

Si la CPU presenta un uso elevado:

1. Identificar el proceso responsable.
2. Comprobar si el comportamiento es esperado.
3. Revisar si existen actualizaciones o errores del proceso.
4. Verificar el uso de memoria y disco.
5. Comprobar si el problema afecta a todos los núcleos o solo a uno.

No siempre es recomendable finalizar un proceso de inmediato, ya que puede tratarse de un servicio esencial del sistema.

---

# Comparativa

| Linux | Windows |
|--------|----------|
| `top` | Administrador de tareas |
| `htop` | Monitor de recursos |
| `ps` | PowerShell (`Get-Process`) |
| `uptime` | PerfMon |
| `lscpu` | `Get-CimInstance Win32_Processor` |

---

# Ejemplo práctico

## Linux

Mostrar los procesos que más CPU consumen:

```bash
ps aux --sort=-%cpu | head
```

Visualizar el sistema en tiempo real:

```bash
htop
```

---

## Windows

Mostrar los procesos con mayor consumo de CPU:

```powershell
Get-Process |
Sort-Object CPU -Descending |
Select-Object -First 10
```

Consultar las características del procesador:

```powershell
Get-CimInstance Win32_Processor
```

---

# Buenas prácticas

- Supervisa la CPU de forma periódica, especialmente en servidores.
- Analiza el consumo junto con la memoria, el disco y la red para obtener una visión completa del sistema.
- No finalices procesos sin conocer su función.
- Mantén el sistema y las aplicaciones actualizadas para corregir posibles problemas de rendimiento.
- Utiliza herramientas de monitorización cuando necesites analizar el comportamiento durante periodos prolongados.
- Investiga cualquier uso elevado y constante que no esté relacionado con tareas previstas.

---

[⬆️ Volver al índice](#índice)

## Uso de memoria RAM

La **memoria RAM (Random Access Memory)** es el espacio de almacenamiento temporal utilizado por el sistema operativo y las aplicaciones mientras se encuentran en ejecución.

Su función principal es proporcionar un acceso rápido a la información que la CPU necesita procesar.

Cuando la memoria RAM disponible es insuficiente, el sistema comienza a utilizar **memoria virtual** (archivo de paginación o *swap*), almacenando parte de la información en el disco. Como el acceso al disco es mucho más lento que a la RAM, esto suele provocar una pérdida significativa de rendimiento.

---

# Conceptos importantes

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

# ¿Es malo tener la RAM llena?

No necesariamente.

Los sistemas operativos modernos intentan aprovechar al máximo la memoria disponible utilizando caché para mejorar el rendimiento.

Por ello es habitual observar un uso elevado de RAM sin que exista ningún problema.

Lo realmente preocupante es cuando:

- La memoria disponible es muy baja.
- El sistema utiliza continuamente la memoria virtual.
- El rendimiento disminuye notablemente debido a la paginación.

---

# Analizar la memoria en Linux

## Ver memoria disponible

```bash
free -h
```

Ejemplo:

```text
               total   used   free  shared  buff/cache  available
Mem:            15Gi   6Gi    2Gi     500Mi      7Gi         8Gi
Swap:            2Gi   0Gi    2Gi
```

La columna más útil suele ser:

```text
available
```

ya que representa la memoria realmente disponible para nuevas aplicaciones.

---

## Monitorización en tiempo real

```bash
top
```

o

```bash
htop
```

Permiten observar:

- Memoria utilizada.
- Memoria libre.
- Uso de swap.
- Consumo por proceso.

---

## Mostrar procesos por consumo de memoria

```bash
ps aux --sort=-%mem
```

Los diez primeros:

```bash
ps aux --sort=-%mem | head
```

---

## Información detallada

```bash
vmstat
```

Muestra información sobre:

- Memoria.
- Swap.
- Procesos.
- CPU.
- Entrada y salida.

---

# Analizar la memoria en Windows

## Administrador de tareas

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

Se muestran datos como:

- RAM instalada.
- RAM utilizada.
- RAM disponible.
- Velocidad.
- Ranuras utilizadas.
- Memoria en caché.

---

## Monitor de recursos

Abrir:

```text
resmon
```

Pestaña:

```text
Memoria
```

Permite analizar:

- Memoria utilizada por proceso.
- Memoria física.
- Memoria disponible.
- Errores de página.
- Memoria en espera.

---

## PowerShell

Consultar la memoria física instalada:

```powershell
Get-CimInstance Win32_PhysicalMemory
```

Consultar el sistema operativo:

```powershell
Get-CimInstance Win32_OperatingSystem
```

Ejemplo:

```powershell
Get-CimInstance Win32_OperatingSystem |
Select-Object TotalVisibleMemorySize,
              FreePhysicalMemory
```

---

## Procesos con mayor consumo de memoria

```powershell
Get-Process |
Sort-Object WorkingSet -Descending |
Select-Object -First 10 Name, WorkingSet
```

---

# Memoria virtual

Cuando la RAM se llena, el sistema utiliza espacio en disco.

Linux:

```text
Swap
```

Windows:

```text
Archivo de paginación (Pagefile)
```

Aunque permite seguir funcionando, su rendimiento es muy inferior al de la memoria RAM.

Un uso continuo de memoria virtual suele indicar:

- Falta de memoria física.
- Aplicaciones demasiado exigentes.
- Fugas de memoria (*memory leaks*).

---

# Fugas de memoria

Una **fuga de memoria** ocurre cuando un programa reserva memoria pero no la libera correctamente.

Consecuencias:

- El consumo de RAM aumenta con el tiempo.
- El sistema se vuelve más lento.
- Puede llegar a agotarse la memoria disponible.

Una aplicación con una fuga de memoria suele mostrar un crecimiento continuo de su consumo de RAM.

---

# Comparativa

| Linux | Windows |
|--------|----------|
| `free -h` | Administrador de tareas |
| `top` | Monitor de recursos |
| `htop` | PerfMon |
| `vmstat` | PowerShell |
| `ps aux --sort=-%mem` | `Get-Process` |

---

# Ejemplo práctico

## Linux

Mostrar memoria disponible:

```bash
free -h
```

Procesos que más memoria consumen:

```bash
ps aux --sort=-%mem | head
```

---

## Windows

Procesos con mayor consumo de memoria:

```powershell
Get-Process |
Sort-Object WorkingSet -Descending |
Select-Object -First 10 Name, WorkingSet
```

Consultar memoria física disponible:

```powershell
Get-CimInstance Win32_OperatingSystem |
Select-Object TotalVisibleMemorySize,
              FreePhysicalMemory
```

---

# Buenas prácticas

- Supervisa periódicamente el uso de la memoria RAM.
- Analiza el consumo junto con la CPU y el disco para obtener una visión completa del sistema.
- Revisa aplicaciones con un crecimiento continuo del consumo de memoria.
- Evita mantener aplicaciones innecesarias ejecutándose en segundo plano.
- Configura adecuadamente la memoria virtual (*swap* o archivo de paginación*).
- Amplía la memoria RAM cuando el uso elevado sea constante y afecte al rendimiento.

---

[⬆️ Volver al índice](#índice)

## Rendimiento del disco

El almacenamiento es uno de los recursos que más influye en el rendimiento de un sistema.

Aunque la CPU y la memoria tengan un uso bajo, un disco saturado puede provocar:

- Lentitud general.
- Apertura lenta de aplicaciones.
- Copias de archivos muy lentas.
- Retrasos en bases de datos.
- Bloqueos temporales del sistema.

Por ello es importante supervisar tanto el espacio disponible como la actividad de entrada y salida (**I/O**).

---

# Conceptos importantes

Al analizar un disco suelen revisarse los siguientes indicadores:

| Indicador | Descripción |
|-----------|-------------|
| Uso del disco (%) | Porcentaje de utilización del dispositivo. |
| Lecturas por segundo | Número de operaciones de lectura realizadas. |
| Escrituras por segundo | Número de operaciones de escritura realizadas. |
| IOPS | Operaciones de entrada/salida por segundo. |
| Latencia | Tiempo que tarda una operación en completarse. |
| Cola de disco | Número de operaciones pendientes de atender. |
| Espacio libre | Capacidad disponible en la unidad. |

---

# HDD vs SSD

El tipo de almacenamiento tiene un gran impacto en el rendimiento.

| HDD | SSD |
|------|-----|
| Componentes mecánicos | Memoria flash |
| Mayor latencia | Muy baja latencia |
| Menor velocidad | Alta velocidad |
| Menor número de IOPS | Gran cantidad de IOPS |
| Más sensible a la fragmentación | La fragmentación apenas afecta |

En servidores modernos es habitual utilizar SSD o NVMe para mejorar el rendimiento.

---

# Analizar el disco en Linux

## Espacio disponible

```bash
df -h
```

Ejemplo:

```text
Filesystem      Size  Used Avail Use%
/dev/sda2       100G   62G   38G  62%
```

---

## Uso de directorios

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

## Actividad del disco

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

## Procesos que utilizan el disco

```bash
iotop
```

Permite identificar qué procesos están realizando más operaciones de lectura y escritura.

> **Nota:** `iotop` puede requerir permisos de administrador.

---

## Información de los dispositivos

```bash
lsblk
```

Muestra:

- Discos.
- Particiones.
- Tamaño.
- Punto de montaje.

---

# Analizar el disco en Windows

## Administrador de tareas

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

Se muestra:

- Tiempo activo.
- Velocidad de lectura.
- Velocidad de escritura.
- Tiempo de respuesta.

---

## Monitor de recursos

Abrir:

```text
resmon
```

Pestaña:

```text
Disco
```

Permite visualizar:

- Procesos que leen y escriben.
- Archivos utilizados.
- Longitud de la cola.
- Actividad por proceso.

---

## Monitor de rendimiento

Abrir:

```text
perfmon
```

Algunos contadores útiles:

- Disk Reads/sec
- Disk Writes/sec
- Avg. Disk Queue Length
- Avg. Disk sec/Read
- Avg. Disk sec/Write

---

## PowerShell

Consultar los discos físicos:

```powershell
Get-PhysicalDisk
```

Consultar las unidades disponibles:

```powershell
Get-Volume
```

Ejemplo:

```powershell
Get-Volume |
Select-Object DriveLetter,
              FileSystem,
              SizeRemaining,
              Size
```

---

# Interpretación

| Situación | Interpretación |
|------------|----------------|
| Uso bajo del disco | Funcionamiento normal. |
| Picos breves | Habitual durante copias o instalaciones. |
| Disco al 100 % durante largos periodos | Posible cuello de botella. |
| Cola elevada | El disco no procesa las solicitudes con suficiente rapidez. |
| Poco espacio libre | Puede afectar al rendimiento y a la estabilidad del sistema. |

---

# Fragmentación

En discos mecánicos (HDD), los archivos pueden quedar almacenados en fragmentos distribuidos por el disco.

Consecuencias:

- Lecturas más lentas.
- Mayor tiempo de acceso.
- Disminución del rendimiento.

En discos SSD no es recomendable realizar desfragmentaciones tradicionales, ya que no aportan mejoras significativas y generan escrituras innecesarias.

---

# Comparativa

| Linux | Windows |
|--------|----------|
| `df` | Explorador de archivos |
| `du` | Propiedades de la unidad |
| `iostat` | Administrador de tareas |
| `iotop` | Monitor de recursos |
| `lsblk` | `Get-PhysicalDisk` |
| `df -h` | `Get-Volume` |

---

# Ejemplo práctico

## Linux

Consultar espacio disponible:

```bash
df -h
```

Ver actividad del disco:

```bash
iostat -x 2
```

Consultar los procesos que más acceden al disco:

```bash
sudo iotop
```

---

## Windows

Consultar los discos físicos:

```powershell
Get-PhysicalDisk
```

Consultar el espacio libre:

```powershell
Get-Volume |
Select-Object DriveLetter,
              SizeRemaining,
              Size
```

---

# Buenas prácticas

- Mantén suficiente espacio libre en las unidades (habitualmente se recomienda disponer de al menos un 15–20 % libre).
- Supervisa periódicamente la actividad del disco en servidores.
- Utiliza SSD o NVMe para cargas de trabajo intensivas.
- Revisa los procesos que realizan un uso excesivo del almacenamiento.
- Evita almacenar registros o archivos temporales de forma indefinida.
- Programa tareas de limpieza y mantenimiento cuando sea necesario.
- Sustituye discos con signos de degradación antes de que fallen.

---

[⬆️ Volver al índice](#índice)

## Rendimiento de red

La red es uno de los recursos más importantes en cualquier sistema conectado.

Un problema de rendimiento en la red puede provocar:

- Lentitud al acceder a recursos compartidos.
- Copias de archivos muy lentas.
- Problemas en aplicaciones web.
- Desconexiones.
- Retrasos en escritorios remotos.
- Mala calidad en videoconferencias y servicios en tiempo real.

Para diagnosticar estos problemas es necesario analizar tanto la configuración como el tráfico y el estado de la conexión.

---

# Conceptos importantes

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

# Ancho de banda vs velocidad

Es habitual confundir ambos conceptos.

- **Ancho de banda:** capacidad máxima de la conexión.
- **Velocidad de transferencia:** velocidad real obtenida en un momento concreto.

Ejemplo:

```text
Conexión:

1 Gbps
```

No significa que siempre se estén transfiriendo datos a esa velocidad.

La velocidad real dependerá de:

- Saturación de la red.
- Servidor remoto.
- Calidad del cableado.
- Equipos intermedios.
- Otros usuarios.

---

# Analizar la red en Linux

## Configuración de interfaces

```bash
ip addr
```

Muestra:

- Interfaces.
- Direcciones IP.
- Estado.
- Máscaras de red.

---

## Estadísticas de red

```bash
ip -s link
```

Permite consultar:

- Paquetes enviados.
- Paquetes recibidos.
- Errores.
- Paquetes descartados.

---

## Conexiones activas

```bash
ss -tuln
```

Muestra:

- Puertos abiertos.
- Protocolos.
- Servicios escuchando.

---

## Tráfico en tiempo real

```bash
iftop
```

Visualiza:

- Equipos conectados.
- Consumo de ancho de banda.
- Velocidad de transmisión.

> **Nota:** `iftop` suele requerir permisos de administrador.

---

## Monitor sencillo

```bash
nload
```

Muestra:

- Velocidad de descarga.
- Velocidad de subida.
- Gráficos en tiempo real.

---

## Comprobar conectividad

```bash
ping 8.8.8.8
```

Permite conocer:

- Latencia.
- Pérdida de paquetes.

---

## Analizar la ruta

```bash
traceroute google.com
```

Muestra los saltos que siguen los paquetes hasta el destino.

---

# Analizar la red en Windows

## Administrador de tareas

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

Se muestra:

- Velocidad de envío.
- Velocidad de recepción.
- Uso de la interfaz.

---

## Monitor de recursos

Abrir:

```text
resmon
```

Pestaña:

```text
Red
```

Permite consultar:

- Procesos con actividad de red.
- Conexiones TCP.
- Puertos abiertos.
- Actividad por proceso.

---

## PowerShell

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

Ejemplo:

```powershell
Get-NetAdapterStatistics
```

Salida:

- Bytes enviados.
- Bytes recibidos.
- Errores.
- Paquetes descartados.

---

## Comprobar conectividad

```powershell
Test-Connection google.com
```

También puede utilizarse:

```powershell
ping google.com
```

---

## Conexiones abiertas

```powershell
Get-NetTCPConnection
```

Permite consultar:

- Dirección local.
- Dirección remota.
- Puerto.
- Estado.

---

# Interpretación

| Situación | Interpretación |
|------------|----------------|
| Latencia baja | Funcionamiento correcto. |
| Latencia elevada | Posible saturación o problema de red. |
| Pérdida de paquetes | Posible fallo de red o hardware. |
| Muchos errores | Revisar cableado o adaptadores. |
| Gran consumo continuo | Analizar el proceso responsable. |

---

# Herramientas adicionales

Algunas herramientas muy utilizadas para analizar el rendimiento de red son:

| Herramienta | Sistema | Función |
|-------------|---------|---------|
| `ping` | Linux / Windows | Comprobar conectividad y latencia. |
| `traceroute` / `tracert` | Linux / Windows | Analizar la ruta hasta un destino. |
| `ss` | Linux | Mostrar conexiones y puertos. |
| `iftop` | Linux | Monitorizar tráfico en tiempo real. |
| `nload` | Linux | Visualizar velocidad de transferencia. |
| `Get-NetTCPConnection` | Windows | Consultar conexiones TCP. |
| `Get-NetAdapterStatistics` | Windows | Obtener estadísticas del adaptador. |

---

# Comparativa

| Linux | Windows |
|--------|----------|
| `ip addr` | `Get-NetIPAddress` |
| `ip -s link` | `Get-NetAdapterStatistics` |
| `ss` | `Get-NetTCPConnection` |
| `iftop` | Monitor de recursos |
| `nload` | Administrador de tareas |
| `ping` | `Test-Connection` |

---

# Ejemplo práctico

## Linux

Consultar la configuración IP:

```bash
ip addr
```

Comprobar la conectividad:

```bash
ping 8.8.8.8
```

Mostrar conexiones activas:

```bash
ss -tuln
```

Visualizar el tráfico:

```bash
sudo iftop
```

---

## Windows

Consultar los adaptadores:

```powershell
Get-NetAdapter
```

Comprobar la conectividad:

```powershell
Test-Connection google.com
```

Mostrar estadísticas del adaptador:

```powershell
Get-NetAdapterStatistics
```

Consultar conexiones TCP:

```powershell
Get-NetTCPConnection
```

---

# Buenas prácticas

- Supervisa periódicamente el uso de la red en servidores y equipos críticos.
- Comprueba la latencia y la pérdida de paquetes cuando existan problemas de conectividad.
- Revisa los procesos que generan un consumo elevado de ancho de banda.
- Mantén actualizados los controladores de las tarjetas de red.
- Verifica el estado del cableado y de los dispositivos de red ante errores frecuentes.
- Utiliza herramientas de monitorización para detectar problemas antes de que afecten a los usuarios.
- Documenta cualquier incidencia o cambio importante en la infraestructura de red.

---

[⬆️ Volver al índice](#índice)

## Monitorización en Linux

La monitorización consiste en observar el estado del sistema de forma continua para detectar problemas de rendimiento antes de que afecten a los usuarios o a los servicios.

Linux dispone de numerosas herramientas para supervisar el consumo de recursos en tiempo real o analizar el comportamiento del sistema a lo largo del tiempo.

Las herramientas pueden clasificarse según el recurso que monitorizan:

- CPU.
- Memoria.
- Disco.
- Red.
- Procesos.
- Sistema completo.

---

# top

`top` es una de las herramientas más conocidas para monitorizar el sistema en tiempo real.

Ejecutar:

```bash
top
```

Permite visualizar:

- Uso de CPU.
- Uso de memoria.
- Procesos activos.
- Tiempo de actividad.
- Carga del sistema.

Controles útiles:

| Tecla | Acción |
|--------|--------|
| `P` | Ordenar por uso de CPU. |
| `M` | Ordenar por uso de memoria. |
| `k` | Finalizar un proceso. |
| `q` | Salir. |

---

# htop

`htop` es una versión mejorada de `top`.

Ejecutar:

```bash
htop
```

Características:

- Interfaz más intuitiva.
- Uso de colores.
- Visualización por núcleos.
- Navegación mediante teclado.
- Búsqueda de procesos.
- Finalización de procesos desde la interfaz.

En muchas distribuciones debe instalarse previamente.

Ejemplo:

```bash
sudo apt install htop
```

---

# free

Consultar el estado de la memoria:

```bash
free -h
```

Muestra:

- Memoria total.
- Memoria utilizada.
- Memoria libre.
- Memoria disponible.
- Swap.

Es una de las herramientas más utilizadas para comprobar rápidamente el consumo de RAM.

---

# vmstat

Consultar estadísticas generales:

```bash
vmstat
```

Actualizar cada segundo:

```bash
vmstat 1
```

Información mostrada:

- Procesos.
- Memoria.
- Swap.
- Entrada y salida.
- CPU.

Resulta especialmente útil para detectar cuellos de botella.

---

# iostat

Analizar el rendimiento del almacenamiento:

```bash
iostat -x 2
```

Permite consultar:

- Lecturas por segundo.
- Escrituras por segundo.
- Tiempo de espera.
- Utilización del disco.

> **Nota:** suele formar parte del paquete `sysstat`.

---

# iotop

Monitorizar la actividad de entrada y salida por proceso:

```bash
sudo iotop
```

Permite identificar:

- Qué proceso está leyendo más datos.
- Qué proceso está escribiendo más datos.
- Velocidad de lectura y escritura.

Muy útil cuando el disco permanece al 100 % de uso.

---

# sar

`sar` (*System Activity Reporter*) permite analizar el rendimiento del sistema utilizando datos históricos.

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

A diferencia de otras herramientas, `sar` puede mostrar información recopilada anteriormente, lo que facilita el análisis de incidencias pasadas.

---

# pidstat

Analizar procesos individualmente:

```bash
pidstat
```

CPU:

```bash
pidstat -u
```

Memoria:

```bash
pidstat -r
```

Disco:

```bash
pidstat -d
```

Permite conocer el comportamiento de cada proceso con gran nivel de detalle.

---

# dstat

`dstat` combina información de varias herramientas en una única vista.

Ejecutar:

```bash
dstat
```

Puede mostrar simultáneamente:

- CPU.
- Memoria.
- Disco.
- Red.
- Procesos.
- Sistema de archivos.

Ejemplo:

```bash
dstat -cdnm
```

Donde:

- `c` → CPU.
- `d` → Disco.
- `n` → Red.
- `m` → Memoria.

---

# uptime

Consultar:

```bash
uptime
```

Ejemplo:

```text
11:42:08 up 15 days, 4:10, 3 users, load average: 0.35, 0.42, 0.51
```

Muestra:

- Hora actual.
- Tiempo encendido.
- Usuarios conectados.
- Carga media.

---

# Herramientas de red

Algunas herramientas habituales para monitorizar la red son:

Consultar conexiones:

```bash
ss -tuln
```

Ver tráfico:

```bash
iftop
```

Velocidad de la interfaz:

```bash
nload
```

---

# Monitorización remota

En servidores es habitual utilizar plataformas de monitorización centralizada.

Algunas de las más utilizadas son:

- Prometheus.
- Grafana.
- Zabbix.
- Nagios.
- Netdata.

Estas herramientas permiten:

- Supervisar múltiples equipos.
- Configurar alertas.
- Visualizar gráficas históricas.
- Detectar incidencias automáticamente.

---

# Comparativa

| Herramienta | Función principal |
|-------------|------------------|
| `top` | Estado general del sistema. |
| `htop` | Monitor interactivo de procesos. |
| `free` | Memoria RAM. |
| `vmstat` | Estadísticas generales. |
| `iostat` | Rendimiento del disco. |
| `iotop` | Actividad de disco por proceso. |
| `sar` | Estadísticas históricas. |
| `pidstat` | Rendimiento por proceso. |
| `dstat` | Resumen de múltiples recursos. |
| `ss` | Conexiones de red. |

---

# Ejemplo práctico

Diagnóstico de un servidor lento:

1. Comprobar la carga general:

```bash
top
```

2. Revisar la memoria:

```bash
free -h
```

3. Analizar el disco:

```bash
iostat -x 2
```

4. Identificar procesos con mayor actividad de disco:

```bash
sudo iotop
```

5. Revisar conexiones de red:

```bash
ss -tuln
```

Este procedimiento permite localizar rápidamente el recurso que está actuando como cuello de botella.

---

# Buenas prácticas

- Supervisa periódicamente los recursos críticos del sistema.
- Utiliza herramientas distintas según el recurso que quieras analizar.
- Compara el estado actual con mediciones anteriores para detectar anomalías.
- Automatiza la monitorización en servidores mediante herramientas especializadas.
- Configura alertas para anticiparte a problemas de rendimiento.
- Documenta las incidencias y las métricas relevantes para facilitar futuros diagnósticos.

---

[⬆️ Volver al índice](#índice)

## Monitorización en Windows

Windows incorpora diversas herramientas para supervisar el estado del sistema y analizar el consumo de recursos en tiempo real.

Estas herramientas permiten detectar:

- Procesos con un consumo elevado.
- Problemas de memoria.
- Saturación del disco.
- Cuellos de botella en la red.
- Fallos de hardware.
- Tendencias de rendimiento a lo largo del tiempo.

Dependiendo de la información que se necesite, puede utilizarse una herramienta gráfica o PowerShell.

---

# Administrador de tareas

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

## Pestaña Procesos

Permite visualizar:

- Aplicaciones abiertas.
- Procesos en segundo plano.
- Uso de CPU.
- Uso de memoria.
- Uso de disco.
- Uso de red.
- Consumo energético (según la versión de Windows).

Puede ordenarse cada columna para localizar rápidamente los procesos que más recursos consumen.

---

## Pestaña Rendimiento

Muestra información en tiempo real sobre:

- CPU.
- Memoria RAM.
- Disco.
- Adaptadores de red.
- GPU.

También incluye datos como:

- Número de núcleos.
- Procesadores lógicos.
- Tiempo activo.
- Velocidad del procesador.
- Memoria instalada.
- Espacio disponible.

---

## Pestaña Usuarios

Permite conocer:

- Usuarios conectados.
- Recursos consumidos por cada usuario.
- Sesiones activas.

Resulta especialmente útil en servidores con Escritorio Remoto (RDS).

---

# Monitor de recursos

Abrir:

```text
resmon
```

O buscar:

```text
Monitor de recursos
```

Permite analizar con mucho más detalle:

- CPU.
- Memoria.
- Disco.
- Red.

Cada pestaña muestra los procesos responsables del consumo de recursos.

---

## CPU

Permite visualizar:

- Uso por proceso.
- Uso por servicio.
- Hilos activos.
- Módulos cargados.

---

## Memoria

Muestra:

- Memoria física utilizada.
- Memoria disponible.
- Memoria en espera.
- Errores de página.

---

## Disco

Permite consultar:

- Archivos abiertos.
- Lecturas por segundo.
- Escrituras por segundo.
- Tiempo de respuesta.
- Longitud de la cola.

---

## Red

Incluye información sobre:

- Procesos que utilizan la red.
- Conexiones TCP.
- Puertos abiertos.
- Actividad por proceso.

---

# Monitor de rendimiento (PerfMon)

Abrir:

```text
perfmon
```

Es la herramienta más completa para monitorizar sistemas Windows.

Permite:

- Supervisar cientos de contadores.
- Registrar datos durante largos periodos.
- Crear informes.
- Configurar alertas.
- Analizar tendencias.

Es ampliamente utilizada en servidores.

---

## Contadores habituales

Algunos de los contadores más utilizados son:

CPU:

```text
Processor

↓

% Processor Time
```

Memoria:

```text
Memory

↓

Available MBytes
```

Disco:

```text
PhysicalDisk

↓

Avg. Disk Queue Length
```

Red:

```text
Network Interface

↓

Bytes Total/sec
```

---

# Monitor de confiabilidad

Abrir:

```text
perfmon /rel
```

O buscar:

```text
Monitor de confiabilidad
```

Permite consultar un historial de:

- Errores de aplicaciones.
- Fallos del sistema.
- Actualizaciones.
- Instalaciones.
- Bloqueos.

Es especialmente útil para investigar problemas recurrentes.

---

# Administrador de dispositivos

Aunque no es una herramienta de monitorización en tiempo real, permite detectar problemas relacionados con el hardware.

Abrir:

```text
devmgmt.msc
```

Permite identificar:

- Controladores con errores.
- Dispositivos deshabilitados.
- Problemas de hardware.

---

# PowerShell

PowerShell permite obtener información de rendimiento mediante diferentes cmdlets.

---

## Procesos

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

## Rendimiento mediante Get-Counter

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

> **Nota:** Los nombres de los contadores pueden variar según el idioma del sistema operativo.

---

## Información general

```powershell
Get-ComputerInfo
```

Permite consultar:

- Sistema operativo.
- Procesador.
- Memoria instalada.
- Fabricante.
- Modelo.

---

# Visor de eventos

Abrir:

```text
eventvwr.msc
```

Permite revisar:

- Errores del sistema.
- Advertencias.
- Eventos de hardware.
- Eventos de aplicaciones.

Aunque no mide directamente el rendimiento, resulta muy útil para identificar el origen de muchos problemas.

---

# Comparativa

| Herramienta | Función principal |
|-------------|------------------|
| Administrador de tareas | Supervisión rápida del sistema. |
| Monitor de recursos | Análisis detallado de CPU, memoria, disco y red. |
| Monitor de rendimiento (PerfMon) | Monitorización avanzada mediante contadores. |
| Monitor de confiabilidad | Historial de errores e incidencias. |
| Visor de eventos | Registro de eventos del sistema. |
| PowerShell | Automatización y consultas de rendimiento. |

---

# Ejemplo práctico

Diagnóstico de un equipo lento:

1. Abrir el Administrador de tareas.

```text
Ctrl + Shift + Esc
```

2. Revisar:

- CPU.
- Memoria.
- Disco.
- Red.

3. Si el problema continúa:

```text
resmon
```

Analizar el proceso responsable.

4. Comprobar errores recientes:

```text
eventvwr.msc
```

5. Revisar el historial del sistema:

```text
perfmon /rel
```

Este procedimiento permite localizar rápidamente la causa de la mayoría de los problemas de rendimiento.

---

# Buenas prácticas

- Utiliza el Administrador de tareas para un diagnóstico rápido.
- Emplea el Monitor de recursos cuando necesites más detalle.
- Configura PerfMon para supervisar servidores de forma continuada.
- Revisa periódicamente el Monitor de confiabilidad para detectar problemas repetitivos.
- Consulta el Visor de eventos cuando sospeches de errores de hardware o software.
- Automatiza las comprobaciones mediante PowerShell cuando sea necesario.

---

[⬆️ Volver al índice](#índice)

## Optimización del rendimiento

Optimizar el rendimiento consiste en mejorar el funcionamiento del sistema utilizando de forma más eficiente los recursos disponibles.

Antes de aplicar cualquier cambio es importante identificar cuál es el **cuello de botella**. Optimizar un recurso que no está limitando el rendimiento rara vez producirá mejoras apreciables.

La optimización puede realizarse sobre:

- CPU.
- Memoria RAM.
- Almacenamiento.
- Red.
- Procesos.
- Servicios.
- Configuración del sistema.

---

# Identificar el cuello de botella

El primer paso siempre debe ser analizar el sistema.

Ejemplo:

```text
CPU      → 18 %

RAM      → 42 %

Disco    → 100 %

Red      → 10 %
```

En este caso, el problema no es la CPU ni la memoria, sino el almacenamiento.

Una optimización eficaz comienza identificando correctamente el recurso que limita el rendimiento.

---

# Optimización de la CPU

Cuando el procesador mantiene un uso elevado durante largos periodos, pueden aplicarse medidas como:

- Finalizar procesos innecesarios.
- Revisar servicios en segundo plano.
- Actualizar aplicaciones con errores conocidos.
- Programar tareas intensivas fuera del horario laboral.
- Distribuir la carga entre varios servidores cuando sea posible.

También conviene comprobar si el uso elevado es puntual o constante.

---

# Optimización de la memoria RAM

Si la memoria disponible es insuficiente:

- Cierra aplicaciones innecesarias.
- Revisa posibles fugas de memoria.
- Ajusta el archivo de paginación o la memoria swap.
- Amplía la memoria RAM si el uso elevado es habitual.

Una utilización alta de RAM no siempre implica un problema; lo importante es comprobar si el sistema está recurriendo continuamente a la memoria virtual.

---

# Optimización del almacenamiento

El almacenamiento suele ser uno de los principales cuellos de botella.

Algunas medidas habituales son:

- Eliminar archivos temporales.
- Liberar espacio en disco.
- Mover datos a unidades con mayor capacidad.
- Sustituir HDD por SSD o NVMe.
- Revisar procesos con gran actividad de lectura o escritura.
- Programar tareas de mantenimiento fuera de las horas de mayor uso.

---

# Optimización de la red

Cuando existen problemas de conectividad o saturación:

- Revisar el estado del cableado.
- Verificar la configuración de red.
- Actualizar los controladores de la tarjeta de red.
- Identificar aplicaciones que consumen un ancho de banda elevado.
- Comprobar la latencia y la pérdida de paquetes.
- Distribuir el tráfico cuando existan varios enlaces disponibles.

---

# Optimización de procesos

Los procesos innecesarios consumen recursos del sistema.

Es recomendable:

- Revisar los programas que se inician automáticamente.
- Finalizar procesos bloqueados.
- Actualizar aplicaciones con problemas conocidos.
- Desinstalar software que ya no se utilice.

No deben finalizarse procesos del sistema sin conocer previamente su función.

---

# Optimización de servicios

Muchos servicios permanecen activos aunque no sean necesarios.

Puede mejorarse el rendimiento:

- Deshabilitando servicios innecesarios.
- Configurando el inicio manual cuando proceda.
- Reiniciando servicios bloqueados.
- Actualizando servicios críticos.

Siempre debe comprobarse el impacto antes de deshabilitar un servicio.

---

# Optimización en Linux

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

# Optimización en Windows

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

# Actualizaciones

Mantener el sistema actualizado mejora tanto la seguridad como el rendimiento.

Es recomendable actualizar:

- Sistema operativo.
- Controladores.
- Firmware.
- Aplicaciones.
- BIOS/UEFI cuando sea necesario.

Muchas actualizaciones incluyen mejoras de rendimiento y corrección de errores.

---

# Automatización

En servidores resulta habitual automatizar determinadas tareas:

- Limpieza de archivos temporales.
- Rotación de registros.
- Supervisión de recursos.
- Copias de seguridad.
- Generación de informes.

Esto reduce la carga administrativa y ayuda a mantener un rendimiento estable.

---

# Cuándo ampliar hardware

En ocasiones la optimización del software no es suficiente.

Puede ser recomendable ampliar hardware cuando:

- La CPU permanece saturada de forma continua.
- La memoria RAM resulta insuficiente de manera habitual.
- El almacenamiento limita el rendimiento incluso tras las tareas de mantenimiento.
- La carga del sistema aumenta debido al crecimiento de usuarios o servicios.

La ampliación de hardware debe realizarse después de analizar el sistema y confirmar que existe un cuello de botella real.

---

# Comparativa

| Recurso | Posibles optimizaciones |
|----------|-------------------------|
| CPU | Revisar procesos y servicios, programar tareas intensivas |
| Memoria | Cerrar aplicaciones, revisar fugas, ampliar RAM |
| Disco | Liberar espacio, sustituir HDD por SSD, revisar I/O |
| Red | Comprobar cableado, latencia y consumo de ancho de banda |
| Sistema | Actualizar software, automatizar mantenimiento |

---

# Ejemplo práctico

Supongamos un servidor con los siguientes datos:

```text
CPU      → 25 %

RAM      → 55 %

Disco    → 98 %

Red      → 12 %
```

En este escenario:

1. Revisar la actividad del disco.
2. Identificar el proceso responsable.
3. Comprobar el espacio disponible.
4. Limpiar archivos innecesarios.
5. Valorar el uso de una unidad SSD si el problema persiste.

No tendría sentido ampliar la memoria RAM o sustituir el procesador, ya que no son el recurso limitante.

---

# Buenas prácticas

- Analiza el sistema antes de aplicar cambios.
- Optimiza únicamente el recurso que actúe como cuello de botella.
- Supervisa el rendimiento antes y después de cada modificación.
- Mantén el sistema actualizado.
- Automatiza las tareas de mantenimiento repetitivas.
- Evita realizar cambios simultáneos; así podrás identificar qué modificación ha producido la mejora.
- Documenta las optimizaciones realizadas y sus resultados.

---

[⬆️ Volver al índice](#índice)

## Buenas prácticas

Mantener un buen rendimiento no depende únicamente del hardware instalado, sino también de una correcta administración y monitorización del sistema.

Aplicar buenas prácticas permite:

- Detectar problemas antes de que afecten a los usuarios.
- Reducir tiempos de inactividad.
- Aprovechar mejor los recursos disponibles.
- Aumentar la estabilidad del sistema.
- Facilitar el mantenimiento y la resolución de incidencias.

---

# Monitorizar de forma periódica

No esperes a que aparezca un problema para revisar el rendimiento.

Supervisa regularmente:

- CPU.
- Memoria RAM.
- Disco.
- Red.
- Procesos.
- Servicios.

En servidores es recomendable utilizar herramientas de monitorización continua.

---

# Identificar el cuello de botella

Antes de aplicar cualquier optimización, determina qué recurso está limitando realmente el rendimiento.

No tomes decisiones basándote únicamente en el uso de la CPU.

Analiza siempre:

- CPU.
- Memoria.
- Disco.
- Red.

---

# Mantener espacio libre en disco

Un disco casi lleno puede provocar:

- Lentitud.
- Problemas con actualizaciones.
- Fallos en aplicaciones.
- Errores en bases de datos.

Como recomendación general, intenta mantener al menos un **15–20 %** de espacio libre en las unidades principales.

---

# Revisar procesos y servicios

Comprueba periódicamente:

- Procesos con un consumo elevado de CPU.
- Aplicaciones que utilizan demasiada memoria.
- Servicios innecesarios.
- Procesos bloqueados.

Finaliza únicamente aquellos procesos cuya función conozcas.

---

# Mantener el sistema actualizado

Instala las actualizaciones del:

- Sistema operativo.
- Controladores.
- Firmware.
- Aplicaciones.

Muchas actualizaciones incluyen mejoras de rendimiento además de correcciones de seguridad.

---

# Automatizar tareas de mantenimiento

Siempre que sea posible, automatiza tareas como:

- Limpieza de archivos temporales.
- Rotación de registros.
- Copias de seguridad.
- Comprobación de espacio libre.
- Generación de informes.
- Monitorización de recursos.

Esto reduce el trabajo manual y ayuda a mantener un rendimiento constante.

---

# Utilizar herramientas adecuadas

Cada herramienta está orientada a un tipo de análisis.

Ejemplos:

Linux:

- `top`
- `htop`
- `free`
- `vmstat`
- `iostat`
- `iotop`
- `sar`

Windows:

- Administrador de tareas.
- Monitor de recursos.
- Monitor de rendimiento (PerfMon).
- PowerShell.

Utiliza la herramienta más adecuada para el recurso que deseas analizar.

---

# Configurar alertas

En servidores resulta recomendable configurar alertas para situaciones como:

- CPU elevada durante un tiempo prolongado.
- Memoria disponible muy baja.
- Poco espacio libre en disco.
- Servicios detenidos.
- Pérdida de conectividad.
- Alto consumo de red.

Las alertas permiten actuar antes de que el problema afecte a los usuarios.

---

# Documentar incidencias

Cuando se produzca un problema de rendimiento, registra información como:

- Fecha y hora.
- Equipo afectado.
- Síntomas observados.
- Recurso implicado.
- Causa identificada.
- Solución aplicada.

Esta información resulta muy útil para resolver incidencias similares en el futuro.

---

# Planificar el crecimiento

El aumento del número de usuarios o servicios puede hacer que los recursos actuales resulten insuficientes.

Revisa periódicamente:

- Uso medio de CPU.
- Consumo de memoria.
- Ocupación del almacenamiento.
- Tráfico de red.

Esto permite anticipar ampliaciones de hardware antes de que aparezcan problemas.

---

# Realizar mantenimiento preventivo

Algunas tareas recomendables son:

- Eliminar archivos innecesarios.
- Revisar registros del sistema.
- Verificar el estado del almacenamiento.
- Comprobar el funcionamiento de las copias de seguridad.
- Revisar servicios y tareas programadas.
- Analizar el estado del hardware.

El mantenimiento preventivo ayuda a reducir averías y mejorar la disponibilidad del sistema.

---

# Resumen de recomendaciones

| Recomendación | Beneficio |
|---------------|-----------|
| Monitorizar periódicamente | Detectar problemas antes de que afecten al servicio. |
| Identificar el cuello de botella | Aplicar optimizaciones eficaces. |
| Mantener espacio libre en disco | Evitar pérdidas de rendimiento. |
| Revisar procesos y servicios | Reducir el consumo innecesario de recursos. |
| Mantener el sistema actualizado | Mejorar rendimiento y seguridad. |
| Automatizar tareas | Reducir errores y trabajo manual. |
| Configurar alertas | Actuar rápidamente ante incidencias. |
| Documentar problemas | Facilitar futuras investigaciones. |
| Planificar el crecimiento | Evitar saturaciones y ampliaciones urgentes. |
| Realizar mantenimiento preventivo | Incrementar la estabilidad del sistema. |

---

[⬆️ Volver al índice](#índice)