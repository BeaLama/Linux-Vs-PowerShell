# Administración de Windows

## Introducción

Microsoft Windows es uno de los sistemas operativos más utilizados en entornos empresariales, tanto en estaciones de trabajo como en servidores. Su administración comprende la gestión de usuarios, servicios, almacenamiento, redes, políticas de seguridad y herramientas de automatización, permitiendo mantener los equipos seguros, estables y correctamente configurados.

En este capítulo se estudiarán los principales aspectos relacionados con la administración de sistemas Windows, incluyendo las herramientas más utilizadas por los administradores para gestionar equipos y servidores en infraestructuras empresariales.

## Índice

- [Arquitectura básica de Windows](#arquitectura-básica-de-windows)
- [Sistema de archivos en Windows](#sistema-de-archivos-en-windows)
- [Gestión de usuarios y grupos](#gestión-de-usuarios-y-grupos)
- [Gestión de permisos NTFS](#gestión-de-permisos-ntfs)
- [Administración de procesos](#administración-de-procesos)
- [Administración de servicios](#administración-de-servicios)
- [Administración del almacenamiento](#administración-del-almacenamiento)
- [Administración de red](#administración-de-red)
- [Registro de Windows](#registro-de-windows)
- [Administración remota](#administración-remota)

---

## Arquitectura básica de Windows

Introducción

Microsoft Windows es un sistema operativo diseñado para proporcionar una interfaz gráfica intuitiva y una administración eficiente de los recursos del equipo. Su arquitectura está formada por distintos componentes que trabajan conjuntamente para permitir la ejecución de aplicaciones, la gestión del hardware y la comunicación entre los usuarios y el sistema operativo.

Comprender la arquitectura de Windows permite al administrador diagnosticar problemas, optimizar el rendimiento y realizar tareas de mantenimiento de forma más eficaz.

---

### Componentes principales

La arquitectura de Windows está formada por varios elementos fundamentales.

Los principales son:

- Hardware.
- Kernel.
- Servicios del sistema.
- Subsistemas de Windows.
- Aplicaciones de usuario.

Cada componente desempeña una función específica dentro del sistema operativo.

---

### Arquitectura general

La relación entre los distintos componentes puede representarse de la siguiente forma:

```text
Aplicaciones

↓

Subsistemas de Windows

↓

Servicios del sistema

↓

Kernel

↓

Hardware
```

El kernel actúa como intermediario entre el software y el hardware del equipo.

---

### Hardware

El hardware corresponde a todos los componentes físicos del equipo.

Incluye elementos como:

- Procesador (CPU).
- Memoria RAM.
- Discos.
- Tarjetas de red.
- Dispositivos USB.
- Tarjetas gráficas.

Windows administra estos recursos mediante controladores (*drivers*).

---

### Kernel

El **kernel** es el núcleo del sistema operativo.

Entre sus principales funciones destacan:

- Gestión de procesos.
- Administración de memoria.
- Control de dispositivos.
- Gestión del sistema de archivos.
- Planificación de tareas.
- Comunicación con el hardware.

El kernel trabaja continuamente para garantizar el funcionamiento estable del sistema.

---

### Servicios del sistema

Los servicios son programas que se ejecutan en segundo plano y proporcionan funciones esenciales.

Algunos ejemplos son:

- Servicio de impresión.
- Windows Update.
- Servicio DHCP.
- Servicio DNS.
- Registro de eventos.

Muchos servicios se inician automáticamente durante el arranque del sistema.

---

### Subsistemas de Windows

Los subsistemas permiten que las aplicaciones interactúen con el sistema operativo.

Entre sus funciones se encuentran:

- Gestión de ventanas.
- Entrada y salida.
- Acceso a archivos.
- Comunicación con el kernel.

Estos componentes facilitan la ejecución de aplicaciones de forma segura.

---

### Aplicaciones

Las aplicaciones son los programas utilizados por los usuarios para realizar diferentes tareas.

Por ejemplo:

- Navegadores web.
- Procesadores de texto.
- Herramientas de administración.
- Aplicaciones empresariales.
- Clientes de correo electrónico.

Todas ellas utilizan los servicios proporcionados por Windows para acceder al hardware.

---

### Comunicación entre componentes

El funcionamiento del sistema puede resumirse así:

```text
Usuario

↓

Aplicación

↓

Servicios del sistema

↓

Kernel

↓

Hardware

↓

Respuesta al usuario
```

Esta estructura permite que el acceso al hardware se realice de forma controlada y segura.

---

### Características de la arquitectura Windows

La arquitectura de Windows presenta diversas características.

Entre ellas:

- Interfaz gráfica integrada.
- Compatibilidad con una amplia variedad de hardware.
- Gestión multitarea.
- Soporte multiusuario.
- Integración con redes empresariales.
- Amplio ecosistema de aplicaciones.

Estas características convierten a Windows en uno de los sistemas operativos más utilizados en empresas y organizaciones.

---

### Ejemplo práctico

Un usuario abre una aplicación de gestión.

Proceso:

```text
Usuario

↓

Aplicación

↓

Servicios de Windows

↓

Kernel

↓

Hardware

↓

Resultado mostrado en pantalla
```

El kernel coordina el acceso a los recursos y devuelve la información necesaria para que la aplicación funcione correctamente.

---

[⬆️ Volver al índice](#índice)

## Sistema de archivos en Windows

Introducción

El sistema de archivos es el encargado de organizar, almacenar y gestionar toda la información contenida en los dispositivos de almacenamiento. En Windows, los archivos y directorios se estructuran mediante unidades identificadas por letras, lo que facilita el acceso a los distintos discos y particiones del sistema.

Conocer la organización del sistema de archivos permite localizar información, administrar el almacenamiento y mantener correctamente los equipos y servidores Windows.

---

### Unidades de almacenamiento

Windows identifica cada dispositivo mediante una letra de unidad.

Algunos ejemplos son:

```text
C:\

D:\

E:\
```

Cada unidad puede corresponder a:

- Un disco duro.
- Una partición.
- Una unidad SSD.
- Una memoria USB.
- Una unidad de red.

La unidad **C:** suele contener el sistema operativo.

---

### Estructura del sistema de archivos

La organización de archivos puede representarse mediante una estructura jerárquica.

```text
C:\

├── Windows
├── Program Files
├── Program Files (x86)
├── Users
├── ProgramData
└── Temp
```

Cada directorio tiene una finalidad específica dentro del sistema operativo.

---

### Carpeta Windows

La carpeta:

```text
C:\Windows
```

contiene los archivos esenciales del sistema operativo.

En ella se almacenan:

- Archivos del sistema.
- Bibliotecas DLL.
- Controladores.
- Herramientas administrativas.
- Componentes de Windows.

No se recomienda modificar su contenido salvo en tareas específicas de administración.

---

### Carpeta Program Files

La carpeta:

```text
C:\Program Files
```

almacena la mayoría de aplicaciones instaladas de 64 bits.

En sistemas de 64 bits también existe:

```text
C:\Program Files (x86)
```

que contiene las aplicaciones de 32 bits.

---

### Carpeta Users

La carpeta:

```text
C:\Users
```

contiene los perfiles de los usuarios.

Por ejemplo:

```text
C:\Users\Administrador

C:\Users\Juan

C:\Users\Maria
```

Cada perfil almacena documentos, configuraciones y datos personales del usuario.

---

### Carpeta ProgramData

La carpeta:

```text
C:\ProgramData
```

contiene información compartida por las aplicaciones para todos los usuarios del sistema.

Almacena, entre otros:

- Configuraciones comunes.
- Bases de datos locales.
- Archivos de funcionamiento interno.

Habitualmente permanece oculta para evitar modificaciones accidentales.

---

### Sistemas de archivos compatibles

Windows admite distintos sistemas de archivos.

Los más habituales son:

| Sistema de archivos | Uso principal |
|---------------------|---------------|
| NTFS | Sistema principal de Windows. |
| FAT32 | Compatibilidad con numerosos dispositivos. |
| exFAT | Memorias USB y discos externos. |
| ReFS | Entornos empresariales y servidores. |

Cada sistema presenta características diferentes según el uso previsto.

---

### Consultar el espacio disponible

El espacio de almacenamiento puede consultarse desde el Explorador de archivos o mediante PowerShell.

Ejemplo:

```powershell
Get-PSDrive
```

Este comando muestra:

- Unidad.
- Espacio utilizado.
- Espacio libre.

Resulta útil para supervisar el almacenamiento del sistema.

---

### Rutas de archivos

Windows utiliza rutas para localizar archivos y directorios.

Ejemplo:

```text
C:\Users\Administrador\Documents\Informe.docx
```

Cada elemento de la ruta identifica un directorio o archivo concreto dentro del sistema.

---

### Ejemplo práctico

Un administrador necesita localizar el perfil de un usuario.

Procedimiento:

```text
Acceder a C:\Users

↓

Localizar la carpeta del usuario

↓

Consultar los archivos necesarios

↓

Realizar la modificación correspondiente
```

Gracias a la organización del sistema de archivos, la localización de información resulta rápida y sencilla.

---

[⬆️ Volver al índice](#índice)

## Gestión de usuarios y grupos

Introducción

Windows permite administrar múltiples usuarios dentro de un mismo equipo o dominio, asignando permisos y recursos específicos a cada uno de ellos. La correcta gestión de usuarios y grupos resulta fundamental para mantener la seguridad del sistema y controlar el acceso a la información.

En entornos empresariales, estas tareas suelen realizarse tanto en equipos locales como mediante servicios de directorio como **Active Directory**.

---

### Usuarios en Windows

Un usuario representa una cuenta que permite acceder al sistema operativo.

Cada cuenta dispone de:

- Nombre de usuario.
- Contraseña.
- Identificador de seguridad (SID).
- Perfil de usuario.
- Permisos asociados.
- Configuración personal.

Esta información identifica de forma única a cada usuario del sistema.

---

### Tipos de usuarios

Windows distingue varios tipos de cuentas.

Las principales son:

- Administrador.
- Usuario estándar.
- Invitado.
- Cuentas de servicio.

Cada una posee distintos niveles de privilegios.

---

### Cuenta de administrador

La cuenta de administrador dispone de permisos elevados para realizar tareas de administración.

Entre sus funciones se encuentran:

- Instalar programas.
- Crear usuarios.
- Modificar configuraciones.
- Gestionar servicios.
- Administrar dispositivos.

Por motivos de seguridad, se recomienda utilizarla únicamente cuando sea necesario.

---

### Usuarios estándar

Los usuarios estándar están diseñados para el trabajo diario.

Normalmente pueden:

- Ejecutar aplicaciones.
- Crear documentos.
- Modificar sus propios archivos.
- Utilizar recursos autorizados.

Sin privilegios administrativos no pueden modificar la configuración global del sistema.

---

### Grupos

Los grupos permiten administrar permisos de forma conjunta.

Por ejemplo:

```text
Grupo: Soporte IT

↓

Usuario1

Usuario2

Usuario3
```

Asignando permisos al grupo, todos sus miembros heredan automáticamente dichos permisos.

---

### Herramientas de administración

En equipos Windows pueden administrarse usuarios mediante diferentes herramientas.

Algunas de las más utilizadas son:

- Administración de equipos.
- Usuarios y grupos locales.
- Panel de control.
- Configuración de Windows.
- PowerShell.

En servidores también es habitual utilizar **Active Directory Users and Computers**.

---

### Crear usuarios mediante PowerShell

Es posible crear usuarios locales utilizando PowerShell.

Ejemplo:

```powershell
New-LocalUser
```

Este comando permite automatizar la creación de cuentas en equipos Windows.

---

### Consultar usuarios

Para visualizar los usuarios locales puede utilizarse:

```powershell
Get-LocalUser
```

La información mostrada incluye:

- Nombre.
- Estado.
- Descripción.
- Último inicio de sesión (según disponibilidad).

Esta herramienta facilita las tareas de auditoría.

---

### Consultar grupos

Para mostrar los grupos locales:

```powershell
Get-LocalGroup
```

También es posible consultar los miembros de un grupo concreto.

Ejemplo:

```powershell
Get-LocalGroupMember Administrators
```

Esto permite verificar rápidamente qué usuarios pertenecen a cada grupo.

---

### Ejemplo práctico

Un nuevo empleado se incorpora a la empresa.

Procedimiento:

```text
Crear la cuenta

↓

Asignar contraseña

↓

Añadir al grupo correspondiente

↓

Comprobar los permisos

↓

Entregar las credenciales
```

Gracias a este procedimiento el usuario dispone únicamente de los permisos necesarios para desempeñar su trabajo.

---

[⬆️ Volver al índice](#índice)

## Gestión de permisos NTFS

Introducción

El sistema de archivos **NTFS (New Technology File System)** es el utilizado por defecto en las versiones actuales de Windows. Una de sus principales características es la posibilidad de asignar permisos detallados sobre archivos y carpetas, permitiendo controlar qué usuarios pueden acceder a la información y qué acciones pueden realizar.

La correcta administración de permisos NTFS resulta fundamental para proteger los datos y garantizar la seguridad en entornos empresariales.

---

### ¿Qué son los permisos NTFS?

Los permisos NTFS determinan las acciones que un usuario o grupo puede realizar sobre un archivo o carpeta.

Estos permisos permiten controlar el acceso de forma muy precisa y pueden aplicarse tanto a usuarios individuales como a grupos.

---

### Tipos de permisos básicos

Los permisos más habituales son:

| Permiso | Función |
|----------|---------|
| Control total | Permite realizar cualquier acción sobre el recurso. |
| Modificar | Permite leer, escribir y eliminar archivos. |
| Lectura y ejecución | Permite abrir y ejecutar archivos. |
| Mostrar contenido de carpeta | Permite visualizar el contenido de una carpeta. |
| Lectura | Permite visualizar el contenido sin modificarlo. |
| Escritura | Permite crear o modificar archivos. |

Estos permisos pueden combinarse según las necesidades de cada organización.

---

### Herencia de permisos

Una de las características más importantes de NTFS es la **herencia**.

Su funcionamiento puede representarse así:

```text
Carpeta principal

↓

Subcarpeta

↓

Archivo
```

Por defecto, los permisos asignados a una carpeta se heredan por las subcarpetas y archivos contenidos en ella.

La herencia facilita la administración de grandes estructuras de directorios.

---

### Propietario de un archivo

Cada archivo o carpeta posee un propietario.

El propietario puede:

- Modificar los permisos.
- Cambiar el propietario.
- Administrar el recurso.

En determinadas situaciones el administrador puede tomar posesión de un archivo para recuperar su control.

---

### Asignación de permisos

Los permisos pueden configurarse desde las propiedades del archivo o carpeta.

Proceso general:

```text
Seleccionar carpeta

↓

Propiedades

↓

Seguridad

↓

Editar permisos

↓

Aplicar cambios
```

Este procedimiento permite controlar el acceso a cada recurso.

---

### Permisos efectivos

Cuando un usuario pertenece a varios grupos, Windows calcula los **permisos efectivos**, que representan los permisos finales aplicables.

En general:

- Los permisos permitidos se combinan.
- Los permisos denegados tienen prioridad sobre los permitidos.

Es importante revisar los permisos efectivos cuando se diagnostican problemas de acceso.

---

### Compartición de carpetas

Cuando una carpeta se comparte en red intervienen dos tipos de permisos:

- Permisos NTFS.
- Permisos de uso compartido.

El acceso final dependerá de la combinación de ambos.

En caso de conflicto, se aplicará la configuración más restrictiva.

---

### Consultar permisos mediante PowerShell

PowerShell permite consultar los permisos asignados a un recurso.

Ejemplo:

```powershell
Get-Acl C:\Datos
```

Este comando muestra el propietario y la lista de permisos asociados a la carpeta.

Resulta especialmente útil para tareas de auditoría y automatización.

---

### Ejemplo práctico

Un departamento necesita acceder únicamente a una carpeta compartida.

Procedimiento:

```text
Crear grupo

↓

Asignar permisos NTFS

↓

Compartir la carpeta

↓

Comprobar el acceso

↓

Verificar permisos efectivos
```

Gracias a este procedimiento se garantiza que únicamente los usuarios autorizados puedan acceder a la información.

---

[⬆️ Volver al índice](#índice)

## Administración de procesos

Introducción

Un **proceso** es una instancia de un programa que se encuentra en ejecución. Cada vez que un usuario abre una aplicación o Windows inicia un servicio, el sistema crea uno o varios procesos para gestionar su funcionamiento. La administración de procesos permite supervisar el consumo de recursos, detectar aplicaciones bloqueadas y optimizar el rendimiento del equipo.

El conocimiento de estas herramientas resulta fundamental para cualquier administrador de sistemas Windows.

---

### ¿Qué es un proceso?

Un proceso representa un programa que está siendo ejecutado por el sistema operativo.

Cada proceso dispone de:

- Identificador de proceso (PID).
- Nombre.
- Usuario propietario.
- Estado.
- Consumo de CPU.
- Consumo de memoria.

Windows administra continuamente todos los procesos activos del sistema.

---

### Identificador del proceso (PID)

Cada proceso recibe un identificador único denominado **PID (Process ID)**.

El PID permite:

- Identificar un proceso.
- Supervisarlo.
- Finalizar su ejecución.
- Analizar su comportamiento.

No existen dos procesos activos con el mismo PID.

---

### Administrador de tareas

La herramienta gráfica más utilizada para gestionar procesos es el **Administrador de tareas**.

Permite visualizar:

- Procesos en ejecución.
- Consumo de CPU.
- Uso de memoria.
- Uso del disco.
- Actividad de red.

También permite finalizar aplicaciones que no responden.

---

### Consultar procesos desde la línea de comandos

Windows incorpora distintas herramientas para consultar los procesos activos.

Mediante CMD:

```cmd
tasklist
```

Este comando muestra todos los procesos actualmente en ejecución.

---

### Consultar procesos con PowerShell

PowerShell proporciona una administración más avanzada mediante:

```powershell
Get-Process
```

Este comando muestra información detallada sobre los procesos, incluyendo el uso de recursos.

---

### Finalizar procesos

Cuando una aplicación deja de responder puede finalizarse desde el Administrador de tareas o mediante línea de comandos.

Desde CMD:

```cmd
taskkill /PID 1234
```

También puede utilizarse:

```cmd
taskkill /IM notepad.exe
```

para finalizar un proceso indicando su nombre.

---

### Finalizar procesos con PowerShell

PowerShell permite detener procesos mediante:

```powershell
Stop-Process
```

Ejemplo:

```powershell
Stop-Process -Name notepad
```

o

```powershell
Stop-Process -Id 1234
```

Esta herramienta resulta especialmente útil para automatizar tareas administrativas.

---

### Prioridad de los procesos

Windows permite modificar la prioridad con la que un proceso utiliza el procesador.

Las prioridades habituales son:

- Tiempo real.
- Alta.
- Superior a la normal.
- Normal.
- Inferior a la normal.
- Baja.

Modificar la prioridad puede mejorar el rendimiento de determinadas aplicaciones, aunque debe hacerse con precaución.

---

### Supervisión del rendimiento

Además del Administrador de tareas, Windows incorpora herramientas como:

- Monitor de recursos.
- Monitor de rendimiento.

Estas aplicaciones permiten analizar:

- Uso del procesador.
- Memoria.
- Disco.
- Red.
- Procesos activos.

Son especialmente útiles para diagnosticar problemas de rendimiento.

---

### Ejemplo práctico

Un equipo presenta un uso excesivo del procesador.

Procedimiento:

```text
Abrir el Administrador de tareas

↓

Ordenar por uso de CPU

↓

Identificar el proceso responsable

↓

Analizar su funcionamiento

↓

Finalizar el proceso si es necesario

↓

Comprobar el rendimiento del sistema
```

Este procedimiento permite localizar rápidamente el origen del problema.

---

[⬆️ Volver al índice](#índice)

## Administración de servicios

Introducción

Los **servicios** son aplicaciones que se ejecutan en segundo plano y proporcionan funciones esenciales para el funcionamiento del sistema operativo y de otras aplicaciones. Muchos de ellos se inician automáticamente al arrancar Windows y permanecen activos sin intervención del usuario.

La correcta administración de los servicios permite mejorar el rendimiento, solucionar incidencias y aumentar la seguridad del sistema.

---

### ¿Qué es un servicio?

Un servicio es un programa que se ejecuta en segundo plano para proporcionar una determinada funcionalidad al sistema.

Algunos ejemplos son:

- Windows Update.
- Servicio DHCP.
- Cliente DNS.
- Cola de impresión.
- Registro de eventos.
- Servicio de Escritorio remoto.

Estos servicios pueden iniciarse automáticamente o bajo demanda.

---

### Tipos de inicio

Cada servicio puede configurarse con distintos modos de inicio.

Los principales son:

| Tipo de inicio | Descripción |
|----------------|-------------|
| Automático | Se inicia durante el arranque del sistema. |
| Automático (inicio retrasado) | Se inicia poco después del arranque para reducir la carga inicial. |
| Manual | Solo se inicia cuando es necesario. |
| Deshabilitado | No puede iniciarse hasta ser habilitado nuevamente. |

La elección del tipo de inicio depende de la función del servicio.

---

### Administrador de servicios

La herramienta gráfica utilizada para administrar servicios es:

```text
services.msc
```

Desde ella es posible:

- Consultar el estado de un servicio.
- Iniciarlo.
- Detenerlo.
- Reiniciarlo.
- Cambiar el tipo de inicio.
- Consultar sus propiedades.

Es una de las herramientas más utilizadas por los administradores de Windows.

---

### Consultar servicios mediante PowerShell

PowerShell permite listar los servicios instalados mediante:

```powershell
Get-Service
```

La información mostrada incluye:

- Nombre.
- Estado.
- Tipo de servicio.

Esta herramienta resulta muy útil para automatizar tareas administrativas.

---

### Iniciar un servicio

Para iniciar un servicio mediante PowerShell:

```powershell
Start-Service NombreServicio
```

Ejemplo:

```powershell
Start-Service Spooler
```

El servicio comenzará a ejecutarse inmediatamente.

---

### Detener un servicio

Para detener un servicio:

```powershell
Stop-Service NombreServicio
```

Ejemplo:

```powershell
Stop-Service Spooler
```

Debe comprobarse previamente que el servicio puede detenerse sin afectar al funcionamiento del sistema.

---

### Reiniciar un servicio

Cuando un servicio presenta problemas puede reiniciarse mediante:

```powershell
Restart-Service NombreServicio
```

El reinicio suele resolver incidencias temporales sin necesidad de reiniciar el equipo.

---

### Consultar un servicio específico

Es posible obtener información de un servicio concreto mediante:

```powershell
Get-Service NombreServicio
```

Ejemplo:

```powershell
Get-Service WinRM
```

Esto facilita la comprobación rápida de su estado.

---

### Dependencias de servicios

Algunos servicios dependen del funcionamiento de otros.

La relación puede representarse así:

```text
Servicio A

↓

Servicio B

↓

Servicio C
```

Si un servicio esencial no está disponible, los servicios dependientes pueden dejar de funcionar correctamente.

---

### Ejemplo práctico

Una impresora deja de funcionar correctamente.

Procedimiento:

```text
Abrir services.msc

↓

Localizar el servicio Cola de impresión

↓

Comprobar su estado

↓

Reiniciar el servicio

↓

Verificar el funcionamiento de la impresora
```

En muchas ocasiones, reiniciar el servicio resuelve la incidencia sin necesidad de reiniciar el equipo.

---

[⬆️ Volver al índice](#índice)

## Administración del almacenamiento

Introducción

La administración del almacenamiento en Windows comprende la gestión de discos, particiones, volúmenes y sistemas de archivos. Una correcta organización del almacenamiento permite mejorar el rendimiento del sistema, garantizar la disponibilidad de los datos y facilitar las tareas de mantenimiento y recuperación.

Windows incorpora diversas herramientas gráficas y de línea de comandos para supervisar y administrar los dispositivos de almacenamiento.

---

### Discos y volúmenes

Un disco físico puede dividirse en uno o varios volúmenes o particiones.

Por ejemplo:

```text
Disco físico

↓

Volumen C:

↓

Volumen D:

↓

Volumen E:
```

Cada volumen puede utilizar un sistema de archivos diferente y almacenar información independiente.

---

### Sistemas de archivos

Windows admite varios sistemas de archivos.

Los más utilizados son:

| Sistema de archivos | Uso principal |
|---------------------|---------------|
| NTFS | Sistema de archivos por defecto en Windows. |
| FAT32 | Compatibilidad con dispositivos antiguos. |
| exFAT | Memorias USB y discos externos. |
| ReFS | Servidores y entornos empresariales. |

La elección dependerá del tipo de dispositivo y del uso previsto.

---

### Administración de discos

La herramienta gráfica utilizada para administrar el almacenamiento es:

```text
diskmgmt.msc
```

Permite realizar operaciones como:

- Crear particiones.
- Eliminar particiones.
- Formatear volúmenes.
- Cambiar letras de unidad.
- Ampliar o reducir particiones.

Es una de las herramientas más utilizadas por los administradores de Windows.

---

### Consultar unidades mediante PowerShell

PowerShell permite visualizar las unidades disponibles mediante:

```powershell
Get-Volume
```

La información mostrada incluye:

- Letra de unidad.
- Sistema de archivos.
- Espacio libre.
- Tamaño total.
- Estado.

Esta herramienta facilita la supervisión del almacenamiento.

---

### Consultar discos físicos

Para mostrar los discos instalados:

```powershell
Get-Disk
```

Este comando permite consultar:

- Número de disco.
- Tamaño.
- Estado.
- Tipo de partición.

Resulta especialmente útil en servidores con varios discos.

---

### Espacio disponible

Windows permite consultar el uso del almacenamiento desde:

- Explorador de archivos.
- Configuración.
- PowerShell.

Ejemplo:

```powershell
Get-PSDrive
```

Este comando muestra el espacio total, utilizado y disponible de cada unidad.

---

### Formateo de unidades

Antes de utilizar un nuevo volumen es necesario formatearlo.

El proceso general es:

```text
Crear volumen

↓

Seleccionar sistema de archivos

↓

Asignar letra

↓

Formatear

↓

Utilizar la unidad
```

El formateo elimina la información existente, por lo que debe realizarse con precaución.

---

### Comprobación del disco

Windows incorpora herramientas para comprobar la integridad del sistema de archivos.

Una de las más utilizadas es:

```cmd
chkdsk
```

Ejemplo:

```cmd
chkdsk C:
```

Esta utilidad permite detectar y, en determinados casos, corregir errores del sistema de archivos.

---

### Optimización del almacenamiento

Para mantener un buen rendimiento se recomienda:

- Eliminar archivos temporales.
- Desinstalar aplicaciones que no se utilicen.
- Liberar espacio periódicamente.
- Supervisar el crecimiento de los datos.
- Mantener suficiente espacio libre en la unidad del sistema.

Estas tareas contribuyen a mejorar el funcionamiento del equipo.

---

### Ejemplo práctico

Un servidor comienza a quedarse sin espacio en la unidad del sistema.

Procedimiento:

```text
Consultar espacio disponible

↓

Identificar los archivos que ocupan más espacio

↓

Eliminar información innecesaria

↓

Comprobar el estado del disco

↓

Verificar el espacio liberado
```

Tras liberar almacenamiento suficiente, el servidor recupera su funcionamiento normal.

---

[⬆️ Volver al índice](#índice)

## Administración de red

Introducción

La administración de red en Windows permite configurar y supervisar la conectividad del sistema, garantizando la comunicación con otros equipos y servicios de la red. Los administradores utilizan herramientas gráficas y de línea de comandos para diagnosticar incidencias, configurar interfaces y verificar el funcionamiento de protocolos y servicios de red.

Una correcta configuración de la red es esencial para el funcionamiento de aplicaciones, servidores y recursos compartidos.

---

### Adaptadores de red

Un adaptador de red es el dispositivo que permite la comunicación del equipo con otras redes.

Puede tratarse de:

- Tarjetas Ethernet.
- Adaptadores Wi-Fi.
- Interfaces virtuales.
- Adaptadores VPN.

Cada adaptador posee su propia configuración de red.

---

### Configuración IP

Cada interfaz puede disponer de:

- Dirección IPv4.
- Dirección IPv6.
- Máscara de subred.
- Puerta de enlace predeterminada.
- Servidores DNS.

Estos parámetros permiten al equipo comunicarse correctamente dentro de la red.

---

### Consultar la configuración de red

Desde el Símbolo del sistema puede utilizarse:

```cmd
ipconfig
```

Para obtener información más detallada:

```cmd
ipconfig /all
```

Estos comandos muestran:

- Adaptadores.
- Direcciones IP.
- DNS.
- DHCP.
- Dirección MAC.

Son herramientas básicas para el diagnóstico de problemas de conectividad.

---

### Comprobar la conectividad

Para verificar la comunicación con otro equipo se utiliza:

```cmd
ping
```

Ejemplo:

```cmd
ping 8.8.8.8
```

Este comando permite comprobar si existe conectividad y medir el tiempo de respuesta.

---

### Comprobar el recorrido de la conexión

Para visualizar los saltos que sigue un paquete hasta su destino:

```cmd
tracert
```

Ejemplo:

```cmd
tracert google.com
```

Esta herramienta ayuda a localizar posibles problemas de enrutamiento.

---

### Resolver problemas DNS

Para comprobar la resolución de nombres puede utilizarse:

```cmd
nslookup
```

Ejemplo:

```cmd
nslookup microsoft.com
```

Permite verificar si el servidor DNS responde correctamente.

---

### Consultar conexiones activas

Para mostrar las conexiones de red activas:

```cmd
netstat
```

Ejemplo:

```cmd
netstat -ano
```

Este comando muestra:

- Conexiones establecidas.
- Puertos abiertos.
- Estado de la conexión.
- PID del proceso asociado.

Resulta muy útil durante tareas de diagnóstico y seguridad.

---

### Configuración mediante PowerShell

PowerShell ofrece herramientas más avanzadas para administrar la red.

Por ejemplo:

Consultar adaptadores:

```powershell
Get-NetAdapter
```

Consultar la configuración IP:

```powershell
Get-NetIPAddress
```

Estas herramientas permiten automatizar numerosas tareas de administración.

---

### Compartición de recursos

Windows permite compartir recursos en red como:

- Carpetas.
- Impresoras.
- Unidades de almacenamiento.

La configuración de estos recursos debe realizarse junto con una correcta asignación de permisos para garantizar la seguridad.

---

### Ejemplo práctico

Un equipo no puede acceder a Internet.

Procedimiento:

```text
Consultar la configuración IP

↓

Comprobar la puerta de enlace

↓

Realizar un ping

↓

Verificar la resolución DNS

↓

Analizar la ruta

↓

Corregir la configuración
```

Siguiendo este procedimiento es posible localizar rápidamente el origen del problema.

---

[⬆️ Volver al índice](#índice)

## Registro de Windows

Introducción

El **Registro de Windows** es una base de datos jerárquica donde el sistema operativo almacena la configuración del propio Windows, del hardware instalado, de los usuarios y de las aplicaciones. Muchas configuraciones que anteriormente se almacenaban en archivos de texto se encuentran actualmente centralizadas en el Registro.

Debido a su importancia, cualquier modificación debe realizarse con precaución, ya que un cambio incorrecto puede afectar al funcionamiento del sistema.

---

### ¿Qué es el Registro de Windows?

El Registro es una base de datos utilizada por Windows para almacenar información relacionada con:

- Configuración del sistema.
- Hardware instalado.
- Controladores.
- Usuarios.
- Aplicaciones.
- Servicios.

El sistema consulta continuamente esta información durante su funcionamiento.

---

### Estructura del Registro

El Registro se organiza mediante una estructura jerárquica formada por claves y valores.

Su organización puede representarse así:

```text
Claves principales

↓

Claves

↓

Subclaves

↓

Valores
```

Esta estructura es similar a la organización de carpetas y archivos en el sistema de archivos.

---

### Claves principales

Las principales ramas del Registro son:

| Clave | Contenido |
|--------|-----------|
| HKEY_CLASSES_ROOT (HKCR) | Asociación de archivos y clases de objetos. |
| HKEY_CURRENT_USER (HKCU) | Configuración del usuario actual. |
| HKEY_LOCAL_MACHINE (HKLM) | Configuración general del equipo. |
| HKEY_USERS (HKU) | Configuración de todos los usuarios. |
| HKEY_CURRENT_CONFIG (HKCC) | Configuración de hardware utilizada durante el inicio. |

Cada rama almacena información específica del sistema.

---

### Editor del Registro

La herramienta utilizada para administrar el Registro es:

```text
regedit
```

Desde ella es posible:

- Consultar claves.
- Crear claves.
- Modificar valores.
- Eliminar entradas.
- Exportar e importar configuraciones.

Debe utilizarse únicamente cuando sea necesario.

---

### Valores del Registro

Cada clave puede contener distintos tipos de valores.

Los más habituales son:

- Valor de cadena (REG_SZ).
- Valor DWORD.
- Valor QWORD.
- Valor binario.
- Valor de cadena múltiple.

Cada tipo almacena la información de una forma diferente.

---

### Exportar el Registro

Antes de realizar modificaciones es recomendable crear una copia de seguridad.

Desde **regedit** puede utilizarse:

```text
Archivo

↓

Exportar
```

El resultado es un archivo con extensión:

```text
.reg
```

que permite restaurar posteriormente la configuración.

---

### Modificación mediante línea de comandos

Windows permite consultar y modificar el Registro mediante la utilidad:

```cmd
reg
```

Por ejemplo:

Consultar una clave:

```cmd
reg query
```

Esta herramienta resulta útil para automatizar configuraciones mediante scripts.

---

### Uso del Registro

Algunas tareas habituales que utilizan el Registro son:

- Configuración de aplicaciones.
- Personalización de Windows.
- Inicio automático de programas.
- Configuración de servicios.
- Ajustes del sistema operativo.

Muchas herramientas administrativas modifican el Registro de forma automática.

---

### Ejemplo práctico

Un administrador necesita modificar una configuración avanzada de Windows.

Procedimiento:

```text
Abrir regedit

↓

Localizar la clave

↓

Exportar la configuración

↓

Modificar el valor

↓

Cerrar el editor

↓

Comprobar el funcionamiento
```

Gracias a la copia de seguridad es posible restaurar la configuración anterior si surge algún problema.

---

[⬆️ Volver al índice](#índice)

## Administración remota

Introducción

La administración remota permite gestionar equipos y servidores Windows sin necesidad de acceder físicamente a ellos. Gracias a esta funcionalidad, los administradores pueden realizar tareas de mantenimiento, configurar servicios, solucionar incidencias y supervisar sistemas desde cualquier ubicación con acceso a la red.

Windows incorpora diversas herramientas y protocolos que facilitan una administración remota segura y eficiente.

---

### Escritorio remoto (RDP)

El protocolo **RDP (Remote Desktop Protocol)** permite conectarse gráficamente a otro equipo Windows como si se estuviera trabajando directamente sobre él.

Sus principales ventajas son:

- Administración remota completa.
- Acceso al escritorio del equipo.
- Ejecución de aplicaciones.
- Configuración del sistema.
- Resolución de incidencias.

Es una de las herramientas más utilizadas en entornos empresariales.

---

### Cliente de Escritorio remoto

La aplicación utilizada para establecer conexiones RDP es:

```text
Conexión a Escritorio remoto (mstsc)
```

Desde ella se introduce:

- Nombre del equipo.
- Dirección IP.
- Usuario.
- Credenciales de acceso.

Una vez autenticado, se muestra el escritorio remoto del equipo.

---

### PowerShell Remoting

Windows permite administrar equipos remotamente mediante **PowerShell Remoting**.

Este mecanismo utiliza el servicio **WinRM (Windows Remote Management)** para ejecutar comandos en equipos remotos de forma segura.

Es especialmente útil para automatizar tareas de administración.

---

### Ejecutar comandos remotos

Una vez configurado PowerShell Remoting, es posible ejecutar comandos mediante:

```powershell
Invoke-Command
```

o iniciar una sesión interactiva con:

```powershell
Enter-PSSession
```

Estas herramientas permiten administrar sistemas sin necesidad de utilizar una interfaz gráfica.

---

### WinRM

**WinRM** es el servicio encargado de gestionar las comunicaciones remotas de PowerShell.

Puede consultarse mediante:

```powershell
Get-Service WinRM
```

Para que PowerShell Remoting funcione correctamente, este servicio debe estar iniciado y configurado.

---

### Asistencia remota

Windows también incorpora la función de **Asistencia remota**, orientada al soporte técnico.

Permite:

- Compartir el escritorio.
- Solicitar ayuda.
- Controlar el equipo con autorización del usuario.

Esta herramienta resulta útil para resolver incidencias en equipos de usuarios.

---

### Administración mediante MMC

La consola **Microsoft Management Console (MMC)** permite administrar equipos locales y remotos utilizando diferentes complementos (*snap-ins*).

Desde ella pueden gestionarse:

- Usuarios.
- Equipos.
- Servicios.
- Visor de eventos.
- Administración de discos.
- Directivas de seguridad.

Es una herramienta ampliamente utilizada en entornos Windows.

---

### Seguridad en la administración remota

Durante la administración remota se recomienda:

- Utilizar cuentas con privilegios adecuados.
- Limitar el acceso únicamente a usuarios autorizados.
- Mantener actualizado el sistema operativo.
- Utilizar conexiones cifradas.
- Registrar las actividades administrativas cuando sea posible.

Estas medidas ayudan a proteger la infraestructura frente a accesos no autorizados.

---

### Ejemplo práctico

Un administrador necesita actualizar un servidor situado en otra sede.

Procedimiento:

```text
Establecer conexión mediante RDP

↓

Autenticarse

↓

Realizar las tareas administrativas

↓

Comprobar el funcionamiento

↓

Cerrar la sesión remota
```

Gracias a la administración remota, el mantenimiento puede realizarse sin desplazamientos físicos.

---

[⬆️ Volver al índice](#índice)