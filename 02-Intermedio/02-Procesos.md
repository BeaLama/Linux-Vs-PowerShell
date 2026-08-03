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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `ps` | `Get-Process` |
| **Ejemplo** | `ps` | `Get-Process -IncludeUserName` |

> 💡 **Diferencia clave** — 🐧 `ps` muestra únicamente los procesos de la sesión actual. · 🪟 `Get-Process` muestra todos los procesos del sistema de forma predeterminada.

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

**Sintaxis**
```bash
ps aux | grep <proceso>
```
```powershell
Get-Process <proceso>
```

> 💡 **Diferencia clave** — 🐧 Utiliza `grep` para filtrar texto. · 🪟 Puede buscar directamente por nombre mediante `Get-Process`.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `top` | `Get-Process` |

**Ejemplo**
```bash
top
```
```powershell
Get-Process |
Sort-Object CPU -Descending
```

> 💡 **Diferencia clave** — 🐧 `top` actualiza la información en tiempo real. · 🪟 `Get-Process` muestra una instantánea del estado actual.

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

**Sintaxis**
```bash
ps aux --sort=<criterio>
```
```powershell
Get-Process | Sort-Object <propiedad>
```

> 💡 **Diferencia clave** — 🐧 `ps aux --sort` ordena la salida según el criterio indicado. · 🪟 `Sort-Object` ordena los objetos utilizando cualquiera de sus propiedades.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `kill <PID>` | `Stop-Process -Name <proceso>` |
| **Ejemplo** | `killall notepad` | `Stop-Process -Name notepad` |

> 💡 **Diferencia clave** — 🐧 `killall` finaliza todos los procesos con el nombre indicado. · 🪟 `Stop-Process -Name` también finaliza todos los procesos que coincidan con ese nombre.

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

[⬆️ Volver al índice](#índice)

## Finalizar un proceso por PID

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `kill <PID>` | `Stop-Process -Id <PID>` |
| **Ejemplo** | `kill -9 2548` | `Stop-Process -Id 2548 -Force` |

> 💡 **Diferencia clave** — 🐧 `kill` envía una señal al proceso. · 🪟 `Stop-Process` solicita al sistema operativo que finalice el proceso.

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

[⬆️ Volver al índice](#índice)

## Iniciar un proceso

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `<comando>` | `Start-Process <programa>` |
| **Ejemplo** | `firefox` | `Start-Process msedge` |

> 💡 **Diferencia clave** — 🐧 Los programas suelen iniciarse escribiendo directamente su nombre. · 🪟 Se utiliza normalmente `Start-Process` para iniciar aplicaciones desde scripts.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `<comando> &` | `Start-Job -ScriptBlock { <comando> }` |
| **Ejemplo** | `jobs` | `Get-Job` |

> 💡 **Diferencia clave** — 🐧 Los procesos pueden enviarse fácilmente al segundo plano con `&`. · 🪟 Los trabajos se crean mediante `Start-Job`.

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