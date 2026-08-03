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
- [Casos prácticos](#casos-prácticos)

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

### Buenas prácticas

Para administrar correctamente un sistema Linux se recomienda:

- Comprender la función de cada componente.
- Mantener actualizado el kernel.
- Instalar únicamente los servicios necesarios.
- Supervisar el consumo de recursos.
- Documentar los cambios realizados en el sistema.

Estas medidas facilitan el mantenimiento y mejoran la estabilidad del sistema operativo.

---

[⬆️ Volver al índice](#índice)