# Procesos

## Introducción

Un proceso es un programa que se encuentra en ejecución. El sistema operativo asigna recursos como memoria, tiempo de CPU y otros elementos necesarios para que cada proceso pueda ejecutarse correctamente.

Aprender a consultar, supervisar y administrar procesos permite detectar problemas de rendimiento, identificar aplicaciones que consumen demasiados recursos y finalizar procesos cuando sea necesario.

---

## Índice

- [Listar procesos](#listar-procesos)
- [Buscar un proceso](#buscar-un-proceso)
- [Mostrar el consumo de recursos](#mostrar-el-consumo-de-recursos)
- [Ordenar procesos](#ordenar-procesos)
- [Finalizar un proceso](#finalizar-un-proceso)
- [Finalizar un proceso por PID](#finalizar-un-proceso-por-pid)
- [Iniciar un proceso](#iniciar-un-proceso)
- [Procesos en segundo plano](#procesos-en-segundo-plano)
- [Resumen de equivalencias](#resumen-de-equivalencias)

---

## Listar procesos

### Linux

```bash
ps
```

También puede utilizarse:

```bash
ps aux
```

**Descripción**

Muestra los procesos que se están ejecutando en el sistema.

- `ps` muestra los procesos asociados a la sesión actual.
- `ps aux` muestra todos los procesos del sistema junto con información detallada como el usuario, el PID, el uso de CPU y memoria.

---

### PowerShell

```powershell
Get-Process
```

**Descripción**

Muestra todos los procesos que se están ejecutando en el sistema, incluyendo información como el nombre del proceso, el identificador (PID), el uso de memoria y el tiempo de CPU.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Listar procesos | `ps` / `ps aux` | `Get-Process` |

---

### Ejemplos

**Mostrar todos los procesos**

Linux

```bash
ps aux
```

PowerShell

```powershell
Get-Process
```

---

**Mostrar únicamente los procesos del usuario actual**

Linux

```bash
ps
```

PowerShell

```powershell
Get-Process -IncludeUserName
```

---

**Mostrar información de un proceso concreto**

Linux

```bash
ps -p 1256
```

PowerShell

```powershell
Get-Process -Id 1256
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `ps` muestra únicamente los procesos de la sesión actual. | `Get-Process` muestra todos los procesos del sistema de forma predeterminada. |
| `ps aux` proporciona información detallada de todos los procesos. | La salida incluye propiedades como `Id`, `ProcessName`, `CPU` y `WorkingSet`. |
| La información se presenta como texto. | La información se devuelve como objetos que pueden filtrarse y ordenarse fácilmente. |

---

### Buenas prácticas

- Utiliza `ps aux` cuando necesites obtener una visión completa del sistema.
- Identifica el **PID** antes de finalizar un proceso.
- Filtra los resultados cuando existan muchos procesos para facilitar su análisis.
- En PowerShell, aprovecha que `Get-Process` devuelve objetos para combinarlo con `Where-Object`, `Sort-Object` o `Measure-Object`.

---

### Comandos relacionados

- [Buscar un proceso](#buscar-un-proceso)
- [Mostrar el consumo de recursos](#mostrar-el-consumo-de-recursos)
- [Ordenar procesos](#ordenar-procesos)

---

[⬆️ Volver al índice](#índice)

## Buscar un proceso

### Linux

```bash
ps aux | grep <proceso>
```

**Descripción**

Buscar un proceso cuyo nombre coincida con el texto especificado.

Generalmente se utiliza junto con `grep` para filtrar la salida de `ps aux`.

---

### PowerShell

```powershell
Get-Process <proceso>
```

También puede utilizarse:

```powershell
Get-Process | Where-Object {$_.ProcessName -like "*<proceso>*"}
```

**Descripción**

Permite buscar uno o varios procesos por su nombre.

Si se necesita una búsqueda más flexible, puede utilizarse `Where-Object`.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar un proceso | `ps aux \| grep` | `Get-Process` / `Where-Object` |

---

### Ejemplos

**Buscar el proceso de Google Chrome**

Linux

```bash
ps aux | grep chrome
```

PowerShell

```powershell
Get-Process chrome
```

---

**Buscar procesos relacionados con SSH**

Linux

```bash
ps aux | grep ssh
```

PowerShell

```powershell
Get-Process | Where-Object {$_.ProcessName -like "*ssh*"}
```

---

**Buscar el proceso del Explorador de Windows**

Linux

```bash
ps aux | grep explorer
```

PowerShell

```powershell
Get-Process explorer
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Utiliza `grep` para filtrar texto. | Puede buscar directamente por nombre mediante `Get-Process`. |
| La búsqueda distingue únicamente el texto mostrado por `ps aux`. | La búsqueda se realiza sobre la propiedad `ProcessName` del objeto. |
| La salida continúa siendo texto. | La salida son objetos que pueden seguir procesándose mediante tuberías. |

---

### Buenas prácticas

- Utiliza nombres completos del proceso siempre que sea posible.
- Si existen varios procesos con nombres similares, utiliza filtros más específicos.
- Comprueba el PID antes de finalizar un proceso.
- En PowerShell, utiliza `Where-Object` cuando necesites búsquedas parciales o más complejas.

---

### Comandos relacionados

- [Listar procesos](#listar-procesos)
- [Mostrar el consumo de recursos](#mostrar-el-consumo-de-recursos)
- [Finalizar un proceso](#finalizar-un-proceso)

---

[⬆️ Volver al índice](#índice)

## Mostrar el consumo de recursos

### Linux

```bash
top
```

También puede utilizarse:

```bash
htop
```

o

```bash
ps aux
```

**Descripción**

Permite supervisar el consumo de recursos del sistema en tiempo real.

- `top` muestra los procesos ordenados dinámicamente según su consumo de CPU.
- `htop` ofrece una interfaz interactiva más intuitiva (si está instalado).
- `ps aux` permite consultar el consumo de recursos mediante una instantánea del sistema.

---

### PowerShell

```powershell
Get-Process
```

También puede utilizarse:

```powershell
Get-Process | Sort-Object CPU -Descending
```

o

```powershell
Get-Process | Sort-Object WorkingSet -Descending
```

**Descripción**

Permite consultar el consumo de CPU y memoria de los procesos en ejecución.

Puede ordenarse por diferentes propiedades para identificar rápidamente los procesos que consumen más recursos.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Monitorizar procesos | `top` / `htop` | `Get-Process` |
| Ver consumo de CPU | `top` | `Sort-Object CPU` |
| Ver consumo de memoria | `top` / `ps aux` | `Sort-Object WorkingSet` |

---

### Ejemplos

**Mostrar los procesos en tiempo real**

Linux

```bash
top
```

PowerShell

```powershell
Get-Process
```

---

**Mostrar los procesos que más CPU consumen**

Linux

```bash
top
```

PowerShell

```powershell
Get-Process |
Sort-Object CPU -Descending
```

---

**Mostrar los procesos que más memoria consumen**

Linux

```bash
ps aux --sort=-%mem
```

PowerShell

```powershell
Get-Process |
Sort-Object WorkingSet -Descending
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `top` actualiza la información en tiempo real. | `Get-Process` muestra una instantánea del estado actual. |
| `htop` permite navegar e interactuar con los procesos desde la propia interfaz. | Es habitual combinar `Get-Process` con `Sort-Object` y `Where-Object`. |
| El consumo de CPU y memoria aparece directamente en la interfaz. | La información se obtiene a partir de las propiedades de cada objeto. |

---

### Buenas prácticas

- Supervisa periódicamente los procesos con mayor consumo de CPU y memoria.
- Investiga cualquier proceso con un consumo anormalmente elevado antes de finalizarlo.
- Utiliza `htop` siempre que esté disponible, ya que facilita la supervisión del sistema.
- Ordena los resultados por CPU o memoria para localizar rápidamente posibles problemas de rendimiento.

---

### Comandos relacionados

- [Listar procesos](#listar-procesos)
- [Buscar un proceso](#buscar-un-proceso)
- [Ordenar procesos](#ordenar-procesos)

---

[⬆️ Volver al índice](#índice)

## Ordenar procesos

### Linux

```bash
ps aux --sort=<criterio>
```

**Descripción**

Permite ordenar la lista de procesos según diferentes criterios, como el uso de CPU, memoria, usuario o identificador del proceso (PID).

---

### PowerShell

```powershell
Get-Process | Sort-Object <propiedad>
```

**Descripción**

Ordena los procesos utilizando cualquiera de sus propiedades, como el nombre, el PID, el consumo de CPU o la memoria utilizada.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ordenar procesos | `ps aux --sort` | `Sort-Object` |

---

### Ejemplos

**Ordenar por consumo de memoria (de mayor a menor)**

Linux

```bash
ps aux --sort=-%mem
```

PowerShell

```powershell
Get-Process |
Sort-Object WorkingSet -Descending
```

---

**Ordenar por consumo de CPU (de mayor a menor)**

Linux

```bash
ps aux --sort=-%cpu
```

PowerShell

```powershell
Get-Process |
Sort-Object CPU -Descending
```

---

**Ordenar por nombre del proceso**

Linux

```bash
ps aux --sort=comm
```

PowerShell

```powershell
Get-Process |
Sort-Object ProcessName
```

---

**Ordenar por PID**

Linux

```bash
ps aux --sort=pid
```

PowerShell

```powershell
Get-Process |
Sort-Object Id
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `ps aux --sort` ordena la salida según el criterio indicado. | `Sort-Object` ordena los objetos utilizando cualquiera de sus propiedades. |
| Los criterios más habituales son `%cpu`, `%mem`, `pid` y `comm`. | Las propiedades más utilizadas son `CPU`, `WorkingSet`, `ProcessName` e `Id`. |
| La salida continúa siendo texto. | La salida sigue siendo una colección de objetos. |

---

### Buenas prácticas

- Ordena los procesos por CPU o memoria para identificar rápidamente posibles problemas de rendimiento.
- Utiliza el nombre del proceso o el PID cuando necesites localizar un proceso concreto.
- Combina la ordenación con filtros para obtener resultados más precisos.
- Antes de finalizar un proceso, verifica que realmente corresponde al que deseas administrar.

---

### Comandos relacionados

- [Listar procesos](#listar-procesos)
- [Mostrar el consumo de recursos](#mostrar-el-consumo-de-recursos)
- [Finalizar un proceso](#finalizar-un-proceso)

---

[⬆️ Volver al índice](#índice)

## Finalizar un proceso

### Linux

```bash
kill <PID>
```

También puede utilizarse:

```bash
killall <proceso>
```

**Descripción**

Permite finalizar uno o varios procesos en ejecución.

- `kill` finaliza un proceso utilizando su identificador (PID).
- `killall` finaliza todos los procesos que tengan el nombre especificado.

---

### PowerShell

```powershell
Stop-Process -Name <proceso>
```

También puede utilizarse:

```powershell
Stop-Process -Id <PID>
```

**Descripción**

Permite detener uno o varios procesos mediante su nombre o su identificador (PID).

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Finalizar un proceso por nombre | `killall` | `Stop-Process -Name` |
| Finalizar un proceso por PID | `kill` | `Stop-Process -Id` |

---

### Ejemplos

**Finalizar Google Chrome**

Linux

```bash
killall chrome
```

PowerShell

```powershell
Stop-Process -Name chrome
```

---

**Finalizar el Bloc de notas**

Linux

```bash
killall notepad
```

PowerShell

```powershell
Stop-Process -Name notepad
```

---

**Forzar el cierre de todos los procesos de Firefox**

Linux

```bash
killall firefox
```

PowerShell

```powershell
Stop-Process -Name firefox
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `killall` finaliza todos los procesos con el nombre indicado. | `Stop-Process -Name` también finaliza todos los procesos que coincidan con ese nombre. |
| `kill` trabaja utilizando el PID. | `Stop-Process` permite utilizar tanto el nombre como el PID. |
| Es posible enviar diferentes señales al proceso (`SIGTERM`, `SIGKILL`, etc.). | Finaliza el proceso utilizando las capacidades del sistema operativo. |

---

### Buenas prácticas

- Comprueba siempre qué proceso vas a finalizar antes de ejecutar el comando.
- Guarda el trabajo antes de cerrar aplicaciones si es posible.
- Evita finalizar procesos críticos del sistema.
- Intenta cerrar una aplicación de forma normal antes de forzar su finalización.

---

### Comandos relacionados

- [Buscar un proceso](#buscar-un-proceso)
- [Finalizar un proceso por PID](#finalizar-un-proceso-por-pid)
- [Iniciar un proceso](#iniciar-un-proceso)

---

> **⚠️ Advertencia:** Finalizar un proceso puede provocar la pérdida de datos no guardados. Antes de hacerlo, verifica que no se trata de un proceso esencial para el sistema o para otros usuarios.

---

[⬆️ Volver al índice](#índice)

## Finalizar un proceso por PID

### Linux

```bash
kill <PID>
```

También puede utilizarse:

```bash
kill -9 <PID>
```

**Descripción**

Permite finalizar un proceso utilizando su identificador (**PID**).

- `kill` envía la señal **SIGTERM (15)**, solicitando al proceso que finalice correctamente.
- `kill -9` envía la señal **SIGKILL (9)**, forzando la finalización inmediata del proceso.

---

### PowerShell

```powershell
Stop-Process -Id <PID>
```

También puede utilizarse:

```powershell
Stop-Process -Id <PID> -Force
```

**Descripción**

Permite detener un proceso utilizando su identificador (PID).

La opción `-Force` intenta finalizar el proceso de forma forzada cuando sea necesario.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Finalizar un proceso por PID | `kill <PID>` | `Stop-Process -Id <PID>` |
| Forzar la finalización | `kill -9 <PID>` | `Stop-Process -Id <PID> -Force` |

---

### Ejemplos

**Finalizar un proceso mediante su PID**

Linux

```bash
kill 2548
```

PowerShell

```powershell
Stop-Process -Id 2548
```

---

**Forzar el cierre de un proceso bloqueado**

Linux

```bash
kill -9 2548
```

PowerShell

```powershell
Stop-Process -Id 2548 -Force
```

---

**Finalizar varios procesos mediante su PID**

Linux

```bash
kill 1256 2410 3987
```

PowerShell

```powershell
Stop-Process -Id 1256,2410,3987
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `kill` envía una señal al proceso. | `Stop-Process` solicita al sistema operativo que finalice el proceso. |
| `kill -9` fuerza la finalización mediante la señal `SIGKILL`. | `-Force` intenta finalizar el proceso cuando no responde correctamente. |
| Existen numerosas señales además de `SIGTERM` y `SIGKILL`. | No se utilizan señales como en Linux; la administración se realiza mediante las funciones del sistema operativo. |

---

### Buenas prácticas

- Utiliza primero `kill` o `Stop-Process` sin forzar el cierre.
- Recurre a `kill -9` o `-Force` únicamente cuando el proceso no responda.
- Comprueba que el PID corresponde al proceso correcto antes de finalizarlo.
- Evita finalizar procesos críticos del sistema, ya que puede provocar inestabilidad o pérdida de datos.

---

### Comandos relacionados

- [Buscar un proceso](#buscar-un-proceso)
- [Finalizar un proceso](#finalizar-un-proceso)
- [Iniciar un proceso](#iniciar-un-proceso)

---

> **⚠️ Advertencia:** `kill -9` y `Stop-Process -Force` finalizan el proceso inmediatamente, sin permitir que cierre archivos o guarde información. Utilízalos únicamente cuando el proceso no pueda finalizarse de forma normal.

---

[⬆️ Volver al índice](#índice)

## Iniciar un proceso

### Linux

```bash
<comando>
```

También puede utilizarse:

```bash
nohup <comando> &
```

**Descripción**

Permite iniciar la ejecución de un programa o proceso.

- Ejecutando directamente el comando se inicia el proceso en primer plano.
- `nohup` permite que el proceso continúe ejecutándose incluso después de cerrar la sesión.
- El símbolo `&` inicia el proceso en segundo plano.

---

### PowerShell

```powershell
Start-Process <programa>
```

**Descripción**

Inicia un programa o aplicación desde PowerShell.

Puede utilizarse para abrir aplicaciones, documentos o ejecutar programas con diferentes parámetros.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Iniciar un proceso | `<comando>` | `Start-Process` |
| Iniciar un proceso en segundo plano | `nohup <comando> &` | `Start-Process` (según la aplicación) |

---

### Ejemplos

**Abrir un editor de texto**

Linux

```bash
nano
```

PowerShell

```powershell
Start-Process notepad
```

---

**Abrir el navegador web**

Linux

```bash
firefox
```

PowerShell

```powershell
Start-Process msedge
```

---

**Ejecutar un script en segundo plano**

Linux

```bash
nohup ./backup.sh &
```

PowerShell

```powershell
Start-Process powershell "-File C:\Scripts\backup.ps1"
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Los programas suelen iniciarse escribiendo directamente su nombre. | Se utiliza normalmente `Start-Process` para iniciar aplicaciones desde scripts. |
| `nohup` permite que el proceso continúe tras cerrar la sesión. | El proceso se ejecuta de forma independiente de la consola cuando la aplicación lo permite. |
| El operador `&` inicia el proceso en segundo plano. | Para trabajos en segundo plano suele utilizarse `Start-Job`, que se estudia en el siguiente apartado. |

---

### Buenas prácticas

- Comprueba que el programa existe antes de intentar ejecutarlo.
- Utiliza rutas completas cuando existan varias versiones del mismo programa.
- Ejecuta procesos en segundo plano únicamente cuando no requieran interacción del usuario.
- Supervisa los procesos iniciados para asegurarte de que funcionan correctamente.

---

### Comandos relacionados

- [Finalizar un proceso](#finalizar-un-proceso)
- [Finalizar un proceso por PID](#finalizar-un-proceso-por-pid)
- [Procesos en segundo plano](#procesos-en-segundo-plano)

---

[⬆️ Volver al índice](#índice)

## Procesos en segundo plano

### Linux

```bash
<comando> &
```

También pueden utilizarse:

```bash
jobs
```

```bash
bg
```

```bash
fg
```

**Descripción**

Linux permite ejecutar procesos en segundo plano para seguir utilizando la terminal mientras continúan ejecutándose.

- `&` inicia un proceso en segundo plano.
- `jobs` muestra los trabajos activos de la sesión.
- `bg` reanuda un trabajo suspendido en segundo plano.
- `fg` devuelve un trabajo al primer plano.

---

### PowerShell

```powershell
Start-Job -ScriptBlock { <comando> }
```

También pueden utilizarse:

```powershell
Get-Job
```

```powershell
Receive-Job
```

```powershell
Stop-Job
```

```powershell
Remove-Job
```

**Descripción**

PowerShell permite ejecutar tareas en segundo plano mediante **Jobs**.

Los trabajos continúan ejecutándose mientras la sesión permanezca abierta y pueden consultarse, detenerse o eliminarse posteriormente.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ejecutar en segundo plano | `&` | `Start-Job` |
| Mostrar trabajos | `jobs` | `Get-Job` |
| Recuperar salida | No es necesario | `Receive-Job` |
| Detener trabajo | `kill` | `Stop-Job` |
| Eliminar trabajo | Finaliza automáticamente | `Remove-Job` |

---

### Ejemplos

**Ejecutar un script en segundo plano**

Linux

```bash
./backup.sh &
```

PowerShell

```powershell
Start-Job -ScriptBlock {
    C:\Scripts\backup.ps1
}
```

---

**Mostrar los trabajos activos**

Linux

```bash
jobs
```

PowerShell

```powershell
Get-Job
```

---

**Volver a llevar un trabajo al primer plano**

Linux

```bash
fg
```

PowerShell

No existe un equivalente directo.

La salida del trabajo puede consultarse mediante:

```powershell
Receive-Job
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Los procesos pueden enviarse fácilmente al segundo plano con `&`. | Los trabajos se crean mediante `Start-Job`. |
| `bg` y `fg` permiten mover procesos entre primer y segundo plano. | No existe un equivalente directo a `fg` o `bg`. |
| `jobs` muestra los trabajos activos de la sesión. | `Get-Job` muestra los trabajos creados con `Start-Job`. |

---

### Buenas prácticas

- Utiliza procesos en segundo plano para tareas largas que no requieran interacción.
- Comprueba periódicamente el estado de los trabajos en ejecución.
- Elimina los trabajos finalizados para mantener la sesión organizada.
- Evita ejecutar un gran número de procesos en segundo plano simultáneamente si el equipo dispone de pocos recursos.

---

### Comandos relacionados

- [Iniciar un proceso](#iniciar-un-proceso)
- [Finalizar un proceso](#finalizar-un-proceso)
- [Resumen de equivalencias](#resumen-de-equivalencias)

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|--------|--------|------------|
| Listar procesos | `ps` / `ps aux` | `Get-Process` |
| Buscar un proceso | `ps aux \| grep` | `Get-Process` / `Where-Object` |
| Mostrar consumo de recursos | `top` / `htop` | `Get-Process` |
| Ordenar procesos | `ps aux --sort` | `Sort-Object` |
| Finalizar un proceso | `killall` | `Stop-Process -Name` |
| Finalizar un proceso por PID | `kill` | `Stop-Process -Id` |
| Forzar la finalización | `kill -9` | `Stop-Process -Force` |
| Iniciar un proceso | `<comando>` | `Start-Process` |
| Ejecutar procesos en segundo plano | `&`, `jobs`, `bg`, `fg` | `Start-Job`, `Get-Job` |

---

### Buenas prácticas generales

- Identifica siempre el proceso antes de finalizarlo.
- Supervisa periódicamente el consumo de CPU y memoria para detectar posibles problemas de rendimiento.
- Evita finalizar procesos críticos del sistema operativo.
- Utiliza procesos o trabajos en segundo plano únicamente cuando sea necesario.
- Finaliza primero un proceso de forma normal antes de recurrir a un cierre forzado.
- Filtra y ordena los procesos para localizar rápidamente la información que necesitas.

---

### Comandos más utilizados

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver todos los procesos | `ps aux` | `Get-Process` |
| Buscar un proceso | `ps aux \| grep chrome` | `Get-Process chrome` |
| Ver procesos que más CPU consumen | `ps aux --sort=-%cpu` | `Get-Process \| Sort-Object CPU -Descending` |
| Ver procesos que más memoria consumen | `ps aux --sort=-%mem` | `Get-Process \| Sort-Object WorkingSet -Descending` |
| Finalizar un proceso | `kill <PID>` | `Stop-Process -Id <PID>` |
| Forzar un proceso | `kill -9 <PID>` | `Stop-Process -Id <PID> -Force` |

---

[⬆️ Volver al índice](#índice)