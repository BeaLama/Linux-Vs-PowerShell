# 11 - Recuperación del sistema

## Introducción

La recuperación del sistema comprende el conjunto de procedimientos y herramientas destinados a restaurar el funcionamiento de un equipo o servidor tras un fallo grave. Estos fallos pueden deberse a errores de hardware, corrupción del sistema operativo, malware, configuraciones incorrectas o desastres que impidan el funcionamiento normal de la infraestructura.

En este apartado se estudian las técnicas de recuperación utilizadas tanto en Windows como en Linux, los distintos modos de recuperación, herramientas disponibles, procedimientos de restauración y buenas prácticas para minimizar el tiempo de inactividad y garantizar la continuidad del servicio.

---

## Índice

- [Fundamentos de la recuperación del sistema](#fundamentos-de-la-recuperación-del-sistema)
- [Recuperación del arranque](#recuperación-del-arranque)
- [Herramientas de recuperación en Windows](#herramientas-de-recuperación-en-windows)
- [Herramientas de recuperación en Linux](#herramientas-de-recuperación-en-linux)
- [Recuperación de servicios y aplicaciones](#recuperación-de-servicios-y-aplicaciones)
- [Recuperación desde copias de seguridad](#recuperación-desde-copias-de-seguridad)
- [Recuperación ante desastres (Disaster Recovery)](#recuperación-ante-desastres-disaster-recovery)
- [Pruebas y validación de la recuperación](#pruebas-y-validación-de-la-recuperación)
- [Buenas prácticas](#buenas-prácticas)

---

## Fundamentos de la recuperación del sistema

La recuperación del sistema comprende el conjunto de procedimientos, herramientas y técnicas destinados a restaurar el funcionamiento normal de un equipo o servidor tras un fallo que impide su uso total o parcial.

Estos fallos pueden afectar al sistema operativo, al proceso de arranque, a los servicios, a las aplicaciones o a los propios datos. El objetivo de la recuperación es minimizar el tiempo de inactividad, reducir la pérdida de información y devolver el sistema a un estado operativo lo antes posible.

Una correcta estrategia de recuperación forma parte del plan de continuidad del negocio y debe estar preparada antes de que ocurra cualquier incidente.

---

### ¿Qué es la recuperación del sistema?

La recuperación del sistema consiste en devolver un equipo o servidor a un estado funcional tras una incidencia.

Proceso:

```text
Sistema operativo

↓

Fallo

↓

Diagnóstico

↓

Recuperación

↓

Sistema operativo
```

Dependiendo del problema, la recuperación puede implicar desde reiniciar un servicio hasta reconstruir completamente un servidor.

---

### Objetivos de la recuperación

Los principales objetivos son:

- Restaurar la disponibilidad del sistema.
- Recuperar la información.
- Reducir el tiempo de inactividad.
- Minimizar la pérdida de datos.
- Garantizar la continuidad del servicio.
- Evitar que el problema vuelva a repetirse.

Una recuperación eficaz busca resolver el incidente con el menor impacto posible para los usuarios.

---

### ¿Cuándo es necesaria una recuperación?

Las situaciones más habituales son:

- Fallo del sistema operativo.
- Corrupción del arranque.
- Eliminación accidental de archivos del sistema.
- Actualizaciones fallidas.
- Malware o ransomware.
- Errores de configuración.
- Averías de hardware.
- Corrupción del sistema de archivos.

Cada tipo de incidencia requiere un procedimiento de recuperación diferente.

---

### Tipos de recuperación

Dependiendo del alcance del problema, la recuperación puede clasificarse en:

- Recuperación del arranque.
- Recuperación del sistema operativo.
- Recuperación de aplicaciones.
- Recuperación de servicios.
- Recuperación de datos.
- Recuperación completa del servidor.

No todas las incidencias requieren reinstalar el sistema.

---

### Recuperación lógica y recuperación física

Las incidencias pueden dividirse en dos grandes grupos.

#### Recuperación lógica

Se produce cuando el hardware funciona correctamente, pero existe un problema de software.

Ejemplos:

- Archivos dañados.
- Configuración incorrecta.
- Servicios detenidos.
- Malware.
- Errores del sistema operativo.

---

#### Recuperación física

Está relacionada con averías de hardware.

Ejemplos:

- Disco duro averiado.
- Memoria RAM defectuosa.
- Fuente de alimentación dañada.
- Controladora RAID averiada.

En estos casos suele ser necesario sustituir componentes antes de restaurar el sistema.

---

### Fases de una recuperación

Toda recuperación debería seguir un proceso estructurado.

```text
Detectar incidencia

↓

Analizar causa

↓

Contener el problema

↓

Recuperar sistema

↓

Validar funcionamiento

↓

Documentar
```

Seguir una metodología reduce errores y acelera la recuperación.

---

### Prioridad de los sistemas

No todos los sistemas tienen la misma importancia.

Ejemplo:

| Prioridad | Sistemas |
|-----------|----------|
| Crítica | Active Directory, ERP, Bases de datos |
| Alta | Servidores de archivos |
| Media | Aplicaciones internas |
| Baja | Equipos de usuario |

Durante una incidencia deben recuperarse primero los servicios más críticos.

---

### Tiempo de recuperación

La velocidad de recuperación depende de factores como:

- Tipo de fallo.
- Disponibilidad de copias.
- Estado del hardware.
- Automatización.
- Complejidad del sistema.

Una buena planificación reduce considerablemente el tiempo necesario.

---

### Relación con RPO y RTO

La recuperación debe cumplir los objetivos definidos previamente.

**RPO (Recovery Point Objective)**

Indica la cantidad máxima de datos que puede perder la organización.

Ejemplo:

```text
RPO = 30 minutos
```

---

**RTO (Recovery Time Objective)**

Representa el tiempo máximo permitido para restaurar el servicio.

Ejemplo:

```text
RTO = 2 horas
```

Estos valores determinan cómo debe diseñarse la estrategia de recuperación.

---

### Importancia del diagnóstico

Antes de comenzar cualquier recuperación conviene identificar correctamente la causa del problema.

Un diagnóstico incorrecto puede:

- Agravar la incidencia.
- Provocar pérdida de datos.
- Aumentar el tiempo de recuperación.

Por ello, siempre debe analizarse la situación antes de aplicar soluciones.

---

### Documentación

Toda organización debería disponer de procedimientos documentados.

Estos documentos suelen incluir:

- Pasos de recuperación.
- Herramientas necesarias.
- Responsables.
- Prioridad de los servicios.
- Tiempos estimados.
- Contactos.

Una documentación clara facilita enormemente la actuación durante una emergencia.

---

### Comparativa

| Concepto | Objetivo |
|----------|----------|
| Recuperación | Restaurar el funcionamiento del sistema |
| Diagnóstico | Identificar la causa del fallo |
| Backup | Recuperar datos perdidos |
| Continuidad del negocio | Mantener los servicios disponibles |
| Disaster Recovery | Recuperar la infraestructura tras un desastre |

---

### Buenas prácticas

- Sigue siempre un procedimiento estructurado antes de intervenir.
- Identifica correctamente la causa del problema antes de aplicar soluciones.
- Prioriza la recuperación de los servicios críticos.
- Documenta todas las actuaciones realizadas durante la incidencia.
- Mantén actualizados los procedimientos de recuperación.
- Define claramente los objetivos de RPO y RTO.
- Comprueba el correcto funcionamiento del sistema una vez finalizada la recuperación.
- Analiza posteriormente la causa raíz para evitar que el problema vuelva a producirse.

---

[⬆️ Volver al índice](#índice)

## Recuperación del arranque

El proceso de arranque es el conjunto de etapas que permiten cargar el sistema operativo desde que el equipo recibe alimentación hasta que el usuario puede iniciar sesión.

Cuando alguno de los componentes implicados falla, el sistema puede dejar de arrancar completamente o quedarse bloqueado durante el inicio.

La recuperación del arranque tiene como objetivo reparar estos componentes sin necesidad de reinstalar el sistema operativo.

---

### Fases del arranque

Aunque existen diferencias entre Windows y Linux, el proceso general suele seguir estas etapas:

```text
Encendido

↓

Firmware (BIOS/UEFI)

↓

Dispositivo de arranque

↓

Bootloader

↓

Kernel

↓

Servicios

↓

Inicio de sesión
```

Un fallo en cualquiera de estas fases puede impedir el arranque del sistema.

---

### Componentes del arranque

Los elementos principales que intervienen son:

- BIOS o UEFI.
- Disco de arranque.
- Partición EFI (en sistemas UEFI).
- Gestor de arranque (Bootloader).
- Kernel.
- Sistema de archivos.
- Servicios iniciales.

Conocer estos componentes facilita la localización del problema.

---

### Problemas habituales

Entre las incidencias más frecuentes se encuentran:

- Disco de arranque no encontrado.
- Bootloader dañado.
- Partición EFI corrupta.
- Archivos del sistema eliminados.
- Actualizaciones fallidas.
- Corrupción del sistema de archivos.
- Fallos del disco duro.
- Configuración incorrecta del firmware.

Cada uno requiere un procedimiento de recuperación específico.

---

### BIOS y UEFI

El firmware del equipo es el encargado de iniciar el proceso de arranque.

Las funciones principales son:

- Detectar el hardware.
- Inicializar los dispositivos.
- Buscar un dispositivo de arranque.
- Ejecutar el gestor de arranque.

Si la secuencia de arranque es incorrecta, el sistema operativo nunca llegará a iniciarse.

---

### Verificación del orden de arranque

Uno de los primeros pasos consiste en comprobar que el firmware intenta arrancar desde el disco correcto.

Ejemplo:

```text
1. SSD principal

2. Disco USB

3. Red (PXE)
```

Una configuración incorrecta puede provocar errores como:

```text
No bootable device
```

---

### Bootloader

El **bootloader** es el programa encargado de cargar el sistema operativo.

Los más habituales son:

**Windows**

- Windows Boot Manager.

**Linux**

- GRUB.
- systemd-boot.
- LILO (prácticamente en desuso).

Si el bootloader se daña, el sistema dejará de arrancar aunque el sistema operativo siga intacto.

---

### Problemas en el Bootloader

Los síntomas más habituales son:

- Pantalla negra.
- Mensajes de "Bootmgr is missing".
- Error de GRUB.
- Reinicios continuos.
- Sistema operativo no encontrado.

En muchos casos basta con reconstruir el gestor de arranque.

---

### Partición EFI

Los equipos modernos utilizan UEFI y una **partición EFI (ESP)**.

Contiene:

- Gestores de arranque.
- Archivos EFI.
- Configuración de inicio.

Si esta partición se elimina o se corrompe, el sistema no podrá arrancar.

---

### Sistema de archivos

El sistema operativo necesita acceder correctamente al sistema de archivos durante el arranque.

Si existen errores importantes pueden aparecer síntomas como:

- Pantalla negra.
- Kernel panic.
- Bucle de reinicios.
- Servicios que no llegan a iniciarse.

Por ello suele ser necesario comprobar la integridad del disco.

---

### Recuperación automática

Los sistemas operativos modernos incorporan herramientas capaces de detectar determinados problemas de arranque.

Ejemplos:

- Reparación automática de Windows.
- GRUB Rescue.
- Modo Rescue de Linux.

Estas herramientas solucionan incidencias sencillas sin intervención manual.

---

### Recuperación manual

Cuando la reparación automática no funciona, puede ser necesario actuar manualmente.

Las tareas habituales incluyen:

- Reconstruir el gestor de arranque.
- Reparar el sistema de archivos.
- Restaurar archivos del sistema.
- Reconfigurar el firmware.
- Recuperar la partición EFI.

Estas operaciones requieren un mayor conocimiento del sistema.

---

### Recuperación desde un medio externo

En muchos casos es necesario arrancar el equipo mediante:

- USB de instalación.
- DVD de recuperación.
- Live USB Linux.
- Entorno WinRE.

Proceso:

```text
USB recuperación

↓

Arranque

↓

Diagnóstico

↓

Reparación
```

Este procedimiento permite acceder al sistema incluso cuando el disco principal no puede iniciarse.

---

### Verificación tras la reparación

Una vez finalizada la recuperación conviene comprobar:

- Que el sistema inicia correctamente.
- Que todos los discos son detectados.
- Que los servicios arrancan.
- Que los usuarios pueden iniciar sesión.
- Que no existen errores en los registros del sistema.

La reparación no debe darse por concluida hasta validar el funcionamiento completo.

---

### Comparativa

| Problema | Posible solución |
|-----------|------------------|
| Disco no detectado | Revisar BIOS/UEFI |
| Orden de arranque incorrecto | Configurar Boot Order |
| Bootloader dañado | Reconstruir gestor de arranque |
| Partición EFI corrupta | Reparar o recrear la partición |
| Sistema de archivos corrupto | Reparar el sistema de archivos |
| Archivos del sistema dañados | Restaurar archivos del sistema |

---

### Buenas prácticas

- Comprueba primero la configuración del BIOS o UEFI antes de realizar cambios más complejos.
- Mantén siempre disponible un medio de recuperación actualizado.
- No reinstales el sistema operativo sin intentar previamente reparar el arranque.
- Realiza diagnósticos antes de modificar particiones o el gestor de arranque.
- Comprueba el estado físico del disco si aparecen errores repetitivos durante el inicio.
- Documenta todas las actuaciones realizadas durante la recuperación.
- Verifica el funcionamiento completo del sistema tras reparar el arranque.
- Mantén copias de seguridad actualizadas para poder restaurar el sistema en caso de fallo irreversible.

---

[⬆️ Volver al índice](#índice)

## Herramientas de recuperación en Windows

Windows incorpora un amplio conjunto de herramientas destinadas a diagnosticar y reparar problemas que impiden el funcionamiento normal del sistema operativo. Estas utilidades permiten solucionar incidencias relacionadas con el arranque, los archivos del sistema, el almacenamiento, las actualizaciones o la configuración del sistema sin necesidad de reinstalar completamente el equipo.

Conocer estas herramientas resulta imprescindible para cualquier administrador de sistemas Windows.

---

### Windows Recovery Environment (WinRE)

**Windows Recovery Environment (WinRE)** es el entorno de recuperación integrado en Windows.

Permite acceder a diferentes herramientas de reparación cuando el sistema operativo no puede iniciarse correctamente.

Proceso:

```text
Equipo

↓

WinRE

↓

Diagnóstico

↓

Reparación
```

Normalmente se inicia automáticamente tras varios intentos fallidos de arranque o desde un medio de instalación.

---

### Opciones disponibles en WinRE

Entre las funciones más importantes se encuentran:

- Reparación de inicio.
- Restaurar sistema.
- Recuperación desde imagen.
- Símbolo del sistema.
- Configuración de inicio.
- Desinstalar actualizaciones.

Estas herramientas permiten resolver la mayoría de incidencias relacionadas con el sistema operativo.

---

### Reparación de inicio

La **Reparación de inicio** analiza automáticamente el proceso de arranque e intenta corregir errores comunes.

Puede solucionar problemas relacionados con:

- Archivos de arranque.
- Configuración BCD.
- Windows Boot Manager.
- Archivos del sistema.

Es la primera opción que debería probarse cuando Windows no inicia correctamente.

---

### Restaurar sistema

**Restaurar sistema** permite volver a un punto de restauración anterior.

Proceso:

```text
Estado actual

↓

Punto de restauración

↓

Sistema recuperado
```

Esta herramienta:

- No elimina documentos personales.
- Revierte configuraciones.
- Desinstala controladores y programas instalados posteriormente.

Es especialmente útil tras actualizaciones o instalaciones problemáticas.

---

### Recuperación desde imagen del sistema

Si se dispone de una imagen completa del sistema, es posible restaurar el equipo exactamente al estado en que se encontraba cuando se creó dicha imagen.

Proceso:

```text
Imagen del sistema

↓

Restauración

↓

Equipo operativo
```

Esta opción sobrescribe completamente el contenido del disco.

---

### Símbolo del sistema

WinRE permite acceder al **Símbolo del sistema (CMD)** para ejecutar comandos de diagnóstico y reparación.

Desde esta consola pueden utilizarse numerosas herramientas avanzadas.

---

### CHKDSK

**CHKDSK (Check Disk)** analiza el sistema de archivos y detecta errores en el disco.

Ejemplo:

```cmd
chkdsk C: /f /r
```

Parámetros habituales:

- `/f` Corrige errores del sistema de archivos.
- `/r` Localiza sectores defectuosos e intenta recuperar la información.

Es recomendable ejecutarlo cuando existen sospechas de corrupción del disco.

---

### SFC (System File Checker)

**SFC** comprueba la integridad de los archivos protegidos del sistema.

Ejemplo:

```cmd
sfc /scannow
```

Si detecta archivos dañados, intentará restaurarlos automáticamente desde la caché del sistema.

---

### DISM

**DISM (Deployment Image Servicing and Management)** repara la imagen del sistema operativo utilizada por Windows.

Ejemplo:

```cmd
DISM /Online /Cleanup-Image /RestoreHealth
```

Normalmente se utiliza cuando **SFC** no consigue reparar determinados archivos.

Una práctica habitual consiste en ejecutar:

```text
DISM

↓

SFC
```

---

### Bootrec

**Bootrec** permite reparar el proceso de arranque.

Comandos habituales:

```cmd
bootrec /fixmbr
```

```cmd
bootrec /fixboot
```

```cmd
bootrec /scanos
```

```cmd
bootrec /rebuildbcd
```

Estas opciones permiten reconstruir el gestor de arranque cuando está dañado.

---

### BCD

El **Boot Configuration Data (BCD)** almacena la configuración de arranque de Windows.

Si el BCD está corrupto pueden aparecer errores como:

```text
Boot Configuration Data file is missing
```

En estos casos suele ser necesario reconstruirlo mediante **Bootrec** o **BCDBoot**.

---

### BCDBoot

**BCDBoot** permite recrear los archivos de arranque.

Ejemplo:

```cmd
bcdboot C:\Windows
```

Se utiliza principalmente cuando la partición EFI ha perdido los archivos necesarios para iniciar Windows.

---

### Configuración de inicio

Desde WinRE también es posible modificar el modo de inicio del sistema.

Entre las opciones disponibles se encuentran:

- Modo seguro.
- Modo seguro con funciones de red.
- Deshabilitar controladores firmados.
- Deshabilitar reinicio automático.

Estas opciones facilitan el diagnóstico de determinados problemas.

---

### Desinstalar actualizaciones

Una actualización defectuosa puede impedir el inicio del sistema.

WinRE permite eliminar:

- La última actualización de calidad.
- La última actualización de características.

Esta opción suele resolver muchos problemas tras grandes actualizaciones de Windows.

---

### Administrador de discos

Una vez iniciado el sistema también pueden utilizarse herramientas gráficas como **Administración de discos** para comprobar:

- Estado de los discos.
- Particiones.
- Letras de unidad.
- Espacio disponible.

---

### Visor de eventos

Tras recuperar el sistema conviene revisar el **Visor de eventos** para localizar la causa del problema.

Permite consultar:

- Errores del sistema.
- Servicios.
- Controladores.
- Aplicaciones.
- Eventos críticos.

Esta información resulta muy útil para evitar futuras incidencias.

---

### Comparativa

| Herramienta | Función |
|-------------|----------|
| WinRE | Entorno de recuperación |
| Reparación de inicio | Reparar el arranque automáticamente |
| Restaurar sistema | Volver a un estado anterior |
| CHKDSK | Reparar errores del disco |
| SFC | Restaurar archivos del sistema |
| DISM | Reparar la imagen de Windows |
| Bootrec | Reparar el gestor de arranque |
| BCDBoot | Reconstruir archivos de arranque |
| Visor de eventos | Analizar errores del sistema |

---

### Buenas prácticas

- Utiliza primero las herramientas automáticas de WinRE antes de aplicar soluciones manuales.
- Ejecuta **CHKDSK** cuando sospeches de problemas en el disco.
- Combina **DISM** y **SFC** para reparar archivos del sistema dañados.
- Mantén siempre un medio de instalación o recuperación actualizado.
- Crea puntos de restauración antes de realizar cambios importantes.
- Revisa el Visor de eventos tras recuperar el sistema para identificar la causa del fallo.
- No reconstruyas el gestor de arranque sin confirmar previamente que el problema está relacionado con él.
- Documenta todas las acciones realizadas durante la recuperación.

---

[⬆️ Volver al índice](#índice)

## Herramientas de recuperación en Linux

Linux dispone de numerosas herramientas para diagnosticar y recuperar sistemas dañados sin necesidad de reinstalar el sistema operativo. Muchas de ellas pueden utilizarse incluso cuando el sistema no consigue arrancar, gracias a los modos de rescate o a distribuciones Live.

La filosofía de Linux permite realizar la mayoría de las tareas de recuperación desde la línea de comandos, ofreciendo un gran control sobre el proceso.

---

### Modos de recuperación

La mayoría de distribuciones Linux incluyen modos especiales para realizar tareas de mantenimiento.

Los más habituales son:

- Recovery Mode.
- Rescue Mode.
- Emergency Mode.
- Live USB.

Cada uno proporciona un nivel distinto de acceso al sistema.

---

### Recovery Mode

El **Recovery Mode** permite iniciar el sistema con un conjunto mínimo de servicios.

Desde este modo es posible:

- Reparar paquetes.
- Comprobar discos.
- Obtener una consola de administrador.
- Reiniciar servicios.
- Modificar configuraciones.

Es uno de los métodos más utilizados para resolver incidencias.

---

### Rescue Mode

El **Rescue Mode** carga únicamente los servicios imprescindibles para acceder al sistema.

Proceso:

```text
Sistema

↓

Rescue Mode

↓

Administrador

↓

Diagnóstico
```

Resulta muy útil cuando el arranque normal falla debido a problemas de configuración.

---

### Emergency Mode

El **Emergency Mode** es el modo de recuperación más básico.

Solo carga:

- Kernel.
- Sistema de archivos raíz.
- Consola de administración.

No inicia servicios de red ni la mayoría de componentes del sistema.

Se utiliza cuando existen errores graves durante el arranque.

---

### Live USB

Una distribución Linux puede ejecutarse directamente desde un dispositivo USB.

Proceso:

```text
USB Live

↓

Arranque

↓

Acceso al disco

↓

Reparación
```

Permite trabajar sobre el sistema instalado aunque este no pueda iniciarse.

---

### GRUB

**GRUB (Grand Unified Bootloader)** es el gestor de arranque más utilizado en Linux.

Sus funciones principales son:

- Detectar sistemas operativos.
- Mostrar el menú de arranque.
- Cargar el kernel.
- Pasar parámetros al sistema operativo.

Si GRUB se daña, Linux dejará de arrancar.

---

### Problemas habituales de GRUB

Algunos errores frecuentes son:

```text
grub rescue>
```

```text
unknown filesystem
```

```text
error: no such partition
```

En muchos casos será necesario reinstalar o reconstruir GRUB.

---

### Reinstalar GRUB

Desde un entorno Live es posible reinstalar el gestor de arranque.

Ejemplo:

```bash
sudo grub-install /dev/sda
```

Posteriormente suele actualizarse la configuración:

```bash
sudo update-grub
```

Esto permite volver a detectar los sistemas operativos instalados.

---

### FSCK

**fsck (File System Check)** comprueba y repara errores en los sistemas de archivos.

Ejemplo:

```bash
sudo fsck /dev/sda1
```

Puede detectar:

- Inodos dañados.
- Errores de bloques.
- Corrupción del sistema de archivos.

Debe ejecutarse con la partición desmontada siempre que sea posible.

---

### Journalctl

**journalctl** permite consultar los registros generados por **systemd**.

Ejemplo:

```bash
journalctl -xb
```

Es una de las herramientas más útiles para investigar por qué un sistema no ha iniciado correctamente.

---

### Chroot

**chroot** permite acceder a un sistema instalado desde un entorno Live como si se hubiera iniciado normalmente.

Proceso:

```text
Live USB

↓

Montar partición

↓

chroot

↓

Sistema instalado
```

Esto facilita la reparación de configuraciones, paquetes o del propio GRUB.

---

### Systemctl

Cuando el sistema consigue arrancar parcialmente, **systemctl** permite comprobar el estado de los servicios.

Ejemplos:

```bash
systemctl status apache2
```

```bash
systemctl restart ssh
```

También es posible habilitar o deshabilitar servicios durante el inicio.

---

### Reparación de paquetes

En sistemas basados en Debian es posible reparar instalaciones incompletas.

Ejemplo:

```bash
sudo apt --fix-broken install
```

o

```bash
sudo dpkg --configure -a
```

Estas órdenes solucionan numerosos problemas tras actualizaciones interrumpidas.

---

### Reparación del sistema de archivos

Si el sistema de archivos presenta daños importantes puede ser necesario:

- Desmontar la partición.
- Ejecutar **fsck**.
- Reiniciar el sistema.
- Verificar los registros.

Nunca debe ejecutarse **fsck** sobre una partición montada en escritura.

---

### Recuperación de configuraciones

Muchas incidencias están relacionadas con archivos de configuración incorrectos.

Algunos ejemplos:

- `/etc/fstab`
- `/etc/network/interfaces`
- `/etc/ssh/sshd_config`
- `/etc/systemd/`

Desde un entorno de rescate es posible editar estos archivos y corregir los errores.

---

### Recuperación del kernel

Si un nuevo kernel provoca problemas, GRUB permite iniciar una versión anterior.

Proceso:

```text
GRUB

↓

Opciones avanzadas

↓

Kernel anterior

↓

Sistema operativo
```

Esto permite recuperar el acceso mientras se investiga la incidencia.

---

### Comparativa

| Herramienta | Función |
|-------------|----------|
| Recovery Mode | Recuperación básica |
| Rescue Mode | Diagnóstico con servicios mínimos |
| Emergency Mode | Recuperación mínima |
| Live USB | Reparación desde un sistema externo |
| GRUB | Gestor de arranque |
| fsck | Reparar sistemas de archivos |
| journalctl | Consultar registros |
| chroot | Acceder al sistema instalado |
| systemctl | Gestionar servicios |

---

### Buenas prácticas

- Mantén siempre un Live USB actualizado para tareas de recuperación.
- Revisa los registros con **journalctl** antes de realizar cambios importantes.
- Ejecuta **fsck** únicamente sobre particiones desmontadas siempre que sea posible.
- Conserva al menos una versión anterior del kernel instalada.
- Verifica cuidadosamente los cambios en archivos críticos como **fstab** antes de reiniciar.
- Documenta todas las modificaciones realizadas durante el proceso de recuperación.
- Utiliza **chroot** para reparar sistemas desde un entorno externo cuando el arranque falle.
- Comprueba el funcionamiento de todos los servicios tras completar la recuperación.

---

[⬆️ Volver al índice](#índice)

## Recuperación de servicios y aplicaciones

No todas las incidencias afectan al sistema operativo completo. En numerosas ocasiones el servidor inicia correctamente, pero uno o varios servicios esenciales dejan de funcionar, provocando la interrupción parcial de la infraestructura.

La recuperación de servicios y aplicaciones consiste en diagnosticar la causa del problema, restaurar el funcionamiento del servicio afectado y verificar que vuelve a operar correctamente sin comprometer el resto del sistema.

---

### ¿Qué es un servicio?

Un servicio es un proceso que se ejecuta en segundo plano y proporciona una funcionalidad específica al sistema o a los usuarios.

Ejemplos:

- Active Directory.
- DNS.
- DHCP.
- IIS.
- Apache.
- Nginx.
- MySQL.
- PostgreSQL.
- SQL Server.
- SSH.

Si uno de estos servicios falla, puede afectar a múltiples equipos o aplicaciones.

---

### Causas habituales de fallo

Los problemas más frecuentes son:

- Configuración incorrecta.
- Archivos dañados.
- Actualizaciones fallidas.
- Certificados caducados.
- Espacio insuficiente en disco.
- Dependencias no iniciadas.
- Permisos incorrectos.
- Bases de datos corruptas.
- Recursos insuficientes (CPU, RAM o almacenamiento).

Antes de reiniciar un servicio conviene identificar la causa del fallo.

---

### Diagnóstico inicial

El primer paso consiste en comprobar el estado del servicio.

Información que conviene revisar:

- Estado actual.
- Hora del último fallo.
- Código de error.
- Dependencias.
- Recursos utilizados.

Un diagnóstico adecuado evita aplicar soluciones innecesarias.

---

### Comprobación del estado del servicio

En Windows:

```powershell
Get-Service
```

o

```powershell
Get-Service -Name DNS
```

En Linux:

```bash
systemctl status apache2
```

o

```bash
systemctl status ssh
```

Estos comandos muestran si el servicio está iniciado, detenido o ha fallado.

---

### Revisión de registros

Los registros suelen proporcionar información muy valiosa.

Windows:

- Visor de eventos.
- Registros de aplicaciones.
- Registros del sistema.

Linux:

```bash
journalctl
```

```bash
/var/log/
```

Consultar los logs suele ser el método más eficaz para localizar la causa del problema.

---

### Reinicio controlado

En muchas ocasiones basta con reiniciar el servicio.

Windows:

```powershell
Restart-Service DNS
```

Linux:

```bash
sudo systemctl restart apache2
```

Tras el reinicio debe comprobarse que el servicio permanece estable y no vuelve a detenerse.

---

### Comprobación de dependencias

Muchos servicios dependen de otros.

Ejemplo:

```text
Aplicación

↓

Base de datos

↓

Red

↓

Sistema operativo
```

Si un servicio dependiente falla, la aplicación principal tampoco podrá funcionar.

---

### Recuperación de aplicaciones web

En servidores web conviene comprobar:

- Estado del servicio web.
- Estado de la base de datos.
- Certificados SSL.
- Configuración.
- Conectividad de red.
- Espacio en disco.

Una aplicación puede dejar de responder aunque el servidor continúe funcionando correctamente.

---

### Recuperación de bases de datos

Cuando una base de datos presenta problemas suele ser necesario:

- Comprobar el servicio.
- Revisar los registros.
- Verificar el almacenamiento.
- Restaurar desde backup si existe corrupción.

No debe restaurarse una base de datos sin intentar identificar previamente la causa del problema.

---

### Recuperación de Active Directory

En entornos Windows uno de los servicios más críticos es Active Directory.

Las comprobaciones habituales incluyen:

- Estado del controlador de dominio.
- Replicación.
- DNS.
- SYSVOL.
- Autenticación.

La indisponibilidad de Active Directory puede afectar a toda la infraestructura.

---

### Recuperación de DNS y DHCP

Cuando los usuarios pierden conectividad conviene verificar:

- Servicio DNS.
- Servicio DHCP.
- Estado de las zonas DNS.
- Ámbitos DHCP.
- Resolución de nombres.

Muchas incidencias aparentemente relacionadas con Internet tienen su origen en estos servicios.

---

### Recuperación de servidores de archivos

Si un servidor de archivos deja de responder deben comprobarse:

- Comparticiones.
- Permisos.
- Estado del almacenamiento.
- Servicios SMB o NFS.
- Espacio disponible.

También es recomendable verificar que los usuarios pueden acceder correctamente a los recursos compartidos.

---

### Recuperación mediante snapshots

En sistemas virtualizados puede recuperarse rápidamente una aplicación mediante un snapshot.

Proceso:

```text
Aplicación

↓

Snapshot

↓

Problema

↓

Restaurar Snapshot

↓

Aplicación operativa
```

Este procedimiento suele ser mucho más rápido que una reinstalación.

---

### Recuperación desde backup

Cuando el problema no puede solucionarse mediante reparación, puede ser necesario restaurar:

- Configuración.
- Archivos.
- Base de datos.
- Máquina virtual completa.

Siempre debe verificarse que la copia utilizada no contiene el mismo problema que el sistema actual.

---

### Validación del servicio

Una vez recuperado conviene comprobar:

- Que permanece iniciado.
- Que responde correctamente.
- Que los usuarios pueden acceder.
- Que no aparecen nuevos errores en los registros.
- Que el rendimiento es normal.

La recuperación no finaliza hasta validar el funcionamiento completo.

---

### Comparativa

| Incidencia | Actuación habitual |
|------------|--------------------|
| Servicio detenido | Reiniciar servicio |
| Configuración incorrecta | Restaurar configuración |
| Base de datos dañada | Reparar o restaurar backup |
| Certificado caducado | Renovar certificado |
| Dependencia detenida | Iniciar servicio dependiente |
| Corrupción grave | Restaurar desde copia de seguridad |

---

### Buenas prácticas

- Analiza la causa del fallo antes de reiniciar un servicio.
- Consulta siempre los registros del sistema y de la aplicación.
- Comprueba las dependencias antes de intervenir.
- Verifica el estado de CPU, memoria, almacenamiento y red.
- Documenta todas las acciones realizadas durante la recuperación.
- Utiliza snapshots antes de aplicar cambios importantes en servidores virtuales.
- Mantén copias de seguridad actualizadas de las configuraciones y bases de datos.
- Valida el funcionamiento del servicio una vez finalizada la recuperación.

---

[⬆️ Volver al índice](#índice)

## Recuperación desde copias de seguridad

La recuperación desde copias de seguridad es uno de los métodos más importantes para restaurar sistemas después de una incidencia grave. Permite devolver archivos, aplicaciones, servidores completos o infraestructuras enteras a un estado operativo anterior.

Una estrategia de backup solo tiene valor cuando existe un procedimiento de restauración probado y capaz de recuperar la información dentro de los tiempos definidos por la organización.

---

### Objetivo de la recuperación desde backup

El objetivo principal es restaurar la disponibilidad de los sistemas reduciendo al mínimo:

- La pérdida de datos.
- El tiempo de inactividad.
- El impacto sobre los usuarios.
- La interrupción de los servicios.

La recuperación debe realizarse siempre siguiendo un procedimiento controlado.

---

### Tipos de recuperación desde backup

Dependiendo del alcance del problema, pueden realizarse diferentes tipos de restauración:

- Recuperación de archivos individuales.
- Recuperación de carpetas completas.
- Restauración de bases de datos.
- Restauración de aplicaciones.
- Restauración de máquinas virtuales.
- Recuperación completa del sistema.

La elección dependerá del tipo de fallo y de la información afectada.

---

### Recuperación de archivos individuales

Es el tipo de restauración más habitual.

Ejemplo:

```text
Usuario elimina archivo

↓

Buscar versión anterior

↓

Restaurar archivo

↓

Archivo recuperado
```

Permite recuperar información concreta sin afectar al resto del sistema.

---

### Recuperación de carpetas completas

Cuando una carpeta completa ha sido eliminada o dañada puede restaurarse desde una copia anterior.

Ejemplo:

```text
Carpeta compartida

↓

Backup

↓

Restauración

↓

Usuarios recuperan acceso
```

Es habitual en servidores de archivos empresariales.

---

### Restauración de bases de datos

Las bases de datos requieren procedimientos específicos debido a la importancia de mantener la consistencia de la información.

Proceso habitual:

```text
Detener servicio

↓

Restaurar backup

↓

Aplicar registros de transacciones

↓

Comprobar integridad

↓

Iniciar servicio
```

Ejemplos:

- SQL Server.
- MySQL.
- PostgreSQL.
- Oracle Database.

---

### Recuperación de máquinas virtuales

En entornos virtualizados, las máquinas completas pueden restaurarse desde una copia.

Proceso:

```text
Backup de VM

↓

Restauración

↓

Hipervisor

↓

Máquina virtual operativa
```

Es uno de los métodos más rápidos para recuperar servidores.

---

### Bare Metal Recovery

La recuperación **Bare Metal Recovery (BMR)** permite reconstruir un equipo completo desde cero.

Incluye:

- Sistema operativo.
- Configuración.
- Aplicaciones.
- Controladores.
- Datos.

Proceso:

```text
Hardware vacío

↓

Restaurar imagen

↓

Sistema completo recuperado
```

Es utilizada principalmente para servidores críticos.

---

### Recuperación granular

La restauración granular permite recuperar elementos concretos sin restaurar todo el sistema.

Ejemplos:

- Un archivo.
- Un correo electrónico.
- Un usuario.
- Un objeto de Active Directory.
- Una tabla de base de datos.

Reduce el tiempo necesario para recuperar información específica.

---

### Restauración completa del sistema

Cuando el sistema operativo está gravemente dañado puede ser necesario recuperar una imagen completa.

Proceso:

```text
Sistema dañado

↓

Seleccionar imagen válida

↓

Restauración completa

↓

Configuración recuperada
```

Este método sustituye completamente el contenido del sistema.

---

### Recuperación ante ransomware

Las copias de seguridad son una pieza clave frente al ransomware.

Procedimiento recomendado:

```text
Aislar equipos afectados

↓

Eliminar amenaza

↓

Comprobar backups

↓

Restaurar información

↓

Validar sistemas
```

Nunca debe restaurarse una copia sin confirmar que el entorno está limpio.

---

### Selección del punto de restauración

Antes de restaurar es necesario elegir correctamente la copia.

Debe analizarse:

- Fecha del backup.
- Estado del sistema en ese momento.
- Integridad de la copia.
- Existencia del problema en esa versión.

Restaurar una copia demasiado reciente puede recuperar también el fallo original.

---

### Restauración en ubicación original

Es la opción más habitual.

Proceso:

```text
Backup

↓

Servidor original

↓

Datos restaurados
```

Ventaja:

- Recuperación rápida.

Inconveniente:

- Puede sobrescribir información actual.

---

### Restauración en ubicación alternativa

Permite recuperar la información en otro equipo o servidor.

Ejemplo:

```text
Servidor antiguo

↓

Backup

↓

Servidor nuevo
```

Es útil cuando el hardware original está dañado.

---

### Recuperación en entornos virtualizados

Las plataformas modernas permiten restaurar servidores rápidamente.

Ejemplos:

- VMware.
- Hyper-V.
- Proxmox.

Ventajas:

- Menor tiempo de recuperación.
- Fácil creación de entornos temporales.
- Posibilidad de pruebas antes de poner el sistema en producción.

---

### Verificación después de la restauración

Después de recuperar un sistema deben comprobarse:

- Servicios iniciados.
- Aplicaciones funcionando.
- Usuarios con acceso.
- Permisos correctos.
- Conectividad.
- Integridad de datos.

La restauración no finaliza hasta validar el funcionamiento.

---

### Pruebas de restauración

Es recomendable realizar pruebas periódicas.

Proceso:

```text
Seleccionar copia

↓

Restaurar en laboratorio

↓

Validar funcionamiento

↓

Registrar resultado
```

Esto permite detectar copias corruptas o procedimientos incorrectos.

---

### Comparativa

| Tipo de recuperación | Uso |
|----------------------|-----|
| Archivo individual | Recuperar documentos eliminados |
| Carpeta completa | Restaurar recursos compartidos |
| Base de datos | Recuperar información estructurada |
| Máquina virtual | Recuperar servidores rápidamente |
| Bare Metal Recovery | Reconstrucción completa |
| Restauración granular | Recuperar elementos concretos |

---

### Buenas prácticas

- Comprueba regularmente que las copias pueden restaurarse.
- Define procedimientos claros de recuperación.
- Mantén diferentes puntos históricos de restauración.
- Verifica siempre la integridad del backup antes de utilizarlo.
- Prueba restauraciones en entornos controlados.
- Prioriza la recuperación de servicios críticos.
- Documenta cada restauración realizada.
- Mantén copias protegidas frente a ransomware mediante almacenamiento offline o inmutable.

---

[⬆️ Volver al índice](#índice)

## Recuperación ante desastres (Disaster Recovery)

La recuperación ante desastres, conocida como **Disaster Recovery (DR)**, engloba el conjunto de procesos, tecnologías y procedimientos destinados a recuperar una infraestructura tecnológica después de un evento grave que afecta a la disponibilidad de los sistemas.

A diferencia de una recuperación puntual, como reparar un servicio o restaurar un archivo, un plan de Disaster Recovery contempla escenarios donde una parte importante o toda la infraestructura deja de estar operativa.

Su objetivo principal es garantizar la continuidad del negocio y reducir el impacto de situaciones críticas.

---

### ¿Qué es Disaster Recovery?

Un plan de **Disaster Recovery** define cómo recuperar los sistemas, aplicaciones y datos después de un desastre.

Ejemplos de desastres:

- Incendios.
- Inundaciones.
- Fallos eléctricos prolongados.
- Ataques ransomware.
- Pérdida completa de servidores.
- Fallos del centro de datos.
- Errores humanos graves.

Proceso general:

```text
Desastre

↓

Activación del plan DR

↓

Recuperación infraestructura

↓

Restauración servicios

↓

Operación normal
```

---

### Diferencia entre Backup y Disaster Recovery

Aunque están relacionados, no son lo mismo.

| Backup | Disaster Recovery |
|--------|-------------------|
| Protege datos | Recupera servicios completos |
| Guarda información | Define procedimientos |
| Permite restaurar archivos | Permite recuperar operaciones |
| Es una parte del DR | Incluye backup, sistemas y procesos |

Un backup sin un plan de recuperación puede no ser suficiente ante un desastre.

---

### Objetivos del Disaster Recovery

Los principales objetivos son:

- Recuperar los servicios críticos.
- Reducir el tiempo de interrupción.
- Minimizar la pérdida de información.
- Definir responsabilidades.
- Establecer procedimientos claros.
- Garantizar la continuidad operativa.

---

### Plan de recuperación ante desastres (DRP)

El **Disaster Recovery Plan (DRP)** es el documento donde se detallan todas las acciones necesarias para recuperar la infraestructura.

Debe incluir:

- Sistemas críticos.
- Responsables.
- Contactos de emergencia.
- Procedimientos técnicos.
- Orden de recuperación.
- Ubicación de copias.
- Proveedores externos.
- Tiempos estimados.

---

### Análisis de impacto del negocio (BIA)

Antes de crear un plan DR es necesario realizar un análisis de impacto.

El **Business Impact Analysis (BIA)** identifica:

- Servicios críticos.
- Dependencias.
- Coste de una interrupción.
- Tiempo máximo sin servicio.
- Prioridad de recuperación.

Ejemplo:

| Servicio | Prioridad |
|----------|-----------|
| Active Directory | Crítica |
| ERP | Crítica |
| Correo | Alta |
| Archivos compartidos | Alta |
| Aplicaciones internas | Media |

---

### Identificación de riesgos

Un plan DR debe analizar posibles amenazas.

Ejemplos:

- Fallos eléctricos.
- Ataques externos.
- Errores humanos.
- Problemas de hardware.
- Fallos de proveedores.
- Desastres naturales.

Para cada riesgo deben definirse medidas preventivas y procedimientos de recuperación.

---

### Estrategias de recuperación

Existen diferentes estrategias según la infraestructura disponible.

Las principales son:

- Backup y restauración.
- Cold Site.
- Warm Site.
- Hot Site.
- Replicación.
- Cloud Disaster Recovery.

---

### Cold Site

Un **Cold Site** es una ubicación preparada pero sin sistemas activos.

Características:

- Bajo coste.
- Requiere instalación antes de recuperar.
- Tiempo de recuperación elevado.

Ejemplo:

```text
Desastre

↓

Enviar hardware

↓

Instalar sistemas

↓

Restaurar backups
```

---

### Warm Site

Un **Warm Site** dispone de parte de la infraestructura preparada.

Características:

- Algunos sistemas disponibles.
- Menor tiempo de recuperación.
- Coste intermedio.

Ejemplo:

```text
Infraestructura preparada

↓

Restaurar datos

↓

Activar servicios
```

---

### Hot Site

Un **Hot Site** es una réplica activa del entorno principal.

Características:

- Sistemas funcionando.
- Datos replicados.
- Recuperación muy rápida.
- Coste elevado.

Ejemplo:

```text
Centro principal

↓

Replicación continua

↓

Centro secundario operativo
```

---

### Recuperación en la nube

Los servicios cloud permiten crear planes DR sin disponer de un segundo centro físico.

Ejemplos:

- Azure Site Recovery.
- AWS Disaster Recovery.
- Google Cloud Disaster Recovery.

Ventajas:

- Escalabilidad.
- Menor inversión inicial.
- Activación rápida.

---

### Replicación de sistemas

La replicación consiste en mantener una copia activa de los sistemas en otra ubicación.

Puede aplicarse a:

- Máquinas virtuales.
- Bases de datos.
- Almacenamiento.
- Aplicaciones.

Ejemplo:

```text
Servidor producción

↓

Replicación

↓

Servidor secundario
```

---

### Orden de recuperación

Durante un desastre no todos los sistemas deben recuperarse al mismo tiempo.

Ejemplo:

```text
1. Red e infraestructura

↓

2. Active Directory

↓

3. DNS/DHCP

↓

4. Bases de datos

↓

5. Aplicaciones

↓

6. Equipos usuarios
```

Recuperar dependencias primero evita problemas posteriores.

---

### Equipo de respuesta

Un plan DR debe definir responsables.

Ejemplo:

| Rol | Función |
|-----|---------|
| Responsable IT | Coordinar recuperación |
| Administrador sistemas | Recuperar servidores |
| Administrador redes | Recuperar comunicaciones |
| Responsable negocio | Validar servicios |

---

### Comunicación durante un desastre

La comunicación es fundamental durante una emergencia.

Debe establecerse:

- Quién informa.
- A quién informar.
- Canales utilizados.
- Frecuencia de actualización.

Una mala comunicación puede aumentar el impacto del incidente.

---

### Pruebas del plan DR

Un plan que nunca se prueba puede fallar cuando más se necesita.

Tipos de pruebas:

- Simulación teórica.
- Prueba técnica parcial.
- Restauración completa.
- Simulación de desastre real.

---

### Comparativa

| Estrategia | Tiempo recuperación | Coste |
|------------|--------------------|-------|
| Backup tradicional | Alto | Bajo |
| Cold Site | Alto | Bajo |
| Warm Site | Medio | Medio |
| Hot Site | Muy bajo | Alto |
| Cloud DR | Bajo | Variable |
| Replicación | Muy bajo | Alto |

---

### Buenas prácticas

- Mantén un plan DR documentado y actualizado.
- Identifica los sistemas críticos mediante un análisis BIA.
- Define claramente RTO y RPO.
- Establece responsables para cada tarea.
- Mantén copias externas e inmutables.
- Realiza pruebas periódicas del plan.
- Actualiza la documentación cuando cambie la infraestructura.
- Prioriza siempre la recuperación de servicios esenciales.
- Coordina la recuperación técnica con las necesidades del negocio.

---

[⬆️ Volver al índice](#índice)

## Pruebas y validación de la recuperación

Una recuperación del sistema no puede considerarse completada simplemente porque el equipo o servicio vuelva a arrancar. Es necesario comprobar que la información es correcta, que las aplicaciones funcionan adecuadamente y que los usuarios pueden volver a trabajar con normalidad.

Las pruebas de recuperación permiten detectar errores en los procedimientos, validar las copias de seguridad y garantizar que la organización está preparada ante una incidencia real.

---

### Importancia de las pruebas de recuperación

Realizar pruebas periódicas permite:

- Confirmar que los procedimientos funcionan.
- Detectar copias dañadas.
- Comprobar tiempos reales de recuperación.
- Identificar problemas antes de una emergencia.
- Mejorar los planes de recuperación.

Una copia de seguridad nunca debe darse por válida hasta que ha sido restaurada correctamente.

---

### Tipos de pruebas de recuperación

Existen diferentes niveles de prueba dependiendo del objetivo.

Las más habituales son:

- Pruebas documentales.
- Pruebas parciales.
- Pruebas completas.
- Simulaciones de desastre.

Cada organización debe elegir el nivel adecuado según la criticidad de sus sistemas.

---

### Pruebas documentales

Son revisiones teóricas del procedimiento de recuperación.

Consisten en comprobar:

- Documentación disponible.
- Responsables asignados.
- Contactos de emergencia.
- Orden de recuperación.
- Procedimientos técnicos.

No implican realizar una restauración real.

---

### Pruebas parciales

Se realizan sobre componentes concretos.

Ejemplos:

- Restaurar un archivo.
- Recuperar una base de datos.
- Arrancar una máquina virtual.
- Recuperar un servicio.

Permiten comprobar partes específicas del proceso sin afectar al entorno de producción.

---

### Pruebas completas

Consisten en realizar una recuperación completa de un sistema o servicio.

Proceso:

```text
Seleccionar escenario

↓

Restaurar sistemas

↓

Validar funcionamiento

↓

Documentar resultados
```

Son más complejas y requieren mayor planificación.

---

### Simulaciones de desastre

Son ejercicios donde se recrea una situación crítica.

Ejemplo:

```text
Caída del servidor principal

↓

Activación del DRP

↓

Recuperación servicios

↓

Validación
```

Permiten evaluar la capacidad real de respuesta de la organización.

---

### Entornos de prueba

Siempre que sea posible, las pruebas deben realizarse en entornos aislados.

Ejemplo:

```text
Producción

↓

Backup

↓

Entorno de pruebas

↓

Restauración
```

Esto evita afectar a los usuarios durante las comprobaciones.

---

### Validación de datos

Después de una restauración es necesario comprobar que los datos recuperados son correctos.

Debe revisarse:

- Integridad de archivos.
- Tamaño de datos.
- Permisos.
- Fechas.
- Consistencia de bases de datos.

---

### Validación de servicios

Además de los datos, deben comprobarse los servicios relacionados.

Ejemplos:

- Inicio correcto de servicios.
- Conectividad.
- Resolución DNS.
- Autenticación.
- Acceso de usuarios.
- Funcionamiento de aplicaciones.

Un servidor restaurado pero sin servicios funcionales no se considera recuperado.

---

### Validación de aplicaciones

Las aplicaciones deben probarse después de la recuperación.

Comprobaciones habituales:

- Inicio correcto.
- Acceso de usuarios.
- Comunicación con bases de datos.
- Carga de información.
- Funcionamiento de procesos críticos.

---

### Medición de RPO y RTO

Durante las pruebas deben medirse los objetivos definidos.

**RPO:**

Comprueba cuánta información se pierde durante la recuperación.

Ejemplo:

```text
RPO esperado: 1 hora

RPO obtenido: 20 minutos
```

---

**RTO:**

Comprueba cuánto tiempo tarda la recuperación.

Ejemplo:

```text
RTO esperado: 4 horas

RTO obtenido: 2 horas
```

---

### Registro de resultados

Cada prueba debería quedar documentada.

Información recomendada:

- Fecha.
- Sistema probado.
- Tipo de prueba.
- Tiempo empleado.
- Problemas encontrados.
- Soluciones aplicadas.
- Resultado final.

Esta información permite mejorar futuras recuperaciones.

---

### Análisis posterior

Después de una prueba o recuperación real debe realizarse una revisión.

Debe analizarse:

- Qué funcionó correctamente.
- Qué problemas aparecieron.
- Qué procedimientos deben modificarse.
- Qué mejoras pueden aplicarse.

Este proceso se conoce como análisis post-incidente.

---

### Automatización de pruebas

Algunas soluciones permiten automatizar validaciones.

Ejemplos:

- Arranque automático de máquinas virtuales.
- Comprobación de servicios.
- Verificación de conectividad.
- Capturas de estado.
- Informes automáticos.

La automatización facilita realizar pruebas frecuentes.

---

### Frecuencia de las pruebas

La periodicidad depende de la criticidad del sistema.

Ejemplo:

| Sistema | Frecuencia |
|---------|------------|
| Sistemas críticos | Mensual |
| Servidores importantes | Trimestral |
| Sistemas secundarios | Semestral |
| Documentación | Revisión continua |

---

### Comparativa

| Prueba | Objetivo |
|--------|----------|
| Documental | Revisar procedimientos |
| Parcial | Validar componentes concretos |
| Completa | Comprobar recuperación total |
| Simulación desastre | Evaluar respuesta global |

---

### Buenas prácticas

- Realiza pruebas de recuperación de forma periódica.
- No confíes únicamente en que los backups existen.
- Documenta todos los resultados obtenidos.
- Utiliza entornos aislados cuando sea posible.
- Mide siempre los tiempos reales de recuperación.
- Comprueba tanto datos como servicios y aplicaciones.
- Actualiza los procedimientos cuando aparezcan nuevos problemas.
- Involucra a las personas responsables de cada área.
- Revisa que los resultados cumplen los objetivos RPO y RTO establecidos.

---

[⬆️ Volver al índice](#índice)

## Buenas prácticas

Una correcta recuperación del sistema no depende únicamente de disponer de herramientas técnicas. Es necesario establecer procedimientos claros, mantener la documentación actualizada y realizar pruebas periódicas para garantizar que los sistemas puedan recuperarse de forma rápida y segura ante cualquier incidencia.

Las siguientes buenas prácticas ayudan a reducir los tiempos de recuperación, minimizar la pérdida de información y mejorar la capacidad de respuesta de la organización.

---

### Planificar antes de que ocurra una incidencia

La recuperación no debe improvisarse durante una emergencia.

Es recomendable definir previamente:

- Procedimientos de actuación.
- Responsables de recuperación.
- Sistemas críticos.
- Orden de restauración.
- Herramientas necesarias.
- Métodos de comunicación.

Una planificación adecuada reduce considerablemente el tiempo de respuesta.

---

### Mantener procedimientos documentados

Toda organización debería disponer de documentación actualizada sobre recuperación.

Debe incluir:

- Pasos técnicos.
- Comandos utilizados.
- Configuraciones necesarias.
- Contactos importantes.
- Dependencias entre sistemas.
- Tiempos estimados.

Una documentación clara permite actuar incluso cuando el personal habitual no está disponible.

---

### Priorizar los sistemas críticos

No todos los servicios tienen la misma importancia.

Durante una recuperación debe establecerse un orden de prioridad.

Ejemplo:

```text
1. Infraestructura de red

↓

2. Active Directory

↓

3. DNS/DHCP

↓

4. Bases de datos

↓

5. Aplicaciones

↓

6. Equipos de usuario
```

Recuperar las dependencias primero evita problemas posteriores.

---

### Mantener copias de seguridad fiables

Las copias son la base de cualquier estrategia de recuperación.

Buenas prácticas:

- Realizar backups periódicos.
- Mantener varias versiones.
- Utilizar almacenamiento externo.
- Aplicar cifrado.
- Mantener copias offline o inmutables.
- Verificar restauraciones.

Una copia no probada no garantiza una recuperación exitosa.

---

### Realizar pruebas periódicas

Los procedimientos deben comprobarse regularmente.

Las pruebas permiten detectar:

- Copias corruptas.
- Procedimientos incorrectos.
- Falta de permisos.
- Problemas de compatibilidad.
- Tiempos de recuperación superiores a los previstos.

La práctica mejora la preparación ante incidentes reales.

---

### Definir objetivos RPO y RTO

Toda estrategia de recuperación debe establecer:

**RPO:**

Cantidad máxima de datos que puede perderse.

Ejemplo:

```text
RPO = 1 hora
```

**RTO:**

Tiempo máximo permitido para recuperar un servicio.

Ejemplo:

```text
RTO = 4 horas
```

Estos valores permiten diseñar una estrategia acorde a las necesidades del negocio.

---

### Mantener medios de recuperación disponibles

Es recomendable disponer siempre de herramientas preparadas.

Ejemplos:

- USB de instalación de Windows.
- Live USB Linux.
- Herramientas de diagnóstico.
- Imágenes de recuperación.
- Documentación técnica.

No esperar a una emergencia para preparar estos recursos.

---

### Monitorizar los sistemas

La detección temprana facilita la recuperación.

Conviene supervisar:

- Estado de discos.
- Espacio disponible.
- Errores del sistema.
- Servicios críticos.
- Rendimiento.
- Copias de seguridad.

Una incidencia detectada rápidamente suele tener menor impacto.

---

### Proteger las herramientas de recuperación

Las herramientas utilizadas para recuperar sistemas también deben protegerse.

Medidas recomendadas:

- Control de acceso.
- Cuentas administrativas separadas.
- MFA.
- Almacenamiento seguro.
- Registro de actividad.

Un atacante que controle las herramientas de recuperación puede inutilizar toda la infraestructura.

---

### Aplicar el principio de mínimo privilegio

Durante una recuperación deben utilizarse únicamente los permisos necesarios.

Buenas prácticas:

- Evitar usar cuentas de administrador del dominio sin necesidad.
- Utilizar cuentas específicas de recuperación.
- Registrar accesos administrativos.

Esto reduce riesgos durante procesos críticos.

---

### Mantener inventario actualizado

Es importante conocer exactamente qué sistemas existen.

El inventario debe incluir:

- Servidores.
- Aplicaciones.
- Dependencias.
- Direcciones IP.
- Versiones.
- Ubicación de backups.

Sin un inventario actualizado es difícil recuperar una infraestructura completa.

---

### Revisar dependencias entre sistemas

Muchos servicios dependen unos de otros.

Ejemplo:

```text
Aplicación ERP

↓

Base de datos

↓

Sistema operativo

↓

Almacenamiento
```

Conocer estas relaciones permite establecer correctamente el orden de recuperación.

---

### Automatizar procesos repetitivos

Siempre que sea posible deben automatizarse tareas como:

- Restauraciones.
- Configuración inicial.
- Validaciones.
- Comprobaciones.
- Informes.

La automatización reduce errores humanos y acelera la recuperación.

---

### Analizar las causas después de una incidencia

Después de una recuperación real debe realizarse un análisis posterior.

Debe revisarse:

- Qué provocó el fallo.
- Qué soluciones funcionaron.
- Qué problemas aparecieron.
- Qué mejoras deben aplicarse.

El objetivo es evitar que vuelva a ocurrir.

---

### Actualizar continuamente el plan de recuperación

La infraestructura cambia constantemente.

Por ello debe revisarse:

- Nuevos servidores.
- Nuevas aplicaciones.
- Cambios de red.
- Nuevas políticas.
- Cambios de proveedores.

Un plan desactualizado puede fallar durante una emergencia.

---

### Errores frecuentes

Algunos errores habituales son:

- No tener documentación.
- No probar las restauraciones.
- No conocer las dependencias.
- Guardar las copias en una única ubicación.
- No actualizar procedimientos.
- Utilizar herramientas sin protección.
- No definir responsables.
- Recuperar sistemas sin validar posteriormente.

---

### Comparativa

| Buena práctica | Beneficio |
|----------------|-----------|
| Documentación | Recuperación más rápida |
| Pruebas periódicas | Detectar errores antes del desastre |
| Inventario actualizado | Conocer la infraestructura |
| RPO/RTO definidos | Establecer objetivos claros |
| Automatización | Reducir errores |
| Monitorización | Detectar problemas rápidamente |
| Análisis posterior | Evitar reincidencias |

---

[⬆️ Volver al índice](#índice)