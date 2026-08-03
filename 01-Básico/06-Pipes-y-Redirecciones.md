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
- [Resumen de equivalencias](#resumen-de-equivalencias)

---

## Redirigir la salida a un archivo

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `<comando> > <archivo>` | `<comando> > <archivo>` |
| **Ejemplo** | `ps aux > procesos.txt` | `Get-Process > procesos.txt` |

> 💡 **Diferencia clave** — 🐧 `>` redirige la salida estándar a un archivo. · 🪟 `>` también redirige la salida, aunque internamente utiliza el pipeline de PowerShell.

---

### Buenas prácticas

- Comprueba si el archivo existe antes de sobrescribirlo.
- Utiliza nombres descriptivos para los archivos generados.
- Guarda los informes en una carpeta específica para facilitar su organización.
- Si deseas conservar el contenido existente, utiliza la redirección de anexado (`>>`).

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

### Buenas prácticas

- Utiliza `>>` cuando quieras conservar el contenido existente del archivo.
- Emplea archivos de registro (logs) o informes para recopilar información de varios comandos.
- Comprueba periódicamente el tamaño de los archivos que reciben información de forma continua.

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

### Buenas prácticas

- Guarda los errores en un archivo cuando ejecutes scripts o tareas largas.
- Revisa siempre el contenido del archivo de errores para detectar posibles incidencias.
- Utiliza nombres descriptivos como `errores.log` o `error.txt`.
- Si necesitas registrar tanto la salida correcta como los errores, utiliza archivos diferentes para facilitar el análisis.

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

### Buenas prácticas

- Divide las tareas complejas en varias tuberías sencillas.
- Utiliza tuberías para evitar crear archivos temporales innecesarios.
- Aprovecha el procesamiento de objetos en PowerShell para acceder directamente a las propiedades de cada elemento.
- Encadena únicamente los comandos necesarios para mantener los scripts legibles.

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

### Buenas prácticas

- Utiliza filtros lo más específicos posible para reducir el número de resultados.
- En PowerShell, utiliza `Where-Object` cuando necesites trabajar con propiedades de los objetos.
- Utiliza `Select-String` cuando únicamente necesites buscar texto dentro de la salida.
- Combina los filtros con tuberías para construir comandos más potentes.

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

### Buenas prácticas

- Ordena los resultados antes de analizarlos cuando trabajes con grandes cantidades de información.
- En PowerShell, utiliza siempre la propiedad más adecuada para obtener un orden correcto.
- Combina `Sort-Object` con `Where-Object` para obtener listados claros y fáciles de interpretar.
- Utiliza `-Descending` cuando necesites mostrar primero los valores más altos.

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

### Buenas prácticas

- Filtra los resultados antes de contarlos para obtener información más precisa.
- Utiliza `Measure-Object` cuando trabajes con objetos en PowerShell.
- En Linux, combina `grep` y `wc -l` para contar únicamente los resultados que cumplan una condición.

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

### Buenas prácticas

- Guarda únicamente los resultados que vayas a reutilizar.
- Utiliza nombres descriptivos para las variables.
- Comprueba el contenido de la variable antes de utilizarla en operaciones críticas.
- Si el resultado contiene muchos elementos, considera filtrarlo antes de almacenarlo.

---

### Comandos relacionados

- [Utilizar tuberías (Pipes)](#utilizar-tuberías-pipes)
- [Filtrar resultados](#filtrar-resultados)
- [Contar resultados](#contar-resultados)

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|--------|--------|------------|
| Redirigir la salida a un archivo | `>` | `>` / `Out-File` |
| Añadir información a un archivo | `>>` | `>>` / `Add-Content` |
| Redirigir errores | `2>` | `2>` |
| Utilizar tuberías | `|` | `|` |
| Filtrar resultados | `grep` | `Where-Object` / `Select-String` |
| Ordenar resultados | `sort` | `Sort-Object` |
| Contar resultados | `wc -l` | `Measure-Object` / `.Count` |
| Guardar el resultado de una tubería | `variable=$(...)` | `$variable = ...` |

---

### Buenas prácticas generales

- Utiliza tuberías para combinar comandos en lugar de ejecutar varios procesos independientes.
- Filtra los resultados antes de ordenarlos o contarlos para mejorar el rendimiento.
- Redirige la salida a archivos cuando necesites generar informes o conservar información.
- Guarda el resultado de las tuberías en variables cuando vayas a reutilizarlo posteriormente.
- En PowerShell, recuerda que las tuberías trabajan con **objetos**, mientras que en Linux trabajan con **texto**.
- Mantén las tuberías simples y legibles; si una línea resulta demasiado larga, considera dividir el proceso en varias variables.

---

[⬆️ Volver al índice](#índice)