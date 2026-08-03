# 10 - Copias de seguridad

## Introducción

Las copias de seguridad constituyen uno de los pilares fundamentales de la administración de sistemas. Su objetivo es garantizar la recuperación de la información ante incidentes como fallos de hardware, errores humanos, ataques de ransomware, desastres naturales o cualquier otra situación que comprometa la disponibilidad de los datos.

En este apartado se profundiza en las estrategias de backup utilizadas en entornos profesionales, los distintos tipos de copias, tecnologías de almacenamiento, automatización, recuperación de datos y buenas prácticas para asegurar la continuidad del servicio.

---

## Índice

- [Fundamentos de las copias de seguridad](#fundamentos-de-las-copias-de-seguridad)
- [Tipos de copias de seguridad](#tipos-de-copias-de-seguridad)
- [Estrategias y planificación](#estrategias-y-planificación)
- [Almacenamiento de las copias](#almacenamiento-de-las-copias)
- [Automatización y herramientas](#automatización-y-herramientas)
- [Restauración y recuperación](#restauración-y-recuperación)
- [Seguridad de las copias](#seguridad-de-las-copias)
- [Buenas prácticas](#buenas-prácticas)

---

## Fundamentos de las copias de seguridad

Las **copias de seguridad** (backup) son duplicados de la información almacenados en un medio distinto al original con el objetivo de poder recuperarla en caso de pérdida, corrupción o eliminación.

Constituyen una de las medidas más importantes para garantizar la continuidad de un sistema, ya que ningún dispositivo de almacenamiento es infalible y cualquier infraestructura está expuesta a incidentes.

Una copia de seguridad correctamente diseñada permite recuperar datos, aplicaciones e incluso sistemas completos con un impacto mínimo sobre la actividad de la organización.

---

### ¿Qué es una copia de seguridad?

Una copia de seguridad consiste en crear una réplica de la información para poder restaurarla posteriormente.

Proceso:

```text
Datos originales

↓

Proceso de copia

↓

Almacenamiento de backup
```

Si los datos originales se pierden:

```text
Backup

↓

Restauración

↓

Datos recuperados
```

---

### Objetivos de una copia de seguridad

Las copias de seguridad permiten:

- Recuperar información eliminada.
- Restaurar sistemas tras un fallo.
- Protegerse frente al ransomware.
- Recuperarse de errores humanos.
- Garantizar la continuidad del negocio.
- Cumplir requisitos legales o normativos.

Su finalidad principal es minimizar el impacto de cualquier incidente relacionado con la pérdida de datos.

---

### ¿Qué debe protegerse?

No toda la información tiene el mismo valor.

Normalmente se incluyen en las copias:

- Documentos.
- Bases de datos.
- Máquinas virtuales.
- Servidores.
- Configuraciones.
- Aplicaciones.
- Sistemas operativos.
- Correos electrónicos.

También conviene respaldar la configuración de dispositivos de red como routers, switches o firewalls.

---

### Riesgos frente a los que protege

Una estrategia de backup ayuda a recuperar la información tras situaciones como:

- Averías de discos.
- Fallos del sistema operativo.
- Eliminaciones accidentales.
- Errores de configuración.
- Corrupción de datos.
- Ataques de ransomware.
- Incendios.
- Inundaciones.
- Robos.

Cada uno de estos escenarios puede provocar pérdidas importantes si no existen copias actualizadas.

---

### Copia de seguridad vs disponibilidad

Una copia de seguridad **no evita que un sistema deje de funcionar**, sino que permite recuperar la información posteriormente.

Por ejemplo:

```text
RAID

↓

Evita pérdida por fallo de disco
```

```text
Backup

↓

Permite recuperar datos
```

Ambas tecnologías son complementarias y no deben confundirse.

---

### Backup, sincronización y replicación

Son conceptos diferentes.

#### Copia de seguridad

Mantiene versiones recuperables de la información.

```text
Datos

↓

Backup

↓

Versiones históricas
```

---

#### Sincronización

Mantiene dos ubicaciones con el mismo contenido.

```text
Carpeta A

⇄

Carpeta B
```

Si un archivo se elimina en un lado, normalmente también desaparecerá en el otro.

---

#### Replicación

Mantiene una copia prácticamente idéntica de los datos en otro sistema.

```text
Servidor principal

↓

Replicación

↓

Servidor secundario
```

Su objetivo principal es la alta disponibilidad.

---

### Elementos de una estrategia de backup

Una estrategia completa debe definir:

- Qué datos se copian.
- Cuándo se realizan las copias.
- Dónde se almacenan.
- Durante cuánto tiempo se conservan.
- Quién puede restaurarlas.
- Cómo se verifican.

Todos estos aspectos forman parte de la política de copias de seguridad.

---

### Frecuencia de las copias

La periodicidad depende de la importancia de la información.

Ejemplos:

| Tipo de información | Frecuencia habitual |
|----------------------|--------------------|
| Bases de datos críticas | Varias veces al día |
| Servidores | Diaria |
| Documentación | Diaria |
| Equipos personales | Semanal |
| Archivos históricos | Mensual |

Cuanto más cambian los datos, mayor suele ser la frecuencia de las copias.

---

### Integridad de las copias

Una copia de seguridad solo es útil si puede restaurarse correctamente.

Por ello es recomendable comprobar periódicamente:

- Que el proceso finaliza sin errores.
- Que los archivos son accesibles.
- Que las restauraciones funcionan correctamente.
- Que las copias no están corruptas.

No basta con crear copias; también hay que verificarlas.

---

### Importancia de la documentación

Toda estrategia de backup debería estar documentada.

Es recomendable registrar:

- Equipos protegidos.
- Horarios.
- Ubicación de las copias.
- Tiempo de retención.
- Procedimientos de restauración.
- Responsables.

Una buena documentación facilita enormemente la recuperación ante incidentes.

---

### Comparativa

| Concepto | Finalidad |
|----------|-----------|
| Backup | Recuperar información |
| Sincronización | Mantener datos iguales |
| Replicación | Alta disponibilidad |
| RAID | Redundancia frente a fallos de disco |

---

### Buenas prácticas

- Realiza copias de seguridad de toda la información crítica.
- Define una política clara sobre qué datos deben protegerse y con qué frecuencia.
- Guarda las copias en un soporte distinto al original.
- Comprueba periódicamente que las copias pueden restaurarse correctamente.
- Documenta todos los procedimientos de copia y recuperación.
- Protege también las configuraciones de servidores y dispositivos de red.
- Automatiza los procesos siempre que sea posible.
- Considera el backup como parte esencial del plan de continuidad del negocio.

---

[⬆️ Volver al índice](#índice)

## Tipos de copias de seguridad

Existen diferentes tipos de copias de seguridad, cada uno con ventajas e inconvenientes en cuanto al tiempo necesario para realizarlas, el espacio de almacenamiento requerido y la velocidad de recuperación.

La elección del tipo de backup depende de factores como la importancia de los datos, la frecuencia con la que cambian y los objetivos de recuperación definidos por la organización.

En la práctica, la mayoría de infraestructuras utilizan una combinación de varios tipos de copias.

---

### Clasificación de las copias

Los tipos más habituales son:

- Copia completa (Full Backup).
- Copia incremental.
- Copia diferencial.
- Copia espejo (Mirror Backup).
- Snapshot.
- Copia sintética.

Cada una está pensada para cubrir necesidades diferentes.

---

### Copia completa (Full Backup)

La copia completa realiza un respaldo de todos los datos seleccionados, independientemente de si han cambiado desde la última copia.

Proceso:

```text
Todos los datos

↓

Backup completo
```

Es el método más sencillo y fiable.

---

### Ventajas de la copia completa

Entre sus ventajas destacan:

- Restauración muy rápida.
- Recuperación sencilla.
- Mayor fiabilidad.
- Independencia de otras copias.

Solo es necesario disponer del último backup completo para restaurar toda la información.

---

### Inconvenientes

También presenta algunos inconvenientes.

Principalmente:

- Mayor consumo de almacenamiento.
- Más tiempo de ejecución.
- Mayor tráfico de red.

Por ello no suele realizarse continuamente.

---

### Copia incremental

Una copia incremental únicamente almacena los archivos modificados desde la última copia realizada, ya sea completa o incremental.

Proceso:

```text
Backup completo

↓

Cambios

↓

Incremental 1

↓

Más cambios

↓

Incremental 2
```

Cada copia contiene únicamente los cambios nuevos.

---

### Ventajas

Las copias incrementales ofrecen:

- Poco espacio ocupado.
- Gran velocidad de ejecución.
- Menor tráfico de red.

Son muy utilizadas para copias diarias.

---

### Inconvenientes

Para restaurar la información es necesario disponer de:

- El último backup completo.
- Todas las copias incrementales posteriores.

Si una incremental se pierde o está dañada, la restauración puede verse comprometida.

---

### Copia diferencial

La copia diferencial guarda todos los cambios realizados desde el último backup completo.

Ejemplo:

```text
Backup completo

↓

Cambios lunes

↓

Diferencial lunes
```

```text
↓

Cambios martes

↓

Diferencial martes
```

La copia del martes contiene también los cambios del lunes.

---

### Ventajas

Las copias diferenciales permiten:

- Restauraciones más sencillas que las incrementales.
- Menor dependencia entre copias.
- Buen equilibrio entre velocidad y almacenamiento.

---

### Inconvenientes

Cada nueva copia diferencial aumenta de tamaño.

Esto implica:

- Mayor espacio ocupado.
- Mayor tiempo de copia conforme pasan los días.

---

### Comparativa

Ejemplo:

Archivo modificado diariamente.

| Día | Completa | Incremental | Diferencial |
|-----|----------|-------------|-------------|
| Lunes | Todo | Todo | Todo |
| Martes | Todo | Cambios martes | Cambios martes |
| Miércoles | Todo | Cambios miércoles | Cambios martes + miércoles |
| Jueves | Todo | Cambios jueves | Cambios martes + miércoles + jueves |

---

### Copia espejo (Mirror Backup)

La copia espejo mantiene una réplica exacta de los datos originales.

Proceso:

```text
Datos originales

↓

Copia espejo
```

Si un archivo se elimina del origen, también desaparecerá del espejo.

No mantiene versiones históricas.

---

### Snapshots

Un **snapshot** captura el estado de un sistema en un momento determinado.

Puede utilizarse en:

- Máquinas virtuales.
- Sistemas de archivos.
- Cabinas SAN.
- NAS.

Proceso:

```text
Sistema

↓

Snapshot

↓

Estado congelado
```

Permiten volver rápidamente a un punto anterior.

---

### Copia sintética

Una copia sintética combina un backup completo anterior con las copias incrementales para generar un nuevo backup completo sin volver a copiar todos los datos desde el origen.

Proceso:

```text
Backup completo

+

Incrementales

↓

Nuevo Full sintético
```

Reduce el tiempo de copia y el tráfico de red.

---

### Backup en caliente (Hot Backup)

Se realiza mientras el sistema continúa funcionando.

Ventajas:

- Sin interrupción del servicio.
- Muy utilizado en servidores.
- Adecuado para bases de datos y máquinas virtuales.

Actualmente es el método más habitual.

---

### Backup en frío (Cold Backup)

Requiere detener el sistema antes de realizar la copia.

Proceso:

```text
Apagar servicio

↓

Realizar backup

↓

Encender servicio
```

Ofrece mayor consistencia, aunque implica indisponibilidad temporal.

---

### Backup online y offline

Las copias también pueden clasificarse según dónde se almacenan.

**Online**

- Siempre disponibles.
- Restauración rápida.

**Offline**

- Desconectadas de la red.
- Mayor protección frente al ransomware.

Muchas organizaciones utilizan ambos tipos simultáneamente.

---

### Comparativa

| Tipo | Espacio | Tiempo de copia | Tiempo de restauración |
|------|----------|-----------------|------------------------|
| Completa | Alto | Alto | Muy rápido |
| Incremental | Bajo | Muy rápido | Más lento |
| Diferencial | Medio | Medio | Rápido |
| Espejo | Igual que el origen | Rápido | Muy rápido |
| Snapshot | Muy bajo inicialmente | Muy rápido | Muy rápido |
| Sintética | Medio | Rápido | Muy rápido |

---

### Buenas prácticas

- Combina copias completas con incrementales o diferenciales para optimizar tiempo y almacenamiento.
- Programa los backups completos en momentos de baja actividad.
- Utiliza snapshots antes de realizar cambios importantes en sistemas o máquinas virtuales.
- Evita depender únicamente de copias espejo, ya que no conservan versiones anteriores.
- Comprueba periódicamente que todos los tipos de copia pueden restaurarse correctamente.
- Documenta la estrategia utilizada y el calendario de ejecución.
- Ajusta el tipo de copia a la criticidad y al volumen de cambios de cada sistema.
- Revisa periódicamente el espacio ocupado por las copias para evitar problemas de capacidad.

---

[⬆️ Volver al índice](#índice)

## Estrategias y planificación

Disponer de copias de seguridad no garantiza por sí solo la recuperación de la información. Es necesario definir una estrategia que determine cuándo se realizan las copias, cuánto tiempo se conservan, dónde se almacenan y cuál es el procedimiento para restaurarlas.

Una correcta planificación permite minimizar la pérdida de datos y reducir el tiempo necesario para recuperar los servicios tras una incidencia.

---

### ¿Qué es una estrategia de backup?

Una estrategia de backup es el conjunto de normas y procedimientos que regulan todo el proceso de copia y recuperación.

Debe responder a preguntas como:

- ¿Qué información debe protegerse?
- ¿Con qué frecuencia se realizan las copias?
- ¿Dónde se almacenan?
- ¿Durante cuánto tiempo se conservan?
- ¿Quién puede restaurarlas?
- ¿Cómo se verifica su integridad?

Una estrategia bien definida evita improvisaciones durante una incidencia.

---

### Clasificación de la información

No todos los datos tienen la misma importancia.

Antes de diseñar una estrategia conviene clasificar la información según su criticidad.

Ejemplo:

| Nivel | Ejemplos |
|--------|----------|
| Crítico | Bases de datos, ERP, Active Directory |
| Alto | Documentación de la empresa |
| Medio | Equipos de usuarios |
| Bajo | Archivos temporales |

Cuanto más crítica sea la información, mayor deberá ser la frecuencia de las copias.

---

### Frecuencia de las copias

La planificación debe establecer cada cuánto tiempo se ejecutarán los backups.

Ejemplo:

| Información | Frecuencia |
|--------------|-----------|
| Bases de datos | Cada hora o varias veces al día |
| Servidores | Diaria |
| Equipos de usuario | Semanal |
| Archivos históricos | Mensual |

La frecuencia dependerá de la cantidad de cambios que sufran los datos.

---

### Ventana de backup

La **ventana de backup** es el periodo durante el cual se realizan las copias.

Generalmente se eligen horarios con poca actividad para minimizar el impacto sobre los usuarios.

Ejemplo:

```text
23:00

↓

Inicio del backup

↓

02:00

↓

Fin del backup
```

En sistemas críticos pueden utilizarse copias en caliente para evitar interrupciones.

---

### Política de retención

La política de retención determina cuánto tiempo deben conservarse las copias.

Ejemplo:

| Tipo | Conservación |
|------|--------------|
| Diarias | 30 días |
| Semanales | 3 meses |
| Mensuales | 1 año |
| Anuales | 5 años |

Eliminar copias demasiado pronto puede impedir recuperar información importante.

---

### Rotación de copias

La rotación consiste en sustituir las copias más antiguas por otras nuevas siguiendo una política determinada.

Esto permite controlar el espacio ocupado sin perder la capacidad de recuperación.

---

### Estrategia Abuelo-Padre-Hijo (GFS)

Una de las políticas de rotación más utilizadas es **Grandfather-Father-Son (GFS)**.

Proceso:

```text
Diarias

↓

Semanales

↓

Mensuales
```

- **Hijo (Son):** copias diarias.
- **Padre (Father):** copias semanales.
- **Abuelo (Grandfather):** copias mensuales.

Esta estrategia proporciona varias versiones históricas de la información.

---

### Regla 3-2-1

La regla **3-2-1** es una de las recomendaciones más conocidas para proteger los datos.

Consiste en disponer de:

- **3** copias de la información.
- **2** soportes diferentes.
- **1** copia almacenada fuera de la ubicación principal (offsite).

Ejemplo:

```text
Datos originales

↓

NAS

↓

Disco externo

↓

Nube
```

Esta estrategia reduce significativamente el riesgo de pérdida total.

---

### Regla 3-2-1-1-0

Una evolución de la regla anterior es la **3-2-1-1-0**.

Añade dos recomendaciones:

- **1** copia inmutable u offline.
- **0** errores tras verificar las copias.

Esta estrategia mejora la protección frente al ransomware y otros ataques.

---

### RPO (Recovery Point Objective)

El **RPO** indica la cantidad máxima de datos que la organización está dispuesta a perder.

Ejemplo:

```text
RPO = 1 hora
```

Si el servidor falla, como máximo se perderán los cambios realizados durante la última hora.

Cuanto menor sea el RPO, mayor será la frecuencia de las copias.

---

### RTO (Recovery Time Objective)

El **RTO** representa el tiempo máximo permitido para recuperar un servicio.

Ejemplo:

```text
RTO = 2 horas
```

La restauración completa deberá finalizar antes de que transcurran dos horas desde la incidencia.

---

### Relación entre RPO y RTO

Ambos conceptos son fundamentales en cualquier plan de continuidad.

| Concepto | Significado |
|----------|-------------|
| RPO | Cantidad máxima de datos que pueden perderse |
| RTO | Tiempo máximo permitido para recuperar el servicio |

Reducir estos valores suele implicar mayores costes en infraestructura y almacenamiento.

---

### Copias locales y externas

Una buena estrategia combina diferentes ubicaciones.

Ejemplo:

```text
Servidor

↓

NAS local
```

```text
↓

Disco externo
```

```text
↓

Nube
```

De esta forma la pérdida de una ubicación no implica la pérdida de todas las copias.

---

### Pruebas de restauración

Las copias deben probarse periódicamente.

Proceso:

```text
Seleccionar backup

↓

Restaurar

↓

Comprobar integridad

↓

Validar aplicaciones
```

Una copia que nunca se ha restaurado no puede considerarse completamente fiable.

---

### Documentación

Toda estrategia debe estar documentada.

Conviene incluir:

- Calendario de copias.
- Equipos protegidos.
- Política de retención.
- Ubicación de los backups.
- Procedimientos de restauración.
- Responsables.

La documentación facilita la actuación durante una incidencia.

---

### Comparativa

| Estrategia | Objetivo |
|------------|----------|
| GFS | Rotación de copias |
| 3-2-1 | Protección frente a pérdidas |
| 3-2-1-1-0 | Protección avanzada contra ransomware |
| RPO | Limitar la pérdida de datos |
| RTO | Reducir el tiempo de recuperación |

---

### Buenas prácticas

- Diseña una estrategia adaptada a la criticidad de los datos.
- Define claramente los objetivos de RPO y RTO.
- Aplica la regla 3-2-1 como mínimo y considera la 3-2-1-1-0 para entornos críticos.
- Establece una política de retención adecuada a las necesidades de la organización.
- Programa las copias durante las ventanas de menor actividad.
- Realiza pruebas periódicas de restauración para validar las copias.
- Documenta todos los procedimientos de backup y recuperación.
- Revisa periódicamente la estrategia para adaptarla al crecimiento de la infraestructura.

---

[⬆️ Volver al índice](#índice)

## Almacenamiento de las copias

La ubicación donde se almacenan las copias de seguridad es tan importante como la propia copia. Un backup almacenado en el mismo equipo que los datos originales puede perderse ante un fallo de hardware, un incendio o un ataque de ransomware.

Por este motivo, las organizaciones suelen combinar diferentes medios de almacenamiento para aumentar la seguridad y garantizar la disponibilidad de las copias en cualquier situación.

---

### Objetivos del almacenamiento

El almacenamiento de las copias debe garantizar:

- Disponibilidad.
- Integridad.
- Confidencialidad.
- Escalabilidad.
- Rapidez de recuperación.

También debe adaptarse al volumen de información y a las necesidades de crecimiento de la organización.

---

### Tipos de almacenamiento

Los soportes más utilizados son:

- Discos duros externos.
- NAS.
- SAN.
- Servidores de backup.
- Cintas magnéticas.
- Almacenamiento en la nube.
- Sistemas híbridos.

Cada uno presenta ventajas e inconvenientes.

---

### Discos duros externos

Son una solución sencilla y económica.

Ventajas:

- Bajo coste.
- Fácil transporte.
- Gran capacidad.
- Restauración rápida.

Inconvenientes:

- Riesgo de pérdida o robo.
- Vida útil limitada.
- No adecuados como única ubicación de backup.

---

### NAS (Network Attached Storage)

Un **NAS** es un dispositivo de almacenamiento conectado a la red.

Proceso:

```text
Servidores

↓

Red

↓

NAS
```

Permite centralizar las copias de varios equipos en un único dispositivo.

---

### Ventajas del NAS

Entre sus ventajas destacan:

- Acceso desde múltiples equipos.
- Gran capacidad de almacenamiento.
- RAID para mayor disponibilidad.
- Automatización de copias.
- Administración centralizada.

Es una de las soluciones más utilizadas en pequeñas y medianas empresas.

---

### SAN (Storage Area Network)

Una **SAN** es una red dedicada exclusivamente al almacenamiento.

Proceso:

```text
Servidores

↓

Red SAN

↓

Cabina de almacenamiento
```

Se utiliza habitualmente en centros de datos y grandes organizaciones.

---

### Servidores de backup

Muchas empresas disponen de un servidor dedicado exclusivamente a almacenar copias.

Ejemplo:

```text
Equipos

↓

Servidor de Backup
```

Este servidor suele ejecutar software especializado para gestionar todas las tareas de copia y restauración.

---

### Cintas magnéticas

Las cintas siguen utilizándose en grandes organizaciones.

Ventajas:

- Muy bajo coste por terabyte.
- Gran capacidad.
- Larga conservación.
- Almacenamiento offline.

Inconvenientes:

- Restauración lenta.
- Requieren unidades específicas.
- Menor comodidad de uso.

Son habituales para copias históricas de larga duración.

---

### Almacenamiento en la nube

Cada vez más organizaciones almacenan parte de sus copias en servicios cloud.

Ejemplos:

- Microsoft Azure Backup.
- Amazon S3.
- Google Cloud Storage.
- Backblaze B2.
- Wasabi.

Proceso:

```text
Empresa

↓

Internet

↓

Nube
```

---

### Ventajas del almacenamiento cloud

Las principales ventajas son:

- Alta disponibilidad.
- Escalabilidad.
- Acceso desde cualquier ubicación.
- Protección frente a desastres locales.
- Pago según el uso.

---

### Inconvenientes

También presenta algunas limitaciones:

- Dependencia de Internet.
- Coste mensual.
- Tiempo de restauración elevado en grandes volúmenes.
- Posibles restricciones legales sobre la ubicación de los datos.

---

### Almacenamiento híbrido

Muchas organizaciones combinan almacenamiento local y cloud.

Ejemplo:

```text
Servidor

↓

NAS
```

```text
↓

Nube
```

De esta forma se obtiene una restauración rápida desde el NAS y una copia externa para recuperación ante desastres.

---

### Copias online

Las copias online permanecen conectadas a la red.

Ventajas:

- Restauración inmediata.
- Automatización.
- Acceso sencillo.

Inconvenientes:

- Mayor exposición frente al ransomware.

---

### Copias offline

Las copias offline permanecen desconectadas de la red.

Ejemplo:

```text
Backup

↓

Disco externo

↓

Guardado en caja fuerte
```

Al no estar conectadas, no pueden ser cifradas por un malware.

---

### Copias offsite

Las copias **offsite** se almacenan en una ubicación distinta a la de los sistemas originales.

Ejemplo:

```text
Oficina principal

↓

Centro de respaldo
```

Esto protege la información frente a incendios, robos o desastres naturales.

---

### Copias inmutables (Immutable Backup)

Una copia inmutable no puede modificarse ni eliminarse durante un periodo determinado.

Proceso:

```text
Backup

↓

Modo inmutable

↓

Sin modificaciones
```

Esta tecnología es especialmente eficaz frente al ransomware.

---

### Cifrado del almacenamiento

Las copias deberían almacenarse cifradas para impedir el acceso no autorizado.

Puede utilizarse:

- AES-256.
- BitLocker.
- LUKS.
- Cifrado integrado del software de backup.

Aunque el soporte sea robado, la información permanecerá protegida.

---

### Deduplicación

La deduplicación elimina bloques de datos repetidos.

Ejemplo:

```text
Archivo A

↓

Bloques repetidos

↓

Almacenamiento único
```

Ventajas:

- Menor espacio ocupado.
- Menor tráfico durante las copias.
- Ahorro de almacenamiento.

---

### Compresión

La compresión reduce el tamaño de los backups antes de almacenarlos.

Ventajas:

- Menor consumo de espacio.
- Menor tiempo de transferencia.
- Menor coste de almacenamiento.

Muchos programas de backup aplican compresión automáticamente.

---

### Comparativa

| Almacenamiento | Ventajas | Inconvenientes |
|----------------|----------|----------------|
| Disco externo | Económico | Riesgo de pérdida |
| NAS | Centralizado | Requiere red |
| SAN | Alto rendimiento | Coste elevado |
| Servidor Backup | Gestión centralizada | Necesita mantenimiento |
| Cinta | Muy económica a largo plazo | Restauración lenta |
| Cloud | Escalable y externa | Dependencia de Internet |
| Híbrido | Combina rapidez y seguridad | Mayor complejidad |

---

### Buenas prácticas

- Almacena las copias en un soporte diferente al de los datos originales.
- Combina almacenamiento local y externo para mejorar la resiliencia.
- Mantén al menos una copia offline u offsite.
- Utiliza almacenamiento inmutable para protegerte frente al ransomware.
- Cifra siempre las copias que contengan información sensible.
- Aprovecha la deduplicación y la compresión para optimizar el espacio disponible.
- Supervisa periódicamente la capacidad de almacenamiento y planifica su crecimiento.
- Comprueba regularmente que las copias almacenadas siguen siendo accesibles y restaurables.

---

[⬆️ Volver al índice](#índice)

## Automatización y herramientas

En infraestructuras profesionales, las copias de seguridad rara vez se realizan de forma manual. La automatización permite ejecutar los procesos de backup de manera periódica, reducir errores humanos, generar informes y garantizar que todas las copias se realizan conforme a la política definida.

Para ello existen numerosas herramientas especializadas capaces de proteger desde equipos individuales hasta grandes centros de datos.

---

### ¿Por qué automatizar las copias?

Realizar copias manualmente presenta numerosos inconvenientes:

- Mayor probabilidad de olvidos.
- Errores humanos.
- Falta de consistencia.
- Dificultad para gestionar muchos equipos.

La automatización garantiza que las copias se ejecuten siempre según la planificación establecida.

---

### Ventajas de la automatización

Automatizar los backups permite:

- Ejecutar copias sin intervención del administrador.
- Reducir errores.
- Ahorrar tiempo.
- Generar informes automáticos.
- Programar distintas políticas.
- Verificar el resultado de cada copia.

Es una práctica imprescindible en cualquier entorno empresarial.

---

### Programación de tareas

Las copias suelen programarse para ejecutarse automáticamente en horarios de baja actividad.

Ejemplo:

```text
23:00

↓

Inicio del backup

↓

Finalización

↓

Informe automático
```

La planificación puede ser:

- Horaria.
- Diaria.
- Semanal.
- Mensual.

---

### Automatización en Linux

En sistemas Linux la herramienta más utilizada es **cron**.

Permite ejecutar tareas automáticamente mediante el archivo **crontab**.

Ejemplo:

```bash
0 2 * * * /usr/local/scripts/backup.sh
```

En este caso el script se ejecutará todos los días a las **02:00**.

---

### Automatización en Windows

Windows utiliza el **Programador de tareas (Task Scheduler)**.

Permite programar:

- Scripts PowerShell.
- Archivos BAT.
- Programas de backup.
- Copias automáticas.

Puede ejecutarlos:

- Al iniciar el sistema.
- Al iniciar sesión.
- A una hora concreta.
- Ante determinados eventos.

---

### Scripts de backup

Muchas organizaciones desarrollan scripts propios.

Ejemplo en Linux:

```bash
rsync -av /datos /backup
```

Ejemplo en PowerShell:

```powershell
Robocopy C:\Datos D:\Backup /MIR
```

Los scripts permiten adaptar el proceso exactamente a las necesidades de la empresa.

---

### Herramientas integradas

Los propios sistemas operativos incluyen soluciones de copia de seguridad.

#### Windows

- Windows Server Backup.
- Historial de archivos.
- Copias del sistema.

#### Linux

- rsync.
- tar.
- dump.
- dd.

Estas herramientas son suficientes para muchos escenarios pequeños y medianos.

---

### Software de backup empresarial

En entornos profesionales suelen utilizarse soluciones especializadas.

Las más conocidas son:

- Veeam Backup & Replication.
- Nakivo Backup.
- Acronis Cyber Protect.
- Commvault.
- Veritas NetBackup.
- Arcserve UDP.

Estas plataformas permiten gestionar miles de equipos desde una única consola.

---

### Veeam Backup & Replication

Es una de las soluciones más utilizadas para proteger:

- Máquinas virtuales.
- Servidores físicos.
- NAS.
- Microsoft 365.
- Azure.
- AWS.

Características:

- Backups incrementales.
- Replicación.
- Restauración granular.
- Copias inmutables.
- Automatización completa.

---

### Restic

**Restic** es una herramienta de código abierto muy utilizada en Linux.

Características:

- Cifrado integrado.
- Deduplicación.
- Copias incrementales.
- Compatibilidad con múltiples almacenamientos.

Es una excelente opción para pequeñas y medianas infraestructuras.

---

### BorgBackup

**BorgBackup** está orientado a realizar copias eficientes.

Ventajas:

- Compresión.
- Deduplicación.
- Cifrado.
- Versionado.

Reduce considerablemente el espacio ocupado por las copias.

---

### Duplicati

Duplicati es una solución gratuita y multiplataforma.

Permite almacenar copias en:

- Disco local.
- NAS.
- FTP.
- SFTP.
- Azure.
- Amazon S3.
- Google Drive.
- OneDrive.

Incluye una interfaz web muy sencilla de utilizar.

---

### Rsync

**rsync** es una de las herramientas más utilizadas en Linux.

Ventajas:

- Copia únicamente los cambios.
- Muy rápida.
- Bajo consumo de ancho de banda.
- Compatible con SSH.

Es ideal para sincronizar servidores.

---

### Robocopy

En Windows destaca **Robocopy**.

Ejemplo:

```powershell
robocopy C:\Datos D:\Backup /MIR /R:2 /W:5
```

Características:

- Copia incremental.
- Reanudación automática.
- Gran rendimiento.
- Muy utilizado en servidores Windows.

---

### Informes automáticos

Las herramientas profesionales generan informes con información como:

- Inicio de la copia.
- Duración.
- Tamaño.
- Archivos copiados.
- Errores detectados.
- Resultado final.

Estos informes permiten verificar rápidamente que el proceso ha finalizado correctamente.

---

### Alertas

Cuando una copia falla es recomendable que el sistema genere una alerta.

Puede enviarse mediante:

- Correo electrónico.
- SMS.
- Aplicaciones de mensajería.
- Plataformas ITSM.
- SIEM.

Una notificación inmediata reduce el tiempo de reacción.

---

### Verificación automática

Algunas herramientas comprueban automáticamente:

- Integridad de los datos.
- Estado de las copias.
- Posibilidad de restauración.

Esta funcionalidad incrementa notablemente la fiabilidad del sistema de backup.

---

### Automatización de restauraciones

Las soluciones más avanzadas permiten automatizar pruebas de restauración.

Proceso:

```text
Backup

↓

Restauración automática

↓

Comprobación

↓

Informe
```

Esto permite validar periódicamente que las copias siguen siendo utilizables.

---

### Comparativa

| Herramienta | Sistema | Características |
|-------------|----------|-----------------|
| Windows Server Backup | Windows | Integrada |
| rsync | Linux | Sincronización eficiente |
| Robocopy | Windows | Copias avanzadas |
| Restic | Multiplataforma | Cifrado y deduplicación |
| BorgBackup | Linux | Deduplicación y compresión |
| Duplicati | Multiplataforma | Interfaz web y nube |
| Veeam | Empresarial | Backup y replicación |
| Nakivo | Empresarial | Virtualización y cloud |

---

### Buenas prácticas

- Automatiza todas las copias de seguridad siempre que sea posible.
- Programa los backups durante las horas de menor actividad.
- Utiliza herramientas adecuadas al tamaño y complejidad de la infraestructura.
- Configura alertas para detectar inmediatamente cualquier fallo en las copias.
- Revisa diariamente los informes automáticos.
- Automatiza también las verificaciones y las pruebas de restauración.
- Mantén actualizadas las herramientas de backup para beneficiarte de mejoras y correcciones de seguridad.
- Documenta la configuración y la programación de todas las tareas automatizadas.

---

[⬆️ Volver al índice](#índice)

## Restauración y recuperación

El objetivo principal de una copia de seguridad es permitir la recuperación de la información cuando se produce una incidencia. Una estrategia de backup solo puede considerarse eficaz si las copias pueden restaurarse correctamente y en un tiempo acorde con las necesidades de la organización.

La restauración debe estar documentada, probarse periódicamente y formar parte del plan de continuidad del negocio.

---

### ¿Qué es una restauración?

La restauración consiste en recuperar información previamente almacenada en una copia de seguridad.

Proceso:

```text
Backup

↓

Proceso de restauración

↓

Datos recuperados
```

Puede afectar a un único archivo o a un sistema completo.

---

### ¿Cuándo es necesario restaurar?

Las situaciones más habituales son:

- Eliminación accidental de archivos.
- Corrupción de datos.
- Fallos del sistema operativo.
- Averías de hardware.
- Ataques de ransomware.
- Errores de configuración.
- Recuperación tras un desastre.

En todos estos casos, disponer de una copia válida resulta fundamental.

---

### Tipos de restauración

Dependiendo de la situación, pueden realizarse distintos tipos de recuperación.

Los más habituales son:

- Restauración de archivos.
- Restauración de carpetas.
- Restauración de bases de datos.
- Restauración de aplicaciones.
- Restauración del sistema completo.
- Recuperación de máquinas virtuales.

Cada una requiere procedimientos diferentes.

---

### Restauración de archivos

Es el escenario más frecuente.

Ejemplo:

```text
Usuario elimina un documento

↓

Seleccionar copia

↓

Restaurar archivo

↓

Documento recuperado
```

Normalmente puede realizarse en pocos minutos.

---

### Restauración de carpetas

Cuando se elimina una estructura completa de directorios, es posible recuperar únicamente esa carpeta sin afectar al resto del sistema.

Ejemplo:

```text
Carpeta compartida

↓

Eliminación accidental

↓

Restauración
```

---

### Restauración de bases de datos

Las bases de datos suelen requerir procedimientos específicos.

Normalmente es necesario:

- Detener el servicio.
- Restaurar la base.
- Aplicar registros de transacciones (si existen).
- Verificar la consistencia.

Este tipo de recuperación debe planificarse cuidadosamente.

---

### Restauración de aplicaciones

En algunos casos basta con restaurar los archivos de una aplicación.

En otros será necesario recuperar también:

- Configuración.
- Bases de datos.
- Certificados.
- Dependencias.

---

### Restauración del sistema completo (Bare Metal Recovery)

La **Bare Metal Recovery (BMR)** permite reconstruir completamente un servidor o equipo desde cero.

Proceso:

```text
Equipo nuevo

↓

Restaurar imagen

↓

Sistema operativo

↓

Aplicaciones

↓

Configuración

↓

Datos
```

Al finalizar, el sistema queda prácticamente igual que antes del fallo.

---

### Restauración de máquinas virtuales

Las plataformas de virtualización permiten recuperar una máquina virtual completa.

Proceso:

```text
Backup VM

↓

Restauración

↓

Máquina virtual operativa
```

Muchas soluciones permiten realizar esta operación en pocos minutos.

---

### Restauración granular

La restauración granular permite recuperar únicamente un elemento concreto.

Ejemplos:

- Un archivo.
- Un correo electrónico.
- Una base de datos.
- Un usuario de Active Directory.
- Una máquina virtual.

Esto evita tener que restaurar sistemas completos innecesariamente.

---

### Recuperación tras ransomware

Si un sistema ha sido cifrado por ransomware:

Proceso recomendado:

```text
Aislar equipo

↓

Eliminar malware

↓

Verificar backups

↓

Restaurar información
```

Nunca debe restaurarse una copia sin asegurarse previamente de que el malware ha sido eliminado.

---

### Verificación tras la restauración

Una vez restaurados los datos conviene comprobar:

- Integridad de los archivos.
- Funcionamiento de las aplicaciones.
- Estado de las bases de datos.
- Permisos.
- Servicios.
- Accesibilidad de los usuarios.

No basta con completar la restauración; también debe verificarse su correcto funcionamiento.

---

### Pruebas periódicas

Las restauraciones deben probarse regularmente.

Ejemplo:

```text
Seleccionar backup

↓

Restaurar en entorno de pruebas

↓

Validar funcionamiento

↓

Documentar resultado
```

Estas pruebas permiten detectar problemas antes de una incidencia real.

---

### Procedimientos documentados

Todo proceso de recuperación debería estar documentado.

Es recomendable incluir:

- Pasos de restauración.
- Responsables.
- Tiempo estimado.
- Herramientas utilizadas.
- Validaciones posteriores.

Una buena documentación reduce considerablemente el tiempo de recuperación.

---

### RPO y RTO durante la restauración

Durante una recuperación deben cumplirse los objetivos establecidos.

Ejemplo:

```text
RPO = 1 hora

↓

Máximo de datos perdidos
```

```text
RTO = 2 horas

↓

Tiempo máximo para recuperar el servicio
```

Estos indicadores permiten medir la eficacia del proceso de recuperación.

---

### Entornos de recuperación

La restauración puede realizarse en diferentes ubicaciones.

Por ejemplo:

- Equipo original.
- Nuevo servidor.
- Máquina virtual.
- Laboratorio de pruebas.
- Infraestructura cloud.

Elegir el entorno adecuado depende del tipo de incidencia.

---


### Comparativa

| Tipo de restauración | Uso habitual |
|-----------------------|--------------|
| Archivo | Recuperar documentos eliminados |
| Carpeta | Recuperar directorios completos |
| Base de datos | Restaurar información crítica |
| Aplicación | Recuperar software y configuración |
| Máquina virtual | Recuperación rápida de servidores virtuales |
| Bare Metal | Reconstrucción completa del sistema |

---

### Buenas prácticas

- Comprueba periódicamente que todas las copias pueden restaurarse correctamente.
- Documenta detalladamente los procedimientos de recuperación.
- Realiza pruebas de restauración en entornos controlados.
- Verifica siempre la integridad de los datos recuperados.
- Asegúrate de eliminar cualquier malware antes de restaurar un sistema comprometido.
- Prioriza la recuperación de los servicios más críticos para la organización.
- Controla que los objetivos de RPO y RTO se cumplen durante las pruebas y las incidencias reales.
- Registra todas las restauraciones realizadas para facilitar auditorías y análisis posteriores.

---

[⬆️ Volver al índice](#índice)

## Seguridad de las copias

Las copias de seguridad contienen, en muchas ocasiones, la misma información crítica que los sistemas originales. Si no se protegen adecuadamente, pueden convertirse en un objetivo para atacantes o provocar fugas de información.

Por ello, una estrategia de backup debe contemplar medidas específicas para garantizar la confidencialidad, integridad y disponibilidad de las copias durante todo su ciclo de vida.

---

### ¿Por qué proteger las copias?

Una copia de seguridad puede contener:

- Información confidencial.
- Bases de datos.
- Credenciales.
- Información financiera.
- Datos personales.
- Configuraciones críticas.

Si un atacante obtiene acceso a los backups, podría comprometer toda la organización.

---

### Principales amenazas

Las copias de seguridad pueden verse afectadas por:

- Ransomware.
- Robo de soportes físicos.
- Accesos no autorizados.
- Eliminación accidental.
- Corrupción de datos.
- Fallos de hardware.
- Errores humanos.

Una estrategia de seguridad debe contemplar todos estos riesgos.

---

### Cifrado de las copias

El cifrado impide que una persona no autorizada pueda acceder al contenido de las copias.

Puede aplicarse:

- Durante el almacenamiento.
- Durante la transmisión.
- En ambos casos.

Los algoritmos más utilizados son:

- AES-256.
- ChaCha20.

El cifrado debe aplicarse especialmente cuando las copias se almacenan fuera de la organización.

---

### Protección durante la transmisión

Cuando una copia se envía a otro servidor o a la nube, la comunicación debe realizarse mediante protocolos seguros.

Ejemplos:

- HTTPS.
- SFTP.
- SSH.
- VPN.
- TLS.

Esto evita la interceptación de la información durante la transferencia.

---

### Control de acceso

No todos los usuarios deberían tener acceso a las copias.

Es recomendable limitar los permisos mediante:

- Usuarios específicos.
- Roles.
- Grupos.
- Autenticación multifactor (MFA).

Solo el personal autorizado debe poder gestionar los backups.

---

### Principio de mínimo privilegio

Los administradores del sistema no siempre necesitan permisos sobre las copias.

Del mismo modo, los administradores de backup no deberían tener acceso completo a toda la infraestructura.

Separar responsabilidades reduce el riesgo de errores y ataques internos.

---

### Copias inmutables (Immutable Backup)

Una copia inmutable no puede modificarse ni eliminarse durante un periodo determinado.

Proceso:

```text
Backup

↓

Modo inmutable

↓

Sin modificaciones
```

Aunque un atacante obtenga privilegios elevados, no podrá cifrar ni borrar estas copias.

Actualmente son una de las mejores defensas frente al ransomware.

---

### Copias offline

Una copia offline permanece completamente desconectada de la red.

Ejemplo:

```text
Backup

↓

Disco externo

↓

Desconectado
```

Al no estar accesible desde la red, el ransomware no puede cifrarla.

---

### Copias offsite

Las copias offsite se almacenan en una ubicación diferente.

Ejemplo:

```text
Sede principal

↓

Centro de respaldo
```

o

```text
Empresa

↓

Proveedor Cloud
```

Esto protege la información frente a incendios, robos o desastres naturales.

---

### Protección frente al ransomware

Una estrategia eficaz debería incluir:

- Copias offline.
- Copias inmutables.
- Segmentación de la red.
- Cuentas independientes para el software de backup.
- MFA para administradores.
- Verificación periódica de las copias.

Estas medidas dificultan enormemente que un ataque afecte a los backups.

---

### Integridad de las copias

Es importante comprobar que las copias no han sido modificadas.

Para ello pueden utilizarse:

- Hashes.
- Checksums.
- Verificaciones automáticas.
- Restauraciones de prueba.

Una copia corrupta resulta inútil durante una recuperación.

---

### Protección física

Los soportes físicos también requieren medidas de seguridad.

Ejemplos:

- Armarios cerrados.
- Cajas fuertes.
- Centros de datos protegidos.
- Control de acceso mediante tarjetas o biometría.

La seguridad física es tan importante como la lógica.

---

### Auditoría

Toda actividad relacionada con los backups debería registrarse.

Es recomendable registrar:

- Creación de copias.
- Eliminaciones.
- Restauraciones.
- Cambios de configuración.
- Accesos administrativos.

Estos registros permiten investigar incidentes y detectar actividades sospechosas.

---

### Rotación de credenciales

Las cuentas utilizadas por el software de backup deben mantenerse protegidas.

Buenas prácticas:

- Contraseñas robustas.
- Rotación periódica.
- MFA.
- Cuentas dedicadas.

Evitar utilizar cuentas de administrador del dominio siempre que sea posible.

---

### Verificación periódica

Conviene revisar regularmente:

- Estado de las copias.
- Integridad.
- Accesos.
- Permisos.
- Caducidad de certificados.
- Correcto funcionamiento del cifrado.

La supervisión continua reduce el riesgo de fallos inesperados.

---

### Comparativa

| Medida | Objetivo |
|---------|----------|
| Cifrado | Proteger la confidencialidad |
| MFA | Evitar accesos no autorizados |
| Copia offline | Proteger frente al ransomware |
| Copia inmutable | Evitar modificaciones o borrados |
| Offsite | Protección ante desastres |
| Auditoría | Registrar actividades |
| Hashes | Verificar integridad |

---

### Buenas prácticas

- Cifra todas las copias que contengan información sensible.
- Protege las cuentas del software de backup mediante MFA.
- Utiliza cuentas específicas con el principio de mínimo privilegio.
- Mantén al menos una copia offline y otra offsite.
- Implementa copias inmutables siempre que sea posible.
- Verifica periódicamente la integridad de los backups mediante restauraciones de prueba.
- Registra todas las operaciones relacionadas con las copias de seguridad.
- Revisa regularmente los permisos de acceso y las políticas de seguridad.

---

[⬆️ Volver al índice](#índice)

## Buenas prácticas

Una estrategia de copias de seguridad solo resulta eficaz cuando se mantiene de forma constante y se adapta a las necesidades de la organización. Las siguientes recomendaciones ayudan a minimizar el riesgo de pérdida de información y garantizan que los datos puedan recuperarse cuando sea necesario.

Aplicar estas buenas prácticas permite reducir el impacto de fallos, ataques informáticos y errores humanos, mejorando la continuidad del negocio.

---

### Diseñar una estrategia de backup

Antes de implementar cualquier solución conviene definir:

- Qué información debe protegerse.
- Frecuencia de las copias.
- Tiempo de conservación.
- Ubicación de las copias.
- Objetivos de RPO y RTO.
- Procedimientos de restauración.

Una estrategia bien planificada evita improvisaciones durante una incidencia.

---

### Aplicar la regla 3-2-1

Como mínimo se recomienda disponer de:

- **3** copias de la información.
- **2** soportes diferentes.
- **1** copia almacenada fuera de la ubicación principal.

Siempre que sea posible, es recomendable evolucionar hacia la regla **3-2-1-1-0**, incorporando una copia inmutable y verificaciones periódicas.

---

### Automatizar los procesos

Las copias manuales aumentan el riesgo de errores.

Es recomendable automatizar:

- Backups.
- Informes.
- Alertas.
- Verificaciones.
- Pruebas de restauración.

La automatización garantiza que las tareas se ejecuten de forma constante.

---

### Realizar copias periódicas

La frecuencia debe ajustarse a la importancia de los datos.

Ejemplo:

| Información | Frecuencia recomendada |
|--------------|------------------------|
| Bases de datos críticas | Cada hora o varias veces al día |
| Servidores | Diaria |
| Equipos de usuario | Semanal |
| Archivos históricos | Mensual |

No todos los sistemas requieren el mismo nivel de protección.

---

### Verificar las copias

Una copia que no puede restaurarse no tiene ningún valor.

Es recomendable comprobar periódicamente:

- Integridad.
- Accesibilidad.
- Restauración.
- Consistencia.

Estas verificaciones deben formar parte del mantenimiento habitual.

---

### Probar la restauración

Las restauraciones deben realizarse regularmente en entornos de prueba.

Proceso:

```text
Seleccionar backup

↓

Restaurar

↓

Validar funcionamiento

↓

Documentar resultado
```

Esto permite detectar problemas antes de una incidencia real.

---

### Mantener varias versiones

Conservar únicamente la última copia puede ser insuficiente.

Es recomendable mantener:

- Copias diarias.
- Copias semanales.
- Copias mensuales.
- Copias anuales.

Disponer de varias versiones facilita la recuperación de información modificada o eliminada hace tiempo.

---

### Proteger las copias

Los backups contienen información crítica.

Debe protegerse mediante:

- Cifrado.
- MFA.
- Control de acceso.
- Copias offline.
- Copias inmutables.

La seguridad del backup debe ser equivalente a la de los datos originales.

---

### Almacenar las copias en diferentes ubicaciones

No es recomendable guardar todas las copias en un único lugar.

Una estrategia habitual consiste en combinar:

```text
Servidor

↓

NAS local
```

```text
↓

Cloud
```

```text
↓

Disco offline
```

Así se reduce el riesgo de pérdida total.

---

### Supervisar el almacenamiento

Conviene revisar periódicamente:

- Espacio disponible.
- Estado de los discos.
- Rendimiento.
- Integridad de los datos.

Un almacenamiento saturado puede impedir la realización de nuevas copias.

---

### Documentar el proceso

Toda estrategia debería incluir documentación sobre:

- Equipos protegidos.
- Calendario.
- Política de retención.
- Procedimientos de restauración.
- Responsables.
- Herramientas utilizadas.

La documentación agiliza la recuperación ante incidentes.

---

### Revisar la estrategia periódicamente

Las necesidades de la organización cambian con el tiempo.

Es recomendable revisar regularmente:

- Nuevos servidores.
- Nuevas aplicaciones.
- Cambios en el volumen de datos.
- Nuevos riesgos.
- Cambios normativos.

La estrategia debe evolucionar junto con la infraestructura.

---

### Cumplir la normativa

Dependiendo del tipo de información, pueden existir requisitos legales relacionados con:

- Protección de datos.
- Conservación documental.
- Auditorías.
- Ubicación del almacenamiento.

La política de backups debe cumplir la legislación vigente.

---

### Formar a los administradores

El personal encargado de los backups debe conocer:

- Procedimientos de copia.
- Restauraciones.
- Herramientas utilizadas.
- Gestión de incidencias.
- Medidas de seguridad.

La formación reduce significativamente los errores operativos.

---

### Ejemplo de estrategia recomendada

```text
Backup incremental diario

↓

Backup completo semanal

↓

Backup mensual externo

↓

Copia inmutable

↓

Prueba mensual de restauración
```

Esta combinación proporciona un alto nivel de protección frente a la mayoría de incidentes.

---

### Errores frecuentes

Algunos de los errores más habituales son:

- No comprobar las copias.
- Guardar todas las copias en el mismo lugar.
- No cifrar los backups.
- No realizar pruebas de restauración.
- Utilizar únicamente copias espejo.
- No documentar los procedimientos.
- No actualizar la estrategia con el crecimiento de la infraestructura.

Evitar estos errores mejora considerablemente la fiabilidad del sistema de backup.

---

### Resumen de recomendaciones

Las principales buenas prácticas son:

- Diseñar una estrategia de backup antes de implantarla.
- Aplicar la regla 3-2-1 o 3-2-1-1-0.
- Automatizar todas las tareas posibles.
- Realizar copias con la frecuencia adecuada.
- Verificar periódicamente la integridad de las copias.
- Ejecutar pruebas de restauración de forma regular.
- Mantener varias versiones históricas.
- Cifrar y proteger el acceso a los backups.
- Combinar almacenamiento local, externo y offline.
- Revisar y actualizar continuamente la estrategia.

---

[⬆️ Volver al índice](#índice)