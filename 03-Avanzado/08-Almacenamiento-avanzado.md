# 08 - Almacenamiento avanzado

## Introducción

El almacenamiento es uno de los componentes más importantes de cualquier sistema informático. Además de guardar la información, influye directamente en el rendimiento, la disponibilidad y la capacidad de recuperación ante fallos de servidores y estaciones de trabajo.

En niveles básicos se estudian conceptos como discos, particiones y sistemas de archivos. En este apartado se profundiza en tecnologías avanzadas de almacenamiento utilizadas en entornos profesionales, incluyendo RAID, LVM, volúmenes dinámicos, sistemas de archivos avanzados, almacenamiento en red, cuotas de disco y técnicas de monitorización y mantenimiento.

Comprender estas tecnologías permite diseñar infraestructuras más seguras, escalables y tolerantes a fallos, optimizando tanto el rendimiento como la protección de los datos.

---

## Índice

- [Tipos de almacenamiento](#tipos-de-almacenamiento)
- [RAID](#raid)
- [LVM y administración de volúmenes](#lvm-y-administración-de-volúmenes)
- [Sistemas de archivos avanzados](#sistemas-de-archivos-avanzados)
- [Almacenamiento en red](#almacenamiento-en-red)
- [Cuotas de disco](#cuotas-de-disco)
- [Monitorización y mantenimiento](#monitorización-y-mantenimiento)
- [Recuperación de almacenamiento](#recuperación-de-almacenamiento)
- [Buenas prácticas](#buenas-prácticas)

---

## Tipos de almacenamiento

El almacenamiento es el componente encargado de guardar de forma permanente la información de un sistema informático. Su elección influye directamente en el rendimiento, la capacidad, la disponibilidad y la tolerancia a fallos de una infraestructura.

Existen diferentes tecnologías de amlacenamiento, cada una diseñada para cubrir necesidades específicas, desde equipos domésticos hasta grandes centros de datos.

Conocer sus características permite seleccionar la solución más adecuada de forma permanente.

---

### ¿Qué es un dispositivo de almacenamiento?

Un dispositivo de almacenamiento es un medio físico o lógico donde se guardan datos de forma permanente.

Puede almacenar:

- Sistema operativo.
- Aplicaciones.
- Archivos de usuario.
- Bases de datos.
- Máquinas virtuales.
- Copias de seguridad.

Su capacidad, velocidad y fiabilidad dependerán de la tecnología utilizada.

---

### Clasificación del almacenamiento

El almacenamiento puede clasificarse según distintos criterios.

Los más habituales son:

- Almacenamiento magnético.
- Almacenamiento de estado sólido.
- Almacenamiento óptico.
- Almacenamiento en red.
- Almacenamiento en la nube.

Cada uno presenta ventajas e inconvenientes.

---

### Discos duros (HDD)

Los **HDD (Hard Disk Drive)** utilizan platos magnéticos giratorios para almacenar la información.

**Características:**

- Gran capacidad.
- Bajo coste por GB.
- Velocidad inferior a los SSD.
- Componentes mecánicos.

**Son adecuados para:**

- Almacenamiento masivo.
- Servidores de archivos.
- Copias de seguridad.

---

### Unidades SSD

Los **SSD (Solid State Drive)** almacenan la información mediante memoria flash.

**Características:**

- Sin partes móviles.
- Muy baja latencia.
- Alta velocidad.
- Menor consumo energético.
- Mayor resistencia a golpes.

**Son ideales para:**

- Sistemas operativos.
- Aplicaciones.
- Bases de datos.
- Equipos que requieren un alto rendimiento.

---

### Unidades NVMe

Las unidades **NVMe (Non-Volatile Memory Express)** son un tipo de SSD que utiliza el bus PCI Express en lugar de SATA.

**Ventajas:**

- Muchísima mayor velocidad.
- Menor latencia.
- Mejor rendimiento en operaciones simultáneas.
- Aprovechan mejor los procesadores modernos.

**Se utilizan habitualmente en:**

- Servidores.
- Virtualización.
- Bases de datos.
- Equipos de alto rendimiento.

---

### Comparativa HDD, SSD y NVMe

| Característica | HDD | SSD SATA | SSD NVMe |
|---------------|------|----------|-----------|
| Tecnología | Magnética | Memoria flash | Memoria flash |
| Velocidad | Baja | Alta | Muy alta |
| Latencia | Alta | Baja | Muy baja |
| Partes móviles | Sí | No | No |
| Consumo | Alto | Bajo | Bajo |
| Precio por GB | Bajo | Medio | Superior |

---

### Almacenamiento óptico

Utiliza discos ópticos como:

- CD.
- DVD.
- Blu-ray.

Actualmente su uso es reducido, aunque todavía resulta útil para:

- Distribución de software.
- Archivado.
- Copias puntuales.

---

### Memorias USB

Las memorias USB utilizan memoria flash.

**Ventajas:**

- Portabilidad.
- Bajo coste.
- Fácil transporte.

No deberían utilizarse como almacenamiento principal de servidores debido a su menor fiabilidad y vida útil.

---

### Tarjetas SD y microSD

Son similares a las memorias USB pero con un formato más compacto.

Se utilizan principalmente en:

- Cámaras.
- Dispositivos IoT.
- Raspberry Pi.
- Equipos embebidos.

---

### Almacenamiento local

El almacenamiento local está conectado directamente al equipo.

**Ejemplos:**

- HDD internos.
- SSD SATA.
- SSD NVMe.
- Unidades USB.

Su acceso es rápido y no depende de la red.

---

### Almacenamiento en red

Permite que varios equipos compartan recursos de almacenamiento a través de una red.

Las tecnologías más utilizadas son:

- NAS.
- SAN.
- iSCSI.
- NFS.
- SMB/CIFS.

Es la solución habitual en entornos empresariales.

---

### NAS (Network Attached Storage)

Un **NAS** es un dispositivo conectado a la red que comparte archivos.

**Características:**

- Fácil administración.
- Bajo coste.
- Acceso desde múltiples equipos.
- Compartición mediante SMB o NFS.
- Puede incorporar RAID.

Es muy habitual en pequeñas y medianas empresas.

---

### SAN (Storage Area Network)

Una **SAN** proporciona almacenamiento a nivel de bloques mediante una red dedicada.

**Características:**

- Alto rendimiento.
- Alta disponibilidad.
- Escalabilidad.
- Utilizada en grandes centros de datos.

Suele emplearse para:

- Virtualización.
- Bases de datos.
- Infraestructuras críticas.

---

### Almacenamiento en la nube

La información se almacena en servidores gestionados por un proveedor externo.

**Ejemplos:**

- Microsoft Azure Storage.
- Amazon S3.
- Google Cloud Storage.

**Ventajas:**

- Escalabilidad.
- Alta disponibilidad.
- Acceso desde cualquier ubicación.

**Inconvenientes:**

- Dependencia de Internet.
- Costes recurrentes.
- Consideraciones sobre privacidad y cumplimiento normativo.

---

### Almacenamiento por bloques y por archivos

Existen dos formas habituales de acceder a los datos.

**Almacenamiento por bloques**

- El sistema operativo gestiona el sistema de archivos.
- Mayor rendimiento.
- Utilizado por SAN e iSCSI.

**Almacenamiento por archivos**

- Se accede directamente a carpetas y archivos.
- Más sencillo de administrar.
- Utilizado por NAS mediante SMB o NFS.

---

### Factores para elegir un almacenamiento

Antes de seleccionar una solución conviene valorar:

- Capacidad.
- Rendimiento.
- Fiabilidad.
- Coste.
- Escalabilidad.
- Disponibilidad.
- Facilidad de administración.

No existe una única solución válida para todos los escenarios.

---

### Comparativa

| Tipo | Uso habitual |
|------|--------------|
| HDD | Almacenamiento masivo |
| SSD SATA | Equipos y servidores |
| SSD NVMe | Alto rendimiento |
| NAS | Compartición de archivos |
| SAN | Virtualización y centros de datos |
| Nube | Escalabilidad y acceso remoto |

---

### Buenas prácticas

- Utiliza SSD o NVMe para sistemas operativos y aplicaciones críticas.
- Reserva los HDD para almacenamiento masivo y copias de seguridad.
- Separa el almacenamiento del sistema y el de los datos cuando sea posible.
- Implementa redundancia (RAID) en servidores para mejorar la disponibilidad.
- Supervisa periódicamente el estado de los dispositivos de almacenamiento.
- Planifica el crecimiento futuro antes de adquirir nueva capacidad.
- Mantén copias de seguridad independientemente del tipo de almacenamiento utilizado.

---

[⬆️ Volver al índice](#índice)

## RAID

El **RAID (Redundant Array of Independent Disks)** es una tecnología que permite combinar varios discos físicos para que el sistema operativo los utilice como una única unidad lógica.

Dependiendo del nivel de RAID utilizado, su objetivo puede ser:

- Mejorar el rendimiento.
- Aumentar la disponibilidad.
- Proteger los datos frente al fallo de uno o varios discos.
- Combinar capacidad y redundancia.

RAID es una de las tecnologías más utilizadas en servidores, sistemas de almacenamiento y centros de datos.

> **Importante:** RAID **no sustituye a una copia de seguridad**. Aunque algunos niveles permiten continuar trabajando tras el fallo de un disco, no protegen frente a errores humanos, malware, corrupción de datos o desastres físicos.

---

### ¿Cómo funciona RAID?

RAID distribuye la información entre varios discos utilizando diferentes técnicas.

Las principales son:

- **Striping:** divide los datos entre varios discos para aumentar el rendimiento.
- **Mirroring:** mantiene una copia idéntica de la información en otro disco.
- **Paridad:** almacena información adicional que permite reconstruir los datos si un disco falla.

Cada nivel de RAID combina estas técnicas de forma diferente.

---

### Tipos de implementación

Existen dos formas principales de implementar RAID.

#### RAID por hardware

Se gestiona mediante una controladora RAID dedicada.

**Ventajas:**

- Mayor rendimiento.
- Menor carga para el procesador.
- Funciones avanzadas.
- Muy utilizado en servidores.

**Inconvenientes:**

- Mayor coste.
- Dependencia de la controladora.

---

#### RAID por software

Es gestionado por el propio sistema operativo.

**Linux**

- `mdadm`

**Windows**

- Storage Spaces (Espacios de almacenamiento).
- Discos dinámicos (versiones anteriores).

**Ventajas:**

- No requiere hardware específico.
- Menor coste.
- Fácil configuración.

**Inconvenientes:**

- Mayor consumo de CPU.
- Algunas funciones dependen del sistema operativo.

---

### RAID 0 (Striping)

RAID 0 distribuye los datos entre todos los discos.

```text
Archivo

↓

Disco 1
Disco 2
Disco 3
```

**Características:**

- Máximo rendimiento.
- Aprovecha el 100 % de la capacidad.
- No ofrece redundancia.

Si un solo disco falla:

```text
↓

Se pierden todos los datos
```

**Uso recomendado:**

- Edición de vídeo.
- Procesamiento temporal.
- Equipos donde el rendimiento sea prioritario y los datos no sean críticos.

---

### RAID 1 (Mirroring)

RAID 1 mantiene una copia idéntica de toda la información.

```text
Disco 1

↓

Copia exacta

↓

Disco 2
```

**Características:**

- Alta disponibilidad.
- Configuración sencilla.
- Excelente protección frente al fallo de un disco.

**Inconveniente:**

Solo se aprovecha aproximadamente el **50 %** de la capacidad instalada.

**Uso recomendado:**

- Sistema operativo.
- Servidores pequeños.
- Equipos críticos.

---

### RAID 5

RAID 5 distribuye los datos junto con información de paridad.

**Requisitos:**

- Mínimo **3 discos**.

**Características:**

- Buen equilibrio entre capacidad y seguridad.
- Permite el fallo de un disco sin pérdida de información.
- Muy utilizado en servidores de archivos.

Durante la reconstrucción del RAID el rendimiento disminuye.

---

### RAID 6

RAID 6 funciona de forma similar a RAID 5, pero utiliza doble paridad.

**Requisitos:**

- Mínimo **4 discos**.

**Características:**

- Permite el fallo simultáneo de dos discos.
- Mayor seguridad.
- Menor capacidad útil debido a la doble paridad.

Es habitual en infraestructuras donde la disponibilidad es prioritaria.

---

### RAID 10 (RAID 1+0)

RAID 10 combina:

```text
RAID 1

+

RAID 0
```

**Características:**

- Alto rendimiento.
- Alta disponibilidad.
- Reconstrucción rápida.
- Excelente rendimiento en lectura y escritura.

**Requisitos:**

- Mínimo **4 discos**.

Es uno de los niveles RAID más recomendados para virtualización y bases de datos.

---

### Comparativa de niveles RAID

| RAID | Discos mínimos | Rendimiento | Redundancia | Capacidad útil |
|------|----------------|-------------|-------------|----------------|
| RAID 0 | 2 | Muy alta | No | 100 % |
| RAID 1 | 2 | Alta | Sí (1 disco) | 50 % |
| RAID 5 | 3 | Alta | Sí (1 disco) | n−1 |
| RAID 6 | 4 | Alta | Sí (2 discos) | n−2 |
| RAID 10 | 4 | Muy alta | Sí | 50 % |

---

### Reconstrucción (Rebuild)

Cuando un disco falla y se sustituye por otro nuevo, el RAID reconstruye automáticamente la información.

Proceso:

```text
Disco averiado

↓

Sustitución

↓

Reconstrucción

↓

RAID operativo
```

Durante este proceso:

- El rendimiento disminuye.
- Existe un mayor riesgo si otro disco falla (según el nivel RAID).

---

### Hot Spare

Un **Hot Spare** es un disco instalado que permanece inactivo hasta que otro falla.

Cuando se produce el fallo:

```text
Disco averiado

↓

Hot Spare

↓

Reconstrucción automática
```

Esto reduce considerablemente el tiempo necesario para restaurar la redundancia.

---

### Monitorización del RAID

Es recomendable comprobar periódicamente:

- Estado de los discos.
- Estado del volumen RAID.
- Procesos de reconstrucción.
- Alertas de la controladora.
- Temperatura de los discos.
- Errores SMART.

Muchas controladoras RAID permiten enviar alertas por correo electrónico cuando detectan un problema.

---

### RAID no es una copia de seguridad

Una idea equivocada muy frecuente es pensar que RAID sustituye a las copias de seguridad.

RAID protege frente al fallo físico de discos.

No protege frente a:

- Eliminación accidental.
- Ransomware.
- Corrupción de datos.
- Errores de configuración.
- Incendios o robos.

Siempre debe existir una estrategia de backup independiente.

---

### Comparativa de uso

| Escenario | RAID recomendado |
|-----------|------------------|
| Máximo rendimiento | RAID 0 |
| Sistema operativo | RAID 1 |
| Servidor de archivos | RAID 5 |
| Datos críticos | RAID 6 |
| Virtualización y bases de datos | RAID 10 |

---

### Buenas prácticas

- Utiliza RAID hardware en servidores siempre que sea posible.
- No consideres RAID como sustituto de las copias de seguridad.
- Supervisa periódicamente el estado de todos los discos.
- Sustituye inmediatamente cualquier disco averiado.
- Configura alertas para detectar fallos cuanto antes.
- Utiliza discos del mismo modelo, capacidad y rendimiento dentro del mismo RAID.
- Implementa discos **Hot Spare** en infraestructuras críticas.
- Comprueba periódicamente el correcto funcionamiento de la reconstrucción del RAID.

---

[⬆️ Volver al índice](#índice)

## LVM y administración de volúmenes

La gestión tradicional de particiones presenta diversas limitaciones: el tamaño de una partición queda fijado durante su creación, ampliar el espacio disponible puede resultar complejo y reorganizar los discos suele requerir interrupciones del servicio.

Para solucionar estos problemas surgió **LVM (Logical Volume Manager)**, una tecnología que permite administrar el almacenamiento de forma mucho más flexible.

LVM desacopla las particiones físicas del sistema de archivos, permitiendo ampliar, reducir o mover volúmenes con mucha mayor facilidad.

En Windows existen tecnologías equivalentes como los **Discos dinámicos** y, actualmente, **Storage Spaces (Espacios de almacenamiento)**.

---

### ¿Qué es LVM?

**LVM (Logical Volume Manager)** es un sistema de gestión de almacenamiento utilizado principalmente en Linux.

Su función consiste en crear una capa lógica entre los discos físicos y los sistemas de archivos.

Gracias a ello es posible:

- Ampliar discos fácilmente.
- Combinar varios discos físicos.
- Crear instantáneas (Snapshots).
- Migrar datos entre discos.
- Reorganizar el almacenamiento sin modificar las aplicaciones.

Es una de las tecnologías más utilizadas en servidores Linux.

---

### Arquitectura de LVM

LVM se organiza en tres niveles principales:

```text
Discos físicos

↓

Physical Volumes (PV)

↓

Volume Groups (VG)

↓

Logical Volumes (LV)

↓

Sistema de archivos
```

Cada uno de estos niveles cumple una función específica dentro de la administración del almacenamiento.

---

### Physical Volume (PV)

El **Physical Volume (PV)** representa un disco físico o una partición preparada para ser utilizada por LVM.

Ejemplo:

```text
/dev/sdb

↓

Physical Volume (PV)
```

Un mismo Volume Group puede estar formado por uno o varios Physical Volumes.

---

### Volume Group (VG)

El **Volume Group (VG)** agrupa uno o varios Physical Volumes y crea un único espacio de almacenamiento.

Puede imaginarse como un gran depósito de espacio libre.

Ejemplo:

```text
Disco 1

+

Disco 2

+

Disco 3

↓

VG_DATOS
```

Todo el espacio disponible podrá repartirse posteriormente entre distintos volúmenes lógicos.

---

### Logical Volume (LV)

Los **Logical Volumes (LV)** son los volúmenes que realmente utiliza el sistema operativo.

Sobre ellos se crea posteriormente el sistema de archivos.

Ejemplo:

```text
VG_DATOS

↓

LV_Sistema

LV_Datos

LV_Backups
```

Cada Logical Volume puede utilizar un sistema de archivos diferente.

---

### Flujo de funcionamiento

La estructura completa de LVM puede resumirse así:

```text
Discos físicos

↓

PV

↓

VG

↓

LV

↓

Sistema de archivos

↓

Punto de montaje
```

Esta separación permite administrar el almacenamiento de forma muy flexible.

---

### Ventajas de LVM

LVM ofrece numerosas ventajas frente al particionado tradicional.

Entre ellas:

- Ampliación sencilla de discos.
- Redimensionamiento dinámico.
- Gestión centralizada del almacenamiento.
- Creación de Snapshots.
- Migración entre discos.
- Administración de múltiples dispositivos como si fueran uno solo.

Estas características hacen que sea muy habitual en servidores Linux.

---

### Creación de un entorno LVM

El proceso habitual consiste en:

```text
Disco

↓

Crear PV

↓

Crear VG

↓

Crear LV

↓

Formatear

↓

Montar
```

Cada paso puede realizarse independientemente.

---

### Consultar la configuración

Linux proporciona diferentes comandos para consultar la información de LVM.

Mostrar Physical Volumes:

```bash
pvs
```

Mostrar Volume Groups:

```bash
vgs
```

Mostrar Logical Volumes:

```bash
lvs
```

Información detallada:

```bash
pvdisplay
vgdisplay
lvdisplay
```

---

### Ampliar un volumen lógico

Una de las principales ventajas de LVM consiste en ampliar fácilmente un volumen lógico.

Ejemplo:

```bash
lvextend -L +20G /dev/vgdatos/lvdatos
```

Tras ampliar el volumen será necesario extender también el sistema de archivos correspondiente.

Dependiendo del sistema de archivos utilizado, esto puede hacerse incluso con el volumen montado.

---

### Reducir un volumen lógico

También es posible reducir el tamaño de un volumen lógico.

Sin embargo:

> Reducir un volumen siempre implica mayor riesgo que ampliarlo.

Antes de hacerlo conviene:

- Realizar una copia de seguridad.
- Reducir primero el sistema de archivos (si procede).
- Verificar que existe espacio libre suficiente.

---

### Snapshots

Una de las funciones más interesantes de LVM son los **Snapshots**.

Un Snapshot crea una instantánea del estado del volumen en un momento concreto.

Ejemplo:

```text
Volumen

↓

Snapshot

↓

Actualización

↓

Restauración si es necesario
```

Los Snapshots permiten:

- Probar actualizaciones.
- Recuperar cambios rápidamente.
- Facilitar tareas de mantenimiento.

---

### Migración entre discos

LVM permite mover datos entre discos sin necesidad de detener el sistema.

Ejemplo:

```text
Disco antiguo

↓

Nuevo disco

↓

Migración

↓

Retirada del disco antiguo
```

Esto resulta muy útil durante ampliaciones o sustituciones de hardware.

---

### Sistemas de archivos compatibles

Los volúmenes LVM pueden utilizar distintos sistemas de archivos.

Los más habituales son:

- ext4
- XFS
- Btrfs
- ReiserFS (obsoleto)

LVM es independiente del sistema de archivos utilizado.

---

### Administración avanzada

Entre las operaciones más habituales encontramos:

- Crear nuevos volúmenes.
- Eliminar volúmenes.
- Ampliar Volume Groups.
- Sustituir discos.
- Crear Snapshots.
- Consultar el estado del almacenamiento.

Estas tareas pueden realizarse sin modificar las aplicaciones que utilizan los datos.

---

### Equivalente en Windows

Windows incorpora tecnologías con funcionalidades similares a LVM.

#### Discos dinámicos

Permiten:

- Volúmenes distribuidos.
- Volúmenes reflejados.
- Volúmenes RAID por software.

Actualmente su uso es cada vez menos frecuente.

---

#### Storage Spaces

La solución recomendada actualmente por Microsoft es **Storage Spaces (Espacios de almacenamiento)**.

Permite:

- Agrupar varios discos.
- Crear almacenamiento redundante.
- Ampliar capacidad fácilmente.
- Añadir nuevos discos sin interrumpir el servicio.

Su filosofía es muy similar a la utilizada por LVM.

---

### Comparativa

| Linux | Windows |
|--------|----------|
| Physical Volume (PV) | Disco físico |
| Volume Group (VG) | Storage Pool |
| Logical Volume (LV) | Disco virtual |
| LVM | Storage Spaces |

---

### Buenas prácticas

- Utiliza LVM en servidores cuyo almacenamiento pueda crecer con el tiempo.
- Planifica correctamente el tamaño inicial del Volume Group.
- Mantén espacio libre dentro del VG para futuras ampliaciones.
- Realiza copias de seguridad antes de reducir volúmenes.
- Utiliza Snapshots antes de realizar cambios importantes.
- Supervisa periódicamente el estado de los discos físicos.
- Documenta la estructura de PV, VG y LV.
- Evita llenar completamente el Volume Group para facilitar futuras ampliaciones.

---

[⬆️ Volver al índice](#índice)

## Sistemas de archivos avanzados

El sistema de archivos es el componente encargado de organizar y gestionar la información almacenada en un dispositivo de almacenamiento.

Su función consiste en definir cómo se guardan los datos, cómo se recuperan y cómo se administran elementos como permisos, directorios, nombres de archivos o metadatos.

Aunque existen numerosos sistemas de archivos, algunos están especialmente diseñados para servidores, grandes volúmenes de información o entornos empresariales donde el rendimiento, la integridad de los datos y la disponibilidad son fundamentales.

---

### ¿Qué es un sistema de archivos?

Un **sistema de archivos** es la estructura lógica que utiliza un sistema operativo para almacenar y organizar la información en un dispositivo.

Se encarga de gestionar:

- Archivos.
- Diectorios.
- Permisos.
- Espacio libre.
- Metadatos.
- Integridad de los datos.

Sin un sistema de archivos, el sistema operativo no podría interpretar correctamente la información almacenada en un disco.

---

### Funciones principales

Todo sistema de archivos permite:

- Crear archivos.
- Eliminar archivos.
- Organizar directorios.
- Asignar permisos.
- Gestionar el espacio disponible.
- Mantener la integridad de la información.
- Recuperarse ante fallos de sistema.

Cada sistema implementa estas funciones de manera diferente.

---

### Sistemas de archivos más utilizados

En entornos profesionales destacan principalmente:

**Linux**

- ext4
- XFS
- Btrfs
- ZFS

**Windows**

- NTFS
- ReFS

Cada uno presenta ventajas específicas dependiendo del escenario.

---

### ext4

**ext4 (Fourth Extended Filesystem)** es el sistema de archivos más utilizado en distribuciones Linux.

**Características:**

- Muy estable.
- Excelente compatibilidad.
- Bajo consumo de recursos.
- Journaling.
- Buen rendimiento general.

**Se utiliza habitualmente en:**

- Equipos personales.
- Servidores Linux.
- Máquinas virtuales.

---

### XFS

**XFS** fue diseñado para trabajar con grandes volúmenes de información.

**Características:**

- Excelente rendimiento.
- Muy eficiente con archivos grandes.
- Gran escalabilidad.
- Journaling.

Es muy habitual en:

- Servidores empresariales.
- Sistemas de almacenamiento.
- Bases de datos.
- Virtualización.

---

### Btrfs

**Btrfs (B-tree File System)** incorpora numerosas funciones avanzadas integradas.

Entre ellas:

- Snapshots.
- Compresión.
- Comprobación de integridad.
- Subvolúmenes.
- RAID integrado.
- Balanceo automático.

Es una alternativa moderna cuando se necesitan funciones avanzadas de administración.

---

### ZFS

**ZFS** es uno de los sistemas de archivos más completos disponibles actualmente.

**Características:**

- Integridad mediante checksum.
- Snapshots.
- Clonación.
- Compresión.
- Deduplicación.
- RAID integrado.
- Gestión avanzada del almacenamiento.

Se utiliza principalmente en:

- Servidores NAS.
- Centros de datos.
- Infraestructuras críticas.
- Grandes sistemas de almacenamiento.

Como inconveniente, suele requerir una mayor cantidad de memoria RAM.

---

### NTFS

**NTFS (New Technology File System)** es el sistema de archivos estándar de Windows.

**Características:**

- ACL (listas de control de acceso).
- Journaling.
- Compresión.
- Cifrado mediante EFS.
- Cuotas de disco.
- Gran compatibilidad.

Es el sistema utilizado por defecto en prácticamente todas las versiones modernas de Windows.

---

### ReFS

**ReFS (Resilient File System)** está orientado principalmente a servidores y grandes infraestructuras.

**Características:**

- Mayor resistencia frente a corrupción de datos.
- Comprobación automática de integridad.
- Escalabilidad.
- Integración con Storage Spaces.

Se utiliza habitualmente en:

- Servidores Windows.
- Virtualización.
- Grandes volúmenes de almacenamiento.

Actualmente convive con NTFS, ya que no todas las funciones de este último están presentes en ReFS.

---

### Journaling

Muchos sistemas de archivos modernos incorporan **Journaling**.

Antes de modificar los datos, registran previamente las operaciones que van a realizar.

Proceso:

```text
Cambio

↓

Registro (Journal)

↓

Escritura definitiva
```

Si el sistema se apaga inesperadamente:

- La recuperación resulta más rápida.
- Se reduce el riesgo de corrupción.
- Se mejora la consistencia del sistema de archivos.

---

### Integridad de datos

Algunos sistemas avanzados verifican automáticamente que los datos almacenados no se hayan corrompido.

Ejemplos:

- Btrfs.
- ZFS.
- ReFS.

Utilizan mecanismos como:

- Checksums.
- Verificación de bloques.
- Corrección automática cuando existe redundancia.

Esto mejora considerablemente la fiabilidad del almacenamiento.

---

### Snapshots

Algunos sistemas de archivos permiten crear **Snapshots**.

Un Snapshot representa el estado exacto del sistema de archivos en un instante determinado.

Ejemplo:

```text
Estado actual

↓

Snapshot

↓

Actualización

↓

Recuperación si es necesario
```

Los Snapshots facilitan:

- Actualizaciones seguras.
- Recuperación rápida.
- Pruebas de configuración.
- Copias consistentes.

---

### Compresión

Algunos sistemas permiten almacenar los datos comprimidos automáticamente.

**Ventajas:**

- Menor consumo de espacio.
- Reducción del tráfico de almacenamiento.

**Inconvenientes:**

- Mayor uso del procesador.

La compresión suele realizarse de forma transparente para el usuario.

---

### Deduplicación

La deduplicación evita almacenar varias copias idénticas de un mismo bloque de datos.

Ejemplo:

```text
Archivo A

Archivo A

Archivo A

↓

Una única copia física
```

Esto permite ahorrar una gran cantidad de espacio en determinados entornos.

---

### Compatibilidad

No todos los sistemas operativos admiten los mismos sistemas de archivos.

| Sistema operativo | Sistemas habituales |
|-------------------|---------------------|
| Linux | ext4, XFS, Btrfs, ZFS |
| Windows | NTFS, ReFS |
| macOS | APFS |

En entornos mixtos suele utilizarse **NTFS** o **exFAT** para facilitar el intercambio de información.

---

### ¿Qué sistema de archivos elegir?

La elección depende del escenario.

| Escenario | Sistema recomendado |
|-----------|---------------------|
| Linux general | ext4 |
| Grandes servidores Linux | XFS |
| Snapshots y administración avanzada | Btrfs |
| Máxima integridad | ZFS |
| Windows general | NTFS |
| Grandes servidores Windows | ReFS |

No existe un sistema de archivos perfecto para todas las situaciones.

---

### Comparativa

| Sistema | Plataforma | Ventaja principal |
|----------|------------|-------------------|
| ext4 | Linux | Estabilidad |
| XFS | Linux | Alto rendimiento |
| Btrfs | Linux | Snapshots y funciones avanzadas |
| ZFS | Linux/BSD | Máxima integridad |
| NTFS | Windows | Compatibilidad y seguridad |
| ReFS | Windows Server | Alta resiliencia |

---

### Buenas prácticas

- Utiliza el sistema de archivos más adecuado para cada tipo de servidor.
- Activa el Journaling siempre que esté disponible.
- Supervisa periódicamente el estado del sistema de archivos.
- Ejecuta comprobaciones de integridad cuando el sistema lo permita.
- Aprovecha los Snapshots antes de realizar cambios importantes.
- Mantén suficiente espacio libre para evitar pérdidas de rendimiento.
- Documenta el sistema de archivos utilizado en cada servidor.
- Recuerda que ningún sistema de archivos sustituye una estrategia adecuada de copias de seguridad.

---

[⬆️ Volver al índice](#índice)

## Almacenamiento en red

En entornos empresariales es habitual que la información no se almacene únicamente en los discos internos de cada equipo o servidor, sino en dispositivos accesibles a través de la red.

El **almacenamiento en red** permite centralizar la información, compartir recursos entre múltiples usuarios y mejorar la disponibilidad, la escalabilidad y la administración del almacenamiento.

Las tecnologías más utilizadas son **NAS**, **SAN**, **SMB/CIFS**, **NFS**, **iSCSI** y **Fibre Channel**, cada una diseñada para cubrir necesidades diferentes.

---

### ¿Qué es el almacenamiento en red?

El almacenamiento en red consiste en guardar la información en dispositivos conectados a una red para que pueda ser utilizada por distintos equipos.

En lugar de acceder a un disco local, los sistemas utilizan recursos remotos.

Ejemplo:

```text
Servidor

↓

Red

↓

Dispositivo de almacenamiento

↓

Datos
```

Desde el punto de vista del usuario, el acceso suele ser completamente transparente.

---

### Ventajas

El almacenamiento en red ofrece numerosas ventajas.

Entre las más importantes destacan:

- Centralización de la información.
- Compartición sencilla de archivos.
- Mayor disponibilidad.
- Escalabilidad.
- Administración simplificada.
- Copias de seguridad centralizadas.
- Mejor aprovechamiento del almacenamiento.

Estas características hacen que sea la solución habitual en empresas.

---

### Inconvenientes

También presenta algunas limitaciones.

Las más habituales son:

- Dependencia de la red.
- Posibles cuellos de botella.
- Mayor coste en infraestructuras complejas.
- Mayor complejidad administrativa.
- Necesidad de gestionar correctamente permisos y accesos.

Por ello resulta fundamental diseñar adecuadamente la infraestructura.

---

### NAS (Network Attached Storage)

Un **NAS (Network Attached Storage)** es un dispositivo especializado en compartir archivos mediante la red.

Su principal función consiste en ofrecer carpetas compartidas a distintos usuarios y equipos.

**Características:**

- Administración sencilla.
- Bajo coste.
- Interfaz web.
- Compartición mediante SMB o NFS.
- Soporte para RAID.
- Fácil ampliación de capacidad.

Es la solución más habitual para:

- Servidores de archivos.
- Oficinas.
- Copias de seguridad.
- Pequeñas y medianas empresas.

---

### Funcionamiento de un NAS

El funcionamiento puede representarse así:

```text
Equipo

↓

Red

↓

NAS

↓

Carpeta compartida
```

El usuario trabaja con los archivos como si estuvieran almacenados localmente.

---

### SAN (Storage Area Network)

Una **SAN (Storage Area Network)** proporciona almacenamiento a nivel de bloques mediante una red dedicada.

A diferencia de un NAS, el servidor interpreta ese almacenamiento como si fuera un disco físico conectado directamente.

**Características:**

- Muy alto rendimiento.
- Baja latencia.
- Gran disponibilidad.
- Alta escalabilidad.
- Infraestructura especializada.

Se utiliza principalmente en:

- Virtualización.
- Bases de datos.
- Clústeres.
- Centros de datos.

---

### Funcionamiento de una SAN

El flujo habitual sería:

```text
Servidor

↓

SAN

↓

Cabina de almacenamiento

↓

Disco lógico
```

Para el sistema operativo, el almacenamiento aparece como un disco local.

---

### Diferencias entre NAS y SAN

Aunque ambos permiten compartir almacenamiento, funcionan de forma diferente.

| NAS | SAN |
|------|-----|
| Comparte archivos | Comparte bloques |
| Acceso mediante SMB o NFS | Acceso mediante iSCSI o Fibre Channel |
| Fácil de administrar | Más complejo |
| Menor coste | Mayor coste |
| Ideal para documentos | Ideal para servidores y virtualización |

---

### SMB/CIFS

**SMB (Server Message Block)** es el protocolo de compartición de archivos utilizado principalmente por Windows.

Permite:

- Compartir carpetas.
- Compartir impresoras.
- Controlar permisos.
- Acceder a recursos remotos.

En Linux puede utilizarse mediante **Samba**.

Es el protocolo más habitual en redes Windows.

---

### NFS (Network File System)

**NFS** es el protocolo de compartición de archivos utilizado tradicionalmente en sistemas Linux y Unix.

**Características:**

- Integración nativa con Linux.
- Alto rendimiento.
- Administración sencilla.
- Muy utilizado en servidores Linux.

Es habitual encontrarlo en:

- Clústeres.
- Virtualización.
- Infraestructuras Linux.

---

### Comparativa SMB y NFS

| SMB | NFS |
|------|-----|
| Principalmente Windows | Principalmente Linux |
| Utiliza Samba en Linux | Integrado en Linux |
| Muy habitual en oficinas | Muy habitual en servidores |

---

### iSCSI

**iSCSI (Internet Small Computer Systems Interface)** permite acceder a almacenamiento remoto utilizando redes IP.

El sistema operativo interpreta el almacenamiento remoto como un disco local.

Proceso:

```text
Servidor

↓

Red IP

↓

iSCSI

↓

Cabina de almacenamiento
```

Es muy utilizado en:

- Virtualización.
- Clústeres.
- Servidores.
- SAN basadas en Ethernet.

---

### Fibre Channel

**Fibre Channel (FC)** es una tecnología de alta velocidad diseñada específicamente para redes SAN.

**Características:**

- Muy alta velocidad.
- Muy baja latencia.
- Gran fiabilidad.
- Red dedicada.

Se utiliza principalmente en:

- Grandes centros de datos.
- Infraestructuras críticas.
- Sistemas empresariales.

Su coste es considerablemente superior al de soluciones basadas en Ethernet.

---

### Permisos en almacenamiento compartido

Cuando varios usuarios acceden a un mismo recurso resulta imprescindible controlar los permisos.

Normalmente se gestionan mediante:

- Usuarios.
- Grupos.
- ACL (Access Control Lists).

Ejemplo:

```text
RRHH

↓

Lectura y escritura
```

```text
Resto de departamentos

↓

Sin acceso
```

Una correcta configuración evita accesos no autorizados.

---

### Alta disponibilidad

En infraestructuras críticas es habitual implementar mecanismos de redundancia.

Los más utilizados son:

- RAID.
- Varias controladoras.
- Varias interfaces de red.
- Fuentes de alimentación redundantes.
- Replicación entre dispositivos.

El objetivo es mantener el servicio disponible incluso ante fallos de hardware.

---

### Monitorización

Conviene supervisar continuamente:

- Espacio libre.
- Estado del RAID.
- Estado SMART de los discos.
- Latencia.
- Rendimiento.
- Uso de red.
- Temperatura.

Muchos dispositivos NAS y SAN permiten generar alertas automáticas por correo electrónico o integrarse con plataformas de monitorización.

---

### Copias de seguridad

Aunque un NAS o una SAN incorporen RAID, **no sustituyen una copia de seguridad**.

```text
RAID

≠

Backup
```

Siempre debe existir una estrategia de backup independiente que proteja frente a:

- Eliminaciones accidentales.
- Ransomware.
- Corrupción de datos.
- Errores humanos.
- Desastres físicos.

---

### Escenarios habituales

**Servidor de archivos**

```text
Usuarios

↓

NAS

↓

Documentación compartida
```

**Virtualización**

```text
Servidores

↓

iSCSI

↓

Cabina SAN
```

**Copias de seguridad**

```text
Servidores

↓

Red

↓

NAS dedicado
```

Cada tecnología está orientada a un escenario distinto.

---

### Comparativa

| Tecnología | Nivel de acceso | Uso habitual |
|------------|-----------------|--------------|
| NAS | Archivos | Compartición de documentos |
| SAN | Bloques | Virtualización y bases de datos |
| SMB | Archivos | Redes Windows |
| NFS | Archivos | Redes Linux |
| iSCSI | Bloques | Servidores sobre Ethernet |
| Fibre Channel | Bloques | Centros de datos |

---

### Buenas prácticas

- Utiliza NAS para compartir archivos y SAN para cargas de trabajo de alto rendimiento.
- Aplica el principio de mínimo privilegio al configurar permisos.
- Implementa RAID para mejorar la disponibilidad, pero mantén siempre copias de seguridad independientes.
- Supervisa periódicamente el estado de discos, red y rendimiento.
- Utiliza redes dedicadas para iSCSI o Fibre Channel cuando sea posible.
- Documenta todos los recursos compartidos y los permisos asignados.
- Protege los servicios mediante autenticación y cifrado cuando esté disponible.

---

[⬆️ Volver al índice](#índice)

## Cuotas de disco

Las **cuotas de disco** permiten limitar la cantidad de espacio de almacenamiento que pueden utilizar los usuarios o grupos dentro de un sistema de archivos.

Su principal objetivo es evitar que un único usuario consuma todo el espacio disponible del servidor, garantizando un uso equilibrado de los recursos y facilitando la administración del almacenamiento.

Las cuotas están disponibles tanto en Linux como en Windows y son especialmente útiles en servidores de archivos, entornos educativos y organizaciones donde múltiples usuarios comparten el mismo almacenamiento.

---

### ¿Qué son las cuotas de disco?

Las cuotas de disco son mecanismos que permiten controlar el uso del almacenamiento asignando límites a usuarios o grupos.

Mediante las cuotas es posible:

- Limitar el espacio ocupado.
- Controlar el número de archivos creados.
- Supervisar el consumo de almacenamiento.
- Evitar el agotamiento del espacio disponible.

Su funcionamiento es completamente transparente para el usuario.

---

### Objetivos de las cuotas

Las cuotas ayudan a:

- Evitar que un usuario ocupe todo el disco.
- Repartir el almacenamiento de forma equitativa.
- Facilitar la planificación de capacidad.
- Detectar consumos anómalos.
- Reducir incidencias por falta de espacio.

Son una herramienta muy utilizada en servidores compartidos.

---

### Tipos de cuotas

Existen dos tipos principales.

#### Cuota por usuario

Limita el almacenamiento utilizado por cada usuario.

Ejemplo:

```text
Usuario Ana

↓

100 GB
```

Cada usuario dispone de su propio límite.

---

#### Cuota por grupo

Limita el espacio utilizado conjuntamente por un grupo.

Ejemplo:

```text
Grupo Marketing

↓

500 GB
```

Todos los miembros comparten la misma cuota.

---

### Límite flexible (Soft Limit)

El **Soft Limit** establece un límite recomendado.

Cuando el usuario lo supera:

- Puede seguir escribiendo información durante un tiempo determinado.
- El sistema genera advertencias.

Ejemplo:

```text
Soft Limit

↓

100 GB

↓

Aviso al usuario
```

---

### Límite estricto (Hard Limit)

El **Hard Limit** representa el límite máximo permitido.

Cuando se alcanza:

- No pueden escribirse más datos.
- El sistema bloquea nuevas operaciones de escritura.

Ejemplo:

```text
Hard Limit

↓

120 GB

↓

Escritura bloqueada
```

---

### Periodo de gracia (Grace Period)

El periodo de gracia es el tiempo durante el cual un usuario puede superar el **Soft Limit** antes de alcanzar el límite definitivo.

Proceso:

```text
Supera Soft Limit

↓

Periodo de gracia

↓

Debe reducir el espacio utilizado

↓

Si no lo hace

↓

Se aplica el Hard Limit
```

---

### Cuotas en Linux

Linux incorpora soporte para cuotas mediante el sistema de archivos.

Las herramientas más habituales son:

- `quota`
- `quotacheck`
- `edquota`
- `repquota`
- `setquota`

Normalmente requieren que el sistema de archivos tenga habilitado el soporte para cuotas.

---

### Consultar cuotas en Linux

Algunos comandos habituales son:

Consultar la cuota del usuario:

```bash
quota
```

Mostrar todas las cuotas:

```bash
repquota -a
```

Modificar cuotas:

```bash
edquota usuario
```

Estas herramientas permiten administrar fácilmente los límites asignados.

---

### Cuotas en Windows

Windows permite configurar cuotas desde las propiedades del volumen NTFS.

Es posible:

- Activar cuotas.
- Limitar espacio por usuario.
- Generar avisos.
- Bloquear escrituras al alcanzar el límite.

La configuración puede realizarse desde:

```text
Propiedades del disco

↓

Cuotas
```

---

### Cuotas en servidores Windows

En entornos empresariales también puede utilizarse:

- **File Server Resource Manager (FSRM)**

FSRM permite:

- Cuotas avanzadas.
- Plantillas reutilizables.
- Informes.
- Alertas por correo.
- Clasificación de archivos.

Es la herramienta recomendada para Windows Server.

---

### Supervisión de cuotas

Conviene revisar periódicamente:

- Usuarios próximos al límite.
- Espacio libre.
- Crecimiento del almacenamiento.
- Alertas generadas.
- Tendencias de consumo.

La monitorización facilita detectar problemas antes de que afecten al servicio.

---

### Ventajas

El uso de cuotas ofrece numerosos beneficios.

Entre ellos:

- Evita el agotamiento del almacenamiento.
- Mejora el reparto de recursos.
- Facilita la administración.
- Reduce incidencias.
- Permite detectar consumos anómalos.

---

### Limitaciones

Las cuotas también presentan algunas limitaciones.

Por ejemplo:

- No sustituyen una correcta planificación del almacenamiento.
- Requieren supervisión periódica.
- Deben adaptarse al crecimiento de los usuarios.
- Pueden resultar insuficientes si el almacenamiento disponible es escaso.

---

### Comparativa

| Tipo | Característica |
|------|----------------|
| Cuota por usuario | Límite individual |
| Cuota por grupo | Límite compartido |
| Soft Limit | Genera avisos |
| Hard Limit | Bloquea la escritura |

---

### Buenas prácticas

- Configura cuotas en servidores compartidos.
- Utiliza Soft Limit antes de aplicar Hard Limit.
- Establece periodos de gracia razonables.
- Revisa periódicamente el consumo de almacenamiento.
- Genera alertas automáticas cuando un usuario se acerque al límite.
- Ajusta las cuotas según las necesidades reales de cada departamento.
- Documenta todas las cuotas configuradas.
- Combina las cuotas con una estrategia adecuada de monitorización y copias de seguridad.

---

[⬆️ Volver al índice](#índice)

## Monitorización y mantenimiento

La monitorización y el mantenimiento del almacenamiento permiten garantizar el correcto funcionamiento de discos, sistemas de archivos y dispositivos de almacenamiento a lo largo del tiempo.

Un almacenamiento puede comenzar a degradarse mucho antes de fallar completamente. Detectar estos problemas de forma anticipada reduce el riesgo de pérdida de datos, mejora la disponibilidad del servicio y facilita la planificación de sustituciones de hardware.

Por este motivo, la supervisión continua forma parte de cualquier estrategia de administración de sistemas.

---

### Objetivos de la monitorización

La monitorización del almacenamiento permite:

- Detectar discos defectuosos.
- Identificar problemas de rendimiento.
- Supervisar el espacio disponible.
- Prevenir pérdidas de información.
- Planificar ampliaciones de capacidad.
- Detectar cuellos de botella.

Cuanto antes se detecte un problema, menor será su impacto.

---

### Elementos que deben supervisarse

En cualquier infraestructura es recomendable controlar:

- Estado físico de los discos.
- Espacio libre.
- Rendimiento de lectura y escritura.
- Latencia.
- Temperatura.
- Estado del RAID.
- Estado del sistema de archivos.
- Uso de IOPS.
- Eventos del sistema.

La combinación de todos estos indicadores ofrece una visión completa del estado del almacenamiento.

---

### Estado SMART

La mayoría de discos HDD y SSD incorporan la tecnología **SMART (Self-Monitoring, Analysis and Reporting Technology)**.

SMART registra información sobre el estado interno del dispositivo.

Entre los parámetros más importantes se encuentran:

- Horas de funcionamiento.
- Sectores reasignados.
- Errores de lectura.
- Errores de escritura.
- Temperatura.
- Número de encendidos.
- Vida útil restante (SSD).

Es uno de los primeros indicadores de un posible fallo físico.

---

### Consultar SMART en Linux

La herramienta más utilizada es **smartctl**, incluida en el paquete **smartmontools**.

Consultar el estado general:

```bash
smartctl -H /dev/sda
```

Mostrar toda la información:

```bash
smartctl -a /dev/sda
```

Ejecutar un test corto:

```bash
smartctl -t short /dev/sda
```

---

### Consultar SMART en Windows

Windows permite consultar parte de esta información mediante PowerShell o herramientas específicas del fabricante.

Ejemplo:

```powershell
Get-PhysicalDisk
```

También es habitual utilizar utilidades como:

- CrystalDiskInfo.
- Dell OpenManage.
- HPE Smart Storage Administrator.
- Samsung Magician (SSD Samsung).

---

### Espacio libre

Uno de los aspectos más importantes es controlar el espacio disponible.

Un volumen cercano al 100 % de ocupación puede provocar:

- Disminución del rendimiento.
- Errores de escritura.
- Fallos en bases de datos.
- Problemas en aplicaciones.

Se recomienda mantener siempre un margen de espacio libre.

---

### Rendimiento del almacenamiento

También conviene supervisar el rendimiento.

Los indicadores más habituales son:

- Velocidad de lectura.
- Velocidad de escritura.
- IOPS.
- Latencia.
- Cola de operaciones.

Estos parámetros permiten detectar cuellos de botella.

---

### IOPS

Las **IOPS (Input/Output Operations Per Second)** indican el número de operaciones de entrada y salida que un dispositivo puede realizar cada segundo.

Generalmente:

- HDD → pocas IOPS.
- SSD SATA → muchas más IOPS.
- NVMe → cientos de miles de IOPS.

Las bases de datos y la virtualización dependen especialmente de este indicador.

---

### Latencia

La latencia representa el tiempo que tarda el almacenamiento en responder a una petición.

Cuanto menor sea la latencia:

- Más rápido responderá el sistema.
- Mejor será el rendimiento percibido.

Los SSD NVMe presentan latencias muy inferiores a los discos mecánicos.

---

### Monitorización del RAID

Cuando existe un RAID es importante comprobar periódicamente:

- Estado de los discos.
- Reconstrucciones.
- Errores de la controladora.
- Hot Spare.
- Degradación del volumen.

Muchos fabricantes proporcionan herramientas específicas para esta tarea.

---

### Estado del sistema de archivos

Además del hardware, también debe supervisarse el sistema de archivos.

Conviene revisar:

- Errores.
- Corrupciones.
- Espacio libre.
- Integridad.
- Journaling.

En Linux pueden utilizarse herramientas como:

```bash
fsck
```

En Windows:

```powershell
chkdsk
```

---

### Alertas

Una buena infraestructura debe generar avisos automáticos cuando se detecten problemas.

Ejemplos:

- Disco averiado.
- RAID degradado.
- Poco espacio libre.
- Temperatura elevada.
- Fallo SMART.
- Sistema de archivos corrupto.

Las alertas permiten actuar antes de que aparezcan incidencias graves.

---

### Herramientas de monitorización

Existen numerosas herramientas para supervisar el almacenamiento.

Algunas de las más utilizadas son:

**Linux**

- smartctl
- iostat
- df
- lsblk
- dmesg

**Windows**

- Performance Monitor
- Event Viewer
- PowerShell
- Storage Spaces
- Windows Admin Center

**Multiplataforma**

- Zabbix.
- PRTG.
- Nagios.
- Prometheus.
- Grafana.

---

### Mantenimiento preventivo

Además de monitorizar, es recomendable realizar tareas periódicas.

Por ejemplo:

- Revisar SMART.
- Sustituir discos degradados.
- Actualizar firmware.
- Comprobar el RAID.
- Revisar logs.
- Verificar copias de seguridad.
- Comprobar la capacidad disponible.

El mantenimiento preventivo reduce significativamente el riesgo de fallos inesperados.

---

### Sustitución de discos

Los discos tienen una vida útil limitada.

Cuando SMART indique degradación o el fabricante lo recomiende, conviene sustituir el disco antes de que falle completamente.

Especialmente en:

- RAID.
- Bases de datos.
- Servidores críticos.

Esperar al fallo completo aumenta el riesgo de pérdida de datos.

---

### Comparativa

| Elemento | Qué supervisa |
|----------|---------------|
| SMART | Estado físico del disco |
| Espacio libre | Capacidad disponible |
| IOPS | Operaciones por segundo |
| Latencia | Tiempo de respuesta |
| RAID | Estado de redundancia |
| Sistema de archivos | Integridad de los datos |

---

### Buenas prácticas

- Supervisa continuamente el estado SMART de todos los discos.
- Configura alertas automáticas para fallos de hardware y falta de espacio.
- Mantén siempre espacio libre suficiente en los volúmenes.
- Sustituye los discos degradados antes de que fallen completamente.
- Comprueba periódicamente el estado del RAID y de los sistemas de archivos.
- Actualiza el firmware de discos y controladoras cuando sea recomendable.
- Documenta las tareas de mantenimiento realizadas.
- Integra la monitorización del almacenamiento en la plataforma de supervisión general de la infraestructura.

---

[⬆️ Volver al índice](#índice)

## Recuperación de almacenamiento

A pesar de aplicar medidas como RAID, copias de seguridad o monitorización, pueden producirse incidencias que afecten al almacenamiento de un sistema.

La recuperación del almacenamiento engloba el conjunto de técnicas destinadas a restaurar el acceso a los datos o al funcionamiento normal de la infraestructura tras un fallo.

Dependiendo del problema, la recuperación puede consistir en reparar un sistema de archivos, reconstruir un RAID, restaurar una copia de seguridad o recuperar información eliminada accidentalmente.

---

### Objetivos de la recuperación

La recuperación del almacenamiento busca:

- Restaurar el acceso a los datos.
- Reducir el tiempo de inactividad.
- Minimizar la pérdida de información.
- Garantizar la continuidad del servicio.
- Recuperar el funcionamiento normal del sistema.

Una buena planificación facilita enormemente este proceso.

---

### Tipos de incidencias

Los problemas más habituales relacionados con el almacenamiento son:

- Fallo de un disco.
- Corrupción del sistema de archivos.
- Eliminación accidental de información.
- RAID degradado.
- Fallo de la controladora.
- Errores SMART.
- Daños físicos.
- Ataques de ransomware.

Cada situación requiere un procedimiento diferente.

---

### Recuperación tras el fallo de un disco

Si un disco falla y existe redundancia (por ejemplo, RAID 1, RAID 5, RAID 6 o RAID 10), el procedimiento habitual consiste en:

```text
Disco averiado

↓

Sustitución

↓

Reconstrucción del RAID

↓

Sistema operativo
```

Mientras el RAID permanezca íntegro, normalmente no será necesario restaurar copias de seguridad.

---

### Recuperación del sistema de archivos

Cuando un sistema de archivos presenta errores puede ser necesario repararlo.

En Linux:

```bash
fsck
```

En Windows:

```powershell
chkdsk
```

Estas herramientas analizan la estructura del sistema de archivos e intentan corregir inconsistencias.

Siempre que sea posible, conviene realizar una copia de seguridad antes de ejecutar procesos de reparación.

---

### Restauración desde copias de seguridad

Cuando los datos no pueden recuperarse directamente, la solución consiste en restaurar una copia de seguridad.

Proceso:

```text
Incidencia

↓

Seleccionar backup

↓

Restauración

↓

Verificación
```

La restauración debe comprobarse siempre para garantizar que la información recuperada es válida.

---

### Recuperación de archivos eliminados

Si un archivo ha sido eliminado accidentalmente:

- Evita escribir nuevos datos sobre el disco.
- Aísla el dispositivo si es posible.
- Utiliza herramientas especializadas de recuperación.

Cuanto antes se actúe, mayores serán las probabilidades de éxito.

---

### Recuperación de particiones

En algunos casos la información sigue existiendo, pero la tabla de particiones ha resultado dañada.

Herramientas como **TestDisk** permiten:

- Detectar particiones perdidas.
- Reconstruir tablas de particiones.
- Restaurar el acceso al sistema de archivos.

Este tipo de recuperación suele ser muy eficaz cuando el daño afecta únicamente a la estructura lógica.

---

### Recuperación de datos

Cuando el sistema de archivos está gravemente dañado pueden utilizarse herramientas de recuperación de datos.

Algunas de las más conocidas son:

- TestDisk.
- PhotoRec.
- R-Studio.
- EaseUS Data Recovery.
- Recuva.

Estas aplicaciones buscan directamente los datos en el dispositivo intentando reconstruir los archivos originales.

---

### Recuperación tras un ransomware

En un incidente de ransomware nunca debe asumirse que el pago garantiza la recuperación.

El procedimiento recomendado suele ser:

```text
Aislar el equipo

↓

Eliminar el malware

↓

Restaurar copias de seguridad

↓

Verificar la integridad

↓

Volver a producción
```

Disponer de copias de seguridad desconectadas es la mejor protección frente a este tipo de ataques.

---

### Recuperación en entornos virtualizados

En plataformas de virtualización es habitual recuperar:

- Máquinas virtuales completas.
- Discos virtuales.
- Snapshots.
- Configuración del hipervisor.

Muchos hipervisores permiten restauraciones muy rápidas cuando existen snapshots o copias de seguridad recientes.

---

### Snapshots

Si el sistema de almacenamiento soporta snapshots (por ejemplo, Btrfs, ZFS o algunos NAS), la recuperación puede ser muy rápida.

Proceso:

```text
Estado actual

↓

Snapshot anterior

↓

Restauración

↓

Sistema operativo
```

Los snapshots reducen considerablemente el tiempo necesario para recuperar cambios recientes.

---

### Verificación tras la recuperación

Una vez finalizada la recuperación conviene comprobar:

- Integridad de los datos.
- Estado del sistema de archivos.
- Estado del RAID.
- Funcionamiento de las aplicaciones.
- Disponibilidad del servicio.

No debe darse por finalizada la recuperación hasta verificar que todo funciona correctamente.

---

### Recuperación ante fallo total

Si el almacenamiento queda completamente inutilizado, el procedimiento suele ser:

```text
Nuevo hardware

↓

Instalación

↓

Configuración

↓

Restauración de backups

↓

Validación

↓

Producción
```

Disponer de procedimientos documentados reduce significativamente el tiempo de recuperación.

---

### Herramientas habituales

**Linux**

- fsck
- TestDisk
- PhotoRec
- ddrescue
- smartctl

**Windows**

- chkdsk
- Recuva
- Windows Backup
- Historial de archivos
- Windows Server Backup

Cada herramienta está orientada a un tipo concreto de incidencia.

---

### Plan de recuperación

Toda organización debería disponer de un procedimiento documentado que incluya:

- Inventario del almacenamiento.
- Ubicación de las copias de seguridad.
- Prioridad de los sistemas.
- Responsables.
- Procedimientos de restauración.
- Verificación posterior.

Este plan facilita una respuesta rápida y coordinada ante cualquier incidente.

---

### Buenas prácticas

- Realiza copias de seguridad periódicas y verifica que pueden restaurarse correctamente.
- Documenta todos los procedimientos de recuperación.
- Sustituye inmediatamente los discos defectuosos.
- Utiliza snapshots antes de realizar cambios importantes.
- Comprueba periódicamente la integridad de los sistemas de archivos.
- Realiza simulacros de recuperación para validar los procedimientos.
- No utilices el disco afectado tras una pérdida de datos hasta completar la recuperación.
- Mantén un plan de continuidad de negocio actualizado.

---

[⬆️ Volver al índice](#índice)

## Buenas prácticas

La correcta administración del almacenamiento no depende únicamente de la tecnología utilizada, sino también de la aplicación de procedimientos adecuados durante todo el ciclo de vida de la infraestructura.

Implementar buenas prácticas permite mejorar el rendimiento, aumentar la disponibilidad de los servicios, reducir el riesgo de pérdida de datos y facilitar las tareas de administración y mantenimiento.

---

### Planificar el almacenamiento

Antes de implementar una infraestructura es recomendable analizar:

- Capacidad necesaria.
- Crecimiento previsto.
- Rendimiento requerido.
- Nivel de disponibilidad.
- Presupuesto disponible.

Una buena planificación evita futuras ampliaciones complejas y reduce costes a largo plazo.

---

### Elegir la tecnología adecuada

No todos los tipos de almacenamiento son apropiados para cualquier escenario.

Por ejemplo:

| Escenario | Tecnología recomendada |
|-----------|------------------------|
| Sistema operativo | SSD o NVMe |
| Bases de datos | SSD NVMe |
| Virtualización | RAID 10 + SSD |
| Servidor de archivos | NAS o RAID 5 |
| Copias de seguridad | HDD de alta capacidad |

Seleccionar correctamente la tecnología mejora el rendimiento y la vida útil de la infraestructura.

---

### Implementar redundancia

Siempre que la disponibilidad sea importante, conviene utilizar mecanismos de redundancia.

Los más habituales son:

- RAID.
- Fuentes de alimentación redundantes.
- Varias interfaces de red.
- Controladoras redundantes.
- Replicación del almacenamiento.

La redundancia reduce el impacto de los fallos de hardware.

---

### Mantener copias de seguridad

RAID protege frente al fallo de discos, pero no sustituye una copia de seguridad.

Toda infraestructura debería disponer de una estrategia de backup que contemple:

- Copias periódicas.
- Versionado.
- Restauraciones de prueba.
- Almacenamiento externo.
- Copias fuera de las instalaciones cuando sea necesario.

Sin una copia de seguridad válida no existe garantía de recuperación.

---

### Supervisar continuamente el almacenamiento

La monitorización permite detectar problemas antes de que afecten al servicio.

Conviene revisar:

- Estado SMART.
- Espacio libre.
- Estado del RAID.
- Rendimiento.
- Latencia.
- Temperatura.
- Eventos del sistema.

Las alertas automáticas facilitan una respuesta rápida ante cualquier incidencia.

---

### Mantener espacio libre

Un sistema de almacenamiento demasiado lleno puede provocar:

- Disminución del rendimiento.
- Errores de escritura.
- Problemas en bases de datos.
- Fallos en aplicaciones.

Como norma general, es recomendable mantener un porcentaje de espacio libre para garantizar el correcto funcionamiento del sistema.

---

### Documentar la infraestructura

Toda la información relacionada con el almacenamiento debería estar documentada.

Por ejemplo:

- Discos instalados.
- Configuración RAID.
- Sistemas de archivos.
- LVM o Storage Spaces.
- Recursos compartidos.
- Procedimientos de recuperación.

Una documentación actualizada facilita enormemente la administración y la resolución de incidencias.

---

### Verificar las copias de seguridad

Una copia de seguridad solo es útil si puede restaurarse correctamente.

Es recomendable realizar pruebas periódicas de restauración para comprobar:

- Integridad de los datos.
- Tiempo de recuperación.
- Funcionamiento de las aplicaciones restauradas.

Esto permite detectar problemas antes de una incidencia real.

---

### Sustituir hardware degradado

Los discos no fallan de forma repentina en todos los casos.

Muchos comienzan mostrando signos de degradación.

Cuando se detecten:

- Errores SMART.
- Sectores defectuosos.
- Temperaturas anómalas.
- Fallos repetitivos.

Debe planificarse la sustitución del dispositivo antes de que deje de funcionar completamente.

---

### Mantener el software actualizado

Conviene mantener actualizados:

- Firmware de discos.
- Controladoras RAID.
- Sistemas de archivos.
- Sistemas operativos.
- NAS y cabinas SAN.

Las actualizaciones suelen corregir errores y mejorar la estabilidad y la seguridad.

---

### Aplicar el principio de mínimo privilegio

El acceso al almacenamiento debe limitarse únicamente a quienes realmente lo necesiten.

Es recomendable:

- Asignar permisos mediante grupos.
- Revisar periódicamente los accesos.
- Eliminar permisos innecesarios.
- Registrar los cambios realizados.

Esto mejora la seguridad y reduce el riesgo de accesos no autorizados.

---

### Automatizar tareas

Muchas tareas de administración pueden automatizarse.

Por ejemplo:

- Supervisión.
- Informes.
- Alertas.
- Copias de seguridad.
- Limpieza de archivos temporales.

La automatización reduce errores humanos y ahorra tiempo.

---

### Revisar periódicamente la capacidad

El crecimiento del almacenamiento debe controlarse de forma continua.

Conviene analizar:

- Evolución del consumo.
- Tendencias de crecimiento.
- Necesidades futuras.
- Posibles ampliaciones.

Una planificación adecuada evita quedarse sin espacio de forma inesperada.

---

### Formar a los administradores

El personal encargado del almacenamiento debe conocer:

- RAID.
- LVM.
- Sistemas de archivos.
- Copias de seguridad.
- Procedimientos de recuperación.
- Herramientas de monitorización.

Una formación adecuada reduce errores operativos y mejora la capacidad de respuesta ante incidencias.

---

### Resumen de recomendaciones

Las principales recomendaciones para una correcta administración del almacenamiento son:

- Planificar la infraestructura antes de su implantación.
- Seleccionar la tecnología más adecuada para cada escenario.
- Implementar redundancia cuando la disponibilidad sea importante.
- Mantener copias de seguridad independientes del almacenamiento principal.
- Supervisar continuamente el estado de discos y sistemas de archivos.
- Sustituir el hardware degradado antes de que falle.
- Automatizar las tareas repetitivas.
- Documentar toda la infraestructura.
- Comprobar periódicamente la restauración de las copias de seguridad.
- Revisar la capacidad disponible y planificar futuras ampliaciones.

---

[⬆️ Volver al índice](#índice)