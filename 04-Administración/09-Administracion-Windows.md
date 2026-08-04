# Administración de Windows — Linux vs PowerShell

Microsoft Windows es uno de los sistemas operativos más utilizados en entornos empresariales, tanto en estaciones de trabajo como en servidores.

## Índice

- [Arquitectura básica de Windows](#arquitectura-basica-de-windows)
- [Sistema de archivos en Windows](#sistema-de-archivos-en-windows)
- [Gestión de usuarios y grupos](#gestion-de-usuarios-y-grupos)
- [Gestión de permisos NTFS](#gestion-de-permisos-ntfs)
- [Administración de procesos](#administracion-de-procesos)
- [Administración de servicios](#administracion-de-servicios)
- [Administración del almacenamiento](#administracion-del-almacenamiento)
- [Administración de red](#administracion-de-red)
- [Registro de Windows](#registro-de-windows)
- [Administración remota](#administracion-remota)

---

## Arquitectura básica de Windows

*Microsoft Windows es un sistema operativo diseñado para proporcionar una interfaz gráfica intuitiva y una administración eficiente de los recursos del equipo.*

**Conceptos clave:**

- **Componentes principales:** La arquitectura de Windows está formada por varios elementos fundamentales.
- **Arquitectura general:** La relación entre los distintos componentes puede representarse de la siguiente forma.
- **Hardware:** El hardware corresponde a todos los componentes físicos del equipo.
- **Kernel:** El kernel es el núcleo del sistema operativo.
- **Servicios del sistema:** Los servicios son programas que se ejecutan en segundo plano y proporcionan funciones esenciales.
- **Subsistemas de Windows:** Los subsistemas permiten que las aplicaciones interactúen con el sistema operativo.
- **Aplicaciones:** Las aplicaciones son los programas utilizados por los usuarios para realizar diferentes tareas.
- **Comunicación entre componentes:** El funcionamiento del sistema puede resumirse así.
- **Características de la arquitectura Windows:** La arquitectura de Windows presenta diversas características.
- **Ejemplo práctico:** Un usuario abre una aplicación de gestión.

## Sistema de archivos en Windows

*El sistema de archivos es el encargado de organizar, almacenar y gestionar toda la información contenida en los dispositivos de almacenamiento.*

**Conceptos clave:**

- **Unidades de almacenamiento:** Windows identifica cada dispositivo mediante una letra de unidad.
- **Estructura del sistema de archivos:** La organización de archivos puede representarse mediante una estructura jerárquica.
- **Carpeta Windows:** La carpeta.
- **Carpeta Program Files:** La carpeta.
- **Carpeta Users:** La carpeta.
- **Carpeta ProgramData:** La carpeta.

### Sistemas de archivos compatibles

*Windows admite distintos sistemas de archivos.*

| Sistema de archivos | Uso principal |
|---------------------|---------------|
| NTFS | Sistema principal de Windows. |
| FAT32 | Compatibilidad con numerosos dispositivos. |
| exFAT | Memorias USB y discos externos. |
| ReFS | Entornos empresariales y servidores. |

---

### Consultar el espacio disponible

*El espacio de almacenamiento puede consultarse desde el Explorador de archivos o mediante PowerShell.*

```powershell
Get-PSDrive
```

---

**Conceptos clave:**

- **Rutas de archivos:** Windows utiliza rutas para localizar archivos y directorios.
- **Ejemplo práctico:** Un administrador necesita localizar el perfil de un usuario.

## Gestión de usuarios y grupos

*Windows permite administrar múltiples usuarios dentro de un mismo equipo o dominio, asignando permisos y recursos específicos a cada uno de ellos.*

**Conceptos clave:**

- **Usuarios en Windows:** Un usuario representa una cuenta que permite acceder al sistema operativo.
- **Tipos de usuarios:** Windows distingue varios tipos de cuentas.
- **Cuenta de administrador:** La cuenta de administrador dispone de permisos elevados para realizar tareas de administración.
- **Usuarios estándar:** Los usuarios estándar están diseñados para el trabajo diario.
- **Grupos:** Los grupos permiten administrar permisos de forma conjunta.
- **Herramientas de administración:** En equipos Windows pueden administrarse usuarios mediante diferentes herramientas.

### Crear usuarios mediante PowerShell

*Es posible crear usuarios locales utilizando PowerShell.*

```powershell
New-LocalUser
```

---

### Consultar usuarios

*Para visualizar los usuarios locales puede utilizarse.*

```powershell
Get-LocalUser
```

---

### Consultar grupos

*Para mostrar los grupos locales.*

```powershell
Get-LocalGroup
```
```powershell
Get-LocalGroupMember Administrators
```

---

**Conceptos clave:**

- **Ejemplo práctico:** Un nuevo empleado se incorpora a la empresa.

## Gestión de permisos NTFS

*El sistema de archivos NTFS (New Technology File System) es el utilizado por defecto en las versiones actuales de Windows.*

**Conceptos clave:**

- **¿Qué son los permisos NTFS?:** Los permisos NTFS determinan las acciones que un usuario o grupo puede realizar sobre un archivo o carpeta.

### Tipos de permisos básicos

*Los permisos más habituales son.*

| Permiso | Función |
|----------|---------|
| Control total | Permite realizar cualquier acción sobre el recurso. |
| Modificar | Permite leer, escribir y eliminar archivos. |
| Lectura y ejecución | Permite abrir y ejecutar archivos. |
| Mostrar contenido de carpeta | Permite visualizar el contenido de una carpeta. |
| Lectura | Permite visualizar el contenido sin modificarlo. |
| Escritura | Permite crear o modificar archivos. |

---

**Conceptos clave:**

- **Herencia de permisos:** Una de las características más importantes de NTFS es la herencia.
- **Propietario de un archivo:** Cada archivo o carpeta posee un propietario.
- **Asignación de permisos:** Los permisos pueden configurarse desde las propiedades del archivo o carpeta.
- **Permisos efectivos:** Cuando un usuario pertenece a varios grupos, Windows calcula los permisos efectivos, que representan los permisos finales aplicables.
- **Compartición de carpetas:** Cuando una carpeta se comparte en red intervienen dos tipos de permisos: Permisos NTFS.

### Consultar permisos mediante PowerShell

*PowerShell permite consultar los permisos asignados a un recurso.*

```powershell
Get-Acl C:\Datos
```

---

**Conceptos clave:**

- **Ejemplo práctico:** Un departamento necesita acceder únicamente a una carpeta compartida.

## Administración de procesos

*Un proceso es una instancia de un programa que se encuentra en ejecución.*

**Conceptos clave:**

- **¿Qué es un proceso?:** Un proceso representa un programa que está siendo ejecutado por el sistema operativo.
- **Identificador del proceso (PID):** Cada proceso recibe un identificador único denominado PID (Process ID).
- **Administrador de tareas:** La herramienta gráfica más utilizada para gestionar procesos es el Administrador de tareas.
- **Consultar procesos desde la línea de comandos:** Windows incorpora distintas herramientas para consultar los procesos activos.

### Consultar procesos con PowerShell

*PowerShell proporciona una administración más avanzada mediante.*

```powershell
Get-Process
```

---

**Conceptos clave:**

- **Finalizar procesos:** Cuando una aplicación deja de responder puede finalizarse desde el Administrador de tareas o mediante línea de comandos.

### Finalizar procesos con PowerShell

*PowerShell permite detener procesos mediante.*

```powershell
Stop-Process
```
```powershell
Stop-Process -Name notepad
```

---

**Conceptos clave:**

- **Prioridad de los procesos:** Windows permite modificar la prioridad con la que un proceso utiliza el procesador.
- **Supervisión del rendimiento:** Además del Administrador de tareas, Windows incorpora herramientas como: Monitor de recursos.
- **Ejemplo práctico:** Un equipo presenta un uso excesivo del procesador.

## Administración de servicios

*Los servicios son aplicaciones que se ejecutan en segundo plano y proporcionan funciones esenciales para el funcionamiento del sistema operativo y de otras aplicaciones.*

**Conceptos clave:**

- **¿Qué es un servicio?:** Un servicio es un programa que se ejecuta en segundo plano para proporcionar una determinada funcionalidad al sistema.

### Tipos de inicio

*Cada servicio puede configurarse con distintos modos de inicio.*

| Tipo de inicio | Descripción |
|----------------|-------------|
| Automático | Se inicia durante el arranque del sistema. |
| Automático (inicio retrasado) | Se inicia poco después del arranque para reducir la carga inicial. |
| Manual | Solo se inicia cuando es necesario. |
| Deshabilitado | No puede iniciarse hasta ser habilitado nuevamente. |

---

**Conceptos clave:**

- **Administrador de servicios:** La herramienta gráfica utilizada para administrar servicios es.

### Consultar servicios mediante PowerShell

*PowerShell permite listar los servicios instalados mediante.*

```powershell
Get-Service
```

---

### Iniciar un servicio

*Para iniciar un servicio mediante PowerShell.*

```powershell
Start-Service NombreServicio
```
```powershell
Start-Service Spooler
```

---

### Detener un servicio

*Para detener un servicio.*

```powershell
Stop-Service NombreServicio
```
```powershell
Stop-Service Spooler
```

---

### Reiniciar un servicio

*Cuando un servicio presenta problemas puede reiniciarse mediante.*

```powershell
Restart-Service NombreServicio
```

---

### Consultar un servicio específico

*Es posible obtener información de un servicio concreto mediante.*

```powershell
Get-Service NombreServicio
```
```powershell
Get-Service WinRM
```

---

**Conceptos clave:**

- **Dependencias de servicios:** Algunos servicios dependen del funcionamiento de otros.
- **Ejemplo práctico:** Una impresora deja de funcionar correctamente.

## Administración del almacenamiento

*La administración del almacenamiento en Windows comprende la gestión de discos, particiones, volúmenes y sistemas de archivos.*

**Conceptos clave:**

- **Discos y volúmenes:** Un disco físico puede dividirse en uno o varios volúmenes o particiones.

### Sistemas de archivos

*Windows admite varios sistemas de archivos.*

| Sistema de archivos | Uso principal |
|---------------------|---------------|
| NTFS | Sistema de archivos por defecto en Windows. |
| FAT32 | Compatibilidad con dispositivos antiguos. |
| exFAT | Memorias USB y discos externos. |
| ReFS | Servidores y entornos empresariales. |

---

**Conceptos clave:**

- **Administración de discos:** La herramienta gráfica utilizada para administrar el almacenamiento es.

### Consultar unidades mediante PowerShell

*PowerShell permite visualizar las unidades disponibles mediante.*

```powershell
Get-Volume
```

---

### Consultar discos físicos

*Para mostrar los discos instalados.*

```powershell
Get-Disk
```

---

### Espacio disponible

*Windows permite consultar el uso del almacenamiento desde: Explorador de archivos.*

```powershell
Get-PSDrive
```

---

**Conceptos clave:**

- **Formateo de unidades:** Antes de utilizar un nuevo volumen es necesario formatearlo.
- **Comprobación del disco:** Windows incorpora herramientas para comprobar la integridad del sistema de archivos.
- **Optimización del almacenamiento:** Para mantener un buen rendimiento se recomienda: Eliminar archivos temporales.
- **Ejemplo práctico:** Un servidor comienza a quedarse sin espacio en la unidad del sistema.

## Administración de red

*La administración de red en Windows permite configurar y supervisar la conectividad del sistema, garantizando la comunicación con otros equipos y servicios de la red.*

**Conceptos clave:**

- **Adaptadores de red:** Un adaptador de red es el dispositivo que permite la comunicación del equipo con otras redes.
- **Configuración IP:** Cada interfaz puede disponer de: Dirección IPv4.
- **Consultar la configuración de red:** Desde el Símbolo del sistema puede utilizarse.
- **Comprobar la conectividad:** Para verificar la comunicación con otro equipo se utiliza.
- **Comprobar el recorrido de la conexión:** Para visualizar los saltos que sigue un paquete hasta su destino.
- **Resolver problemas DNS:** Para comprobar la resolución de nombres puede utilizarse.
- **Consultar conexiones activas:** Para mostrar las conexiones de red activas.

### Configuración mediante PowerShell

*PowerShell ofrece herramientas más avanzadas para administrar la red.*

```powershell
Get-NetAdapter
```
```powershell
Get-NetIPAddress
```

---

**Conceptos clave:**

- **Compartición de recursos:** Windows permite compartir recursos en red como: Carpetas.
- **Ejemplo práctico:** Un equipo no puede acceder a Internet.

## Registro de Windows

*El Registro de Windows es una base de datos jerárquica donde el sistema operativo almacena la configuración del propio Windows, del hardware instalado, de los usuarios y de las aplicaciones.*

**Conceptos clave:**

- **¿Qué es el Registro de Windows?:** El Registro es una base de datos utilizada por Windows para almacenar información relacionada con: Configuración del sistema.
- **Estructura del Registro:** El Registro se organiza mediante una estructura jerárquica formada por claves y valores.

### Claves principales

*Las principales ramas del Registro son.*

| Clave | Contenido |
|--------|-----------|
| HKEY_CLASSES_ROOT (HKCR) | Asociación de archivos y clases de objetos. |
| HKEY_CURRENT_USER (HKCU) | Configuración del usuario actual. |
| HKEY_LOCAL_MACHINE (HKLM) | Configuración general del equipo. |
| HKEY_USERS (HKU) | Configuración de todos los usuarios. |
| HKEY_CURRENT_CONFIG (HKCC) | Configuración de hardware utilizada durante el inicio. |

---

**Conceptos clave:**

- **Editor del Registro:** La herramienta utilizada para administrar el Registro es.
- **Valores del Registro:** Cada clave puede contener distintos tipos de valores.
- **Exportar el Registro:** Antes de realizar modificaciones es recomendable crear una copia de seguridad.
- **Modificación mediante línea de comandos:** Windows permite consultar y modificar el Registro mediante la utilidad.
- **Uso del Registro:** Algunas tareas habituales que utilizan el Registro son: Configuración de aplicaciones.
- **Ejemplo práctico:** Un administrador necesita modificar una configuración avanzada de Windows.

## Administración remota

*La administración remota permite gestionar equipos y servidores Windows sin necesidad de acceder físicamente a ellos.*

**Conceptos clave:**

- **Escritorio remoto (RDP):** El protocolo RDP (Remote Desktop Protocol) permite conectarse gráficamente a otro equipo Windows como si se estuviera trabajando directamente sobre él.
- **Cliente de Escritorio remoto:** La aplicación utilizada para establecer conexiones RDP es.
- **PowerShell Remoting:** Windows permite administrar equipos remotamente mediante PowerShell Remoting.

### Ejecutar comandos remotos

*Una vez configurado PowerShell Remoting, es posible ejecutar comandos mediante.*

```powershell
Invoke-Command
```
```powershell
Enter-PSSession
```

---

### WinRM

*WinRM es el servicio encargado de gestionar las comunicaciones remotas de PowerShell.*

```powershell
Get-Service WinRM
```

---

**Conceptos clave:**

- **Asistencia remota:** Windows también incorpora la función de Asistencia remota, orientada al soporte técnico.
- **Administración mediante MMC:** La consola Microsoft Management Console (MMC) permite administrar equipos locales y remotos utilizando diferentes complementos (*snap-ins*).
- **Seguridad en la administración remota:** Durante la administración remota se recomienda: Utilizar cuentas con privilegios adecuados.
- **Ejemplo práctico:** Un administrador necesita actualizar un servidor situado en otra sede.

[⬆️ Volver al índice](#índice)
