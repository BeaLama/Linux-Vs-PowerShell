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

### Comandos relacionados

- [Extraer un archivo TAR](#extraer-un-archivo-tar)
- [Comprimir con GZIP](#comprimir-con-gzip)
- [Ver el contenido de un archivo comprimido](#ver-el-contenido-de-un-archivo-comprimido)

---

[⬆️ Volver al índice](#índice)

## Extraer un archivo TAR

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

### Comandos relacionados

- [Comprimir archivos en ZIP](#comprimir-archivos-en-zip)
- [Extraer archivos ZIP](#extraer-archivos-zip)
- [Extraer un archivo TAR](#extraer-un-archivo-tar)

---

[⬆️ Volver al índice](#índice)