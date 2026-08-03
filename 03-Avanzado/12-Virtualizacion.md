# 12 - Virtualización

## Introducción

La virtualización es una tecnología que permite crear representaciones virtuales de recursos físicos como servidores, sistemas operativos, redes o almacenamiento.

Mediante un hipervisor es posible ejecutar múltiples máquinas virtuales sobre un único servidor físico, optimizando el uso del hardware, reduciendo costes y facilitando la administración de infraestructuras.

---

## Índice

- [Fundamentos de la virtualización](#fundamentos-de-la-virtualización)
- [Tipos de virtualización](#tipos-de-virtualización)
- [Hipervisores](#hipervisores)
- [Máquinas virtuales](#máquinas-virtuales)
- [Gestión de recursos virtuales](#gestión-de-recursos-virtuales)
- [Redes virtuales](#redes-virtuales)
- [Almacenamiento en entornos virtualizados](#almacenamiento-en-entornos-virtualizados)
- [Alta disponibilidad y migración](#alta-disponibilidad-y-migración)
- [Seguridad en virtualización](#seguridad-en-virtualización)
- [Copias de seguridad y recuperación en entornos virtuales](#copias-de-seguridad-y-recuperación-en-entornos-virtuales)
- [Monitorización y administración](#monitorización-y-administración)

---

## Fundamentos de la virtualización

La virtualización es una tecnología que permite crear versiones virtuales de recursos físicos, permitiendo ejecutar varios sistemas independientes sobre un mismo equipo físico.

En lugar de dedicar un servidor completo a una única aplicación, la virtualización permite dividir los recursos disponibles entre varias máquinas virtuales, mejorando el aprovechamiento del hardware y simplificando la administración de la infraestructura.

Actualmente es una de las tecnologías más utilizadas en centros de datos, servidores empresariales y entornos cloud.

---

### ¿Qué es la virtualización?

La virtualización consiste en crear una capa de abstracción entre el hardware físico y los sistemas que se ejecutan sobre él.

Esta capa permite que varios sistemas operativos funcionen de manera independiente utilizando los recursos de un mismo servidor.

Ejemplo:

```text
Servidor físico

        ↓

Hipervisor

        ↓

┌─────────────┐
│ Máquina VM  │ Windows Server
└─────────────┘

┌─────────────┐
│ Máquina VM  │ Linux
└─────────────┘

┌─────────────┐
│ Máquina VM  │ Base de datos
└─────────────┘
```

Cada máquina virtual funciona como si fuera un equipo independiente.

---

### Objetivos de la virtualización

Los principales objetivos son:

- Optimizar el uso del hardware.
- Reducir costes de infraestructura.
- Facilitar la administración.
- Aumentar la disponibilidad.
- Simplificar las copias de seguridad.
- Mejorar la recuperación ante fallos.
- Facilitar la escalabilidad.

---

### Funcionamiento básico

La virtualización funciona mediante un componente llamado **hipervisor**, encargado de gestionar los recursos físicos y asignarlos a las máquinas virtuales.

Proceso:

```text
Hardware físico

↓

Hipervisor

↓

Máquinas virtuales

↓

Sistemas operativos

↓

Aplicaciones
```

El hipervisor controla elementos como:

- CPU.
- Memoria RAM.
- Almacenamiento.
- Red.
- Dispositivos virtuales.

---

### Componentes de un entorno virtualizado

Un entorno de virtualización está formado por varios elementos:

#### Hardware físico

Es el servidor real donde se ejecuta la infraestructura.

Incluye:

- Procesadores.
- Memoria RAM.
- Discos.
- Tarjetas de red.
- Controladoras.

---

#### Hipervisor

Es la plataforma encargada de crear y administrar las máquinas virtuales.

Funciones:

- Crear máquinas virtuales.
- Asignar recursos.
- Gestionar dispositivos virtuales.
- Controlar el aislamiento.

---

#### Máquina virtual (VM)

Es un equipo virtual que funciona sobre el hipervisor.

Puede contener:

- Sistema operativo.
- Aplicaciones.
- Configuración propia.
- Discos virtuales.

---

#### Sistema operativo invitado

Es el sistema operativo que se ejecuta dentro de la máquina virtual.

Ejemplos:

- Windows Server.
- Ubuntu Server.
- Debian.
- Rocky Linux.

---

### Ventajas de la virtualización

La virtualización proporciona numerosos beneficios.

---

### Optimización de recursos

Un servidor físico tradicional puede utilizar solo una parte de su capacidad.

Ejemplo:

```text
Servidor físico

CPU utilizada: 20%

RAM utilizada: 30%
```

Mediante virtualización pueden ejecutarse varios sistemas aprovechando mejor los recursos disponibles.

---

### Reducción de costes

Permite reducir:

- Número de servidores físicos.
- Consumo eléctrico.
- Espacio en rack.
- Costes de mantenimiento.

Ejemplo:

Antes:

```text
Servidor 1 → Aplicación A

Servidor 2 → Aplicación B

Servidor 3 → Aplicación C
```

Después:

```text
Servidor físico

↓

Hipervisor

↓

VM A
VM B
VM C
```

---

### Aislamiento entre sistemas

Cada máquina virtual funciona de forma independiente.

Un problema en una VM no debería afectar al resto.

Ejemplo:

```text
VM Windows

↓

Error del sistema

↓

VM Linux continúa funcionando
```

Este aislamiento mejora la seguridad y estabilidad.

---

### Facilidad de despliegue

Crear nuevos servidores virtuales es mucho más rápido que instalar equipos físicos.

Proceso:

```text
Plantilla VM

↓

Clonado

↓

Configuración

↓

Servidor disponible
```

Esto permite desplegar infraestructuras rápidamente.

---

### Portabilidad

Una máquina virtual puede moverse entre diferentes servidores compatibles.

Ejemplo:

```text
Servidor físico A

↓

Exportar VM

↓

Servidor físico B
```

Esto facilita migraciones y mantenimiento.

---

### Mejora de la recuperación ante fallos

La virtualización facilita la recuperación mediante:

- Snapshots.
- Clonado.
- Replicación.
- Migración.
- Restauración rápida.

En caso de fallo del hardware, una máquina virtual puede recuperarse en otro host.

---

### Limitaciones de la virtualización

Aunque ofrece muchas ventajas, también presenta algunos inconvenientes.

---

### Consumo de recursos

Todas las máquinas virtuales comparten el hardware físico.

Si se asignan demasiadas máquinas puede producirse:

- Falta de memoria.
- Saturación de CPU.
- Problemas de rendimiento.

---

### Complejidad administrativa

Una infraestructura virtualizada requiere conocimientos sobre:

- Hipervisores.
- Redes virtuales.
- Almacenamiento.
- Seguridad.
- Monitorización.

---

### Dependencia del hardware físico

Aunque existan máquinas virtuales, siguen dependiendo del servidor físico.

Si el host falla y no existe alta disponibilidad, todas las máquinas alojadas pueden quedar fuera de servicio.

---

### Virtualización frente a servidores físicos

| Servidor físico | Virtualización |
|-----------------|----------------|
| Un sistema por hardware | Varias máquinas por hardware |
| Mayor consumo | Mejor aprovechamiento |
| Menor flexibilidad | Mayor flexibilidad |
| Migración compleja | Migración sencilla |
| Recuperación más lenta | Recuperación rápida |

---

[⬆️ Volver al índice](#índice)

## Tipos de virtualización

La virtualización puede aplicarse sobre diferentes recursos tecnológicos, no únicamente sobre servidores. Dependiendo del elemento que se abstraiga, existen distintos tipos de virtualización con objetivos y características diferentes.

Cada modalidad permite optimizar una parte concreta de la infraestructura, mejorar la flexibilidad y simplificar la administración de los recursos.

---

### Virtualización de servidores

La virtualización de servidores es el tipo más conocido y utilizado.

Consiste en dividir un servidor físico en múltiples máquinas virtuales independientes mediante un hipervisor.

Ejemplo:

```text
Servidor físico

↓

Hipervisor

↓

┌──────────────┐
│ VM Windows   │
└──────────────┘

┌──────────────┐
│ VM Linux     │
└──────────────┘

┌──────────────┐
│ VM BD        │
└──────────────┘
```

Cada máquina virtual dispone de:

- CPU virtual.
- Memoria asignada.
- Disco virtual.
- Tarjeta de red virtual.
- Sistema operativo propio.

---

### Ventajas de la virtualización de servidores

Permite:

- Consolidar servidores físicos.
- Reducir costes.
- Crear entornos de prueba.
- Migrar sistemas fácilmente.
- Mejorar la disponibilidad.
- Facilitar las copias de seguridad.

Es la base de muchas infraestructuras empresariales actuales.

---

### Virtualización de escritorios (VDI)

La virtualización de escritorios permite ejecutar escritorios de usuario desde servidores centrales.

En lugar de tener todo instalado en el equipo local, el usuario accede a un escritorio remoto.

Arquitectura:

```text
Usuario

↓

Cliente ligero / PC

↓

Servidor VDI

↓

Escritorio virtual
```

---

### Ventajas de VDI

Entre sus beneficios se encuentran:

- Administración centralizada.
- Mayor control de seguridad.
- Facilidad para aplicar políticas.
- Acceso remoto.
- Menor dependencia del hardware del usuario.

Es utilizada habitualmente en empresas con muchos usuarios.

---

### Virtualización de aplicaciones

Permite ejecutar aplicaciones sin instalarlas directamente en el sistema operativo del usuario.

La aplicación se ejecuta en un entorno aislado.

Ejemplo:

```text
Usuario

↓

Aplicación virtualizada

↓

Servidor de aplicaciones
```

Ventajas:

- Evita conflictos entre aplicaciones.
- Facilita actualizaciones.
- Simplifica despliegues.
- Mejora la compatibilidad.

---

### Virtualización de redes

La virtualización de redes permite crear redes lógicas independientes sobre una infraestructura física común.

Incluye tecnologías como:

- VLAN.
- VXLAN.
- SDN (Software Defined Networking).
- Switches virtuales.

Ejemplo:

```text
Red física

↓

Switch virtual

↓

┌───────────┐
│ VLAN 10   │
└───────────┘

┌───────────┐
│ VLAN 20   │
└───────────┘
```

---

### Ventajas de la virtualización de redes

Permite:

- Crear redes rápidamente.
- Separar tráfico.
- Mejorar seguridad.
- Automatizar configuraciones.
- Facilitar entornos cloud.

---

### Virtualización del almacenamiento

La virtualización del almacenamiento permite agrupar diferentes dispositivos físicos de almacenamiento y presentarlos como un único recurso lógico.

Ejemplo:

```text
Discos físicos

↓

Capa virtual

↓

Almacenamiento lógico
```

Puede aplicarse en:

- SAN.
- NAS.
- Cabinas de almacenamiento.
- Clústeres.

---

### Ventajas del almacenamiento virtualizado

Permite:

- Mejor aprovechamiento del espacio.
- Migración de datos.
- Administración centralizada.
- Creación de volúmenes dinámicos.
- Mayor disponibilidad.

---

### Virtualización de sistemas operativos

Consiste en ejecutar varios sistemas operativos independientes sobre un mismo hardware.

Ejemplo:

```text
Servidor físico

↓

Hipervisor

↓

Windows Server

Linux

BSD
```

Cada sistema funciona de forma aislada.

---

### Contenedores

Los contenedores son una forma de virtualización a nivel de sistema operativo.

A diferencia de una máquina virtual, no incluyen un sistema operativo completo.

Ejemplo:

```text
Sistema operativo Linux

↓

Motor de contenedores

↓

Contenedor 1
Contenedor 2
Contenedor 3
```

Ejemplos:

- Docker.
- Podman.
- Kubernetes.

---

### Diferencias entre máquinas virtuales y contenedores

| Máquina virtual | Contenedor |
|----------------|------------|
| Incluye sistema operativo completo | Comparte kernel |
| Mayor consumo de recursos | Menor consumo |
| Más aislamiento | Más rápido de desplegar |
| Arranque más lento | Arranque casi inmediato |

---

### Virtualización de hardware

Permite crear representaciones virtuales de componentes físicos.

Ejemplos:

- CPU virtual.
- Memoria virtual.
- Discos virtuales.
- Tarjetas de red virtuales.

El hipervisor se encarga de traducir estos recursos hacia el hardware real.

---

### Virtualización completa

La virtualización completa permite ejecutar un sistema operativo sin modificarlo.

El hipervisor proporciona todo el hardware virtual necesario.

Ejemplo:

```text
Windows Server

↓

Hardware virtual

↓

Hipervisor

↓

Servidor físico
```

Es la utilizada habitualmente por plataformas como VMware o Hyper-V.

---

### Paravirtualización

En la paravirtualización, el sistema operativo invitado conoce que está ejecutándose sobre un entorno virtual.

Esto permite una comunicación más eficiente con el hipervisor.

Ventajas:

- Mejor rendimiento.
- Menor sobrecarga.

Inconveniente:

- Requiere soporte del sistema operativo.

---

### Virtualización asistida por hardware

Los procesadores modernos incluyen tecnologías específicas para mejorar la virtualización.

Ejemplos:

**Intel**

- Intel VT-x.
- Intel VT-d.

**AMD**

- AMD-V.

Estas tecnologías permiten que el hipervisor gestione mejor los recursos del procesador.

---

### Comparativa de tipos de virtualización

| Tipo | Objetivo |
|------|----------|
| Servidores | Ejecutar múltiples sistemas |
| Escritorios | Centralizar escritorios de usuario |
| Aplicaciones | Ejecutar software aislado |
| Redes | Crear redes lógicas |
| Almacenamiento | Gestionar recursos de disco |
| Contenedores | Ejecutar aplicaciones ligeras |

---

[⬆️ Volver al índice](#índice)

## Hipervisores

El hipervisor es el componente principal de una infraestructura de virtualización. Se trata del software encargado de crear, ejecutar y administrar máquinas virtuales, proporcionando una capa intermedia entre el hardware físico y los sistemas operativos invitados.

Su función principal es repartir los recursos disponibles del servidor físico entre las diferentes máquinas virtuales, garantizando aislamiento, estabilidad y comunicación entre los componentes virtualizados.

---

### ¿Qué es un hipervisor?

Un hipervisor es una plataforma que permite ejecutar varios sistemas operativos independientes sobre un mismo equipo físico.

Actúa como intermediario entre:

```text
Hardware físico

↓

Hipervisor

↓

Máquinas virtuales

↓

Sistemas operativos invitados
```

El hipervisor administra:

- Procesador.
- Memoria RAM.
- Almacenamiento.
- Red.
- Dispositivos virtuales.

---

### Funciones principales de un hipervisor

Las funciones más importantes son:

- Crear y eliminar máquinas virtuales.
- Asignar recursos.
- Gestionar dispositivos virtuales.
- Controlar el aislamiento entre máquinas.
- Supervisar el rendimiento.
- Gestionar snapshots.
- Facilitar migraciones.
- Aplicar políticas de seguridad.

---

### Tipos de hipervisores

Existen dos grandes categorías:

- Hipervisores de tipo 1 (Bare Metal).
- Hipervisores de tipo 2 (Hosted).

La diferencia principal está en la forma en la que interactúan con el hardware.

---

## Hipervisores de tipo 1 (Bare Metal)

Los hipervisores de tipo 1 se ejecutan directamente sobre el hardware físico.

No necesitan un sistema operativo intermedio.

Arquitectura:

```text
Hardware físico

↓

Hipervisor

↓

Máquinas virtuales
```

Son los más utilizados en entornos empresariales y centros de datos.

---

### Ventajas de los hipervisores tipo 1

Sus principales ventajas son:

- Mayor rendimiento.
- Menor sobrecarga.
- Mayor estabilidad.
- Mejor escalabilidad.
- Más opciones de alta disponibilidad.

---

### Ejemplos de hipervisores tipo 1

Algunos ejemplos son:

- VMware ESXi.
- Microsoft Hyper-V Server.
- KVM.
- Xen.
- Proxmox VE.

---

### VMware ESXi

**VMware ESXi** es uno de los hipervisores empresariales más utilizados.

Características:

- Arquitectura Bare Metal.
- Gestión mediante vCenter.
- Alta disponibilidad.
- Migración en caliente.
- Gestión avanzada de recursos.

Es habitual encontrarlo en centros de datos corporativos.

---

### Microsoft Hyper-V

**Hyper-V** es la plataforma de virtualización de Microsoft.

Está integrada en:

- Windows Server.
- Algunas ediciones profesionales de Windows.

Características:

- Integración con Active Directory.
- Gestión mediante PowerShell.
- Live Migration.
- Clústeres de alta disponibilidad.

Ejemplo:

```powershell
Get-VM
```

Permite consultar máquinas virtuales desde PowerShell.

---

### KVM

**Kernel-based Virtual Machine (KVM)** es una solución de virtualización integrada en Linux.

Características:

- Utiliza el kernel Linux.
- Código abierto.
- Alto rendimiento.
- Compatible con múltiples sistemas operativos.

Es utilizado en muchas plataformas cloud.

---

### Proxmox VE

**Proxmox Virtual Environment** es una plataforma basada en Linux que integra:

- KVM para máquinas virtuales.
- LXC para contenedores.
- Gestión web.
- Clústeres.
- Almacenamiento distribuido.

Es una solución muy utilizada en pequeñas y medianas empresas.

---

## Hipervisores de tipo 2 (Hosted)

Los hipervisores de tipo 2 se ejecutan sobre un sistema operativo existente.

Arquitectura:

```text
Hardware físico

↓

Sistema operativo

↓

Hipervisor

↓

Máquinas virtuales
```

Son más habituales en equipos personales o laboratorios.

---

### Ventajas de los hipervisores tipo 2

Permiten:

- Instalación sencilla.
- Uso en equipos de escritorio.
- Creación rápida de laboratorios.
- Pruebas de sistemas.

---

### Inconvenientes de los hipervisores tipo 2

Sus limitaciones son:

- Menor rendimiento.
- Mayor consumo de recursos.
- Dependencia del sistema operativo anfitrión.
- Menor disponibilidad.

---

### Ejemplos de hipervisores tipo 2

Algunos ejemplos:

- VirtualBox.
- VMware Workstation.
- VMware Fusion.
- Parallels Desktop.

---

### VirtualBox

**VirtualBox** es un hipervisor gratuito desarrollado por Oracle.

Características:

- Código abierto.
- Compatible con Windows, Linux y macOS.
- Ideal para aprendizaje y pruebas.
- Permite crear snapshots.

Ejemplo:

```text
PC Windows

↓

VirtualBox

↓

VM Linux
```

---

### VMware Workstation

**VMware Workstation** está orientado a estaciones de trabajo profesionales.

Permite:

- Crear laboratorios.
- Probar sistemas operativos.
- Simular redes.
- Ejecutar múltiples máquinas virtuales.

Es muy utilizado por administradores y técnicos.

---

### Comparativa tipo 1 vs tipo 2

| Característica | Tipo 1 | Tipo 2 |
|----------------|--------|--------|
| Ejecución | Directo sobre hardware | Sobre sistema operativo |
| Rendimiento | Alto | Medio |
| Uso principal | Empresas y servidores | Laboratorios y usuarios |
| Complejidad | Mayor | Menor |
| Ejemplos | ESXi, Hyper-V, KVM | VirtualBox, Workstation |

---

### Arquitectura de un entorno virtualizado

Ejemplo empresarial:

```text
Servidor físico

↓

VMware ESXi

↓

┌─────────────────┐
│ VM Windows      │
│ Active Directory│
└─────────────────┘

┌─────────────────┐
│ VM Linux        │
│ Web Server      │
└─────────────────┘

┌─────────────────┐
│ VM Base Datos   │
│ SQL             │
└─────────────────┘
```

---

### Virtualización y CPU

Los hipervisores modernos utilizan características del procesador para mejorar el rendimiento.

Ejemplos:

Intel:

- VT-x.
- VT-d.

AMD:

- AMD-V.

Estas tecnologías permiten ejecutar instrucciones virtualizadas de forma más eficiente.

---

### Virtualización y memoria

El hipervisor gestiona la memoria asignada a cada máquina virtual.

Funciones habituales:

- Asignación dinámica.
- Reserva de memoria.
- Compartición de páginas.
- Control de consumo.

Un mal dimensionamiento puede provocar problemas de rendimiento.

---

### Virtualización y dispositivos

Los hipervisores crean dispositivos virtuales:

Ejemplos:

- Tarjetas de red virtuales.
- Controladoras de disco virtuales.
- Adaptadores gráficos virtuales.

Estos dispositivos permiten que el sistema operativo invitado funcione sin conocer el hardware real.

---

### Seguridad del hipervisor

El hipervisor es una pieza crítica de la infraestructura.

Buenas prácticas:

- Mantenerlo actualizado.
- Limitar accesos administrativos.
- Aplicar MFA.
- Separar redes de gestión.
- Monitorizar actividad.
- Realizar copias de configuración.

Un compromiso del hipervisor puede afectar a todas las máquinas virtuales.

---

[⬆️ Volver al índice](#índice)

## Máquinas virtuales

Las máquinas virtuales (**Virtual Machines o VM**) son sistemas informáticos independientes que se ejecutan dentro de un entorno virtualizado mediante un hipervisor.

Una máquina virtual emula un equipo físico completo, proporcionando sus propios recursos virtuales como procesador, memoria, almacenamiento y dispositivos de red.

Aunque comparte el hardware físico con otras máquinas virtuales, funciona de manera aislada como si fuera un servidor independiente.

---

### ¿Qué es una máquina virtual?

Una máquina virtual es una representación software de un equipo físico.

Dentro de una VM se pueden instalar:

- Sistema operativo.
- Aplicaciones.
- Servicios.
- Configuraciones propias.
- Usuarios.
- Políticas de seguridad.

Ejemplo:

```text
Servidor físico

↓

Hipervisor

↓

┌──────────────────┐
│ Máquina virtual  │
│ Windows Server   │
└──────────────────┘

┌──────────────────┐
│ Máquina virtual  │
│ Linux            │
└──────────────────┘
```

Cada máquina virtual tiene su propio entorno independiente.

---

### Componentes de una máquina virtual

Una máquina virtual está formada por diferentes elementos virtualizados.

Los principales son:

- CPU virtual.
- Memoria RAM virtual.
- Disco virtual.
- Tarjeta de red virtual.
- BIOS/UEFI virtual.
- Controladores virtuales.
- Sistema operativo invitado.

---

### CPU virtual (vCPU)

Las máquinas virtuales utilizan procesadores virtuales llamados **vCPU**.

El hipervisor asigna parte de la capacidad del procesador físico a cada VM.

Ejemplo:

```text
Servidor físico

16 núcleos CPU

↓

VM1 → 4 vCPU

VM2 → 8 vCPU

VM3 → 2 vCPU
```

La asignación debe realizarse correctamente para evitar problemas de rendimiento.

---

### Memoria virtual (vRAM)

La memoria RAM asignada a una máquina virtual se denomina memoria virtual.

Ejemplo:

```text
Servidor físico

64 GB RAM

↓

VM Windows → 16 GB

VM Linux → 8 GB

VM BD → 24 GB
```

Una mala distribución puede provocar:

- Falta de memoria.
- Intercambio excesivo.
- Lentitud de aplicaciones.

---

### Disco virtual

Las máquinas virtuales utilizan discos virtuales en lugar de discos físicos propios.

Los formatos más habituales son:

**VMware**

- VMDK.

**Hyper-V**

- VHD.
- VHDX.

**VirtualBox**

- VDI.

---

### Características de los discos virtuales

Los discos virtuales permiten:

- Ampliar capacidad.
- Crear snapshots.
- Clonar máquinas.
- Migrar sistemas.
- Realizar copias más fácilmente.

Ejemplo:

```text
Archivo VHDX

↓

Máquina virtual Windows
```

---

### Tarjeta de red virtual

Cada máquina virtual puede disponer de una o varias tarjetas de red virtuales.

Estas permiten:

- Comunicación con otras VMs.
- Acceso a Internet.
- Conexión con redes físicas.
- Separación mediante VLAN.

Ejemplo:

```text
VM Aplicación

↓

vNIC

↓

Switch virtual

↓

Red física
```

---

### Sistema operativo invitado

El sistema operativo instalado dentro de una máquina virtual se denomina **Guest OS**.

Ejemplos:

- Windows Server.
- Windows 11.
- Ubuntu Server.
- Debian.
- Rocky Linux.

El sistema operativo funciona igual que en un equipo físico.

---

### Máquina virtual frente a equipo físico

| Equipo físico | Máquina virtual |
|---------------|----------------|
| Hardware dedicado | Hardware compartido |
| Instalación física | Instalación virtual |
| Migración compleja | Migración sencilla |
| Recuperación más lenta | Recuperación rápida |
| Mayor coste | Mejor aprovechamiento |

---

### Creación de una máquina virtual

El proceso habitual es:

```text
Crear VM

↓

Asignar recursos

↓

Seleccionar ISO

↓

Instalar sistema operativo

↓

Configurar red

↓

Instalar herramientas
```

---

### Plantillas de máquinas virtuales

Las plantillas permiten crear nuevas máquinas rápidamente.

Ejemplo:

```text
VM base Windows Server

↓

Convertir en plantilla

↓

Crear nuevas máquinas
```

Ventajas:

- Despliegue rápido.
- Configuración uniforme.
- Menos errores.

---

### Clonado de máquinas virtuales

El clonado permite crear una copia de una máquina existente.

Tipos principales:

---

### Clonado completo

Genera una copia independiente de la máquina original.

Ventajas:

- Total independencia.
- Fácil administración.

Inconveniente:

- Mayor consumo de almacenamiento.

---

### Clonado enlazado

Comparte parte de los archivos con la máquina original.

Ventajas:

- Menor consumo.
- Creación rápida.

Inconvenientes:

- Dependencia de la máquina base.

---

### Snapshots

Un snapshot guarda el estado de una máquina virtual en un momento concreto.

Puede incluir:

- Disco.
- Memoria.
- Configuración.

Ejemplo:

```text
VM funcionando

↓

Crear snapshot

↓

Realizar cambios

↓

Problema

↓

Volver al snapshot
```

---

### Limitaciones de los snapshots

Aunque son útiles, no deben utilizarse como sustituto de una copia de seguridad.

Problemas:

- Consumen espacio.
- Pueden afectar al rendimiento.
- No protegen frente a pérdida del almacenamiento.
- No sustituyen un backup externo.

---

### Herramientas de integración

Los hipervisores proporcionan herramientas para mejorar la comunicación entre host y máquina virtual.

Ejemplos:

**VMware**

- VMware Tools.

**Hyper-V**

- Integration Services.

Permiten:

- Mejor control del tiempo.
- Mejor rendimiento.
- Apagado correcto.
- Mejor gestión de dispositivos.

---

### Estados de una máquina virtual

Una VM puede encontrarse en diferentes estados:

| Estado | Descripción |
|-|-|
| Encendida | Sistema operativo ejecutándose |
| Apagada | VM detenida |
| Suspendida | Estado guardado temporalmente |
| Pausada | Ejecución detenida |
| Migrando | Moviéndose entre hosts |

---

### Migración de máquinas virtuales

La virtualización permite mover máquinas entre servidores.

Ejemplo:

```text
Host A

↓

Migración

↓

Host B
```

Ventajas:

- Mantenimiento sin detener servicios.
- Equilibrio de carga.
- Recuperación ante fallos.

---

### Seguridad de las máquinas virtuales

Las máquinas virtuales deben protegerse igual que los equipos físicos.

Medidas recomendadas:

- Actualizar sistemas operativos.
- Aplicar parches.
- Proteger credenciales.
- Separar redes.
- Controlar permisos.
- Monitorizar actividad.

---

[⬆️ Volver al índice](#índice)

## Gestión de recursos virtuales

La gestión de recursos virtuales consiste en administrar y optimizar los recursos físicos de un servidor para distribuirlos correctamente entre las máquinas virtuales que se ejecutan sobre él.

Una correcta asignación de recursos permite obtener el máximo rendimiento de la infraestructura evitando problemas como falta de memoria, saturación del procesador o lentitud en las aplicaciones.

Los principales recursos gestionados por un hipervisor son:

- Procesador.
- Memoria RAM.
- Almacenamiento.
- Red.
- Dispositivos virtuales.

---

### Importancia de la gestión de recursos

En un entorno virtualizado varias máquinas comparten el mismo hardware físico.

Ejemplo:

```text
Servidor físico

CPU: 32 núcleos
RAM: 128 GB
Almacenamiento: 10 TB

↓

VM1 → Servidor web

VM2 → Base de datos

VM3 → Active Directory

VM4 → Aplicaciones internas
```

Si una máquina consume demasiados recursos puede afectar al resto.

Por ello es necesario controlar y equilibrar la infraestructura.

---

## Gestión de CPU

La CPU física del servidor se divide en procesadores virtuales (**vCPU**) asignados a las máquinas virtuales.

El hipervisor controla cómo se utilizan estos recursos.

---

### Asignación de vCPU

Cada máquina virtual recibe un número determinado de procesadores virtuales.

Ejemplo:

```text
Servidor físico

16 núcleos

↓

VM Web
2 vCPU

VM Base de datos
8 vCPU

VM Aplicación
4 vCPU
```

Una asignación incorrecta puede provocar:

- Falta de capacidad.
- Esperas de CPU.
- Bajo rendimiento.

---

### Sobreasignación de CPU

La sobreasignación permite asignar más vCPU que núcleos físicos disponibles.

Ejemplo:

```text
Servidor físico

8 núcleos

↓

VM1 → 4 vCPU

VM2 → 4 vCPU

VM3 → 4 vCPU

VM4 → 4 vCPU
```

Total:

```text
16 vCPU asignadas

8 núcleos físicos
```

Puede funcionar correctamente si las máquinas no utilizan todos los recursos simultáneamente.

---

### Riesgos de la sobreasignación

Una sobreasignación excesiva puede provocar:

- Latencia.
- Aplicaciones lentas.
- Esperas de procesador.
- Reducción del rendimiento general.

Debe utilizarse con planificación.

---

### Reserva, límite y prioridad de CPU

Los hipervisores permiten controlar el acceso a CPU mediante:

**Reserva**

Garantiza una cantidad mínima de CPU.

**Límite**

Impide que una VM supere un consumo determinado.

**Prioridad**

Define qué máquinas tienen preferencia cuando existe falta de recursos.

Ejemplo:

```text
Servidor SQL

↓

Alta prioridad

Servidor pruebas

↓

Baja prioridad
```

---

# Gestión de memoria RAM

La memoria es uno de los recursos más críticos en virtualización.

Cada máquina virtual necesita memoria suficiente para ejecutar su sistema operativo y aplicaciones.

---

### Asignación de memoria

Ejemplo:

```text
Servidor físico

64 GB RAM

↓

VM Windows Server
16 GB

VM Linux
8 GB

VM SQL
24 GB
```

La asignación debe ajustarse a las necesidades reales.

---

### Sobreasignación de memoria

Algunos hipervisores permiten asignar más memoria virtual que memoria física disponible.

Ejemplo:

```text
RAM física

64 GB

↓

VM1 → 32 GB

VM2 → 32 GB

VM3 → 16 GB
```

Total asignado:

```text
80 GB virtuales
```

---

### Técnicas de optimización de memoria

Los hipervisores utilizan diferentes técnicas:

---

### Memory Ballooning

Permite recuperar memoria no utilizada de una máquina virtual para entregarla a otra.

Ejemplo:

```text
VM con memoria libre

↓

Hipervisor

↓

VM con mayor necesidad
```

---

### Memory Sharing

Permite compartir páginas de memoria idénticas entre máquinas virtuales.

Ejemplo:

Varias VMs Windows pueden compartir componentes comunes.

---

### Swapping

Cuando no existe suficiente memoria física, parte de la información se mueve temporalmente al disco.

Esto puede reducir mucho el rendimiento.

---

### Gestión del almacenamiento

El almacenamiento virtualizado es fundamental para el rendimiento de las máquinas virtuales.

Debe gestionarse:

- Capacidad.
- Rendimiento.
- Disponibilidad.
- Copias de seguridad.

---

### Discos virtuales

Las máquinas utilizan archivos de disco virtual.

Ejemplos:

| Plataforma | Formato |
|-|-|
| VMware | VMDK |
| Hyper-V | VHD/VHDX |
| VirtualBox | VDI |

---

### Aprovisionamiento de discos

Existen diferentes formas de asignar almacenamiento.

---

### Thick Provisioning

Reserva todo el espacio desde el principio.

Ejemplo:

```text
Disco virtual

500 GB asignados

↓

500 GB ocupados físicamente
```

Ventajas:

- Mejor previsibilidad.
- Buen rendimiento.

Inconveniente:

- Mayor consumo inicial.

---

### Thin Provisioning

Asigna espacio según la necesidad real.

Ejemplo:

```text
Disco virtual

500 GB disponibles

↓

Uso actual

120 GB
```

Ventajas:

- Ahorro de espacio.

Riesgo:

- Puede agotarse el almacenamiento físico.

---

### Gestión de red

Los recursos de red también deben administrarse correctamente.

Incluyen:

- Tarjetas virtuales.
- Switches virtuales.
- Ancho de banda.
- VLAN.
- Segmentación.

---

### Control del ancho de banda

Algunas plataformas permiten limitar el tráfico.

Ejemplo:

```text
VM Producción

↓

1000 Mbps

VM Pruebas

↓

100 Mbps
```

Esto evita que una máquina consuma toda la capacidad disponible.

---

### Balanceo de carga

En entornos grandes se distribuyen máquinas virtuales entre diferentes hosts.

Ejemplo:

```text
Host A

VM1
VM2

↓

Carga elevada

↓

Migración

↓

Host B
```

Esto mejora el rendimiento y disponibilidad.

---

### Monitorización de recursos

Es necesario supervisar continuamente la infraestructura.

Elementos a controlar:

- Uso de CPU.
- Memoria.
- Disco.
- Red.
- Temperatura.
- Estado del host.

---

### Herramientas de monitorización

Ejemplos:

**VMware**

- vCenter.
- vRealize Operations.

**Microsoft**

- Windows Admin Center.
- System Center.

**Linux**

- Zabbix.
- Nagios.
- Prometheus.

---

### Identificación de máquinas problemáticas

Una VM puede afectar al resto del entorno.

Ejemplos:

```text
VM Base de datos

CPU 100%

↓

Ralentiza otras máquinas
```

Debe analizarse:

- Aplicaciones.
- Procesos.
- Configuración.
- Recursos asignados.

---

### Optimización de recursos

Buenas estrategias:

- Eliminar máquinas no utilizadas.
- Ajustar memoria asignada.
- Revisar discos antiguos.
- Actualizar herramientas de integración.
- Distribuir cargas entre hosts.

---

[⬆️ Volver al índice](#índice)

## Redes virtuales

La virtualización de redes permite crear infraestructuras de red lógicas independientes sobre una misma infraestructura física.

En un entorno virtualizado, las máquinas virtuales no se conectan directamente a tarjetas de red físicas, sino que utilizan componentes virtuales gestionados por el hipervisor.

Esto permite crear redes flexibles, segmentadas y fácilmente administrables sin necesidad de modificar constantemente el cableado físico.

---

### Funcionamiento de una red virtual

En una infraestructura tradicional:

```text
Servidor físico

↓

Tarjeta de red física

↓

Switch físico

↓

Red
```

En un entorno virtualizado:

```text
Máquina virtual

↓

Tarjeta de red virtual (vNIC)

↓

Switch virtual

↓

Tarjeta física

↓

Red física
```

El hipervisor actúa como intermediario entre las máquinas virtuales y la red física.

---

## Componentes de una red virtual

Una red virtual está formada por diferentes elementos:

- Tarjetas de red virtuales.
- Switches virtuales.
- Adaptadores físicos.
- VLAN.
- Redes virtuales aisladas.
- Firewalls virtuales.

---

### Tarjeta de red virtual (vNIC)

Cada máquina virtual dispone de una o varias tarjetas de red virtuales.

La vNIC funciona como una tarjeta física tradicional.

Puede tener:

- Dirección MAC propia.
- Dirección IP.
- Configuración VLAN.
- Control de velocidad.

Ejemplo:

```text
VM Windows Server

↓

vNIC

MAC:
00:50:56:AA:12:34

IP:
192.168.1.20
```

---

### Switch virtual (vSwitch)

El switch virtual es uno de los componentes principales de las redes virtualizadas.

Su función es conectar las máquinas virtuales entre sí y con la red física.

Ejemplo:

```text
VM1

↓

      vSwitch

↓

VM2

↓

Tarjeta física

↓

Red LAN
```

---

### Tipos de switches virtuales

Los principales tipos son:

- Switch interno.
- Switch externo.
- Switch privado.

---

### Switch externo

Permite comunicación entre:

- Máquinas virtuales.
- Equipo físico.
- Red corporativa.
- Internet.

Ejemplo:

```text
VM

↓

vSwitch externo

↓

NIC física

↓

Red empresarial
```

Es el tipo utilizado normalmente en producción.

---

### Switch interno

Permite comunicación entre:

- Máquinas virtuales.
- Sistema operativo anfitrión.

No tiene acceso directo a la red física.

Ejemplo:

```text
VM1

↓

vSwitch interno

↓

VM2

↓

Host físico
```

Útil para laboratorios.

---

### Switch privado

Permite comunicación únicamente entre máquinas virtuales.

No existe acceso al host ni a la red física.

Ejemplo:

```text
VM1

↓

vSwitch privado

↓

VM2
```

Se utiliza para entornos aislados.

---

# VLAN en entornos virtualizados

Las VLAN permiten separar redes lógicamente utilizando la misma infraestructura física.

Ejemplo:

```text
Servidor físico

↓

Switch virtual

↓

VLAN 10 → Servidores

VLAN 20 → Usuarios

VLAN 30 → Administración
```

---

### Ventajas de utilizar VLAN

Permiten:

- Separar tráfico.
- Mejorar seguridad.
- Organizar redes.
- Reducir dominios de broadcast.
- Aplicar políticas diferentes.

---

### VLAN tagging

El etiquetado VLAN permite identificar a qué red pertenece cada paquete.

El estándar más utilizado es:

```text
802.1Q
```

Ejemplo:

```text
Paquete

↓

Etiqueta VLAN 10

↓

Switch

↓

Destino correcto
```

---

# Redes aisladas

Una de las ventajas de la virtualización es poder crear redes completamente independientes.

Ejemplo:

```text
Red producción

↓

VM servidores reales


Red laboratorio

↓

VM pruebas
```

Esto permite probar configuraciones sin afectar a sistemas críticos.

---

# Redes definidas por software (SDN)

La tecnología **Software Defined Networking (SDN)** permite administrar redes mediante software en lugar de depender únicamente del hardware físico.

Arquitectura:

```text
Aplicaciones

↓

Controlador SDN

↓

Dispositivos de red

↓

Infraestructura física
```

---

### Ventajas de SDN

Permite:

- Automatización.
- Configuración centralizada.
- Mayor flexibilidad.
- Creación rápida de redes.
- Integración con cloud.

---

# Redes virtuales en VMware

VMware utiliza diferentes componentes para gestionar redes.

Principales elementos:

- vSwitch estándar.
- Distributed Switch.
- Port Groups.

---

### vSwitch estándar

Es un switch virtual configurado individualmente en cada host ESXi.

Características:

- Configuración local.
- Fácil de administrar.
- Adecuado para entornos pequeños.

---

### Distributed Switch

Permite administrar la red de varios hosts desde una ubicación central.

Ventajas:

- Configuración uniforme.
- Menor administración manual.
- Mejor control empresarial.

---

### Port Groups

Los grupos de puertos permiten asociar máquinas virtuales a determinadas redes.

Ejemplo:

```text
Port Group:

Producción

↓

VLAN 10
```

```text
Port Group:

Administración

↓

VLAN 20
```

---

# Redes virtuales en Hyper-V

Hyper-V utiliza switches virtuales para conectar máquinas virtuales.

Tipos:

- Externo.
- Interno.
- Privado.

Ejemplo:

```powershell
New-VMSwitch
```

Permite crear switches virtuales mediante PowerShell.

---

# Adaptadores de red virtuales

Los hipervisores permiten configurar diferentes características de las vNIC.

Ejemplos:

- Dirección MAC dinámica.
- Dirección MAC estática.
- Ancho de banda.
- VLAN.
- QoS.

---

# Balanceo y redundancia de red

En servidores críticos se utilizan varias tarjetas físicas para mejorar disponibilidad.

Ejemplo:

```text
NIC1

↓

Equipo físico


NIC2

↓

Equipo físico
```

Mediante tecnologías como:

- NIC Teaming.
- LACP.
- Bonding en Linux.

---

### NIC Teaming

Permite combinar varias tarjetas de red físicas.

Ventajas:

- Mayor disponibilidad.
- Más ancho de banda.
- Protección frente a fallos.

---

### Bonding en Linux

Linux permite agrupar interfaces mediante bonding.

Ejemplo:

```bash
cat /proc/net/bonding/bond0
```

Permite consultar el estado de una interfaz agrupada.

---

# Seguridad en redes virtuales

Las redes virtuales deben protegerse igual que las redes físicas.

Medidas recomendadas:

- Separar redes críticas.
- Utilizar VLAN.
- Controlar acceso administrativo.
- Aplicar firewalls virtuales.
- Monitorizar tráfico.
- Limitar comunicaciones innecesarias.

---

# Firewalls virtuales

Los firewalls pueden ejecutarse como máquinas virtuales.

Ejemplos:

- pfSense.
- OPNsense.
- Fortinet FortiGate VM.

Ventajas:

- Despliegue rápido.
- Gestión centralizada.
- Integración con entornos cloud.

---

# Monitorización de redes virtuales

Debe supervisarse:

- Uso de ancho de banda.
- Errores de conexión.
- Latencia.
- Paquetes perdidos.
- Estado de switches virtuales.

Herramientas:

- Zabbix.
- PRTG.
- Nagios.
- vCenter.

---

# Ejemplo práctico

Una empresa necesita separar sus servidores.

Configuración:

```text
Servidor físico

↓

Hipervisor

↓

vSwitch

↓

VLAN 10
VM Web

VLAN 20
VM Base de datos

VLAN 30
VM Administración
```

Gracias a la red virtual, los sistemas están separados aunque utilicen el mismo servidor físico.

---

[⬆️ Volver al índice](#índice)

## Almacenamiento en entornos virtualizados

El almacenamiento es uno de los componentes más importantes dentro de una infraestructura virtualizada, ya que todas las máquinas virtuales dependen de él para guardar sus sistemas operativos, aplicaciones y datos.

A diferencia de un servidor físico tradicional, donde cada equipo puede tener sus propios discos internos, en un entorno virtualizado el almacenamiento suele estar centralizado y gestionado por el hipervisor.

Una correcta planificación del almacenamiento permite mejorar el rendimiento, aumentar la disponibilidad y facilitar tareas como migraciones, copias de seguridad y recuperación ante fallos.

---

### Funcionamiento del almacenamiento virtualizado

En un entorno virtualizado, las máquinas virtuales utilizan discos virtuales que se almacenan sobre dispositivos físicos.

Arquitectura básica:

```text
Máquina virtual

↓

Disco virtual

↓

Almacenamiento del hipervisor

↓

Discos físicos

↓

Hardware de almacenamiento
```

La máquina virtual no accede directamente al disco físico, sino que utiliza una capa de abstracción gestionada por el hipervisor.

---

### Componentes del almacenamiento virtualizado

Los principales componentes son:

- Discos virtuales.
- Datastores.
- Cabinas de almacenamiento.
- Sistemas NAS.
- Sistemas SAN.
- Almacenamiento local.
- Almacenamiento distribuido.

---

## Discos virtuales

Un disco virtual es un archivo o volumen que representa un disco físico para una máquina virtual.

Contiene:

- Sistema operativo.
- Aplicaciones.
- Datos.
- Configuración.

Ejemplos de formatos:

| Plataforma | Formato |
|-|-|
| VMware | VMDK |
| Hyper-V | VHD/VHDX |
| VirtualBox | VDI |
| KVM | QCOW2 |

---

### Ventajas de los discos virtuales

Permiten:

- Ampliar capacidad fácilmente.
- Crear copias.
- Migrar máquinas.
- Realizar snapshots.
- Clonar sistemas.

Ejemplo:

```text
Archivo VMDK

↓

VM Windows Server

↓

Sistema operativo
```

---

## Datastore

Un datastore es una ubicación de almacenamiento utilizada por un hipervisor para guardar máquinas virtuales.

Puede estar basado en:

- Discos locales.
- NAS.
- SAN.
- Almacenamiento distribuido.

Ejemplo VMware:

```text
ESXi Host

↓

Datastore

↓

VM1.vmdk

VM2.vmdk

VM3.vmdk
```

---

### Tipos de almacenamiento

Existen diferentes formas de proporcionar almacenamiento a un entorno virtualizado.

Los principales son:

- Almacenamiento local.
- NAS.
- SAN.
- Almacenamiento distribuido.

---

# Almacenamiento local

El almacenamiento local utiliza discos instalados directamente en el servidor físico.

Ejemplo:

```text
Servidor físico

↓

RAID interno

↓

Máquinas virtuales
```

---

### Ventajas del almacenamiento local

- Bajo coste.
- Configuración sencilla.
- Buen rendimiento.

---

### Inconvenientes del almacenamiento local

- Menor disponibilidad.
- Difícil migración entre hosts.
- Dependencia del servidor físico.

Es adecuado para entornos pequeños.

---

# NAS (Network Attached Storage)

Un NAS es un sistema de almacenamiento conectado a la red que proporciona recursos mediante protocolos de archivos.

Protocolos habituales:

- SMB/CIFS.
- NFS.

Ejemplo:

```text
Servidor virtualización

↓

Red

↓

NAS

↓

Discos almacenamiento
```

---

### Ventajas del NAS

- Administración sencilla.
- Compartición de archivos.
- Menor coste.
- Fácil ampliación.

---

### Inconvenientes del NAS

- Dependencia de la red.
- Rendimiento limitado frente a SAN.
- Puede convertirse en punto crítico.

---

# SAN (Storage Area Network)

Una SAN proporciona almacenamiento mediante una red dedicada de alto rendimiento.

Normalmente utiliza:

- Fibre Channel.
- iSCSI.

Ejemplo:

```text
Servidor ESXi

↓

Red SAN

↓

Cabina almacenamiento

↓

Discos
```

---

### Ventajas de SAN

- Alto rendimiento.
- Alta disponibilidad.
- Escalabilidad.
- Ideal para centros de datos.

---

### Inconvenientes de SAN

- Mayor coste.
- Mayor complejidad.
- Requiere conocimientos especializados.

---

# RAID en almacenamiento virtualizado

El RAID permite combinar varios discos físicos para mejorar rendimiento o disponibilidad.

Tipos habituales:

| RAID | Característica |
|-|-|
| RAID 0 | Rendimiento |
| RAID 1 | Espejo |
| RAID 5 | Paridad |
| RAID 6 | Doble paridad |
| RAID 10 | Rendimiento + seguridad |

---

### Importancia del RAID

El RAID protege frente al fallo de discos individuales, pero no sustituye a una copia de seguridad.

Ejemplo:

```text
RAID 1

Disco A

↓

Copia idéntica

↓

Disco B
```

---

# Thin Provisioning

El almacenamiento Thin Provisioning permite asignar más espacio virtual del disponible inicialmente.

Ejemplo:

```text
VM

↓

Disco virtual 1 TB

↓

Uso real 200 GB
```

---

### Ventajas del Thin Provisioning

- Ahorro de espacio.
- Mejor aprovechamiento.
- Crecimiento dinámico.

---

### Riesgos del Thin Provisioning

Si todas las máquinas crecen demasiado:

```text
Almacenamiento físico lleno

↓

Máquinas virtuales afectadas
```

Debe monitorizarse continuamente.

---

# Thick Provisioning

El Thick Provisioning reserva todo el espacio desde el principio.

Ejemplo:

```text
VM

↓

Disco virtual 500 GB

↓

500 GB reservados físicamente
```

---

### Ventajas del Thick Provisioning

- Rendimiento más predecible.
- Menor riesgo de falta de espacio.

---

### Inconveniente

Consume más almacenamiento desde el inicio.

---

# IOPS y rendimiento del almacenamiento

En entornos virtualizados no solo importa la capacidad, sino también el rendimiento.

Factores importantes:

- IOPS.
- Latencia.
- Velocidad de transferencia.
- Tipo de disco.

---

### IOPS

Los IOPS indican cuántas operaciones de entrada/salida puede realizar un almacenamiento por segundo.

Ejemplo:

```text
SSD

↓

Mayor cantidad de IOPS

↓

Mejor rendimiento VM
```

---

### Latencia

La latencia es el tiempo que tarda una operación de almacenamiento en completarse.

Una latencia alta provoca:

- Aplicaciones lentas.
- Bases de datos con bajo rendimiento.
- Problemas de usuario.

---

# Almacenamiento distribuido

El almacenamiento distribuido combina varios nodos para crear un único sistema de almacenamiento.

Ejemplos:

- VMware vSAN.
- Ceph.
- Azure Storage.

Ventajas:

- Alta disponibilidad.
- Escalabilidad.
- Redundancia.

---

# Snapshots y almacenamiento

Los snapshots utilizan espacio adicional en el almacenamiento.

Ejemplo:

```text
VM original

↓

Snapshot

↓

Cambios almacenados aparte
```

Un exceso de snapshots puede provocar:

- Consumo elevado.
- Reducción de rendimiento.
- Problemas de consolidación.

---

# Migración de almacenamiento

La virtualización permite mover discos virtuales entre sistemas de almacenamiento.

Ejemplo:

```text
Datastore antiguo

↓

Migración

↓

Datastore nuevo
```

Ventajas:

- Mantenimiento sin apagar máquinas.
- Mejor distribución de recursos.
- Actualización de almacenamiento.

---

# Seguridad del almacenamiento virtualizado

Medidas recomendadas:

- Controlar permisos.
- Cifrar datos sensibles.
- Separar redes de almacenamiento.
- Monitorizar accesos.
- Proteger snapshots.
- Realizar copias externas.

---

# Monitorización del almacenamiento

Debe revisarse:

- Espacio disponible.
- Rendimiento.
- Latencia.
- Estado de discos.
- Errores.
- Crecimiento de máquinas virtuales.

Herramientas:

- vCenter.
- Zabbix.
- PRTG.
- Windows Admin Center.

---

# Ejemplo práctico

Una empresa tiene tres servidores virtuales:

```text
Servidor físico

↓

Hipervisor

↓

Datastore SAN

↓

VM Windows Server

VM Linux

VM Base de datos
```

El almacenamiento centralizado permite realizar migraciones, copias y recuperación de forma más sencilla.

---

[⬆️ Volver al índice](#índice)

## Alta disponibilidad y migración

La alta disponibilidad y la migración son dos de las principales ventajas que ofrecen los entornos virtualizados frente a las infraestructuras tradicionales.

Estas tecnologías permiten mantener los servicios funcionando, reducir tiempos de parada, realizar tareas de mantenimiento sin interrupciones y recuperar sistemas rápidamente ante fallos de hardware.

En entornos empresariales donde la disponibilidad de los servicios es crítica, estas funcionalidades son fundamentales.

---

### Concepto de alta disponibilidad (HA)

La alta disponibilidad (**High Availability o HA**) consiste en diseñar una infraestructura capaz de mantener los servicios operativos incluso cuando se produce un fallo.

El objetivo es reducir al mínimo el tiempo de interrupción.

Ejemplo:

```text
Servidor principal

↓

Fallo hardware

↓

Servidor secundario

↓

Servicio continúa funcionando
```

---

### Objetivos de la alta disponibilidad

Los principales objetivos son:

- Reducir tiempos de caída.
- Mantener servicios críticos disponibles.
- Evitar puntos únicos de fallo.
- Automatizar recuperaciones.
- Mejorar la continuidad del negocio.

---

### Clúster de virtualización

La alta disponibilidad normalmente se consigue mediante clústeres.

Un clúster agrupa varios servidores físicos para trabajar como una única infraestructura.

Ejemplo:

```text
        Clúster

 ┌──────────────┐
 │ Host 1       │
 └──────────────┘

 ┌──────────────┐
 │ Host 2       │
 └──────────────┘

 ┌──────────────┐
 │ Host 3       │
 └──────────────┘
```

Las máquinas virtuales pueden distribuirse entre diferentes hosts.

---

### Funcionamiento de un clúster HA

Proceso:

```text
VM ejecutándose

↓

Fallo del host

↓

Detección automática

↓

Reinicio VM en otro host

↓

Servicio recuperado
```

El usuario puede experimentar una interrupción mínima.

---

### Requisitos para alta disponibilidad

Para implementar HA suelen ser necesarios:

- Varios hosts físicos.
- Almacenamiento compartido.
- Red redundante.
- Monitorización.
- Gestión centralizada.
- Configuración adecuada del clúster.

---

### Puntos únicos de fallo

Un punto único de fallo (**Single Point of Failure**) es un componente cuya caída provoca la interrupción completa del servicio.

Ejemplos:

- Un único servidor.
- Una única fuente de alimentación.
- Un único almacenamiento.
- Una única conexión de red.

La alta disponibilidad busca eliminar estos riesgos.

---

### Redundancia de hardware

Los entornos críticos utilizan componentes redundantes.

Ejemplos:

- Fuentes de alimentación dobles.
- Varias tarjetas de red.
- Controladoras RAID.
- Almacenamiento replicado.
- Varios hosts.

Ejemplo:

```text
Fuente alimentación A

+

Fuente alimentación B

↓

Servidor continúa funcionando
```

---

# Migración de máquinas virtuales

La migración permite mover una máquina virtual de un host a otro.

Puede utilizarse para:

- Mantenimiento.
- Equilibrio de carga.
- Recuperación.
- Actualización de hardware.

---

### Migración en frío (Cold Migration)

La máquina virtual debe estar apagada para realizar el movimiento.

Proceso:

```text
Apagar VM

↓

Mover archivos

↓

Encender VM
```

Ventaja:

- Más sencilla.

Inconveniente:

- Existe interrupción del servicio.

---

### Migración en caliente (Live Migration)

Permite mover una máquina virtual mientras está funcionando.

Proceso:

```text
VM funcionando

↓

Copiar memoria

↓

Transferir estado

↓

Cambiar host

↓

Servicio continúa
```

El tiempo de interrupción suele ser muy reducido.

---

### VMware vMotion

**vMotion** es la tecnología de VMware para migrar máquinas virtuales en ejecución entre hosts.

Permite:

- Mover VMs sin apagarlas.
- Realizar mantenimiento.
- Equilibrar cargas.

Ejemplo:

```text
ESXi Host A

↓

vMotion

↓

ESXi Host B
```

---

### Hyper-V Live Migration

Hyper-V dispone de una tecnología equivalente llamada **Live Migration**.

Permite mover máquinas virtuales entre servidores Hyper-V.

Ventajas:

- Mantenimiento sin interrupción.
- Mejor distribución de recursos.
- Mayor disponibilidad.

---

### Migración de almacenamiento

Además de mover máquinas entre hosts, también puede migrarse su almacenamiento.

Proceso:

```text
Datastore antiguo

↓

Migración almacenamiento

↓

Nuevo datastore
```

Permite actualizar sistemas de almacenamiento sin detener servicios.

---

### Migración planificada

Se realiza cuando existe tiempo para preparar el cambio.

Ejemplos:

- Renovación de servidores.
- Cambio de almacenamiento.
- Mantenimiento programado.

Proceso:

```text
Planificación

↓

Pruebas

↓

Migración

↓

Validación
```

---

### Migración ante fallos

Se realiza cuando existe una incidencia.

Ejemplo:

```text
Host con fallo

↓

Mover VMs

↓

Nuevo host operativo
```

Es una parte importante de la recuperación ante desastres.

---

# Balanceo de carga

El balanceo de carga distribuye máquinas virtuales entre diferentes hosts para evitar saturaciones.

Ejemplo:

Antes:

```text
Host 1

VM1
VM2
VM3
VM4
```

Después:

```text
Host 1

VM1
VM2

Host 2

VM3
VM4
```

---

### DRS (Distributed Resource Scheduler)

VMware DRS permite distribuir automáticamente máquinas virtuales según el consumo de recursos.

Analiza:

- CPU.
- Memoria.
- Carga de hosts.

Puede mover máquinas automáticamente.

---

### Live Migration automática

Algunas plataformas permiten migraciones automáticas cuando detectan problemas.

Ejemplo:

```text
Host saturado

↓

Sistema detecta carga

↓

Migración VM

↓

Rendimiento mejorado
```

---

# Replicación de máquinas virtuales

La replicación mantiene copias de máquinas virtuales en otro sistema.

Ejemplo:

```text
Servidor producción

↓

Replicación

↓

Servidor secundario
```

Se utiliza para recuperación ante desastres.

---

### VMware Replication

Permite replicar máquinas virtuales hacia otro entorno.

Características:

- Copias periódicas.
- Recuperación rápida.
- Integración con planes DR.

---

### Hyper-V Replica

Hyper-V permite replicar máquinas virtuales entre servidores.

Ventajas:

- Protección frente a fallos.
- Recuperación sencilla.
- Integración con Windows Server.

---

# Fault Tolerance (FT)

La tolerancia a fallos permite mantener una copia activa de una máquina virtual.

Ejemplo:

```text
VM primaria

↓

Sincronización continua

↓

VM secundaria
```

Si la principal falla, la secundaria puede continuar.

---

### Diferencia entre HA y Fault Tolerance

| HA | Fault Tolerance |
|-|-|
| Reinicia VM en otro host | Mantiene copia activa |
| Puede existir parada breve | Sin interrupción |
| Menor coste | Mayor coste |

---

# Monitorización de disponibilidad

Para garantizar alta disponibilidad deben supervisarse:

- Estado de hosts.
- Estado de máquinas virtuales.
- Red.
- Almacenamiento.
- Recursos.

Herramientas:

- vCenter.
- System Center.
- Zabbix.
- PRTG.

---

# Ejemplo práctico

Una empresa tiene tres hosts VMware:

```text
Host 1

VM Active Directory


Host 2

VM SQL Server


Host 3

VM Aplicaciones
```

Si Host 2 falla:

```text
Detección fallo

↓

HA reinicia VM SQL

↓

Servicio recuperado
```

La infraestructura continúa operativa.

---

[⬆️ Volver al índice](#índice)

## Seguridad en virtualización

La seguridad en entornos virtualizados es un aspecto fundamental, ya que una única infraestructura física puede alojar múltiples sistemas, aplicaciones y servicios críticos.

Aunque las máquinas virtuales proporcionan aislamiento entre ellas, una configuración incorrecta puede provocar riesgos que afecten a todo el entorno.

La seguridad debe aplicarse en todas las capas:

- Hardware físico.
- Hipervisor.
- Máquinas virtuales.
- Redes virtuales.
- Almacenamiento.
- Usuarios y permisos.

---

### Importancia de la seguridad en virtualización

En un entorno tradicional, un fallo suele afectar a un único servidor.

En virtualización:

```text
Servidor físico

↓

Hipervisor

↓

VM1
VM2
VM3
VM4
```

Un compromiso del hipervisor podría afectar a todas las máquinas virtuales alojadas.

Por ello, la protección del entorno virtual debe considerarse prioritaria.

---

## Seguridad del hipervisor

El hipervisor es uno de los componentes más críticos de la infraestructura.

Si un atacante obtiene acceso administrativo al hipervisor podría:

- Apagar máquinas virtuales.
- Modificar configuraciones.
- Acceder a discos virtuales.
- Crear nuevas máquinas.
- Extraer información.

---

### Actualización del hipervisor

Es importante mantener actualizado el software de virtualización.

Buenas prácticas:

- Aplicar parches de seguridad.
- Revisar vulnerabilidades conocidas.
- Mantener versiones soportadas.
- Planificar actualizaciones.

Ejemplos:

- VMware ESXi.
- Microsoft Hyper-V.
- Proxmox VE.

---

### Protección de accesos administrativos

Los accesos al hipervisor deben estar altamente protegidos.

Medidas recomendadas:

- Utilizar contraseñas robustas.
- Activar MFA.
- Limitar usuarios administrativos.
- Separar cuentas personales y administrativas.
- Registrar accesos.

Ejemplo:

```text
Usuario técnico

↓

Cuenta normal

↓

Cuenta administrador independiente
```

---

### Segmentación de la red de administración

La red de gestión del hipervisor debe estar separada del tráfico normal.

Ejemplo:

```text
VLAN Usuarios

↓

Usuarios finales


VLAN Administración

↓

Hipervisores
```

Esto reduce la superficie de ataque.

---

# Seguridad de las máquinas virtuales

Las máquinas virtuales deben protegerse igual que los equipos físicos.

Deben aplicarse:

- Actualizaciones.
- Antivirus.
- Firewall.
- Control de usuarios.
- Políticas de seguridad.

---

### Actualización de sistemas invitados

Cada máquina virtual debe mantenerse actualizada.

Ejemplo:

```text
VM Windows Server

↓

Windows Update

↓

Parches seguridad
```

Un sistema operativo vulnerable puede comprometer el entorno.

---

### Antivirus y protección endpoint

Las máquinas virtuales deben contar con medidas de protección.

Ejemplos:

- Microsoft Defender.
- EDR.
- Antivirus empresarial.

Debe evitarse pensar que la virtualización elimina la necesidad de seguridad.

---

### Configuración segura de máquinas virtuales

Buenas prácticas:

- Desactivar dispositivos innecesarios.
- Reducir servicios activos.
- Aplicar políticas de contraseña.
- Eliminar máquinas no utilizadas.
- Revisar permisos.

---

# Aislamiento entre máquinas virtuales

Uno de los objetivos de la virtualización es mantener separadas las máquinas.

Ejemplo:

```text
VM Producción

↓

Aislada

↓

VM Laboratorio
```

Sin embargo, existen riesgos si la configuración es incorrecta.

---

### Escape de máquina virtual (VM Escape)

Un **VM Escape** ocurre cuando un atacante consigue salir de una máquina virtual y acceder al hipervisor o al sistema físico.

Ejemplo:

```text
Máquina virtual comprometida

↓

Vulnerabilidad hipervisor

↓

Host físico
```

Es un ataque poco frecuente, pero de alto impacto.

---

### Medidas contra VM Escape

Para reducir riesgos:

- Mantener hipervisor actualizado.
- Aplicar parches.
- Reducir privilegios.
- Evitar configuraciones inseguras.
- Monitorizar actividad sospechosa.

---

# Seguridad de redes virtuales

Las redes virtuales deben protegerse mediante segmentación y controles adecuados.

Medidas:

- VLAN.
- Firewalls virtuales.
- ACL.
- Separación de redes.
- Monitorización.

---

### Separación de redes

Es recomendable separar:

- Red de administración.
- Red de almacenamiento.
- Red de usuarios.
- Red de máquinas virtuales.
- Red de backup.

Ejemplo:

```text
VLAN 10

Gestión


VLAN 20

Producción


VLAN 30

Backup
```

---

### Firewalls virtuales

Los firewalls pueden ejecutarse como máquinas virtuales.

Ejemplos:

- pfSense.
- OPNsense.
- Fortigate VM.

Permiten:

- Filtrar tráfico.
- Crear reglas.
- Controlar accesos.

---

# Seguridad del almacenamiento virtual

El almacenamiento contiene información crítica de las máquinas virtuales.

Debe protegerse mediante:

- Control de permisos.
- Cifrado.
- Copias de seguridad.
- Monitorización.

---

### Protección de discos virtuales

Los archivos de máquinas virtuales pueden contener:

- Sistemas operativos.
- Datos empresariales.
- Credenciales.
- Configuraciones.

Ejemplo:

```text
Servidor.vmdk

↓

Datos completos de la VM
```

Por ello deben protegerse adecuadamente.

---

### Cifrado de máquinas virtuales

Algunas plataformas permiten cifrar máquinas virtuales.

Ventajas:

- Protección frente a robo de discos.
- Mayor confidencialidad.
- Cumplimiento normativo.

Ejemplos:

- VMware VM Encryption.
- BitLocker en máquinas Windows.

---

# Seguridad de snapshots

Los snapshots pueden contener información sensible.

Riesgos:

- Acceso no autorizado.
- Consumo excesivo.
- Exposición de datos antiguos.

Buenas prácticas:

- Limitar su uso.
- Proteger permisos.
- Eliminarlos cuando ya no sean necesarios.

---

# Seguridad en copias de máquinas virtuales

Las copias de seguridad de VMs deben protegerse.

Medidas:

- Cifrado.
- Control de acceso.
- Copias offline.
- Almacenamiento externo.
- Pruebas de restauración.

---

# Control de permisos

Debe aplicarse el principio de mínimo privilegio.

Ejemplo:

```text
Administrador virtualización

↓

Puede modificar VMs


Operador backup

↓

Solo gestiona copias
```

No todos los usuarios necesitan acceso completo.

---

# Auditoría y registro de actividad

Es importante registrar acciones realizadas sobre la infraestructura virtual.

Debe controlarse:

- Inicio de sesión.
- Cambios de configuración.
- Creación de máquinas.
- Eliminaciones.
- Migraciones.

Ejemplos:

- Logs VMware.
- Eventos Windows.
- Syslog Linux.

---

# Monitorización de seguridad

Debe supervisarse:

- Cambios inesperados.
- Consumo anormal.
- Nuevas máquinas creadas.
- Accesos administrativos.
- Tráfico sospechoso.

Herramientas:

- SIEM.
- Zabbix.
- Splunk.
- Wazuh.

---

# Hardening del entorno virtual

El hardening consiste en aplicar medidas para reducir riesgos.

Ejemplos:

- Desactivar servicios innecesarios.
- Limitar accesos.
- Configurar políticas seguras.
- Eliminar configuraciones por defecto.
- Revisar permisos.

---

# Ejemplo práctico

Una empresa tiene un entorno VMware:

```text
Servidor físico

↓

ESXi

↓

VM Windows

VM Linux

VM Base datos
```

Medidas aplicadas:

- VLAN de administración separada.
- MFA para administradores.
- Backups cifrados.
- Actualización del hipervisor.
- Monitorización de eventos.

Resultado:

Mayor protección frente a accesos no autorizados.

---

[⬆️ Volver al índice](#índice)

## Copias de seguridad y recuperación en entornos virtuales

Las copias de seguridad en entornos virtualizados son un elemento fundamental para garantizar la continuidad de los servicios y proteger las máquinas virtuales frente a fallos, errores humanos, ataques o pérdidas de información.

Aunque la virtualización facilita la recuperación mediante snapshots, migraciones y clonados, estos mecanismos no sustituyen a una estrategia completa de copias de seguridad.

Un entorno virtualizado correctamente protegido debe combinar copias periódicas, almacenamiento seguro y procedimientos de restauración probados.

---

### Importancia de las copias de seguridad en virtualización

En una infraestructura virtualizada, una única máquina física puede contener múltiples sistemas críticos.

Ejemplo:

```text
Servidor físico

↓

Hipervisor

↓

VM Active Directory

VM Base de datos

VM Aplicación empresarial
```

Un fallo del almacenamiento o del hipervisor podría afectar a todas las máquinas virtuales.

Por ello, las copias son esenciales para:

- Recuperar servicios.
- Evitar pérdida de datos.
- Reducir tiempos de parada.
- Cumplir requisitos de continuidad.
- Proteger frente a ransomware.

---

## Tipos de copias de seguridad de máquinas virtuales

Existen diferentes estrategias para realizar backups en entornos virtualizados.

Las más utilizadas son:

- Copia completa.
- Copia incremental.
- Copia diferencial.
- Copia basada en snapshots.
- Replicación.

---

### Copia completa

Realiza una copia completa de todos los datos de una máquina virtual.

Incluye:

- Disco virtual.
- Configuración.
- Sistema operativo.
- Aplicaciones.

Ejemplo:

```text
VM completa

↓

Backup completo
```

Ventajas:

- Restauración sencilla.
- Recuperación rápida.

Inconvenientes:

- Mayor consumo de espacio.
- Mayor tiempo de ejecución.

---

### Copia incremental

Guarda únicamente los cambios realizados desde la última copia.

Ejemplo:

```text
Lunes

Backup completo


Martes

Cambios nuevos


Miércoles

Cambios nuevos
```

Ventajas:

- Menor espacio.
- Mayor velocidad.

Inconvenientes:

- Restauración más compleja.

---

### Copia diferencial

Guarda los cambios realizados desde la última copia completa.

Ejemplo:

```text
Lunes

Backup completo


Martes

Cambios desde lunes


Miércoles

Cambios desde lunes
```

Ventajas:

- Restauración más sencilla que incremental.

Inconveniente:

- Crece con el tiempo.

---

# Snapshots frente a backups

Los snapshots son una característica habitual de las plataformas virtualizadas.

Permiten guardar el estado de una máquina virtual en un momento concreto.

Ejemplo:

```text
VM funcionando

↓

Crear snapshot

↓

Actualizar aplicación

↓

Problema

↓

Volver al snapshot
```

---

### Diferencias entre snapshot y backup

| Snapshot | Backup |
|-|-|
| Estado temporal | Copia independiente |
| Usa el mismo almacenamiento | Puede estar externo |
| Recuperación rápida | Protección ante desastre |
| No protege frente fallo almacenamiento | Protege frente pérdida total |

---

### Riesgos de utilizar snapshots como backup

Los snapshots no deben utilizarse como sistema principal de protección.

Problemas:

- Consumen almacenamiento.
- Pueden degradar rendimiento.
- Dependencia del almacenamiento original.
- Pueden crecer demasiado.
- No protegen frente ransomware.

---

# Herramientas de backup para virtualización

Existen soluciones específicas para entornos virtualizados.

Ejemplos:

- Veeam Backup & Replication.
- Nakivo.
- Acronis Cyber Protect.
- Commvault.
- Veritas Backup Exec.

---

### Veeam Backup & Replication

Es una de las soluciones más utilizadas en entornos VMware y Hyper-V.

Permite:

- Backup de máquinas virtuales.
- Restauración completa.
- Restauración de archivos.
- Replicación.
- Copias inmutables.

---

### Integración con hipervisores

Las herramientas de backup pueden integrarse con:

- VMware vSphere.
- Microsoft Hyper-V.
- Proxmox.
- KVM.

Esto permite realizar copias sin necesidad de instalar agentes dentro de cada máquina virtual.

---

# Restauración de máquinas virtuales

La restauración permite recuperar una máquina virtual después de una pérdida o fallo.

Tipos habituales:

---

### Restauración completa de VM

Recupera la máquina virtual completa.

Incluye:

- Configuración.
- Discos virtuales.
- Sistema operativo.
- Aplicaciones.

Ejemplo:

```text
Backup VM

↓

Restauración

↓

VM funcionando
```

---

### Restauración de archivos individuales

Permite recuperar únicamente archivos concretos.

Ejemplo:

```text
Usuario elimina documento

↓

Backup VM

↓

Recuperar archivo
```

Evita restaurar toda la máquina.

---

### Restauración instantánea

Algunas soluciones permiten arrancar una máquina directamente desde el backup.

Proceso:

```text
Backup

↓

Arranque temporal

↓

Servicio disponible

↓

Restauración definitiva
```

Reduce mucho los tiempos de recuperación.

---

# Recuperación ante fallos del host

Si un servidor físico falla, las máquinas virtuales deben poder recuperarse.

Opciones:

- Alta disponibilidad.
- Migración.
- Restauración desde backup.
- Replicación.

Ejemplo:

```text
Host físico falla

↓

Nuevo host disponible

↓

Restaurar VM

↓

Servicio operativo
```

---

# Estrategia 3-2-1 de copias

Una estrategia recomendada es la regla 3-2-1.

Consiste en:

```text
3 copias de los datos

↓

2 medios diferentes

↓

1 copia fuera de la ubicación principal
```

Ejemplo:

```text
Servidor producción

↓

Backup local

↓

NAS

↓

Copia externa
```

---

# Copias inmutables

Las copias inmutables no pueden modificarse ni eliminarse durante un periodo determinado.

Son especialmente importantes frente a ransomware.

Ejemplo:

```text
Backup creado

↓

Bloqueado

↓

No puede ser modificado
```

---

### Ventajas de los backups inmutables

Protegen frente a:

- Ransomware.
- Borrado accidental.
- Manipulación maliciosa.

---

# Replicación de máquinas virtuales

La replicación mantiene una copia de una máquina virtual en otro sistema.

Ejemplo:

```text
Producción

↓

Replicación

↓

Servidor secundario
```

Permite recuperaciones rápidas ante fallos graves.

---

# Plan de recuperación de máquinas virtuales

Un procedimiento de recuperación debe definir:

- Sistemas prioritarios.
- Orden de recuperación.
- Responsables.
- Ubicación de backups.
- Tiempos objetivo.

Ejemplo:

```text
1. Recuperar red

↓

2. Recuperar Active Directory

↓

3. Recuperar bases de datos

↓

4. Recuperar aplicaciones
```

---

# Validación después de una restauración

Después de recuperar una máquina virtual deben realizarse comprobaciones.

Revisar:

- Inicio del sistema operativo.
- Servicios activos.
- Conectividad.
- Aplicaciones.
- Datos.
- Permisos.

Una restauración no se considera correcta hasta que el servicio funciona.

---

# Seguridad de los backups virtuales

Las copias deben protegerse mediante:

- Cifrado.
- Control de acceso.
- MFA.
- Segmentación de red.
- Almacenamiento seguro.
- Monitorización.

---

# Ejemplo práctico

Una empresa sufre un fallo del almacenamiento donde están sus máquinas virtuales.

Situación:

```text
Almacenamiento principal

↓

Falló
```

Proceso de recuperación:

```text
Activar almacenamiento secundario

↓

Restaurar backups

↓

Arrancar máquinas virtuales

↓

Validar servicios
```

Resultado:

Los servicios vuelven a estar operativos.

---

[⬆️ Volver al índice](#índice)

## Monitorización y administración

La monitorización y administración de entornos virtualizados son procesos esenciales para garantizar el rendimiento, disponibilidad y seguridad de la infraestructura.

A diferencia de un entorno físico tradicional, donde cada servidor se gestiona de forma independiente, en virtualización es necesario supervisar múltiples capas:

- Hardware físico.
- Hipervisor.
- Máquinas virtuales.
- Redes virtuales.
- Almacenamiento.
- Servicios ejecutados.

Una correcta monitorización permite detectar problemas antes de que afecten a los usuarios y facilita la toma de decisiones sobre ampliaciones, optimización y mantenimiento.

---

### Importancia de la monitorización en virtualización

En una infraestructura virtualizada, un único problema puede afectar a múltiples sistemas.

Ejemplo:

```text
Servidor físico

↓

Hipervisor

↓

VM1
VM2
VM3
```

Si el host presenta problemas de CPU, memoria o almacenamiento, todas las máquinas virtuales pueden verse afectadas.

La monitorización permite:

- Detectar fallos.
- Analizar rendimiento.
- Prevenir saturaciones.
- Optimizar recursos.
- Mejorar disponibilidad.

---

# Elementos que deben monitorizarse

Los principales componentes a supervisar son:

- Hosts físicos.
- Hipervisores.
- Máquinas virtuales.
- CPU.
- Memoria RAM.
- Almacenamiento.
- Red.
- Servicios.
- Eventos y registros.

---

## Monitorización del host físico

El servidor físico es la base de toda la infraestructura virtual.

Debe controlarse:

- Estado del hardware.
- Temperatura.
- Ventiladores.
- Fuentes de alimentación.
- Discos.
- Controladoras RAID.

---

### Estado del hardware

Muchos servidores incluyen sistemas de gestión remota.

Ejemplos:

- Dell iDRAC.
- HPE iLO.
- Lenovo XClarity.

Permiten consultar:

- Estado de componentes.
- Alertas.
- Errores de hardware.

---

# Monitorización del hipervisor

El hipervisor debe supervisarse constantemente.

Elementos importantes:

- Estado del host.
- Uso de recursos.
- Máquinas virtuales activas.
- Errores.
- Configuración.

---

### VMware vCenter

vCenter es la plataforma de administración centralizada de VMware.

Permite:

- Gestionar hosts ESXi.
- Crear máquinas virtuales.
- Monitorizar recursos.
- Administrar clústeres.
- Gestionar migraciones.

---

### Microsoft Hyper-V Manager

Hyper-V Manager permite administrar entornos Hyper-V.

Funciones:

- Crear VMs.
- Configurar recursos.
- Encender y apagar máquinas.
- Revisar estado.

---

### Proxmox Web Interface

Proxmox proporciona una interfaz web para administrar:

- Máquinas virtuales.
- Contenedores.
- Clústeres.
- Almacenamiento.
- Redes.

---

# Monitorización de CPU

El consumo de CPU debe controlarse para evitar saturaciones.

Indicadores:

- Uso de procesador.
- Tiempo de espera.
- Número de vCPU.
- Carga del host.

Ejemplo:

```text
Host CPU

90%

↓

Riesgo de saturación
```

---

### Problemas habituales de CPU

Pueden producirse por:

- Exceso de máquinas virtuales.
- Aplicaciones mal configuradas.
- Asignación incorrecta de vCPU.

Soluciones:

- Optimizar recursos.
- Migrar máquinas.
- Aumentar capacidad.

---

# Monitorización de memoria RAM

La memoria es un recurso crítico.

Debe revisarse:

- RAM utilizada.
- Memoria disponible.
- Ballooning.
- Swapping.

Ejemplo:

```text
RAM física

64 GB

↓

Uso actual

60 GB
```

---

### Problemas habituales de memoria

Síntomas:

- Lentitud.
- Aplicaciones bloqueadas.
- Alto uso de disco.

Soluciones:

- Ajustar memoria asignada.
- Añadir RAM.
- Optimizar máquinas virtuales.

---

# Monitorización del almacenamiento

El almacenamiento afecta directamente al rendimiento de las máquinas virtuales.

Debe supervisarse:

- Espacio disponible.
- Latencia.
- IOPS.
- Errores.
- Crecimiento de discos virtuales.

---

### Problemas habituales de almacenamiento

Ejemplos:

```text
Datastore lleno

↓

Máquinas virtuales detenidas
```

o:

```text
Alta latencia

↓

Aplicaciones lentas
```

---

# Monitorización de red

La red virtual debe supervisarse igual que una red física.

Controlar:

- Ancho de banda.
- Latencia.
- Paquetes perdidos.
- Estado de switches virtuales.
- VLAN.

---

### Problemas habituales de red

Ejemplos:

- Configuración incorrecta de VLAN.
- Saturación de ancho de banda.
- Fallo de tarjeta física.
- Problemas de switch virtual.

---

# Herramientas de monitorización

Existen diferentes soluciones para supervisar infraestructuras virtualizadas.

---

### Zabbix

Plataforma de monitorización de código abierto.

Permite controlar:

- Servidores.
- Redes.
- Máquinas virtuales.
- Servicios.

---

### Nagios

Herramienta utilizada para supervisión de sistemas.

Permite:

- Crear alertas.
- Monitorizar disponibilidad.
- Revisar servicios.

---

### PRTG

Solución comercial de monitorización.

Incluye sensores para:

- VMware.
- Hyper-V.
- Redes.
- Sistemas.

---

### Grafana + Prometheus

Solución moderna basada en métricas.

Permite:

- Recoger datos.
- Crear dashboards.
- Analizar tendencias.

---

# Administración de máquinas virtuales

La administración incluye todas las tareas necesarias para mantener las VMs operativas.

Incluye:

- Creación.
- Configuración.
- Actualización.
- Eliminación.
- Migración.
- Backup.

---

# Automatización de administración

La automatización permite reducir tareas manuales.

Ejemplos:

- Crear máquinas.
- Configurar redes.
- Generar informes.
- Realizar comprobaciones.

---

### PowerShell y virtualización

Microsoft permite administrar Hyper-V mediante PowerShell.

Ejemplos:

Ver máquinas virtuales:

```powershell
Get-VM
```

Iniciar una VM:

```powershell
Start-VM NombreVM
```

Apagar una VM:

```powershell
Stop-VM NombreVM
```

---

### Automatización en VMware

VMware dispone de PowerCLI.

Ejemplo:

```powershell
Get-VM
```

Permite administrar entornos VMware mediante comandos.

---

# Gestión de inventario

Es importante mantener información actualizada de la infraestructura.

Debe registrarse:

- Nombre de VM.
- Sistema operativo.
- IP.
- Recursos asignados.
- Host donde se ejecuta.
- Responsable.

Ejemplo:

| VM | Sistema | CPU | RAM |
|-|-|-|-|
| WEB01 | Linux | 2 vCPU | 8 GB |
| SQL01 | Windows | 8 vCPU | 32 GB |

---

# Gestión de capacidad

La administración debe prever el crecimiento futuro.

Debe analizarse:

- Recursos disponibles.
- Crecimiento de almacenamiento.
- Nuevas máquinas.
- Necesidades del negocio.

---

# Alertas y eventos

Las plataformas virtuales generan eventos continuamente.

Ejemplos:

- Fallo de hardware.
- Máquina apagada.
- Falta de espacio.
- Problemas de red.

Las alertas permiten actuar rápidamente.

---

# Registro de actividad

La administración segura requiere registrar cambios.

Ejemplos:

- Creación de VM.
- Eliminación.
- Cambios de recursos.
- Migraciones.
- Accesos administrativos.

---

# Ejemplo práctico

Una empresa monitoriza su infraestructura:

```text
Zabbix

↓

Servidor VMware

↓

Hosts ESXi

↓

Máquinas virtuales

↓

Servicios críticos
```

Si una máquina consume demasiada CPU:

```text
Alerta

↓

Administrador revisa

↓

Ajusta recursos

↓

Problema solucionado
```

---

[⬆️ Volver al índice](#índice)