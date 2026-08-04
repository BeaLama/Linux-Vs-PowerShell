# 12 - Virtualización

## Introducción

La virtualización es una tecnología que permite crear representaciones virtuales de recursos físicos como servidores, sistemas operativos, redes o almacenamiento.

## Índice

- [Fundamentos de la virtualización](#fundamentos-de-la-virtualizacion)
- [Tipos de virtualización](#tipos-de-virtualizacion)
- [Hipervisores](#hipervisores)
- [Hipervisores de tipo 1 (Bare Metal)](#hipervisores-de-tipo-1-bare-metal)
- [Hipervisores de tipo 2 (Hosted)](#hipervisores-de-tipo-2-hosted)
- [Máquinas virtuales](#maquinas-virtuales)
- [Gestión de recursos virtuales](#gestion-de-recursos-virtuales)
- [Gestión de CPU](#gestion-de-cpu)
- [Redes virtuales](#redes-virtuales)
- [Componentes de una red virtual](#componentes-de-una-red-virtual)
- [Almacenamiento en entornos virtualizados](#almacenamiento-en-entornos-virtualizados)
- [Discos virtuales](#discos-virtuales)
- [Datastore](#datastore)
- [Alta disponibilidad y migración](#alta-disponibilidad-y-migracion)
- [Seguridad en virtualización](#seguridad-en-virtualizacion)
- [Seguridad del hipervisor](#seguridad-del-hipervisor)
- [Copias de seguridad y recuperación en entornos virtuales](#copias-de-seguridad-y-recuperacion-en-entornos-virtuales)
- [Tipos de copias de seguridad de máquinas virtuales](#tipos-de-copias-de-seguridad-de-maquinas-virtuales)
- [Monitorización y administración](#monitorizacion-y-administracion)
- [Monitorización del host físico](#monitorizacion-del-host-fisico)

---

## Fundamentos de la virtualización

*La virtualización es una tecnología que permite crear versiones virtuales de recursos físicos, permitiendo ejecutar varios sistemas independientes sobre un mismo equipo físico.*

### Virtualización frente a servidores físicos

| Servidor físico | Virtualización |
|-----------------|----------------|
| Un sistema por hardware | Varias máquinas por hardware |
| Mayor consumo | Mejor aprovechamiento |
| Menor flexibilidad | Mayor flexibilidad |
| Migración compleja | Migración sencilla |
| Recuperación más lenta | Recuperación rápida |

---

## Tipos de virtualización

*La virtualización puede aplicarse sobre diferentes recursos tecnológicos, no únicamente sobre servidores.*

### Diferencias entre máquinas virtuales y contenedores

| Máquina virtual | Contenedor |
|----------------|------------|
| Incluye sistema operativo completo | Comparte kernel |
| Mayor consumo de recursos | Menor consumo |
| Más aislamiento | Más rápido de desplegar |
| Arranque más lento | Arranque casi inmediato |

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

## Hipervisores

*El hipervisor es el componente principal de una infraestructura de virtualización.*

**Conceptos clave:**

- **¿Qué es un hipervisor?:** Un hipervisor es una plataforma que permite ejecutar varios sistemas operativos independientes sobre un mismo equipo físico.
- **Funciones principales de un hipervisor:** Las funciones más importantes son: Crear y eliminar máquinas virtuales.
- **Tipos de hipervisores:** Existen dos grandes categorías: Hipervisores de tipo 1 (Bare Metal).

---

## Hipervisores de tipo 1 (Bare Metal)

*Los hipervisores de tipo 1 se ejecutan directamente sobre el hardware físico.*

### Microsoft Hyper-V

*Hyper-V es la plataforma de virtualización de Microsoft.*

```powershell
Get-VM
```

- Windows Server.
- Algunas ediciones profesionales de Windows.

**Conceptos clave:**

- **Ventajas de los hipervisores tipo 1:** Sus principales ventajas son: Mayor rendimiento.
- **Ejemplos de hipervisores tipo 1:** Algunos ejemplos son: VMware ESXi.
- **VMware ESXi:** VMware ESXi es uno de los hipervisores empresariales más utilizados.
- **KVM:** Kernel-based Virtual Machine (KVM) es una solución de virtualización integrada en Linux.
- **Proxmox VE:** Proxmox Virtual Environment es una plataforma basada en Linux que integra: KVM para máquinas virtuales.

---

## Hipervisores de tipo 2 (Hosted)

*Los hipervisores de tipo 2 se ejecutan sobre un sistema operativo existente.*

### Comparativa tipo 1 vs tipo 2

| Característica | Tipo 1 | Tipo 2 |
|----------------|--------|--------|
| Ejecución | Directo sobre hardware | Sobre sistema operativo |
| Rendimiento | Alto | Medio |
| Uso principal | Empresas y servidores | Laboratorios y usuarios |
| Complejidad | Mayor | Menor |
| Ejemplos | ESXi, Hyper-V, KVM | VirtualBox, Workstation |

---

## Máquinas virtuales

*Las máquinas virtuales (Virtual Machines o VM) son sistemas informáticos independientes que se ejecutan dentro de un entorno virtualizado mediante un hipervisor.*

### Máquina virtual frente a equipo físico

| Equipo físico | Máquina virtual |
|---------------|----------------|
| Hardware dedicado | Hardware compartido |
| Instalación física | Instalación virtual |
| Migración compleja | Migración sencilla |
| Recuperación más lenta | Recuperación rápida |
| Mayor coste | Mejor aprovechamiento |

### Estados de una máquina virtual

*Una VM puede encontrarse en diferentes estados.*

| Estado | Descripción |
|-|-|
| Encendida | Sistema operativo ejecutándose |
| Apagada | VM detenida |
| Suspendida | Estado guardado temporalmente |
| Pausada | Ejecución detenida |
| Migrando | Moviéndose entre hosts |

---

## Gestión de recursos virtuales

*La gestión de recursos virtuales consiste en administrar y optimizar los recursos físicos de un servidor para distribuirlos correctamente entre las máquinas virtuales que se ejecutan sobre él.*

**Conceptos clave:**

- **Importancia de la gestión de recursos:** En un entorno virtualizado varias máquinas comparten el mismo hardware físico.

---

## Gestión de CPU

*La CPU física del servidor se divide en procesadores virtuales (vCPU) asignados a las máquinas virtuales.*

### Discos virtuales

*Las máquinas utilizan archivos de disco virtual.*

| Plataforma | Formato |
|-|-|
| VMware | VMDK |
| Hyper-V | VHD/VHDX |
| VirtualBox | VDI |

---

## Redes virtuales

*La virtualización de redes permite crear infraestructuras de red lógicas independientes sobre una misma infraestructura física.*

**Conceptos clave:**

- **Funcionamiento de una red virtual:** En una infraestructura tradicional.

---

## Componentes de una red virtual

*Una red virtual está formada por diferentes elementos: Tarjetas de red virtuales.*

### Port Groups

*Los grupos de puertos permiten asociar máquinas virtuales a determinadas redes.*

```powershell
New-VMSwitch
```

- Externo.
- Interno.
- Privado.

### Bonding en Linux

*Linux permite agrupar interfaces mediante bonding.*

```bash
cat /proc/net/bonding/bond0
```

- Separar redes críticas.
- Utilizar VLAN.
- Controlar acceso administrativo.
- Aplicar firewalls virtuales.
- Monitorizar tráfico.
- Limitar comunicaciones innecesarias.

**Conceptos clave:**

- **Tarjeta de red virtual (vNIC):** Cada máquina virtual dispone de una o varias tarjetas de red virtuales.
- **Switch virtual (vSwitch):** El switch virtual es uno de los componentes principales de las redes virtualizadas.
- **Tipos de switches virtuales:** Los principales tipos son: Switch interno.
- **Switch externo:** Permite comunicación entre: Máquinas virtuales.
- **Switch interno:** Permite comunicación entre: Máquinas virtuales.
- **Switch privado:** Permite comunicación únicamente entre máquinas virtuales.
- **Ventajas de utilizar VLAN:** Permiten: Separar tráfico.
- **VLAN tagging:** El etiquetado VLAN permite identificar a qué red pertenece cada paquete.
- **Ventajas de SDN:** Permite: Automatización.
- **vSwitch estándar:** Es un switch virtual configurado individualmente en cada host ESXi.
- **Distributed Switch:** Permite administrar la red de varios hosts desde una ubicación central.
- **NIC Teaming:** Permite combinar varias tarjetas de red físicas.

---

## Almacenamiento en entornos virtualizados

*El almacenamiento es uno de los componentes más importantes dentro de una infraestructura virtualizada, ya que todas las máquinas virtuales dependen de él para guardar sus sistemas operativos, aplicaciones y datos.*

**Conceptos clave:**

- **Funcionamiento del almacenamiento virtualizado:** En un entorno virtualizado, las máquinas virtuales utilizan discos virtuales que se almacenan sobre dispositivos físicos.
- **Componentes del almacenamiento virtualizado:** Los principales componentes son: Discos virtuales.

---

## Discos virtuales

*Un disco virtual es un archivo o volumen que representa un disco físico para una máquina virtual.*

| Plataforma | Formato |
|-|-|
| VMware | VMDK |
| Hyper-V | VHD/VHDX |
| VirtualBox | VDI |
| KVM | QCOW2 |

**Conceptos clave:**

- **Ventajas de los discos virtuales:** Permiten: Ampliar capacidad fácilmente.

---

## Datastore

*Un datastore es una ubicación de almacenamiento utilizada por un hipervisor para guardar máquinas virtuales.*

### Inconvenientes de SAN

*- Mayor coste.*

| RAID | Característica |
|-|-|
| RAID 0 | Rendimiento |
| RAID 1 | Espejo |
| RAID 5 | Paridad |
| RAID 6 | Doble paridad |
| RAID 10 | Rendimiento + seguridad |

- Mayor coste.
- Mayor complejidad.
- Requiere conocimientos especializados.

**Conceptos clave:**

- **Tipos de almacenamiento:** Existen diferentes formas de proporcionar almacenamiento a un entorno virtualizado.
- **Ventajas del almacenamiento local:** - Bajo coste.
- **Inconvenientes del almacenamiento local:** - Menor disponibilidad.
- **Ventajas del NAS:** - Administración sencilla.
- **Inconvenientes del NAS:** - Dependencia de la red.
- **Ventajas de SAN:** - Alto rendimiento.
- **Importancia del RAID:** El RAID protege frente al fallo de discos individuales, pero no sustituye a una copia de seguridad.
- **Ventajas del Thin Provisioning:** - Ahorro de espacio.
- **Riesgos del Thin Provisioning:** Si todas las máquinas crecen demasiado.
- **Ventajas del Thick Provisioning:** - Rendimiento más predecible.
- **Inconveniente:** Consume más almacenamiento desde el inicio.
- **IOPS:** Los IOPS indican cuántas operaciones de entrada/salida puede realizar un almacenamiento por segundo.
- **Latencia:** La latencia es el tiempo que tarda una operación de almacenamiento en completarse.

---

## Alta disponibilidad y migración

*La alta disponibilidad y la migración son dos de las principales ventajas que ofrecen los entornos virtualizados frente a las infraestructuras tradicionales.*

### Diferencia entre HA y Fault Tolerance

| HA | Fault Tolerance |
|-|-|
| Reinicia VM en otro host | Mantiene copia activa |
| Puede existir parada breve | Sin interrupción |
| Menor coste | Mayor coste |

- Estado de hosts.
- Estado de máquinas virtuales.
- Red.
- Almacenamiento.
- Recursos.

**Conceptos clave:**

- **Concepto de alta disponibilidad (HA):** La alta disponibilidad (High Availability o HA) consiste en diseñar una infraestructura capaz de mantener los servicios operativos incluso cuando se produce un fallo.
- **Objetivos de la alta disponibilidad:** Los principales objetivos son: Reducir tiempos de caída.
- **Clúster de virtualización:** La alta disponibilidad normalmente se consigue mediante clústeres.
- **Funcionamiento de un clúster HA:** Proceso.
- **Requisitos para alta disponibilidad:** Para implementar HA suelen ser necesarios: Varios hosts físicos.
- **Puntos únicos de fallo:** Un punto único de fallo (Single Point of Failure) es un componente cuya caída provoca la interrupción completa del servicio.
- **Redundancia de hardware:** Los entornos críticos utilizan componentes redundantes.
- **Migración en frío (Cold Migration):** La máquina virtual debe estar apagada para realizar el movimiento.
- **Migración en caliente (Live Migration):** Permite mover una máquina virtual mientras está funcionando.
- **VMware vMotion:** vMotion es la tecnología de VMware para migrar máquinas virtuales en ejecución entre hosts.
- **Hyper-V Live Migration:** Hyper-V dispone de una tecnología equivalente llamada Live Migration.
- **Migración de almacenamiento:** Además de mover máquinas entre hosts, también puede migrarse su almacenamiento.
- **Migración planificada:** Se realiza cuando existe tiempo para preparar el cambio.
- **Migración ante fallos:** Se realiza cuando existe una incidencia.
- **DRS (Distributed Resource Scheduler):** VMware DRS permite distribuir automáticamente máquinas virtuales según el consumo de recursos.
- **Live Migration automática:** Algunas plataformas permiten migraciones automáticas cuando detectan problemas.
- **VMware Replication:** Permite replicar máquinas virtuales hacia otro entorno.
- **Hyper-V Replica:** Hyper-V permite replicar máquinas virtuales entre servidores.

---

## Seguridad en virtualización

*La seguridad en entornos virtualizados es un aspecto fundamental, ya que una única infraestructura física puede alojar múltiples sistemas, aplicaciones y servicios críticos.*

**Conceptos clave:**

- **Importancia de la seguridad en virtualización:** En un entorno tradicional, un fallo suele afectar a un único servidor.

---

## Seguridad del hipervisor

*El hipervisor es uno de los componentes más críticos de la infraestructura.*

**Conceptos clave:**

- **Actualización del hipervisor:** Es importante mantener actualizado el software de virtualización.
- **Protección de accesos administrativos:** Los accesos al hipervisor deben estar altamente protegidos.
- **Segmentación de la red de administración:** La red de gestión del hipervisor debe estar separada del tráfico normal.
- **Actualización de sistemas invitados:** Cada máquina virtual debe mantenerse actualizada.
- **Antivirus y protección endpoint:** Las máquinas virtuales deben contar con medidas de protección.
- **Configuración segura de máquinas virtuales:** Buenas prácticas: Desactivar dispositivos innecesarios.
- **Escape de máquina virtual (VM Escape):** Un VM Escape ocurre cuando un atacante consigue salir de una máquina virtual y acceder al hipervisor o al sistema físico.
- **Medidas contra VM Escape:** Para reducir riesgos: Mantener hipervisor actualizado.
- **Separación de redes:** Es recomendable separar: Red de administración.
- **Firewalls virtuales:** Los firewalls pueden ejecutarse como máquinas virtuales.
- **Protección de discos virtuales:** Los archivos de máquinas virtuales pueden contener: Sistemas operativos.
- **Cifrado de máquinas virtuales:** Algunas plataformas permiten cifrar máquinas virtuales.

---

## Copias de seguridad y recuperación en entornos virtuales

**Conceptos clave:**

- **Importancia de las copias de seguridad en virtualización:** En una infraestructura virtualizada, una única máquina física puede contener múltiples sistemas críticos.

---

## Tipos de copias de seguridad de máquinas virtuales

*Existen diferentes estrategias para realizar backups en entornos virtualizados.*

### Diferencias entre snapshot y backup

| Snapshot | Backup |
|-|-|
| Estado temporal | Copia independiente |
| Usa el mismo almacenamiento | Puede estar externo |
| Recuperación rápida | Protección ante desastre |
| No protege frente fallo almacenamiento | Protege frente pérdida total |

**Conceptos clave:**

- **Copia completa:** Realiza una copia completa de todos los datos de una máquina virtual.
- **Copia incremental:** Guarda únicamente los cambios realizados desde la última copia.
- **Copia diferencial:** Guarda los cambios realizados desde la última copia completa.
- **Riesgos de utilizar snapshots como backup:** Los snapshots no deben utilizarse como sistema principal de protección.
- **Veeam Backup & Replication:** Es una de las soluciones más utilizadas en entornos VMware y Hyper-V.
- **Integración con hipervisores:** Las herramientas de backup pueden integrarse con: VMware vSphere.
- **Restauración completa de VM:** Recupera la máquina virtual completa.
- **Restauración de archivos individuales:** Permite recuperar únicamente archivos concretos.
- **Restauración instantánea:** Algunas soluciones permiten arrancar una máquina directamente desde el backup.
- **Ventajas de los backups inmutables:** Protegen frente a: Ransomware.

---

## Monitorización y administración

*La monitorización y administración de entornos virtualizados son procesos esenciales para garantizar el rendimiento, disponibilidad y seguridad de la infraestructura.*

**Conceptos clave:**

- **Importancia de la monitorización en virtualización:** En una infraestructura virtualizada, un único problema puede afectar a múltiples sistemas.

---

## Monitorización del host físico

*El servidor físico es la base de toda la infraestructura virtual.*

### PowerShell y virtualización

*Microsoft permite administrar Hyper-V mediante PowerShell.*

```powershell
Get-VM
```

### Automatización en VMware

*VMware dispone de PowerCLI.*

| VM | Sistema | CPU | RAM |
|-|-|-|-|
| WEB01 | Linux | 2 vCPU | 8 GB |
| SQL01 | Windows | 8 vCPU | 32 GB |

```powershell
Get-VM
```

- Nombre de VM.
- Sistema operativo.
- IP.
- Recursos asignados.
- Host donde se ejecuta.
- Responsable.

**Conceptos clave:**

- **Estado del hardware:** Muchos servidores incluyen sistemas de gestión remota.
- **VMware vCenter:** vCenter es la plataforma de administración centralizada de VMware.
- **Microsoft Hyper-V Manager:** Hyper-V Manager permite administrar entornos Hyper-V.
- **Proxmox Web Interface:** Proxmox proporciona una interfaz web para administrar: Máquinas virtuales.
- **Problemas habituales de CPU:** Pueden producirse por: Exceso de máquinas virtuales.
- **Problemas habituales de memoria:** Síntomas: Lentitud.
- **Problemas habituales de almacenamiento:** Ejemplos.
- **Problemas habituales de red:** Ejemplos: Configuración incorrecta de VLAN.
- **Zabbix:** Plataforma de monitorización de código abierto.
- **Nagios:** Herramienta utilizada para supervisión de sistemas.
- **PRTG:** Solución comercial de monitorización.
- **Grafana + Prometheus:** Solución moderna basada en métricas.

---

[⬆️ Volver al índice](#índice)
