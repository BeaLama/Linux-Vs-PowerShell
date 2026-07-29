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

### Linux

```bash
zip <archivo.zip> <archivo>
```

También puede utilizarse:

```bash
zip -r <archivo.zip> <directorio>
```

**Descripción**

Permite crear archivos comprimidos en formato **ZIP**.

El formato ZIP es uno de los más utilizados por su compatibilidad entre sistemas operativos.

La opción `-r` (*recursive*) comprime directorios completos junto con todo su contenido.

---

### PowerShell

```powershell
Compress-Archive
```

**Descripción**

Permite crear archivos comprimidos en formato ZIP.

Puede comprimir uno o varios archivos, así como directorios completos.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Comprimir archivos en ZIP | `zip` | `Compress-Archive` |

---

### Ejemplos

**Comprimir un único archivo**

Linux

```bash
zip documentos.zip informe.pdf
```

PowerShell

```powershell
Compress-Archive `
-Path ".\informe.pdf" `
-DestinationPath ".\documentos.zip"
```

---

**Comprimir un directorio completo**

Linux

```bash
zip -r copia.zip Documentos/
```

PowerShell

```powershell
Compress-Archive `
-Path ".\Documentos" `
-DestinationPath ".\copia.zip"
```

---

**Comprimir varios archivos**

Linux

```bash
zip copia.zip archivo1.txt archivo2.txt imagen.png
```

PowerShell

```powershell
Compress-Archive `
-Path ".\archivo1.txt",
      ".\archivo2.txt",
      ".\imagen.png" `
-DestinationPath ".\copia.zip"
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `zip` utiliza la opción `-r` para incluir directorios completos. | `Compress-Archive` comprime archivos y carpetas mediante el parámetro `-Path`. |
| Puede añadirse contenido a un ZIP existente ejecutando nuevamente `zip`. | Si el archivo ZIP ya existe, normalmente será necesario utilizar `-Update` o eliminarlo previamente. |
| La salida es texto estructurado. | La salida son objetos y mensajes del cmdlet. |

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

> **💡 Consejo:** El formato **ZIP** es la mejor opción cuando el archivo va a compartirse entre distintos sistemas operativos, ya que está soportado de forma nativa tanto en Windows como en la mayoría de distribuciones Linux.

---

[⬆️ Volver al índice](#índice)

## Extraer archivos ZIP

### Linux

```bash
unzip <archivo.zip>
```

También puede utilziarse

```bash
unzip <archivo.zip> -d <directorio>
```

**Descripción**

Permite extraer el contenido de un archivo comprimido en formato **ZIP**.

Por defecto, los archivos se extraen en el directorio actual.

La opción `-d` permite indicar un directorio de destino.

---

### PowerShell

```powershell
Expand-Archive
```

**Descripción**

Permite extraer el contenido de un archivo ZIP.

Puede indicarse el directorio donde se descomprimirán los archivos mediante el parámetro `-DestinationPath`.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Extraer archivos ZIP | `unzip` | `Expand-Archive` |

---

### Ejemplos

**Extraer un archivo ZIP en el directorio actual**

Linux

```bash
unzip copia.zip
```

PowerShell

```powershell
Expand-Archive `
-Path ".\copia.zip" `
-DestinationPath "."
```

---

**Extraer un archivo ZIP en otro directorio**

Linux

```bash
unzip copia.zip -d /home/usuario/Documentos
```

PowerShell

```powershell
Expand-Archive `
-Path ".\copia.zip" `
-DestinationPath "C:\Users\Usuario\Documentos"
```

---

**Sobrescribir archivos existentes**

Linux

```bash
unzip -o copia.zip
```

PowerShell

```powershell
Expand-Archive `
-Path ".\copia.zip" `
-DestinationPath ".\Destino" `
-Force
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `unzip` extrae el contenido en el directorio actual por defecto. | Es recomendable indicar siempre el directorio mediante `-DestinationPath`. |
| La opción `-o` sobrescribe automáticamente los archivos existentes. | El parámetro `-Force` permite sobrescribir archivos existentes cuando es necesario. |
| La salida es texto estructurado. | La salida son mensajes y objetos del cmdlet. |

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

> **💡 Consejo:** Antes de extraer un archivo ZIP descargado de Internet, revisa su contenido para asegurarte de que no incluye archivos inesperados o potencialmente maliciosos.

---

[⬆️ Volver al índice](#índice)

## Crear un archivo TAR

### Linux

```bash
tar -cvf <archivo.tar> <archivo_o_directorio>
```

**Descripción**

Permite crear un archivo **TAR** (*Tape Archive*).

A diferencia de ZIP, **TAR no comprime los archivos**. Su función consiste en agrupar uno o varios archivos y directorios en un único archivo.

Es habitual combinar TAR con herramientas de compresión como **GZIP**, **BZIP2** o **XZ**, dando lugar a formatos como:

- `.tar.gz`
- `.tar.bz2`
- `.tar.xz`

---

### PowerShell

```powershell
tar -cvf
```

**Descripción**

Las versiones modernas de Windows incluyen la utilidad **tar** (basada en **bsdtar**), que permite crear archivos TAR de forma muy similar a Linux.

Su funcionamiento es prácticamente idéntico.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Crear un archivo TAR | `tar -cvf` | `tar -cvf` |

---

### Significado de las opciones

| Opción | Significado |
|---------|-------------|
| `-c` | Crear un archivo TAR |
| `-v` | Mostrar los archivos procesados (*Verbose*) |
| `-f` | Indicar el nombre del archivo TAR |

---

### Ejemplos

**Agrupar un único archivo**

Linux

```bash
tar -cvf copia.tar informe.pdf
```

PowerShell

```powershell
tar -cvf copia.tar informe.pdf
```

---

**Agrupar un directorio completo**

Linux

```bash
tar -cvf copia.tar Documentos/
```

PowerShell

```powershell
tar -cvf copia.tar Documentos
```

---

**Agrupar varios archivos**

Linux

```bash
tar -cvf copia.tar archivo1.txt archivo2.txt imagen.png
```

PowerShell

```powershell
tar -cvf copia.tar `
archivo1.txt `
archivo2.txt `
imagen.png
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Utiliza GNU tar en la mayoría de distribuciones. | Utiliza bsdtar incluido en Windows. |
| El funcionamiento y la sintaxis son prácticamente idénticos. | La compatibilidad con los parámetros más comunes es prácticamente total. |
| La salida es texto estructurado. | La salida también es texto estructurado. |

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

> **💡 Consejo:** Mucha gente cree que **TAR comprime los archivos**, pero no es así. **TAR únicamente agrupa archivos y directorios**. La compresión la realizan herramientas como **GZIP**, **BZIP2** o **XZ**, por eso existen extensiones como `.tar.gz`, `.tar.bz2` o `.tar.xz`.

---

[⬆️ Volver al índice](#índice)







































## Resumen de equivalencias

| Acción | Linux | PowerShell |
|--------|-------|------------|
| Comprimir archivos en ZIP |
| Extraer archivos ZIP |
| Crear un archivo TAR |
| Extraer un archivo TAR |
| Comprimir con GZIP |
| Descomprimir archivos GZIP
| Comprimir con BZIP2 y XZ |
| Ver el contenido de un archivo comprimido | 