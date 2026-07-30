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
- [Buenas prácticas en la gestión de procesos](#buenas-prácticas-en-la-gestión-de-procesos)
- [Casos prácticos](#casos-prácticos)

---

## Concepto de proceso

### Introducción

Un **proceso** es una instancia de un programa que se encuentra en ejecución.

Cuando un usuario abre una aplicación o el sistema operativo ejecuta una tarea, el programa almacenado en el disco se carga en memoria y comienza a ejecutarse. En ese momento deja de ser simplemente un archivo y pasa a convertirse en un proceso.

Un mismo programa puede generar varios procesos independientes, cada uno con su propio estado y recursos asignados.

Ejemplo:

```text
Programa (almacenado en disco)

↓

Se ejecuta

↓

Proceso (en memoria)
```

---

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

### Introducción

Desde que un proceso es creado hasta que finaliza, no permanece siempre ejecutándose. A lo largo de su ciclo de vida puede pasar por diferentes **estados**, dependiendo de si está utilizando la CPU, esperando un recurso o ha terminado su ejecución.

El sistema operativo controla continuamente estos cambios mediante el **planificador de procesos (Scheduler)**, que decide qué proceso debe ejecutarse en cada momento.

Comprender los estados de un proceso es fundamental para interpretar el funcionamiento del sistema y diagnosticar problemas de rendimiento o bloqueos.

---

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

### Introducción

Un proceso no siempre ejecuta una única tarea. Muchas aplicaciones modernas realizan varias operaciones al mismo tiempo, como mostrar la interfaz, descargar información de Internet o guardar datos en segundo plano.

Para conseguirlo, los sistemas operativos utilizan los **hilos de ejecución** o **Threads**, que permiten dividir el trabajo de un proceso en varias tareas que pueden ejecutarse de forma simultánea.

Comprender la diferencia entre procesos e hilos es fundamental para entender cómo funcionan las aplicaciones actuales y cómo aprovechan los procesadores multinúcleo.

---

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