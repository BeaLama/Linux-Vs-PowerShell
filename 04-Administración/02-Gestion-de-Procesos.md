# Gestión de procesos

## Introducción

Los procesos son la base del funcionamiento de cualquier sistema operativo. Cada vez que un usuario ejecuta una aplicación, abre un documento o el propio sistema realiza una tarea en segundo plano, se inicia uno o varios procesos encargados de llevar a cabo esas acciones.

La gestión de procesos consiste en controlar cómo se crean, ejecutan, priorizan y finalizan dichos procesos, garantizando un uso eficiente de los recursos del sistema, como la CPU, la memoria y los dispositivos de entrada y salida.

Una correcta administración de los procesos permite mejorar el rendimiento del sistema, identificar aplicaciones que consumen recursos de forma excesiva, solucionar bloqueos y mantener la estabilidad tanto en equipos de usuario como en servidores.

# Gestión de procesos

## Índice

- [Concepto de proceso](#concepto-de-proceso)
- [Estados de un proceso](#estados-de-un-proceso)
- [Procesos e hilos (Threads)](#procesos-e-hilos-threads)
- [Planificación de procesos](#planificación-de-procesos)
- [Prioridad de procesos](#prioridad-de-procesos)
- [Gestión de procesos en Windows](#gestión-de-procesos-en-windows)
- [Gestión de procesos en Linux](#gestión-de-procesos-en-linux)
- [Servicios del sistema](#servicios-del-sistema)
- [Monitorización del rendimiento](#monitorización-del-rendimiento)
- [Procesos bloqueados y finalización de procesos](#procesos-bloqueados-y-finalización-de-procesos)
- [Procesos en segundo plano](#procesos-en-segundo-plano)
- [Automatización y tareas programadas](#automatización-y-tareas-programadas)
- [Auditoría y registros de procesos](#auditoría-y-registros-de-procesos)

---

## Concepto de proceso

# Programa vs. proceso

Aunque suelen confundirse, un programa y un proceso no son lo mismo.

| Programa | Proceso |
|----------|----------|
| Conjunto de instrucciones almacenadas en disco. | Programa que se está ejecutando en memoria. |
| Es un elemento pasivo. | Es un elemento activo. |
| No consume recursos mientras no se ejecuta. | Consume CPU, memoria y otros recursos del sistema. |

Ejemplo:

```text
Archivo:

Chrome.exe

↓

Se ejecuta

↓

Proceso Chrome
```

Es posible ejecutar varias instancias del mismo programa al mismo tiempo, creando múltiples procesos independientes.

---

# Recursos de un proceso

Cada proceso dispone de recursos propios necesarios para su ejecución.

Entre los más importantes se encuentran:

- Espacio de memoria.
- Tiempo de CPU.
- Identificador del proceso (PID).
- Prioridad de ejecución.
- Archivos abiertos.
- Recursos de entrada y salida.
- Variables de entorno.
- Hilos de ejecución (Threads).

Cada proceso administra sus propios recursos de forma independiente.

---

# Identificador del proceso (PID)

Todos los procesos poseen un identificador único denominado **PID (Process Identifier)**.

El sistema operativo utiliza este identificador para distinguir un proceso de otro.

Ejemplo:

```text
PID 1256

↓

explorer.exe
```

Otro ejemplo:

```text
PID 4312

↓

chrome.exe
```

Dos procesos nunca comparten el mismo PID al mismo tiempo.

---

# Ciclo de vida de un proceso

Todo proceso sigue un ciclo de vida desde que se crea hasta que finaliza.

De forma simplificada:

```text
Creación

↓

Ejecución

↓

Finalización
```

Durante ese tiempo el sistema operativo administra sus recursos y controla su ejecución.

En el siguiente apartado se estudiarán con mayor detalle los diferentes estados por los que puede pasar un proceso.

---

# Creación de un proceso

Un proceso puede iniciarse de diferentes formas.

Por ejemplo:

- Un usuario ejecuta una aplicación.
- El sistema operativo inicia un servicio.
- Una tarea programada ejecuta un script.
- Otro proceso crea un nuevo proceso.

Ejemplo:

```text
Usuario

↓

Abre Microsoft Word

↓

Windows crea un nuevo proceso
```

---

# Finalización de un proceso

Un proceso puede finalizar por diferentes motivos.

Los más habituales son:

- El usuario cierra la aplicación.
- El programa termina correctamente.
- Se produce un error inesperado.
- El administrador finaliza el proceso manualmente.
- El sistema operativo lo detiene.

Ejemplo:

```text
Administrador

↓

Finalizar proceso

↓

Proceso detenido
```

---

# Procesos del sistema y procesos de usuario

No todos los procesos tienen el mismo propósito.

---

## Procesos del sistema

Son iniciados por el sistema operativo y permiten su correcto funcionamiento.

Ejemplos:

- Gestión de memoria.
- Servicios del sistema.
- Controladores.
- Seguridad.

Normalmente comienzan durante el arranque del equipo.

---

## Procesos de usuario

Son iniciados por los usuarios o por las aplicaciones.

Ejemplos:

- Microsoft Word.
- Google Chrome.
- Visual Studio Code.
- Adobe Acrobat.

Estos procesos finalizan cuando el usuario cierra la aplicación o esta deja de ejecutarse.

---

# Importancia de la gestión de procesos

Una correcta gestión de procesos permite:

- Optimizar el uso de la CPU.
- Administrar la memoria.
- Detectar aplicaciones bloqueadas.
- Resolver problemas de rendimiento.
- Identificar procesos maliciosos.
- Mantener la estabilidad del sistema.

Por ello, la gestión de procesos es una de las funciones más importantes de cualquier sistema operativo.

---

# Ejemplo práctico

Un usuario abre varias aplicaciones al iniciar su jornada.

```text
Usuario

↓

Google Chrome

↓

Microsoft Outlook

↓

Microsoft Teams

↓

Visual Studio Code
```

Aunque únicamente ha ejecutado cuatro programas, el sistema operativo crea numerosos procesos adicionales para gestionar cada aplicación y los servicios asociados.

Todos estos procesos comparten los recursos del sistema y son administrados por el planificador del sistema operativo.

---

[⬆️ Volver al índice](#índice)

## Estados de un proceso

# Ciclo de vida de un proceso

De forma simplificada, un proceso pasa por los siguientes estados:

```text
Nuevo

↓

Listo

↓

En ejecución

↓

En espera

↓

Finalizado
```

Un proceso puede cambiar varias veces entre algunos de estos estados antes de terminar.

---

# Estado: Nuevo (New)

Es el primer estado de un proceso.

En esta fase:

- El proceso acaba de ser creado.
- El sistema operativo reserva los recursos necesarios.
- Se genera el PID.
- Se prepara su entrada en la cola de ejecución.

Ejemplo:

```text
Usuario ejecuta Word

↓

Windows crea el proceso

↓

Estado: Nuevo
```

---

# Estado: Listo (Ready)

Una vez creado, el proceso pasa al estado **Listo**.

Características:

- Está preparado para ejecutarse.
- Ya dispone de memoria.
- Espera a que la CPU quede disponible.

No significa que esté funcionando, únicamente está esperando su turno.

Ejemplo:

```text
Proceso listo

↓

Cola de procesos

↓

Esperando CPU
```

---

# Estado: En ejecución (Running)

En este estado el proceso está utilizando el procesador.

Durante este tiempo puede:

- Ejecutar instrucciones.
- Leer o escribir datos.
- Utilizar memoria.
- Comunicarse con otros procesos.

Solo un número limitado de procesos puede estar ejecutándose simultáneamente, dependiendo del número de núcleos del procesador.

Ejemplo:

```text
CPU

↓

Chrome.exe

↓

Ejecutándose
```

---

# Estado: En espera o Bloqueado (Waiting / Blocked)

En ocasiones un proceso necesita esperar antes de continuar.

Algunos ejemplos son:

- Esperar datos del disco.
- Esperar una respuesta de red.
- Esperar la pulsación de una tecla.
- Esperar a otro proceso.

Mientras espera, no consume tiempo de CPU.

Ejemplo:

```text
Proceso

↓

Solicita lectura del disco

↓

Esperando respuesta

↓

Estado: En espera
```

Cuando el recurso está disponible, vuelve al estado **Listo**.

---

# Estado: Finalizado (Terminated)

Es el último estado del proceso.

Se alcanza cuando:

- La aplicación termina correctamente.
- El usuario la cierra.
- El administrador finaliza el proceso.
- El sistema operativo lo detiene debido a un error.

Tras finalizar:

- Se libera la memoria.
- Se liberan los recursos.
- El PID deja de estar asociado al proceso.

Ejemplo:

```text
Usuario cierra Word

↓

Proceso finalizado

↓

Recursos liberados
```

---

# Cambios entre estados

Un proceso puede cambiar varias veces de estado durante su ejecución.

Ejemplo:

```text
Nuevo

↓

Listo

↓

En ejecución

↓

Esperando disco

↓

Listo

↓

En ejecución

↓

Finalizado
```

Este comportamiento es completamente normal y ocurre constantemente en cualquier sistema operativo.

---

# Cambio de contexto (Context Switching)

Cuando la CPU deja de ejecutar un proceso y comienza a ejecutar otro, el sistema operativo realiza un **cambio de contexto**.

Durante este proceso:

- Guarda el estado del proceso actual.
- Carga el estado del siguiente proceso.
- Continúa la ejecución.

Ejemplo:

```text
CPU

↓

Proceso A

↓

Guardar estado

↓

Proceso B

↓

Continuar ejecución
```

Aunque ocurre muy rápidamente, un número excesivo de cambios de contexto puede afectar al rendimiento.

---

# Estados en Windows

Windows administra internamente estos estados mediante su planificador.

Herramientas como:

- Administrador de tareas.
- Monitor de recursos.
- Process Explorer.

permiten visualizar procesos en ejecución y analizar su comportamiento.

---

# Estados en Linux

Linux utiliza estados similares, aunque suelen representarse mediante letras.

Al ejecutar:

```bash
ps aux
```

puede observarse una columna denominada **STAT**.

Algunos estados habituales son:

| Código | Significado |
|---------|-------------|
| R | Running (En ejecución) |
| S | Sleeping (Esperando) |
| D | Espera ininterrumpida (normalmente E/S) |
| T | Detenido |
| Z | Zombie |

Estos estados ayudan a diagnosticar el comportamiento de los procesos.

---

# Procesos Zombie

Un proceso **Zombie** es un proceso que ha finalizado su ejecución, pero cuya información aún permanece en la tabla de procesos porque el proceso padre todavía no ha recogido su estado de finalización.

Características:

- No consume CPU.
- Apenas consume memoria.
- Mantiene su PID.
- Desaparece cuando el proceso padre lo gestiona correctamente.

Ejemplo:

```text
Proceso hijo termina

↓

Proceso padre aún no recoge su estado

↓

Proceso Zombie
```

---

# Importancia de conocer los estados

Comprender los estados de los procesos permite:

- Detectar aplicaciones bloqueadas.
- Analizar problemas de rendimiento.
- Identificar cuellos de botella.
- Interpretar herramientas de monitorización.
- Diagnosticar incidencias en servidores.

---

# Ejemplo práctico

Un usuario abre un navegador web.

Proceso:

```text
Chrome.exe

↓

Nuevo

↓

Listo

↓

En ejecución

↓

Esperando respuesta de Internet

↓

Listo

↓

En ejecución

↓

Finalizado al cerrar el navegador
```

Durante toda su ejecución, el proceso cambia de estado continuamente según los recursos que necesita.

---

[⬆️ Volver al índice](#índice)

## Proceso e hilos (Threads)

# ¿Qué es un hilo?

Un **hilo (Thread)** es la unidad básica de ejecución dentro de un proceso.

Mientras que un proceso representa una aplicación en funcionamiento, un hilo representa una tarea concreta que se ejecuta dentro de dicho proceso.

Un proceso puede contener:

- Un único hilo.
- Varios hilos ejecutándose simultáneamente.

Ejemplo:

```text
Proceso

↓

Thread 1

Thread 2

Thread 3
```

---

# Diferencia entre proceso e hilo

Aunque están relacionados, no son lo mismo.

| Proceso | Hilo (Thread) |
|----------|---------------|
| Programa en ejecución. | Unidad de ejecución dentro de un proceso. |
| Tiene memoria y recursos propios. | Comparte los recursos del proceso. |
| Puede contener varios hilos. | Pertenece siempre a un único proceso. |

---

# Recursos compartidos

Todos los hilos de un mismo proceso comparten:

- Memoria.
- Archivos abiertos.
- Variables globales.
- Recursos de entrada y salida.

Sin embargo, cada hilo dispone de sus propios elementos:

- Contador de programa.
- Registros de CPU.
- Pila de ejecución (Stack).

Ejemplo:

```text
Proceso

↓

Memoria compartida

↓

Thread A

Thread B

Thread C
```

---

# Procesos monohilo

Un proceso **monohilo** únicamente dispone de un hilo de ejecución.

Esto significa que solo puede realizar una tarea cada vez.

Ejemplo:

```text
Proceso

↓

Thread único
```

Si ese hilo se bloquea, toda la aplicación deja de responder hasta que pueda continuar.

---

# Procesos multihilo

Un proceso **multihilo** contiene varios hilos que pueden trabajar de forma simultánea.

Ejemplo:

```text
Proceso

├── Thread interfaz

├── Thread descarga

├── Thread impresión

└── Thread guardado
```

Esto mejora la experiencia del usuario y aprovecha mejor los procesadores con varios núcleos.

---

# Ventajas de utilizar hilos

El uso de múltiples hilos ofrece numerosas ventajas:

- Mayor rendimiento.
- Mejor aprovechamiento de la CPU.
- Aplicaciones más fluidas.
- Posibilidad de realizar varias tareas al mismo tiempo.
- Menor consumo de recursos que crear varios procesos.

Ejemplo:

```text
Navegador

↓

Abrir varias pestañas

↓

Cada una utiliza diferentes hilos
```

---

# Inconvenientes de los hilos

Trabajar con varios hilos también presenta algunos desafíos.

Los principales son:

- Sincronización entre hilos.
- Acceso simultáneo a la memoria.
- Condiciones de carrera (*Race Conditions*).
- Bloqueos (*Deadlocks*).
- Mayor complejidad de programación.

Por ello, los desarrolladores deben controlar cuidadosamente cómo comparten la información los distintos hilos.

---

# Procesos e hilos en Windows

Windows administra tanto procesos como hilos de forma independiente.

Herramientas como:

- Administrador de tareas.
- Monitor de recursos.
- Process Explorer.

permiten visualizar el número de hilos asociados a cada proceso.

En **Process Explorer**, por ejemplo, es posible consultar el detalle de todos los threads de un proceso y su consumo de CPU.

---

# Procesos e hilos en Linux

Linux también utiliza un modelo multihilo.

Algunos comandos útiles son:

Mostrar procesos:

```bash
ps -ef
```

Mostrar hilos de un proceso:

```bash
ps -T -p PID
```

Otra opción:

```bash
top -H
```

El parámetro **-H** permite visualizar los hilos en lugar de mostrar únicamente los procesos.

---

# Ejemplo práctico

Un navegador web moderno realiza múltiples tareas simultáneamente.

Ejemplo:

```text
Google Chrome

├── Interfaz gráfica

├── Motor JavaScript

├── Descarga de archivos

├── Reproducción de vídeo

└── Comunicación de red
```

Cada una de estas tareas puede ejecutarse mediante distintos hilos, permitiendo que el navegador continúe respondiendo al usuario mientras realiza operaciones en segundo plano.

---

[⬆️ Volver al índice](#índice)

## Planificación de procesos

### ¿Qué es el planificador de procesos?

El **planificador de procesos** es el componente del sistema operativo responsable de administrar el acceso a la CPU.

Su función principal consiste en seleccionar qué proceso utilizará el procesador en cada instante.

Su función principal consiste en seleccionar qué proceso utilizará el procesador en cada instante.

Su objetivo es:

- Aprovechar al máximo la CPU.
- Evitar que un proceso monopolice el procesador.
- Mantener un sistema fluido y estable.
- Garantizar tiempos de respuesta adecuados.

Ejemplo:

```text
Procesos disponibles

↓

Planificador

↓

CPU
```

---

# ¿Por qué es necesaria la planificación?

Si todos los procesos intentaran utilizar la CPU al mismo tiempo, el sistema dejaría de funcionar correctamente.

El planificador organiza la ejecución para que todos los procesos tengan oportunidad de ejecutarse.

Ejemplo:

```text
Proceso A

Proceso B

Proceso C

↓

Planificador

↓

CPU
```

Aunque parezca que todas las aplicaciones funcionan a la vez, realmente el procesador alterna rápidamente entre ellas.

---

# Cola de procesos

Los procesos que están preparados para ejecutarse permanecen en una **cola de procesos listos**.

Cuando la CPU queda disponible, el planificador selecciona uno de ellos.

Ejemplo:

```text
Cola de procesos

↓

Proceso A

Proceso B

Proceso C

↓

CPU
```

---

# Quantum o intervalo de tiempo

Para evitar que un único proceso utilice la CPU indefinidamente, el sistema operativo asigna un **quantum** o **cuanto de tiempo**.

El quantum es el tiempo máximo durante el cual un proceso puede ejecutarse antes de ceder el procesador.

Ejemplo:

```text
Proceso A

↓

20 ms

↓

CPU pasa al siguiente proceso
```

Si el proceso aún no ha terminado, volverá a la cola de procesos listos.

---

# Cambio de contexto (Context Switch)

Cuando finaliza el quantum o un proceso debe esperar un recurso, el sistema operativo realiza un **cambio de contexto**.

Durante este proceso:

- Guarda el estado del proceso actual.
- Selecciona otro proceso.
- Restaura su estado.
- Continúa la ejecución.

Ejemplo:

```text
CPU

↓

Proceso A

↓

Guardar estado

↓

Proceso B

↓

Continuar ejecución
```

Aunque el cambio de contexto es muy rápido, realizar demasiados cambios puede afectar al rendimiento.

---

# Tipos de planificación

Los sistemas operativos pueden utilizar distintos métodos para decidir qué proceso ejecutar.

Los más habituales son:

- FIFO (First In, First Out).
- Round Robin.
- Prioridades.
- Multinivel.

Windows y Linux utilizan algoritmos mucho más complejos que combinan varias de estas técnicas.

---

## FIFO (First In, First Out)

Los procesos se ejecutan en el mismo orden en el que llegan.

Ejemplo:

```text
Proceso A

↓

Proceso B

↓

Proceso C
```

Es sencillo, pero puede provocar que procesos cortos esperen demasiado si uno anterior tarda mucho en finalizar.

---

## Round Robin

Cada proceso recibe un pequeño intervalo de tiempo (quantum).

Cuando este termina, la CPU pasa al siguiente proceso.

Ejemplo:

```text
A

↓

B

↓

C

↓

A

↓

B

↓

C
```

Este método es muy utilizado en sistemas multitarea.

---

## Planificación por prioridades

Cada proceso dispone de una prioridad.

Los procesos con mayor prioridad suelen ejecutarse antes que los de menor prioridad.

Ejemplo:

```text
Prioridad alta

↓

Proceso crítico

↓

CPU
```

Este sistema permite dar preferencia a procesos importantes, aunque debe evitarse que los procesos de baja prioridad queden indefinidamente sin ejecutarse.

---

# Planificación en procesadores multinúcleo

Los procesadores actuales disponen de varios núcleos.

Esto permite ejecutar varios procesos al mismo tiempo.

Ejemplo:

```text
CPU

├── Núcleo 1 → Proceso A

├── Núcleo 2 → Proceso B

├── Núcleo 3 → Proceso C

└── Núcleo 4 → Proceso D
```

El planificador decide tanto qué proceso ejecutar como en qué núcleo hacerlo.

---

# Planificación en Windows

Windows utiliza un planificador basado en:

- Prioridades dinámicas.
- Prioridades estáticas.
- Reparto entre núcleos.
- Balanceo de carga.

Además, adapta automáticamente la prioridad de los procesos para mantener una buena experiencia de usuario.

---

# Planificación en Linux

Linux utiliza el **Completely Fair Scheduler (CFS)** como planificador principal.

Su objetivo es repartir el tiempo de CPU de la forma más equitativa posible entre todos los procesos.

Características:

- Distribución equilibrada del tiempo de CPU.
- Optimización para sistemas multinúcleo.
- Adaptación dinámica a la carga del sistema.

---

# Importancia de una buena planificación

Una planificación eficiente permite:

- Mejorar el rendimiento.
- Reducir tiempos de espera.
- Mantener aplicaciones fluidas.
- Aprovechar todos los núcleos del procesador.
- Evitar bloqueos y saturaciones.

---

# Ejemplo práctico

Un usuario está realizando varias tareas al mismo tiempo.

Aplicaciones abiertas:

```text
Google Chrome

Microsoft Teams

Visual Studio Code

Microsoft Outlook
```

El planificador alterna constantemente entre los procesos asociados a estas aplicaciones, asignándoles pequeños intervalos de tiempo de CPU para que todas puedan responder de forma fluida al usuario.

---

[⬆️ Volver al índice](#índice)

## Prioridad de procesos

Introducción

No todos los procesos tienen la misma importancia para el sistema operativo. Algunas tareas requieren una respuesta inmediata, mientras que otras pueden ejecutarse en segundo plano sin afectar al usuario.

Para gestionar esta situación, los sistemas operativos asignan una **prioridad** a cada proceso. Esta prioridad ayuda al planificador a decidir qué procesos deben ejecutarse antes que otros cuando varios compiten por utilizar la CPU.

Una correcta gestión de prioridades permite mejorar el rendimiento del sistema y garantizar que las tareas críticas reciban los recursos necesarios.

---

# ¿Qué es la prioridad de un proceso?

La prioridad es un valor que indica la importancia de un proceso frente a los demás.

Cuanto mayor sea la prioridad, más posibilidades tendrá el proceso de utilizar la CPU antes que otros procesos de menor prioridad.

Ejemplo:

```text
Proceso A

Prioridad Alta

↓

CPU


Proceso B

Prioridad Baja

↓

Espera
```

---

# ¿Para qué sirve la prioridad?

El uso de prioridades permite:

- Favorecer procesos críticos.
- Mejorar la respuesta del sistema.
- Optimizar el uso del procesador.
- Evitar que procesos poco importantes afecten al rendimiento general.

Gracias a ello, el sistema operativo puede adaptarse mejor a diferentes cargas de trabajo.

---

# Tipos de prioridad

Aunque depende del sistema operativo, normalmente las prioridades pueden clasificarse en distintos niveles.

Ejemplo:

```text
Tiempo real

Alta

Superior a la normal

Normal

Inferior a la normal

Baja
```

La mayoría de los procesos utilizan prioridad **Normal**.

---

# Prioridad estática y dinámica

Existen dos formas principales de gestionar la prioridad.

---

## Prioridad estática

Es una prioridad fija establecida por el sistema o por el administrador.

No cambia durante la ejecución del proceso salvo que se modifique manualmente.

Ejemplo:

```text
Proceso

↓

Prioridad Alta

↓

Permanece igual
```

---

## Prioridad dinámica

El sistema operativo modifica automáticamente la prioridad según el comportamiento del proceso.

Por ejemplo:

- Procesos interactivos pueden recibir mayor prioridad.
- Procesos que consumen mucha CPU pueden reducir su prioridad temporalmente.

Esto mejora la capacidad de respuesta del sistema.

---

# Prioridad en Windows

Windows dispone de varias clases de prioridad.

Las más habituales son:

| Prioridad | Uso habitual |
|-----------|--------------|
| Tiempo real | Procesos extremadamente críticos |
| Alta | Aplicaciones importantes |
| Superior a la normal | Aplicaciones exigentes |
| Normal | Mayoría de aplicaciones |
| Inferior a la normal | Procesos secundarios |
| Baja | Procesos en segundo plano |

La prioridad puede modificarse desde:

```text
Administrador de tareas

↓

Detalles

↓

Establecer prioridad
```

---

# Prioridad en Linux

Linux utiliza un sistema basado en los valores **Nice**.

El valor Nice determina la prioridad relativa de un proceso.

Su rango es:

```text
-20

↓

Mayor prioridad

↓

0

↓

Prioridad normal

↓

19

↓

Menor prioridad
```

Cuanto menor sea el valor Nice, mayor prioridad tendrá el proceso.

---

## Consultar prioridad

Ejemplo:

```bash
ps -el
```

También puede utilizarse:

```bash
top
```

---

## Iniciar un proceso con prioridad distinta

Ejemplo:

```bash
nice -n 10 programa
```

Esto inicia el programa con una prioridad inferior a la normal.

---

## Modificar la prioridad de un proceso

Ejemplo:

```bash
renice 5 -p 3218
```

Donde:

- **5** → Nuevo valor Nice.
- **3218** → PID del proceso.

---

# Riesgos de modificar prioridades

Modificar la prioridad de un proceso puede afectar al funcionamiento del sistema.

Por ejemplo:

- Una prioridad demasiado alta puede ralentizar otras aplicaciones.
- Una prioridad demasiado baja puede hacer que un proceso tarde excesivamente en ejecutarse.
- Utilizar prioridad de tiempo real sin necesidad puede provocar inestabilidad.

Por ello, únicamente deben modificarse cuando exista una necesidad justificada.

---

# Procesos de tiempo real

Algunos sistemas necesitan ejecutar determinadas tareas con la máxima prioridad.

Ejemplos:

- Control industrial.
- Sistemas médicos.
- Equipos de telecomunicaciones.
- Producción audiovisual en tiempo real.

Estos procesos reciben prioridad muy elevada para minimizar los tiempos de respuesta.

---

# Ejemplo práctico

Un usuario está editando un vídeo mientras ejecuta una copia de seguridad.

Configuración recomendada:

```text
Editor de vídeo

↓

Prioridad Alta


Proceso de copia

↓

Prioridad Baja
```

De esta forma, el editor responde con mayor fluidez mientras la copia continúa ejecutándose en segundo plano.

---

[⬆️ Volver al índice](#índice)

## Gestión de procesos en Windows

Introducción

Windows proporciona diversas herramientas para visualizar, supervisar y administrar los procesos que se ejecutan en el sistema. Estas herramientas permiten conocer el consumo de recursos, finalizar procesos bloqueados, modificar su prioridad o analizar su comportamiento.

Una correcta gestión de los procesos resulta esencial para mantener el rendimiento del equipo, solucionar incidencias y detectar aplicaciones que puedan afectar a la estabilidad o seguridad del sistema.

---

# Administrador de tareas

El **Administrador de tareas (Task Manager)** es la herramienta principal para gestionar procesos en Windows.

Puede abrirse de varias formas:

- **Ctrl + Shift + Esc**
- **Ctrl + Alt + Supr** → Administrador de tareas
- Clic derecho sobre la barra de tareas → **Administrador de tareas**
- Ejecutando:

```text
taskmgr
```

---

# Pestaña Procesos

Es la vista más utilizada.

Muestra:

- Aplicaciones abiertas.
- Procesos en segundo plano.
- Procesos de Windows.

Para cada proceso se puede consultar:

- Nombre.
- Uso de CPU.
- Consumo de memoria.
- Uso de disco.
- Consumo de red.
- Consumo de GPU (si está disponible).

Ejemplo:

```text
Chrome

↓

CPU: 8 %

RAM: 1,2 GB
```

---

# Finalizar un proceso

Si una aplicación deja de responder, puede finalizarse manualmente.

Procedimiento:

```text
Administrador de tareas

↓

Seleccionar proceso

↓

Finalizar tarea
```

También puede hacerse con el botón derecho sobre el proceso.

---

# Pestaña Detalles

La pestaña **Detalles** ofrece información más técnica sobre cada proceso.

Entre los datos disponibles se encuentran:

- Nombre del ejecutable.
- PID.
- Estado.
- Usuario que ejecuta el proceso.
- Uso de memoria.
- Prioridad.

Esta vista es especialmente útil para tareas de administración y diagnóstico.

---

# Cambiar la prioridad de un proceso

Desde la pestaña **Detalles** es posible modificar la prioridad de un proceso.

Procedimiento:

```text
Detalles

↓

Clic derecho

↓

Establecer prioridad
```

Opciones habituales:

- Tiempo real.
- Alta.
- Superior a la normal.
- Normal.
- Inferior a la normal.
- Baja.

Estos cambios afectan únicamente a la sesión actual.

---

# Abrir la ubicación del archivo

Es posible localizar el ejecutable asociado a un proceso.

Procedimiento:

```text
Detalles

↓

Clic derecho

↓

Abrir ubicación del archivo
```

Esta función resulta útil para:

- Verificar el origen de una aplicación.
- Detectar posibles archivos maliciosos.
- Comprobar instalaciones.

---

# Monitor de recursos

Windows incorpora el **Monitor de recursos (Resource Monitor)**, una herramienta más avanzada que el Administrador de tareas.

Puede abrirse mediante:

```text
resmon
```

Permite analizar:

- CPU.
- Memoria.
- Disco.
- Red.

Además, muestra las relaciones entre procesos y recursos utilizados.

---

# Monitor de rendimiento

El **Monitor de rendimiento (Performance Monitor)** permite supervisar el sistema mediante contadores de rendimiento.

Puede iniciarse ejecutando:

```text
perfmon
```

Es una herramienta ampliamente utilizada para:

- Diagnóstico.
- Monitorización de servidores.
- Análisis del rendimiento.

---

# Gestión mediante Símbolo del sistema (CMD)

Windows dispone de varios comandos para administrar procesos.

---

## Mostrar procesos

```cmd
tasklist
```

Ejemplo:

```cmd
tasklist
```

Muestra todos los procesos en ejecución junto con su PID y consumo de memoria.

---

## Finalizar un proceso

Por nombre:

```cmd
taskkill /IM notepad.exe /F
```

Por PID:

```cmd
taskkill /PID 3456 /F
```

Parámetros:

- **/IM** → Nombre del proceso.
- **/PID** → Identificador del proceso.
- **/F** → Forzar finalización.

---

# Gestión mediante PowerShell

PowerShell proporciona comandos más completos para administrar procesos.

---

## Mostrar procesos

```powershell
Get-Process
```

---

## Buscar un proceso

```powershell
Get-Process chrome
```

---

## Finalizar un proceso

```powershell
Stop-Process -Name chrome
```

O utilizando el PID:

```powershell
Stop-Process -Id 3456
```

---

## Ordenar procesos por consumo de memoria

```powershell
Get-Process | Sort-Object WorkingSet -Descending
```

---

## Mostrar los procesos que más CPU consumen

```powershell
Get-Process | Sort-Object CPU -Descending
```

Estos comandos son muy utilizados en tareas de administración y automatización.

---

# Process Explorer (Sysinternals)

**Process Explorer** es una herramienta gratuita desarrollada por Microsoft dentro del paquete **Sysinternals**.

Ofrece mucha más información que el Administrador de tareas.

Permite visualizar:

- Árbol de procesos.
- Hilos (Threads).
- DLL cargadas.
- Archivos abiertos.
- Uso detallado de recursos.
- Firma digital del ejecutable.

Es una herramienta muy utilizada por administradores de sistemas y analistas de seguridad.

---

# Identificación de procesos sospechosos

Al analizar procesos conviene prestar atención a aspectos como:

- Nombre desconocido.
- Consumo elevado e inusual.
- Ruta de instalación sospechosa.
- Ausencia de firma digital.
- Múltiples instancias inesperadas.

Ante un proceso sospechoso es recomendable:

- Consultar su ubicación.
- Verificar su firma digital.
- Analizar el archivo con un antivirus.
- Revisar su comportamiento.

---

# Ejemplo práctico

Un usuario informa de que el equipo funciona muy lento.

Procedimiento:

```text
Abrir Administrador de tareas

↓

Ordenar por uso de CPU

↓

Identificar proceso

↓

Comprobar memoria

↓

Verificar ubicación

↓

Finalizar proceso si es necesario
```

Si el problema persiste, puede utilizarse **Process Explorer** para realizar un análisis más detallado.

---

[⬆️ Volver al índice](#índice)

## Gestión de procesos en Linux

Introducción

Linux ofrece un amplio conjunto de herramientas para visualizar, administrar y controlar los procesos del sistema. A diferencia de Windows, gran parte de estas herramientas funcionan desde la línea de comandos, lo que proporciona una gran flexibilidad y permite automatizar numerosas tareas de administración.

Conocer estos comandos es fundamental para diagnosticar problemas de rendimiento, identificar procesos bloqueados, administrar servicios y optimizar el funcionamiento de servidores y equipos Linux.

---

# Visualizar procesos

Linux permite consultar los procesos en ejecución mediante diferentes comandos.

Los más utilizados son:

- `ps`
- `top`
- `htop`
- `pstree`

Cada uno proporciona un nivel de detalle diferente.

---

# Comando ps

El comando **ps (Process Status)** muestra información sobre los procesos activos.

Mostrar los procesos del usuario actual:

```bash
ps
```

Mostrar todos los procesos del sistema:

```bash
ps -ef
```

Otra opción muy utilizada es:

```bash
ps aux
```

La salida incluye información como:

- Usuario propietario.
- PID.
- Consumo de CPU.
- Consumo de memoria.
- Estado.
- Comando ejecutado.

---

# Filtrar procesos

Es posible buscar procesos concretos utilizando `grep`.

Ejemplo:

```bash
ps -ef | grep apache
```

También:

```bash
ps aux | grep mysql
```

Esto resulta útil para localizar rápidamente un servicio o aplicación.

---

# Comando top

El comando **top** muestra información del sistema en tiempo real.

Ejecutarlo:

```bash
top
```

Permite visualizar:

- Procesos activos.
- Uso de CPU.
- Memoria utilizada.
- Tiempo de actividad.
- Carga del sistema.

La información se actualiza continuamente mientras el comando permanece abierto.

---

# Comando htop

**htop** es una versión mejorada de `top`.

Características:

- Interfaz más intuitiva.
- Colores.
- Navegación mediante teclado.
- Gestión directa de procesos.

Ejecutar:

```bash
htop
```

Si no está instalado:

```bash
sudo apt install htop
```

---

# Árbol de procesos

Linux permite visualizar la relación entre procesos padre e hijo.

Comando:

```bash
pstree
```

Ejemplo:

```bash
systemd

├── sshd

├── apache2

└── mysql
```

Esta representación facilita la comprensión de la jerarquía de procesos.

---

# Identificador del proceso (PID)

Cada proceso dispone de un identificador único.

Puede consultarse mediante:

```bash
ps -ef
```

Ejemplo:

```text
PID 2487

↓

apache2
```

El PID se utiliza posteriormente para administrar el proceso.

---

# Finalizar procesos

Linux permite detener procesos de diferentes maneras.

---

## kill

Finaliza un proceso utilizando su PID.

Ejemplo:

```bash
kill 2487
```

---

## Forzar la finalización

Si el proceso no responde:

```bash
kill -9 2487
```

La señal **-9 (SIGKILL)** obliga al sistema a finalizar inmediatamente el proceso.

Debe utilizarse únicamente cuando otras opciones no funcionan.

---

## killall

Permite finalizar procesos por nombre.

Ejemplo:

```bash
killall firefox
```

---

## pkill

Permite finalizar procesos utilizando parte del nombre.

Ejemplo:

```bash
pkill chrome
```

---

# Prioridad de procesos

Linux utiliza el valor **Nice** para establecer la prioridad.

Consultar procesos:

```bash
top
```

Cambiar prioridad:

```bash
renice 5 -p 2487
```

Iniciar un proceso con otra prioridad:

```bash
nice -n 10 programa
```

Cuanto menor sea el valor Nice, mayor prioridad tendrá el proceso.

---

# Procesos en segundo plano

Es posible ejecutar aplicaciones sin mantener la terminal ocupada.

Ejemplo:

```bash
programa &
```

El símbolo **&** envía el proceso al segundo plano.

---

# Consultar trabajos en segundo plano

```bash
jobs
```

Ejemplo:

```bash
jobs
```

Muestra los procesos iniciados desde la terminal actual.

---

# Pasar procesos al primer plano

Si un proceso está ejecutándose en segundo plano:

```bash
fg
```

También puede especificarse el número del trabajo:

```bash
fg %1
```

---

# Pasar procesos al segundo plano

Si un proceso está detenido temporalmente:

```bash
bg
```

Esto permite continuar su ejecución sin ocupar la terminal.

---

# Supervisión del consumo de recursos

Además de `top` y `htop`, Linux dispone de otras herramientas útiles.

Ejemplos:

Uso de memoria:

```bash
free -h
```

Uso del procesador:

```bash
uptime
```

Carga del sistema:

```bash
vmstat
```

Estas herramientas ayudan a diagnosticar problemas de rendimiento.

---

# Identificación de procesos sospechosos

Al analizar un sistema Linux conviene revisar:

- Procesos desconocidos.
- Consumo excesivo de CPU.
- Alto consumo de memoria.
- Procesos ejecutados por usuarios inesperados.
- Servicios iniciados automáticamente.

En caso de duda se recomienda comprobar:

- Ruta del ejecutable.
- Usuario propietario.
- Servicio asociado.
- Firma o procedencia del software.

---

# Ejemplo práctico

Un servidor comienza a responder lentamente.

Procedimiento:

```text
Ejecutar top

↓

Ordenar procesos por CPU

↓

Identificar proceso problemático

↓

Comprobar PID

↓

Analizar servicio

↓

Finalizar proceso si es necesario
```

Si el problema persiste, será necesario revisar los registros del sistema y el estado del servicio correspondiente.

---

[⬆️ Volver al índice](#índice)

## Servicios del sistema

Introducción

Además de los procesos iniciados por los usuarios, los sistemas operativos ejecutan numerosos **servicios del sistema**, encargados de realizar tareas esenciales en segundo plano sin necesidad de interacción directa.

Estos servicios permiten que el sistema operativo y las aplicaciones funcionen correctamente, proporcionando funcionalidades como acceso a la red, impresión, bases de datos, autenticación o copias de seguridad.

Su correcta administración es una tarea fundamental para garantizar la estabilidad, el rendimiento y la seguridad de cualquier equipo o servidor.

---

# ¿Qué es un servicio?

Un **servicio** es un proceso especializado que se ejecuta en segundo plano para proporcionar una función concreta al sistema operativo o a otras aplicaciones.

A diferencia de las aplicaciones convencionales:

- No suelen mostrar interfaz gráfica.
- Se inician automáticamente o bajo demanda.
- Permanecen ejecutándose mientras sean necesarios.

Ejemplo:

```text
Sistema operativo

↓

Servicio DNS

↓

Resolución de nombres
```

---

# Características de los servicios

Los servicios suelen compartir una serie de características:

- Funcionan en segundo plano.
- Pueden iniciarse automáticamente.
- No requieren intervención del usuario.
- Consumen recursos del sistema.
- Pueden depender de otros servicios.

---

# Tipos de inicio

Los servicios pueden configurarse para iniciarse de distintas formas.

---

## Automático

El servicio se inicia durante el arranque del sistema.

Ejemplo:

```text
Inicio del equipo

↓

Servicio Antivirus

↓

Ejecutándose
```

---

## Automático (inicio retrasado)

El servicio se inicia automáticamente unos segundos después del arranque.

Este modo reduce la carga inicial del sistema.

---

## Manual

El servicio únicamente se inicia cuando una aplicación o un usuario lo solicita.

---

## Deshabilitado

El servicio no puede iniciarse hasta que su configuración sea modificada.

---

# Estado de un servicio

Los estados más habituales son:

- En ejecución.
- Detenido.
- Iniciándose.
- Deteniéndose.
- Pausado.

Ejemplo:

```text
Servicio DHCP

↓

En ejecución
```

---

# Servicios en Windows

Windows utiliza el **Administrador de control de servicios (Service Control Manager - SCM)** para gestionar todos los servicios del sistema.

La herramienta gráfica puede abrirse ejecutando:

```text
services.msc
```

Desde ella es posible:

- Iniciar servicios.
- Detener servicios.
- Reiniciarlos.
- Cambiar el tipo de inicio.
- Consultar dependencias.

---

# Gestión mediante CMD

Mostrar servicios:

```cmd
sc query
```

Iniciar un servicio:

```cmd
net start NombreServicio
```

Detener un servicio:

```cmd
net stop NombreServicio
```

Ejemplo:

```cmd
net stop spooler
```

---

# Gestión mediante PowerShell

Mostrar servicios:

```powershell
Get-Service
```

Consultar un servicio concreto:

```powershell
Get-Service spooler
```

Iniciar un servicio:

```powershell
Start-Service spooler
```

Detener un servicio:

```powershell
Stop-Service spooler
```

Reiniciarlo:

```powershell
Restart-Service spooler
```

Cambiar el tipo de inicio:

```powershell
Set-Service spooler -StartupType Automatic
```

---

# Servicios en Linux

La mayoría de distribuciones actuales utilizan **systemd** como sistema de gestión de servicios.

La herramienta principal es:

```bash
systemctl
```

---

# Consultar servicios

Mostrar todos los servicios:

```bash
systemctl list-units --type=service
```

Consultar un servicio concreto:

```bash
systemctl status apache2
```

---

# Iniciar y detener servicios

Iniciar:

```bash
sudo systemctl start apache2
```

Detener:

```bash
sudo systemctl stop apache2
```

Reiniciar:

```bash
sudo systemctl restart apache2
```

Recargar configuración:

```bash
sudo systemctl reload apache2
```

---

# Habilitar y deshabilitar servicios

Habilitar inicio automático:

```bash
sudo systemctl enable apache2
```

Deshabilitar:

```bash
sudo systemctl disable apache2
```

Comprobar si está habilitado:

```bash
systemctl is-enabled apache2
```

---

# Dependencias entre servicios

Algunos servicios necesitan que otros estén funcionando previamente.

Ejemplo:

```text
Servidor web

↓

Servicio de red

↓

DNS

↓

Sistema de archivos
```

Si uno de los servicios necesarios falla, el servicio dependiente puede no iniciarse correctamente.

---

# Servicios habituales

Algunos ejemplos comunes son:

### Windows

- Print Spooler
- Windows Update
- Windows Defender
- DHCP Client
- DNS Client
- Remote Desktop Services

### Linux

- ssh
- apache2
- nginx
- mysql
- docker
- cron

---

# Riesgos relacionados con los servicios

Una mala configuración puede provocar:

- Consumo excesivo de recursos.
- Problemas de rendimiento.
- Fallos durante el arranque.
- Exposición de servicios innecesarios.
- Vulnerabilidades de seguridad.

Por ello, únicamente deben mantenerse activos los servicios realmente necesarios.

---

# Ejemplo práctico

Un usuario no puede imprimir documentos.

Procedimiento:

```text
Comprobar servicio Print Spooler

↓

Verificar estado

↓

Reiniciar servicio

↓

Realizar prueba de impresión
```

En Linux, un ejemplo similar sería un servidor web que deja de responder:

```text
Comprobar estado de Apache

↓

systemctl status apache2

↓

Reiniciar servicio

↓

Verificar funcionamiento
```

---

[⬆️ Volver al índice](#índice)

## Monitorización del rendimiento

Introducción

La monitorización del rendimiento consiste en supervisar el estado y el consumo de los recursos del sistema para garantizar un funcionamiento eficiente y detectar posibles problemas antes de que afecten a los usuarios.

Los sistemas operativos ofrecen diversas herramientas que permiten analizar el uso de la CPU, la memoria, el almacenamiento, la red y los procesos en ejecución. Gracias a esta información, los administradores pueden identificar cuellos de botella, optimizar el rendimiento y solucionar incidencias con mayor rapidez.

---

# ¿Qué es la monitorización del rendimiento?

La monitorización del rendimiento es el proceso de recopilar y analizar información sobre el funcionamiento del sistema.

Su objetivo es:

- Detectar problemas de rendimiento.
- Supervisar el uso de recursos.
- Identificar procesos que consumen demasiados recursos.
- Comprobar la estabilidad del sistema.
- Facilitar el diagnóstico de incidencias.

---

# Recursos que deben monitorizarse

Los principales recursos de un sistema son:

- Procesador (CPU).
- Memoria RAM.
- Disco.
- Red.
- Procesos.
- Servicios.

El análisis conjunto de todos ellos permite obtener una visión completa del estado del equipo o servidor.

---

# Monitorización de la CPU

La CPU es uno de los recursos más importantes del sistema.

Durante la monitorización se suele comprobar:

- Porcentaje de utilización.
- Procesos que más CPU consumen.
- Número de núcleos utilizados.
- Tiempo de actividad.

Un uso elevado de CPU durante periodos prolongados puede indicar:

- Procesos mal optimizados.
- Software malicioso.
- Sobrecarga del sistema.

---

# Monitorización de la memoria RAM

La memoria debe supervisarse para detectar:

- Consumo total.
- Memoria disponible.
- Procesos que utilizan más RAM.
- Intercambio con memoria virtual (Swap o Page File).

Un consumo excesivo puede provocar ralentizaciones y un uso intensivo de la memoria virtual.

---

# Monitorización del disco

El almacenamiento también influye directamente en el rendimiento.

Es recomendable controlar:

- Espacio libre.
- Lecturas por segundo.
- Escrituras por segundo.
- Tiempo de respuesta del disco.
- Actividad de entrada y salida (I/O).

Un disco saturado puede afectar al rendimiento de todo el sistema.

---

# Monitorización de la red

La supervisión de la red permite analizar:

- Tráfico recibido.
- Tráfico enviado.
- Velocidad de transferencia.
- Conexiones activas.
- Procesos que utilizan la red.

Esto ayuda a detectar:

- Descargas inesperadas.
- Aplicaciones consumiendo ancho de banda.
- Problemas de conectividad.

---

# Herramientas de monitorización en Windows

Windows dispone de varias herramientas integradas.

## Administrador de tareas

Permite consultar:

- CPU.
- Memoria.
- Disco.
- Red.
- GPU.
- Procesos activos.

---

## Monitor de recursos

Puede abrirse mediante:

```text
resmon
```

Proporciona información detallada sobre:

- Procesos.
- CPU.
- Disco.
- Memoria.
- Red.

---

## Monitor de rendimiento

Puede iniciarse mediante:

```text
perfmon
```

Permite trabajar con contadores de rendimiento y generar informes detallados.

Es una herramienta muy utilizada en servidores Windows.

---

# Herramientas de monitorización en Linux

Linux dispone de numerosos comandos para supervisar el rendimiento.

---

## top

```bash
top
```

Permite observar en tiempo real:

- Procesos.
- CPU.
- Memoria.
- Carga del sistema.

---

## htop

```bash
htop
```

Versión mejorada de `top`, con una interfaz más intuitiva.

---

## free

Consultar memoria:

```bash
free -h
```

---

## df

Consultar espacio en disco:

```bash
df -h
```

---

## vmstat

Consultar información del sistema:

```bash
vmstat
```

---

## iostat

Analizar el rendimiento del almacenamiento:

```bash
iostat
```

---

## sar

Obtener estadísticas históricas:

```bash
sar
```

---

# Indicadores de rendimiento

Algunos indicadores especialmente importantes son:

| Recurso | Indicador |
|----------|------------|
| CPU | % de utilización |
| RAM | Memoria utilizada |
| Disco | Tiempo de respuesta |
| Red | Tráfico enviado y recibido |
| Procesos | Consumo de CPU y memoria |

Estos valores ayudan a detectar problemas antes de que afecten al funcionamiento del sistema.

---

# Identificación de cuellos de botella

Un cuello de botella aparece cuando un recurso limita el rendimiento del sistema.

Ejemplos:

- CPU al 100 %.
- Memoria RAM agotada.
- Disco trabajando constantemente.
- Red saturada.

La monitorización permite localizar rápidamente el recurso afectado.

---

# Importancia de la monitorización

Supervisar el rendimiento permite:

- Detectar problemas antes de que se agraven.
- Optimizar recursos.
- Mejorar la estabilidad.
- Planificar ampliaciones de hardware.
- Resolver incidencias con mayor rapidez.

---

# Ejemplo práctico

Un usuario informa de que el equipo funciona muy lentamente.

Procedimiento:

```text
Comprobar CPU

↓

Revisar memoria

↓

Analizar disco

↓

Ver procesos con mayor consumo

↓

Identificar la causa
```

Tras el análisis se detecta que un proceso consume el 95 % de la CPU y varios gigabytes de memoria, provocando la ralentización del sistema.

---

[⬆️ Volver al índice](#índice)

## Procesos bloqueados y finalización de procesos

Introducción

Durante el funcionamiento de un sistema operativo, es posible que algunos procesos dejen de responder correctamente debido a errores de programación, falta de recursos o conflictos con otros procesos. Estas situaciones pueden provocar que una aplicación quede bloqueada o consuma recursos de forma anormal.

Los sistemas operativos proporcionan diferentes herramientas para identificar estos procesos y, si es necesario, finalizarlos de forma segura para recuperar el funcionamiento normal del sistema.

---

# ¿Qué es un proceso bloqueado?

Un proceso bloqueado es aquel que no puede continuar su ejecución con normalidad.

Puede deberse a que:

- Espera un recurso que no está disponible.
- Se ha producido un error interno.
- Ha dejado de responder.
- Está esperando una operación de entrada o salida (E/S).

En algunos casos el proceso se recupera automáticamente; en otros, es necesario finalizarlo manualmente.

---

# Síntomas de un proceso bloqueado

Los síntomas más habituales son:

- La aplicación deja de responder.
- La interfaz se congela.
- El consumo de CPU o memoria aumenta de forma anormal.
- El sistema funciona con lentitud.
- Aparece un mensaje indicando que la aplicación no responde.

Ejemplo:

```text
Aplicación

↓

"No responde"
```

---

# Causas habituales

Algunas de las causas más comunes son:

- Errores de programación.
- Consumo excesivo de memoria.
- Conflictos entre aplicaciones.
- Problemas de acceso al disco.
- Espera de recursos compartidos.
- Dependencias con otros procesos.

Identificar la causa ayuda a evitar que el problema vuelva a repetirse.

---

# Identificación de procesos bloqueados

Antes de finalizar un proceso conviene comprobar:

- Uso de CPU.
- Consumo de memoria.
- Estado del proceso.
- Tiempo de ejecución.
- Recursos utilizados.

Estas comprobaciones permiten determinar si realmente existe un problema.

---

# Finalizar procesos en Windows

La forma más sencilla consiste en utilizar el **Administrador de tareas**.

Procedimiento:

```text
Administrador de tareas

↓

Procesos

↓

Seleccionar proceso

↓

Finalizar tarea
```

Si el proceso continúa bloqueado, puede utilizarse la pestaña **Detalles** para finalizarlo mediante su PID.

---

# Finalizar procesos mediante CMD

Windows permite finalizar procesos desde la línea de comandos.

Por nombre:

```cmd
taskkill /IM notepad.exe /F
```

Por PID:

```cmd
taskkill /PID 3456 /F
```

Parámetros:

- **/IM** → Nombre del proceso.
- **/PID** → Identificador del proceso.
- **/F** → Fuerza la finalización.

---

# Finalizar procesos mediante PowerShell

Consultar procesos:

```powershell
Get-Process
```

Finalizar por nombre:

```powershell
Stop-Process -Name notepad
```

Finalizar por PID:

```powershell
Stop-Process -Id 3456
```

PowerShell también permite automatizar estas tareas mediante scripts.

---

# Finalizar procesos en Linux

Linux ofrece varias herramientas para detener procesos.

---

## kill

Finaliza un proceso utilizando su PID.

```bash
kill 3456
```

El sistema envía por defecto la señal **SIGTERM (15)**, permitiendo que el proceso finalice correctamente.

---

## kill -9

Si el proceso no responde:

```bash
kill -9 3456
```

La señal **SIGKILL (9)** obliga al sistema a finalizar inmediatamente el proceso.

Debe utilizarse únicamente cuando otras opciones no funcionan.

---

## killall

Finaliza todos los procesos con un mismo nombre.

```bash
killall firefox
```

---

## pkill

Permite finalizar procesos utilizando parte de su nombre.

```bash
pkill chrome
```

---

# Señales en Linux

Linux utiliza señales para comunicarse con los procesos.

Algunas de las más habituales son:

| Señal | Nombre | Descripción |
|--------|---------|-------------|
| 15 | SIGTERM | Finalización normal |
| 9 | SIGKILL | Finalización inmediata |
| 2 | SIGINT | Interrupción (Ctrl + C) |
| 19 | SIGSTOP | Detener proceso |
| 18 | SIGCONT | Reanudar proceso |

El uso de **SIGTERM** es preferible siempre que sea posible, ya que permite que el proceso cierre correctamente archivos y libere recursos.

---

# Riesgos de finalizar procesos

Finalizar un proceso de forma incorrecta puede provocar:

- Pérdida de información no guardada.
- Corrupción de archivos.
- Interrupción de servicios.
- Inestabilidad del sistema.

Por ello, siempre debe intentarse cerrar la aplicación de forma normal antes de forzar su finalización.

---

# Ejemplo práctico

Un usuario informa de que Microsoft Word ha dejado de responder.

Procedimiento:

```text
Abrir Administrador de tareas

↓

Comprobar consumo de CPU

↓

Seleccionar WINWORD.EXE

↓

Finalizar tarea

↓

Volver a iniciar la aplicación
```

En Linux, el procedimiento sería:

```text
Identificar PID

↓

kill PID

↓

Si no responde

↓

kill -9 PID
```

---

[⬆️ Volver al índice](#índice)

## Procesos en segundo plano

Introducción

No todos los procesos requieren la interacción directa del usuario. Muchos de ellos se ejecutan de forma silenciosa mientras el sistema operativo o las aplicaciones realizan tareas como comprobar actualizaciones, sincronizar archivos, gestionar la red o prestar servicios al resto del sistema.

Estos procesos reciben el nombre de **procesos en segundo plano** y son fundamentales para el funcionamiento de cualquier sistema operativo moderno.

Conocer su funcionamiento permite comprender mejor el comportamiento del sistema, optimizar el rendimiento y detectar posibles procesos innecesarios o maliciosos.

---

# ¿Qué es un proceso en segundo plano?

Un proceso en segundo plano es un proceso que se ejecuta sin mostrar una interfaz gráfica o sin requerir la interacción continua del usuario.

Su función consiste en realizar tareas de apoyo mientras el usuario continúa utilizando otras aplicaciones.

Ejemplo:

```text
Usuario navega por Internet

↓

Antivirus analiza archivos

↓

Proceso en segundo plano
```

---

# Características

Los procesos en segundo plano suelen:

- Ejecutarse automáticamente.
- No mostrar ventanas.
- Consumir recursos del sistema.
- Permanecer activos durante largos periodos.
- Iniciarse junto con el sistema operativo o una aplicación.

---

# Diferencia entre primer plano y segundo plano

| Primer plano | Segundo plano |
|---------------|---------------|
| Interacción directa con el usuario. | Sin interacción directa. |
| Normalmente muestra una ventana. | Habitualmente no muestra interfaz gráfica. |
| El usuario controla su ejecución. | El sistema o la aplicación la controlan automáticamente. |

Ejemplo:

```text
Primer plano

↓

Microsoft Word


Segundo plano

↓

Servicio de impresión
```

---

# Procesos habituales en segundo plano

Algunos ejemplos son:

- Antivirus.
- Sincronización en la nube.
- Actualizaciones automáticas.
- Servicios de impresión.
- Clientes VPN.
- Servicios de bases de datos.
- Servicios de red.
- Agentes de monitorización.

Todos ellos trabajan mientras el usuario continúa utilizando el equipo.

---

# Procesos en segundo plano en Windows

Windows ejecuta numerosos procesos de este tipo.

Pueden consultarse mediante:

```text
Administrador de tareas

↓

Procesos
```

O en la pestaña:

```text
Detalles
```

Algunos ejemplos habituales son:

- Explorer.exe
- Windows Defender
- OneDrive
- Spooler
- Runtime Broker
- svchost.exe

---

# svchost.exe

Uno de los procesos más comunes en Windows es:

```text
svchost.exe
```

Su función consiste en alojar múltiples servicios del sistema.

Por este motivo es habitual encontrar varias instancias ejecutándose simultáneamente.

Ejemplo:

```text
svchost.exe

↓

Servicio A

Servicio B

Servicio C
```

No debe considerarse sospechoso únicamente por aparecer varias veces.

---

# Procesos en segundo plano en Linux

En Linux la mayoría de procesos en segundo plano corresponden a:

- Daemons.
- Servicios del sistema.
- Procesos iniciados automáticamente.

Ejemplos:

```text
sshd

cron

systemd

apache2

mysql
```

Pueden visualizarse mediante:

```bash
ps -ef
```

O:

```bash
top
```

---

# Ejecutar procesos en segundo plano

En Linux es posible iniciar un proceso directamente en segundo plano utilizando el símbolo **&**.

Ejemplo:

```bash
firefox &
```

La terminal queda libre mientras el proceso continúa ejecutándose.

---

# Consultar procesos en segundo plano

Los trabajos iniciados desde una terminal pueden visualizarse mediante:

```bash
jobs
```

Ejemplo:

```bash
jobs
```

---

# Controlar procesos en segundo plano

Pasar un proceso al primer plano:

```bash
fg
```

Enviar un proceso al segundo plano:

```bash
bg
```

Estas herramientas son especialmente útiles cuando se trabaja desde la consola.

---

# Riesgos asociados

Aunque son necesarios, algunos procesos en segundo plano pueden provocar problemas.

Entre los más habituales:

- Consumo excesivo de CPU.
- Uso elevado de memoria.
- Inicio lento del sistema.
- Software innecesario.
- Malware ejecutándose de forma oculta.

Por ello es recomendable revisar periódicamente qué procesos permanecen activos.

---

# Ejemplo práctico

Un usuario informa de que el equipo tarda mucho en arrancar.

Procedimiento:

```text
Abrir Administrador de tareas

↓

Pestaña Inicio

↓

Revisar aplicaciones configuradas para iniciarse

↓

Deshabilitar las innecesarias

↓

Reiniciar el equipo
```

En Linux, una situación similar puede analizarse revisando los servicios habilitados durante el arranque:

```bash
systemctl list-unit-files --type=service
```

---

[⬆️ Volver al índice](#índice)

## Automatización y tareas programadas

Introducción

En la administración de sistemas es habitual que determinadas tareas deban ejecutarse de forma periódica o automática, sin necesidad de la intervención de un usuario. Ejemplos comunes son las copias de seguridad, la limpieza de archivos temporales, la actualización de bases de datos o la generación de informes.

Los sistemas operativos incorporan herramientas que permiten programar la ejecución de procesos en fechas y horas determinadas o como respuesta a determinados eventos, facilitando la automatización de tareas repetitivas y reduciendo el trabajo manual.

---

# ¿Qué es la automatización?

La automatización consiste en ejecutar tareas de forma automática mediante procesos previamente configurados.

Sus principales ventajas son:

- Reducir tareas repetitivas.
- Ahorrar tiempo.
- Disminuir errores humanos.
- Garantizar la ejecución periódica de procesos.
- Mejorar la administración del sistema.

Ejemplo:

```text
Cada día

↓

02:00

↓

Copia de seguridad automática
```

---

# ¿Qué es una tarea programada?

Una tarea programada es un proceso que el sistema operativo ejecuta automáticamente cuando se cumple una condición determinada.

Las condiciones más habituales son:

- Una fecha y hora.
- El inicio del sistema.
- El inicio de sesión de un usuario.
- La aparición de un evento específico.

---

# Automatización en Windows

Windows dispone del **Programador de tareas (Task Scheduler)**.

Puede abrirse mediante:

```text
taskschd.msc
```

O desde:

```text
Herramientas administrativas

↓

Programador de tareas
```

---

# Crear una tarea programada

Al crear una tarea es necesario definir varios elementos.

Entre ellos:

- Nombre.
- Desencadenador.
- Acción.
- Condiciones.
- Configuración adicional.

Ejemplo:

```text
Nombre

↓

Copia de seguridad

↓

Todos los días

↓

03:00

↓

Ejecutar script
```

---

# Desencadenadores

Los desencadenadores indican cuándo debe iniciarse la tarea.

Algunos ejemplos son:

- Al iniciar el equipo.
- Al iniciar sesión.
- Diariamente.
- Semanalmente.
- Mensualmente.
- Al producirse un evento.

Ejemplo:

```text
Inicio del sistema

↓

Ejecutar script de comprobación
```

---

# Acciones

Una tarea puede realizar diferentes acciones.

Las más habituales son:

- Ejecutar un programa.
- Ejecutar un script.
- Abrir un documento.
- Lanzar un comando de PowerShell.

Ejemplo:

```text
powershell.exe

↓

Inventario.ps1
```

---

# Automatización mediante PowerShell

PowerShell permite automatizar prácticamente cualquier tarea administrativa.

Ejemplo:

Mostrar procesos:

```powershell
Get-Process
```

Guardar el resultado:

```powershell
Get-Process > procesos.txt
```

Este tipo de scripts puede programarse desde el Programador de tareas.

---

# Automatización en Linux

Linux utiliza principalmente el servicio **cron** para ejecutar tareas periódicas.

También existe **systemd timers**, aunque `cron` continúa siendo una de las soluciones más utilizadas.

---

# Cron

Cada usuario dispone de una tabla denominada **crontab**, donde se almacenan las tareas programadas.

Editar la tabla:

```bash
crontab -e
```

Mostrar las tareas:

```bash
crontab -l
```

Eliminar todas las tareas:

```bash
crontab -r
```

---

# Sintaxis de cron

Cada línea de una crontab sigue la siguiente estructura:

```text
Minuto Hora Día Mes DíaSemana Comando
```

Ejemplo:

```text
0 3 * * * /home/admin/backup.sh
```

Significado:

- Minuto → 0
- Hora → 3
- Todos los días.
- Todos los meses.
- Todos los días de la semana.

Resultado:

```text
Todos los días

↓

03:00

↓

Ejecutar backup.sh
```

---

# Ejemplos de tareas cron

Ejecutar cada hora:

```text
0 * * * * comando
```

Cada lunes a las 08:00:

```text
0 8 * * 1 comando
```

Cada cinco minutos:

```text
*/5 * * * * comando
```

---

# Automatización mediante scripts

Las tareas programadas suelen ejecutar scripts.

Ejemplo en PowerShell:

```powershell
Get-Service
```

Ejemplo en Bash:

```bash
#!/bin/bash

df -h
```

Esto permite automatizar procesos complejos utilizando un único archivo.

---

# Casos habituales de automatización

Algunos ejemplos frecuentes son:

- Copias de seguridad.
- Limpieza de archivos temporales.
- Actualización de bases de datos.
- Generación de informes.
- Reinicio de servicios.
- Comprobaciones de conectividad.
- Inventarios automáticos.

---

# Ejemplo práctico

Una empresa necesita generar un inventario diario de sus equipos.

Procedimiento:

```text
Script PowerShell

↓

Obtiene información del sistema

↓

Guarda el resultado

↓

Programador de tareas

↓

Ejecución diaria

↓

08:00
```

En Linux, el mismo proceso podría automatizarse mediante una entrada en la **crontab**.

---

[⬆️ Volver al índice](#índice)

## Auditoría y registros de procesos

Introducción

La auditoría de procesos consiste en registrar y analizar la información relacionada con la creación, ejecución y finalización de los procesos del sistema. Estos registros permiten conocer qué aplicaciones se han ejecutado, cuándo lo han hecho, qué recursos han utilizado y si se ha producido algún comportamiento anómalo.

La revisión periódica de estos registros resulta fundamental para la administración de sistemas, la resolución de incidencias y la detección de posibles amenazas de seguridad.

---

# ¿Qué es la auditoría de procesos?

La auditoría de procesos es el conjunto de mecanismos utilizados para registrar la actividad de los procesos del sistema operativo.

Su objetivo es:

- Supervisar la actividad del sistema.
- Detectar errores.
- Analizar incidentes.
- Identificar procesos sospechosos.
- Facilitar investigaciones forenses.

---

# Información registrada

Dependiendo del sistema operativo y de la configuración, pueden registrarse datos como:

- Nombre del proceso.
- PID.
- Usuario que lo ejecuta.
- Fecha y hora de inicio.
- Fecha y hora de finalización.
- Recursos utilizados.
- Resultado de la ejecución.
- Errores producidos.

Esta información permite reconstruir la actividad del sistema.

---

# Importancia de la auditoría

Mantener registros de los procesos ayuda a:

- Detectar aplicaciones que fallan con frecuencia.
- Identificar procesos maliciosos.
- Analizar problemas de rendimiento.
- Investigar incidentes de seguridad.
- Cumplir políticas y normativas de auditoría.

---

# Auditoría en Windows

Windows registra gran parte de la actividad del sistema mediante el **Visor de eventos (Event Viewer)**.

Puede abrirse ejecutando:

```text
eventvwr.msc
```

O desde:

```text
Herramientas administrativas

↓

Visor de eventos
```

---

# Registros más importantes

Dentro del Visor de eventos destacan:

- Aplicación.
- Seguridad.
- Sistema.
- Configuración.
- Eventos reenviados.

Cada uno almacena información relacionada con distintos componentes del sistema.

---

# Eventos relacionados con procesos

Algunos eventos permiten conocer:

- Inicio de aplicaciones.
- Finalización de procesos.
- Errores de ejecución.
- Bloqueos.
- Fallos de servicios.

Estos eventos son especialmente útiles durante la resolución de incidencias.

---

# Auditoría avanzada

En entornos empresariales es posible habilitar auditorías avanzadas mediante las directivas de seguridad.

Estas permiten registrar, entre otros aspectos:

- Creación de procesos.
- Finalización de procesos.
- Uso de privilegios.
- Ejecución de aplicaciones.

La información registrada puede consultarse posteriormente en el Visor de eventos.

---

# Auditoría en Linux

Linux almacena información del sistema en diferentes archivos de registro (**logs**).

Dependiendo de la distribución, los más habituales son:

```text
/var/log/syslog

/var/log/messages

/var/log/auth.log

/var/log/kern.log
```

Estos registros permiten analizar el comportamiento del sistema y detectar incidencias.

---

# Visualización de registros

Consultar un archivo completo:

```bash
cat /var/log/syslog
```

Mostrar únicamente las últimas líneas:

```bash
tail /var/log/syslog
```

Seguir un registro en tiempo real:

```bash
tail -f /var/log/syslog
```

Buscar información específica:

```bash
grep "apache" /var/log/syslog
```

---

# journalctl

En sistemas que utilizan **systemd**, la herramienta principal para consultar registros es:

```bash
journalctl
```

Algunos ejemplos:

Mostrar todos los registros:

```bash
journalctl
```

Mostrar únicamente los del último arranque:

```bash
journalctl -b
```

Consultar un servicio concreto:

```bash
journalctl -u apache2
```

---

# Análisis de registros

Al revisar los registros conviene prestar atención a:

- Procesos que finalizan inesperadamente.
- Errores repetitivos.
- Reinicios frecuentes de servicios.
- Mensajes de advertencia.
- Intentos de ejecución no autorizados.

La repetición de determinados eventos puede indicar problemas de configuración o intentos de ataque.

---

# Herramientas de monitorización

Además de los registros del sistema, existen herramientas específicas que permiten supervisar procesos en tiempo real.

Algunos ejemplos:

### Windows

- Visor de eventos.
- Monitor de rendimiento.
- Process Explorer.
- Sysmon.

### Linux

- journalctl.
- top.
- htop.
- ps.
- systemctl.

Estas herramientas complementan la información almacenada en los registros.

---

# Ejemplo práctico

Un servicio deja de funcionar de forma inesperada.

Procedimiento:

```text
Comprobar registros

↓

Identificar el error

↓

Analizar el proceso afectado

↓

Aplicar la corrección

↓

Verificar que el servicio vuelve a iniciarse correctamente
```

En Linux, el análisis podría comenzar con:

```bash
journalctl -u nombre_del_servicio
```

---

[⬆️ Volver al índice](#índice)