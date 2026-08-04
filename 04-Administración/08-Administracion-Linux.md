# Administración de Linux 

## Introducción

Linux es uno de los sistemas operativos más utilizados en servidores, centros de datos, dispositivos de red y plataformas en la nube debido a su estabilidad, seguridad y flexibilidad.

## Índice

- [Arquitectura básica de Linux](#arquitectura-basica-de-linux)
- [Sistema de archivos en Linux](#sistema-de-archivos-en-linux)
- [Gestión de usuarios y grupos](#gestion-de-usuarios-y-grupos)
- [Gestión de permisos](#gestion-de-permisos)
- [Administración de procesos](#administracion-de-procesos)
- [Gestión de servicios con systemd](#gestion-de-servicios-con-systemd)
- [Administración del almacenamiento](#administracion-del-almacenamiento)
- [Administración de red](#administracion-de-red)
- [Gestión de paquetes](#gestion-de-paquetes)
- [Administración remota mediante SSH](#administracion-remota-mediante-ssh)

---

## Arquitectura básica de Linux

*La arquitectura de Linux está formada por varios elementos fundamentales.*

**Conceptos clave:**

- **Arquitectura general:** La relación entre los distintos componentes puede representarse de la siguiente forma.
- **Hardware:** El hardware constituye la parte física del sistema.
- **Kernel:** El kernel es el núcleo del sistema operativo y uno de los componentes más importantes de Linux.
- **Espacio de usuario:** El espacio de usuario es la zona donde se ejecutan los programas utilizados por los usuarios.
- **Shell:** La Shell es el intérprete de comandos que permite al usuario interactuar con el sistema operativo.
- **Aplicaciones:** Las aplicaciones son los programas que utilizan los usuarios para realizar distintas tareas.
- **Comunicación entre componentes:** El funcionamiento general del sistema puede resumirse así.
- **Características de la arquitectura Linux:** La arquitectura de Linux presenta diversas ventajas.

## Sistema de archivos en Linux

*El sistema de archivos de Linux organiza toda la información almacenada en discos y otros dispositivos mediante una estructura jerárquica en forma de árbol.*

**Conceptos clave:**

- **Estructura jerárquica:** En Linux todos los archivos y directorios dependen de un único directorio principal denominado raíz.
- **Directorio raíz (/):** El directorio / constituye el punto de inicio del sistema de archivos.
- **Directorio /home:** El directorio /home almacena los directorios personales de los usuarios.
- **Directorio /etc:** El directorio /etc contiene la mayoría de los archivos de configuración del sistema.
- **Directorios /bin y /sbin:** Estos directorios contienen los ejecutables esenciales del sistema.
- **Directorio /var:** El directorio /var almacena información que cambia frecuentemente.
- **Directorio /tmp:** El directorio /tmp se utiliza para almacenar archivos temporales.
- **Directorio /usr:** El directorio /usr contiene gran parte de las aplicaciones y bibliotecas instaladas.
- **Directorios /dev, /proc y /sys:** Estos directorios permiten acceder a información relacionada con el hardware y el funcionamiento interno del sistema.

### Navegación por el sistema de archivos

*Algunos comandos habituales son.*

```bash
pwd
```
```bash
ls
```

---

**Conceptos clave:**

- **Ejemplo práctico:** Un administrador necesita localizar el archivo de configuración de un servicio.

## Gestión de usuarios y grupos

*Linux es un sistema operativo multiusuario, lo que significa que varias personas pueden utilizar el mismo sistema de forma simultánea, cada una con su propia cuenta y permisos.*

**Conceptos clave:**

- **Usuarios en Linux:** Un usuario representa una identidad dentro del sistema operativo.
- **Tipos de usuarios:** En Linux pueden encontrarse distintos tipos de usuarios.
- **Usuario root:** El usuario root posee privilegios completos sobre el sistema.
- **Usuarios normales:** Los usuarios normales son las cuentas utilizadas por las personas que trabajan con el sistema.
- **Grupos:** Un grupo permite reunir varios usuarios para administrar permisos de forma conjunta.
- **Archivos de configuración:** La información de usuarios y grupos se almacena principalmente en.

### Creación de usuarios

*Para crear un nuevo usuario puede utilizarse.*

```bash
sudo useradd usuario
```
```bash
sudo adduser usuario
```

---

### Gestión de grupos

*Para crear un grupo.*

```bash
sudo groupadd desarrollo
```
```bash
sudo usermod -aG desarrollo usuario
```

---

### Consultar información

*Algunos comandos útiles son.*

```bash
whoami
```
```bash
groups
```

---

**Conceptos clave:**

- **Ejemplo práctico:** Un nuevo empleado se incorpora al departamento de informática.

## Gestión de permisos

*Uno de los aspectos más importantes de la administración de Linux es el control de acceso a los archivos y directorios.*

**Conceptos clave:**

- **¿Qué son los permisos?:** Los permisos indican las acciones que un usuario puede realizar sobre un archivo o directorio.

### Tipos de permisos

*Linux utiliza tres permisos básicos.*

| Permiso | Símbolo | Función |
|----------|---------|---------|
| Lectura | **r** | Permite visualizar el contenido. |
| Escritura | **w** | Permite modificar el contenido. |
| Ejecución | **x** | Permite ejecutar un archivo o acceder a un directorio. |

---

**Conceptos clave:**

- **Propietario, grupo y otros:** Los permisos se asignan a tres categorías de usuarios.
- **Representación de permisos:** Los permisos suelen mostrarse mediante una secuencia de caracteres.

### Permisos numéricos

*Los permisos también pueden expresarse mediante valores numéricos.*

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

---

### Cambiar permisos

*Para modificar los permisos se utiliza.*

```bash
chmod
```
```bash
chmod 755 script.sh
```

---

### Cambiar propietario

*Para modificar el propietario de un archivo se utiliza.*

```bash
chown
```
```bash
sudo chown usuario archivo.txt
```

---

### Cambiar grupo

*Para modificar el grupo asociado a un archivo se utiliza.*

```bash
chgrp
```
```bash
sudo chgrp desarrollo proyecto.txt
```

---

**Conceptos clave:**

- **Permisos en directorios:** En los directorios, los permisos tienen un significado específico.

### Ejemplo práctico

*Un administrador necesita permitir la ejecución de un script únicamente a su propietario.*

```bash
chmod 700 script.sh
```

---

## Administración de procesos

*Un proceso es una instancia de un programa que se encuentra en ejecución.*

**Conceptos clave:**

- **¿Qué es un proceso?:** Un proceso representa un programa que está siendo ejecutado por el sistema operativo.
- **Identificador del proceso (PID):** Cada proceso recibe un número denominado PID (Process ID).
- **Estados de un proceso:** Durante su ciclo de vida un proceso puede encontrarse en distintos estados.

### Consultar procesos

*Para visualizar los procesos en ejecución pueden utilizarse distintos comandos.*

```bash
ps
```
```bash
ps -ef
```

---

### Supervisión en tiempo real

*Linux dispone de herramientas para observar los procesos mientras se ejecutan.*

```bash
top
```
```bash
htop
```

---

### Finalizar procesos

*Cuando una aplicación deja de responder puede ser necesario finalizar su ejecución.*

```bash
kill PID
```
```bash
kill -9 PID
```

---

### Buscar procesos

*Es posible localizar un proceso concreto utilizando.*

```bash
pgrep nombre
```
```bash
pidof nombre
```

---

### Prioridad de procesos

*Linux permite modificar la prioridad con la que un proceso utiliza la CPU.*

```bash
nice
```
```bash
renice
```

---

### Procesos en segundo plano

*Linux permite ejecutar programas en segundo plano para continuar utilizando la terminal.*

```bash
comando &
```
```bash
jobs
```

---

**Conceptos clave:**

- **Ejemplo práctico:** Un servidor presenta un consumo elevado de CPU.

## Gestión de servicios con systemd

*En la mayoría de las distribuciones Linux modernas, systemd es el sistema encargado de iniciar el sistema operativo y administrar los servicios.*

**Conceptos clave:**

- **¿Qué es systemd?:** systemd es el gestor de servicios e inicialización utilizado por la mayoría de distribuciones Linux.
- **¿Qué es un servicio?:** Un servicio es un programa que se ejecuta en segundo plano para proporcionar una determinada funcionalidad al sistema o a los usuarios.
- **Unidades de systemd:** Systemd organiza los recursos mediante unidades (*units*).

### Consultar el estado de un servicio

*Para conocer el estado de un servicio se utiliza.*

```bash
systemctl status nombre_servicio
```
```bash
systemctl status ssh
```

---

### Iniciar un servicio

*Para iniciar un servicio.*

```bash
sudo systemctl start nombre_servicio
```
```bash
sudo systemctl start apache2
```

---

### Detener un servicio

*Para detener un servicio.*

```bash
sudo systemctl stop nombre_servicio
```
```bash
sudo systemctl stop apache2
```

---

### Reiniciar un servicio

*Cuando un servicio presenta problemas suele ser suficiente con reiniciarlo.*

```bash
sudo systemctl restart nombre_servicio
```

---

### Habilitar el inicio automático

*Para que un servicio se inicie automáticamente al arrancar el sistema.*

```bash
sudo systemctl enable nombre_servicio
```
```bash
sudo systemctl enable ssh
```

---

### Deshabilitar el inicio automático

*Si no se desea que un servicio arranque con el sistema.*

```bash
sudo systemctl disable nombre_servicio
```

---

### Consultar los registros

*Systemd integra un sistema de registros denominado journal.*

```bash
journalctl
```
```bash
journalctl -u ssh
```

---

**Conceptos clave:**

- **Ejemplo práctico:** Un servidor web deja de responder.

## Administración del almacenamiento

*El almacenamiento constituye uno de los recursos más importantes de cualquier sistema Linux.*

**Conceptos clave:**

- **Dispositivos de almacenamiento:** Linux identifica los dispositivos de almacenamiento mediante archivos especiales ubicados en el directorio.
- **Particiones:** Una partición representa una división lógica de un disco físico.
- **Sistemas de archivos:** Antes de utilizar una partición es necesario formatearla con un sistema de archivos.

### Consultar discos y particiones

*Para visualizar los dispositivos disponibles puede utilizarse.*

```bash
lsblk
```

---

### Consultar el espacio disponible

*Para comprobar el uso del almacenamiento se utiliza.*

```bash
df -h
```

---

### Consultar el tamaño de directorios

*Cuando es necesario localizar qué directorios ocupan más espacio puede utilizarse.*

```bash
du -sh directorio
```
```bash
du -sh /var
```

---

**Conceptos clave:**

- **Montaje de sistemas de archivos:** Antes de acceder a una partición es necesario montarla en un directorio.

### Consultar sistemas montados

*Para visualizar los sistemas de archivos actualmente montados puede utilizarse.*

```bash
mount
```
```bash
findmnt
```

---

**Conceptos clave:**

- **Archivo fstab:** El archivo.
- **Ejemplo práctico:** Un servidor comienza a funcionar lentamente por falta de espacio.

## Administración de red

**Conceptos clave:**

- **Interfaces de red:** Una interfaz de red representa el dispositivo que permite la comunicación entre el sistema y la red.

### Consultar interfaces

*Para mostrar las interfaces disponibles puede utilizarse.*

```bash
ip link
```

---

### Consultar direcciones IP

*Para visualizar la configuración IP se utiliza.*

```bash
ip addr
```

---

### Comprobar la conectividad

*Para verificar la comunicación con otro equipo se emplea.*

```bash
ping
```
```bash
ping 8.8.8.8
```

---

### Comprobar rutas

*La tabla de enrutamiento puede consultarse mediante.*

```bash
ip route
```

---

### Resolución de nombres

*Para comprobar la resolución DNS pueden utilizarse herramientas como.*

```bash
nslookup
```
```bash
dig
```

---

### Comprobar conexiones

*Para visualizar las conexiones activas del sistema puede utilizarse.*

```bash
ss
```
```bash
ss -tuln
```

---

### Reiniciar la red

*En algunas distribuciones es posible reiniciar el servicio de red mediante.*

```bash
sudo systemctl restart NetworkManager
```

---

**Conceptos clave:**

- **Archivos de configuración:** La configuración de red puede almacenarse en diferentes ubicaciones según la distribución Linux.
- **Ejemplo práctico:** Un servidor no puede acceder a Internet.

## Gestión de paquetes

*La instalación, actualización y eliminación de software es una de las tareas más habituales en la administración de sistemas Linux.*

**Conceptos clave:**

- **¿Qué es un paquete?:** Un paquete es un archivo que contiene todo lo necesario para instalar una aplicación o componente del sistema.

### Gestores de paquetes

*Existen diferentes gestores de paquetes según la distribución Linux.*

| Distribución | Gestor de paquetes |
|---------------|--------------------|
| Debian / Ubuntu | APT |
| Fedora | DNF |
| CentOS / Rocky Linux | DNF |
| openSUSE | Zypper |
| Arch Linux | Pacman |

---

**Conceptos clave:**

- **Repositorios:** Los repositorios son servidores que almacenan miles de paquetes de software organizados y mantenidos por la comunidad o por los fabricantes de las distribuciones.

### Actualizar la información de los repositorios

*En distribuciones basadas en Debian es habitual actualizar primero la información disponible.*

```bash
sudo apt update
```

---

### Instalar software

*Para instalar una aplicación mediante APT se utiliza.*

```bash
sudo apt install nombre_paquete
```
```bash
sudo apt install nginx
```

---

### Actualizar el sistema

*Para instalar las actualizaciones disponibles.*

```bash
sudo apt upgrade
```

---

### Eliminar paquetes

*Para desinstalar una aplicación.*

```bash
sudo apt remove nombre_paquete
```
```bash
sudo apt purge nombre_paquete
```

---

### Buscar paquetes

*Es posible localizar aplicaciones disponibles mediante.*

```bash
apt search nombre
```
```bash
apt search apache
```

---

### Consultar paquetes instalados

*Para obtener un listado del software instalado puede utilizarse.*

```bash
apt list --installed
```

---

**Conceptos clave:**

- **Ejemplo práctico:** Un administrador necesita instalar un servidor web.

## Administración remota mediante SSH

*La administración remota permite gestionar un sistema Linux desde otro equipo sin necesidad de acceder físicamente a él.*

**Conceptos clave:**

- **¿Qué es SSH?:** SSH (Secure Shell) es un protocolo de comunicación que permite acceder de forma remota a un sistema mediante una conexión cifrada.
- **Funcionamiento:** El proceso de una conexión SSH puede representarse así.
- **Servicio SSH:** En Linux, el acceso remoto suele gestionarse mediante el servicio.

### Conectarse mediante SSH

*Para iniciar una conexión remota se utiliza.*

```bash
ssh usuario@servidor
```
```bash
ssh admin@192.168.1.100
```

---

### Transferencia de archivos

*SSH permite copiar archivos entre equipos de forma segura.*

```bash
scp
```
```bash
scp archivo.txt usuario@192.168.1.100:/home/usuario
```

---

**Conceptos clave:**

- **Autenticación mediante claves:** Además de la autenticación mediante contraseña, SSH permite utilizar pares de claves criptográficas.
- **Archivo de configuración:** La configuración principal del servidor SSH suele encontrarse en.

### Reiniciar el servicio

*Tras modificar la configuración puede reiniciarse el servicio mediante.*

```bash
sudo systemctl restart ssh
```

---

**Conceptos clave:**

- **Ejemplo práctico:** Un administrador necesita configurar un servidor situado en otra sede.

[⬆️ Volver al índice](#índice)
