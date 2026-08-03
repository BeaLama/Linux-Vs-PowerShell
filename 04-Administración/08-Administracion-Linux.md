# Administración de Linux

## Introducción

Linux es uno de los sistemas operativos más utilizados en servidores, centros de datos, dispositivos de red y plataformas en la nube debido a su estabilidad, seguridad y flexibilidad. Su administración requiere conocer el funcionamiento del sistema, la gestión de usuarios, archivos, servicios, procesos y redes, así como las herramientas disponibles para automatizar tareas y supervisar el funcionamiento del sistema.

## Índice

- [Arquitectura básica de Linux](#arquitectura-básica-de-linux)
- [Sistema de archivos en Linux](#sistema-de-archivos-en-linux)
- [Gestión de usuarios y grupos](#gestión-de-usuarios-y-grupos)
- [Gestión de permisos](#gestión-de-permisos)
- [Administración de procesos](#administración-de-procesos)
- [Gestión de servicios con systemd](#gestión-de-servicios-con-systemd)
- [Administración del almacenamiento](#administración-del-almacenamiento)
- [Administración de red](#administración-de-red)
- [Gestión de paquetes](#gestión-de-paquetes)
- [Administración remota mediante SSH](#administración-remota-mediante-ssh)

---

## Arquitectura básica de Linux

La arquitectura de Linux está formada por varios elementos fundamentales.

Los principales son:

- Hardware.
- Kernel.
- Espacio de usuario.
- Shell.
- Aplicaciones.

Cada uno desempeña una función específica dentro del sistema operativo.

---

### Arquitectura general

La relación entre los distintos componentes puede representarse de la siguiente forma:

```text
Aplicaciones

↓

Shell

↓

Kernel

↓

Hardware
```

El kernel actúa como intermediario entre el software y el hardware del equipo.

---

### Hardware

El hardware constituye la parte física del sistema.

Incluye dispositivos como:

- Procesador (CPU).
- Memoria RAM.
- Discos.
- Tarjetas de red.
- Dispositivos USB.
- Tarjetas gráficas.

El sistema operativo utiliza estos recursos para ejecutar las aplicaciones.

---

### Kernel

El **kernel** es el núcleo del sistema operativo y uno de los componentes más importantes de Linux.

Entre sus funciones destacan:

- Gestión de procesos.
- Administración de memoria.
- Control de dispositivos.
- Gestión del sistema de archivos.
- Comunicación con el hardware.
- Gestión de la red.

Todas las aplicaciones acceden al hardware a través del kernel.

---

### Espacio de usuario

El espacio de usuario es la zona donde se ejecutan los programas utilizados por los usuarios.

En este nivel se encuentran:

- Aplicaciones.
- Herramientas administrativas.
- Intérpretes de comandos.
- Bibliotecas del sistema.

Las aplicaciones no acceden directamente al hardware, sino mediante llamadas al kernel.

---

### Shell

La **Shell** es el intérprete de comandos que permite al usuario interactuar con el sistema operativo.

Sus funciones principales son:

- Ejecutar comandos.
- Lanzar programas.
- Ejecutar scripts.
- Automatizar tareas.

La shell más utilizada en Linux es **Bash**.

---

### Aplicaciones

Las aplicaciones son los programas que utilizan los usuarios para realizar distintas tareas.

Algunos ejemplos son:

- Navegadores web.
- Editores de texto.
- Servidores web.
- Bases de datos.
- Herramientas de administración.

Estas aplicaciones utilizan los servicios ofrecidos por el kernel para funcionar correctamente.

---

### Comunicación entre componentes

El funcionamiento general del sistema puede resumirse así:

```text
Usuario

↓

Shell

↓

Aplicación

↓

Kernel

↓

Hardware

↓

Respuesta al usuario
```

Este modelo garantiza un acceso controlado y seguro a los recursos del sistema.

---

### Características de la arquitectura Linux

La arquitectura de Linux presenta diversas ventajas.

Entre ellas:

- Modularidad.
- Estabilidad.
- Seguridad.
- Multitarea.
- Multiusuario.
- Gran capacidad de personalización.

Estas características explican su amplia utilización en servidores y entornos empresariales.

---

[⬆️ Volver al índice](#índice)

## Sistema de archivos en Linux

Introducción

El sistema de archivos de Linux organiza toda la información almacenada en discos y otros dispositivos mediante una estructura jerárquica en forma de árbol. A diferencia de otros sistemas operativos, todos los archivos y directorios parten de un único directorio raíz, lo que proporciona una organización uniforme y facilita la administración del sistema.

Conocer la estructura del sistema de archivos resulta imprescindible para localizar configuraciones, administrar aplicaciones y realizar tareas de mantenimiento.

---

### Estructura jerárquica

En Linux todos los archivos y directorios dependen de un único directorio principal denominado **raíz**.

Su estructura puede representarse así:

```text
/

├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var
```

Toda la información del sistema se organiza a partir de este directorio.

---

### Directorio raíz (/)

El directorio **/** constituye el punto de inicio del sistema de archivos.

Desde él cuelgan todos los demás directorios, independientemente del disco físico donde se encuentren almacenados.

Es el nivel más alto de la jerarquía.

---

### Directorio /home

El directorio **/home** almacena los directorios personales de los usuarios.

Por ejemplo:

```text
/home/juan
/home/maria
/home/admin
```

Cada usuario dispone de su propio espacio de trabajo donde guarda documentos y configuraciones personales.

---

### Directorio /etc

El directorio **/etc** contiene la mayoría de los archivos de configuración del sistema.

Entre ellos:

- Configuración de red.
- Usuarios y grupos.
- Servicios.
- Programas instalados.

Es uno de los directorios más importantes para la administración del sistema.

---

### Directorios /bin y /sbin

Estos directorios contienen los ejecutables esenciales del sistema.

- **/bin**: comandos básicos accesibles para todos los usuarios.
- **/sbin**: herramientas de administración utilizadas principalmente por el administrador del sistema.

Muchos comandos habituales se encuentran en estas ubicaciones.

---

### Directorio /var

El directorio **/var** almacena información que cambia frecuentemente.

Por ejemplo:

- Archivos de registro (*logs*).
- Caché.
- Colas de impresión.
- Bases de datos de algunos servicios.

Es habitual supervisar este directorio para controlar el crecimiento de los registros del sistema.

---

### Directorio /tmp

El directorio **/tmp** se utiliza para almacenar archivos temporales.

Sus características principales son:

- Contiene información temporal.
- Puede limpiarse automáticamente.
- Es utilizado por numerosas aplicaciones.

No debe emplearse para almacenar información permanente.

---

### Directorio /usr

El directorio **/usr** contiene gran parte de las aplicaciones y bibliotecas instaladas.

Incluye:

- Programas.
- Documentación.
- Bibliotecas.
- Archivos compartidos.

Es uno de los directorios con mayor tamaño en la mayoría de sistemas Linux.

---

### Directorios /dev, /proc y /sys

Estos directorios permiten acceder a información relacionada con el hardware y el funcionamiento interno del sistema.

- **/dev**: dispositivos del sistema.
- **/proc**: información sobre procesos y kernel.
- **/sys**: información sobre dispositivos y hardware.

Muchos administradores utilizan estos directorios durante tareas de diagnóstico.

---

### Navegación por el sistema de archivos

Algunos comandos habituales son:

Mostrar el directorio actual:

```bash
pwd
```

Listar el contenido de un directorio:

```bash
ls
```

Cambiar de directorio:

```bash
cd
```

Estos comandos permiten desplazarse fácilmente por la estructura del sistema.

---

### Ejemplo práctico

Un administrador necesita localizar el archivo de configuración de un servicio.

Procedimiento:

```text
Acceder a /etc

↓

Localizar el archivo

↓

Modificar la configuración

↓

Guardar los cambios

↓

Reiniciar el servicio
```

Gracias a la organización del sistema de archivos, la localización de configuraciones resulta sencilla y uniforme.

---

[⬆️ Volver al índice](#índice)

## Gestión de usuarios y grupos

Introducción

Linux es un sistema operativo **multiusuario**, lo que significa que varias personas pueden utilizar el mismo sistema de forma simultánea, cada una con su propia cuenta y permisos. Para garantizar la seguridad y una correcta organización de los recursos, el sistema permite administrar usuarios y grupos de manera flexible.

La gestión adecuada de usuarios y grupos es una de las tareas más habituales para cualquier administrador de sistemas Linux.

---

### Usuarios en Linux

Un usuario representa una identidad dentro del sistema operativo.

Cada usuario dispone de:

- Un nombre de usuario.
- Un identificador único (UID).
- Una contraseña.
- Un directorio personal.
- Un intérprete de comandos (*shell*).

Esta información permite identificar al usuario y controlar los recursos a los que puede acceder.

---

### Tipos de usuarios

En Linux pueden encontrarse distintos tipos de usuarios.

Los principales son:

- Usuario **root**.
- Usuarios normales.
- Usuarios del sistema o de servicios.

Cada tipo tiene una finalidad diferente dentro del sistema operativo.

---

### Usuario root

El usuario **root** posee privilegios completos sobre el sistema.

Puede realizar operaciones como:

- Instalar software.
- Crear usuarios.
- Modificar configuraciones.
- Gestionar servicios.
- Eliminar archivos del sistema.

Por motivos de seguridad, su utilización debe limitarse únicamente a tareas administrativas.

---

### Usuarios normales

Los usuarios normales son las cuentas utilizadas por las personas que trabajan con el sistema.

Habitualmente pueden:

- Acceder a su directorio personal.
- Ejecutar aplicaciones.
- Crear y modificar sus propios archivos.
- Utilizar los recursos autorizados.

No pueden modificar configuraciones críticas sin permisos administrativos.

---

### Grupos

Un grupo permite reunir varios usuarios para administrar permisos de forma conjunta.

Por ejemplo:

```text
Grupo: desarrollo

↓

Usuario1

Usuario2

Usuario3
```

Gracias a los grupos es posible asignar permisos a varios usuarios simultáneamente.

---

### Archivos de configuración

La información de usuarios y grupos se almacena principalmente en:

```text
/etc/passwd
```

Contiene información básica sobre las cuentas de usuario.

```text
/etc/shadow
```

Almacena las contraseñas cifradas y la información relacionada con ellas.

```text
/etc/group
```

Contiene la información sobre los grupos del sistema.

Estos archivos forman parte de la administración básica de Linux.

---

### Creación de usuarios

Para crear un nuevo usuario puede utilizarse:

```bash
sudo useradd usuario
```

En muchas distribuciones también es habitual utilizar:

```bash
sudo adduser usuario
```

Tras la creación de la cuenta suele asignarse una contraseña.

---

### Gestión de grupos

Para crear un grupo:

```bash
sudo groupadd desarrollo
```

Para añadir un usuario a un grupo:

```bash
sudo usermod -aG desarrollo usuario
```

Estas operaciones permiten organizar fácilmente los permisos dentro de la organización.

---

### Consultar información

Algunos comandos útiles son:

Mostrar el usuario actual:

```bash
whoami
```

Mostrar los grupos del usuario:

```bash
groups
```

Mostrar el identificador del usuario:

```bash
id
```

Estos comandos ayudan a comprobar la configuración de las cuentas.

---

### Ejemplo práctico

Un nuevo empleado se incorpora al departamento de informática.

Procedimiento:

```text
Crear usuario

↓

Asignar contraseña

↓

Añadir al grupo correspondiente

↓

Verificar la configuración

↓

Entregar las credenciales
```

Gracias a este procedimiento, el nuevo usuario dispone del acceso necesario para comenzar a trabajar.

---

[⬆️ Volver al índice](#índice)

## Gestión de permisos

Introducción

Uno de los aspectos más importantes de la administración de Linux es el control de acceso a los archivos y directorios. El sistema de permisos permite determinar qué usuarios pueden leer, modificar o ejecutar un recurso, garantizando así la seguridad y la integridad de la información.

Comprender el funcionamiento de los permisos resulta imprescindible para administrar correctamente cualquier sistema Linux.

---

### ¿Qué son los permisos?

Los permisos indican las acciones que un usuario puede realizar sobre un archivo o directorio.

Las operaciones permitidas son:

- Leer.
- Escribir.
- Ejecutar.

Cada archivo y directorio posee su propia configuración de permisos.

---

### Tipos de permisos

Linux utiliza tres permisos básicos.

| Permiso | Símbolo | Función |
|----------|---------|---------|
| Lectura | **r** | Permite visualizar el contenido. |
| Escritura | **w** | Permite modificar el contenido. |
| Ejecución | **x** | Permite ejecutar un archivo o acceder a un directorio. |

La combinación de estos permisos determina el nivel de acceso de cada usuario.

---

### Propietario, grupo y otros

Los permisos se asignan a tres categorías de usuarios.

- **Propietario (User)**.
- **Grupo (Group)**.
- **Otros usuarios (Others)**.

Su estructura puede representarse así:

```text
Archivo

↓

Propietario

Grupo

Otros
```

Cada categoría puede disponer de permisos diferentes.

---

### Representación de permisos

Los permisos suelen mostrarse mediante una secuencia de caracteres.

Ejemplo:

```text
-rwxr-xr--
```

Su interpretación sería:

```text
-

Tipo de archivo

rwx

Permisos del propietario

r-x

Permisos del grupo

r--

Permisos de otros usuarios
```

Esta representación permite conocer rápidamente quién puede acceder al recurso.

---

### Permisos numéricos

Los permisos también pueden expresarse mediante valores numéricos.

| Valor | Permisos |
|------:|----------|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |
| 3 | -wx |
| 2 | -w- |
| 1 | --x |
| 0 | --- |

Por ejemplo:

```text
755
```

equivale a:

```text
rwxr-xr-x
```

---

### Cambiar permisos

Para modificar los permisos se utiliza:

```bash
chmod
```

Ejemplo:

```bash
chmod 755 script.sh
```

También pueden utilizarse permisos simbólicos.

Ejemplo:

```bash
chmod u+x script.sh
```

Estos comandos permiten adaptar el acceso a cada archivo o directorio.

---

### Cambiar propietario

Para modificar el propietario de un archivo se utiliza:

```bash
chown
```

Ejemplo:

```bash
sudo chown usuario archivo.txt
```

También es posible cambiar simultáneamente el propietario y el grupo.

---

### Cambiar grupo

Para modificar el grupo asociado a un archivo se utiliza:

```bash
chgrp
```

Ejemplo:

```bash
sudo chgrp desarrollo proyecto.txt
```

Esto facilita la administración de recursos compartidos entre varios usuarios.

---

### Permisos en directorios

En los directorios, los permisos tienen un significado específico.

- **r** → Permite listar el contenido.
- **w** → Permite crear, eliminar o renombrar archivos.
- **x** → Permite acceder al directorio.

La combinación de estos permisos determina qué operaciones pueden realizar los usuarios.

---

### Ejemplo práctico

Un administrador necesita permitir la ejecución de un script únicamente a su propietario.

Procedimiento:

```text
Comprobar permisos

↓

Asignar permiso de ejecución

↓

Verificar la configuración

↓

Ejecutar el script
```

Comando utilizado:

```bash
chmod 700 script.sh
```

El propietario puede leer, modificar y ejecutar el archivo, mientras que el resto de usuarios no dispone de acceso.

---

[⬆️ Volver al índice](#índice)

## Administración de procesos

Introducción

Un **proceso** es una instancia de un programa que se encuentra en ejecución. Cada vez que una aplicación se inicia, el sistema operativo crea uno o varios procesos para gestionar su funcionamiento. La administración de procesos es una de las tareas más habituales en Linux, ya que permite supervisar el consumo de recursos, finalizar aplicaciones bloqueadas y controlar el comportamiento del sistema.

Comprender cómo funcionan los procesos resulta fundamental para mantener un sistema estable y con un buen rendimiento.

---

### ¿Qué es un proceso?

Un proceso representa un programa que está siendo ejecutado por el sistema operativo.

Cada proceso dispone de:

- Un identificador único (PID).
- Un propietario.
- Un estado.
- Prioridad de ejecución.
- Consumo de memoria.
- Consumo de CPU.

El kernel administra todos los procesos activos del sistema.

---

### Identificador del proceso (PID)

Cada proceso recibe un número denominado **PID (Process ID)**.

Este identificador permite:

- Localizar un proceso.
- Supervisarlo.
- Modificar su prioridad.
- Finalizar su ejecución.

No existen dos procesos activos con el mismo PID.

---

### Estados de un proceso

Durante su ciclo de vida un proceso puede encontrarse en distintos estados.

Los más habituales son:

- **En ejecución (Running)**.
- **Preparado (Ready)**.
- **En espera (Sleeping)**.
- **Detenido (Stopped)**.
- **Finalizado (Zombie o Terminated)**.

El sistema operativo cambia automáticamente el estado de los procesos según sea necesario.

---

### Consultar procesos

Para visualizar los procesos en ejecución pueden utilizarse distintos comandos.

Mostrar los procesos actuales:

```bash
ps
```

Mostrar todos los procesos del sistema:

```bash
ps -ef
```

Estos comandos permiten obtener información detallada sobre cada proceso.

---

### Supervisión en tiempo real

Linux dispone de herramientas para observar los procesos mientras se ejecutan.

La más utilizada es:

```bash
top
```

También existen herramientas más avanzadas como:

```bash
htop
```

Estas utilidades muestran en tiempo real el consumo de CPU, memoria y otros recursos.

---

### Finalizar procesos

Cuando una aplicación deja de responder puede ser necesario finalizar su ejecución.

Para ello se utiliza:

```bash
kill PID
```

Si el proceso no responde, puede forzarse su finalización mediante:

```bash
kill -9 PID
```

Debe utilizarse esta opción únicamente cuando el proceso no pueda finalizarse de forma normal.

---

### Buscar procesos

Es posible localizar un proceso concreto utilizando:

```bash
pgrep nombre
```

o

```bash
pidof nombre
```

Estos comandos permiten obtener rápidamente el PID de una aplicación.

---

### Prioridad de procesos

Linux permite modificar la prioridad con la que un proceso utiliza la CPU.

Para ello se emplean herramientas como:

```bash
nice
```

y

```bash
renice
```

Una prioridad adecuada mejora el reparto de recursos entre las aplicaciones.

---

### Procesos en segundo plano

Linux permite ejecutar programas en segundo plano para continuar utilizando la terminal.

Ejemplo:

```bash
comando &
```

También pueden gestionarse mediante:

```bash
jobs
```

Esto facilita la ejecución simultánea de varias tareas.

---

### Ejemplo práctico

Un servidor presenta un consumo elevado de CPU.

Procedimiento:

```text
Consultar procesos

↓

Identificar el proceso con mayor consumo

↓

Analizar su funcionamiento

↓

Finalizar el proceso si es necesario

↓

Verificar el rendimiento del sistema
```

Gracias a este procedimiento se recupera el funcionamiento normal del servidor.

---

[⬆️ Volver al índice](#índice)

## Gestión de servicios con systemd

Introducción

En la mayoría de las distribuciones Linux modernas, **systemd** es el sistema encargado de iniciar el sistema operativo y administrar los servicios. Gracias a esta herramienta es posible iniciar, detener, reiniciar y supervisar servicios de forma sencilla, además de gestionar su ejecución automática durante el arranque del sistema.

El conocimiento de **systemd** resulta esencial para cualquier administrador de sistemas Linux.

---

### ¿Qué es systemd?

**systemd** es el gestor de servicios e inicialización utilizado por la mayoría de distribuciones Linux.

Entre sus funciones destacan:

- Iniciar el sistema operativo.
- Gestionar servicios.
- Controlar dependencias.
- Registrar eventos del sistema.
- Administrar procesos de inicio.

Actualmente es el estándar en distribuciones como Ubuntu, Debian, Fedora, CentOS o Rocky Linux.

---

### ¿Qué es un servicio?

Un servicio es un programa que se ejecuta en segundo plano para proporcionar una determinada funcionalidad al sistema o a los usuarios.

Algunos ejemplos son:

- Servidor web.
- Servidor SSH.
- Servidor DNS.
- Base de datos.
- Servicio de impresión.

Estos servicios suelen iniciarse automáticamente al arrancar el sistema.

---

### Unidades de systemd

Systemd organiza los recursos mediante **unidades** (*units*).

Las más habituales son:

- **.service** → Servicios.
- **.socket** → Sockets.
- **.target** → Objetivos de arranque.
- **.mount** → Sistemas de archivos.
- **.timer** → Tareas programadas.

La unidad más utilizada por los administradores es **.service**.

---

### Consultar el estado de un servicio

Para conocer el estado de un servicio se utiliza:

```bash
systemctl status nombre_servicio
```

Ejemplo:

```bash
systemctl status ssh
```

Este comando muestra información como:

- Estado.
- Tiempo de ejecución.
- PID.
- Registros recientes.

---

### Iniciar un servicio

Para iniciar un servicio:

```bash
sudo systemctl start nombre_servicio
```

Ejemplo:

```bash
sudo systemctl start apache2
```

El servicio comenzará a ejecutarse sin necesidad de reiniciar el sistema.

---

### Detener un servicio

Para detener un servicio:

```bash
sudo systemctl stop nombre_servicio
```

Ejemplo:

```bash
sudo systemctl stop apache2
```

El servicio dejará de estar disponible hasta que vuelva a iniciarse.

---

### Reiniciar un servicio

Cuando un servicio presenta problemas suele ser suficiente con reiniciarlo.

Comando:

```bash
sudo systemctl restart nombre_servicio
```

Esto detiene el servicio y lo inicia nuevamente.

---

### Habilitar el inicio automático

Para que un servicio se inicie automáticamente al arrancar el sistema:

```bash
sudo systemctl enable nombre_servicio
```

Ejemplo:

```bash
sudo systemctl enable ssh
```

A partir del siguiente reinicio el servicio se iniciará automáticamente.

---

### Deshabilitar el inicio automático

Si no se desea que un servicio arranque con el sistema:

```bash
sudo systemctl disable nombre_servicio
```

Esto evita que el servicio se inicie automáticamente en futuros arranques.

---

### Consultar los registros

Systemd integra un sistema de registros denominado **journal**.

Para consultar los registros se utiliza:

```bash
journalctl
```

También es posible visualizar los registros de un servicio concreto.

Ejemplo:

```bash
journalctl -u ssh
```

Estos registros resultan muy útiles para diagnosticar incidencias.

---

### Ejemplo práctico

Un servidor web deja de responder.

Procedimiento:

```text
Consultar el estado del servicio

↓

Analizar los registros

↓

Reiniciar el servicio

↓

Comprobar su funcionamiento

↓

Verificar que responde correctamente
```

Gracias a este procedimiento es posible restaurar rápidamente el funcionamiento del servicio.

---

[⬆️ Volver al índice](#índice)

## Administración del almacenamiento

Introducción

El almacenamiento constituye uno de los recursos más importantes de cualquier sistema Linux. Una correcta administración de discos, particiones y sistemas de archivos garantiza el buen funcionamiento del sistema operativo, evita la pérdida de información y permite aprovechar eficientemente el espacio disponible.

Los administradores de sistemas deben supervisar periódicamente el estado del almacenamiento y conocer las herramientas necesarias para gestionar dispositivos, particiones y volúmenes.

---

### Dispositivos de almacenamiento

Linux identifica los dispositivos de almacenamiento mediante archivos especiales ubicados en el directorio:

```text
/dev
```

Algunos ejemplos son:

```text
/dev/sda
/dev/sdb
/dev/nvme0n1
```

Cada dispositivo puede contener una o varias particiones.

---

### Particiones

Una partición representa una división lógica de un disco físico.

Por ejemplo:

```text
Disco

↓

Partición 1

↓

Partición 2

↓

Partición 3
```

Cada partición puede utilizar un sistema de archivos diferente.

---

### Sistemas de archivos

Antes de utilizar una partición es necesario formatearla con un sistema de archivos.

Algunos de los más habituales son:

- ext4.
- XFS.
- Btrfs.
- FAT32.
- NTFS.

La elección dependerá del uso previsto y de la distribución Linux utilizada.

---

### Consultar discos y particiones

Para visualizar los dispositivos disponibles puede utilizarse:

```bash
lsblk
```

Este comando muestra:

- Discos.
- Particiones.
- Puntos de montaje.

Es una de las herramientas más utilizadas para consultar el almacenamiento.

---

### Consultar el espacio disponible

Para comprobar el uso del almacenamiento se utiliza:

```bash
df -h
```

Este comando muestra:

- Espacio total.
- Espacio utilizado.
- Espacio libre.
- Porcentaje de ocupación.

La opción **-h** presenta los datos en un formato fácilmente legible.

---

### Consultar el tamaño de directorios

Cuando es necesario localizar qué directorios ocupan más espacio puede utilizarse:

```bash
du -sh directorio
```

Por ejemplo:

```bash
du -sh /var
```

Esta información resulta útil para detectar consumos anómalos de almacenamiento.

---

### Montaje de sistemas de archivos

Antes de acceder a una partición es necesario montarla en un directorio.

El procedimiento es:

```text
Dispositivo

↓

Montaje

↓

Directorio

↓

Acceso al contenido
```

Linux utiliza puntos de montaje para integrar distintos dispositivos en una única estructura de directorios.

---

### Consultar sistemas montados

Para visualizar los sistemas de archivos actualmente montados puede utilizarse:

```bash
mount
```

También es posible consultar únicamente la información relevante mediante:

```bash
findmnt
```

Estos comandos muestran el estado actual del almacenamiento.

---

### Archivo fstab

El archivo:

```text
/etc/fstab
```

define los sistemas de archivos que deben montarse automáticamente durante el arranque del sistema.

En él se especifican:

- Dispositivo.
- Punto de montaje.
- Sistema de archivos.
- Opciones de montaje.

Una configuración incorrecta puede impedir el inicio normal del sistema.

---

### Ejemplo práctico

Un servidor comienza a funcionar lentamente por falta de espacio.

Procedimiento:

```text
Consultar espacio disponible

↓

Identificar el directorio con mayor tamaño

↓

Eliminar archivos innecesarios

↓

Liberar espacio

↓

Verificar el funcionamiento
```

Tras liberar almacenamiento suficiente, el servidor recupera su rendimiento habitual.

---

[⬆️ Volver al índice](#índice)

## Administración de red

Introducción

La administración de red es una de las tareas más importantes en un sistema Linux, ya que permite configurar la comunicación entre equipos, acceder a servicios remotos y garantizar el correcto funcionamiento de aplicaciones que dependen de la conectividad. Linux incorpora numerosas herramientas para consultar, configurar y diagnosticar el estado de la red.

Un administrador de sistemas debe conocer estos comandos para resolver incidencias y mantener la infraestructura en funcionamiento.

---

### Interfaces de red

Una **interfaz de red** representa el dispositivo que permite la comunicación entre el sistema y la red.

Puede tratarse de:

- Tarjetas Ethernet.
- Adaptadores Wi-Fi.
- Interfaces virtuales.
- Interfaces de bucle local (*loopback*).

Cada interfaz dispone de una configuración propia.

---

### Consultar interfaces

Para mostrar las interfaces disponibles puede utilizarse:

```bash
ip link
```

Este comando muestra información como:

- Nombre de la interfaz.
- Estado.
- Dirección MAC.

Permite comprobar rápidamente qué interfaces están disponibles.

---

### Consultar direcciones IP

Para visualizar la configuración IP se utiliza:

```bash
ip addr
```

Entre la información mostrada se encuentra:

- Dirección IPv4.
- Dirección IPv6.
- Máscara de red.
- Estado de la interfaz.

Es uno de los comandos más utilizados durante el diagnóstico de problemas de red.

---

### Comprobar la conectividad

Para verificar la comunicación con otro equipo se emplea:

```bash
ping
```

Ejemplo:

```bash
ping 8.8.8.8
```

Este comando permite comprobar si existe conectividad con el destino y medir el tiempo de respuesta.

---

### Comprobar rutas

La tabla de enrutamiento puede consultarse mediante:

```bash
ip route
```

En ella se muestra información como:

- Puerta de enlace predeterminada.
- Redes conocidas.
- Interfaces utilizadas.

Esta información resulta fundamental para diagnosticar problemas de comunicación.

---

### Resolución de nombres

Para comprobar la resolución DNS pueden utilizarse herramientas como:

```bash
nslookup
```

o

```bash
dig
```

Estas utilidades permiten verificar si un nombre de dominio se resuelve correctamente a una dirección IP.

---

### Comprobar conexiones

Para visualizar las conexiones activas del sistema puede utilizarse:

```bash
ss
```

Por ejemplo:

```bash
ss -tuln
```

Este comando muestra:

- Puertos abiertos.
- Servicios en escucha.
- Protocolos utilizados.
- Direcciones IP asociadas.

Es especialmente útil para comprobar el funcionamiento de servicios de red.

---

### Reiniciar la red

En algunas distribuciones es posible reiniciar el servicio de red mediante:

```bash
sudo systemctl restart NetworkManager
```

o el servicio correspondiente según la distribución utilizada.

Esto permite aplicar cambios de configuración sin reiniciar el sistema.

---

### Archivos de configuración

La configuración de red puede almacenarse en diferentes ubicaciones según la distribución Linux.

Algunos ejemplos son:

- **/etc/network/interfaces** (Debian y derivados).
- Archivos gestionados por **NetworkManager**.
- Configuración mediante **netplan** en versiones recientes de Ubuntu.

Es importante conocer el método utilizado por la distribución administrada.

---

### Ejemplo práctico

Un servidor no puede acceder a Internet.

Procedimiento:

```text
Comprobar la dirección IP

↓

Verificar la puerta de enlace

↓

Realizar un ping

↓

Comprobar la resolución DNS

↓

Revisar la tabla de rutas

↓

Corregir la configuración
```

Gracias a este procedimiento es posible localizar rápidamente el origen de la incidencia.

---

[⬆️ Volver al índice](#índice)

## Gestión de paquetes

Introducción

La instalación, actualización y eliminación de software es una de las tareas más habituales en la administración de sistemas Linux. Para facilitar este proceso, las distribuciones incorporan **gestores de paquetes**, herramientas que permiten administrar aplicaciones y sus dependencias de forma sencilla y segura.

El uso de gestores de paquetes garantiza que el software instalado sea compatible con el sistema y facilita el mantenimiento y las actualizaciones.

---

### ¿Qué es un paquete?

Un **paquete** es un archivo que contiene todo lo necesario para instalar una aplicación o componente del sistema.

Habitualmente incluye:

- Archivos del programa.
- Bibliotecas.
- Archivos de configuración.
- Información sobre dependencias.
- Metadatos de instalación.

Los gestores de paquetes se encargan de instalar estos componentes de forma automática.

---

### Gestores de paquetes

Existen diferentes gestores de paquetes según la distribución Linux.

Los más utilizados son:

| Distribución | Gestor de paquetes |
|---------------|--------------------|
| Debian / Ubuntu | APT |
| Fedora | DNF |
| CentOS / Rocky Linux | DNF |
| openSUSE | Zypper |
| Arch Linux | Pacman |

Cada uno utiliza su propio formato de paquetes y comandos.

---

### Repositorios

Los **repositorios** son servidores que almacenan miles de paquetes de software organizados y mantenidos por la comunidad o por los fabricantes de las distribuciones.

Gracias a ellos es posible:

- Instalar aplicaciones.
- Descargar actualizaciones.
- Corregir errores.
- Obtener nuevas versiones del software.

La mayoría de instalaciones se realizan directamente desde estos repositorios.

---

### Actualizar la información de los repositorios

En distribuciones basadas en Debian es habitual actualizar primero la información disponible.

Comando:

```bash
sudo apt update
```

Este proceso no instala software, únicamente actualiza el listado de paquetes disponibles.

---

### Instalar software

Para instalar una aplicación mediante APT se utiliza:

```bash
sudo apt install nombre_paquete
```

Ejemplo:

```bash
sudo apt install nginx
```

El gestor descargará automáticamente el paquete y las dependencias necesarias.

---

### Actualizar el sistema

Para instalar las actualizaciones disponibles:

```bash
sudo apt upgrade
```

Este comando actualiza los paquetes ya instalados a sus versiones más recientes.

Mantener el sistema actualizado mejora la seguridad y la estabilidad.

---

### Eliminar paquetes

Para desinstalar una aplicación:

```bash
sudo apt remove nombre_paquete
```

Si también se desea eliminar la configuración asociada:

```bash
sudo apt purge nombre_paquete
```

Esto permite liberar espacio y mantener el sistema organizado.

---

### Buscar paquetes

Es posible localizar aplicaciones disponibles mediante:

```bash
apt search nombre
```

Por ejemplo:

```bash
apt search apache
```

El comando muestra todos los paquetes relacionados con el término indicado.

---

### Consultar paquetes instalados

Para obtener un listado del software instalado puede utilizarse:

```bash
apt list --installed
```

Esta información resulta útil durante tareas de auditoría y mantenimiento.

---

### Ejemplo práctico

Un administrador necesita instalar un servidor web.

Procedimiento:

```text
Actualizar repositorios

↓

Buscar el paquete

↓

Instalar la aplicación

↓

Verificar la instalación

↓

Iniciar el servicio
```

Tras finalizar el proceso, el servidor web queda preparado para su utilización.

---

[⬆️ Volver al índice](#índice)

## Administración remota mediante SSH

Introducción

La administración remota permite gestionar un sistema Linux desde otro equipo sin necesidad de acceder físicamente a él. El protocolo más utilizado para esta finalidad es **SSH (Secure Shell)**, que proporciona una comunicación cifrada y segura entre el cliente y el servidor.

Gracias a SSH, los administradores pueden configurar servidores, ejecutar comandos, transferir archivos y realizar tareas de mantenimiento desde cualquier ubicación con acceso a la red.

---

### ¿Qué es SSH?

**SSH (Secure Shell)** es un protocolo de comunicación que permite acceder de forma remota a un sistema mediante una conexión cifrada.

Sus principales funciones son:

- Administración remota.
- Ejecución de comandos.
- Transferencia segura de archivos.
- Tunelización de conexiones.
- Automatización de tareas.

SSH sustituye a protocolos antiguos como Telnet, que transmitían la información sin cifrar.

---

### Funcionamiento

El proceso de una conexión SSH puede representarse así:

```text
Cliente SSH

↓

Conexión cifrada

↓

Servidor SSH

↓

Ejecución de comandos
```

Toda la comunicación viaja cifrada, garantizando la confidencialidad de los datos.

---

### Servicio SSH

En Linux, el acceso remoto suele gestionarse mediante el servicio:

```text
sshd
```

Este servicio permanece en ejecución esperando conexiones de clientes autorizados.

---

### Conectarse mediante SSH

Para iniciar una conexión remota se utiliza:

```bash
ssh usuario@servidor
```

Ejemplo:

```bash
ssh admin@192.168.1.100
```

Tras introducir la contraseña o autenticarse mediante una clave, el usuario obtiene acceso al sistema remoto.

---

### Transferencia de archivos

SSH permite copiar archivos entre equipos de forma segura.

Una de las herramientas más utilizadas es:

```bash
scp
```

Ejemplo:

```bash
scp archivo.txt usuario@192.168.1.100:/home/usuario
```

Este comando copia el archivo al servidor remoto utilizando una conexión cifrada.

---

### Autenticación mediante claves

Además de la autenticación mediante contraseña, SSH permite utilizar pares de claves criptográficas.

El proceso es:

```text
Generar clave

↓

Copiar clave pública al servidor

↓

Autenticación automática

↓

Acceso seguro
```

Este método es más seguro y evita introducir la contraseña en cada conexión.

---

### Archivo de configuración

La configuración principal del servidor SSH suele encontrarse en:

```text
/etc/ssh/sshd_config
```

Desde este archivo es posible configurar aspectos como:

- Puerto de escucha.
- Métodos de autenticación.
- Usuarios permitidos.
- Acceso del usuario root.

Cualquier modificación requiere reiniciar el servicio para que los cambios surtan efecto.

---

### Reiniciar el servicio

Tras modificar la configuración puede reiniciarse el servicio mediante:

```bash
sudo systemctl restart ssh
```

Es recomendable comprobar siempre que el servicio continúa funcionando correctamente después de aplicar cambios.

---

### Ejemplo práctico

Un administrador necesita configurar un servidor situado en otra sede.

Procedimiento:

```text
Iniciar conexión SSH

↓

Autenticarse

↓

Ejecutar tareas administrativas

↓

Guardar cambios

↓

Cerrar la sesión
```

Gracias a SSH es posible administrar el servidor sin necesidad de desplazarse físicamente.

---

[⬆️ Volver al índice](#índice)