# Permisos

## Introducción

Los permisos determinan qué usuarios pueden leer, modificar o ejecutar archivos y directorios.

Comprender el funcionamiento de los permisos es fundamental para proteger la información del sistema, evitar accesos no autorizados y administrar correctamente equipos y servidores.

Linux y Windows utilizan modelos de permisos diferentes, pero ambos persiguen el mismo objetivo: controlar el acceso a los recursos del sistema.

---

## Índice
- [Consultar permisos](#consultar-permisos)
- [Interpretar los permisos](#interpretar-los-permisos)
- [Cambiar permisos](#cambiar-permisos)
- [Cambiar propietario](#cambiar-propietario)
- [Cambiar grupo](#cambiar-grupo)
- [Permisos recursivos](#permisos-recursivos)
- [Permisos especiales](#permisos-especiales)
- [Resumen de equivalencias](#resumen-de-equivalencias)

---


## Consultar permisos

### Linux

```bash
ls -l
```

**Descripción**

Muestra los permisos, propietario, grupo y otra información detallada de los archivos y directorios.

---

### PowerShell

```powershell
Get-Acl <ruta>
```

**Descripción**

Muestra una lista de control de acceso (ACL) de un archivo o directorio, incluyendo propietarios, permisos y reglas de acceso.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Consultar permisos | `ls -l` | `Get-Acl` |

---

### Ejemplos

**Consultar los permisos del directorio actual**

Linux

```bash
ls -l
```

PowerShell

```powershell
Get-Acl .
```

---

**Consultar los permisos de un archivo**

Linux

```bash
ls -l informe.txt
```

PowerShell

```powershell
Get-Acl .\informe.txt
```

---

**Consultar los permisos de un directorio**

Linux

```bash
ls -ld Documentos
```

PowerShell

```powershell
Get-Acl .\Documentos
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `ls -l` muestra los permisos mediante la notación `rwx`. | `Get-Acl` utiliza listas de control de acceso (ACL). |
| La salida incluye propietario, grupo y permisos en una única línea. | La salida incluye el propietario y las reglas de acceso asociadas al recurso. |
| Es posible consultar archivos y directorios con el mismo comando. | También permite consultar archivos y directorios mediante la misma sintaxis. |

---

### Buenas prácticas

- Comprueba siempre los permisos antes de modificarlos.
- Verifica que el propietario y el grupo sean los esperados.
- Consulta los permisos de directorios con `ls -ld` para evitar mostrar su contenido.
- En PowerShell, revisa las reglas de acceso antes de realizar cambios sobre una ACL.

---

### Comandos relacionados

- [Interpretar los permisos](#interpretar-los-permisos)
- [Cambiar permisos](#cambiar-permisos)
- [Cambiar propietario](#cambiar-propietario)

---

[⬆️ Volver al índice](#índice)

## Interpretar los permisos

### Linux

```text
-rwxr-xr--
```

**Descripción**

En Linux, los permisos se representan mediante una cadena de caracteres que indica el tipo de archivo y los permisos asignados al propietario, al grupo y al resto de usuarios.

La estructura es la siguiente:

```text
-rwxr-xr--
│││ │││ │││
│││ │││ │└┴─ Otros
│││ └┴┴──── Grupo
│└┴──────── Propietario
└────────── Tipo de archivo
```

**Tipos de archivo más habituales**

| Símbolo | Tipo |
|---------|------|
| `-` | Archivo |
| `d` | Directorio |
| `l` | Enlace simbólico |

**Permisos**

| Símbolo | Significado |
|---------|-------------|
| `r` | Lectura (Read) |
| `w` | Escritura (Write) |
| `x` | Ejecución (Execute) |
| `-` | Sin permiso |

---

### PowerShell

```powershell
Get-Acl .\archivo.txt
```

**Descripción**

PowerShell utiliza listas de control de acceso (**ACL - Access Control List**) para definir los permisos de un archivo o directorio.

Cada regla especifica:

- Usuario o grupo.
- Permisos concedidos.
- Tipo de acceso (Permitir o Denegar).
- Herencia.

Ejemplo de salida:

```text
Path   : Microsoft.PowerShell.Core\FileSystem::C:\Datos\archivo.txt
Owner  : EQUIPO\Administrador

Access :
SYSTEM                Allow  FullControl
Administradores       Allow  FullControl
Usuario               Allow  ReadAndExecute
```

---

### Equivalencia

| Linux | PowerShell |
|--------|------------|
| Permisos POSIX (`rwx`) | Permisos NTFS (ACL) |
| Propietario, grupo y otros | Usuarios y grupos con reglas individuales |
| Tres niveles de permisos | Permisos granulares por usuario o grupo |

---

### Ejemplos

**Archivo con permisos completos para el propietario**

Linux

```text
-rwxr-xr--
```

Significa:

- Propietario → Lectura, escritura y ejecución.
- Grupo → Lectura y ejecución.
- Otros → Solo lectura.

---

**Archivo con permisos de solo lectura**

Linux

```text
-r--r--r--
```

Significa:

- Todos los usuarios pueden leer el archivo.
- Nadie puede modificarlo ni ejecutarlo.

---

**Permisos mediante ACL**

PowerShell

```powershell
Get-Acl .\archivo.txt
```

Resultado:

```text
Usuario        Allow Read
Administradores Allow FullControl
SYSTEM          Allow FullControl
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Utiliza permisos POSIX representados mediante `rwx`. | Utiliza listas de control de acceso (ACL). |
| Solo existen tres entidades: propietario, grupo y otros. | Puede haber reglas independientes para numerosos usuarios y grupos. |
| La representación es muy compacta. | La información es más detallada y flexible. |

---

### Buenas prácticas

- Comprende el significado de los permisos antes de modificarlos.
- Evita conceder permisos de escritura o ejecución cuando no sean necesarios.
- Revisa periódicamente los permisos de archivos sensibles.
- En PowerShell, comprueba siempre las ACL antes de realizar cambios.

---

### Comandos relacionados

- [Consultar permisos](#consultar-permisos)
- [Cambiar permisos](#cambiar-permisos)
- [Cambiar propietario](#cambiar-propietario)

---

[⬆️ Volver al índice](#índice)

## Cambiar permisos

### Linux

```bash
chmod <permisos> <archivo>
```

**Descripción**

Modifica los permisos de un archivo o directorio.

Los permisos pueden especificarse mediante **notación simbólica** o **notación octal**.

---

### PowerShell

```powershell
icacls <ruta> /grant <usuario>:<permisos>
```

**Descripción**

Modifica los permisos de un archivo o directorio mediante las listas de control de acceso (ACL).

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Cambiar permisos | `chmod` | `icacls` |

---

### Ejemplos

**Conceder permisos de ejecución al propietario**

Linux

```bash
chmod u+x script.sh
```

PowerShell

```powershell
icacls .\script.ps1 /grant Usuario:RX
```

---

**Conceder permisos de lectura y escritura al propietario**

Linux

```bash
chmod 600 informe.txt
```

PowerShell

```powershell
icacls .\informe.txt /grant Usuario:M
```

---

**Permitir lectura y ejecución para todos los usuarios**

Linux

```bash
chmod 755 programa
```

PowerShell

```powershell
icacls .\programa.exe /grant Todos:RX
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `chmod` modifica permisos POSIX (`rwx`). | `icacls` modifica permisos NTFS mediante ACL. |
| Puede utilizar notación simbólica (`u+x`) u octal (`755`). | Los permisos se conceden mediante reglas asociadas a usuarios o grupos. |
| Los cambios afectan al propietario, grupo o resto de usuarios. | Los cambios afectan únicamente a los usuarios o grupos especificados. |

---

### Buenas prácticas

- Aplica siempre el principio de **mínimo privilegio**, concediendo únicamente los permisos necesarios.
- Utiliza la notación simbólica cuando solo necesites modificar un permiso concreto.
- Utiliza la notación octal para aplicar una configuración completa de permisos.
- Comprueba los permisos después de modificarlos para verificar que el resultado es el esperado.

---

### Comandos relacionados

- [Consultar permisos](#consultar-permisos)
- [Cambiar propietario](#cambiar-propietario)
- [Cambiar grupo](#cambiar-grupo)

---

[⬆️ Volver al índice](#índice)

## Cambiar propietario

### Linux

```bash
chown <propietario> <archivo>
```

**Descripción**

Permite cambiar el propietario de un archivo o directorio. Solo el usuario **root** o un usuario con privilegios suficientes puede modificar el propietario de un recurso.

---

### PowerShell

```powershell
takeown /F <ruta>
```

También puede utilizarse:

```powershell
$acl = Get-Acl <ruta>
$acl.SetOwner([System.Security.Principal.NTAccount]"Usuario")
Set-Acl <ruta> $acl
```

**Descripción**

En Windows, el propietario de un archivo o directorio puede cambiarse utilizando `takeown` o modificando la ACL mediante `Set-Acl`.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Cambiar propietario | `chown` | `takeown` / `Set-Acl` |

---

### Ejemplos

**Cambiar el propietario de un archivo**

Linux

```bash
sudo chown beatriz informe.txt
```

PowerShell

```powershell
takeown /F .\informe.txt
```

---

**Cambiar el propietario de un directorio**

Linux

```bash
sudo chown beatriz Documentos
```

PowerShell

```powershell
takeown /F .\Documentos
```

---

**Cambiar propietario de forma recursiva**

Linux

```bash
sudo chown -R beatriz Proyecto
```

PowerShell

```powershell
takeown /F .\Proyecto /R
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `chown` cambia el propietario de archivos y directorios. | `takeown` asigna la propiedad del recurso al usuario actual o al administrador. |
| Puede utilizarse junto con `-R` para aplicar el cambio de forma recursiva. | Puede utilizarse `/R` para aplicar el cambio de forma recursiva. |
| Es necesario disponer de privilegios elevados para cambiar el propietario. | También se requieren permisos de administrador para tomar posesión de un recurso. |

---

### Buenas prácticas

- Cambia el propietario únicamente cuando sea necesario.
- Comprueba siempre quién es el propietario antes y después del cambio.
- Utiliza la opción recursiva con precaución, especialmente sobre directorios con muchos archivos.
- Evita modificar el propietario de archivos del sistema si desconoces las consecuencias.

---

### Comandos relacionados

- [Consultar permisos](#consultar-permisos)
- [Cambiar permisos](#cambiar-permisos)
- [Cambiar grupo](#cambiar-grupo)

---

[⬆️ Volver al índice](#índice)

## Permisos recursivos

### Linux

```bash
chmod -R <permisos> <directorio>
```

También puede utilizarse:

```bash
chown -R <propietario> <directorio>
```

```bash
chgrp -R <grupo> <directorio>
```

**Descripción**

Aplica los cambios de permisos, propietario o grupo a un directorio y a todo su contenido (subdirectorios y archivos).

---

### PowerShell

```powershell
icacls <ruta> /grant <usuario>:<permisos> /T
```

También puede utilizarse:

```powershell
takeown /F <ruta> /R
```

**Descripción**

Permite aplicar cambios de permisos o de propietario de forma recursiva sobre un directorio y todos los elementos que contiene.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Aplicar permisos de forma recursiva | `chmod -R` | `icacls /T` |
| Cambiar propietario de forma recursiva | `chown -R` | `takeown /R` |

---

### Ejemplos

**Conceder permisos de lectura y ejecución a un directorio completo**

Linux

```bash
chmod -R 755 Proyecto
```

PowerShell

```powershell
icacls .\Proyecto /grant Usuario:RX /T
```

---

**Cambiar el propietario de todo un directorio**

Linux

```bash
sudo chown -R beatriz Proyecto
```

PowerShell

```powershell
takeown /F .\Proyecto /R
```

---

**Cambiar el grupo de todo un directorio**

Linux

```bash
sudo chgrp -R desarrolladores Proyecto
```

PowerShell

```powershell
icacls .\Proyecto /grant Desarrolladores:M /T
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| La opción `-R` aplica los cambios a todos los archivos y subdirectorios. | La opción `/T` aplica los cambios de permisos de forma recursiva. |
| Puede utilizarse con `chmod`, `chown` y `chgrp`. | Puede utilizarse con `icacls` y `takeown`. |
| Es una operación muy rápida, pero puede afectar a un gran número de archivos. | También modifica todos los elementos contenidos en la ruta especificada. |

---

### Buenas prácticas

- Comprueba la ruta antes de utilizar opciones recursivas.
- Evita ejecutar cambios recursivos sobre directorios del sistema.
- Realiza una copia de seguridad antes de modificar permisos en grandes estructuras de directorios.
- Verifica el resultado tras finalizar la operación para asegurarte de que los permisos son los esperados.

---

### Comandos relacionados

- [Cambiar permisos](#cambiar-permisos)
- [Cambiar propietario](#cambiar-propietario)
- [Cambiar grupo](#cambiar-grupo)

---

[⬆️ Volver al índice](#índice)

## Permisos especiales

### Linux

Además de los permisos tradicionales (`rwx`), Linux dispone de tres permisos especiales que modifican el comportamiento de archivos y directorios.

| Permiso | Valor octal | Descripción |
|---------|------------:|-------------|
| **SUID** | `4` | Ejecuta un programa con los permisos del propietario. |
| **SGID** | `2` | Ejecuta un programa con los permisos del grupo o hace que los nuevos archivos hereden el grupo del directorio. |
| **Sticky Bit** | `1` | En un directorio, únicamente el propietario del archivo (o el administrador) puede eliminarlo. |

---

### PowerShell

Windows no dispone de permisos especiales equivalentes a **SUID**, **SGID** o **Sticky Bit**.

En su lugar, utiliza características propias del sistema de permisos NTFS, como:

- Herencia de permisos.
- Permisos explícitos.
- Permisos heredados.
- Propietario del recurso.
- Listas de control de acceso (ACL).

---

### Equivalencia

| Linux | PowerShell |
|--------|------------|
| SUID | No existe equivalente directo |
| SGID | No existe equivalente directo |
| Sticky Bit | No existe equivalente directo |
| Herencia mediante SGID | Herencia de permisos mediante ACL |

---

### Ejemplos

**Asignar SUID a un programa**

Linux

```bash
chmod u+s programa
```

También puede utilizarse:

```bash
chmod 4755 programa
```

---

**Asignar SGID a un directorio**

Linux

```bash
chmod g+s Proyecto
```

También puede utilizarse:

```bash
chmod 2755 Proyecto
```

---

**Asignar Sticky Bit a un directorio**

Linux

```bash
chmod +t Compartido
```

También puede utilizarse:

```bash
chmod 1777 Compartido
```

---

**Consultar permisos especiales**

Linux

```bash
ls -l
```

Ejemplo:

```text
-rwsr-xr-x
drwxr-sr-x
drwxrwxrwt
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Existen permisos especiales además de `rwx`. | No existen permisos especiales equivalentes. |
| Se representan mediante `s`, `S`, `t` o `T`. | La seguridad se basa en ACL y herencia de permisos. |
| Se configuran con `chmod`. | La administración se realiza mediante ACL (`Get-Acl`, `Set-Acl`, `icacls`). |

---

### Buenas prácticas

- Utiliza **SUID** únicamente cuando sea imprescindible, ya que puede representar un riesgo de seguridad.
- Emplea **SGID** para facilitar el trabajo colaborativo en directorios compartidos.
- Utiliza **Sticky Bit** en directorios públicos para impedir que los usuarios eliminen archivos ajenos.
- Revisa periódicamente qué archivos tienen permisos especiales asignados.

---

### Comandos relacionados

- [Consultar permisos](#consultar-permisos)
- [Cambiar permisos](#cambiar-permisos)
- [Permisos recursivos](#permisos-recursivos)

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|--------|--------|------------|
| Consultar permisos | `ls -l` | `Get-Acl` |
| Cambiar permisos | `chmod` | `icacls` |
| Cambiar propietario | `chown` | `takeown` / `Set-Acl` |
| Cambiar grupo | `chgrp` | No existe un equivalente directo |
| Aplicar cambios de forma recursiva | `chmod -R` / `chown -R` / `chgrp -R` | `icacls /T` / `takeown /R` |
| Consultar permisos especiales | `ls -l` | No existe equivalente directo |
| Asignar SUID | `chmod u+s` | No existe equivalente directo |
| Asignar SGID | `chmod g+s` | No existe equivalente directo |
| Asignar Sticky Bit | `chmod +t` | No existe equivalente directo |

---

### Buenas prácticas generales

- Aplica siempre el **principio de mínimo privilegio**, concediendo únicamente los permisos necesarios.
- Comprueba los permisos actuales antes de modificarlos.
- Evita utilizar permisos excesivamente permisivos como `777`, salvo en situaciones muy concretas.
- Utiliza grupos para administrar permisos en lugar de asignarlos usuario por usuario.
- Antes de aplicar cambios recursivos, verifica cuidadosamente la ruta seleccionada.
- Revisa periódicamente los permisos de archivos y directorios críticos.
- En PowerShell, recuerda que los permisos se administran mediante **ACL**, no mediante permisos POSIX.

---

[⬆️ Volver al índice](#índice)