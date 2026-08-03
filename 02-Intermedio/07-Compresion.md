# Compresión y archivos

## Introducción

La compresión de archivos permite reducir el espacio ocupado por la información y facilitar su almacenamiento, transferencia y distribución.

Tanto Linux como Windows incorporan herramientas para crear, extraer y administrar archivos comprimidos utilizando distintos formatos como **ZIP**, **TAR**, **GZIP**, **BZIP2** o **XZ**.

---

## Índice

- [Comprimir archivos en ZIP](#comprimir-archivos-en-zip)
- [Extraer archivos ZIP](#extraer-archivos-zip)
- [Crear un archivo TAR](#crear-un-archivo-tar)
- [Extraer un archivo TAR](#extraer-un-archivo-tar)
- [Comprimir con GZIP](#comprimir-con-gzip)
- [Descomprimir archivos GZIP](#descomprimir-archivos-gzip)
- [Comprimir con BZIP2 y XZ](#comprimir-con-bzip2-y-xz)
- [Ver el contenido de un archivo comprimido](#ver-el-contenido-de-un-archivo-comprimido)
- [Resumen de equivalencias](#resumen-de-equivalencias)

---

## Comprimir archivos en ZIP

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `zip <archivo.zip> <archivo>` | `Compress-Archive` |

**Ejemplo**
```bash
zip -r copia.zip Documentos/
```
```powershell
Compress-Archive `
-Path ".\Documentos" `
-DestinationPath ".\copia.zip"
```

> 💡 **Diferencia clave** — 🐧 `zip` utiliza la opción `-r` para incluir directorios completos. · 🪟 `Compress-Archive` comprime archivos y carpetas mediante el parámetro `-Path`.

---

### Buenas prácticas

- Utiliza nombres descriptivos para los archivos comprimidos.
- Comprime directorios completos cuando necesites conservar su estructura.
- Comprueba el contenido del archivo ZIP antes de eliminar los archivos originales.
- Evita comprimir archivos ya comprimidos (como `.jpg`, `.mp4` o `.zip`), ya que normalmente apenas reducirán su tamaño.

---

### Comandos relacionados

- [Extraer archivos ZIP](#extraer-archivos-zip)
- [Crear un archivo TAR](#crear-un-archivo-tar)
- [Ver el contenido de un archivo comprimido](#ver-el-contenido-de-un-archivo-comprimido)

---

[⬆️ Volver al índice](#índice)

## Extraer archivos ZIP

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `unzip <archivo.zip>` | `Expand-Archive` |

**Ejemplo**
```bash
unzip copia.zip -d /home/usuario/Documentos
```
```powershell
Expand-Archive `
-Path ".\copia.zip" `
-DestinationPath "C:\Users\Usuario\Documentos"
```

> 💡 **Diferencia clave** — 🐧 `unzip` extrae el contenido en el directorio actual por defecto. · 🪟 Es recomendable indicar siempre el directorio mediante `-DestinationPath`.

---

### Buenas prácticas

- Extrae el contenido en un directorio específico para mantener los archivos organizados.
- Comprueba el contenido del archivo ZIP antes de sobrescribir archivos existentes.
- Verifica que dispones de espacio suficiente antes de descomprimir archivos grandes.
- Evita extraer archivos comprimidos de procedencia desconocida sin comprobar previamente su contenido.

---

### Comandos relacionados

- [Comprimir archivos en ZIP](#comprimir-archivos-en-zip)
- [Ver el contenido de un archivo comprimido](#ver-el-contenido-de-un-archivo-comprimido)
- [Crear un archivo TAR](#crear-un-archivo-tar)

---

[⬆️ Volver al índice](#índice)

## Crear un archivo TAR

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `tar -cvf <archivo.tar> <archivo_o_directorio>` | `tar -cvf` |
| **Ejemplo** | `tar -cvf copia.tar Documentos/` | `tar -cvf copia.tar Documentos` |

> 💡 **Diferencia clave** — 🐧 Utiliza GNU tar en la mayoría de distribuciones. · 🪟 Utiliza bsdtar incluido en Windows.

---

### Buenas prácticas

- Utiliza TAR cuando quieras agrupar múltiples archivos manteniendo su estructura de directorios.
- Si además deseas reducir el tamaño del archivo, combina TAR con GZIP, BZIP2 o XZ.
- Utiliza nombres descriptivos para identificar fácilmente el contenido del archivo TAR.
- Comprueba el contenido del archivo antes de eliminar los originales.

---

### Comandos relacionados

- [Extraer un archivo TAR](#extraer-un-archivo-tar)
- [Comprimir con GZIP](#comprimir-con-gzip)
- [Ver el contenido de un archivo comprimido](#ver-el-contenido-de-un-archivo-comprimido)

---

[⬆️ Volver al índice](#índice)

## Exrtaer un archivo TAR

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `tar -xvf <archivo.tar>` | `tar -xvf` |

**Ejemplo**
```bash
tar -xvf copia.tar -C /home/usuario/Documentos
```
```powershell
tar -xvf copia.tar `
-C C:\Users\Usuario\Documentos
```

> 💡 **Diferencia clave** — 🐧 GNU tar está presente en prácticamente todas las distribuciones. · 🪟 Windows utiliza bsdtar, pero la sintaxis es prácticamente idéntica.

---

### Buenas prácticas

- Extrae los archivos en un directorio específico para mantener el contenido organizado.
- Comprueba el contenido del archivo TAR antes de eliminar la copia original.
- Verifica que dispones de espacio suficiente antes de extraer archivos de gran tamaño.
- Si el archivo tiene extensión `.tar.gz`, `.tar.bz2` o `.tar.xz`, utiliza las opciones de extracción correspondientes.

---

### Comandos relacionados

- [Crear un archivo TAR](#crear-un-archivo-tar)
- [Comprimir con GZIP](#comprimir-con-gzip)
- [Ver el contenido de un archivo comprimido](#ver-el-contenido-de-un-archivo-comprimido)

---

[⬆️ Volver al índice](#índice)

## Comprimir con GZIP

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `gzip <archivo>` | `tar -czf` |
| **Ejemplo** | `tar -czf copia.tar.gz Documentos/` | `tar -czf copia.tar.gz Documentos` |

> 💡 **Diferencia clave** — 🐧 `gzip` puede comprimir directamente un archivo. · 🪟 Normalmente se utiliza `tar -czf` para generar archivos `.tar.gz`.

---

### Buenas prácticas

- Utiliza `gzip` para comprimir archivos individuales.
- Utiliza `tar -czf` cuando necesites conservar la estructura de un directorio completo.
- Añade la opción `-v` únicamente cuando quieras visualizar el progreso de la operación.
- Comprueba el tamaño del archivo generado antes de eliminar los originales.

---

### Comandos relacionados

- [Descomprimir archivos GZIP](#descomprimir-archivos-gzip)
- [Crear un archivo TAR](#crear-un-archivo-tar)
- [Extraer un archivo TAR](#extraer-un-archivo-tar)

---

[⬆️ Volver al índice](#índice)

## Descomprimir archivos GZIP

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `gunzip <archivo.gz>` | `tar -xzf` |
| **Ejemplo** | `tar -xzf copia.tar.gz` | `tar -xzf copia.tar.gz` |

> 💡 **Diferencia clave** — 🐧 `gunzip` descomprime archivos `.gz` individuales. · 🪟 Lo habitual es utilizar `tar -xzf` para archivos `.tar.gz`.

---

### Buenas prácticas

- Comprueba si el archivo es un `.gz` o un `.tar.gz` antes de descomprimirlo.
- Extrae el contenido en un directorio específico cuando trabajes con archivos grandes.
- Verifica que dispones de espacio suficiente antes de iniciar la extracción.
- Conserva el archivo comprimido original si se trata de una copia de seguridad.

---

### Comandos relacionados

- [Comprimir con GZIP](#comprimir-con-gzip)
- [Crear un archivo TAR](#crear-un-archivo-tar)
- [Extraer un archivo TAR](#extraer-un-archivo-tar)

---

[⬆️ Volver al índice](#índice)

## Comprimir con BZIP2 y XZ

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `bzip2 <archivo>` | `tar -cjf` |
| **Ejemplo** | `xz informe.log` | *(no aplica)* |

> 💡 **Diferencia clave** — 🐧 `bzip2` y `xz` pueden comprimir directamente archivos individuales. · 🪟 Lo habitual es utilizar `tar` con las opciones `-j` o `-J`.

---

### Buenas prácticas

- Utiliza **BZIP2** cuando busques una mejor compresión que GZIP y el tiempo de procesamiento no sea crítico.
- Utiliza **XZ** cuando el objetivo sea obtener el menor tamaño posible del archivo.
- Emplea **TAR** junto con BZIP2 o XZ para conservar la estructura de directorios.
- Comprueba siempre que el sistema de destino sea compatible con el formato utilizado antes de compartir el archivo.

---

### Comandos relacionados

- [Comprimir con GZIP](#comprimir-con-gzip)
- [Descomprimir archivos GZIP](#descomprimir-archivos-gzip)
- [Ver el contenido de un archivo comprimido](#ver-el-contenido-de-un-archivo-comprimido)

---

[⬆️ Volver al índice](#índice)

## Ver el contenido de un archivo comprimido

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `unzip -l <archivo.zip>` | `tar -tf` |
| **Ejemplo** | `tar -tf copia.tar` | `tar -tf copia.tar` |

> 💡 **Diferencia clave** — 🐧 `unzip -l` permite listar fácilmente el contenido de archivos ZIP. · 🪟 Windows no dispone de un cmdlet específico para listar ZIP desde PowerShell.

---

### Buenas prácticas

- Comprueba el contenido antes de extraer archivos comprimidos de origen desconocido.
- Verifica que la estructura del archivo es la esperada antes de restaurar una copia de seguridad.
- Utiliza esta comprobación para confirmar que el archivo comprimido no está dañado.
- Evita extraer archivos innecesarios cuando solo necesitas consultar su contenido.

---

### Comandos relacionados

- [Comprimir archivos en ZIP](#comprimir-archivos-en-zip)
- [Extraer archivos ZIP](#extraer-archivos-zip)
- [Extraer un archivo TAR](#extraer-un-archivo-tar)

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|--------|--------|------------|
| Comprimir archivos en ZIP | `zip` | `Compress-Archive` |
| Extraer archivos ZIP | `unzip` | `Expand-Archive` |
| Crear un archivo TAR | `tar -cvf` | `tar -cvf` |
| Extraer un archivo TAR | `tar -xvf` | `tar -xvf` |
| Comprimir con GZIP | `gzip` / `tar -czf` | `tar -czf` |
| Descomprimir archivos GZIP | `gunzip` / `tar -xzf` | `tar -xzf` |
| Comprimir con BZIP2 | `bzip2` / `tar -cjf` | `tar -cjf` |
| Comprimir con XZ | `xz` / `tar -cJf` | `tar -cJf` |
| Ver el contenido de un archivo comprimido | `unzip -l` / `tar -tf` | `tar -tf` |

---

### Buenas prácticas generales

- Utiliza **ZIP** cuando necesites la máxima compatibilidad entre distintos sistemas operativos.
- Recuerda que **TAR no comprime**, únicamente agrupa archivos y directorios.
- Elige el algoritmo de compresión en función de tus necesidades:
  - **GZIP** → Mayor velocidad.
  - **BZIP2** → Mejor compresión.
  - **XZ** → Máxima compresión.
- Comprueba el contenido de un archivo comprimido antes de extraerlo, especialmente si procede de una fuente externa.
- Conserva la copia comprimida original cuando se trate de copias de seguridad.
- Verifica siempre que dispones de espacio suficiente antes de crear o extraer archivos comprimidos de gran tamaño.

---

[⬆️ Volver al índice](#índice)
