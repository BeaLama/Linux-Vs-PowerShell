# Monitorización

## Introducción

La monitorización consiste en supervisar de forma continua el estado de un sistema, servidor o infraestructura para detectar problemas antes de que afecten a los usuarios.

---

## Índice

- [Conceptos básicos](#conceptos-básicos)
- [Tipos de monitorización](#tipos-de-monitorización)
- [Métricas principales](#métricas-principales)
- [Monitorización en Linux](#monitorización-en-linux)
- [Monitorización en-Windows](#monitorización-en-windows)
- [Herramientas de monitorización](#herramientas-de-monitorización)
- [Alertas y notificaciones](#alertas-y-notificaciones)

---

## Conceptos básicos

La monitorización consiste en recopilar, analizar y visualizar información sobre el estado de un sistema de forma continua.

Su objetivo es detectar anomalías antes de que se conviertan en incidencias, permitiendo actuar de forma preventiva en lugar de reactiva.

---

### Objetivos de la monitorización

Una correcta monitorización permite:

- Detectar problemas antes de que afecten al servicio.
- Supervisar el estado de servidores y equipos.
- Analizar el rendimiento de aplicaciones.
- Comprobar la disponibilidad de servicios.
- Planificar ampliaciones de infraestructura.
- Reducir los tiempos de resolución de incidencias.
- Generar informes y estadísticas.

---

[⬆️ Volver al índice](#índice)

## Tipos de monitorización

Existen diferentes formas de monitorizar una infraestructura según el objetivo perseguido y el tipo de información que se desea obtener.

---

### Monitorización de infraestructura

Se centra en supervisar el estado del hardware y del sistema operativo.

Elementos monitorizados:

- CPU.
- Memoria RAM.
- Disco.
- Red.

---

### Monitorización de servicios

Comprueba que los servicios se encuentren disponibles y funcionando correctamente.

Ejemplos de servicios:

- HTTP / HTTPS.
- DNS.
- DHCP.
- Active Directory.

---

### Monitorización de aplicaciones

Analiza el funcionamiento de aplicaciones concretas.

Ejemplos:

- ERP.
- CRM.
- Aplicaciones web.
- Servidores de correo.

---

### Monitorización de red

Supervisa el estado de la infraestructura de comunicaciones.

Se pueden controlar:

- Routers.
- Switches.
- Firewalls.
- Puntos de acceso Wi-Fi.

---

### Monitorización de almacenamiento

Permite supervisar el estado de discos y sistemas de almacenamiento.

Aspectos habituales:

- Espacio libre.
- IOPS.
- Latencia.
- Estado SMART.

---

### Monitorización de seguridad

Se centra en detectar comportamientos anómalos o posibles incidentes de seguridad.

Ejemplos:

- Intentos de inicio de sesión fallidos.
- Accesos fuera del horario habitual.
- Cambios de permisos.

---

### Monitorización activa

En la monitorización activa, la herramienta realiza comprobaciones periódicas enviando solicitudes al sistema.

Ejemplos:

- Ping.
- Consultas HTTP.
- Consultas DNS.

---

### Monitorización pasiva

En este caso, el sistema monitorizado envía información cuando ocurre un evento.

Ejemplos:

- Logs.
- Syslog.
- Eventos de Windows.

---

[⬆️ Volver al índice](#índice)

## Métricas principales

Las **métricas** son valores numéricos que describen el estado de un sistema en un momento determinado.

---

### CPU

Una de las métricas más importantes.

Normalmente se monitoriza:

- Uso total (%).
- Uso por núcleo.
- Tiempo de usuario.
- Tiempo de sistema.
- Tiempo inactivo.
- Carga media (Linux).

---

### Memoria RAM

Permite conocer la disponibilidad de memoria física.

Las métricas más habituales son:

- RAM total.
- RAM utilizada.
- RAM libre.
- RAM disponible.
- Caché.
- Swap o archivo de paginación.

---

### Disco

Las métricas relacionadas con el almacenamiento incluyen:

- Espacio libre.
- Espacio utilizado.
- Lecturas por segundo.
- Escrituras por segundo.
- IOPS.
- Latencia.
- Cola de disco.

---

### Red

Las métricas de red permiten supervisar el estado de las comunicaciones.

Las más comunes son:

- Tráfico de entrada.
- Tráfico de salida.
- Latencia.
- Pérdida de paquetes.
- Errores.
- Velocidad de transferencia.

---

### Procesos

Es importante controlar los procesos que consumen más recursos.

Las métricas habituales son:

- Uso de CPU.
- Consumo de memoria.
- Actividad de disco.
- Tráfico de red.
- Tiempo de ejecución.

Esto facilita la identificación de aplicaciones problemáticas.

---

### Servicios

No basta con saber que un servidor está encendido; también hay que comprobar que los servicios funcionan correctamente.

Algunas métricas habituales son:

- Estado del servicio.
- Tiempo de respuesta.
- Número de reinicios.
- Disponibilidad.

---

### Disponibilidad

La disponibilidad (*uptime*) indica el tiempo durante el que un sistema permanece operativo.

Ejemplos:

- Servidor accesible.
- Sitio web disponible.
- Base de datos funcionando.
- Servicio DNS operativo.

---

### Temperatura

En servidores físicos también es habitual supervisar:

- Temperatura del procesador.
- Temperatura de discos.
- Temperatura del chasis.

---

### Alimentación

En equipos empresariales se monitoriza:

- Estado de las fuentes de alimentación.
- Consumo eléctrico.
- Estado de baterías UPS.
- Alimentación redundante.

---

[⬆️ Volver al índice](#índice)

## Monitorización en Linux

Linux dispone de numerosas herramientas para supervisar el estado del sistema, tanto de forma puntual como continua.

---

### Herramientas locales

Las herramientas locales permiten conocer el estado del sistema directamente desde el propio servidor.

Las más utilizadas son:

| Herramienta | Función |
|-------------|---------|
| `top` | Estado general del sistema. |
| `htop` | Monitor interactivo de procesos. |
| `free` | Uso de memoria RAM. |
| `vmstat` | Estadísticas del sistema. |
| `iostat` | Rendimiento del disco. |
| `iotop` | Actividad de disco por proceso. |
| `ss` | Conexiones de red. |
| `sar` | Estadísticas históricas. |
| `pidstat` | Rendimiento por proceso. |
| `dstat` | Resumen de varios recursos. |

Estas herramientas resultan ideales para el diagnóstico de incidencias directamente sobre el servidor.

---

### Monitorización mediante logs

Linux registra continuamente información sobre el funcionamiento del sistema.

Los registros suelen encontrarse en:

```text
/var/log
```

---

### journalctl

En sistemas que utilizan **systemd**, los registros pueden consultarse mediante:

```bash
journalctl
```

Seguir los registros en tiempo real:

```bash
journalctl -f
```

Consultar únicamente los errores:

```bash
journalctl -p err
```

---

### Monitorización de servicios

Comprobar el estado de un servicio:

```bash
systemctl status nginx
```

Listar servicios activos:

```bash
systemctl list-units --type=service
```

Consultar servicios fallidos:

```bash
systemctl --failed
```

---

### Monitorización de procesos

Consultar los procesos con mayor consumo de CPU:

```bash
ps aux --sort=-%cpu
```

Monitorizar procesos en tiempo real:

```bash
htop
```

---

### Monitorización de red

Comprobar conexiones activas:

```bash
ss -tuln
```

Visualizar el tráfico:

```bash
iftop
```

```bash
ping 8.8.8.8
```

---

### Monitorización del almacenamiento

Consultar espacio libre:

```bash
df -h
```

---

### Estado del hardware

Consultar dispositivos de almacenamiento:

```bash
lsblk
```

Información de CPU:

```bash
lscpu
```

Información de memoria:

```bash
cat /proc/meminfo
```

Información general del sistema:

```bash
hostnamectl
```

---

### SMART

El estado de los discos puede comprobarse mediante SMART.

Ejemplo:

```bash
sudo smartctl -a /dev/sda
```

---

[⬆️ Volver al índice](#índice)

## Monitorización en Windows

Windows incorpora numerosas herramientas para supervisar el estado del sistema, analizar el rendimiento y detectar incidencias.

---

### Administrador de tareas

Es la herramienta más utilizada para comprobar rápidamente el estado del sistema.

Abrir:

```text
Ctrl + Shift + Esc
```

---

### Monitor de recursos

Abrir:

```text
resmon
```

---

### Monitor de rendimiento (PerfMon)

Abrir:

```text
perfmon
```

---

### Contadores de rendimiento

PerfMon utiliza **Performance Counters**, que proporcionan métricas del sistema.

Ejemplos:

CPU

```text
Processor

↓

% Processor Time
```

---

### Visor de eventos

Abrir:

```text
eventvwr.msc
```

---

### Monitor de confiabilidad

Abrir:

```text
perfmon /rel
```

---

### PowerShell

PowerShell permite automatizar la recopilación de información.

---

#### Procesos

Procesos con mayor consumo de CPU:

```powershell
Get-Process |
Sort-Object CPU -Descending
```

Procesos con mayor consumo de memoria:

```powershell
Get-Process |
Sort-Object WorkingSet -Descending
```

---

#### Información del sistema

```powershell
Get-ComputerInfo
```

---

#### Rendimiento

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

#### Supervisión de servicios

Consultar todos los servicios:

```powershell
Get-Service
```

---

#### Supervisión de procesos

Procesos ordenados por memoria:

```powershell
Get-Process |
Sort-Object WorkingSet -Descending
```

Procesos ordenados por CPU:

```powershell
Get-Process |
Sort-Object CPU -Descending
```

---

#### Supervisión de red

Consultar adaptadores:

```powershell
Get-NetAdapter
```

---

#### Supervisión del almacenamiento

Consultar discos físicos:

```powershell
Get-PhysicalDisk
```

Consultar volúmenes:

```powershell
Get-Volume
```

Consultar espacio libre:

```powershell
Get-PSDrive -PSProvider FileSystem
```

---

#### WMI

Windows permite obtener información mediante **WMI (Windows Management Instrumentation)**.

Ejemplo:

```powershell
Get-CimInstance Win32_OperatingSystem
```

---

[⬆️ Volver al índice](#índice)

## Herramientas de monitorización

Estas herramientas recopilan información de múltiples dispositivos, almacenan métricas históricas, generan alertas y muestran paneles gráficos con el estado de los sistemas.

---

### Prometheus

**Prometheus** es una plataforma de monitorización de código abierto desarrollada inicialmente por SoundCloud.

Características:

- Código abierto.
- Lenguaje de consultas PromQL.
- Excelente integración con Grafana.

---

### Grafana

**Grafana** es una plataforma de visualización de datos.

No recopila información directamente, sino que obtiene datos de múltiples fuentes como:

- Prometheus.
- InfluxDB.
- MySQL.
- PostgreSQL.
- Elasticsearch.
- Zabbix.

Permite crear:

- Dashboards interactivos.
- Gráficos en tiempo real.
- Informes.
- Alertas.

---

### Zabbix

**Zabbix** es una plataforma de monitorización empresarial muy completa.

Puede funcionar:

- Con agentes.
- Sin agentes.

Monitoriza:

- Linux.
- Windows.
- Equipos de red.
- Bases de datos.
- Aplicaciones.
- Servicios.

Incluye:

- Alertas.
- Mapas.
- Dashboards.
- Descubrimiento automático.
- Informes.

Es una de las soluciones más utilizadas en empresas.

---

[⬆️ Volver al índice](#índice)

## Alertas y notificaciones

Una de las principales ventajas de la monitorización es la posibilidad de generar **alertas automáticas** cuando un sistema presenta un comportamiento anómalo.

---

### ¿Qué es una alerta?

Una alerta es una notificación que se genera cuando una métrica o un evento cumple una condición previamente definida.

Las alertas pueden configurarse para prácticamente cualquier recurso monitorizado.

---

### ¿Cuándo generar una alerta?

No todas las situaciones requieren una alerta.

Es recomendable configurar avisos cuando se detecten condiciones que puedan afectar al funcionamiento del sistema.

Ejemplos:

- CPU muy elevada durante varios minutos.
- Memoria disponible insuficiente.
- Poco espacio libre en disco.

---

### Tipos de notificaciones

Las plataformas de monitorización permiten enviar avisos mediante distintos canales.

Los más habituales son:

- Correo electrónico.
- Mensajes SMS.
- Aplicaciones móviles.

---

[⬆️ Volver al índice](#índice)