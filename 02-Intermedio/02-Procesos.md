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

---

## Listar procesos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `ps` | `Get-Process` |
| **Ejemplo** | `ps` | `Get-Process -IncludeUserName` |

> 💡 **Diferencia clave** — 🐧 `ps` muestra únicamente los procesos de la sesión actual. · 🪟 `Get-Process` muestra todos los procesos del sistema de forma predeterminada.

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

### Comandos relacionados

- [Iniciar un proceso](#iniciar-un-proceso)
- [Finalizar un proceso](#finalizar-un-proceso)
- [Resumen de equivalencias](#resumen-de-equivalencias)

---

[⬆️ Volver al índice](#índice)