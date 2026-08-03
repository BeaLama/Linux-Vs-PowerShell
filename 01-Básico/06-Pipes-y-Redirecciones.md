# Pipes y redirecciones

## Introducción

Las tuberías y las redirecciones permiten combinar comandos, reutilizar resultados y guardar información en archivos.

En Linux, las tuberías transmiten texto entre comandos, mientras que en PowerShell transmiten objetos completos, proporcionando una forma mucho más potente de procesar información.

Aprender a utilizar correctamente estas herramientas permite automatizar tareas, generar informes y crear scripts más eficientes.

---

## Índice

- [Redirigir la salida a un archivo](#redirigir-la-salida-a-un-archivo)
- [Añadir información a un archivo](#añadir-información-a-un-archivo)
- [Redirigir errores](#redirigir-errores)
- [Utilizar tuberías (Pipes)](#utilizar-tuberías-pipes)
- [Filtrar resultados](#filtrar-resultados)
- [Ordenar resultados](#ordenar-resultados)
- [Contar resultados](#contar-resultados)
- [Guardar el resultado de una tubería](#guardar-el-resultado-de-una-tubería)

---

## Redirigir la salida a un archivo

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `<comando> > <archivo>` | `<comando> > <archivo>` |
| **Ejemplo** | `ps aux > procesos.txt` | `Get-Process > procesos.txt` |

> 💡 **Diferencia clave** — 🐧 `>` redirige la salida estándar a un archivo. · 🪟 `>` también redirige la salida, aunque internamente utiliza el pipeline de PowerShell.

---


### Comandos relacionados

- [Añadir información a un archivo](#añadir-información-a-un-archivo)
- [Redirigir errores](#redirigir-errores)
- [Utilizar tuberías (Pipes)](#utilizar-tuberías-pipes)

---

[⬆️ Volver al índice](#índice)

## Añadir información a un archivo

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `<comando> > <archivo>` | `<comando> > <archivo>` |
| **Ejemplo** | `ps aux > procesos.txt` | `Get-Process > procesos.txt` |

> 💡 **Diferencia clave** — 🐧 `>` redirige la salida estándar a un archivo. · 🪟 `>` también redirige la salida, aunque internamente utiliza el pipeline de PowerShell.

---

### Comandos relacionados

- [Redirigir la salida a un archivo](#redirigir-la-salida-a-un-archivo)
- [Redirigir errores](#redirigir-errores)
- [Guardar el resultado de una tubería](#guardar-el-resultado-de-una-tubería)

---

[⬆️ Volver al índice](#índice)

## Redirigir errores

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `<comando> 2> <archivo>` | `<comando> 2> <archivo>` |
| **Ejemplo** | `rm archivo.txt 2> errores.txt` | `Remove-Item archivo.txt 2> errores.txt` |

> 💡 **Diferencia clave** — 🐧 `2>` redirige únicamente la salida de error estándar (`stderr`). · 🪟 `2>` redirige el flujo de errores al archivo indicado.

---

### Comandos relacionados

- [Redirigir la salida a un archivo](#redirigir-la-salida-a-un-archivo)
- [Añadir información a un archivo](#añadir-información-a-un-archivo)
- [Utilizar tuberías (Pipes)](#utilizar-tuberías-pipes)

---

[⬆️ Volver al índice](#índice)

## Utilizar tuberías (Pipes)

**Sintaxis**
```bash
<comando1> | <comando2>
```
```powershell
<cmdlet1> | <cmdlet2>
```

> 💡 **Diferencia clave** — 🐧 Las tuberías transmiten texto entre comandos. · 🪟 Las tuberías transmiten objetos completos entre cmdlets.

---

### Comandos relacionados

- [Filtrar resultados](#filtrar-resultados)
- [Ordenar resultados](#ordenar-resultados)
- [Guardar el resultado de una tubería](#guardar-el-resultado-de-una-tubería)

---

[⬆️ Volver al índice](#índice)

## Filtrar resultados

**Sintaxis**
```bash
<comando> | grep "<texto>"
```
```powershell
<cmdlet> | Where-Object {<condición>}
```

> 💡 **Diferencia clave** — 🐧 `grep` filtra texto plano. · 🪟 `Where-Object` filtra objetos utilizando sus propiedades.

---

### Comandos relacionados

- [Utilizar tuberías (Pipes)](#utilizar-tuberías-pipes)
- [Ordenar resultados](#ordenar-resultados)
- [Contar resultados](#contar-resultados)

---

[⬆️ Volver al índice](#índice)

## Ordenar resultados

**Sintaxis**
```bash
<comando> | sort
```
```powershell
<cmdlet> | Sort-Object
```

> 💡 **Diferencia clave** — 🐧 `sort` ordena texto plano. · 🪟 `Sort-Object` ordena objetos completos.

---

### Comandos relacionados

- [Utilizar tuberías (Pipes)](#utilizar-tuberías-pipes)
- [Filtrar resultados](#filtrar-resultados)
- [Contar resultados](#contar-resultados)

---

[⬆️ Volver al índice](#índice)

## Contar resultados

**Sintaxis**
```bash
<comando> | wc -l
```
```powershell
<cmdlet> | Measure-Object
```

> 💡 **Diferencia clave** — 🐧 `wc -l` cuenta líneas de texto. · 🪟 `Measure-Object` cuenta objetos.

---

### Comandos relacionados

- [Utilizar tuberías (Pipes)](#utilizar-tuberías-pipes)
- [Filtrar resultados](#filtrar-resultados)
- [Ordenar resultados](#ordenar-resultados)

---

[⬆️ Volver al índice](#índice)

## Guardar el resultado de una tubería

**Sintaxis**
```bash
variable=$(<comando1> | <comando2>)
```
```powershell
$variable = <cmdlet1> | <cmdlet2>
```

> 💡 **Diferencia clave** — 🐧 La variable almacena el texto generado por la tubería. · 🪟 La variable almacena los objetos generados por la tubería.

---

### Comandos relacionados

- [Utilizar tuberías (Pipes)](#utilizar-tuberías-pipes)
- [Filtrar resultados](#filtrar-resultados)
- [Contar resultados](#contar-resultados)

---

[⬆️ Volver al índice](#índice)