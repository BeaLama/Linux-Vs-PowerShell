# Gestión de logs 

## Introducción

Los logs o registros del sistema son archivos que almacenan información sobre el funcionamiento del sistema operativo, las aplicaciones y los servicios.

## Índice

- [Concepto de log](#concepto-de-log)
- [Importancia de los logs](#importancia-de-los-logs)
- [Tipos de logs](#tipos-de-logs)
- [Formato y estructura de un log](#formato-y-estructura-de-un-log)
- [Visor de eventos en Windows](#visor-de-eventos-en-windows)
- [Administración mediante PowerShell](#administracion-mediante-powershell)
- [Logs en Linux](#logs-en-linux)
- [Journalctl y systemd Journal](#journalctl-y-systemd-journal)
- [Rotación y conservación de logs](#rotacion-y-conservacion-de-logs)
- [Monitorización y análisis de logs](#monitorizacion-y-analisis-de-logs)
- [Herramientas de gestión centralizada](#herramientas-de-gestion-centralizada)

---

## Concepto de log

*Un log o registro es un archivo o conjunto de datos donde el sistema operativo, las aplicaciones y los servicios almacenan información sobre los eventos que ocurren durante su funcionamiento.*

**Conceptos clave:**

- **¿Qué es un log?:** Un log es un registro cronológico de eventos generados automáticamente por un sistema o una aplicación.
- **¿Para qué sirven los logs?:** Los logs tienen múltiples aplicaciones en la administración de sistemas.
- **Funcionamiento básico:** El funcionamiento de un sistema de registros puede representarse de la siguiente forma.
- **Información que contiene un log:** Aunque el contenido puede variar según el sistema o la aplicación, normalmente cada registro incluye información como: Fecha y hora del evento.
- **Características de los logs:** Los registros del sistema presentan varias características comunes.
- **Ejemplos de eventos registrados:** Algunos eventos que suelen aparecer en los logs son: Inicio correcto del sistema.

### Logs en Windows y Linux

*Todos los sistemas operativos modernos generan registros automáticamente.*

```bash
journalctl
```

---

**Conceptos clave:**

- **Importancia para la administración:** La consulta de logs es una de las tareas más habituales en la administración de sistemas.

## Importancia de los logs

**Conceptos clave:**

- **Diagnóstico de incidencias:** Una de las funciones principales de los logs es facilitar la resolución de problemas.
- **Supervisión del sistema:** Los registros permiten comprobar el funcionamiento de: Servicios.
- **Investigación de incidentes de seguridad:** Los logs desempeñan un papel fundamental en la ciberseguridad.
- **Auditoría y cumplimiento normativo:** Muchas organizaciones deben conservar registros para cumplir normativas y políticas de seguridad.
- **Análisis del rendimiento:** Los registros también ayudan a detectar problemas relacionados con el rendimiento.
- **Resolución más rápida de problemas:** Cuando una incidencia se acompaña de registros detallados, el administrador puede localizar su origen con mayor rapidez.
- **Toma de decisiones:** El análisis de los registros proporciona información útil para mejorar la infraestructura.
- **Evidencia de eventos:** Los registros actúan como una evidencia de lo ocurrido en el sistema.
- **Consecuencias de no revisar los logs:** No supervisar los registros puede provocar: Errores que permanecen sin detectar.

---

## Tipos de logs

*Los sistemas operativos, aplicaciones y dispositivos generan diferentes tipos de registros según el tipo de evento que desean almacenar.*

**Conceptos clave:**

- **Logs del sistema:** Recogen eventos relacionados con el funcionamiento del sistema operativo.
- **Logs de aplicaciones:** Almacenan los eventos generados por las aplicaciones instaladas.
- **Logs de seguridad:** Registran eventos relacionados con la seguridad del sistema.
- **Logs de servicios:** Los servicios del sistema también generan sus propios registros.
- **Logs de red:** Registran información sobre las comunicaciones realizadas por el equipo.
- **Logs de auditoría:** Los registros de auditoría permiten realizar un seguimiento de las acciones efectuadas por usuarios y administradores.
- **Logs de hardware:** Algunos componentes físicos generan registros relacionados con su funcionamiento.
- **Logs en Windows:** Windows organiza sus registros principalmente en varias categorías dentro del Visor de eventos.

### Logs en Linux

*En Linux los registros suelen almacenarse en el directorio.*

```bash
journalctl
```

---

**Conceptos clave:**

- **Clasificación por nivel de gravedad:** Muchos sistemas clasifican los registros según su importancia.

---

## Formato y estructura de un log

*Aunque los registros pueden variar según el sistema operativo, la aplicación o el dispositivo que los genera, la mayoría siguen una estructura similar.*

**Conceptos clave:**

- **¿Qué es una entrada de log?:** Un log está formado por una colección de entradas o registros.
- **Información habitual:** Aunque el contenido depende del sistema, la mayoría de los registros incluyen los siguientes datos: Fecha y hora.
- **Fecha y hora:** La fecha y la hora indican el momento exacto en que ocurrió el evento.
- **Origen del evento:** El origen identifica el componente que ha generado el registro.

### Nivel de gravedad

*Muchos sistemas clasifican los eventos según su importancia.*

| Nivel | Descripción |
|--------|-------------|
| Información | Evento normal del sistema. |
| Advertencia | Situación que puede requerir atención. |
| Error | Se ha producido un fallo. |
| Crítico | Error grave que afecta al funcionamiento del sistema. |

---

**Conceptos clave:**

- **Identificador del evento:** Algunos sistemas asignan un identificador único a cada tipo de evento.
- **Descripción:** La descripción explica lo ocurrido durante el evento.
- **Ejemplo de una entrada de log:** Una entrada simplificada podría ser.
- **Formatos de almacenamiento:** Los registros pueden almacenarse en distintos formatos.
- **Formato en Windows y Linux:** Windows Los registros del Visor de eventos utilizan un formato estructurado que almacena información como: Fecha.

---

## Visor de eventos en Windows

*El Visor de eventos (*Event Viewer*) es la herramienta integrada en Windows que permite consultar y administrar los registros generados por el sistema operativo, las aplicaciones y los servicios.*

**Conceptos clave:**

- **¿Qué es el Visor de eventos?:** El Visor de eventos es una consola de administración que muestra todos los registros generados por Windows.
- **Abrir el Visor de eventos:** Existen varias formas de acceder a esta herramienta.
- **Interfaz principal:** La consola se divide en tres zonas principales.
- **Registros de Windows:** Los registros principales se encuentran dentro del apartado Registros de Windows.
- **Registro de Aplicación:** Contiene eventos generados por las aplicaciones instaladas.
- **Registro de Sistema:** Almacena eventos relacionados con el propio sistema operativo.
- **Registro de Seguridad:** Contiene eventos relacionados con la seguridad.
- **Información de un evento:** Cada evento incluye información detallada.
- **Filtrar eventos:** Cuando existen miles de registros resulta útil aplicar filtros.
- **Exportar registros:** Los eventos pueden guardarse para su análisis o conservación.
- **Ejemplos de uso:** El Visor de eventos suele utilizarse para: Investigar reinicios inesperados.

---

## Administración mediante PowerShell

*PowerShell permite consultar y administrar los registros de eventos de Windows desde la línea de comandos mediante diferentes cmdlets especializados.*

### Obtener los registros disponibles

*Para mostrar todos los registros de eventos existentes en el sistema.*

```powershell
Get-WinEvent -ListLog *
```

---

### Consultar eventos de un registro

*Para mostrar los eventos de un registro concreto.*

```powershell
Get-WinEvent -LogName System
```
```powershell
Get-WinEvent -LogName Application
```

---

### Mostrar los eventos más recientes

*Para visualizar únicamente los últimos eventos registrados.*

```powershell
Get-WinEvent -LogName System -MaxEvents 10
```

---

### Filtrar eventos por nivel

*Es posible mostrar únicamente los eventos que correspondan a un determinado nivel de gravedad.*

```powershell
Get-WinEvent -LogName System |
Where-Object LevelDisplayName -eq "Error"
```

---

### Buscar eventos por identificador

*Cuando se conoce el Event ID, la búsqueda resulta mucho más sencilla.*

```powershell
Get-WinEvent -FilterHashtable @{
LogName="System";
Id=7036
}
```

---

### Consultar eventos recientes

*También es posible obtener los eventos generados durante un periodo determinado.*

```powershell
Get-WinEvent -FilterHashtable @{
LogName="System";
StartTime=(Get-Date).AddDays(-1)
}
```

---

### Exportar registros

*Los eventos obtenidos pueden exportarse para su posterior análisis.*

```powershell
Get-WinEvent -LogName System |
Export-Csv C:\Informes\logs.csv -NoTypeInformation
```

---

**Conceptos clave:**

- **Utilizar filtros avanzados:** PowerShell permite combinar distintos criterios de búsqueda.

### Automatización mediante scripts

*Una de las principales ventajas de PowerShell consiste en automatizar consultas repetitivas.*

```powershell
Get-WinEvent -LogName System |
Where-Object LevelDisplayName -eq "Critical"
```

---

**Conceptos clave:**

- **Ventajas de PowerShell:** Entre sus principales ventajas destacan: Consultas rápidas.

---

## Logs en Linux

*Linux registra de forma continua los eventos generados por el sistema operativo, los servicios y las aplicaciones.*

### ¿Dónde se almacenan los logs?

*La mayoría de los registros del sistema se almacenan en el directorio.*

```bash
ls /var/log
```

---

### Archivos de log más habituales

*Algunos de los registros más importantes son.*

| Archivo | Contenido |
|----------|-----------|
| `/var/log/syslog` | Eventos generales del sistema. |
| `/var/log/auth.log` | Autenticación e inicios de sesión. |
| `/var/log/kern.log` | Eventos del núcleo (kernel). |
| `/var/log/dmesg` | Mensajes del arranque y hardware. |
| `/var/log/boot.log` | Información del proceso de arranque. |

---

### Consultar un log

*Los archivos de registro pueden visualizarse mediante diferentes comandos.*

```bash
cat /var/log/syslog
```
```bash
less /var/log/syslog
```

---

### Buscar información en un log

*Cuando un registro contiene miles de líneas, resulta útil buscar únicamente la información necesaria.*

```bash
grep "error" /var/log/syslog
```
```bash
grep -i "failed" /var/log/auth.log
```

---

### Supervisar un log en tiempo real

*Es posible visualizar cómo un archivo de log se actualiza mientras el sistema continúa funcionando.*

```bash
tail -f /var/log/syslog
```

---

**Conceptos clave:**

- **Logs de autenticación:** Uno de los registros más importantes es.
- **Logs del kernel:** El archivo.
- **Logs de aplicaciones:** Muchas aplicaciones crean sus propios registros dentro de.
- **Herramientas habituales:** Los administradores utilizan con frecuencia herramientas como: `cat`.

---

## Journalctl y systemd Journal

*Las distribuciones Linux modernas que utilizan systemd incorporan un sistema de registros denominado systemd Journal.*

**Conceptos clave:**

- **¿Qué es systemd Journal?:** systemd Journal es el sistema de registro integrado en systemd.

### ¿Qué es journalctl?

*`journalctl` es la herramienta utilizada para consultar los registros almacenados en systemd Journal.*

```bash
journalctl
```

---

### Mostrar los registros más recientes

*Para visualizar únicamente las últimas entradas.*

```bash
journalctl -n 20
```

---

### Consultar los registros en tiempo real

*Al igual que con `tail -f`, es posible supervisar los registros conforme se generan.*

```bash
journalctl -f
```

---

### Consultar los registros del arranque actual

*Para mostrar únicamente los eventos registrados desde el último inicio del sistema.*

```bash
journalctl -b
```

---

### Consultar un servicio concreto

*Es posible mostrar únicamente los registros asociados a un servicio.*

```bash
journalctl -u ssh
```
```bash
journalctl -u apache2
```

---

### Filtrar por fecha

*Los registros también pueden consultarse indicando un periodo concreto.*

```bash
journalctl --since "today"
```
```bash
journalctl --since "1 hour ago"
```

---

### Filtrar por prioridad

*Los eventos pueden clasificarse según su nivel de gravedad.*

```bash
journalctl -p err
```
```bash
journalctl -p crit
```

---

### Consultar registros del kernel

*Para visualizar únicamente los mensajes del núcleo.*

```bash
journalctl -k
```

---

**Conceptos clave:**

- **Ventajas de systemd Journal:** Entre sus principales ventajas destacan: Centralización de registros.

---

## Rotación y conservación de logs

*Los registros del sistema se generan continuamente y, con el paso del tiempo, pueden ocupar una gran cantidad de espacio en disco.*

**Conceptos clave:**

- **¿Qué es la rotación de logs?:** La rotación de logs consiste en reemplazar un archivo de registro activo por uno nuevo cuando se cumple una determinada condición.
- **Funcionamiento de la rotación:** El proceso de rotación puede representarse de la siguiente forma.
- **Conservación de logs:** La conservación consiste en mantener los registros durante un periodo determinado.
- **Rotación en Linux: logrotate:** En la mayoría de distribuciones Linux, la rotación de logs se realiza mediante la herramienta logrotate.
- **Opciones habituales de logrotate:** Algunas directivas frecuentes son.
- **Rotación en Windows:** Windows también dispone de mecanismos para controlar el tamaño de los registros.
- **Compresión de logs:** Los registros antiguos suelen comprimirse automáticamente para ahorrar espacio.
- **Importancia de conservar los registros:** Mantener los logs durante un periodo adecuado permite: Investigar incidencias antiguas.
- **Riesgos de una mala gestión:** Una gestión incorrecta de los logs puede provocar: Falta de espacio en disco.

---

## Monitorización y análisis de logs

*La generación de registros no resulta útil si estos no son supervisados y analizados de forma periódica.*

**Conceptos clave:**

- **¿Qué es la monitorización de logs?:** La monitorización consiste en supervisar continuamente los registros generados por el sistema para detectar eventos relevantes.
- **Objetivos del análisis de logs:** El análisis de registros permite: Diagnosticar incidencias.
- **Análisis manual:** El análisis manual consiste en revisar directamente los registros.
- **Monitorización automática:** En sistemas con un gran volumen de eventos resulta recomendable automatizar la supervisión.
- **Indicadores importantes:** Durante el análisis conviene prestar especial atención a: Errores críticos.
- **Búsqueda de patrones:** El análisis de logs no se limita a revisar eventos aislados.
- **Generación de alertas:** Muchos sistemas de monitorización permiten configurar alertas automáticas.
- **Elaboración de informes:** Los registros también pueden utilizarse para generar informes periódicos.
- **Procedimiento de análisis:** Un procedimiento habitual puede representarse así.

---

## Herramientas de gestión centralizada

*En infraestructuras con numerosos equipos y servidores, consultar los registros de cada sistema de forma individual resulta poco práctico.*

**Conceptos clave:**

- **¿Qué es una gestión centralizada de logs?:** La gestión centralizada consiste en recopilar los registros generados por diferentes equipos, servidores, dispositivos de red y aplicaciones en un servidor o plataforma común.
- **Ventajas de la centralización:** Centralizar los registros ofrece numerosos beneficios.
- **Syslog:** Uno de los protocolos más utilizados para enviar registros en sistemas Linux y dispositivos de red es Syslog.
- **SIEM:** Un SIEM (*Security Information and Event Management*) es una plataforma especializada en recopilar, correlacionar y analizar registros procedentes de múltiples fuentes.
- **Elastic Stack (ELK):** Una de las soluciones más utilizadas para la gestión centralizada de logs es Elastic Stack, también conocido como ELK.
- **Graylog:** Graylog es otra plataforma muy utilizada para la centralización y análisis de registros.
- **Splunk:** Splunk es una plataforma comercial especializada en el análisis de grandes volúmenes de datos y registros.
- **Microsoft Sentinel:** En entornos Microsoft es habitual utilizar Microsoft Sentinel, un SIEM basado en la nube.
- **Características deseables:** Una herramienta de gestión centralizada debería ofrecer: Recopilación automática de registros.

---

[⬆️ Volver al índice](#índice)
