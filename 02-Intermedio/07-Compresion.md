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

## Exrtaer un archivo TAR

### Linux

```bash
tar -xvf <archivo.tar>
```

**Descripción**

Permite extraer el contenido de un archivo **TAR**.

Al igual que en su creación, TAR únicamente contiene archivos agrupados, por lo que este comando restaura manteniendo la estructura de directorios original.

---

### PowerShell

```powershell
tar -xvf
```
**Descripción**

Windows incluye la utilidad **tar** (bsdtar), que permite extraer archivos TAR utilizando prácticamente la misma sintaxis que en Linux.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Extraer un archivo TAR | `tar -xvf` | `tar -xvf` |

---

### Significado de las opciones

| Opción | Significado |
|---------|-------------|
| `-x` | Extraer el contenido del archivo TAR |
| `-v` | Mostrar los archivos extraídos (*Verbose*) |
| `-f` | Indicar el archivo TAR que se va a extraer |

---

### Ejemplos

**Extraer un archivo TAR en el directorio actual**

Linux

```bash
tar -xvf copia.tar
```

PowerShell

```powershell
tar -xvf copia.tar
```

---

**Extraer un archivo TAR en un directorio concreto**

Linux

```bash
tar -xvf copia.tar -C /home/usuario/Documentos
```

PowerShell

```powershell
tar -xvf copia.tar `
-C C:\Users\Usuario\Documentos
```

---

**Extraer únicamente un archivo concreto del TAR**

Linux

```bash
tar -xvf copia.tar informe.pdf
```

PowerShell

```powershell
tar -xvf copia.tar informe.pdf
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| GNU tar está presente en prácticamente todas las distribuciones. | Windows utiliza bsdtar, pero la sintaxis es prácticamente idéntica. |
| Puede extraerse el contenido completo o archivos concretos. | También permite extraer archivos específicos del TAR. |
| La salida es texto estructurado. | La salida también es texto estructurado. |

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

> **💡 Consejo:** Si únicamente necesitas recuperar uno o dos archivos de un TAR, no es necesario extraer todo el contenido. Puedes indicar directamente el nombre del archivo al comando `tar -xvf` para extraer solo ese elemento.

---

[⬆️ Volver al índice](#índice)

## Comprimir con GZIP

### Linux

```bash
gzip <archivo>
```

También puede utilizarse:

```bash
tar -czf <archivo.tar.gz> <directorio>
```

**Descripción**

GZIP es uno de los algoritmos de compresión más utilizados en sistemas Linux.

Puede utilizarse de dos formas:

- **Comprimir un único archivo** mediante `gzip`.
- **Crear un archivo TAR comprimido** utilizando `tar` junto con la opción `-z`.

> **Importante:** `gzip` comprime **archivos individuales**. Para comprimir directorios completos es habitual utilizar `tar` junto con `gzip`.

---

### PowerShell

```powershell
tar -czf
```

**Descripción**

Windows incluye la utilidad **tar** (bsdtar), que permite crear archivos comprimidos utilizando el algoritmo **GZIP** mediante la opción `-z`.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Comprimir con GZIP | `gzip` / `tar -czf` | `tar -czf` |

---

### Significado de las opciones

| Opción | Significado |
|---------|-------------|
| `-c` | Crear un archivo TAR |
| `-z` | Comprimir utilizando GZIP |
| `-v` | Mostrar los archivos procesados (*Verbose*) |
| `-f` | Indicar el nombre del archivo generado |

---

### Ejemplos

**Comprimir un único archivo**

Linux

```bash
gzip informe.log
```

Resultado:

```text
informe.log.gz
```

---

**Crear un archivo TAR comprimido**

Linux

```bash
tar -czf copia.tar.gz Documentos/
```

PowerShell

```powershell
tar -czf copia.tar.gz Documentos
```

---

**Crear un archivo TAR.GZ mostrando el progreso**

Linux

```bash
tar -czvf copia.tar.gz Documentos/
```

PowerShell

```powershell
tar -czvf copia.tar.gz Documentos
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `gzip` puede comprimir directamente un archivo. | Normalmente se utiliza `tar -czf` para generar archivos `.tar.gz`. |
| Es habitual combinar `tar` y `gzip` para comprimir directorios completos. | El funcionamiento de `tar -czf` es prácticamente idéntico al de Linux. |
| La salida es texto estructurado. | La salida también es texto estructurado. |

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

> **💡 Consejo:** Un archivo **`.gz`** contiene normalmente **un único archivo comprimido**, mientras que un archivo **`.tar.gz`** contiene **uno o varios archivos agrupados mediante TAR y posteriormente comprimidos con GZIP**. Es una diferencia importante que conviene recordar.

---

[⬆️ Volver al índice](#índice)

## Descomprimir archivos GZIP

### Linux

```bash
gunzip <archivo.gz>
```

También puede utilizarse:

```bash
gzip -d <archivo.gz>
```

o, si se trata de un archivo TAR comprimido:

```bash
tar -xzf <archivo.tar.gz>
```

**Descripción**

Permite descomprimir archivos comprimidos con **GZIP**.

Dependiendo del tipo de archivo:

- `gunzip` descomprime archivos **.gz**.
- `gzip -d` realiza la misma función que `gunzip`.
- `tar -xzf` extrae directamente el contenido de un archivo **.tar.gz**.

---

### PowerShell

```powershell
tar -xzf
```

**Descripción**

Permite extraer el contenido de archivos comprimidos en formato **.tar.gz** utilizando la utilidad **tar** incluida en Windows.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Descomprimir un archivo GZIP | `gunzip` / `gzip -d` | `tar -xzf` (para `.tar.gz`) |
| Extraer un archivo TAR.GZ | `tar -xzf` | `tar -xzf` |

---

### Significado de las opciones

| Opción | Significado |
|---------|-------------|
| `-x` | Extraer archivos |
| `-z` | Utilizar GZIP durante la extracción |
| `-v` | Mostrar los archivos extraídos (*Verbose*) |
| `-f` | Indicar el archivo comprimido |

---

### Ejemplos

**Descomprimir un archivo `.gz`**

Linux

```bash
gunzip informe.log.gz
```

o

```bash
gzip -d informe.log.gz
```

---

**Extraer un archivo `.tar.gz`**

Linux

```bash
tar -xzf copia.tar.gz
```

PowerShell

```powershell
tar -xzf copia.tar.gz
```

---

**Extraer un archivo `.tar.gz` mostrando el progreso**

Linux

```bash
tar -xzvf copia.tar.gz
```

PowerShell

```powershell
tar -xzvf copia.tar.gz
```

---

**Extraer un archivo `.tar.gz` en otro directorio**

Linux

```bash
tar -xzf copia.tar.gz -C /home/usuario/Documentos
```

PowerShell

```powershell
tar -xzf copia.tar.gz `
-C C:\Users\Usuario\Documentos
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `gunzip` descomprime archivos `.gz` individuales. | Lo habitual es utilizar `tar -xzf` para archivos `.tar.gz`. |
| `gzip -d` y `gunzip` realizan la misma función. | La sintaxis de `tar` es prácticamente idéntica a la de Linux. |
| La salida es texto estructurado. | La salida también es texto estructurado. |

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

> **💡 Consejo:** Si ves un archivo con extensión **`.tar.gz`**, recuerda que primero fue **agrupado con TAR** y después **comprimido con GZIP**. Por eso el comando `tar -xzf` realiza ambas operaciones automáticamente en un único paso.

---

[⬆️ Volver al índice](#índice)

## Comprimir con BZIP2 y XZ

### Linux

```bash
bzip2 <archivo>
```

También puede utilizarse:

```bash
xz <archivo>
```

o, para comprimir un directorio completo:

```bash
tar -cjf <archivo.tar.bz2> <directorio>
```

```bash
tar -cJf <archivo.tar.xz> <directorio>
```

**Descripción**

BZIP2 y XZ son algoritmos de compresión alternativos a GZIP.

- **BZIP2** suele ofrecer una mejor compresión que GZIP, aunque requiere más tiempo.
- **XZ** consigue una compresión aún mayor, siendo muy utilizado para distribuir software y realizar copias de seguridad.

Al igual que GZIP:

- `bzip2` y `xz` comprimen archivos individuales.
- Para comprimir directorios completos se utilizan junto con `tar`.

---

### PowerShell

```powershell
tar -cjf
```

o

```powershell
tar -cJf
```

**Descripción**

La utilidad **tar** incluida en Windows permite crear archivos comprimidos utilizando los algoritmos **BZIP2** (`-j`) y **XZ** (`-J`).

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Comprimir con BZIP2 | `bzip2` / `tar -cjf` | `tar -cjf` |
| Comprimir con XZ | `xz` / `tar -cJf` | `tar -cJf` |

---

### Significado de las opciones

| Opción | Significado |
|---------|-------------|
| `-c` | Crear un archivo TAR |
| `-j` | Utilizar compresión BZIP2 |
| `-J` | Utilizar compresión XZ |
| `-v` | Mostrar los archivos procesados (*Verbose*) |
| `-f` | Indicar el nombre del archivo generado |

---

### Ejemplos

**Comprimir un archivo con BZIP2**

Linux

```bash
bzip2 informe.log
```

Resultado:

```text
informe.log.bz2
```

---

**Comprimir un archivo con XZ**

Linux

```bash
xz informe.log
```

Resultado:

```text
informe.log.xz
```

---

**Crear un archivo TAR.BZ2**

Linux

```bash
tar -cjf copia.tar.bz2 Documentos/
```

PowerShell

```powershell
tar -cjf copia.tar.bz2 Documentos
```

---

**Crear un archivo TAR.XZ**

Linux

```bash
tar -cJf copia.tar.xz Documentos/
```

PowerShell

```powershell
tar -cJf copia.tar.xz Documentos
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `bzip2` y `xz` pueden comprimir directamente archivos individuales. | Lo habitual es utilizar `tar` con las opciones `-j` o `-J`. |
| Ambos algoritmos pueden combinarse con `tar` para comprimir directorios completos. | La sintaxis es prácticamente idéntica a la utilizada en Linux. |
| La salida es texto estructurado. | La salida también es texto estructurado. |

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

> **💡 Consejo:** Como regla general:
>
> - **GZIP** → Más rápido.
> - **BZIP2** → Mejor compresión.
> - **XZ** → Máxima compresión, pero también el mayor tiempo de procesamiento.
>
> La elección depende de si priorizas la velocidad o el tamaño final del archivo.

---

[⬆️ Volver al índice](#índice)

## Ver el contenido de un archivo comprimido

### Linux

```bash
unzip -l <archivo.zip>
```

También puede utilizarse:

```bash
tar -tf <archivo.tar>
```

o, para archivos comprimidos:

```bash
tar -tzf <archivo.tar.gz>
```

```bash
tar -tjf <archivo.tar.bz2>
```

```bash
tar -tJf <archivo.tar.xz>
```

**Descripción**

Permite consultar el contenido de un archivo comprimido sin necesidad de extraerlo.

Es especialmente útil para:

- Verificar qué archivos contiene.
- Comprobar la estructura de directorios.
- Confirmar que el archivo es el esperado antes de extraerlo.

---

### PowerShell

```powershell
tar -tf
```

También puede utilizarse:

```powershell
tar -tzf
```

para archivos `.tar.gz`.

**Descripción**

La utilidad **tar** incluida en Windows permite listar el contenido de archivos TAR y TAR comprimidos sin necesidad de descomprimirlos.

Para archivos ZIP, PowerShell no dispone de un cmdlet específico, por lo que suele utilizarse el Explorador de archivos o librerías .NET.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver contenido de un archivo ZIP | `unzip -l` | Explorador de archivos |
| Ver contenido de un archivo TAR | `tar -tf` | `tar -tf` |
| Ver contenido de un archivo TAR.GZ | `tar -tzf` | `tar -tzf` |

---

### Significado de las opciones

| Opción | Significado |
|---------|-------------|
| `-t` | Mostrar el contenido del archivo |
| `-z` | Utilizar GZIP |
| `-j` | Utilizar BZIP2 |
| `-J` | Utilizar XZ |
| `-f` | Indicar el archivo comprimido |

---

### Ejemplos

**Ver el contenido de un archivo ZIP**

Linux

```bash
unzip -l copia.zip
```

---

**Ver el contenido de un archivo TAR**

Linux

```bash
tar -tf copia.tar
```

PowerShell

```powershell
tar -tf copia.tar
```

---

**Ver el contenido de un archivo TAR.GZ**

Linux

```bash
tar -tzf copia.tar.gz
```

PowerShell

```powershell
tar -tzf copia.tar.gz
```

---

**Ver el contenido de un archivo TAR.XZ**

Linux

```bash
tar -tJf copia.tar.xz
```

PowerShell

```powershell
tar -tJf copia.tar.xz
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `unzip -l` permite listar fácilmente el contenido de archivos ZIP. | Windows no dispone de un cmdlet específico para listar ZIP desde PowerShell. |
| `tar` permite listar archivos TAR y sus variantes comprimidas. | `tar` ofrece prácticamente la misma funcionalidad que en Linux. |
| La salida es texto estructurado. | La salida también es texto estructurado. |

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

> **💡 Consejo:** Antes de descomprimir una copia de seguridad o un archivo descargado de Internet, consulta primero su contenido. Es una forma rápida de verificar que contiene exactamente los archivos esperados sin modificar nada en el sistema.

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

### Comandos más utilizados

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Crear un ZIP | `zip` | `Compress-Archive` |
| Extraer un ZIP | `unzip` | `Expand-Archive` |
| Crear un TAR | `tar -cvf` | `tar -cvf` |
| Extraer un TAR | `tar -xvf` | `tar -xvf` |
| Crear un TAR.GZ | `tar -czf` | `tar -czf` |
| Extraer un TAR.GZ | `tar -xzf` | `tar -xzf` |
| Crear un TAR.BZ2 | `tar -cjf` | `tar -cjf` |
| Crear un TAR.XZ | `tar -cJf` | `tar -cJf` |
| Ver contenido de un TAR | `tar -tf` | `tar -tf` |

---

### Formatos más comunes

| Formato | Agrupa archivos | Comprime | Uso habitual |
|---------|:---------------:|:---------:|--------------|
| **.zip** | ✅ | ✅ | Compartir archivos entre distintos sistemas |
| **.tar** | ✅ | ❌ | Agrupar archivos manteniendo su estructura |
| **.tar.gz** | ✅ | ✅ | Copias de seguridad y distribución de software |
| **.tar.bz2** | ✅ | ✅ | Mayor compresión que GZIP |
| **.tar.xz** | ✅ | ✅ | Máxima compresión |

---

[⬆️ Volver al índice](#índice)
