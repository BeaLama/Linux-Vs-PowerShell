# Gestión de logs

## Introducción

Los **logs** o registros del sistema son archivos que almacenan información sobre el funcionamiento del sistema operativo, las aplicaciones y los servicios. Gracias a ellos es posible conocer qué eventos han ocurrido, identificar errores, detectar incidentes de seguridad y analizar el comportamiento de un equipo o servidor.

La gestión de logs constituye una tarea fundamental para cualquier administrador de sistemas, ya que permite diagnosticar problemas, realizar auditorías, supervisar la actividad del sistema y cumplir con numerosos requisitos de seguridad y normativa. Tanto Windows como Linux incorporan herramientas específicas para generar, consultar y administrar estos registros.

## Índice

- [Concepto de log](#concepto-de-log)
- [Importancia de los logs](#importancia-de-los-logs)
- [Tipos de logs](#tipos-de-logs)
- [Formato y estructura de un log](#formato-y-estructura-de-un-log)
- [Visor de eventos en Windows](#visor-de-eventos-en-windows)
- [Administración mediante PowerShell](#administración-mediante-powershell)
- [Logs en Linux](#logs-en-linux)
- [Journalctl y systemd Journal](#journalctl-y-systemd-journal)
- [Rotación y conservación de logs](#rotación-y-conservación-de-logs)
- [Monitorización y análisis de logs](#monitorización-y-análisis-de-logs)
- [Herramientas de gestión centralizada](#herramientas-de-gestión-centralizada)

---

## Concepto de log

Introducción

Un **log** o **registro** es un archivo o conjunto de datos donde el sistema operativo, las aplicaciones y los servicios almacenan información sobre los eventos que ocurren durante su funcionamiento. Estos registros permiten conocer qué acciones se han realizado, cuándo han ocurrido y cuál ha sido su resultado, convirtiéndose en una herramienta esencial para la administración, el mantenimiento y la seguridad de los sistemas.

La consulta de los logs es una de las primeras tareas que realiza un administrador cuando necesita diagnosticar una incidencia o investigar un problema.

---

### ¿Qué es un log?

Un log es un registro cronológico de eventos generados automáticamente por un sistema o una aplicación.

Cada vez que ocurre una acción importante, el sistema genera una nueva entrada que queda almacenada para su posterior consulta.

Algunos ejemplos de eventos registrados son:

- Inicio y apagado del sistema.
- Inicio de sesión de usuarios.
- Errores de aplicaciones.
- Fallos de servicios.
- Conexiones de red.
- Instalación de software.
- Actualizaciones del sistema.

Gracias a esta información es posible reconstruir lo ocurrido en un equipo o servidor.

---

### ¿Para qué sirven los logs?

Los logs tienen múltiples aplicaciones en la administración de sistemas.

Entre las más importantes destacan:

- Diagnosticar errores.
- Resolver incidencias.
- Supervisar el funcionamiento del sistema.
- Detectar problemas de seguridad.
- Auditar la actividad de usuarios y aplicaciones.
- Analizar el rendimiento.
- Cumplir requisitos legales y normativos.

Por ello, constituyen una fuente de información imprescindible para administradores y equipos de ciberseguridad.

---

### Funcionamiento básico

El funcionamiento de un sistema de registros puede representarse de la siguiente forma:

```text
Ocurre un evento

↓

El sistema genera un registro

↓

El registro se almacena

↓

El administrador consulta el log

↓

Se analiza la información
```

Este proceso se realiza automáticamente y de forma continua.

---

### Información que contiene un log

Aunque el contenido puede variar según el sistema o la aplicación, normalmente cada registro incluye información como:

- Fecha y hora del evento.
- Equipo o dispositivo donde ocurrió.
- Usuario implicado.
- Aplicación o servicio afectado.
- Tipo de evento.
- Nivel de gravedad.
- Descripción del suceso.

Estos datos permiten comprender qué ha ocurrido y cuándo.

---

### Características de los logs

Los registros del sistema presentan varias características comunes.

Generalmente son:

- Generados automáticamente.
- Ordenados cronológicamente.
- Acumulativos.
- Consultables posteriormente.
- Utilizados para auditoría y diagnóstico.

En muchos casos también pueden exportarse para su análisis o almacenamiento.

---

### Ejemplos de eventos registrados

Algunos eventos que suelen aparecer en los logs son:

- Inicio correcto del sistema.
- Error durante el arranque de un servicio.
- Inicio de sesión de un usuario.
- Intento fallido de autenticación.
- Instalación de una actualización.
- Error de una aplicación.
- Reinicio inesperado del equipo.

Cada uno de estos eventos queda registrado con la información necesaria para facilitar su análisis.

---

### Logs en Windows y Linux

Todos los sistemas operativos modernos generan registros automáticamente.

En **Windows**, los eventos se almacenan principalmente mediante el **Visor de eventos (Event Viewer)**.

En **Linux**, los registros suelen almacenarse en el directorio:

```text
/var/log
```

En distribuciones con **systemd**, también pueden consultarse mediante:

```bash
journalctl
```

---

### Importancia para la administración

La consulta de logs es una de las tareas más habituales en la administración de sistemas.

Permite:

- Detectar rápidamente incidencias.
- Conocer la causa de un problema.
- Verificar el funcionamiento de servicios.
- Analizar el comportamiento del sistema.
- Investigar incidentes de seguridad.

Sin registros, sería mucho más difícil localizar el origen de un fallo.

---

[⬆️ Volver al índice](#índice)

## Importancia de los logs

### Diagnóstico de incidencias

Una de las funciones principales de los logs es facilitar la resolución de problemas.

Cuando se produce un fallo, los registros permiten conocer:

- Qué ocurrió.
- Cuándo ocurrió.
- Dónde ocurrió.
- Qué componente estuvo implicado.
- Qué error se produjo.

Esta información acelera considerablemente el proceso de diagnóstico.

---

### Supervisión del sistema

Los registros permiten comprobar el funcionamiento de:

- Servicios.
- Aplicaciones.
- Hardware.
- Sistema operativo.
- Procesos programados.

Gracias a esta supervisión es posible detectar comportamientos anómalos antes de que se conviertan en una incidencia grave.

---

### Investigación de incidentes de seguridad

Los logs desempeñan un papel fundamental en la ciberseguridad.

Permiten identificar eventos como:

- Intentos fallidos de inicio de sesión.
- Accesos no autorizados.
- Cambios en la configuración del sistema.
- Instalación de software.
- Elevaciones de privilegios.
- Conexiones sospechosas.

Estos registros son esenciales para detectar y analizar posibles ataques.

---

### Auditoría y cumplimiento normativo

Muchas organizaciones deben conservar registros para cumplir normativas y políticas de seguridad.

Los logs permiten demostrar:

- Qué usuarios accedieron al sistema.
- Qué operaciones realizaron.
- Cuándo se produjeron los cambios.
- Qué incidencias ocurrieron.

Esta información resulta fundamental durante auditorías internas o externas.

---

### Análisis del rendimiento

Los registros también ayudan a detectar problemas relacionados con el rendimiento.

Por ejemplo:

- Servicios que tardan demasiado en iniciarse.
- Aplicaciones que generan errores repetitivos.
- Consumo excesivo de recursos.
- Procesos que finalizan inesperadamente.

Analizar estos eventos permite optimizar el funcionamiento del sistema.

---

### Resolución más rápida de problemas

Cuando una incidencia se acompaña de registros detallados, el administrador puede localizar su origen con mayor rapidez.

Sin logs:

```text
Problema

↓

Buscar posibles causas

↓

Realizar pruebas
```

Con logs:

```text
Problema

↓

Consultar registros

↓

Identificar el error

↓

Aplicar solución
```

El tiempo necesario para resolver la incidencia se reduce considerablemente.

---

### Toma de decisiones

El análisis de los registros proporciona información útil para mejorar la infraestructura.

Permite decidir, por ejemplo:

- Qué servicios requieren mantenimiento.
- Qué aplicaciones generan más errores.
- Qué equipos presentan incidencias frecuentes.
- Qué procesos conviene automatizar.

Los logs se convierten así en una herramienta de apoyo para la toma de decisiones técnicas.

---

### Evidencia de eventos

Los registros actúan como una evidencia de lo ocurrido en el sistema.

Pueden utilizarse para:

- Investigar incidencias.
- Analizar ataques informáticos.
- Reconstruir una secuencia de eventos.
- Justificar actuaciones realizadas por los administradores.

Por ello, en muchos casos tienen un importante valor probatorio.

---

### Consecuencias de no revisar los logs

No supervisar los registros puede provocar:

- Errores que permanecen sin detectar.
- Incidencias repetitivas.
- Pérdida de información importante.
- Dificultad para investigar problemas.
- Mayor riesgo de seguridad.

Por este motivo, la revisión periódica de los logs forma parte de las tareas habituales de administración.

---

[⬆️ Volver al índice](#índice)

## Tipos de logs

Introducción

Los sistemas operativos, aplicaciones y dispositivos generan diferentes tipos de registros según el tipo de evento que desean almacenar. Clasificar los logs permite localizar con mayor rapidez la información necesaria para diagnosticar incidencias, realizar auditorías o investigar problemas de seguridad.

Aunque cada sistema puede utilizar una organización distinta, la mayoría de los registros pueden agruparse en varias categorías principales.

---

### Logs del sistema

Recogen eventos relacionados con el funcionamiento del sistema operativo.

Entre la información que suelen almacenar se encuentra:

- Inicio y apagado del sistema.
- Carga de controladores.
- Errores del sistema operativo.
- Problemas de hardware.
- Cambios en la configuración.

Estos registros son fundamentales para diagnosticar problemas relacionados con el propio sistema.

---

### Logs de aplicaciones

Almacenan los eventos generados por las aplicaciones instaladas.

Por ejemplo:

- Inicio y cierre de aplicaciones.
- Errores internos.
- Fallos durante la ejecución.
- Actualizaciones.
- Mensajes de advertencia.

Cada aplicación puede generar sus propios registros con información específica.

---

### Logs de seguridad

Registran eventos relacionados con la seguridad del sistema.

Entre ellos destacan:

- Inicio y cierre de sesión.
- Intentos fallidos de autenticación.
- Cambios de contraseñas.
- Modificación de permisos.
- Elevación de privilegios.
- Accesos a recursos protegidos.

Estos registros son esenciales para detectar actividades sospechosas e investigar incidentes de seguridad.

---

### Logs de servicios

Los servicios del sistema también generan sus propios registros.

Pueden contener información sobre:

- Inicio del servicio.
- Detención del servicio.
- Reinicios.
- Errores de funcionamiento.
- Problemas de configuración.

Son especialmente útiles para diagnosticar incidencias relacionadas con servidores y aplicaciones.

---

### Logs de red

Registran información sobre las comunicaciones realizadas por el equipo.

Entre los eventos registrados pueden encontrarse:

- Conexiones establecidas.
- Errores de red.
- Cambios de configuración.
- Actividad de interfaces.
- Conexiones VPN.
- Resolución DNS.

Estos registros ayudan a analizar problemas de conectividad y comunicaciones.

---

### Logs de auditoría

Los registros de auditoría permiten realizar un seguimiento de las acciones efectuadas por usuarios y administradores.

Normalmente almacenan:

- Accesos al sistema.
- Modificación de archivos.
- Cambios en la configuración.
- Instalación o eliminación de software.
- Acciones administrativas.

Son muy utilizados para cumplir políticas de seguridad y requisitos legales.

---

### Logs de hardware

Algunos componentes físicos generan registros relacionados con su funcionamiento.

Por ejemplo:

- Discos duros.
- Memoria.
- Procesadores.
- Tarjetas de red.
- Controladoras RAID.
- Sensores de temperatura.

Estos registros permiten detectar posibles fallos físicos antes de que provoquen averías mayores.

---

### Logs en Windows

Windows organiza sus registros principalmente en varias categorías dentro del **Visor de eventos**.

Las más importantes son:

- Aplicación.
- Seguridad.
- Sistema.
- Instalación.
- Eventos reenviados.

Cada categoría almacena información relacionada con un tipo concreto de evento.

---

### Logs en Linux

En Linux los registros suelen almacenarse en el directorio:

```text
/var/log
```

Algunos archivos habituales son:

```text
/var/log/syslog
```

```text
/var/log/auth.log
```

```text
/var/log/kern.log
```

```text
/var/log/dmesg
```

Además, en sistemas con **systemd**, muchos registros pueden consultarse mediante:

```bash
journalctl
```

---

### Clasificación por nivel de gravedad

Muchos sistemas clasifican los registros según su importancia.

Los niveles más habituales son:

- Información (*Information*).
- Advertencia (*Warning*).
- Error (*Error*).
- Crítico (*Critical*).

Esta clasificación ayuda a identificar rápidamente los eventos que requieren atención inmediata.

---

[⬆️ Volver al índice](#índice)

## Formato y estructura de un log

Introducción

Aunque los registros pueden variar según el sistema operativo, la aplicación o el dispositivo que los genera, la mayoría siguen una estructura similar. Cada entrada de un log contiene información organizada que permite identificar qué ocurrió, cuándo ocurrió, quién estuvo implicado y cuál fue el resultado del evento.

Comprender el formato de los logs es fundamental para interpretar correctamente la información registrada y localizar rápidamente la causa de una incidencia.

---

### ¿Qué es una entrada de log?

Un **log** está formado por una colección de **entradas** o **registros**.

Cada entrada representa un único evento ocurrido en el sistema.

Su estructura general puede representarse así:

```text
Fecha y hora

↓

Origen del evento

↓

Nivel de gravedad

↓

Descripción

↓

Información adicional
```

Cada nueva acción registrada genera una nueva entrada.

---

### Información habitual

Aunque el contenido depende del sistema, la mayoría de los registros incluyen los siguientes datos:

- Fecha y hora.
- Equipo o dispositivo.
- Usuario.
- Aplicación o servicio.
- Identificador del evento.
- Nivel de gravedad.
- Descripción del evento.

Esta información permite reconstruir lo ocurrido con gran precisión.

---

### Fecha y hora

La fecha y la hora indican el momento exacto en que ocurrió el evento.

Ejemplo:

```text
31/07/2026 09:15:42
```

Este dato es fundamental para:

- Ordenar cronológicamente los eventos.
- Relacionar distintos registros.
- Investigar incidencias.

---

### Origen del evento

El origen identifica el componente que ha generado el registro.

Puede tratarse de:

- Sistema operativo.
- Servicio.
- Aplicación.
- Controlador.
- Hardware.
- Proceso.

Conocer el origen ayuda a localizar rápidamente el componente afectado.

---

### Nivel de gravedad

Muchos sistemas clasifican los eventos según su importancia.

Los niveles más habituales son:

| Nivel | Descripción |
|--------|-------------|
| Información | Evento normal del sistema. |
| Advertencia | Situación que puede requerir atención. |
| Error | Se ha producido un fallo. |
| Crítico | Error grave que afecta al funcionamiento del sistema. |

Esta clasificación permite priorizar el análisis de los registros.

---

### Identificador del evento

Algunos sistemas asignan un identificador único a cada tipo de evento.

Por ejemplo, en Windows:

```text
Event ID: 4625
```

Este identificador facilita la búsqueda de información técnica y documentación relacionada con el problema.

---

### Descripción

La descripción explica lo ocurrido durante el evento.

Por ejemplo:

```text
El servicio Spooler se detuvo inesperadamente.
```

O bien:

```text
Error al iniciar sesión del usuario.
```

Es el campo que suele aportar más información para el diagnóstico.

---

### Ejemplo de una entrada de log

Una entrada simplificada podría ser:

```text
Fecha: 31/07/2026 09:15:42

Origen: Servicio de impresión

Nivel: Error

ID: 7031

Descripción: El servicio terminó de forma inesperada.
```

Esta información permite identificar rápidamente el problema.

---

### Formatos de almacenamiento

Los registros pueden almacenarse en distintos formatos.

Los más habituales son:

- Texto plano (`.log`).
- XML.
- Binario.
- JSON.
- Bases de datos.

El formato utilizado depende del sistema operativo o de la aplicación que genera el registro.

---

### Formato en Windows y Linux

**Windows**

Los registros del Visor de eventos utilizan un formato estructurado que almacena información como:

- Fecha.
- Origen.
- Nivel.
- ID del evento.
- Usuario.
- Descripción.

**Linux**

En Linux muchos registros son archivos de texto ubicados en:

```text
/var/log
```

Cada línea suele contener:

- Fecha.
- Hora.
- Equipo.
- Servicio.
- Mensaje.

Esto facilita su lectura mediante herramientas como `cat`, `less`, `grep` o `journalctl`.

---

[⬆️ Volver al índice](#índice)

## Visor de eventos en Windows

Introducción

El **Visor de eventos** (*Event Viewer*) es la herramienta integrada en Windows que permite consultar y administrar los registros generados por el sistema operativo, las aplicaciones y los servicios. Gracias a ella es posible analizar errores, advertencias, eventos de seguridad y otros sucesos importantes que ayudan a diagnosticar incidencias y supervisar el funcionamiento del sistema.

Se trata de una de las herramientas más utilizadas por los administradores de sistemas para investigar problemas y realizar auditorías.

---

### ¿Qué es el Visor de eventos?

El Visor de eventos es una consola de administración que muestra todos los registros generados por Windows.

Permite:

- Consultar eventos.
- Filtrar registros.
- Buscar incidencias.
- Exportar logs.
- Analizar errores.
- Supervisar el funcionamiento del sistema.

Toda la información se organiza en diferentes categorías para facilitar su consulta.

---

### Abrir el Visor de eventos

Existen varias formas de acceder a esta herramienta.

Desde **Ejecutar**:

```text
eventvwr.msc
```

También puede abrirse desde:

```text
Panel de control

↓

Herramientas de Windows

↓

Visor de eventos
```

O buscándolo directamente desde el menú Inicio.

---

### Interfaz principal

La consola se divide en tres zonas principales.

- **Panel izquierdo:** árbol con los diferentes registros.
- **Panel central:** lista de eventos.
- **Panel derecho:** acciones disponibles.

Desde esta interfaz es posible navegar entre los distintos registros del sistema.

---

### Registros de Windows

Los registros principales se encuentran dentro del apartado **Registros de Windows**.

Las categorías más importantes son:

- Aplicación.
- Seguridad.
- Instalación.
- Sistema.
- Eventos reenviados.

Cada una almacena información relacionada con un tipo concreto de evento.

---

### Registro de Aplicación

Contiene eventos generados por las aplicaciones instaladas.

Por ejemplo:

- Errores de programas.
- Fallos de aplicaciones.
- Advertencias.
- Información de funcionamiento.

Es uno de los primeros registros que debe revisarse cuando una aplicación presenta problemas.

---

### Registro de Sistema

Almacena eventos relacionados con el propio sistema operativo.

Entre ellos:

- Inicio del sistema.
- Servicios.
- Controladores.
- Hardware.
- Reinicios inesperados.

Resulta fundamental para diagnosticar problemas generales del sistema.

---

### Registro de Seguridad

Contiene eventos relacionados con la seguridad.

Algunos ejemplos son:

- Inicio de sesión.
- Cierre de sesión.
- Intentos fallidos de autenticación.
- Cambios de permisos.
- Auditorías de seguridad.

Este registro es especialmente importante para investigar incidentes de ciberseguridad.

---

### Información de un evento

Cada evento incluye información detallada.

Normalmente aparece:

- Fecha y hora.
- Nivel.
- Origen.
- Identificador del evento (Event ID).
- Usuario.
- Equipo.
- Descripción.

Estos datos permiten analizar con precisión cada incidencia.

---

### Filtrar eventos

Cuando existen miles de registros resulta útil aplicar filtros.

Es posible filtrar por:

- Nivel.
- Fecha.
- Identificador del evento.
- Origen.
- Usuario.

Esto facilita localizar rápidamente la información necesaria.

---

### Exportar registros

Los eventos pueden guardarse para su análisis o conservación.

El Visor de eventos permite exportarlos en diferentes formatos.

Esta opción resulta útil para:

- Auditorías.
- Soporte técnico.
- Investigación de incidencias.
- Conservación de evidencias.

---

### Ejemplos de uso

El Visor de eventos suele utilizarse para:

- Investigar reinicios inesperados.
- Detectar errores de aplicaciones.
- Analizar problemas de hardware.
- Revisar intentos de acceso fallidos.
- Comprobar el funcionamiento de servicios.

Es una herramienta imprescindible para el diagnóstico de incidencias en Windows.

---

[⬆️ Volver al índice](#índice)

## Administración mediante PowerShell

Introducción

PowerShell permite consultar y administrar los registros de eventos de Windows desde la línea de comandos mediante diferentes cmdlets especializados. Esta forma de administración resulta especialmente útil para automatizar consultas, generar informes, filtrar grandes cantidades de información o administrar múltiples equipos de forma remota.

Gracias a PowerShell es posible acceder a los registros del sistema de una forma más rápida y flexible que utilizando únicamente el Visor de eventos.

---

### Obtener los registros disponibles

Para mostrar todos los registros de eventos existentes en el sistema:

```powershell
Get-WinEvent -ListLog *
```

La salida incluye información como:

- Nombre del registro.
- Número de eventos.
- Tamaño máximo.
- Estado.

Este comando permite conocer qué registros están disponibles.

---

### Consultar eventos de un registro

Para mostrar los eventos de un registro concreto:

```powershell
Get-WinEvent -LogName System
```

También pueden consultarse otros registros, por ejemplo:

```powershell
Get-WinEvent -LogName Application
```

```powershell
Get-WinEvent -LogName Security
```

---

### Mostrar los eventos más recientes

Para visualizar únicamente los últimos eventos registrados:

```powershell
Get-WinEvent -LogName System -MaxEvents 10
```

Este comando muestra los diez eventos más recientes del registro indicado.

---

### Filtrar eventos por nivel

Es posible mostrar únicamente los eventos que correspondan a un determinado nivel de gravedad.

Por ejemplo, para obtener únicamente errores:

```powershell
Get-WinEvent -LogName System |
Where-Object LevelDisplayName -eq "Error"
```

Este tipo de filtrado facilita localizar incidencias importantes.

---

### Buscar eventos por identificador

Cuando se conoce el **Event ID**, la búsqueda resulta mucho más sencilla.

Ejemplo:

```powershell
Get-WinEvent -FilterHashtable @{
LogName="System";
Id=7036
}
```

Este comando devuelve únicamente los eventos cuyo identificador sea **7036**.

---

### Consultar eventos recientes

También es posible obtener los eventos generados durante un periodo determinado.

Ejemplo:

```powershell
Get-WinEvent -FilterHashtable @{
LogName="System";
StartTime=(Get-Date).AddDays(-1)
}
```

En este caso se muestran únicamente los eventos registrados durante el último día.

---

### Exportar registros

Los eventos obtenidos pueden exportarse para su posterior análisis.

Por ejemplo:

```powershell
Get-WinEvent -LogName System |
Export-Csv C:\Informes\logs.csv -NoTypeInformation
```

Esto genera un archivo CSV que puede abrirse con Excel u otras herramientas de análisis.

---

### Utilizar filtros avanzados

PowerShell permite combinar distintos criterios de búsqueda.

Por ejemplo:

- Registro.
- Fecha.
- Identificador.
- Nivel.
- Proveedor.
- Usuario.

Esta capacidad convierte a PowerShell en una herramienta muy potente para investigar incidencias complejas.

---

### Automatización mediante scripts

Una de las principales ventajas de PowerShell consiste en automatizar consultas repetitivas.

Por ejemplo, generar un informe diario con los errores críticos:

```powershell
Get-WinEvent -LogName System |
Where-Object LevelDisplayName -eq "Critical"
```

Este tipo de consultas puede integrarse fácilmente en tareas programadas o scripts de administración.

---

### Ventajas de PowerShell

Entre sus principales ventajas destacan:

- Consultas rápidas.
- Filtrado avanzado.
- Automatización.
- Exportación de resultados.
- Administración remota.
- Integración con scripts.

Estas características hacen que PowerShell sea una herramienta imprescindible para administradores de sistemas Windows.

---

[⬆️ Volver al índice](#índice)

## Logs en Linux

Introducción

Linux registra de forma continua los eventos generados por el sistema operativo, los servicios y las aplicaciones. Estos registros se almacenan principalmente como archivos de texto, lo que facilita su consulta mediante herramientas de línea de comandos. Analizar estos logs es una tarea habitual para diagnosticar incidencias, supervisar el funcionamiento del sistema e investigar problemas de seguridad.

Aunque muchas distribuciones modernas utilizan **systemd Journal**, los archivos de log tradicionales continúan siendo ampliamente utilizados.

---

### ¿Dónde se almacenan los logs?

La mayoría de los registros del sistema se almacenan en el directorio:

```text
/var/log
```

En esta ubicación se encuentran los archivos generados por el sistema operativo, los servicios y numerosas aplicaciones.

Puede consultarse su contenido mediante:

```bash
ls /var/log
```

---

### Archivos de log más habituales

Algunos de los registros más importantes son:

| Archivo | Contenido |
|----------|-----------|
| `/var/log/syslog` | Eventos generales del sistema. |
| `/var/log/auth.log` | Autenticación e inicios de sesión. |
| `/var/log/kern.log` | Eventos del núcleo (kernel). |
| `/var/log/dmesg` | Mensajes del arranque y hardware. |
| `/var/log/boot.log` | Información del proceso de arranque. |

Dependiendo de la distribución, algunos nombres pueden variar.

---

### Consultar un log

Los archivos de registro pueden visualizarse mediante diferentes comandos.

Mostrar el contenido completo:

```bash
cat /var/log/syslog
```

Visualizar página a página:

```bash
less /var/log/syslog
```

Mostrar únicamente las últimas líneas:

```bash
tail /var/log/syslog
```

Estos comandos facilitan la consulta de archivos de gran tamaño.

---

### Buscar información en un log

Cuando un registro contiene miles de líneas, resulta útil buscar únicamente la información necesaria.

Ejemplo:

```bash
grep "error" /var/log/syslog
```

También pueden realizarse búsquedas ignorando mayúsculas y minúsculas:

```bash
grep -i "failed" /var/log/auth.log
```

Esto permite localizar rápidamente eventos concretos.

---

### Supervisar un log en tiempo real

Es posible visualizar cómo un archivo de log se actualiza mientras el sistema continúa funcionando.

Para ello se utiliza:

```bash
tail -f /var/log/syslog
```

Cada nuevo evento aparecerá automáticamente en pantalla.

Esta técnica resulta muy útil durante tareas de diagnóstico.

---

### Logs de autenticación

Uno de los registros más importantes es:

```text
/var/log/auth.log
```

Contiene información relacionada con:

- Inicios de sesión.
- Cambios de usuario.
- Uso de sudo.
- Intentos fallidos de autenticación.
- Accesos mediante SSH.

Es un archivo esencial para el análisis de incidentes de seguridad.

---

### Logs del kernel

El archivo:

```text
/var/log/kern.log
```

Registra eventos relacionados con el núcleo del sistema.

Entre ellos:

- Errores de hardware.
- Problemas con controladores.
- Mensajes del kernel.
- Detección de dispositivos.

Estos registros ayudan a diagnosticar incidencias relacionadas con el hardware y el sistema operativo.

---

### Logs de aplicaciones

Muchas aplicaciones crean sus propios registros dentro de:

```text
/var/log
```

O en subdirectorios específicos.

Por ejemplo:

```text
/var/log/apache2/
```

```text
/var/log/nginx/
```

```text
/var/log/mysql/
```

Cada aplicación almacena información adaptada a su funcionamiento.

---

### Herramientas habituales

Los administradores utilizan con frecuencia herramientas como:

- `cat`
- `less`
- `more`
- `head`
- `tail`
- `grep`

Estas utilidades permiten consultar y analizar rápidamente grandes cantidades de información.

---

[⬆️ Volver al índice](#índice)

## Journalctl y systemd Journal

Introducción

Las distribuciones Linux modernas que utilizan **systemd** incorporan un sistema de registros denominado **systemd Journal**. A diferencia de los archivos de log tradicionales almacenados en `/var/log`, este sistema centraliza los eventos generados por el núcleo, los servicios y las aplicaciones, facilitando su consulta mediante la herramienta **journalctl**.

Gracias a esta utilidad, los administradores pueden realizar búsquedas avanzadas, filtrar información y analizar registros de forma rápida y eficiente.

---

### ¿Qué es systemd Journal?

**systemd Journal** es el sistema de registro integrado en **systemd**.

Su función consiste en recopilar eventos procedentes de:

- Sistema operativo.
- Kernel.
- Servicios.
- Aplicaciones.
- Procesos.
- Usuarios.

Toda esta información queda almacenada en una base de datos de registros administrada por systemd.

---

### ¿Qué es journalctl?

`journalctl` es la herramienta utilizada para consultar los registros almacenados en **systemd Journal**.

Su sintaxis básica es:

```bash
journalctl
```

Este comando muestra todos los eventos registrados por el sistema.

---

### Mostrar los registros más recientes

Para visualizar únicamente las últimas entradas:

```bash
journalctl -n 20
```

En este ejemplo se muestran los veinte eventos más recientes.

---

### Consultar los registros en tiempo real

Al igual que con `tail -f`, es posible supervisar los registros conforme se generan.

Para ello se utiliza:

```bash
journalctl -f
```

Cada nuevo evento aparecerá automáticamente en pantalla.

Esta opción resulta muy útil durante tareas de diagnóstico.

---

### Consultar los registros del arranque actual

Para mostrar únicamente los eventos registrados desde el último inicio del sistema:

```bash
journalctl -b
```

Esta consulta facilita el análisis de problemas ocurridos durante el arranque.

---

### Consultar un servicio concreto

Es posible mostrar únicamente los registros asociados a un servicio.

Ejemplo:

```bash
journalctl -u ssh
```

También pueden consultarse otros servicios:

```bash
journalctl -u apache2
```

```bash
journalctl -u nginx
```

De esta forma se reduce considerablemente la cantidad de información mostrada.

---

### Filtrar por fecha

Los registros también pueden consultarse indicando un periodo concreto.

Por ejemplo:

```bash
journalctl --since "today"
```

Mostrar únicamente los eventos de la última hora:

```bash
journalctl --since "1 hour ago"
```

También es posible indicar una fecha específica.

---

### Filtrar por prioridad

Los eventos pueden clasificarse según su nivel de gravedad.

Por ejemplo, mostrar únicamente errores:

```bash
journalctl -p err
```

O únicamente eventos críticos:

```bash
journalctl -p crit
```

Esto facilita localizar rápidamente las incidencias más importantes.

---

### Consultar registros del kernel

Para visualizar únicamente los mensajes del núcleo:

```bash
journalctl -k
```

Estos registros contienen información relacionada con:

- Hardware.
- Controladores.
- Arranque.
- Dispositivos.

Son especialmente útiles para diagnosticar problemas del sistema.

---

### Ventajas de systemd Journal

Entre sus principales ventajas destacan:

- Centralización de registros.
- Consultas rápidas mediante filtros.
- Integración con systemd.
- Supervisión de servicios.
- Búsquedas por fecha y prioridad.
- Visualización en tiempo real.

Estas características convierten a `journalctl` en una herramienta muy potente para la administración de sistemas Linux.

---

[⬆️ Volver al índice](#índice)

## Rotación y conservación de logs

Introducción

Los registros del sistema se generan continuamente y, con el paso del tiempo, pueden ocupar una gran cantidad de espacio en disco. Para evitar que los archivos crezcan de forma indefinida y garantizar la disponibilidad de almacenamiento, los sistemas operativos utilizan mecanismos de **rotación** y **conservación de logs**.

Una gestión adecuada permite mantener únicamente los registros necesarios, mejorar el rendimiento del sistema y facilitar las tareas de administración y auditoría.

---

### ¿Qué es la rotación de logs?

La **rotación de logs** consiste en reemplazar un archivo de registro activo por uno nuevo cuando se cumple una determinada condición.

Las condiciones más habituales son:

- Alcanzar un tamaño máximo.
- Transcurrir un periodo de tiempo.
- Finalizar un ciclo de ejecución.

El archivo antiguo se conserva durante un tiempo determinado antes de ser eliminado.

---

### Funcionamiento de la rotación

El proceso de rotación puede representarse de la siguiente forma:

```text
Log activo

↓

Alcanza el límite configurado

↓

Se renombra

↓

Se crea un nuevo log

↓

El log antiguo se conserva
```

Este procedimiento evita que un único archivo alcance un tamaño excesivo.

---

### Conservación de logs

La conservación consiste en mantener los registros durante un periodo determinado.

El tiempo de conservación depende de factores como:

- Políticas internas.
- Requisitos legales.
- Auditorías.
- Necesidades operativas.

Una vez superado el periodo establecido, los registros pueden eliminarse automáticamente.

---

### Rotación en Linux: logrotate

En la mayoría de distribuciones Linux, la rotación de logs se realiza mediante la herramienta **logrotate**.

Su configuración principal se encuentra en:

```text
/etc/logrotate.conf
```

Además, muchas aplicaciones disponen de configuraciones específicas en:

```text
/etc/logrotate.d/
```

---

### Opciones habituales de logrotate

Algunas directivas frecuentes son:

```text
daily
```

Realiza la rotación diariamente.

```text
weekly
```

Realiza la rotación semanalmente.

```text
monthly
```

Realiza la rotación mensualmente.

```text
rotate 7
```

Conserva los siete archivos más recientes.

```text
compress
```

Comprime automáticamente los registros antiguos para reducir el espacio ocupado.

---

### Rotación en Windows

Windows también dispone de mecanismos para controlar el tamaño de los registros.

Desde el **Visor de eventos** es posible configurar:

- Tamaño máximo del registro.
- Sobrescribir eventos antiguos.
- Archivar el registro cuando esté lleno.
- Impedir la sobrescritura.

Estas opciones permiten adaptar la conservación de los eventos a las necesidades de la organización.

---

### Compresión de logs

Los registros antiguos suelen comprimirse automáticamente para ahorrar espacio.

En Linux es habitual encontrar archivos como:

```text
syslog.1
```

```text
syslog.2.gz
```

```text
auth.log.1.gz
```

Los archivos comprimidos conservan la información y pueden consultarse cuando sea necesario.

---

### Importancia de conservar los registros

Mantener los logs durante un periodo adecuado permite:

- Investigar incidencias antiguas.
- Realizar auditorías.
- Analizar tendencias.
- Cumplir requisitos legales.
- Obtener evidencias de seguridad.

Eliminar los registros demasiado pronto puede dificultar el análisis de problemas.

---

### Riesgos de una mala gestión

Una gestión incorrecta de los logs puede provocar:

- Falta de espacio en disco.
- Pérdida de información importante.
- Incumplimiento de normativas.
- Dificultad para investigar incidentes.
- Reducción del rendimiento del sistema.

Por ello es importante definir políticas de conservación adecuadas.

---

[⬆️ Volver al índice](#índice)

## Monitorización y análisis de logs

Introducción

La generación de registros no resulta útil si estos no son supervisados y analizados de forma periódica. La monitorización de logs permite detectar errores, identificar comportamientos anómalos y responder rápidamente ante incidencias o posibles amenazas de seguridad. Un análisis adecuado facilita el mantenimiento preventivo y mejora la disponibilidad de los sistemas.

En entornos empresariales, donde se generan miles o incluso millones de eventos diarios, la monitorización automatizada resulta imprescindible.

---

### ¿Qué es la monitorización de logs?

La monitorización consiste en supervisar continuamente los registros generados por el sistema para detectar eventos relevantes.

Su objetivo es identificar:

- Errores.
- Advertencias.
- Fallos de servicios.
- Problemas de rendimiento.
- Incidentes de seguridad.
- Comportamientos anómalos.

Esta supervisión puede realizarse de forma manual o automática.

---

### Objetivos del análisis de logs

El análisis de registros permite:

- Diagnosticar incidencias.
- Detectar errores repetitivos.
- Identificar intentos de acceso no autorizados.
- Supervisar servicios críticos.
- Analizar el rendimiento del sistema.
- Investigar incidentes de seguridad.

Toda esta información facilita la toma de decisiones por parte del administrador.

---

### Análisis manual

El análisis manual consiste en revisar directamente los registros.

Puede realizarse mediante herramientas como:

**Windows**

- Visor de eventos.
- PowerShell.

**Linux**

- `journalctl`
- `grep`
- `less`
- `tail`

Este método es adecuado cuando se investigan incidencias concretas.

---

### Monitorización automática

En sistemas con un gran volumen de eventos resulta recomendable automatizar la supervisión.

Un sistema automático puede:

- Analizar continuamente los registros.
- Detectar errores críticos.
- Generar alertas.
- Enviar notificaciones.
- Crear informes.

De esta forma, el administrador puede actuar antes de que el problema afecte al servicio.

---

### Indicadores importantes

Durante el análisis conviene prestar especial atención a:

- Errores críticos.
- Reinicios inesperados.
- Servicios detenidos.
- Intentos fallidos de autenticación.
- Incremento anormal de eventos.
- Errores repetitivos.

Estos indicadores suelen reflejar incidencias que requieren una intervención rápida.

---

### Búsqueda de patrones

El análisis de logs no se limita a revisar eventos aislados.

También permite identificar patrones como:

- Errores que se repiten diariamente.
- Reinicios siempre a la misma hora.
- Incremento progresivo de advertencias.
- Intentos continuos de acceso desde una misma dirección IP.

Detectar estos patrones ayuda a localizar problemas persistentes.

---

### Generación de alertas

Muchos sistemas de monitorización permiten configurar alertas automáticas.

Por ejemplo, cuando ocurre:

- Un error crítico.
- La caída de un servicio.
- Un intento de acceso no autorizado.
- Un consumo anómalo de recursos.

Las alertas pueden enviarse mediante:

- Correo electrónico.
- Mensajería.
- Consolas de monitorización.
- Sistemas de tickets.

---

### Elaboración de informes

Los registros también pueden utilizarse para generar informes periódicos.

Estos informes suelen incluir:

- Número de errores.
- Servicios con más incidencias.
- Eventos críticos.
- Actividad de usuarios.
- Tendencias de funcionamiento.

La información obtenida facilita el mantenimiento preventivo del sistema.

---

### Procedimiento de análisis

Un procedimiento habitual puede representarse así:

```text
Recopilar registros

↓

Filtrar información relevante

↓

Identificar eventos importantes

↓

Buscar patrones

↓

Analizar la causa

↓

Aplicar la solución

↓

Verificar el resultado
```

Este método permite realizar investigaciones de forma ordenada.

---

[⬆️ Volver al índice](#índice)

## Herramientas de gestión centralizada

Introducción

En infraestructuras con numerosos equipos y servidores, consultar los registros de cada sistema de forma individual resulta poco práctico. Para solucionar este problema existen herramientas de **gestión centralizada de logs**, que recopilan los registros de múltiples dispositivos en un único lugar, facilitando su almacenamiento, búsqueda y análisis.

Estas soluciones son ampliamente utilizadas en empresas y centros de datos, ya que permiten supervisar toda la infraestructura desde una única plataforma.

---

### ¿Qué es una gestión centralizada de logs?

La gestión centralizada consiste en recopilar los registros generados por diferentes equipos, servidores, dispositivos de red y aplicaciones en un servidor o plataforma común.

Su funcionamiento puede representarse así:

```text
Equipos y servidores

↓

Envían registros

↓

Servidor central de logs

↓

Búsqueda y análisis
```

De esta forma, el administrador no necesita consultar cada equipo por separado.

---

### Ventajas de la centralización

Centralizar los registros ofrece numerosos beneficios.

Entre los principales destacan:

- Consulta desde un único punto.
- Mayor rapidez en el análisis.
- Correlación de eventos entre distintos equipos.
- Conservación centralizada de registros.
- Detección más rápida de incidencias.
- Facilita auditorías y tareas de seguridad.

Estas ventajas hacen que sea una práctica habitual en entornos empresariales.

---

### Syslog

Uno de los protocolos más utilizados para enviar registros en sistemas Linux y dispositivos de red es **Syslog**.

Permite que diferentes equipos envíen automáticamente sus eventos a un servidor central.

Es compatible con:

- Linux.
- Routers.
- Switches.
- Firewalls.
- Impresoras de red.
- Dispositivos IoT.

Gracias a su amplia compatibilidad, es uno de los estándares más extendidos.

---

### SIEM

Un **SIEM** (*Security Information and Event Management*) es una plataforma especializada en recopilar, correlacionar y analizar registros procedentes de múltiples fuentes.

Además de almacenar los eventos, un SIEM puede:

- Detectar comportamientos anómalos.
- Generar alertas automáticas.
- Correlacionar eventos.
- Facilitar investigaciones de seguridad.
- Crear informes.

Estas herramientas son habituales en los centros de operaciones de seguridad (SOC).

---

### Elastic Stack (ELK)

Una de las soluciones más utilizadas para la gestión centralizada de logs es **Elastic Stack**, también conocido como **ELK**.

Está formado por:

- **Elasticsearch** → almacena e indexa los datos.
- **Logstash** → recopila y procesa los registros.
- **Kibana** → visualiza la información mediante paneles y gráficos.

Esta plataforma permite realizar búsquedas rápidas y generar cuadros de mando muy completos.

---

### Graylog

**Graylog** es otra plataforma muy utilizada para la centralización y análisis de registros.

Sus principales características son:

- Recopilación de logs.
- Búsquedas avanzadas.
- Paneles de control.
- Alertas.
- Gestión de grandes volúmenes de información.

Es una solución ampliamente utilizada en entornos empresariales.

---

### Splunk

**Splunk** es una plataforma comercial especializada en el análisis de grandes volúmenes de datos y registros.

Permite:

- Centralizar logs.
- Buscar información rápidamente.
- Crear informes.
- Detectar anomalías.
- Generar alertas.

Se utiliza con frecuencia en grandes organizaciones y equipos de ciberseguridad.

---

### Microsoft Sentinel

En entornos Microsoft es habitual utilizar **Microsoft Sentinel**, un SIEM basado en la nube.

Entre sus funciones destacan:

- Recopilación de eventos.
- Correlación automática.
- Detección de amenazas.
- Investigación de incidentes.
- Automatización de respuestas.

Se integra fácilmente con servicios como Microsoft 365 y Azure.

---

### Características deseables

Una herramienta de gestión centralizada debería ofrecer:

- Recopilación automática de registros.
- Búsquedas rápidas.
- Filtrado avanzado.
- Paneles de visualización.
- Generación de alertas.
- Conservación segura de los registros.
- Escalabilidad.

Estas características facilitan la administración de grandes infraestructuras.

---

[⬆️ Volver al índice](#índice)