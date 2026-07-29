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

### Linux

```bash
<comando> > <archivo>
```

**Descripción**

Redirige la salida estándar de un comando a un archivo. Si el archivo ya existe, su contenido será reemplazado.

---

### PowerShell

```powershell
<comando> > <archivo>
```

También puede utilizarse:

```powershell
<comando> | Out-File <archivo>
```

**Descripción**

Redirige la salida de un comando a un archivo. Si el archivo ya existe, será sobrescrito.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Redirigir la salida a un archivo | `>` | `>` / `Out-File` |

---

### Ejemplos

**Guardar el listado de archivos de un directorio**

Linux

```bash
ls > archivos.txt
```

PowerShell

```powershell
Get-ChildItem > archivos.txt
```

---

**Guardar la lista de procesos**

Linux

```bash
ps aux > procesos.txt
```

PowerShell

```powershell
Get-Process > procesos.txt
```

---

**Guardar la configuración de red**

Linux

```bash
ip addr > red.txt
```

PowerShell

```powershell
Get-NetIPAddress > red.txt
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `>` redirige la salida estándar a un archivo. | `>` también redirige la salida, aunque internamente utiliza el pipeline de PowerShell. |
| Si el archivo existe, se sobrescribe. | Si el archivo existe, también se sobrescribe. |
| Es habitual combinar `>` con otros comandos mediante tuberías. | También puede utilizarse `Out-File`, que ofrece opciones adicionales como codificación o ancho de línea. |

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

### Linux

```bash
<comando> >> <archivo>
```

**Descripción**

Añade la salida de un comando al final de un archivo. Si el archivo no existe, se crea automáticamente.

---

### PowerShell

```powershell
<comando> >> <archivo>
```

También puede utilizarse:

```powershell
<comando> | Add-Content <archivo>
```

**Descripción**

Añade la salida de un comando al final de un archivo sin eliminar el contenido existente.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Añadir información a un archivo | `>>` | `>>` / `Add-Content` |

---

### Ejemplos

**Añadir el listado de archivos a un informe**

Linux

```bash
ls >> informe.txt
```

PowerShell

```powershell
Get-ChildItem >> informe.txt
```

---

**Añadir la lista de procesos**

Linux

```bash
ps aux >> informe.txt
```

PowerShell

```powershell
Get-Process >> informe.txt
```

---

**Añadir la configuración de red**

Linux

```bash
ip addr >> informe.txt
```

PowerShell

```powershell
Get-NetIPAddress >> informe.txt
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `>>` añade la salida al final del archivo. | `>>` también añade la salida sin sobrescribir el contenido existente. |
| Si el archivo no existe, se crea automáticamente. | También crea el archivo si no existe. |
| Es habitual utilizar `>>` para generar informes de forma progresiva. | Puede utilizarse `Add-Content` cuando se desee añadir contenido de forma explícita. |

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

### Linux

```bash
<comando> 2> <archivo>
```

**Descripción**

Redirige la salida de error estándar (**stderr**) a un archivo. Los mensajes de error no se mostrarán por pantalla.

---

### PowerShell

```powershell
<comando> 2> <archivo>
```

**Descripción**

Redirige la salida de error de un cmdlet o comando a un archivo.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Redirigir errores | `2>` | `2>` |

---

### Ejemplos

**Guardar los errores al listar un directorio inexistente**

Linux

```bash
ls /directorio_inexistente 2> errores.txt
```

PowerShell

```powershell
Get-ChildItem C:\DirectorioInexistente 2> errores.txt
```

---

**Guardar los errores al eliminar un archivo inexistente**

Linux

```bash
rm archivo.txt 2> errores.txt
```

PowerShell

```powershell
Remove-Item archivo.txt 2> errores.txt
```

---

**Guardar únicamente los errores de un comando de red**

Linux

```bash
ping servidor_inexistente 2> errores.txt
```

PowerShell

```powershell
Test-Connection servidor_inexistente 2> errores.txt
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `2>` redirige únicamente la salida de error estándar (`stderr`). | `2>` redirige el flujo de errores al archivo indicado. |
| La salida correcta continúa mostrándose por pantalla. | La salida correcta también continúa mostrándose por pantalla. |
| Puede combinarse con `>` para separar la salida correcta de los errores. | También puede combinarse con `>` para almacenar ambos flujos por separado. |

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

### Linux

```bash
<comando1> | <comando2>
```

**Descripción**

Envía la salida de un comando como entrada del siguiente. En Linux, las tuberías transmiten **texto** entre comandos.

---

### PowerShell

```powershell
<cmdlet1> | <cmdlet2>
```

**Descripción**

Envía la salida de un cmdlet como entrada del siguiente. En PowerShell, las tuberías transmiten **objetos**, permitiendo acceder a sus propiedades y métodos.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Utilizar tuberías | `|` | `|` |

---

### Ejemplos

**Buscar un proceso**

Linux

```bash
ps aux | grep ssh
```

PowerShell

```powershell
Get-Process | Where-Object {$_.ProcessName -like "*ssh*"}
```

---

**Buscar archivos de texto**

Linux

```bash
ls | grep ".txt"
```

PowerShell

```powershell
Get-ChildItem | Where-Object {$_.Extension -eq ".txt"}
```

---

**Mostrar únicamente los servicios en ejecución**

Linux

```bash
systemctl list-units | grep running
```

PowerShell

```powershell
Get-Service | Where-Object {$_.Status -eq "Running"}
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Las tuberías transmiten texto entre comandos. | Las tuberías transmiten objetos completos entre cmdlets. |
| Es habitual combinar comandos como `grep`, `sort` o `wc`. | Es habitual combinar cmdlets como `Where-Object`, `Sort-Object` o `Measure-Object`. |
| Cada comando interpreta el texto recibido. | Cada cmdlet trabaja directamente con las propiedades del objeto recibido. |

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

### Linux

```bash
<comando> | grep "<texto>"
```

**Descripción**

Filtra la salida de un comando mostrando únicamente las líneas que contienen el texto especificado.

---

### PowerShell

```powershell
<cmdlet> | Where-Object {<condición>}
```

También puede utilizarse:

```powershell
<cmdlet> | Select-String "<texto>"
```

**Descripción**

Filtra los resultados de un cmdlet utilizando una condición o buscando una cadena de texto.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Filtrar resultados | `grep` | `Where-Object` / `Select-String` |

---

### Ejemplos

**Mostrar únicamente los procesos relacionados con SSH**

Linux

```bash
ps aux | grep ssh
```

PowerShell

```powershell
Get-Process | Where-Object {$_.ProcessName -like "*ssh*"}
```

---

**Mostrar únicamente los archivos PDF**

Linux

```bash
ls | grep ".pdf"
```

PowerShell

```powershell
Get-ChildItem | Where-Object {$_.Extension -eq ".pdf"}
```

---

**Mostrar únicamente los servicios en ejecución**

Linux

```bash
systemctl list-units | grep running
```

PowerShell

```powershell
Get-Service | Where-Object {$_.Status -eq "Running"}
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `grep` filtra texto plano. | `Where-Object` filtra objetos utilizando sus propiedades. |
| El criterio de búsqueda suele ser una cadena de texto o una expresión regular. | El criterio puede ser cualquier condición lógica (`-eq`, `-gt`, `-like`, etc.). |
| La salida continúa siendo texto. | La salida sigue siendo una colección de objetos. |

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

### Linux

```bash
<comando> | sort
```

**Descripción**

Ordena alfabéticamente la salida de un comando.

---

### PowerShell

```powershell
<cmdlet> | Sort-Object
```

**Descripción**

Ordena los resultados de un cmdlet. Permite ordenar tanto por el valor completo como por una propiedad específica del objeto.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ordenar resultados | `sort` | `Sort-Object` |

---

### Ejemplos

**Ordenar un listado de archivos**

Linux

```bash
ls | sort
```

PowerShell

```powershell
Get-ChildItem | Sort-Object Name
```

---

**Ordenar usuarios alfabéticamente**

Linux

```bash
cat usuarios.txt | sort
```

PowerShell

```powershell
Get-Content usuarios.txt | Sort-Object
```

---

**Ordenar procesos por consumo de memoria**

Linux

```bash
ps aux | sort -k4 -n
```

PowerShell

```powershell
Get-Process | Sort-Object WorkingSet -Descending
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `sort` ordena texto plano. | `Sort-Object` ordena objetos completos. |
| El orden se realiza sobre líneas de texto. | Puede ordenarse por cualquier propiedad del objeto (`Name`, `CPU`, `WorkingSet`, etc.). |
| Para ordenaciones complejas es necesario indicar la columna correspondiente. | Basta con indicar el nombre de la propiedad que se desea ordenar. |

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

### Linux

```bash
<comando> | wc -l
```

**Descripción**

Cuenta el número de líneas generadas por un comando. Es muy utilizado para conocer la cantidad de archivos, procesos, usuarios o cualquier otro elemento devuelto por una tubería.

---

### PowerShell

```powershell
<cmdlet> | Measure-Object
```

También puede utilizarse:

```powershell
(<cmdlet>).Count
```

**Descripción**

Cuenta el número de objetos devueltos por un cmdlet.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Contar resultados | `wc -l` | `Measure-Object` / `.Count` |

---

### Ejemplos

**Contar el número de archivos de un directorio**

Linux

```bash
ls | wc -l
```

PowerShell

```powershell
Get-ChildItem | Measure-Object
```

---

**Contar los procesos en ejecución**

Linux

```bash
ps aux | wc -l
```

PowerShell

```powershell
Get-Process | Measure-Object
```

---

**Contar los servicios en ejecución**

Linux

```bash
systemctl list-units --type=service --state=running | wc -l
```

PowerShell

```powershell
Get-Service |
Where-Object {$_.Status -eq "Running"} |
Measure-Object
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `wc -l` cuenta líneas de texto. | `Measure-Object` cuenta objetos. |
| El resultado depende del número de líneas recibidas por la tubería. | El resultado depende del número de objetos recibidos. |
| Devuelve directamente un número. | Devuelve un objeto con varias propiedades, siendo `Count` la más utilizada. |

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

### Linux

```bash
variable=$(<comando1> | <comando2>)
```

**Descripción**

Guarda el resultado de una tubería dentro de una variable para reutilizarlo posteriormente en el mismo script o sesión.

---

### PowerShell

```powershell
$variable = <cmdlet1> | <cmdlet2>
```

**Descripción**

Guarda el resultado de una tubería en una variable. En PowerShell, la variable almacena los objetos generados por la tubería.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Guardar el resultado de una tubería | `variable=$(...)` | `$variable = ...` |

---

### Ejemplos

**Guardar el número de archivos de un directorio**

Linux

```bash
total=$(ls | wc -l)
```

PowerShell

```powershell
$total = Get-ChildItem | Measure-Object
```

---

**Guardar los procesos relacionados con PowerShell**

Linux

```bash
procesos=$(ps aux | grep powershell)
```

PowerShell

```powershell
$procesos = Get-Process |
Where-Object {$_.ProcessName -like "*powershell*"}
```

---

**Guardar los servicios en ejecución**

Linux

```bash
servicios=$(systemctl list-units --type=service --state=running)
```

PowerShell

```powershell
$servicios = Get-Service |
Where-Object {$_.Status -eq "Running"}
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| La variable almacena el texto generado por la tubería. | La variable almacena los objetos generados por la tubería. |
| Se utiliza la sustitución de comandos `$( )`. | Basta con asignar la salida de la tubería a una variable. |
| El contenido suele procesarse posteriormente como texto. | Posteriormente pueden utilizarse directamente las propiedades y métodos de los objetos almacenados. |

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