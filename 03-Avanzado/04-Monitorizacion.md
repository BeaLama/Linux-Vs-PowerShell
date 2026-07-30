# Monitorización

## Introducción

La monitorización consiste en supervisar de forma continua el estado de un sistema, servidor o infraestructura para detectar problemas antes de que afecten a los usuarios.

A diferencia de las herramientas de diagnóstico utilizadas de forma puntual, la monitorización recopila información constantemente y permite analizar la evolución del sistema a lo largo del tiempo.

Una correcta monitorización permite:

- Detectar incidencias de forma temprana.
- Generar alertas automáticas.
- Analizar tendencias de rendimiento.
- Anticipar problemas de capacidad.
- Reducir tiempos de inactividad.
- Facilitar el diagnóstico de averías.

Actualmente es una práctica imprescindible en cualquier infraestructura profesional, tanto en entornos Linux como Windows.

---

## Índice

- [Conceptos básicos](#conceptos-básicos)
- [Tipos de monitorización](#tipos-de-monitorización)
- [Métricas principales](#métricas-principales)
- [Monitorización en Linux](#monitorización-en-linux)
- [Monitorización en-Windows](#monitorización-en-windows)
- [Herramientas de monitorización](#herramientas-de-monitorización)
- [Alertas y notificaciones](#alertas-y-notificaciones)
- [Buenas prácticas](#buenas-prácticas)

---

## Conceptos básicos

La monitorización consiste en recopilar, analizar y visualizar información sobre el estado de un sistema de forma continua.

Su objetivo es detectar anomalías antes de que se conviertan en incidencias, permitiendo actuar de forma preventiva en lugar de reactiva.

Mientras que una comprobación manual muestra el estado del sistema en un momento concreto, la monitorización registra información de manera constante, facilitando el análisis histórico y la generación de alertas.

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

### ¿Qué se puede monitorizar?

Prácticamente cualquier elemento de una infraestructura puede supervisarse.

Los más habituales son:

- Servidores.
- Equipos cliente.
- Máquinas virtuales.
- Contenedores.
- Bases de datos.
- Aplicaciones.
- Servicios.
- Redes.
- Firewalls.
- Switches.
- Routers.
- Sistemas de almacenamiento.
- Sitios web.

---

### Monitorización proactiva y reactiva

Existen dos formas principales de actuar frente a una incidencia.

### Reactiva

Se interviene cuando el problema ya ha ocurrido.

Ejemplo:

```text
Servidor sin espacio en disco

↓

Los usuarios dejan de poder trabajar

↓

El administrador recibe el aviso
```

---

### Proactiva

El sistema detecta el problema antes de que afecte al servicio.

Ejemplo:

```text
Espacio libre

↓

15 %

↓

Se genera una alerta

↓

El administrador actúa antes del fallo
```

La monitorización moderna busca trabajar siempre de forma proactiva.

---

### Métricas

Una **métrica** es un dato numérico que describe el estado de un recurso.

Ejemplos:

- Uso de CPU.
- Memoria disponible.
- Espacio libre.
- Latencia.
- Temperatura.
- Número de usuarios conectados.
- Tiempo de respuesta.
- Tráfico de red.

Estas métricas se almacenan periódicamente para analizar su evolución.

---

### Eventos

Un **evento** representa un hecho ocurrido en el sistema.

Ejemplos:

- Inicio del servidor.
- Reinicio inesperado.
- Servicio detenido.
- Error de autenticación.
- Disco desconectado.
- Inicio de sesión de un usuario.

Los eventos suelen almacenarse en registros o logs.

---

### Alertas

Una **alerta** se genera cuando una métrica supera un umbral definido.

Ejemplos:

```text
CPU > 90 %

↓

Alerta
```

```text
Espacio libre < 10 %

↓

Alerta
```

```text
Servidor inaccesible

↓

Alerta crítica
```

Las alertas permiten actuar rápidamente ante posibles problemas.

---

### Dashboard

Un **dashboard** es un panel que muestra gráficamente el estado de la infraestructura.

Normalmente incluye:

- CPU.
- RAM.
- Disco.
- Red.
- Servicios.
- Estado de servidores.
- Alertas activas.

Permite conocer de un vistazo la situación general del sistema.

---

### Disponibilidad

Uno de los aspectos más importantes de la monitorización es comprobar que los servicios permanecen disponibles.

Ejemplos:

- Servidor web operativo.
- Base de datos funcionando.
- Servicio DNS respondiendo.
- Correo electrónico disponible.
- VPN activa.

En muchos casos basta con verificar que un puerto o servicio responde correctamente.

---

### Umbrales

Los umbrales determinan cuándo debe generarse una alerta.

Ejemplo:

| Métrica | Advertencia | Crítico |
|----------|------------:|---------:|
| CPU | 80 % | 95 % |
| RAM | 85 % | 95 % |
| Disco | 15 % libre | 5 % libre |
| Latencia | 100 ms | 250 ms |

Estos valores pueden variar según el tipo de infraestructura.

---

### Frecuencia de monitorización

No todos los recursos necesitan comprobarse con la misma frecuencia.

Ejemplo:

| Recurso | Frecuencia habitual |
|----------|--------------------|
| CPU | Cada 30-60 segundos |
| Memoria | Cada minuto |
| Disco | Cada 5 minutos |
| Servicios | Cada minuto |
| Sitios web | Cada 1-5 minutos |
| Copias de seguridad | Diariamente |

Una frecuencia demasiado alta puede generar una carga innecesaria sobre el sistema.

---

### Almacenamiento histórico

Las plataformas de monitorización suelen guardar los datos recopilados durante semanas, meses o incluso años.

Esto permite:

- Comparar el rendimiento entre distintos periodos.
- Detectar tendencias.
- Analizar incidencias pasadas.
- Planificar ampliaciones de infraestructura.

---

### Componentes de un sistema de monitorización

Un sistema de monitorización suele estar formado por:

```text
Equipos y servidores

↓

Recopilación de métricas

↓

Base de datos

↓

Motor de monitorización

↓

Dashboard

↓

Alertas
```

Cada componente cumple una función específica dentro del proceso.

---

### Beneficios

Una infraestructura correctamente monitorizada permite:

- Reducir tiempos de inactividad.
- Detectar incidencias rápidamente.
- Mejorar el rendimiento.
- Automatizar avisos.
- Facilitar auditorías.
- Optimizar la planificación del hardware.
- Incrementar la disponibilidad de los servicios.

---

### Resumen

| Concepto | Descripción |
|----------|-------------|
| Métrica | Valor numérico que describe un recurso. |
| Evento | Suceso registrado por el sistema. |
| Alerta | Aviso generado al superar un umbral. |
| Dashboard | Panel gráfico de supervisión. |
| Umbral | Valor a partir del cual se genera una alerta. |
| Disponibilidad | Estado operativo de un servicio. |

---

[⬆️ Volver al índice](#índice)

## Tipos de monitorización

Existen diferentes formas de monitorizar una infraestructura según el objetivo perseguido y el tipo de información que se desea obtener.

En la práctica, las organizaciones suelen combinar varios tipos de monitorización para obtener una visión completa del estado de sus sistemas.

---

### Monitorización de infraestructura

Se centra en supervisar el estado del hardware y del sistema operativo.

Elementos monitorizados:

- CPU.
- Memoria RAM.
- Disco.
- Red.
- Temperatura.
- Estado del hardware.
- Alimentación eléctrica.
- Ventiladores.

Ejemplo:

```text
Servidor

↓

CPU al 95 %

↓

Alerta
```

---

### Monitorización de servicios

Comprueba que los servicios se encuentren disponibles y funcionando correctamente.

Ejemplos de servicios:

- HTTP / HTTPS.
- DNS.
- DHCP.
- Active Directory.
- LDAP.
- FTP / SFTP.
- SMTP.
- SSH.
- RDP.
- VPN.

No basta con que el servidor esté encendido; el servicio también debe responder correctamente.

---

### Monitorización de aplicaciones

Analiza el funcionamiento de aplicaciones concretas.

Ejemplos:

- ERP.
- CRM.
- Aplicaciones web.
- Servidores de correo.
- Plataformas de virtualización.
- Software de gestión empresarial.

Permite conocer:

- Tiempo de respuesta.
- Número de usuarios.
- Errores.
- Consumo de recursos.
- Disponibilidad.

---

### Monitorización de red

Supervisa el estado de la infraestructura de comunicaciones.

Se pueden controlar:

- Routers.
- Switches.
- Firewalls.
- Puntos de acceso Wi-Fi.
- Enlaces WAN.
- Interfaces de red.

Las métricas más habituales son:

- Latencia.
- Ancho de banda.
- Tráfico.
- Errores.
- Pérdida de paquetes.
- Disponibilidad.

---

### Monitorización de almacenamiento

Permite supervisar el estado de discos y sistemas de almacenamiento.

Aspectos habituales:

- Espacio libre.
- IOPS.
- Latencia.
- Estado SMART.
- RAID.
- Cabinas SAN o NAS.

Detectar un fallo de disco antes de que se produzca una pérdida de datos es uno de sus principales objetivos.

---

### Monitorización de seguridad

Se centra en detectar comportamientos anómalos o posibles incidentes de seguridad.

Ejemplos:

- Intentos de inicio de sesión fallidos.
- Accesos fuera del horario habitual.
- Cambios de permisos.
- Creación de nuevos usuarios.
- Modificaciones de archivos críticos.
- Actividad sospechosa en la red.

Suele complementarse con plataformas SIEM.

---

### Monitorización de disponibilidad

También conocida como **monitorización de uptime**.

Comprueba si un sistema o servicio permanece accesible.

Ejemplo:

```text
Cada minuto

↓

Petición HTTP

↓

¿Responde?

↓

Sí → Correcto

No → Alerta
```

Es uno de los tipos de monitorización más sencillos y utilizados.

---

### Monitorización del rendimiento

Analiza cómo utilizan los recursos las aplicaciones y el sistema operativo.

Incluye:

- CPU.
- RAM.
- Disco.
- Red.
- Procesos.
- Servicios.

Su objetivo es detectar cuellos de botella y optimizar el funcionamiento del sistema.

---

### Monitorización activa

En la monitorización activa, la herramienta realiza comprobaciones periódicas enviando solicitudes al sistema.

Ejemplos:

- Ping.
- Consultas HTTP.
- Consultas DNS.
- Conexiones TCP.
- Acceso a servicios.

Ventajas:

- Detección rápida de fallos.
- Fácil de configurar.
- Muy utilizada para comprobar disponibilidad.

---

### Monitorización pasiva

En este caso, el sistema monitorizado envía información cuando ocurre un evento.

Ejemplos:

- Logs.
- Syslog.
- Eventos de Windows.
- SNMP Traps.
- Alertas generadas por aplicaciones.

Ventajas:

- Menor carga sobre la infraestructura.
- Permite conocer eventos que no serían detectables mediante comprobaciones activas.

---

### Monitorización basada en agentes

Se instala un software (agente) en el equipo monitorizado.

El agente recopila información y la envía al servidor de monitorización.

Ejemplo:

```text
Servidor

↓

Agente

↓

Servidor de monitorización
```

Ventajas:

- Gran cantidad de información.
- Datos muy detallados.
- Mayor capacidad de personalización.

Inconvenientes:

- Requiere instalación y mantenimiento.

---

### Monitorización sin agentes

No se instala ningún software adicional.

La información se obtiene mediante protocolos estándar como:

- SNMP.
- WMI.
- SSH.
- WinRM.
- HTTP.
- ICMP.

Ventajas:

- Configuración sencilla.
- Sin instalación de software.

Inconvenientes:

- Menor nivel de detalle.

---

### Comparativa

| Tipo | Qué supervisa |
|------|---------------|
| Infraestructura | Hardware y sistema operativo |
| Servicios | Disponibilidad de servicios |
| Aplicaciones | Funcionamiento del software |
| Red | Comunicaciones |
| Almacenamiento | Discos y sistemas de almacenamiento |
| Seguridad | Eventos de seguridad |
| Disponibilidad | Estado operativo de equipos y servicios |
| Rendimiento | Uso de recursos |

---

### Activa vs Pasiva

| Activa | Pasiva |
|---------|---------|
| La herramienta realiza comprobaciones | El sistema envía eventos |
| Detecta caídas rápidamente | Detecta eventos específicos |
| Utiliza ping, HTTP, TCP... | Utiliza logs, Syslog, SNMP Traps... |

---

### Agentes vs Sin agentes

| Con agentes | Sin agentes |
|--------------|-------------|
| Mayor cantidad de información | Instalación más sencilla |
| Datos muy detallados | Menor mantenimiento |
| Requiere software adicional | Utiliza protocolos estándar |

---

### Ejemplo práctico

Una empresa puede utilizar varios tipos de monitorización al mismo tiempo:

```text
Servidor Web

↓

CPU, RAM y Disco

↓

Monitorización de infraestructura

↓

HTTP

↓

Monitorización de disponibilidad

↓

Logs

↓

Monitorización de seguridad

↓

Tiempo de respuesta

↓

Monitorización de aplicaciones
```

De esta forma se obtiene una visión completa del estado del sistema.

---

### Buenas prácticas

- Combina distintos tipos de monitorización para cubrir toda la infraestructura.
- No te limites a comprobar que un servidor está encendido; verifica también que sus servicios funcionan correctamente.
- Utiliza monitorización activa para comprobar la disponibilidad y pasiva para registrar eventos relevantes.
- Emplea agentes cuando necesites información detallada y monitorización sin agentes cuando busques simplicidad.
- Ajusta la frecuencia de las comprobaciones según la importancia del recurso.
- Revisa periódicamente los umbrales y alertas para adaptarlos a las necesidades del entorno.

---

[⬆️ Volver al índice](#índice)

## Métricas principales

Las **métricas** son valores numéricos que describen el estado de un sistema en un momento determinado.

Son la base de cualquier plataforma de monitorización, ya que permiten:

- Detectar anomalías.
- Generar alertas.
- Analizar tendencias.
- Comparar periodos de tiempo.
- Planificar ampliaciones de infraestructura.

Las métricas pueden obtenerse cada pocos segundos, minutos u horas, dependiendo de la importancia del recurso supervisado.

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

Ejemplo:

```text
CPU

↓

82 %
```

Un uso elevado constante puede indicar un cuello de botella o un proceso con un consumo excesivo.

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

Ejemplo:

```text
RAM utilizada

↓

91 %
```

Si el sistema comienza a utilizar memoria virtual de forma continua, el rendimiento suele disminuir considerablemente.

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

Ejemplo:

```text
Espacio libre

↓

8 %
```

Es habitual configurar alertas cuando el espacio libre desciende por debajo de determinados umbrales.

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

Ejemplo:

```text
Latencia

↓

15 ms
```

Una latencia elevada o la pérdida de paquetes suelen indicar problemas de conectividad.

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

Ejemplo:

```text
Servicio Web

↓

Activo
```

---

### Disponibilidad

La disponibilidad (*uptime*) indica el tiempo durante el que un sistema permanece operativo.

Ejemplos:

- Servidor accesible.
- Sitio web disponible.
- Base de datos funcionando.
- Servicio DNS operativo.

Muchas organizaciones establecen objetivos de disponibilidad, como:

```text
99,9 %

99,99 %

99,999 %
```

---

### Temperatura

En servidores físicos también es habitual supervisar:

- Temperatura del procesador.
- Temperatura de discos.
- Temperatura del chasis.

Un aumento excesivo puede provocar:

- Reducción del rendimiento (*thermal throttling*).
- Reinicios inesperados.
- Fallos de hardware.

---

### Alimentación

En equipos empresariales se monitoriza:

- Estado de las fuentes de alimentación.
- Consumo eléctrico.
- Estado de baterías UPS.
- Alimentación redundante.

Una fuente defectuosa puede generar una alerta antes de provocar una interrupción del servicio.

---

### Estado SMART

Los discos modernos proporcionan información sobre su estado mediante la tecnología **SMART (Self-Monitoring, Analysis and Reporting Technology)**.

Algunos indicadores son:

- Sectores reasignados.
- Errores de lectura.
- Temperatura.
- Horas de funcionamiento.
- Estado general.

Monitorizar estos valores ayuda a detectar discos próximos al fallo.

---

### Tiempo de respuesta

Muchas aplicaciones se supervisan midiendo cuánto tardan en responder.

Ejemplo:

```text
Página web

↓

350 ms
```

Un incremento progresivo del tiempo de respuesta suele indicar problemas de rendimiento o sobrecarga.

---

### Usuarios conectados

En determinados servicios resulta útil conocer:

- Número de usuarios activos.
- Sesiones abiertas.
- Sesiones remotas.
- Conexiones simultáneas.

Esto permite detectar incrementos de carga o accesos inusuales.

---

### Tendencias

Una métrica aislada aporta poca información.

Lo realmente útil es observar su evolución.

Ejemplo:

```text
CPU

20 %

↓

35 %

↓

55 %

↓

80 %
```

Una tendencia creciente puede indicar la necesidad de ampliar recursos o investigar la causa del incremento.

---

### Métricas habituales

| Recurso | Métricas principales |
|----------|----------------------|
| CPU | Uso, carga, tiempo de usuario y sistema |
| Memoria | RAM utilizada, disponible y swap |
| Disco | Espacio libre, IOPS, latencia, cola |
| Red | Tráfico, latencia, pérdida de paquetes |
| Procesos | CPU, memoria, disco y red por proceso |
| Servicios | Estado y tiempo de respuesta |
| Hardware | Temperatura, ventiladores, alimentación |
| Disponibilidad | Uptime y accesibilidad |

---

### Ejemplo práctico

Un servidor presenta las siguientes métricas:

```text
CPU

92 %
```

```text
RAM

58 %
```

```text
Disco

22 %
```

```text
Red

18 %
```

En este caso, la CPU es el recurso que requiere atención, mientras que el resto de métricas se mantienen dentro de valores normales.

---

### Buenas prácticas

- Supervisa únicamente métricas relevantes para cada tipo de sistema.
- Establece umbrales adecuados para generar alertas.
- Analiza la evolución de las métricas y no solo su valor actual.
- Combina métricas de diferentes recursos para obtener una visión completa del sistema.
- Conserva datos históricos para identificar tendencias y facilitar la planificación de capacidad.
- Revisa periódicamente las métricas monitorizadas para adaptarlas a los cambios de la infraestructura.

---

# Resumen

[⬆️ Volver al índice](#índice)

## Monitorización en Linux

Linux dispone de numerosas herramientas para supervisar el estado del sistema, tanto de forma puntual como continua.

Además de las utilidades incluidas por defecto, existen soluciones profesionales capaces de monitorizar miles de equipos simultáneamente.

La monitorización puede realizarse desde:

- La propia terminal.
- Herramientas gráficas.
- Agentes instalados en el sistema.
- Plataformas centralizadas.

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

Algunos archivos habituales son:

```text
/var/log/syslog
```

```text
/var/log/messages
```

```text
/var/log/auth.log
```

```text
/var/log/kern.log
```

La revisión de estos registros permite detectar errores, fallos de servicios y problemas de seguridad.

---

### journalctl

En sistemas que utilizan **systemd**, los registros pueden consultarse mediante:

```bash
journalctl
```

Mostrar los últimos eventos:

```bash
journalctl -n 50
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

Esto permite detectar rápidamente servicios detenidos o con errores.

---

### Monitorización de procesos

Consultar los procesos con mayor consumo de CPU:

```bash
ps aux --sort=-%cpu
```

Consultar los procesos con mayor consumo de memoria:

```bash
ps aux --sort=-%mem
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

Consultar velocidad de la interfaz:

```bash
nload
```

Comprobar conectividad:

```bash
ping 8.8.8.8
```

Analizar la ruta:

```bash
traceroute google.com
```

---

### Monitorización del almacenamiento

Consultar espacio libre:

```bash
df -h
```

Ver tamaño de directorios:

```bash
du -sh *
```

Analizar actividad del disco:

```bash
iostat -x 2
```

Monitorizar procesos con actividad de disco:

```bash
sudo iotop
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

Permite conocer:

- Temperatura.
- Horas de funcionamiento.
- Sectores defectuosos.
- Estado general del disco.

Normalmente forma parte del paquete:

```text
smartmontools
```

---

### Monitorización remota

En entornos empresariales es habitual centralizar toda la información.

Algunas soluciones muy utilizadas son:

- Prometheus.
- Grafana.
- Zabbix.
- Nagios.
- Checkmk.
- Netdata.
- LibreNMS.

Estas plataformas permiten monitorizar decenas o miles de servidores desde un único panel.

---

### Agentes

Muchas plataformas utilizan un agente instalado en el servidor.

El agente recopila información sobre:

- CPU.
- Memoria.
- Disco.
- Red.
- Procesos.
- Servicios.
- Logs.

Posteriormente envía estos datos al servidor de monitorización.

Ejemplos:

- Zabbix Agent.
- Netdata Agent.
- Prometheus Node Exporter.

---

### Monitorización sin agentes

Algunas herramientas obtienen información utilizando protocolos estándar.

Los más habituales son:

- SSH.
- SNMP.
- HTTP.
- ICMP.

Ventajas:

- No requieren instalación.
- Configuración sencilla.

Inconvenientes:

- Menor nivel de detalle.

---

### Automatización

Muchas tareas de monitorización pueden automatizarse mediante scripts.

Ejemplo:

Comprobar espacio libre:

```bash
df -h
```

Enviar un aviso si el disco supera un determinado porcentaje de uso.

También es habitual utilizar:

- Cron.
- Scripts Bash.
- Systemd Timers.

---

### Comparativa

| Herramienta | Función |
|-------------|---------|
| `top` | Estado general del sistema |
| `htop` | Procesos en tiempo real |
| `journalctl` | Registros del sistema |
| `systemctl` | Servicios |
| `df` | Espacio en disco |
| `iostat` | Rendimiento del disco |
| `ss` | Conexiones de red |
| `smartctl` | Estado SMART de discos |

---

### Ejemplo práctico

Diagnóstico de un servidor con problemas de rendimiento:

1. Comprobar procesos:

```bash
htop
```

2. Revisar memoria:

```bash
free -h
```

3. Analizar actividad del disco:

```bash
iostat -x 2
```

4. Consultar registros:

```bash
journalctl -p err
```

5. Revisar servicios:

```bash
systemctl --failed
```

Con estas comprobaciones suele ser posible identificar rápidamente el origen de la mayoría de incidencias.

---

### Buenas prácticas

- Utiliza herramientas locales para diagnósticos rápidos y plataformas centralizadas para la monitorización continua.
- Revisa periódicamente los registros del sistema.
- Supervisa los servicios críticos y configura alertas ante su detención.
- Comprueba el estado SMART de los discos para anticipar fallos de hardware.
- Automatiza comprobaciones repetitivas mediante scripts o tareas programadas.
- Mantén las herramientas de monitorización actualizadas y documenta los umbrales utilizados.

---

[⬆️ Volver al índice](#índice)

## Monitorización en Windows

Windows incorpora numerosas herramientas para supervisar el estado del sistema, analizar el rendimiento y detectar incidencias.

Estas herramientas permiten monitorizar tanto equipos individuales como grandes infraestructuras empresariales.

La monitorización puede realizarse mediante:

- Herramientas gráficas.
- PowerShell.
- Registros del sistema.
- Agentes de monitorización.
- Plataformas centralizadas.

---

### Administrador de tareas

Es la herramienta más utilizada para comprobar rápidamente el estado del sistema.

Abrir:

```text
Ctrl + Shift + Esc
```

Permite supervisar:

- CPU.
- Memoria.
- Disco.
- Red.
- GPU.
- Procesos.
- Usuarios conectados.
- Programas de inicio.

Resulta ideal para realizar un diagnóstico inicial.

---

### Monitor de recursos

Abrir:

```text
resmon
```

Ofrece información mucho más detallada que el Administrador de tareas.

Permite analizar:

- Procesos.
- CPU.
- Memoria.
- Disco.
- Red.

Además muestra qué proceso está utilizando exactamente cada recurso.

---

### Monitor de rendimiento (PerfMon)

Abrir:

```text
perfmon
```

Es la herramienta de monitorización profesional incluida en Windows.

Permite:

- Supervisar cientos de contadores.
- Crear registros históricos.
- Configurar alertas.
- Generar informes.
- Analizar tendencias.

Es muy utilizada en servidores Windows.

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

Memoria

```text
Memory

↓

Available MBytes
```

Disco

```text
PhysicalDisk

↓

Avg. Disk Queue Length
```

Red

```text
Network Interface

↓

Bytes Total/sec
```

Estos contadores pueden visualizarse en tiempo real o almacenarse para su análisis posterior.

---

### Visor de eventos

Abrir:

```text
eventvwr.msc
```

Permite consultar los registros del sistema.

Los principales registros son:

- Aplicación.
- Sistema.
- Seguridad.
- Instalación.
- Eventos reenviados.

Es una herramienta fundamental para investigar errores y fallos del sistema.

---

### Monitor de confiabilidad

Abrir:

```text
perfmon /rel
```

Muestra un historial cronológico de:

- Bloqueos.
- Errores.
- Actualizaciones.
- Instalaciones.
- Problemas de hardware.

Facilita la identificación de incidencias repetitivas.

---

### PowerShell

PowerShell permite automatizar la recopilación de información.

---

### Procesos

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

### Información del sistema

```powershell
Get-ComputerInfo
```

Obtiene información sobre:

- Sistema operativo.
- Memoria instalada.
- Procesador.
- Fabricante.
- Modelo.

---

### Rendimiento

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

### Supervisión de servicios

Consultar todos los servicios:

```powershell
Get-Service
```

Servicios detenidos:

```powershell
Get-Service |
Where-Object Status -eq Stopped
```

Consultar un servicio concreto:

```powershell
Get-Service Spooler
```

Esto permite comprobar rápidamente el estado de los servicios críticos.

---

### Supervisión de procesos

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

También es posible finalizar procesos:

```powershell
Stop-Process -Id 1234
```

---

### Supervisión de red

Consultar adaptadores:

```powershell
Get-NetAdapter
```

Consultar estadísticas:

```powershell
Get-NetAdapterStatistics
```

Consultar conexiones TCP:

```powershell
Get-NetTCPConnection
```

Comprobar conectividad:

```powershell
Test-Connection google.com
```

---

### Supervisión del almacenamiento

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

### WMI

Windows permite obtener información mediante **WMI (Windows Management Instrumentation)**.

Ejemplo:

```powershell
Get-CimInstance Win32_OperatingSystem
```

Otros ejemplos:

```powershell
Get-CimInstance Win32_Processor
```

```powershell
Get-CimInstance Win32_LogicalDisk
```

Muchas plataformas de monitorización utilizan WMI para obtener información de equipos Windows.

---

### Plataformas de monitorización

Las soluciones empresariales más utilizadas son:

- Microsoft System Center Operations Manager (SCOM).
- Zabbix.
- PRTG Network Monitor.
- Nagios.
- Checkmk.
- Prometheus + Windows Exporter.
- Grafana.
- ManageEngine OpManager.

Estas herramientas permiten centralizar la monitorización de cientos o miles de equipos Windows.

---

### Agentes

Muchas plataformas utilizan un agente instalado en el equipo.

Ejemplos:

- Windows Exporter.
- Zabbix Agent.
- PRTG Probe.
- SCOM Agent.

El agente recopila información y la envía al servidor de monitorización.

---

### Automatización

PowerShell permite automatizar tareas de supervisión.

Ejemplo:

Comprobar espacio libre:

```powershell
Get-Volume
```

Comprobar servicios detenidos:

```powershell
Get-Service |
Where-Object Status -eq Stopped
```

Estos scripts pueden ejecutarse mediante:

- Programador de tareas.
- PowerShell Remoting.
- Plataformas de monitorización.

---

### Comparativa

| Herramienta | Función |
|-------------|---------|
| Administrador de tareas | Diagnóstico rápido |
| Monitor de recursos | Análisis detallado |
| PerfMon | Monitorización avanzada |
| Visor de eventos | Registros del sistema |
| Monitor de confiabilidad | Historial de incidencias |
| PowerShell | Automatización |
| WMI | Obtención de información del sistema |

---

### Ejemplo práctico

Diagnóstico de un servidor Windows:

1. Revisar procesos:

```text
Ctrl + Shift + Esc
```

2. Analizar recursos:

```text
resmon
```

3. Consultar errores recientes:

```text
eventvwr.msc
```

4. Comprobar servicios:

```powershell
Get-Service
```

5. Obtener métricas del sistema:

```powershell
Get-Counter '\Processor(_Total)\% Processor Time'
```

Este procedimiento permite identificar rápidamente la mayoría de problemas relacionados con el rendimiento.

---

### Buenas prácticas

- Utiliza el Administrador de tareas para un análisis rápido y PerfMon para una supervisión más completa.
- Revisa periódicamente el Visor de eventos y el Monitor de confiabilidad.
- Automatiza comprobaciones habituales mediante PowerShell.
- Supervisa los servicios críticos y configura alertas cuando se detengan.
- Aprovecha WMI y PowerShell para integrar equipos Windows en plataformas de monitorización centralizada.
- Documenta los contadores y umbrales utilizados en tu infraestructura.

---

[⬆️ Volver al índice](#índice)

## Herramientas de monitorización

Aunque los sistemas operativos incluyen utilidades para supervisar el estado de un equipo, en entornos profesionales se utilizan plataformas especializadas que permiten centralizar la monitorización de toda la infraestructura.

Estas herramientas recopilan información de múltiples dispositivos, almacenan métricas históricas, generan alertas y muestran paneles gráficos con el estado de los sistemas.

Dependiendo de la solución elegida, pueden monitorizar:

- Servidores.
- Equipos cliente.
- Máquinas virtuales.
- Contenedores.
- Redes.
- Aplicaciones.
- Bases de datos.
- Servicios.
- Dispositivos IoT.
- Equipos de red.

---

### Prometheus

**Prometheus** es una plataforma de monitorización de código abierto desarrollada inicialmente por SoundCloud.

Su funcionamiento se basa en recopilar métricas mediante consultas periódicas (*pull*).

Características:

- Código abierto.
- Muy utilizada en Kubernetes.
- Base de datos de series temporales.
- Lenguaje de consultas PromQL.
- Excelente integración con Grafana.

Es una de las herramientas más utilizadas actualmente en entornos Linux y cloud.

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

Es habitual utilizar Grafana junto con Prometheus.

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

### Nagios

**Nagios** es una de las herramientas de monitorización más veteranas.

Características:

- Gran estabilidad.
- Amplio catálogo de plugins.
- Muy configurable.
- Monitorización de servicios y disponibilidad.

Aunque su interfaz es menos moderna que otras soluciones, sigue siendo ampliamente utilizada.

---

### Checkmk

**Checkmk** simplifica la administración de grandes infraestructuras.

Características:

- Descubrimiento automático.
- Gestión centralizada.
- Dashboards.
- Integración con Nagios.
- Supervisión mediante agentes o sin ellos.

Está especialmente orientada a grandes organizaciones.

---

### PRTG Network Monitor

**PRTG** es una solución comercial desarrollada por Paessler.

Se caracteriza por utilizar sensores.

Puede monitorizar:

- Redes.
- Servidores.
- Bases de datos.
- Aplicaciones.
- Equipos industriales.
- Servicios cloud.

Incluye una interfaz muy sencilla y rápida de configurar.

---

### Netdata

**Netdata** es una herramienta centrada en la monitorización en tiempo real.

Características:

- Instalación sencilla.
- Interfaz web.
- Muy bajo consumo.
- Actualización en tiempo real.

Resulta ideal para supervisar servidores Linux individuales.

---

### LibreNMS

**LibreNMS** está orientado principalmente a la monitorización de redes.

Supervisa:

- Switches.
- Routers.
- Firewalls.
- Impresoras.
- NAS.
- Equipos mediante SNMP.

Incluye:

- Descubrimiento automático.
- Mapas.
- Alertas.
- Informes.

---

### Microsoft SCOM

**System Center Operations Manager (SCOM)** es la solución de Microsoft para la monitorización empresarial.

Está especialmente orientada a:

- Windows Server.
- Active Directory.
- SQL Server.
- Exchange.
- Hyper-V.
- Azure.

Permite una integración muy profunda con el ecosistema Microsoft.

---

### Comparativa

| Herramienta | Código abierto | Windows | Linux | Dashboards | Alertas |
|--------------|:-------------:|:--------:|:------:|:----------:|:--------:|
| Prometheus | ✔ | ✔ | ✔ | Parcial | ✔ |
| Grafana | ✔ | ✔ | ✔ | ✔ | ✔ |
| Zabbix | ✔ | ✔ | ✔ | ✔ | ✔ |
| Nagios | ✔ | ✔ | ✔ | Básicos | ✔ |
| Checkmk | ✔ / Comercial | ✔ | ✔ | ✔ | ✔ |
| PRTG | ✘ | ✔ | ✔ | ✔ | ✔ |
| Netdata | ✔ | ✔ | ✔ | ✔ | ✔ |
| LibreNMS | ✔ | ✔ | ✔ | ✔ | ✔ |
| SCOM | ✘ | ✔ | Parcial | ✔ | ✔ |

---

### Agentes

Muchas herramientas utilizan un agente instalado en el equipo.

Ventajas:

- Información muy detallada.
- Recopilación automática.
- Mayor número de métricas.

Ejemplos:

- Zabbix Agent.
- Windows Exporter.
- Node Exporter.
- SCOM Agent.

---

### Sin agentes

Otras herramientas utilizan protocolos estándar.

Los más habituales son:

- SNMP.
- WMI.
- SSH.
- WinRM.
- HTTP.
- ICMP.

Ventajas:

- No requieren instalación.
- Configuración más sencilla.

Inconvenientes:

- Menor nivel de detalle.

---

### Exporters

En Prometheus es habitual utilizar **exporters**, pequeños servicios que exponen métricas para distintos componentes.

Algunos ejemplos:

| Exporter | Función |
|-----------|---------|
| Node Exporter | Métricas de Linux. |
| Windows Exporter | Métricas de Windows. |
| Blackbox Exporter | HTTP, HTTPS, DNS, ICMP y TCP. |
| MySQL Exporter | Bases de datos MySQL. |
| PostgreSQL Exporter | Bases de datos PostgreSQL. |
| SNMP Exporter | Equipos de red mediante SNMP. |

---

### ¿Qué herramienta elegir?

La elección depende del entorno.

| Situación | Herramienta recomendada |
|------------|-------------------------|
| Servidores Linux | Prometheus + Grafana |
| Infraestructura mixta | Zabbix |
| Redes | LibreNMS o PRTG |
| Windows empresarial | SCOM |
| Servidor individual | Netdata |
| Alta personalización | Prometheus |
| Configuración sencilla | PRTG |

No existe una solución única para todos los escenarios.

---

### Ejemplo práctico

Supongamos una empresa con:

- 50 servidores Linux.
- 20 servidores Windows.
- 40 switches.
- 10 firewalls.

Una posible arquitectura sería:

```text
Servidores Linux
        │
        ├────────────┐
        │            │
Windows Exporter  Node Exporter
        │            │
        └──────┬─────┘
               │
          Prometheus
               │
           Grafana
               │
      Dashboards y alertas
```

En otros entornos podría optarse por una única plataforma como Zabbix para centralizar toda la infraestructura.

---

### Buenas prácticas

- Elige la herramienta en función del tamaño y las necesidades de la infraestructura.
- Centraliza la monitorización siempre que sea posible.
- Combina herramientas de recopilación de métricas con plataformas de visualización.
- Utiliza agentes cuando necesites información detallada y monitorización sin agentes para dispositivos donde no sea posible instalar software.
- Configura correctamente las alertas para evitar tanto falsos positivos como incidencias sin detectar.
- Mantén las herramientas de monitorización actualizadas y documenta su configuración.

---

[⬆️ Volver al índice](#índice)

## Alertas y notificaciones

Una de las principales ventajas de la monitorización es la posibilidad de generar **alertas automáticas** cuando un sistema presenta un comportamiento anómalo.

En lugar de esperar a que un usuario informe de un problema, la plataforma de monitorización detecta la incidencia y avisa al administrador de forma inmediata.

Esto permite actuar rápidamente y, en muchos casos, evitar que el problema llegue a afectar al servicio.

---

### ¿Qué es una alerta?

Una alerta es una notificación que se genera cuando una métrica o un evento cumple una condición previamente definida.

Ejemplo:

```text
CPU > 90 %

↓

Alerta
```

Otro ejemplo:

```text
Servidor no responde

↓

Alerta crítica
```

Las alertas pueden configurarse para prácticamente cualquier recurso monitorizado.

---

### ¿Cuándo generar una alerta?

No todas las situaciones requieren una alerta.

Es recomendable configurar avisos cuando se detecten condiciones que puedan afectar al funcionamiento del sistema.

Ejemplos:

- CPU muy elevada durante varios minutos.
- Memoria disponible insuficiente.
- Poco espacio libre en disco.
- Servicio detenido.
- Servidor inaccesible.
- Pérdida de conectividad.
- Temperatura excesiva.
- Fallo de un disco.
- Número elevado de errores en los registros.

---

### Umbrales

Las alertas se basan normalmente en **umbrales**.

Un umbral define el valor a partir del cual se considera que existe un problema.

Ejemplo:

| Métrica | Advertencia | Crítico |
|----------|------------:|---------:|
| CPU | 80 % | 95 % |
| RAM | 85 % | 95 % |
| Disco | 15 % libre | 5 % libre |
| Latencia | 100 ms | 250 ms |

Utilizar varios niveles permite priorizar las incidencias.

---

### Niveles de severidad

La mayoría de plataformas clasifican las alertas según su gravedad.

Un ejemplo habitual es:

| Nivel | Descripción |
|--------|-------------|
| Información | Evento informativo, sin impacto. |
| Advertencia | Posible problema que conviene revisar. |
| Crítico | Incidencia que requiere actuación inmediata. |

Esta clasificación ayuda a priorizar el trabajo del administrador.

---

### Evitar falsos positivos

Una alerta no debería generarse por un problema puntual de pocos segundos.

Ejemplo incorrecto:

```text
CPU > 90 %

↓

1 segundo

↓

Alerta
```

Ejemplo recomendado:

```text
CPU > 90 %

↓

5 minutos

↓

Alerta
```

De esta forma se reducen los avisos innecesarios.

---

### Tipos de notificaciones

Las plataformas de monitorización permiten enviar avisos mediante distintos canales.

Los más habituales son:

- Correo electrónico.
- Mensajes SMS.
- Aplicaciones móviles.
- Microsoft Teams.
- Slack.
- Discord.
- Telegram.
- Webhooks.
- Sistemas de ticketing.

En muchas organizaciones se utilizan varios canales al mismo tiempo.

---

### Escalado de alertas

Cuando una incidencia no se resuelve en un tiempo determinado, puede notificarse automáticamente a otro responsable.

Ejemplo:

```text
Alerta

↓

Administrador de guardia

↓

Sin respuesta durante 15 minutos

↓

Supervisor

↓

Sin respuesta durante 30 minutos

↓

Responsable del departamento
```

Este mecanismo se conoce como **escalado**.

---

### Alertas por disponibilidad

Una de las comprobaciones más habituales consiste en verificar que un servicio sigue disponible.

Ejemplo:

```text
HTTP

↓

Sin respuesta

↓

Alerta
```

Otros ejemplos:

- DNS no responde.
- Servidor SSH inaccesible.
- Base de datos detenida.
- VPN desconectada.

---

### Alertas por rendimiento

También pueden configurarse alertas relacionadas con el uso de recursos.

Ejemplos:

```text
RAM

↓

95 %

↓

Alerta
```

```text
Espacio libre

↓

4 %

↓

Alerta crítica
```

```text
Temperatura

↓

85 °C

↓

Alerta
```

---

### Alertas por eventos

No todas las alertas dependen de métricas.

También pueden generarse a partir de eventos del sistema.

Ejemplos:

- Reinicio inesperado.
- Error de autenticación.
- Creación de un nuevo usuario administrador.
- Servicio detenido.
- Fallo de un disco.
- Cambio de configuración.

Estas alertas suelen obtenerse a partir de registros o logs.

---

### Mantenimiento programado

Antes de realizar tareas de mantenimiento es recomendable desactivar temporalmente las alertas relacionadas.

Ejemplo:

```text
Actualización del servidor

↓

Reinicio previsto

↓

Sin alertas
```

Una vez finalizado el mantenimiento, las alertas deben volver a habilitarse.

---

### Buenas prácticas para las alertas

Una alerta debe cumplir varias condiciones:

- Ser relevante.
- Ser clara.
- Indicar qué recurso está afectado.
- Mostrar la gravedad del problema.
- Facilitar el diagnóstico.
- Evitar duplicados.

Una alerta mal diseñada genera más problemas que beneficios.

---

### Ejemplo práctico

Supongamos que un servidor alcanza un uso elevado de CPU.

Configuración:

```text
CPU > 90 %

↓

Durante 5 minutos

↓

Nivel crítico

↓

Enviar correo

↓

Crear ticket

↓

Enviar mensaje a Teams
```

Si el uso vuelve a la normalidad antes de los cinco minutos, no se genera ninguna alerta.

---

### Comparativa

| Tipo de alerta | Ejemplo |
|----------------|---------|
| Disponibilidad | Servidor sin respuesta |
| Rendimiento | CPU al 95 % |
| Almacenamiento | Disco con menos del 5 % libre |
| Red | Latencia elevada |
| Hardware | Temperatura excesiva |
| Seguridad | Múltiples intentos de inicio de sesión fallidos |
| Servicios | Servicio detenido |

---

### Buenas prácticas

- Configura umbrales realistas adaptados a tu infraestructura.
- Utiliza varios niveles de severidad para priorizar las incidencias.
- Evita generar alertas por problemas temporales o de corta duración.
- Configura distintos canales de notificación según la criticidad del servicio.
- Implementa mecanismos de escalado para incidencias críticas.
- Desactiva temporalmente las alertas durante mantenimientos programados.
- Revisa periódicamente las reglas de alerta para eliminar falsos positivos y adaptar los umbrales a la evolución de la infraestructura.

---

[⬆️ Volver al índice](#índice)

## Buenas prácticas

Una plataforma de monitorización solo resulta útil si está correctamente configurada y mantenida.

Monitorizar demasiados elementos puede generar ruido y dificultar la detección de incidencias importantes, mientras que una monitorización insuficiente puede provocar que los problemas pasen desapercibidos.

Aplicar buenas prácticas permite obtener información útil, reducir falsos positivos y mejorar la disponibilidad de los sistemas.

---

### Monitoriza lo realmente importante

No es necesario monitorizar absolutamente todo.

Prioriza siempre los elementos críticos:

- Servidores.
- Bases de datos.
- Servicios esenciales.
- Equipos de red.
- Sistemas de almacenamiento.
- Aplicaciones de producción.

Esto facilita la identificación rápida de incidencias relevantes.

---

### Define umbrales adecuados

Los umbrales deben adaptarse a las características de cada sistema.

Ejemplo:

Un servidor con una CPU al 80 % de forma habitual puede estar funcionando correctamente.

Por el contrario, otro servidor con una CPU al 80 % de forma puntual puede indicar un problema.

Evita utilizar los mismos valores para todos los equipos.

---

### Evita los falsos positivos

Uno de los problemas más habituales es generar demasiadas alertas.

Si el administrador recibe decenas de avisos diarios que no requieren actuación, terminará ignorándolos.

Para evitarlo:

- Añade tiempos de espera antes de generar una alerta.
- Agrupa eventos relacionados.
- Elimina comprobaciones innecesarias.
- Ajusta correctamente los umbrales.

Una alerta debe indicar un problema real.

---

### Clasifica las alertas

No todas las incidencias tienen la misma importancia.

Organiza las alertas por niveles de gravedad.

Ejemplo:

| Nivel | Actuación |
|--------|-----------|
| Información | No requiere intervención inmediata. |
| Advertencia | Revisar cuando sea posible. |
| Crítico | Actuación inmediata. |

Esta clasificación facilita la priorización del trabajo.

---

### Centraliza la monitorización

Siempre que sea posible, utiliza una plataforma centralizada.

Ventajas:

- Un único panel de control.
- Gestión más sencilla.
- Alertas unificadas.
- Informes centralizados.
- Históricos compartidos.

Esto resulta especialmente útil en infraestructuras con numerosos equipos.

---

### Conserva métricas históricas

Los datos históricos permiten:

- Analizar tendencias.
- Detectar patrones.
- Investigar incidencias pasadas.
- Planificar ampliaciones.

No elimines los datos demasiado pronto.

La información histórica es muy valiosa para la administración del sistema.

---

### Documenta la configuración

Registra información como:

- Equipos monitorizados.
- Servicios supervisados.
- Umbrales configurados.
- Destinatarios de las alertas.
- Procedimientos de actuación.

Una buena documentación facilita el mantenimiento y la resolución de incidencias.

---

### Revisa periódicamente la configuración

La infraestructura cambia con el tiempo.

Es recomendable revisar periódicamente:

- Equipos monitorizados.
- Servicios existentes.
- Umbrales.
- Canales de notificación.
- Alertas obsoletas.

Esto evita mantener configuraciones innecesarias.

---

### Supervisa la propia plataforma

La herramienta de monitorización también puede fallar.

Comprueba regularmente:

- Estado del servidor de monitorización.
- Espacio libre.
- Base de datos.
- Copias de seguridad.
- Agentes.
- Actualizaciones.

Una plataforma caída no podrá detectar incidencias en el resto de la infraestructura.

---

### Automatiza siempre que sea posible

Automatiza tareas como:

- Descubrimiento de equipos.
- Alta de nuevos servidores.
- Generación de informes.
- Limpieza de datos antiguos.
- Actualizaciones de agentes.
- Envío de alertas.

La automatización reduce errores y simplifica la administración.

---

### Protege la plataforma

La monitorización suele almacenar información muy sensible.

Es recomendable:

- Limitar el acceso mediante permisos.
- Utilizar autenticación multifactor cuando sea posible.
- Cifrar las comunicaciones.
- Mantener el software actualizado.
- Registrar los accesos administrativos.
- Realizar copias de seguridad periódicas.

La seguridad de la plataforma es tan importante como la del resto de la infraestructura.

---

### Prueba las alertas

Configurar una alerta no garantiza que funcione correctamente.

Realiza pruebas periódicas para comprobar:

- Que la alerta se genera.
- Que llega al destinatario correcto.
- Que el procedimiento de actuación es el adecuado.

Esto evita descubrir fallos en el sistema de notificaciones durante una incidencia real.

---

### Escala la monitorización

A medida que la infraestructura crece, la plataforma debe adaptarse.

Ten en cuenta:

- Número de equipos.
- Cantidad de métricas.
- Frecuencia de recopilación.
- Espacio necesario para históricos.
- Rendimiento del servidor de monitorización.

Una plataforma sobredimensionada o infradimensionada puede afectar a la calidad de la supervisión.

---

### Resumen de recomendaciones

| Recomendación | Beneficio |
|---------------|-----------|
| Monitorizar recursos críticos | Detectar antes las incidencias importantes |
| Ajustar umbrales | Reducir falsos positivos |
| Clasificar alertas | Priorizar actuaciones |
| Centralizar la monitorización | Simplificar la gestión |
| Conservar históricos | Analizar tendencias |
| Documentar la configuración | Facilitar el mantenimiento |
| Revisar periódicamente la plataforma | Mantener la monitorización actualizada |
| Automatizar tareas | Reducir errores y trabajo manual |
| Proteger la plataforma | Evitar accesos no autorizados |
| Probar las alertas | Garantizar su funcionamiento |

---

[⬆️ Volver al índice](#índice)