# 06 - Servicios avanzados

## Introducción

Los servicios son procesos especiales que se ejecutan en segundo plano para proporcionar funciones esenciales al sistema operativo o a las aplicaciones.

Comprender el funcionamiento de los servicios es fundamental para mantener la disponibilidad de servidores, solucionar incidencias y administrar infraestructuras de forma eficiente.

---

## Índice

- [Arquitectura de un servicio](#arquitectura-de-un-servicio)
- [Dependencias entre servicios](#dependencias-entre-servicios)
- [Tipos de inicio y estados](#tipos-de-inicio-y-estados)
- [Servicios críticos del sistema](#servicios-críticos-del-sistema)
- [Recuperación automática de servicios](#recuperación-automática-de-servicios)
- [Monitorización y diagnóstico](#monitorización-y-diagnóstico)
- [Seguridad de los servicios](#seguridad-de-los-servicios)
- [Automatización](#automatización)
- [Buenas prácticas](#buenas-prácticas)

---

## Arquitectura de un servicio

Un **servicio** es un tipo especial de proceso diseñado para ejecutarse en segundo plano y proporcionar funciones al sistema operativo o a otras aplicaciones.

A diferencia de un programa convencional, un servicio no necesita la intervención directa del usuario y suele iniciarse automáticamente durante el arranque del sistema.

Los servicios son fundamentales para el funcionamiento de servidores y equipos de escritorio, ya que gestionan tareas como la red, la autenticación, el almacenamiento, la impresión o las bases de datos.

---

### ¿Qué es un servicio?

Un servicio es una aplicación que:

- Se ejecuta en segundo plano.
- No requiere interacción con el usuario.
- Puede iniciarse automáticamente.
- Permanece activa hasta que se detiene o finaliza.

Ejemplos:

- Servidor web.
- Servidor DNS.
- Servicio SSH.
- Servicio de impresión.
- Base de datos.
- Antivirus.
- Servicio de actualizaciones.

---

### Diferencia entre proceso y servicio

Aunque ambos son procesos en ejecución, tienen finalidades distintas.

| Proceso | Servicio |
|----------|-----------|
| Puede iniciarlo un usuario. | Normalmente lo inicia el sistema operativo. |
| Suele tener interfaz gráfica. | Normalmente no tiene interfaz. |
| Finaliza cuando termina su trabajo. | Permanece ejecutándose continuamente. |
| Depende del usuario. | Proporciona funciones al sistema o a otras aplicaciones. |

Todo servicio es un proceso, pero no todo proceso es un servicio.

---

### Ciclo de vida de un servicio

De forma simplificada, un servicio sigue este ciclo:

```text
Instalación

↓

Inicio

↓

Ejecución

↓

Detención

↓

Reinicio (opcional)

↓

Finalización
```

Durante este ciclo el sistema operativo controla su estado y disponibilidad.

---

### Componentes de un servicio

Un servicio suele estar formado por varios elementos.

Los principales son:

- Ejecutable del servicio.
- Configuración.
- Dependencias.
- Cuenta de ejecución.
- Registros.
- Estado.
- Tipo de inicio.

Cada uno cumple una función específica dentro del funcionamiento del servicio.

---

### Ejecutable

Es el programa que realiza el trabajo del servicio.

Ejemplos:

Linux:

```text
/usr/sbin/sshd
```

Windows:

```text
svchost.exe
```

o

```text
spoolsv.exe
```

---

### Configuración

Los servicios utilizan archivos o parámetros de configuración para definir su funcionamiento.

Linux:

Habitualmente se almacenan en:

```text
/etc
```

Ejemplos:

```text
/etc/ssh/sshd_config
```

```text
/etc/nginx/nginx.conf
```

Windows:

La configuración suele almacenarse en:

- Registro de Windows.
- Archivos XML.
- Archivos INI.
- Archivos JSON.
- Bases de datos internas de la aplicación.

---

### Cuenta de ejecución

Todo servicio necesita ejecutarse con una identidad determinada.

Linux:

Puede utilizar usuarios específicos como:

```text
root

www-data

mysql

postgres
```

Windows:

Algunas cuentas habituales son:

- Local System.
- Local Service.
- Network Service.
- Usuario de dominio.
- Usuario local.

La elección de la cuenta afecta directamente a los permisos disponibles.

---

### Estado

Los servicios pueden encontrarse en distintos estados.

Los más habituales son:

- Iniciado.
- Detenido.
- Iniciando.
- Deteniendo.
- En pausa.
- Reanudándose.

Estos estados permiten conocer su situación en cada momento.

---

### Tipo de inicio

El sistema operativo determina cuándo debe iniciarse un servicio.

Los modos más habituales son:

- Automático.
- Automático (inicio retrasado).
- Manual.
- Deshabilitado.

No todos los servicios necesitan iniciarse automáticamente.

---

### Dependencias

Muchos servicios necesitan que otros servicios estén disponibles antes de poder iniciarse.

Ejemplo:

```text
Servidor Web

↓

Red

↓

DNS

↓

Sistema de archivos
```

Las dependencias permiten garantizar un orden correcto durante el arranque.

---

### Registros

Los servicios suelen generar información de funcionamiento.

Estos registros permiten conocer:

- Inicio.
- Detención.
- Errores.
- Advertencias.
- Configuración.
- Incidencias.

Son una herramienta fundamental para el diagnóstico.

---

### Servicios en Linux

En la mayoría de distribuciones actuales los servicios son administrados por:

```text
systemd
```

Cada servicio se define mediante una **unidad (.service)**.

Ejemplo:

```text
sshd.service
```

---

### Servicios en Windows

Windows utiliza el **Service Control Manager (SCM)** para administrar todos los servicios del sistema.

El SCM se encarga de:

- Iniciar servicios.
- Detener servicios.
- Reiniciarlos.
- Gestionar dependencias.
- Supervisar estados.

Es el componente central de administración de servicios en Windows.

---

### Ejemplos de servicios habituales

| Servicio | Función |
|-----------|----------|
| SSH | Acceso remoto seguro |
| Apache / Nginx | Servidor web |
| MySQL / PostgreSQL | Base de datos |
| DNS | Resolución de nombres |
| DHCP | Asignación automática de IP |
| Print Spooler | Gestión de impresión |
| Windows Update | Actualizaciones del sistema |

---

### Comparativa Linux / Windows

| Linux | Windows |
|--------|----------|
| systemd | Service Control Manager |
| Unidades `.service` | Servicios registrados en el SCM |
| Archivos de configuración | Registro y archivos de configuración |
| Usuarios del sistema | Cuentas de servicio |
| `systemctl` | Consola Servicios / PowerShell |

---

### Buenas prácticas

- Ejecuta cada servicio con la cuenta que disponga únicamente de los permisos necesarios.
- Mantén los archivos de configuración organizados y documentados.
- Revisa periódicamente el estado de los servicios críticos.
- Comprueba las dependencias antes de modificar o deshabilitar un servicio.
- Consulta los registros cuando un servicio no funcione correctamente.
- Deshabilita los servicios que no sean necesarios para reducir la superficie de ataque y el consumo de recursos.

---

[⬆️ Volver al índice](#índice)

## Dependencias entre servicios

En la mayoría de los sistemas, los servicios no funcionan de forma aislada.

Es habitual que un servicio necesite que otros estén disponibles antes de poder iniciarse correctamente.

Estas relaciones reciben el nombre de **dependencias** y permiten que el sistema operativo inicie y detenga los servicios en el orden adecuado.

Comprender las dependencias resulta fundamental para diagnosticar errores de arranque y evitar interrupciones en servicios críticos.

---

### ¿Qué es una dependencia?

Una dependencia indica que un servicio necesita otro servicio para funcionar correctamente.

Ejemplo:

```text
Servidor Web

↓

Servicio de red

↓

Sistema de archivos

↓

Resolución DNS
```

Si alguno de estos servicios falla, el servidor web podría no iniciarse o funcionar de forma incorrecta.

---

### ¿Por qué son importantes?

Las dependencias permiten:

- Garantizar el orden correcto de arranque.
- Evitar errores durante el inicio.
- Asegurar que los recursos necesarios estén disponibles.
- Facilitar la recuperación automática de servicios.

Sin ellas, un servicio podría iniciarse antes de que existan los recursos que necesita.

---

### Dependencias directas e indirectas

Existen dos tipos principales.

### Dependencia directa

Un servicio necesita otro servicio específico.

```text
Servicio A

↓

Servicio B
```

---

### Dependencia indirecta

El servicio depende de otro que, a su vez, depende de un tercero.

```text
Servicio A

↓

Servicio B

↓

Servicio C
```

Si el servicio C falla, A tampoco podrá funcionar correctamente.

---

### Dependencias en Linux

En sistemas modernos, las dependencias son gestionadas por **systemd**.

Las relaciones se definen dentro de las unidades (`.service`).

Algunas directivas habituales son:

| Directiva | Función |
|------------|----------|
| `Requires=` | Dependencia obligatoria. |
| `Wants=` | Dependencia recomendada pero no obligatoria. |
| `After=` | Orden de inicio. |
| `Before=` | Indica que el servicio debe iniciarse antes que otro. |

---

### Requires

Indica que otro servicio es imprescindible.

Ejemplo:

```ini
Requires=mysql.service
```

Si `mysql.service` falla, el servicio actual también fallará.

---

### Wants

Indica una dependencia no obligatoria.

```ini
Wants=network-online.target
```

Si el servicio indicado no está disponible, el sistema intentará continuar con el arranque.

---

### After

No crea una dependencia.

Únicamente establece el orden de inicio.

Ejemplo:

```ini
After=network.target
```

Significa:

```text
Primero

↓

network.target

↓

Después

↓

Nuestro servicio
```

---

### Before

Es la directiva opuesta.

```ini
Before=apache2.service
```

Indica que el servicio debe iniciarse antes que Apache.

---

### Consultar dependencias

Mostrar dependencias de un servicio:

```bash
systemctl list-dependencies sshd
```

Mostrar dependencias inversas:

```bash
systemctl list-dependencies --reverse sshd
```

Esto permite conocer qué servicios dependen de él.

---

### Dependencias en Windows

Windows también permite definir relaciones entre servicios.

Cada servicio puede depender de:

- Otros servicios.
- Grupos de servicios.

Si una dependencia no está disponible, Windows impedirá el inicio del servicio.

---

### Consultar dependencias

PowerShell:

```powershell
Get-Service Spooler | Select-Object -ExpandProperty ServicesDependedOn
```

Mostrar los servicios que dependen de él:

```powershell
Get-Service Spooler | Select-Object -ExpandProperty DependentServices
```

---

### Consola Servicios

También pueden consultarse desde:

```text
services.msc

↓

Propiedades

↓

Dependencias
```

Se mostrará:

- Servicios necesarios.
- Servicios dependientes.

---

### Problemas habituales

Los errores más frecuentes relacionados con dependencias son:

- Servicio dependiente detenido.
- Servicio deshabilitado.
- Error durante el arranque.
- Configuración incorrecta.
- Dependencias circulares.
- Recursos no disponibles.

---

### Dependencias circulares

Una dependencia circular ocurre cuando dos servicios dependen mutuamente.

Ejemplo:

```text
Servicio A

↓

Servicio B

↓

Servicio A
```

Este tipo de configuración impide el inicio correcto de ambos servicios y debe evitarse.

---

### Diagnóstico

Cuando un servicio no inicia correctamente:

1. Comprobar su estado.

Linux:

```bash
systemctl status servicio
```

Windows:

```powershell
Get-Service NombreServicio
```

2. Revisar las dependencias.

3. Verificar que todas estén iniciadas.

4. Consultar los registros del sistema.

---

### Buen diseño

En infraestructuras grandes es recomendable:

- Reducir el número de dependencias innecesarias.
- Documentar todas las relaciones.
- Evitar dependencias circulares.
- Utilizar únicamente dependencias justificadas.
- Revisarlas tras cambios importantes.

Esto facilita el mantenimiento y reduce el riesgo de fallos en cascada.

---

### Comparativa

| Linux | Windows |
|--------|----------|
| `Requires=` | Dependencia obligatoria |
| `Wants=` | Dependencia opcional |
| `After=` | Orden de inicio |
| `Before=` | Orden previo |
| `systemctl list-dependencies` | `Get-Service` / `services.msc` |

---

### Buenas prácticas

- Define únicamente las dependencias realmente necesarias.
- Diferencia entre dependencias obligatorias y opcionales.
- Evita crear dependencias circulares.
- Comprueba siempre las dependencias antes de deshabilitar un servicio.
- Revisa los registros cuando un servicio falle durante el arranque.
- Documenta las relaciones entre servicios en servidores de producción para facilitar futuras intervenciones.

---

[⬆️ Volver al índice](#índice)

## Tipos de inicio y estados

Cada servicio dispone de una **configuración de inicio** y de un **estado de ejecución**.

Estos dos conceptos son diferentes:

- El **tipo de inicio** determina cuándo intentará iniciarse el servicio.
- El **estado** indica qué está haciendo el servicio en ese momento.

Comprender esta diferencia facilita el diagnóstico de problemas relacionados con el arranque y la disponibilidad de los servicios.

---

### Tipo de inicio

El tipo de inicio define cómo y cuándo el sistema operativo iniciará un servicio.

Los modos más habituales son:

- Automático.
- Automático (inicio retrasado).
- Manual.
- Deshabilitado.

No todos los servicios deben iniciarse automáticamente.

---

### Inicio automático

El servicio se inicia durante el arranque del sistema operativo.

Ejemplo:

```text
Arranque del sistema

↓

Inicio automático

↓

Servicio disponible
```

Es el modo habitual para:

- Servicios de red.
- Servidores web.
- Bases de datos.
- DNS.
- DHCP.
- Servicios de autenticación.

---

### Inicio automático (retrasado)

Disponible principalmente en Windows.

El servicio se inicia automáticamente, pero unos segundos después del arranque.

Su objetivo es:

- Reducir la carga durante el inicio del sistema.
- Mejorar el tiempo de arranque.
- Evitar que muchos servicios se inicien simultáneamente.

Se utiliza en servicios que no necesitan estar disponibles inmediatamente.

---

### Inicio manual

El servicio no se inicia automáticamente.

Solo comenzará cuando:

- Lo inicie un administrador.
- Lo solicite otra aplicación.
- Se produzca un evento específico.

Resulta útil para servicios poco utilizados.

---

### Servicio deshabilitado

El sistema operativo no permitirá iniciar el servicio.

```text
Servicio

↓

Deshabilitado

↓

No puede ejecutarse
```

Debe utilizarse únicamente cuando se tenga la certeza de que el servicio no es necesario.

---

### Estados de un servicio

Durante su funcionamiento un servicio puede encontrarse en distintos estados.

Los más habituales son:

- Iniciado.
- Detenido.
- Iniciando.
- Deteniendo.
- En pausa.
- Reanudándose.
- Error.

---

### Servicio iniciado

El servicio está funcionando correctamente.

```text
Disponible

↓

Aceptando solicitudes
```

Es el estado esperado para los servicios que proporcionan funciones al sistema.

---

### Servicio detenido

El servicio no está ejecutándose.

Puede deberse a:

- Se ha detenido manualmente.
- Está configurado como manual.
- Ha fallado.
- Nunca llegó a iniciarse.

---

### Iniciando

Durante el arranque algunos servicios permanecen unos segundos en estado:

```text
Starting...
```

Hasta completar su inicialización.

---

### Deteniendo

Cuando se solicita la detención de un servicio, este puede necesitar tiempo para:

- Finalizar tareas.
- Guardar información.
- Cerrar conexiones.
- Liberar recursos.

Mientras tanto permanecerá en estado:

```text
Stopping...
```

---

### Pausado

Algunos servicios permiten suspender temporalmente su funcionamiento.

```text
Ejecutándose

↓

Pausa

↓

Reanudación
```

No todos los servicios soportan este estado.

---

### Servicio con error

Si un servicio no consigue iniciarse correctamente puede aparecer en estado de error.

Las causas más frecuentes son:

- Configuración incorrecta.
- Dependencias no disponibles.
- Permisos insuficientes.
- Archivo ejecutable inexistente.
- Puerto ocupado.
- Error interno de la aplicación.

En estos casos deben consultarse los registros antes de intentar reiniciarlo.

---

### Estados en Linux

En sistemas con **systemd**, los estados más habituales son:

| Estado | Significado |
|---------|-------------|
| active | Servicio funcionando. |
| inactive | Servicio detenido. |
| failed | Error durante el inicio o ejecución. |
| activating | Iniciándose. |
| deactivating | Deteniéndose. |

Estos estados pueden consultarse con:

```bash
systemctl status servicio
```

---

### Estados en Windows

Windows utiliza estados similares.

Los principales son:

- Running.
- Stopped.
- Start Pending.
- Stop Pending.
- Paused.
- Pause Pending.
- Continue Pending.

Pueden consultarse desde:

- Administrador de servicios.
- PowerShell.
- Administrador de tareas.

---

### Cambio de estado

El ciclo habitual de un servicio es:

```text
Detenido

↓

Iniciando

↓

Iniciado

↓

Deteniendo

↓

Detenido
```

En caso de fallo:

```text
Iniciando

↓

Error

↓

Detenido
```

---

### Diagnóstico

Si un servicio no está disponible conviene comprobar:

1. Su estado actual.
2. Su tipo de inicio.
3. Sus dependencias.
4. Los registros del sistema.
5. Si existe algún conflicto de recursos.

No siempre un servicio detenido implica una incidencia; puede estar configurado para iniciarse manualmente.

---

### Buenas prácticas

- Configura como automáticos únicamente los servicios necesarios.
- Utiliza el inicio manual para servicios poco utilizados.
- Evita deshabilitar servicios sin conocer su función.
- Comprueba siempre el estado antes de reiniciar un servicio.
- Consulta los registros cuando un servicio aparezca en estado de error.
- Revisa periódicamente los servicios configurados para iniciarse automáticamente y elimina aquellos que no sean necesarios.

---

[⬆️ Volver al índice](#índice)

## Servicios críticos del sistema

No todos los servicios tienen la misma importancia.

Algunos son imprescindibles para el funcionamiento del sistema operativo y detenerlos puede provocar desde la pérdida de determinadas funciones hasta el bloqueo completo del equipo.

Estos servicios reciben el nombre de **servicios críticos** y deben administrarse con especial precaución.

---

### ¿Qué es un servicio crítico?

Un servicio crítico es aquel cuya ejecución resulta necesaria para que el sistema operativo o aplicaciones esenciales funcionen correctamente.

Estos servicios suelen encargarse de tareas como:

- Inicio del sistema.
- Gestión de usuarios.
- Red.
- Almacenamiento.
- Seguridad.
- Registro de eventos.
- Impresión.
- Actualizaciones.

Su detención puede afectar a uno o varios componentes del sistema.

---

### Características

Los servicios críticos suelen:

- Iniciarse automáticamente.
- Tener múltiples dependencias.
- Ejecutarse con cuentas privilegiadas.
- Permanecer activos durante toda la sesión.
- Ser utilizados por numerosos procesos.

En muchos casos, otros servicios dependen directamente de ellos.

---

### Servicios críticos en Linux

Algunos ejemplos habituales son:

| Servicio | Función |
|----------|----------|
| `systemd` | Sistema de inicio y gestión de servicios. |
| `systemd-journald` | Registro de eventos. |
| `NetworkManager` | Gestión de la red. |
| `systemd-logind` | Gestión de sesiones de usuario. |
| `sshd` | Acceso remoto mediante SSH (en servidores). |
| `cron` o `crond` | Ejecución de tareas programadas. |

Dependiendo de la distribución, pueden existir otros servicios igualmente importantes.

---

### Servicios críticos en Windows

Entre los más importantes se encuentran:

| Servicio | Función |
|----------|----------|
| Service Control Manager (SCM) | Administración de servicios. |
| Windows Event Log | Registro de eventos. |
| Remote Procedure Call (RPC) | Comunicación entre procesos. |
| Windows Update | Actualizaciones del sistema. |
| DHCP Client | Obtención automática de direcciones IP. |
| DNS Client | Resolución de nombres. |
| Print Spooler | Gestión de impresión. |

Muchos servicios de Windows dependen del servicio **RPC**, por lo que su interrupción afecta a gran parte del sistema.

---

### Dependencias

Los servicios críticos suelen tener numerosas dependencias.

Ejemplo:

```text
Aplicación

↓

Servidor web

↓

Red

↓

DNS

↓

Sistema operativo
```

Si un servicio de nivel inferior deja de funcionar, todos los superiores pueden verse afectados.

---

### Riesgos al detener un servicio crítico

Detener un servicio importante puede provocar:

- Pérdida de conectividad.
- Imposibilidad de iniciar sesión.
- Fallo de aplicaciones.
- Interrupción de servicios de red.
- Reinicios inesperados.
- Inestabilidad del sistema.

Por ello siempre debe evaluarse el impacto antes de detener un servicio.

---

### ¿Cómo identificar un servicio crítico?

Antes de realizar cualquier cambio conviene comprobar:

- Si otros servicios dependen de él.
- Si se inicia automáticamente.
- Su función dentro del sistema.
- La documentación del fabricante.
- Los registros del sistema.

Nunca debe asumirse que un servicio puede deshabilitarse únicamente porque su nombre resulte desconocido.

---

### Servicios innecesarios

No todos los servicios instalados son críticos.

Algunos pertenecen a:

- Software de terceros.
- Aplicaciones concretas.
- Herramientas de administración.
- Componentes opcionales.

En servidores es habitual deshabilitar servicios que no sean necesarios para reducir el consumo de recursos y la superficie de ataque.

---

### Antes de deshabilitar un servicio

Es recomendable seguir este procedimiento:

1. Identificar el servicio.
2. Revisar sus dependencias.
3. Comprobar si otras aplicaciones lo utilizan.
4. Consultar la documentación.
5. Realizar una copia de seguridad de la configuración si procede.
6. Probar el cambio en un entorno de pruebas cuando sea posible.

---

### Recuperación

Si un servicio crítico deja de funcionar:

1. Revisar los registros del sistema.
2. Comprobar las dependencias.
3. Verificar la configuración.
4. Intentar reiniciarlo.
5. Confirmar que vuelve a su estado operativo.

En algunos casos puede ser necesario reiniciar el sistema para restaurar determinados servicios.

---

### Comparativa

| Servicio | Linux | Windows |
|----------|--------|----------|
| Gestión de servicios | `systemd` | Service Control Manager |
| Registro de eventos | `systemd-journald` | Windows Event Log |
| Gestión de red | `NetworkManager` | DHCP Client / DNS Client |
| Programación de tareas | `cron` | Task Scheduler |
| Acceso remoto | `sshd` | Remote Desktop Services (si está habilitado) |

---

### Buenas prácticas

- No deshabilites un servicio sin conocer exactamente su función.
- Comprueba siempre las dependencias antes de detener un servicio.
- Mantén activos los servicios esenciales para el funcionamiento del sistema.
- Deshabilita únicamente servicios innecesarios y tras evaluar su impacto.
- Documenta cualquier cambio realizado sobre servicios críticos.
- Realiza las pruebas en un entorno controlado antes de aplicar cambios en producción.
- Consulta los registros del sistema si un servicio crítico deja de funcionar.

---

[⬆️ Volver al índice](#índice)

## Recuperación automática de servicios

Un servicio puede detenerse inesperadamente debido a errores de software, problemas de configuración, falta de recursos o fallos del sistema operativo.

Para minimizar el impacto de estas incidencias, tanto Linux como Windows permiten configurar **mecanismos de recuperación automática**, de forma que el servicio vuelva a estar disponible sin intervención del administrador.

Estas funciones son especialmente importantes en servidores y servicios críticos que deben permanecer operativos el mayor tiempo posible.

---

### ¿Qué es la recuperación automática?

La recuperación automática consiste en ejecutar una acción cuando un servicio finaliza de forma inesperada.

Las acciones más habituales son:

- Reiniciar el servicio.
- Reiniciar el equipo.
- Ejecutar un programa o script.
- Registrar el error.
- Enviar una alerta.

El objetivo es reducir el tiempo de indisponibilidad del servicio.

---

### ¿Cuándo se utiliza?

La recuperación automática es recomendable para servicios como:

- Servidores web.
- Bases de datos.
- DNS.
- DHCP.
- Aplicaciones empresariales.
- Servicios de autenticación.
- Monitorización.

En cambio, no suele ser necesaria para servicios utilizados de forma puntual o manual.

---

### Recuperación en Linux

En sistemas con **systemd**, la recuperación se configura mediante el archivo de unidad (`.service`).

Algunas directivas habituales son:

```ini
Restart=always
```

o

```ini
Restart=on-failure
```

Estas opciones indican cuándo debe reiniciarse automáticamente el servicio.

---

### Directiva Restart

Las opciones más utilizadas son:

| Valor | Comportamiento |
|--------|----------------|
| `no` | No reiniciar. |
| `always` | Reiniciar siempre. |
| `on-failure` | Reiniciar solo si falla. |
| `on-abnormal` | Reiniciar tras una finalización anómala. |
| `on-success` | Reiniciar tras finalizar correctamente. |

La opción más utilizada en servidores suele ser:

```ini
Restart=on-failure
```

---

### Tiempo de espera

Puede configurarse un retraso antes del reinicio.

Ejemplo:

```ini
RestartSec=5
```

Esto hace que systemd espere cinco segundos antes de volver a iniciar el servicio.

---

### Ejemplo

```ini
[Service]

ExecStart=/usr/bin/app

Restart=on-failure

RestartSec=10
```

Si la aplicación falla:

```text
Error

↓

Esperar 10 segundos

↓

Reinicio automático
```

---

### Límite de reinicios

Para evitar bucles infinitos, systemd controla cuántas veces puede reiniciarse un servicio en un periodo determinado.

Si supera ese límite:

```text
Servicio

↓

Demasiados errores

↓

Estado failed
```

Será necesaria la intervención del administrador.

---

### Recuperación en Windows

Windows incorpora opciones de recuperación desde las propiedades del servicio.

Ruta:

```text
services.msc

↓

Propiedades

↓

Recuperación
```

---

### Acciones disponibles

Windows permite configurar acciones distintas para:

- Primer error.
- Segundo error.
- Errores posteriores.

Las acciones posibles son:

- No realizar ninguna acción.
- Reiniciar el servicio.
- Ejecutar un programa.
- Reiniciar el equipo.

Esto ofrece una gran flexibilidad para adaptarse a distintos escenarios.

---

### Reinicio automático

Ejemplo:

```text
Primer error

↓

Reiniciar servicio

↓

Segundo error

↓

Reiniciar servicio

↓

Errores posteriores

↓

Ejecutar script
```

Es una configuración habitual en servicios críticos.

---

### Ejecutar un programa

En Windows también es posible ejecutar un programa cuando un servicio falla.

Ejemplos:

- Enviar un correo.
- Ejecutar un script de PowerShell.
- Registrar información adicional.
- Lanzar una herramienta de monitorización.

---

### Reinicio del equipo

En situaciones críticas puede configurarse el reinicio automático del servidor.

Debe utilizarse únicamente cuando:

- El servicio es imprescindible.
- El reinicio resulta menos perjudicial que mantener el servicio inactivo.
- Existe un procedimiento documentado para ello.

---

### Monitorización

La recuperación automática no sustituye a la monitorización.

Siempre es recomendable:

- Revisar los registros.
- Identificar la causa del fallo.
- Corregir el problema de origen.

Si un servicio entra en un ciclo continuo de reinicios, debe investigarse antes de considerar el problema resuelto.

---

### Problemas habituales

Algunos errores frecuentes son:

- Configurar reinicios infinitos.
- No establecer tiempos de espera.
- Ignorar los registros del sistema.
- Reiniciar un servicio con una configuración incorrecta.
- Ocultar fallos reales mediante reinicios continuos.

La recuperación automática debe complementar el diagnóstico, no sustituirlo.

---

### Comparativa

| Linux | Windows |
|--------|----------|
| `Restart=` | Acciones de recuperación |
| `RestartSec=` | Tiempo antes del reinicio |
| systemd | Service Control Manager |
| Archivo `.service` | Propiedades del servicio |
| Reinicio automático | Reinicio automático |

---

### Buenas prácticas

- Configura la recuperación automática únicamente en servicios que deban permanecer siempre disponibles.
- Utiliza tiempos de espera razonables antes de reiniciar un servicio.
- Evita los bucles de reinicio continuo.
- Revisa siempre los registros tras un reinicio automático.
- Corrige la causa del fallo en lugar de depender únicamente de la recuperación automática.
- Documenta la política de recuperación aplicada a los servicios críticos.
- Comprueba periódicamente que las acciones de recuperación siguen siendo adecuadas para el entorno.

---

[⬆️ Volver al índice](#índice)

## Monitorización y diagnóstico

Supervisar el estado de los servicios es una tarea fundamental para garantizar la disponibilidad de un sistema.

La **monitorización** permite detectar incidencias antes de que afecten a los usuarios, mientras que el **diagnóstico** ayuda a identificar la causa de un problema cuando un servicio deja de funcionar correctamente.

En entornos de producción, una buena estrategia de monitorización reduce el tiempo de respuesta ante fallos y facilita el mantenimiento preventivo.

---

### ¿Qué es la monitorización?

La monitorización consiste en supervisar continuamente el estado de uno o varios servicios.

Permite conocer aspectos como:

- Estado del servicio.
- Disponibilidad.
- Tiempo de actividad.
- Consumo de recursos.
- Errores registrados.
- Reinicios inesperados.

Su objetivo es detectar problemas lo antes posible.

---

### ¿Qué es el diagnóstico?

El diagnóstico comienza cuando se detecta una incidencia.

Consiste en analizar:

- Registros.
- Configuración.
- Dependencias.
- Recursos utilizados.
- Estado del sistema.

El objetivo es localizar la causa del problema y aplicar la solución adecuada.

---

### Información importante

Cuando un servicio falla conviene recopilar:

- Nombre del servicio.
- Estado actual.
- Hora del fallo.
- Últimos cambios realizados.
- Dependencias.
- Consumo de CPU.
- Consumo de memoria.
- Eventos registrados.

Cuanta más información se obtenga, más sencillo será encontrar la causa.

---

### Registros del sistema

Los registros son la principal fuente de información para diagnosticar servicios.

Linux:

```text
journalctl
```

Windows:

```text
Visor de eventos
```

Muchos problemas pueden resolverse revisando únicamente los registros.

---

### Registros del servicio

Además de los registros generales, muchas aplicaciones generan sus propios archivos de log.

Ejemplos:

```text
Apache

↓

access.log

error.log
```

```text
Nginx

↓

access.log

error.log
```

```text
MySQL

↓

error.log
```

Estos registros contienen información específica sobre el funcionamiento del servicio.

---

### Supervisión del estado

Un servicio puede encontrarse en diferentes estados:

- Ejecutándose.
- Detenido.
- Iniciando.
- Deteniéndose.
- Error.

Es recomendable supervisar periódicamente los servicios críticos para detectar cambios inesperados.

---

### Supervisión del rendimiento

No basta con comprobar que un servicio está iniciado.

También debe vigilarse su rendimiento.

Aspectos habituales:

- Uso de CPU.
- Uso de memoria.
- Número de conexiones.
- Tiempo de respuesta.
- Consumo de disco.
- Tráfico de red.

Un servicio puede estar funcionando y, aun así, ofrecer un rendimiento deficiente.

---

### Alertas

Las plataformas de monitorización suelen generar alertas cuando detectan situaciones como:

- Servicio detenido.
- Consumo elevado de CPU.
- Falta de memoria.
- Espacio en disco insuficiente.
- Número excesivo de errores.
- Reinicios repetitivos.

Estas alertas permiten actuar antes de que el problema afecte a los usuarios.

---

### Herramientas habituales

Algunas herramientas utilizadas para monitorizar servicios son:

Linux:

- `journalctl`
- `systemctl`
- `top`
- `htop`
- `sar`

Windows:

- Administrador de tareas.
- Monitor de recursos.
- Visor de eventos.
- Performance Monitor (PerfMon).

En entornos empresariales también es habitual utilizar soluciones como:

- Zabbix.
- Nagios.
- PRTG.
- Centreon.

---

### Diagnóstico paso a paso

Cuando un servicio deja de funcionar, un procedimiento habitual sería:

1. Comprobar si el servicio está iniciado.
2. Revisar los registros del sistema.
3. Consultar los registros propios de la aplicación.
4. Verificar las dependencias.
5. Revisar la configuración.
6. Analizar el consumo de recursos.
7. Comprobar si existen conflictos de red o almacenamiento.
8. Reiniciar el servicio únicamente si es necesario.

Seguir siempre el mismo procedimiento ayuda a reducir errores durante la resolución de incidencias.

---

### Problemas habituales

Entre las causas más frecuentes de fallo se encuentran:

- Configuración incorrecta.
- Dependencias no disponibles.
- Falta de permisos.
- Puerto ocupado.
- Espacio insuficiente en disco.
- Memoria agotada.
- Certificados caducados.
- Errores tras una actualización.

No todos los fallos tienen el mismo origen, por lo que es importante analizar la información disponible antes de aplicar una solución.

---

### Monitorización continua

En servidores críticos es recomendable implementar monitorización permanente.

Esto permite:

- Detectar incidencias en tiempo real.
- Registrar tendencias.
- Analizar el rendimiento histórico.
- Planificar ampliaciones de recursos.
- Mejorar la disponibilidad del servicio.

La monitorización continua es una parte esencial de cualquier infraestructura profesional.

---

### Buenas prácticas

- Supervisa periódicamente todos los servicios críticos.
- Revisa los registros antes de reiniciar un servicio.
- Analiza tanto el estado como el rendimiento del servicio.
- Configura alertas para detectar fallos importantes de forma automática.
- Documenta las incidencias y las acciones realizadas durante el diagnóstico.
- Mantén un procedimiento de diagnóstico estructurado para evitar omitir comprobaciones importantes.
- Utiliza herramientas de monitorización centralizada en entornos con múltiples servidores.

---

[⬆️ Volver al índice](#índice)

## Seguridad de los servicios

Los servicios suelen ejecutarse de forma continua y, en muchos casos, están accesibles desde la red.

Por este motivo constituyen uno de los principales objetivos de los ataques informáticos y deben administrarse siguiendo criterios de seguridad.

Una configuración inadecuada puede permitir:

- Escalada de privilegios.
- Ejecución de código.
- Acceso no autorizado.
- Robo de información.
- Denegación de servicio (DoS).
- Movimiento lateral dentro de la red.

Proteger los servicios es una parte esencial de la administración de sistemas.

---

### Principio de mínimo privilegio

Todo servicio debe ejecutarse únicamente con los permisos estrictamente necesarios para realizar su función.

No es recomendable ejecutar todos los servicios como administrador o **root**.

Ejemplo:

```text
Incorrecto

↓

Servicio

↓

root
```

```text
Correcto

↓

Servicio

↓

Usuario específico
```

Reducir los privilegios limita el impacto de un posible compromiso.

---

### Cuentas de servicio

Es recomendable utilizar cuentas específicas para cada servicio.

Ejemplos:

Linux:

```text
www-data

mysql

postgres
```

Windows:

- Local Service.
- Network Service.
- Usuario de servicio dedicado.
- Cuenta administrada de dominio (gMSA).

Esto facilita el control de permisos y mejora el aislamiento entre aplicaciones.

---

### Limitar permisos

Un servicio solo debería tener acceso a:

- Sus archivos.
- Sus directorios.
- Su configuración.
- Los recursos necesarios para funcionar.

Debe evitarse conceder permisos innecesarios sobre:

- Todo el sistema de archivos.
- Otras aplicaciones.
- Directorios de usuarios.
- Recursos compartidos.

---

### Servicios innecesarios

Cada servicio activo aumenta la superficie de ataque.

Es recomendable:

- Identificar servicios que no se utilizan.
- Deshabilitarlos.
- Eliminarlos si no son necesarios.

Menos servicios activos implican menos posibilidades de explotación.

---

### Mantener el software actualizado

Las vulnerabilidades descubiertas en un servicio suelen corregirse mediante actualizaciones.

Es importante mantener actualizados:

- Sistema operativo.
- Servicios.
- Aplicaciones.
- Bibliotecas.
- Dependencias.

Una actualización puede solucionar fallos de seguridad críticos.

---

### Protección de la configuración

Los archivos de configuración suelen contener información sensible.

Por ejemplo:

- Credenciales.
- Certificados.
- Claves privadas.
- Rutas internas.
- Direcciones IP.

Es recomendable:

- Restringir los permisos de acceso.
- Evitar compartirlos innecesariamente.
- Mantener copias de seguridad.

---

### Exposición a la red

No todos los servicios deben estar accesibles desde Internet.

Antes de publicar un servicio conviene comprobar:

- Si realmente necesita acceso externo.
- Qué puertos utiliza.
- Qué usuarios podrán acceder.
- Qué mecanismos de autenticación emplea.

Siempre que sea posible, limita el acceso mediante reglas de firewall.

---

### Cifrado

Cuando un servicio transmite información sensible debe utilizar conexiones cifradas.

Ejemplos:

- HTTPS.
- SSH.
- SFTP.
- SMTPS.
- LDAPS.

Evita protocolos inseguros cuando existan alternativas cifradas.

---

### Autenticación

Los servicios deben utilizar mecanismos de autenticación adecuados.

Recomendaciones:

- Contraseñas robustas.
- Autenticación multifactor (MFA), cuando sea posible.
- Certificados.
- Claves SSH.
- Integración con directorios corporativos.

Evita el uso de credenciales predeterminadas.

---

### Auditoría

Es recomendable registrar:

- Inicios y detenciones del servicio.
- Cambios de configuración.
- Errores.
- Accesos.
- Intentos de autenticación.

Estos registros permiten detectar comportamientos anómalos y facilitar investigaciones posteriores.

---

### Supervisión

Además de proteger el servicio, conviene supervisarlo continuamente.

Aspectos recomendables:

- Estado.
- Disponibilidad.
- Reinicios inesperados.
- Consumo de recursos.
- Intentos de acceso fallidos.
- Errores repetitivos.

Una supervisión adecuada permite detectar incidentes antes de que afecten al funcionamiento del sistema.

---

### Aislamiento

Siempre que sea posible, los servicios deben ejecutarse de forma aislada.

Ejemplos:

- Máquinas virtuales.
- Contenedores.
- Usuarios independientes.
- Redes separadas.

El aislamiento reduce el impacto en caso de compromiso.

---

### Problemas habituales

Algunas configuraciones inseguras son:

- Ejecutar servicios como `root` o Administrador sin necesidad.
- Mantener servicios innecesarios activos.
- Utilizar credenciales débiles.
- No aplicar actualizaciones.
- Exponer servicios directamente a Internet.
- Compartir cuentas de servicio entre varias aplicaciones.
- No revisar los registros de seguridad.

---

### Comparativa

| Medida | Beneficio |
|---------|-----------|
| Mínimo privilegio | Reduce el impacto de un ataque |
| Cuentas dedicadas | Mejor aislamiento |
| Actualizaciones | Corrigen vulnerabilidades |
| Firewall | Reduce la exposición |
| Cifrado | Protege la información |
| Auditoría | Facilita investigaciones |
| Monitorización | Detecta incidencias rápidamente |
| Aislamiento | Limita la propagación de un compromiso |

---

### Buenas prácticas

- Ejecuta cada servicio con la cuenta de menor privilegio posible.
- Deshabilita o elimina los servicios que no sean necesarios.
- Mantén el sistema y las aplicaciones actualizados.
- Protege los archivos de configuración y las credenciales.
- Expón únicamente los servicios que deban ser accesibles desde la red.
- Utiliza protocolos cifrados para transmitir información sensible.
- Revisa periódicamente los registros y los intentos de acceso.
- Documenta los cambios de configuración relacionados con la seguridad.
- Realiza auditorías periódicas sobre los servicios críticos.

---

[⬆️ Volver al índice](#índice)

## Automatización

En entornos con numerosos equipos o servidores, administrar manualmente los servicios resulta poco práctico.

La **automatización** permite ejecutar tareas repetitivas de forma automática, reduciendo errores, mejorando la eficiencia y garantizando una administración homogénea de toda la infraestructura.

Las tareas automatizadas pueden utilizarse tanto para mantenimiento preventivo como para la resolución automática de incidencias.

---

### ¿Qué es la automatización?

Automatizar consiste en ejecutar acciones sin intervención manual mediante:

- Scripts.
- Programadores de tareas.
- Herramientas de administración.
- Plataformas de gestión centralizada.

Su objetivo es reducir el tiempo dedicado a tareas repetitivas.

---

### Ventajas

La automatización permite:

- Reducir errores humanos.
- Ahorrar tiempo.
- Estandarizar procedimientos.
- Mejorar la disponibilidad de los servicios.
- Facilitar la administración de múltiples equipos.
- Responder rápidamente ante incidencias.

Es una práctica habitual en cualquier infraestructura empresarial.

---

### Tareas que pueden automatizarse

Algunos ejemplos son:

- Iniciar servicios.
- Detener servicios.
- Reiniciarlos.
- Comprobar su estado.
- Registrar incidencias.
- Enviar alertas.
- Generar informes.
- Aplicar configuraciones.

Muchas de estas tareas pueden ejecutarse diariamente sin intervención del administrador.

---

### Automatización mediante scripts

Los scripts son una de las formas más habituales de automatizar servicios.

Linux:

- Bash.
- Python.

Windows:

- PowerShell.
- Batch (CMD).

Los scripts permiten combinar múltiples acciones en un único procedimiento.

---

### Ejemplo de automatización

Un script podría realizar el siguiente proceso:

```text
Comprobar servicio

↓

¿Está detenido?

↓

Sí

↓

Reiniciar

↓

Registrar la acción

↓

Enviar notificación
```

Todo ello sin intervención manual.

---

### Programación de tareas

La automatización suele combinarse con tareas programadas.

Ejemplos:

Linux:

- `cron`
- Timers de `systemd`

Windows:

- Programador de tareas (Task Scheduler)

Esto permite ejecutar comprobaciones periódicas.

---

### Supervisión automática

Un procedimiento habitual consiste en comprobar periódicamente:

- Si el servicio está iniciado.
- Si consume demasiada memoria.
- Si responde correctamente.
- Si existen errores recientes.

Cuando se detecta una anomalía, el sistema puede actuar automáticamente.

---

### Alertas

Los scripts pueden generar avisos cuando ocurre una incidencia.

Ejemplos:

- Correo electrónico.
- Mensaje en Microsoft Teams.
- Notificación en Slack.
- Registro en un sistema ITSM.
- Mensaje mediante API.

Esto permite actuar rápidamente incluso antes de que los usuarios detecten el problema.

---

### Automatización masiva

En grandes organizaciones es habitual administrar cientos o miles de equipos.

La automatización permite aplicar cambios simultáneamente.

Ejemplo:

```text
Servidor de administración

↓

100 servidores

↓

Reinicio del mismo servicio

↓

Verificación del resultado

↓

Informe final
```

Este procedimiento sería inviable de realizar manualmente.

---

### Herramientas habituales

Algunas soluciones utilizadas para automatizar la administración de servicios son:

- PowerShell.
- Bash.
- Ansible.
- Puppet.
- Chef.
- SaltStack.
- System Center.
- Microsoft Intune.

Estas plataformas permiten gestionar infraestructuras completas desde un único punto.

---

### Automatización segura

Automatizar no significa ejecutar cualquier acción sin control.

Antes de aplicar cambios automáticos es recomendable:

- Validar la configuración.
- Comprobar dependencias.
- Registrar todas las acciones.
- Notificar los errores.
- Probar los scripts en un entorno de pruebas.

La automatización debe aumentar la fiabilidad, no introducir nuevos problemas.

---

### Errores habituales

Algunos fallos frecuentes son:

- Reiniciar servicios de forma continua sin investigar la causa.
- Ejecutar scripts con permisos excesivos.
- No registrar las acciones realizadas.
- No controlar los errores del script.
- Automatizar procesos sin haberlos probado previamente.

Una automatización mal diseñada puede generar más incidencias que las que pretende resolver.

---

### Automatización vs intervención manual

| Automatización | Administración manual |
|----------------|-----------------------|
| Rápida | Más lenta |
| Repetible | Depende del operador |
| Menos errores | Mayor riesgo de errores humanos |
| Escalable | Difícil de aplicar en muchos equipos |
| Requiere planificación | Útil para tareas puntuales |

Lo habitual es combinar ambos enfoques según la situación.

---

### Buenas prácticas

- Automatiza únicamente tareas repetitivas y bien definidas.
- Prueba los scripts antes de utilizarlos en producción.
- Registra todas las acciones realizadas automáticamente.
- Controla los errores y excepciones de los scripts.
- Utiliza cuentas con los permisos mínimos necesarios.
- Programa comprobaciones periódicas para los servicios críticos.
- Revisa y actualiza los scripts cuando cambie la infraestructura.
- Documenta el funcionamiento de cada automatización.

---

[⬆️ Volver al índice](#índice)

## Buenas prácticas

Una correcta administración de los servicios es fundamental para garantizar la disponibilidad, el rendimiento y la seguridad de un sistema.

Aplicar buenas prácticas reduce el riesgo de interrupciones, facilita el mantenimiento y simplifica la resolución de incidencias.

Estas recomendaciones son aplicables tanto a equipos de usuario como a servidores Linux y Windows.

---

### Conoce la función de cada servicio

Antes de modificar un servicio es importante conocer:

- Qué función realiza.
- Qué aplicaciones lo utilizan.
- Qué dependencias tiene.
- Qué impacto tendría su detención.

No deshabilites un servicio únicamente porque su nombre resulte desconocido.

---

### Mantén solo los servicios necesarios

Cada servicio en ejecución consume recursos y aumenta la superficie de ataque.

Es recomendable:

- Deshabilitar servicios que no se utilicen.
- Eliminar aplicaciones innecesarias.
- Revisar periódicamente los servicios instalados.

Un sistema con menos servicios activos suele ser más seguro y eficiente.

---

### Utiliza el principio de mínimo privilegio

Ejecuta cada servicio con la cuenta que disponga únicamente de los permisos necesarios.

Evita utilizar:

- `root` en Linux.
- Administrador o **Local System** en Windows.

Salvo cuando sea estrictamente necesario.

Esto limita el impacto de un posible compromiso del servicio.

---

### Documenta los cambios

Cada modificación importante debería quedar registrada.

Por ejemplo:

- Fecha.
- Servicio afectado.
- Motivo del cambio.
- Configuración anterior.
- Configuración nueva.
- Responsable.

La documentación facilita el mantenimiento y las auditorías.

---

### Revisa los registros

Cuando un servicio falle:

1. Consulta los registros del sistema.
2. Revisa los registros propios de la aplicación.
3. Analiza el mensaje de error antes de reiniciar el servicio.

Evita solucionar problemas únicamente mediante reinicios continuos.

---

### Configura la recuperación automática

Los servicios críticos deberían disponer de mecanismos de recuperación.

Por ejemplo:

```text
Error

↓

Reinicio automático

↓

Servicio operativo
```

Esto reduce el tiempo de indisponibilidad y mejora la continuidad del servicio.

---

### Supervisa el estado de los servicios

Realiza comprobaciones periódicas para verificar:

- Estado.
- Tiempo de actividad.
- Consumo de CPU.
- Memoria.
- Errores.
- Reinicios inesperados.

La monitorización continua permite detectar problemas antes de que afecten a los usuarios.

---

### Mantén el software actualizado

Las actualizaciones permiten:

- Corregir vulnerabilidades.
- Mejorar el rendimiento.
- Solucionar errores.
- Incorporar nuevas funciones.

Mantén actualizados:

- Sistema operativo.
- Servicios.
- Aplicaciones.
- Dependencias.

---

### Protege la configuración

Los archivos de configuración pueden contener información sensible.

Es recomendable:

- Restringir los permisos de acceso.
- Proteger credenciales y certificados.
- Realizar copias de seguridad antes de modificarlos.
- Documentar los cambios realizados.

---

### Automatiza tareas repetitivas

Siempre que sea posible:

- Automatiza comprobaciones.
- Genera informes automáticamente.
- Programa tareas de mantenimiento.
- Envía alertas cuando se detecten incidencias.

La automatización mejora la eficiencia y reduce los errores humanos.

---

### Prueba antes de aplicar cambios

Antes de modificar servicios críticos:

- Utiliza un entorno de pruebas cuando sea posible.
- Verifica la configuración.
- Comprueba las dependencias.
- Evalúa el impacto del cambio.

Aplicar cambios directamente en producción incrementa el riesgo de interrupciones.

---

### Planifica el mantenimiento

Las intervenciones importantes deberían realizarse:

- En horarios de baja actividad.
- Con copia de seguridad disponible.
- Informando previamente a los usuarios si procede.
- Con un plan de reversión en caso de fallo.

Una buena planificación reduce el impacto sobre la disponibilidad del servicio.

---

### Auditorías periódicas

Es recomendable revisar de forma periódica:

- Servicios instalados.
- Servicios activos.
- Configuración.
- Permisos.
- Dependencias.
- Registros de errores.

Estas revisiones ayudan a detectar configuraciones obsoletas o problemas potenciales.

---

### Resumen de recomendaciones

| Recomendación | Beneficio |
|---------------|-----------|
| Conocer la función de cada servicio | Evita cambios innecesarios |
| Mantener solo los servicios necesarios | Reduce consumo y superficie de ataque |
| Aplicar el principio de mínimo privilegio | Mejora la seguridad |
| Documentar los cambios | Facilita el mantenimiento |
| Revisar los registros | Agiliza el diagnóstico |
| Configurar recuperación automática | Reduce el tiempo de indisponibilidad |
| Supervisar los servicios | Detecta incidencias de forma temprana |
| Mantener el software actualizado | Corrige errores y vulnerabilidades |
| Automatizar tareas | Reduce errores humanos |
| Probar antes de modificar | Disminuye el riesgo en producción |

---

[⬆️ Volver al índice](#índice)