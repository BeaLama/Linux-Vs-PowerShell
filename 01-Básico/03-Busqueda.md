# Búsqueda

## Introducción

Localizar archivos, directorios o información específica es una de las tareas más habituales tanto en Linux como en Windows.

Mientras que Linux utiliza principalmente herramientas como `find` y `grep`, PowerShell dispone de cmdlets como `Get-ChildItem` y `Select-String`, capaces de realizar búsquedas muy precisas gracias al uso de objetos.

---

## Índice

- [Buscar archivos por nombre](#buscar-archivos-por-nombre)
- [Buscar directorios](#buscar-directorios)
- [Buscar por extensión](#buscar-por-extensión)
- [Buscar texto dentro de archivos](#buscar-texto-dentro-de-archivos)
- [Buscar de forma recursiva](#buscar-de-forma-recursiva)
- [Buscar archivos modificados recientemente](#buscar-archivos-modificados-recientemente)
- [Buscar archivos por tamaño](#buscar-archivos-por-tamaño)
- [Buscar archivos vacíos](#buscar-archivos-vacíos)
- [Buscar archivos ocultos](#buscar-archivos-ocultos)

---

## Buscar archivos por nombre

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `find <ruta> -name "<nombre_archivo>"` | `Get-ChildItem -Path <ruta> -Filter "<nombre_archivo>" -File -Recurse` |

**Ejemplo**
```bash
find /home/usuario/Documentos -name "informe.txt"
```
```powershell
Get-ChildItem -Path C:\Users\usuario\Documents -Filter "informe.txt" -File -Recurse
```

> 💡 **Diferencia clave** — 🐧 `find` busca tanto archivos como directorios; el comportamiento depende de los parámetros utilizados. · 🪟 `-File` limita la búsqueda únicamente a archivos.

---

### Comandos relacionados

- [Buscar directorios](#buscar-directorios)
- [Buscar por extensión](#buscar-por-extensión)
- [Buscar de forma recursiva](#buscar-de-forma-recursiva)

---

[⬆️ Volver al índice](#índice)

## Buscar directorios

**Sintaxis**
```bash
find <ruta> -type d -name "<nombre_directorio>"
```
```powershell
Get-ChildItem -Path <ruta> -Directory -Filter "<nombre_directorio>" -Recurse
```

> 💡 **Diferencia clave** — 🐧 `-type d` limita la búsqueda únicamente a directorios. · 🪟 `-Directory` devuelve exclusivamente directorios.

---


### Comandos relacionados

- [Buscar archivos por nombre](#buscar-archivos-por-nombre)
- [Buscar por extensión](#buscar-por-extensión)
- [Buscar de forma recursiva](#buscar-de-forma-recursiva)

---

[⬆️ Volver al índice](#índice)

## Buscar por extensión

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `find <ruta> -name "*.extensión"` | `Get-ChildItem -Path <ruta> -Filter "*.extensión" -File -Recurse` |

**Ejemplo**
```bash
find /home/usuario/Documentos -name "*.pdf"
```
```powershell
Get-ChildItem -Path C:\Users\usuario\Documents -Filter "*.pdf" -File -Recurse
```

> 💡 **Diferencia clave** — 🐧 La búsqueda se realiza mediante `find` utilizando el parámetro `-name`. · 🪟 Se utiliza `Get-ChildItem` junto con `-Filter`, lo que mejora el rendimiento.

---

### Buenas prácticas

- Utiliza `-Filter` en PowerShell siempre que sea posible para obtener un mejor rendimiento.
- Limita la búsqueda a la carpeta necesaria para reducir el tiempo de ejecución.
- Utiliza extensiones específicas cuando conozcas el tipo de archivo que deseas localizar.

---

### Comandos relacionados

- [Buscar archivos por nombre](#buscar-archivos-por-nombre)
- [Buscar directorios](#buscar-directorios)
- [Buscar texto dentro de archivos](#buscar-texto-dentro-de-archivos)

---

[⬆️ Volver al índice](#índice)

## Buscar texto dentro de archivos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `grep "<texto>" <archivo>` | `Select-String -Path <archivo> -Pattern "<texto>"` |
| **Ejemplo** | `grep "ERROR" *.log` | `Select-String -Path *.log -Pattern "ERROR"` |

> 💡 **Diferencia clave** — 🐧 `grep` busca texto plano dentro de archivos. · 🪟 `Select-String` utiliza expresiones regulares por defecto y devuelve objetos con información de la coincidencia.ormación como el archivo, el número de línea y el texto encontrado. |

---

### Comandos relacionados

- [Buscar archivos por nombre](#buscar-archivos-por-nombre)
- [Buscar por extensión](#buscar-por-extensión)
- [Buscar de forma recursiva](#buscar-de-forma-recursiva)

---

[⬆️ Volver al índice](#índice)

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `find <ruta> <criterios>` | `Get-ChildItem -Path <ruta> -Recurse` |

**Ejemplo**
```bash
grep -r "ERROR" .
```
```powershell
Get-ChildItem -Path . -Filter *.txt -Recurse |
Select-String -Pattern "ERROR"
```

> 💡 **Diferencia clave** — 🐧 `find` realiza búsquedas recursivas por defecto. · 🪟 La búsqueda recursiva requiere el parámetro `-Recurse`.

---

### Comandos relacionados

- [Buscar archivos por nombre](#buscar-archivos-por-nombre)
- [Buscar texto dentro de archivos](#buscar-texto-dentro-de-archivos)
- [Buscar por extensión](#buscar-por-extensión)

---

[⬆️ Volver al índice](#índice)

## Buscar archivos modificados recientemente

**Sintaxis**
```bash
find <ruta> -mtime <días>
```
```powershell
Get-ChildItem -Path <ruta> -File -Recurse |
Where-Object {$_.LastWriteTime -gt (Get-Date).AddDays(<días>)}
```

> 💡 **Diferencia clave** — 🐧 `-mtime` trabaja con días completos desde la última modificación. · 🪟 Se compara la propiedad `LastWriteTime` con una fecha calculada mediante `Get-Date`.

---

### Comandos relacionados

- [Buscar archivos por nombre](#buscar-archivos-por-nombre)
- [Buscar por extensión](#buscar-por-extensión)
- [Buscar archivos por tamaño](#buscar-archivos-por-tamaño)

---

[⬆️ Volver al índice](#índice)

## Buscar archivos por tamaño

**Sintaxis**
```bash
find <ruta> -size <tamaño>
```
```powershell
Get-ChildItem -Path <ruta> -File -Recurse |
Where-Object {$_.Length <operador> <tamaño>}
```

> 💡 **Diferencia clave** — 🐧 `find` utiliza el parámetro `-size` junto con unidades como `k`, `M` o `G`. · 🪟 PowerShell compara el tamaño mediante la propiedad `Length`.

---

### Comandos relacionados

- [Buscar por extensión](#buscar-por-extensión)
- [Buscar archivos modificados recientemente](#buscar-archivos-modificados-recientemente)
- [Buscar archivos vacíos](#buscar-archivos-vacíos)

---

[⬆️ Volver al índice](#índice)

## Buscar archivos vacíos

**Sintaxis**
```bash
find <ruta> -type f -empty
```
```powershell
Get-ChildItem -Path <ruta> -File -Recurse |
Where-Object {$_.Length -eq 0}
```

> 💡 **Diferencia clave** — 🐧 `-empty` permite localizar archivos y directorios vacíos. · 🪟 Se utiliza la propiedad `Length` para comprobar el tamaño del archivo.

---

### Comandos relacionados

- [Buscar archivos por tamaño](#buscar-archivos-por-tamaño)
- [Buscar por extensión](#buscar-por-extensión)
- [Buscar archivos modificados recientemente](#buscar-archivos-modificados-recientemente)

---

[⬆️ Volver al índice](#índice)

## Buscar archivos ocultos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `find <ruta> -name ".*"` | `Get-ChildItem -Path <ruta> -File -Force -Recurse` |

**Ejemplo**
```bash
find /home/usuario -type f -name ".*"
```
```powershell
Get-ChildItem -Path C:\Users\usuario -File -Force -Recurse |
Where-Object {$_.Attributes -match "Hidden"}
```

> 💡 **Diferencia clave** — 🐧 Los archivos ocultos se identifican porque su nombre comienza por un punto (`.`). · 🪟 Los archivos ocultos se identifican mediante el atributo `Hidden`.

---

### Comandos relacionados

- [Buscar archivos por nombre](#buscar-archivos-por-nombre)
- [Buscar directorios](#buscar-directorios)
- [Buscar archivos vacíos](#buscar-archivos-vacíos)

---

[⬆️ Volver al índice](#índice)
