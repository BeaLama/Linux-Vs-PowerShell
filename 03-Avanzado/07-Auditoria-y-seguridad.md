# 07 - Auditoría y seguridad

## Introducción

La auditoría y la seguridad son elementos fundamentales en la administración de sistemas modernos. No basta con configurar correctamente un servidor o mantenerlo actualizado; también es necesario registrar la actividad del sistema, controlar quién accede a los recursos, supervisar continuamente posibles amenazas y disponer de procedimientos para responder ante incidentes de seguridad.

En este apartado se estudian los principales mecanismos de auditoría, los registros de seguridad, el control de acceso, la autenticación, las políticas de seguridad, el hardening de sistemas y la monitorización de eventos, así como las buenas prácticas para proteger infraestructuras tanto Linux como Windows.

El conocimiento de estos conceptos permite mejorar la seguridad, facilitar las tareas de administración y responder de forma eficaz ante posibles incidentes.

---

## Índice

- [Auditoría de sistemas](#auditoría-de-sistemas)
- [Registros de seguridad](#registros-de-seguridad)
- [Control de acceso](#control-de-acceso)
- [Autenticación y autorización](#autenticación-y-autorización)
- [Políticas de seguridad](#políticas-de-seguridad)
- [Hardening del sistema](#hardening-del-sistema)
- [Monitorización de seguridad](#monitorización-de-seguridad)
- [Respuesta ante incidentes](#respuesta-ante-incidentes)
- [Buenas prácticas](#buenas-prácticas)

---

## Auditoría de sistemas

La **auditoría de sistemas** consiste en recopilar, revisar y analizar la actividad de un sistema operativo con el objetivo de comprobar que funciona de forma correcta, segura y conforme a las políticas establecidas.

Mediante la auditoría es posible conocer quién ha realizado una acción, cuándo se produjo, sobre qué recurso actuó y cuál fue el resultado.

Es una práctica fundamental para la administración de sistemas, la seguridad informática y el cumplimiento normativo.

---

### ¿Qué es una auditoría?

Una auditoría es el proceso de registrar y analizar los eventos que ocurren en un sistema.

Estos eventos pueden incluir:

- Inicios y cierres de sesión.
- Accesos a archivos.
- Cambios de permisos.
- Instalación de software.
- Ejecución de programas.
- Modificación de la configuración.
- Errores del sistema.

Toda esta información queda registrada para su posterior análisis.

---

### Objetivos de la auditoría

La auditoría permite:

- Detectar accesos no autorizados.
- Investigar incidentes de seguridad.
- Identificar cambios realizados en el sistema.
- Comprobar el cumplimiento de políticas internas.
- Facilitar tareas de mantenimiento.
- Obtener evidencias durante una investigación.

No está orientada únicamente a detectar ataques, sino también a comprender el comportamiento normal del sistema.

---

### ¿Qué información registra?

Dependiendo de la configuración, un sistema puede registrar información como:

- Usuario que realizó la acción.
- Fecha y hora.
- Equipo afectado.
- Recurso utilizado.
- Acción realizada.
- Resultado (éxito o error).

Ejemplo:

```text
Usuario: beatriz

Hora: 10:42

Acción: Inicio de sesión

Resultado: Correcto
```

---

### Tipos de auditoría

Las auditorías pueden centrarse en distintos aspectos.

Los más habituales son:

- Auditoría de accesos.
- Auditoría de autenticación.
- Auditoría de archivos.
- Auditoría de cambios de configuración.
- Auditoría de procesos.
- Auditoría de servicios.
- Auditoría de red.

Cada una proporciona información sobre un área concreta del sistema.

---

### Auditoría de accesos

Registra quién accede al sistema.

Ejemplos:

- Inicio de sesión.
- Cierre de sesión.
- Intentos fallidos.
- Bloqueos de cuenta.
- Accesos remotos.

Es una de las auditorías más utilizadas.

---

### Auditoría de archivos

Permite registrar operaciones realizadas sobre archivos y carpetas.

Por ejemplo:

- Lectura.
- Escritura.
- Eliminación.
- Cambio de permisos.
- Cambio de propietario.

Es especialmente útil cuando se trabaja con información sensible.

---

### Auditoría de cambios

Registra modificaciones importantes en el sistema.

Ejemplos:

- Creación de usuarios.
- Eliminación de cuentas.
- Instalación de aplicaciones.
- Cambios de configuración.
- Modificación de servicios.

Facilita identificar quién realizó cada cambio.

---

### Auditoría en Linux

Linux registra gran parte de la actividad mediante:

- `journald`
- `syslog`
- `auditd`

Cuando se requiere una auditoría detallada, suele utilizarse **Auditd**, que permite registrar eventos específicos relacionados con la seguridad.

---

### Auditoría en Windows

Windows incorpora un sistema de auditoría integrado.

Puede registrar eventos relacionados con:

- Inicio de sesión.
- Acceso a objetos.
- Cambios de permisos.
- Uso de privilegios.
- Administración de cuentas.
- Creación de procesos.

La información se almacena en el **Visor de eventos**, especialmente en el registro de **Seguridad**.

---

### Importancia de los registros

Una auditoría solo resulta útil si los registros son:

- Precisos.
- Completos.
- Protegidos frente a modificaciones.
- Conservados durante el tiempo necesario.

Eliminar o alterar los registros dificulta el análisis de cualquier incidencia.

---

### Limitaciones

La auditoría también presenta algunos inconvenientes.

Entre ellos:

- Mayor consumo de almacenamiento.
- Incremento del número de eventos registrados.
- Necesidad de revisar grandes volúmenes de información.
- Posible impacto en el rendimiento si se auditan demasiados eventos.

Por ello conviene registrar únicamente la información realmente necesaria.

---

### Beneficios

Una auditoría correctamente configurada permite:

- Mejorar la seguridad.
- Facilitar investigaciones.
- Detectar actividades sospechosas.
- Cumplir requisitos legales y normativos.
- Obtener trazabilidad sobre las acciones realizadas.

Es una herramienta imprescindible en cualquier entorno profesional.

---

### Comparativa

| Linux | Windows |
|--------|----------|
| `journald` | Visor de eventos |
| `syslog` | Registro de Seguridad |
| `auditd` | Directivas de auditoría |
| Archivos de log | Eventos centralizados |

---

### Buenas prácticas

- Audita únicamente los eventos que aporten información útil.
- Conserva los registros durante el tiempo establecido por la organización o la normativa aplicable.
- Protege los registros frente a modificaciones o eliminaciones no autorizadas.
- Sincroniza la hora de los equipos para garantizar la coherencia temporal de los eventos.
- Revisa periódicamente los registros en busca de actividades anómalas.
- Documenta la configuración de la auditoría para facilitar su mantenimiento y revisión.
- Automatiza el análisis de registros cuando el volumen de información sea elevado.

---

[⬆️ Volver al índice](#índice)

## Registros de seguridad

Los **registros de seguridad** (*security logs*) son archivos o bases de datos donde el sistema operativo almacena los eventos relacionados con la seguridad.

Estos registros permiten reconstruir lo ocurrido en un equipo o servidor, identificar comportamientos anómalos y obtener evidencias durante una investigación.

Su correcta configuración y revisión constituye uno de los pilares de la administración segura de sistemas.

---

### ¿Qué es un registro de seguridad?

Un registro de seguridad contiene información sobre eventos que afectan a la protección del sistema.

Por ejemplo:

- Inicios de sesión.
- Intentos de acceso fallidos.
- Cambios de permisos.
- Creación o eliminación de usuarios.
- Ejecución de programas.
- Modificaciones importantes del sistema.

Cada evento queda almacenado junto con información adicional para facilitar su análisis.

---

### Información registrada

Un evento suele incluir:

- Fecha y hora.
- Usuario.
- Equipo.
- Proceso implicado.
- Recurso afectado.
- Acción realizada.
- Resultado (correcto o error).

Ejemplo:

```text
Fecha: 15/07/2026 10:42

Usuario: beatriz

Evento: Inicio de sesión

Resultado: Correcto
```

---

### Tipos de eventos

Los registros de seguridad pueden contener información sobre:

- Autenticación.
- Autorización.
- Accesos a archivos.
- Cambios de configuración.
- Instalación de software.
- Servicios.
- Procesos.
- Red.

Cada sistema operativo organiza estos eventos de forma distinta.

---

### Registros en Linux

Linux dispone de varios registros relacionados con la seguridad.

Algunos de los más habituales son:

| Archivo | Contenido |
|----------|-----------|
| `/var/log/auth.log` | Autenticación (Debian/Ubuntu). |
| `/var/log/secure` | Autenticación (RHEL, Rocky, AlmaLinux). |
| `/var/log/syslog` | Eventos generales del sistema. |
| `/var/log/messages` | Eventos generales (según la distribución). |
| `journalctl` | Registro centralizado mediante systemd. |

La ubicación puede variar según la distribución utilizada.

---

### journalctl

En sistemas con **systemd**, gran parte de la información puede consultarse mediante:

```bash
journalctl
```

Mostrar únicamente los errores:

```bash
journalctl -p err
```

Mostrar los registros desde el último arranque:

```bash
journalctl -b
```

Seguir los eventos en tiempo real:

```bash
journalctl -f
```

---

### Registros en Windows

Windows almacena los eventos mediante el **Visor de eventos**.

Los registros principales son:

- Aplicación.
- Sistema.
- Seguridad.
- Configuración.
- Reenvío de eventos.

El registro más importante para auditoría suele ser el de **Seguridad**.

---

### Visor de eventos

Puede abrirse mediante:

```text
eventvwr.msc
```

o desde:

```text
Herramientas administrativas

↓

Visor de eventos
```

Permite filtrar, buscar y exportar eventos para su análisis.

---

### Identificadores de evento (Event ID)

Cada evento de Windows dispone de un identificador numérico.

Algunos ejemplos habituales son:

| Event ID | Descripción |
|-----------|-------------|
| 4624 | Inicio de sesión correcto |
| 4625 | Inicio de sesión fallido |
| 4634 | Cierre de sesión |
| 4720 | Creación de usuario |
| 4726 | Eliminación de usuario |
| 4732 | Usuario añadido a un grupo |

Estos identificadores facilitan la búsqueda de eventos concretos.

---

### ¿Qué revisar?

Durante una revisión de seguridad conviene prestar atención a:

- Múltiples intentos de inicio de sesión fallidos.
- Accesos fuera del horario habitual.
- Creación de cuentas inesperadas.
- Cambios de permisos.
- Instalación de software no autorizada.
- Reinicios inesperados de servicios.
- Errores repetitivos.

La combinación de varios eventos puede indicar un incidente de seguridad.

---

### Conservación de registros

Los registros no deben conservarse indefinidamente.

Es recomendable definir:

- Tiempo de retención.
- Tamaño máximo.
- Rotación de archivos.
- Copias de seguridad.
- Almacenamiento centralizado cuando sea necesario.

Esto evita la pérdida de información importante y facilita su gestión.

---

### Protección de los registros

Los registros deben protegerse frente a modificaciones o eliminaciones no autorizadas.

Recomendaciones:

- Limitar el acceso.
- Utilizar permisos adecuados.
- Realizar copias de seguridad.
- Centralizar los registros en servidores específicos cuando sea posible.

Si un atacante modifica los registros, la investigación posterior será mucho más difícil.

---

### Correlación de eventos

En muchas ocasiones un único evento no proporciona suficiente información.

Es recomendable analizar varios eventos relacionados.

Ejemplo:

```text
Inicio de sesión fallido

↓

Inicio correcto

↓

Elevación de privilegios

↓

Creación de usuario

↓

Cambio de permisos
```

Analizar la secuencia completa facilita comprender lo sucedido.

---

### Comparativa

| Linux | Windows |
|--------|----------|
| `journalctl` | Visor de eventos |
| `/var/log/auth.log` | Registro de Seguridad |
| `/var/log/secure` | Event ID |
| `syslog` | Registros del sistema |

---

### Buenas prácticas

- Revisa periódicamente los registros de seguridad.
- Configura la rotación y conservación de los registros para evitar su pérdida.
- Protege los archivos de registro frente a modificaciones no autorizadas.
- Sincroniza la hora de todos los equipos mediante NTP para mantener una línea temporal coherente.
- Filtra y prioriza los eventos relevantes para evitar el exceso de información.
- Automatiza el análisis cuando el volumen de registros sea elevado.
- Conserva los registros durante el tiempo establecido por la organización o la normativa aplicable.

---

[⬆️ Volver al índice](#índice)

## Control de acceso

El **control de acceso** es el conjunto de mecanismos que determinan qué usuarios o procesos pueden acceder a un recurso y qué acciones están autorizados a realizar.

Su objetivo es garantizar que únicamente las personas o aplicaciones autorizadas puedan utilizar la información y los recursos del sistema.

Es uno de los principios fundamentales de la seguridad informática y está presente tanto en Linux como en Windows.

---

### ¿Qué es el control de acceso?

El control de acceso consiste en verificar si un usuario o proceso tiene permiso para realizar una determinada acción.

Por ejemplo:

- Leer un archivo.
- Modificar una carpeta.
- Ejecutar una aplicación.
- Administrar un servicio.
- Acceder a un recurso compartido.
- Conectarse a un servidor.

No basta con conocer la identidad del usuario; también es necesario comprobar sus permisos.

---

### Objetivos

El control de acceso permite:

- Proteger la información.
- Evitar modificaciones no autorizadas.
- Limitar el uso de recursos.
- Reducir el riesgo de errores.
- Impedir accesos indebidos.

Su finalidad es garantizar la **confidencialidad**, la **integridad** y la **disponibilidad** de los recursos.

---

### Elementos del control de acceso

Todo sistema de control de acceso se basa en tres elementos:

- **Sujeto:** quien solicita el acceso (usuario, grupo o proceso).
- **Objeto:** recurso al que se desea acceder (archivo, carpeta, servicio, impresora, etc.).
- **Permisos:** acciones autorizadas sobre ese recurso.

Ejemplo:

```text
Usuario

↓

Archivo

↓

Lectura
```

---

### Tipos de permisos

Los permisos más habituales son:

- Lectura.
- Escritura.
- Ejecución.
- Modificación.
- Eliminación.
- Control total.

Cada recurso puede tener una combinación distinta de permisos.

---

### Principio de mínimo privilegio

Una de las reglas más importantes consiste en conceder únicamente los permisos necesarios.

Ejemplo:

```text
Usuario

↓

Solo lectura
```

En lugar de:

```text
Usuario

↓

Control total
```

Reducir los privilegios limita el impacto de errores y posibles ataques.

---

### Control de acceso en Linux

Linux utiliza un sistema basado principalmente en:

- Propietario.
- Grupo.
- Otros usuarios.

Cada uno puede disponer de permisos de:

- Lectura (r).
- Escritura (w).
- Ejecución (x).

Ejemplo:

```text
-rwxr-x---
```

Este modelo resulta sencillo y eficiente para la mayoría de situaciones.

---

### ACL (Access Control Lists)

Cuando los permisos tradicionales no son suficientes, Linux permite utilizar **Listas de Control de Acceso (ACL)**.

Las ACL permiten asignar permisos específicos a usuarios o grupos adicionales sin modificar el propietario o el grupo principal del archivo.

Resultan especialmente útiles en entornos con múltiples usuarios.

---

### Control de acceso en Windows

Windows utiliza **ACL (Access Control Lists)** como mecanismo principal de autorización.

Cada recurso puede definir permisos específicos para:

- Usuarios.
- Grupos.
- Cuentas del sistema.

Entre los permisos más habituales se encuentran:

- Lectura.
- Escritura.
- Modificación.
- Lectura y ejecución.
- Control total.

---

### Herencia de permisos

Muchos sistemas permiten heredar permisos desde un recurso superior.

Ejemplo:

```text
Carpeta

↓

Subcarpeta

↓

Archivo
```

Si la herencia está habilitada, los permisos de la carpeta pueden aplicarse automáticamente a su contenido.

Esto simplifica la administración de grandes estructuras de directorios.

---

### Permisos explícitos e heredados

Los permisos pueden ser:

- **Explícitos:** asignados directamente al recurso.
- **Heredados:** recibidos desde un recurso superior.

Es importante diferenciarlos para comprender el origen de cada permiso y evitar configuraciones inesperadas.

---

### Acceso denegado

Un acceso puede rechazarse por diversos motivos:

- Usuario sin permisos.
- Grupo incorrecto.
- Recurso inexistente.
- Credenciales inválidas.
- Restricciones de seguridad.

El sistema operativo registrará normalmente este tipo de eventos en los registros de seguridad.

---

### Gestión mediante grupos

En lugar de asignar permisos individualmente a cada usuario, es recomendable utilizar grupos.

Ejemplo:

```text
Grupo RRHH

↓

Carpeta Recursos Humanos

↓

Lectura y escritura
```

Cuando un nuevo empleado se incorpora, basta con añadirlo al grupo correspondiente.

Esto facilita enormemente la administración.

---

### Riesgos de una mala configuración

Una configuración incorrecta puede provocar:

- Acceso no autorizado a información sensible.
- Modificación accidental de archivos.
- Eliminación de datos importantes.
- Escalada de privilegios.
- Dificultades para administrar permisos.

Por ello es importante revisar periódicamente la configuración de acceso.

---

### Comparativa

| Linux | Windows |
|--------|----------|
| Propietario | Usuario |
| Grupo | Grupo |
| Otros | Usuarios específicos |
| Permisos rwx | ACL |
| ACL opcionales | ACL integradas |

---

### Buenas prácticas

- Aplica siempre el principio de mínimo privilegio.
- Asigna permisos preferentemente mediante grupos en lugar de usuarios individuales.
- Revisa periódicamente los permisos de archivos y carpetas.
- Elimina permisos que ya no sean necesarios.
- Evita conceder control total salvo cuando sea imprescindible.
- Mantén habilitada la herencia únicamente cuando simplifique la administración y no comprometa la seguridad.
- Audita los accesos a recursos sensibles para detectar actividades no autorizadas.
- Documenta los cambios importantes relacionados con permisos y accesos.

---

[⬆️ Volver al índice](#índice)

## Autenticación y autorización

Aunque suelen utilizarse conjuntamente, **autenticación** y **autorización** son dos conceptos diferentes dentro de la seguridad informática.

La autenticación responde a la pregunta:

> **¿Quién eres?**

La autorización responde a:

> **¿Qué puedes hacer?**

Comprender esta diferencia es fundamental para administrar correctamente usuarios, permisos y recursos tanto en Linux como en Windows.

---

### ¿Qué es la autenticación?

La autenticación es el proceso mediante el cual el sistema verifica la identidad de un usuario, dispositivo o aplicación.

Su objetivo es confirmar que quien intenta acceder es realmente quien dice ser.

Solo después de autenticarse correctamente podrá acceder al sistema.

---

### Métodos de autenticación

Existen diferentes formas de autenticar a un usuario.

Las más habituales son:

- Usuario y contraseña.
- Certificados digitales.
- Claves SSH.
- Tarjetas inteligentes.
- Huella dactilar.
- Reconocimiento facial.
- Autenticación multifactor (MFA).

Cada organización selecciona el método más adecuado según sus necesidades.

---

### Factores de autenticación

Los métodos de autenticación suelen clasificarse en tres factores principales.

### Algo que sabes

Información conocida únicamente por el usuario.

Ejemplos:

- Contraseña.
- PIN.
- Pregunta secreta.

---

### Algo que tienes

Elemento físico que posee el usuario.

Ejemplos:

- Teléfono móvil.
- Token de seguridad.
- Tarjeta inteligente.
- Llave de seguridad USB.

---

### Algo que eres

Características biométricas del usuario.

Ejemplos:

- Huella dactilar.
- Iris.
- Rostro.
- Voz.

---

### Autenticación multifactor (MFA)

La autenticación multifactor combina dos o más factores distintos.

Ejemplo:

```text
Usuario

↓

Contraseña

↓

Código enviado al móvil

↓

Acceso concedido
```

El uso de MFA aumenta significativamente la seguridad frente al robo de credenciales.

---

### ¿Qué es la autorización?

Una vez autenticado el usuario, el sistema debe determinar qué acciones puede realizar.

Este proceso recibe el nombre de **autorización**.

La autorización controla aspectos como:

- Archivos accesibles.
- Carpetas disponibles.
- Aplicaciones permitidas.
- Servicios administrables.
- Recursos compartidos.

Dos usuarios autenticados correctamente pueden disponer de permisos completamente diferentes.

---

### Relación entre autenticación y autorización

El proceso habitual es:

```text
Usuario

↓

Autenticación

↓

Identidad verificada

↓

Autorización

↓

Permisos asignados
```

La autorización nunca debería producirse sin una autenticación previa.

---

### Autenticación en Linux

Linux admite distintos mecanismos de autenticación.

Los más habituales son:

- Usuario y contraseña.
- Claves SSH.
- PAM (Pluggable Authentication Modules).
- LDAP.
- Kerberos.

En servidores suele recomendarse el uso de claves SSH en lugar de contraseñas para el acceso remoto.

---

### PAM (Pluggable Authentication Modules)

PAM permite centralizar y modular los mecanismos de autenticación.

Gracias a PAM es posible:

- Establecer políticas de contraseñas.
- Configurar bloqueo de cuentas.
- Integrar autenticación biométrica.
- Utilizar autenticación multifactor.
- Integrar directorios corporativos.

Muchos servicios del sistema utilizan PAM para validar usuarios.

---

### Autenticación en Windows

Windows utiliza distintos mecanismos según el entorno.

Los principales son:

- Usuario y contraseña.
- Windows Hello.
- Tarjetas inteligentes.
- Certificados.
- Active Directory.
- Microsoft Entra ID (Azure AD).

En entornos empresariales, Active Directory suele centralizar la autenticación de usuarios y equipos.

---

### Autorización mediante permisos

Una vez autenticado, el sistema consulta los permisos asignados.

Estos permisos pueden depender de:

- Usuario.
- Grupo.
- Rol.
- ACL (Listas de Control de Acceso).

El resultado determinará las acciones permitidas sobre cada recurso.

---

### Roles

En muchas organizaciones se asignan permisos mediante **roles**.

Ejemplo:

```text
Administrador

↓

Control total
```

```text
Técnico

↓

Administración limitada
```

```text
Usuario

↓

Uso básico
```

Este enfoque simplifica la administración y reduce errores.

---

### Errores habituales

Algunos problemas frecuentes son:

- Contraseñas débiles.
- Reutilización de credenciales.
- Ausencia de MFA.
- Permisos excesivos.
- Cuentas compartidas.
- Usuarios con privilegios innecesarios.
- Cuentas que permanecen activas tras dejar de utilizarse.

---

### Comparativa

| Autenticación | Autorización |
|---------------|--------------|
| Verifica la identidad | Determina los permisos |
| Se realiza primero | Se realiza después |
| Usuario y contraseña | Permisos y ACL |
| Claves SSH | Roles |
| MFA | Grupos |

---

### Buenas prácticas

- Utiliza contraseñas robustas y únicas.
- Habilita la autenticación multifactor siempre que sea posible.
- Evita compartir cuentas entre varios usuarios.
- Aplica el principio de mínimo privilegio al asignar permisos.
- Revisa periódicamente los permisos y roles de los usuarios.
- Deshabilita o elimina las cuentas que ya no sean necesarias.
- Registra los intentos de autenticación y los accesos a recursos sensibles.
- Documenta las políticas de autenticación y autorización de la organización.

---

[⬆️ Volver al índice](#índice)

## Políticas de seguridad

Las **políticas de seguridad** son un conjunto de normas, procedimientos y directrices que establecen cómo deben protegerse los sistemas, los datos y los recursos de una organización.

Su finalidad es reducir riesgos, unificar criterios de actuación y garantizar que todos los usuarios y administradores sigan unas mismas reglas de seguridad.

Una política bien definida ayuda tanto a prevenir incidentes como a responder adecuadamente cuando estos se producen.

---

##### ¿Qué es una política de seguridad?

Una política de seguridad es un documento que define:

- Qué debe protegerse.
- Frente a qué amenazas.
- Quién es responsable.
- Qué medidas deben aplicarse.
- Qué acciones están permitidas o prohibidas.

Debe ser conocida por todos los usuarios de la organización.

---

### Objetivos

Las políticas de seguridad permiten:

- Proteger la información.
- Reducir el riesgo de incidentes.
- Definir responsabilidades.
- Cumplir requisitos legales y normativos.
- Establecer procedimientos comunes.
- Facilitar auditorías.

No sustituyen a las medidas técnicas, sino que las complementan.

---

### Alcance

Una política puede aplicarse a:

- Usuarios.
- Equipos.
- Servidores.
- Redes.
- Aplicaciones.
- Dispositivos móviles.
- Servicios en la nube.

Es importante definir claramente qué sistemas quedan incluidos.

---

### Políticas habituales

Entre las más comunes se encuentran:

- Política de contraseñas.
- Política de cuentas de usuario.
- Política de actualizaciones.
- Política de copias de seguridad.
- Política de acceso remoto.
- Política de uso aceptable.
- Política de gestión de incidentes.

Cada organización puede definir políticas adicionales según sus necesidades.

---

### Política de contraseñas

Debe establecer aspectos como:

- Longitud mínima.
- Complejidad.
- Caducidad.
- Historial de contraseñas.
- Número máximo de intentos fallidos.

Ejemplo:

```text
Longitud mínima

↓

12 caracteres
```

Una política adecuada reduce el riesgo de ataques por fuerza bruta o credenciales débiles.

---

### Política de cuentas

Debe definir:

- Creación de usuarios.
- Modificación de permisos.
- Bloqueo de cuentas.
- Eliminación de usuarios inactivos.
- Gestión de cuentas privilegiadas.

El objetivo es mantener un control adecuado sobre las identidades que acceden al sistema.

---

### Política de actualizaciones

Debe indicar:

- Frecuencia de actualización.
- Procedimiento de pruebas.
- Instalación de parches críticos.
- Gestión de actualizaciones de emergencia.

Mantener el software actualizado reduce la exposición a vulnerabilidades conocidas.

---

### Política de copias de seguridad

Debe responder a cuestiones como:

- Qué información se copia.
- Con qué frecuencia.
- Dónde se almacenan las copias.
- Cuánto tiempo se conservan.
- Cómo se restauran.

Una copia de seguridad que nunca se ha probado puede no ser útil cuando realmente se necesite.

---

### Política de acceso remoto

Cuando los usuarios acceden desde fuera de la organización, conviene definir:

- Métodos de autenticación.
- Uso de VPN.
- Equipos autorizados.
- Restricciones de acceso.
- Registro de conexiones.

El acceso remoto suele ser uno de los puntos más sensibles desde el punto de vista de la seguridad.

---

### Política de uso aceptable

Establece qué usos están permitidos y cuáles no.

Por ejemplo:

Permitido:

- Utilizar el correo corporativo para fines laborales.
- Acceder a aplicaciones autorizadas.

No permitido:

- Instalar software sin autorización.
- Compartir credenciales.
- Utilizar dispositivos no autorizados.
- Acceder a contenido prohibido por la organización.

---

### Política de respuesta ante incidentes

Debe definir:

- Cómo identificar un incidente.
- A quién comunicarlo.
- Qué medidas iniciales aplicar.
- Cómo registrar la información.
- Quién coordina la respuesta.

Disponer de un procedimiento claro reduce el tiempo de actuación.

---

### Revisión de las políticas

Las políticas no deben permanecer invariables.

Es recomendable revisarlas:

- Tras cambios importantes en la infraestructura.
- Cuando aparezcan nuevas amenazas.
- Después de un incidente de seguridad.
- De forma periódica.

Las necesidades de una organización evolucionan con el tiempo.

---

### Cumplimiento

Una política solo resulta útil si realmente se aplica.

Para ello es recomendable:

- Formar a los usuarios.
- Supervisar su cumplimiento.
- Realizar auditorías.
- Actualizar la documentación.

Las políticas deben ser conocidas y comprendidas por todo el personal.

---

### Comparativa

| Política | Finalidad |
|-----------|-----------|
| Contraseñas | Proteger las credenciales |
| Cuentas | Gestionar identidades |
| Actualizaciones | Corregir vulnerabilidades |
| Copias de seguridad | Garantizar la recuperación de datos |
| Acceso remoto | Proteger conexiones externas |
| Uso aceptable | Regular el uso de los recursos |
| Respuesta ante incidentes | Actuar correctamente ante un incidente |

---

### Buenas prácticas

- Define políticas claras, sencillas y fáciles de aplicar.
- Adapta las políticas al tamaño y necesidades de la organización.
- Revisa y actualiza la documentación periódicamente.
- Forma a los usuarios sobre las normas de seguridad.
- Aplica el principio de mínimo privilegio en todas las políticas relacionadas con permisos.
- Supervisa el cumplimiento mediante auditorías y revisiones periódicas.
- Documenta las excepciones y autorízalas únicamente cuando exista una necesidad justificada.

---

[⬆️ Volver al índice](#índice)

## Hardening del sistema

El **hardening** consiste en aplicar un conjunto de medidas destinadas a reducir la superficie de ataque de un sistema operativo, un servidor o una aplicación.

Su objetivo es minimizar las posibilidades de que un atacante pueda aprovechar una configuración insegura, un servicio innecesario o una vulnerabilidad para comprometer el sistema.

El hardening no elimina todos los riesgos, pero dificulta considerablemente un ataque.

---

### ¿Qué es el hardening?

El hardening consiste en reforzar la seguridad de un sistema mediante cambios de configuración y buenas prácticas.

Algunas de estas medidas son:

- Eliminar servicios innecesarios.
- Configurar correctamente los permisos.
- Mantener el sistema actualizado.
- Limitar los accesos.
- Aplicar políticas de seguridad.
- Reducir la exposición a la red.

Su finalidad es reducir al máximo la superficie de ataque.

---

### Objetivos

El hardening permite:

- Reducir vulnerabilidades.
- Limitar el impacto de un ataque.
- Mejorar la seguridad del sistema.
- Cumplir políticas y normativas.
- Facilitar la administración segura.

Debe realizarse antes de poner un sistema en producción.

---

### Reducir la superficie de ataque

Cada componente instalado representa una posible vía de ataque.

Es recomendable:

- Desinstalar software innecesario.
- Deshabilitar servicios que no se utilicen.
- Cerrar puertos que no sean necesarios.
- Eliminar cuentas sin uso.

Cuantos menos componentes existan, menor será el riesgo.

---

### Actualizaciones

Mantener el sistema actualizado es una de las medidas de hardening más importantes.

Debe actualizarse:

- Sistema operativo.
- Aplicaciones.
- Servicios.
- Bibliotecas.
- Firmware cuando proceda.

Las actualizaciones corrigen errores y vulnerabilidades conocidas.

---

### Configuración segura

Es recomendable revisar la configuración predeterminada del sistema.

Algunos ejemplos:

- Cambiar contraseñas por defecto.
- Deshabilitar cuentas innecesarias.
- Revisar permisos.
- Configurar correctamente los servicios.
- Limitar el acceso remoto.

La configuración inicial rara vez es la más segura.

---

### Gestión de servicios

Solo deberían permanecer activos los servicios imprescindibles.

Antes de mantener un servicio en ejecución conviene preguntarse:

- ¿Es necesario?
- ¿Quién lo utiliza?
- ¿Está expuesto a la red?
- ¿Puede sustituirse por una alternativa más segura?

Reducir el número de servicios disminuye la superficie de ataque.

---

### Gestión de usuarios

Un sistema endurecido debe mantener un control estricto sobre las cuentas.

Recomendaciones:

- Eliminar cuentas obsoletas.
- Deshabilitar cuentas no utilizadas.
- Evitar cuentas compartidas.
- Aplicar el principio de mínimo privilegio.

Las cuentas privilegiadas deben revisarse periódicamente.

---

### Configuración de permisos

Los permisos deben limitarse a lo estrictamente necesario.

Ejemplos:

- Restringir el acceso a archivos sensibles.
- Proteger los archivos de configuración.
- Evitar permisos de escritura innecesarios.
- Revisar las ACL periódicamente.

Una mala configuración de permisos puede facilitar una escalada de privilegios.

---

### Protección de la red

El hardening también incluye medidas relacionadas con la conectividad.

Por ejemplo:

- Configurar el firewall.
- Cerrar puertos innecesarios.
- Restringir el acceso mediante listas de control.
- Utilizar protocolos cifrados.
- Deshabilitar protocolos inseguros.

No todos los servicios deben ser accesibles desde cualquier red.

---

### Auditoría y registros

Un sistema endurecido debe registrar los eventos importantes.

Es recomendable auditar:

- Inicios de sesión.
- Cambios de configuración.
- Accesos a recursos sensibles.
- Creación y eliminación de cuentas.
- Errores críticos.

Estos registros facilitan la detección e investigación de incidentes.

---

### Herramientas de hardening

Existen herramientas que ayudan a comprobar el nivel de seguridad de un sistema.

Algunas de las más conocidas son:

Linux:

- Lynis.
- OpenSCAP.

Windows:

- Microsoft Security Compliance Toolkit.
- Microsoft Defender.
- Baselines de seguridad de Microsoft.

Estas herramientas ayudan a detectar configuraciones inseguras y proponen mejoras.

---

### Listas de comprobación (Checklists)

Muchas organizaciones utilizan listas de comprobación para verificar que un sistema cumple unos requisitos mínimos de seguridad.

Ejemplos:

- Servicios innecesarios deshabilitados.
- Firewall configurado.
- Actualizaciones instaladas.
- Contraseñas robustas.
- Auditoría habilitada.
- Copias de seguridad configuradas.

Las checklists ayudan a mantener una configuración homogénea.

---

### Comparativa

| Sistema sin hardening | Sistema con hardening |
|------------------------|-----------------------|
| Muchos servicios activos | Solo los necesarios |
| Configuración por defecto | Configuración revisada |
| Puertos abiertos | Puertos mínimos |
| Permisos amplios | Mínimo privilegio |
| Actualizaciones pendientes | Sistema actualizado |
| Escasa auditoría | Auditoría configurada |

---

### Buenas prácticas

- Aplica el hardening antes de poner un sistema en producción.
- Elimina software y servicios que no sean necesarios.
- Mantén el sistema y las aplicaciones completamente actualizados.
- Cambia todas las credenciales predeterminadas.
- Configura correctamente el firewall y limita los puertos abiertos.
- Revisa periódicamente los permisos y las cuentas privilegiadas.
- Activa la auditoría y conserva los registros de seguridad.
- Utiliza herramientas de evaluación para verificar el nivel de endurecimiento.
- Documenta todas las modificaciones realizadas durante el proceso de hardening.

---

[⬆️ Volver al índice](#índice)

## Monitorización de seguridad

La **monitorización de seguridad** consiste en supervisar de forma continua la actividad de un sistema para detectar comportamientos anómalos, intentos de intrusión o posibles incidentes de seguridad.

Su objetivo es identificar amenazas lo antes posible para poder responder antes de que causen un impacto importante.

Mientras que la auditoría registra lo ocurrido, la monitorización permite detectar lo que está ocurriendo en tiempo real o casi en tiempo real.

---

### ¿Qué es la monitorización de seguridad?

La monitorización de seguridad recopila y analiza eventos generados por:

- Sistemas operativos.
- Servidores.
- Aplicaciones.
- Equipos de red.
- Firewalls.
- Antivirus.
- Sistemas de autenticación.

Toda esta información ayuda a identificar actividades sospechosas.

---

### Objetivos

La monitorización permite:

- Detectar accesos no autorizados.
- Identificar intentos de ataque.
- Detectar malware.
- Descubrir cambios no autorizados.
- Supervisar la actividad de usuarios privilegiados.
- Reducir el tiempo de respuesta ante incidentes.

Cuanto antes se detecte un problema, menor será su impacto.

---

### ¿Qué debe supervisarse?

Los elementos más importantes son:

- Inicios de sesión.
- Intentos fallidos de autenticación.
- Cambios de permisos.
- Creación de cuentas.
- Instalación de software.
- Ejecución de procesos.
- Reinicio de servicios.
- Cambios en la configuración.
- Tráfico de red.

No todos los eventos tienen la misma importancia, por lo que conviene priorizar aquellos relacionados con la seguridad.

---

### Indicadores de compromiso (IoC)

Durante la monitorización pueden detectarse **Indicadores de Compromiso (IoC)**.

Algunos ejemplos son:

- Múltiples intentos fallidos de inicio de sesión.
- Conexiones desde ubicaciones inusuales.
- Procesos desconocidos.
- Creación inesperada de usuarios.
- Comunicación con direcciones IP maliciosas.
- Modificaciones de archivos críticos.

Un único IoC no siempre confirma un ataque, pero varios relacionados pueden indicar una actividad maliciosa.

---

### Alertas

Las herramientas de monitorización pueden generar alertas cuando detectan determinados eventos.

Ejemplos:

```text
10 intentos fallidos

↓

Generar alerta
```

```text
Nuevo usuario administrador

↓

Generar alerta
```

```text
Servicio crítico detenido

↓

Notificación inmediata
```

Las alertas permiten actuar con rapidez sin necesidad de revisar continuamente los registros.

---

### Monitorización de usuarios

Es recomendable supervisar especialmente:

- Administradores.
- Cuentas de servicio.
- Usuarios privilegiados.
- Accesos remotos.

Estas cuentas representan un mayor riesgo si son comprometidas.

---

### Monitorización de integridad

Además de la actividad del sistema, también puede supervisarse la integridad de archivos importantes.

Por ejemplo:

- Archivos de configuración.
- Binarios del sistema.
- Certificados.
- Scripts de administración.

Si alguno cambia inesperadamente, el sistema puede generar una alerta.

---

### Herramientas habituales

Algunas herramientas utilizadas para monitorizar la seguridad son:

Linux:

- `auditd`
- `journalctl`
- `fail2ban`
- `osquery`

Windows:

- Visor de eventos.
- Microsoft Defender.
- Microsoft Defender for Endpoint.

En infraestructuras empresariales también es habitual utilizar:

- Wazuh.
- Splunk.
- Elastic Security.
- Microsoft Sentinel.
- QRadar.

Estas soluciones permiten centralizar la información de múltiples equipos.

---

### SIEM

Un **SIEM** (*Security Information and Event Management*) recopila eventos procedentes de distintos sistemas y los analiza de forma centralizada.

Permite:

- Correlacionar eventos.
- Detectar patrones sospechosos.
- Generar alertas.
- Facilitar investigaciones.

En organizaciones grandes suele ser una pieza fundamental de la monitorización de seguridad.

---

### Correlación de eventos

Una única actividad puede no resultar sospechosa.

Sin embargo, varias acciones relacionadas sí pueden indicar un incidente.

Ejemplo:

```text
Intentos fallidos

↓

Inicio de sesión correcto

↓

Creación de usuario

↓

Cambio de permisos

↓

Alerta
```

La correlación permite detectar patrones que pasarían desapercibidos si se analizaran los eventos de forma aislada.

---

### Monitorización continua

La monitorización debe realizarse de forma permanente.

Esto permite:

- Detectar amenazas rápidamente.
- Reducir el tiempo de respuesta.
- Obtener información histórica.
- Analizar tendencias.
- Mejorar la seguridad de la infraestructura.

No debe limitarse únicamente a revisar los registros cuando ocurre un problema.

---

### Comparativa

| Auditoría | Monitorización |
|------------|----------------|
| Registra eventos | Supervisa continuamente |
| Análisis posterior | Detección en tiempo real |
| Investigación | Prevención y respuesta |
| Registros | Alertas y supervisión |

Ambos procesos son complementarios y necesarios.

---

### Buenas prácticas

- Supervisa de forma continua los sistemas críticos.
- Configura alertas para eventos relevantes relacionados con la seguridad.
- Revisa periódicamente las cuentas con privilegios elevados.
- Centraliza los registros cuando existan múltiples servidores o equipos.
- Correlaciona eventos para detectar patrones de ataque.
- Ajusta los umbrales de alerta para reducir los falsos positivos.
- Conserva un historial suficiente para facilitar investigaciones posteriores.
- Documenta las alertas relevantes y las acciones realizadas.

---

[⬆️ Volver al índice](#índice)

## Respuesta ante incidentes

Un **incidente de seguridad** es cualquier evento que compromete o puede comprometer la confidencialidad, integridad o disponibilidad de los sistemas o de la información.

La **respuesta ante incidentes** consiste en aplicar un procedimiento organizado para detectar, contener, analizar y resolver estos eventos, reduciendo al máximo su impacto sobre la organización.

Disponer de un plan de respuesta permite actuar de forma rápida, coordinada y eficaz.

---

### ¿Qué es un incidente?

Un incidente de seguridad puede ser:

- Acceso no autorizado.
- Infección por malware.
- Robo de credenciales.
- Eliminación de información.
- Ataque de denegación de servicio (DoS).
- Fuga de datos.
- Compromiso de un servidor.

No todos los incidentes tienen la misma gravedad, pero todos deben tratarse siguiendo un procedimiento.

---

### Objetivos

La respuesta ante incidentes persigue varios objetivos:

- Reducir el impacto del incidente.
- Proteger la información.
- Recuperar los servicios afectados.
- Investigar las causas.
- Evitar que vuelva a producirse.

Una actuación rápida puede evitar daños mucho mayores.

---

### Fases de la respuesta

La mayoría de metodologías siguen un ciclo similar:

```text
Preparación

↓

Detección

↓

Análisis

↓

Contención

↓

Erradicación

↓

Recuperación

↓

Lecciones aprendidas
```

Cada fase tiene una finalidad concreta.

---

### 1. Preparación

Antes de que ocurra un incidente es recomendable disponer de:

- Procedimientos documentados.
- Personal formado.
- Copias de seguridad.
- Herramientas de monitorización.
- Inventario actualizado.
- Contactos de emergencia.

Una buena preparación facilita la respuesta posterior.

---

### 2. Detección

El incidente puede detectarse mediante:

- Alertas del sistema.
- Monitorización.
- Antivirus.
- Usuarios.
- Auditorías.
- Herramientas SIEM.

Cuanto antes se detecte, menor será el impacto.

---

### 3. Análisis

Una vez detectado el incidente debe determinarse:

- Qué ha ocurrido.
- Qué sistemas están afectados.
- Cuándo comenzó.
- Cómo se produjo.
- Qué información puede haberse visto comprometida.

No conviene actuar sin comprender previamente la situación.

---

### 4. Contención

El objetivo es impedir que el incidente continúe propagándose.

Algunas medidas son:

- Aislar un equipo de la red.
- Bloquear una cuenta.
- Detener un servicio comprometido.
- Bloquear una dirección IP.
- Deshabilitar accesos remotos.

La contención debe realizarse intentando minimizar el impacto sobre el resto de la infraestructura.

---

### 5. Erradicación

Consiste en eliminar la causa del incidente.

Ejemplos:

- Eliminar malware.
- Aplicar un parche.
- Corregir una configuración insegura.
- Cambiar credenciales comprometidas.
- Eliminar cuentas no autorizadas.

La erradicación debe realizarse únicamente cuando el incidente esté controlado.

---

### 6. Recuperación

Una vez eliminado el problema, se restauran los sistemas afectados.

Puede incluir:

- Restauración desde copias de seguridad.
- Reinicio de servicios.
- Reincorporación de equipos a la red.
- Verificación del funcionamiento.
- Supervisión reforzada.

Antes de considerar finalizado el incidente debe comprobarse que el sistema funciona correctamente.

---

### 7. Lecciones aprendidas

Tras resolver el incidente es recomendable analizar:

- Qué ocurrió.
- Qué falló.
- Qué funcionó correctamente.
- Cómo mejorar la respuesta.
- Qué medidas preventivas deben implantarse.

Esta fase ayuda a fortalecer la seguridad de la organización.

---

### Conservación de evidencias

Durante la investigación es importante preservar las evidencias.

Ejemplos:

- Registros.
- Archivos de configuración.
- Capturas de memoria (cuando proceda).
- Copias de discos.
- Eventos del sistema.

Modificar o eliminar información puede dificultar el análisis posterior.

---

### Comunicación

Dependiendo del incidente, puede ser necesario informar a:

- Administradores.
- Dirección.
- Usuarios afectados.
- Equipo de respuesta.
- Autoridades competentes, cuando la legislación lo requiera.

La comunicación debe ser clara, documentada y realizada por las personas autorizadas.

---

### Documentación

Todo incidente debería registrarse.

La documentación suele incluir:

- Fecha y hora.
- Sistemas afectados.
- Descripción del incidente.
- Acciones realizadas.
- Responsable.
- Resultado.
- Medidas preventivas adoptadas.

Esta información resulta muy útil para futuras investigaciones y auditorías.

---

### Comparativa

| Fase | Objetivo |
|------|----------|
| Preparación | Estar preparado antes del incidente |
| Detección | Identificar el problema |
| Análisis | Comprender el incidente |
| Contención | Evitar su propagación |
| Erradicación | Eliminar la causa |
| Recuperación | Restaurar los servicios |
| Lecciones aprendidas | Mejorar la respuesta futura |

---

### Buenas prácticas

- Mantén un procedimiento de respuesta documentado y actualizado.
- Forma al personal para actuar correctamente ante un incidente.
- Actúa con rapidez, pero evita tomar decisiones precipitadas.
- Conserva las evidencias necesarias para el análisis.
- Documenta todas las acciones realizadas durante la respuesta.
- Revisa los registros y verifica que el incidente ha sido completamente erradicado.
- Analiza las causas y aplica medidas preventivas para evitar incidentes similares.
- Realiza simulacros periódicos para comprobar la eficacia del procedimiento.

---

[⬆️ Volver al índice](#índice)

## Buenas prácticas

La seguridad de un sistema no depende únicamente del software utilizado, sino también de la forma en que se administra.

Aplicar buenas prácticas reduce significativamente el riesgo de incidentes, facilita la detección de problemas y mejora la protección de la infraestructura frente a amenazas internas y externas.

Estas recomendaciones son aplicables tanto a estaciones de trabajo como a servidores Linux y Windows.

---

### Aplica el principio de mínimo privilegio

Concede a cada usuario únicamente los permisos necesarios para realizar su trabajo.

Evita:

- Cuentas con privilegios excesivos.
- Usuarios administradores innecesarios.
- Servicios ejecutándose como `root` o Administrador sin justificación.

Cuantos menos privilegios tenga una cuenta, menor será el impacto si resulta comprometida.

---

### Utiliza contraseñas robustas

Las contraseñas deben ser:

- Largas.
- Únicas.
- Difíciles de adivinar.
- Distintas para cada servicio.

Evita utilizar:

- Fechas de nacimiento.
- Nombres propios.
- Palabras del diccionario.
- Contraseñas reutilizadas.

Siempre que sea posible, utiliza un gestor de contraseñas.

---

### Habilita la autenticación multifactor

La autenticación multifactor (MFA) añade una capa adicional de seguridad.

Aunque un atacante obtenga la contraseña, necesitará un segundo factor para acceder.

Debe utilizarse especialmente en:

- Accesos remotos.
- Cuentas administrativas.
- Servicios en la nube.
- Correo corporativo.

---

### Mantén el sistema actualizado

Instala periódicamente las actualizaciones de:

- Sistema operativo.
- Aplicaciones.
- Servicios.
- Firmware.
- Controladores cuando sea necesario.

Las actualizaciones corrigen vulnerabilidades conocidas y mejoran la estabilidad del sistema.

---

### Deshabilita lo que no utilices

Elimina o deshabilita:

- Servicios innecesarios.
- Aplicaciones sin uso.
- Protocolos obsoletos.
- Puertos abiertos innecesariamente.
- Cuentas inactivas.

Reducir la superficie de ataque es una de las medidas de protección más eficaces.

---

### Revisa los registros

Consulta periódicamente los registros de seguridad para detectar:

- Intentos fallidos de autenticación.
- Cambios inesperados.
- Accesos fuera de horario.
- Errores repetitivos.
- Actividad sospechosa.

La revisión periódica permite identificar incidentes antes de que provoquen daños importantes.

---

### Realiza copias de seguridad

Mantén copias de seguridad periódicas de:

- Configuración.
- Bases de datos.
- Archivos críticos.
- Documentación.

Además, verifica regularmente que pueden restaurarse correctamente.

Una copia de seguridad que no puede recuperarse carece de utilidad.

---

### Protege el acceso remoto

Cuando un sistema sea accesible desde Internet:

- Utiliza VPN cuando sea posible.
- Habilita MFA.
- Limita las direcciones IP autorizadas.
- Utiliza protocolos cifrados.
- Supervisa las conexiones.

Evita exponer servicios innecesarios directamente a Internet.

---

### Documenta los cambios

Registra siempre:

- Cambios de configuración.
- Modificaciones de permisos.
- Instalación de software.
- Actualizaciones importantes.
- Incidentes de seguridad.

La documentación facilita el mantenimiento y las investigaciones posteriores.

---

### Supervisa continuamente

No esperes a que aparezca un problema.

Monitoriza:

- Servicios.
- Recursos.
- Usuarios.
- Registros.
- Red.
- Alertas de seguridad.

La monitorización continua reduce el tiempo necesario para detectar y responder a incidentes.

---

### Forma a los usuarios

Muchos incidentes tienen su origen en errores humanos.

Es recomendable formar a los usuarios sobre:

- Phishing.
- Gestión de contraseñas.
- Uso seguro del correo electrónico.
- Ingeniería social.
- Manejo de información sensible.

La concienciación es una de las mejores medidas preventivas.

---

### Realiza auditorías periódicas

Comprueba regularmente:

- Permisos.
- Usuarios.
- Servicios.
- Configuración.
- Registros.
- Políticas de seguridad.

Las auditorías permiten detectar configuraciones incorrectas antes de que sean explotadas.

---

### Planifica la respuesta ante incidentes

Todo sistema debería disponer de un procedimiento para actuar cuando ocurre un incidente.

Debe incluir:

- Personas responsables.
- Procedimientos.
- Contactos.
- Copias de seguridad.
- Documentación.

Una buena preparación reduce considerablemente el impacto de cualquier incidente.

---

### Resumen de recomendaciones

| Recomendación | Beneficio |
|---------------|-----------|
| Mínimo privilegio | Reduce el impacto de un compromiso |
| Contraseñas robustas | Protege las credenciales |
| MFA | Añade una capa adicional de seguridad |
| Actualizaciones | Corrigen vulnerabilidades |
| Deshabilitar servicios innecesarios | Reduce la superficie de ataque |
| Revisar registros | Detecta actividades sospechosas |
| Copias de seguridad | Facilita la recuperación |
| Documentar cambios | Mejora la trazabilidad |
| Monitorización continua | Reduce el tiempo de detección |
| Formación de usuarios | Disminuye el riesgo de errores humanos |

---

### Errores habituales

Algunas prácticas que deben evitarse son:

- Utilizar cuentas administrativas para tareas cotidianas.
- Reutilizar contraseñas en distintos servicios.
- Ignorar las actualizaciones de seguridad.
- No revisar los registros del sistema.
- Mantener servicios innecesarios activos.
- Compartir cuentas entre varios usuarios.
- No documentar cambios importantes.
- No comprobar periódicamente las copias de seguridad.

---

[⬆️ Volver al índice](#índice)