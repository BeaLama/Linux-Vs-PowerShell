# Permisos avanzados

## Introducción

Los permisos son uno de los elementos fundamentales en la administración de sistemas, ya que permiten controlar quién puede acceder a los recursos y qué acciones puede realizar sobre ellos.

El objetivo es aprender a gestionar correctamente los permisos en entornos profesionales, evitando configuraciones demasiado permisivas y aplicando el principio de mínimo privilegio.

---

## Índice

- [ACL en Linux](#acl-en-linux)
- [Permisos especiales Linux](#permisos-especiales-linux)
- [ACL en Windows](#acl-en-windows)
- [Herencia de permisos](#herencia-de-permisos)
- [Permisos efectivos](#permisos-efectivos)
- [Delegación de permisos](#delegación-de-permisos)
- [Auditoría de permisos](#auditoría-de-permisos)
- [Buenas prácticas](#buenas-prácticas)

---

## ACL en Linux

Las **ACL (Access Control Lists)** permiten asignar permisos específicos a usuarios y grupos individuales sin modificar los permisos tradicionales de propietario, grupo y otros.

Mientras que los permisos tradicionales de Linux solo permiten definir permisos para:

- Propietario.
- Grupo propietario.
- Otros usuarios.

Las ACL permiten conceder permisos adicionales a usuarios o grupos concretos.

Esto resulta especialmente útil en enternos donde varios usuarios necesitan acceder a un mismo recurso con permisos diferentes.

---

### Comprobar si el sistema admite ACL

La mayoría de distribuciones Linux actuales soportan ACL de forma nativa.

Puede comprobarse mediante:

```bash
mount | grep acl
```

O consultando las opciones de montaje:

```bash
mount
```

En sistemas modernos (ext4, XFS, Btrfs, etc.) normalmente no es necesario realizar ninguna configuración adicional.

---

### Ver las ACL de un archivo

Para consultar las ACL de un archivo se utiliza:

```bash
getfacl archivo.txt
```
Ejemplo:

```bash
getfacl informe.txt
```

Salida:

```text
# file: informe.txt
# owner: admin
# group: ventas
user::rw-
user:juan:r--
group::r--
mask::r--
other::---
```

---

### Interpretación

En el ejemplo anterior:

| Entrada | Significado |
|---------|-------------|
| `user::rw-` | Permisos del propietario |
| `user:juan:r--` | Permisos específicos para el usuario **juan** |
| `group::r--` | Permisos del grupo propietario |
| `mask::r--` | Permisos máximos que pueden tener las ACL |
| `other::---` | Permisos para el resto de usuarios |

---

### Asignar ACL a un usuario

Para conceder permisos a un usuario específico:

```bash
setfacl -m u:usuario:permisos archivo
```

Ejemplo:

```bash
setfacl -m u:juan:rw informe.txt
```

Ahora **juan** podrá leer y modificar el archivo aunque no sea el propietario.

Comprobar:

```bash
getfacl informe.txt
```

---

### Asignar ACL a un grupo

También pueden asignarse permisos a un grupo.

Sintaxis:

```bash
setfacl -m g:grupo:permisos archivo
```

Ejemplo:

```bash
setfacl -m g:informatica:rwx proyecto
```

Todos los usuarios pertenecientes al grupo **informatica** heredarán esos permisos.

---

### Eliminar una ACL

Eliminar permisos de un usuario:

```bash
setfacl -x u:juan informe.txt
```

Eliminar permisos de un grupo:

```bash
setfacl -x g:informatica informe.txt
```

---

### Eliminar todas las ACL

Para volver únicamente a los permisos tradicionales:

```bash
setfacl -b informe.txt
```

Esto elimina todas las ACL del archivo.

---

### ACL por defecto

En directorios es posible definir ACL que heredarán automáticamente los nuevos archivos y carpetas.

Sintaxis:

```bash
setfacl -d -m u:usuario:rwx directorio
```

Ejemplo:

```bash
setfacl -d -m u:juan:rwx proyectos
```

Todo archivo creado dentro de **proyectos** heredará esa ACL.

Consultar:

```bash
getfacl proyectos
```

---

### Copiar ACL

Al copiar archivos es posible conservar las ACL utilizando herramientas como:

```bash
cp --preserve=all origen destino
```

O mediante:

```bash
rsync -A origen destino
```

El parámetro:

```text
-A
```

preserva las listas de control de acceso.

---

### Equivalencia con permisos tradicionales

Permisos clásicos:

```text
Propietario
Grupo
Otros
```

ACL:

```text
Propietario
Grupo
Otros
Usuario adicional
Grupo adicional
ACL por defecto
```

Las ACL amplían el modelo tradicional permitiendo un control mucho más granular.

---

### Diferencias entre permisos tradicionales y ACL

| Permisos tradicionales | ACL |
|-------------------------|-----|
| Solo propietario, grupo y otros. | Permiten múltiples usuarios y grupos adicionales. |
| Configuración sencilla. | Configuración más flexible. |
| Adecuados para entornos simples. | Recomendados en servidores y entornos compartidos. |
| Se gestionan con `chmod`. | Se gestionan con `setfacl` y `getfacl`. |

---

### Buenas prácticas

- Utiliza ACL únicamente cuando los permisos tradicionales no sean suficientes.
- Documenta las ACL aplicadas en servidores compartidos.
- Revisa periódicamente las ACL existentes para evitar accesos innecesarios.
- Utiliza ACL por defecto únicamente cuando sea necesario.
- Elimina ACL antiguas que ya no se utilicen.
- Aplica siempre el principio de mínimo privilegio.

---

[⬆️ Volver al índice](#índice)

## Permisos especiales Linux

Además de los permisos tradicionales (**lectura, escritura y ejecución**), Linux dispone de tres permisos especiales que proporcionan un comportamiento diferente al habitual:

- **SUID (Set User ID)**
- **SGID (Set Group ID)**
- **Sticky Bit**

Estos permisos se utilizan principalmente para controlar cómo se ejecutan programas y cómo se gestionan los archivos compartidos entre varios usuarios.

---

### SUID (Set User ID)

El permiso **SUID** permite que un programa se ejecute con los privilegios del propietario del archivo y no con los del usuario que lo ejecuta.

Es muy utilizado en herramientas del sistema que necesitan realizar operaciones privilegiadas.

---

### Comprobar SUID

Los archivos con SUID muestran una **s** en lugar de la **x** del propietario.

Ejemplo:

```bash
ls -l /usr/bin/passwd
```

Salida:

```text
-rwsr-xr-x 1 root root ...
```

La letra:

```text
s
```

indica que el bit SUID está activado.

---

### Asignar SUID

```bash
chmod u+s archivo
```

Ejemplo:

```bash
chmod u+s programa
```

También puede utilizarse el valor numérico:

```bash
chmod 4755 programa
```

---

### Eliminar SUID

```bash
chmod u-s archivo
```

o

```bash
chmod 0755 archivo
```

---

### SGID (Set Group ID)

El permiso **SGID** tiene dos comportamientos distintos según se aplique a un archivo o a un directorio.

---

### SGID en archivos

Cuando un ejecutable tiene SGID, se ejecuta utilizando el grupo propietario del archivo.

Comprobar:

```bash
ls -l archivo
```

Ejemplo:

```text
-rwxr-sr-x
```

---

### SGID en directorios

Es el uso más habitual.

Cuando un directorio tiene SGID:

- Los nuevos archivos heredan automáticamente el grupo del directorio.
- Todos los usuarios trabajan bajo el mismo grupo.

Esto facilita enormemente el trabajo colaborativo.

---

### Asignar SGID

```bash
chmod g+s directorio
```

Ejemplo:

```bash
chmod g+s proyectos
```

También puede utilizarse:

```bash
chmod 2755 proyectos
```

---

### Eliminar SGID

```bash
chmod g-s directorio
```

---

## Ejemplo práctico

Supongamos un directorio compartido:

```text
/proyectos
```

Grupo propietario:

```text
informatica
```

Activar SGID:

```bash
chmod g+s proyectos
```

Ahora cualquier archivo nuevo creado dentro del directorio pertenecerá automáticamente al grupo:

```text
informatica
```

independientemente del grupo principal del usuario que lo haya creado.

---

### Sticky Bit

El **Sticky Bit** se utiliza casi exclusivamente en directorios compartidos.

Permite que:

- Todos los usuarios puedan crear archivos.
- Cada usuario solo pueda eliminar sus propios archivos.
- El propietario del directorio también pueda eliminarlos.

---

### Comprobar Sticky Bit

Los directorios muestran:

```text
t
```

Ejemplo:

```bash
drwxrwxrwt
```

---

### Asignar Sticky Bit

```bash
chmod +t directorio
```

Ejemplo:

```bash
chmod +t compartido
```

También puede utilizarse:

```bash
chmod 1777 compartido
```

---

### Eliminar Sticky Bit

```bash
chmod -t directorio
```

---<>

### Valores numéricos

Los permisos especiales pueden combinarse con la notación octal.

| Valor | Permiso |
|-------:|----------|
| `1` | Sticky Bit |
| `2` | SGID |
| `4` | SUID |

Ejemplos:

| Permiso | Valor |
|---------|------:|
| SUID | `4755` |
| SGID | `2755` |
| Sticky Bit | `1777` |

También pueden combinarse.

---

### Resumen visual

| Permiso | Archivos | Directorios |
|----------|----------|-------------|
| SUID | Ejecuta como propietario | No suele utilizarse |
| SGID | Ejecuta con el grupo propietario | Hereda el grupo del directorio |
| Sticky Bit | Sin uso habitual | Solo el propietario puede eliminar sus archivos |

---

### Casos de uso habituales

| Permiso | Uso habitual |
|----------|-------------|
| SUID | Programas del sistema (`passwd`, `sudo`, etc.) |
| SGID | Carpetas compartidas entre equipos de trabajo |
| Sticky Bit | Directorios públicos como `/tmp` |

---

### Buenas prácticas

- Utiliza **SUID** únicamente en programas que realmente necesiten privilegios elevados.
- Evita asignar SUID a scripts o ejecutables propios sin analizar previamente los riesgos de seguridad.
- Utiliza **SGID** en directorios compartidos para mantener una administración coherente de grupos.
- Aplica **Sticky Bit** en directorios donde varios usuarios deban crear archivos sin poder eliminar los de otros.
- Revisa periódicamente los archivos con SUID y SGID para detectar posibles riesgos.

---

[⬆️ Volver al índice](#índice)

## ACL en Windows

En Windows, los permisos avanzados se gestionan mediante las **ACL (Access Control Lists)** o **Listas de Control de Acceso**.

A diferencia del modelo tradicional de Linux (propietario, grupo y otros), Windows utiliza un sistema mucho más flexible que permite asignar permisos específicos a:

- Usuarios individuales.
- Grupos.
- Equipos.
- Cuentas del sistema.
- Usuarios autenticados.
- Todos los usuarios.

Las ACL constituyen la base del sistema de permisos **NTFS**.

---

### Componentes de una ACL

Una ACL está formada por una colección de entradas denominadas **ACE (Access Control Entry)**.

Cada ACE indica:

- El usuario o grupo al que se aplica.
- Los permisos concedidos o denegados.
- Si dichos permisos se heredan.

Ejemplo simplificado:

```text
Usuarios
 ├── Administradores → Control total
 ├── Soporte → Modificar
 ├── Ventas → Lectura
 └── Invitados → Sin acceso
```

---

### Consultar permisos desde el Explorador

Para visualizar las ACL de un archivo o carpeta:

1. Clic derecho sobre el recurso.
2. **Propiedades**.
3. **Seguridad**.

Desde esta pestaña pueden verse:

- Usuarios.
- Grupos.
- Permisos asignados.
- Herencia.
- Configuración avanzada.

---

### Permisos NTFS más habituales

Los permisos más utilizados son:

| Permiso | Descripción |
|----------|-------------|
| Control total | Acceso completo al recurso. |
| Modificar | Leer, escribir y eliminar archivos. |
| Lectura y ejecución | Leer archivos y ejecutarlos. |
| Mostrar contenido | Ver el contenido de carpetas. |
| Lectura | Solo permite consultar la información. |
| Escritura | Crear y modificar archivos. |

---

### Configuración avanzada

Desde:

```text
Propiedades
    ↓
Seguridad
    ↓
Opciones avanzadas
```

puede administrarse:

- Propietario.
- Herencia.
- Entradas de permisos.
- Permisos efectivos.
- Auditoría.

Es la herramienta principal para administrar ACL complejas.

---

### Consultar ACL mediante PowerShell

PowerShell permite obtener las ACL utilizando:

```powershell
Get-Acl
```

Ejemplo:

```powershell
Get-Acl C:\Datos
```

Salida simplificada:

```text
Path   : Microsoft.PowerShell.Core\FileSystem::C:\Datos

Owner  : Administradores

Access :

Administradores Allow FullControl
Usuarios Allow ReadAndExecute
```

---

### Mostrar únicamente las entradas

```powershell
(Get-Acl C:\Datos).Access
```

Resultado:

```text
IdentityReference : BUILTIN\Administradores
FileSystemRights  : FullControl

IdentityReference : BUILTIN\Users
FileSystemRights  : ReadAndExecute
```

---

### Modificar permisos mediante PowerShell

Los permisos pueden modificarse utilizando objetos de tipo:

```powershell
FileSystemAccessRule
```

Ejemplo:

```powershell
$acl = Get-Acl "C:\Datos"

$permiso = New-Object System.Security.AccessControl.FileSystemAccessRule(
    "Soporte",
    "Modify",
    "Allow"
)

$acl.AddAccessRule($permiso)

Set-Acl "C:\Datos" $acl
```

Este ejemplo concede permisos de modificación al grupo **Soporte**.

---

### Eliminar permisos

Para eliminar una entrada:

```powershell
$acl.RemoveAccessRule($permiso)

Set-Acl "C:\Datos" $acl
```

---

### Permisos explícitos y heredados

Las ACL distinguen entre:

### Permisos explícitos

Son asignados directamente sobre el recurso.

Ejemplo:

```text
Carpeta Datos

Usuario:
    Juan → Modificar
```

---

### Permisos heredados

Proceden de la carpeta superior.

Ejemplo:

```text
C:\Empresa
    ↓
C:\Empresa\Ventas
    ↓
C:\Empresa\Ventas\Informes
```

Si la herencia está activada, los permisos de **Empresa** llegarán automáticamente hasta **Informes**, salvo que se rompa la herencia.

---

### Permisos de denegación

Windows permite definir permisos de tipo:

```text
Deny
```

Estos permisos tienen prioridad sobre los permisos de tipo:

```text
Allow
```

Ejemplo:

```text
Grupo Ventas → Lectura

Usuario Juan → Denegar lectura
```

Resultado:

```text
Juan NO podrá leer el recurso.
```

---

### Consultar el propietario

PowerShell:

```powershell
(Get-Acl C:\Datos).Owner
```

Ejemplo:

```text
BUILTIN\Administrators
```

---

### Equivalencia

| Acción | Linux | Windows |
|---------|--------|----------|
| Consultar permisos | `getfacl` | `Get-Acl` |
| Modificar permisos | `setfacl` | `Set-Acl` |
| Propietario | `chown` | Owner |
| Permisos especiales | ACL | ACL NTFS |
| Gestión gráfica | No habitual | Explorador de archivos |

---

### Diferencias

| Linux (ACL) | Windows (ACL NTFS) |
|--------------|--------------------|
| Basadas en usuarios y grupos. | Basadas en usuarios, grupos y cuentas del sistema. |
| Se gestionan principalmente mediante comandos. | Disponen de una interfaz gráfica muy completa. |
| Menor número de permisos predefinidos. | Gran variedad de permisos específicos. |
| La herencia suele utilizarse principalmente en directorios. | La herencia es un elemento fundamental del sistema NTFS. |

---

### Buenas prácticas

- Asigna permisos a grupos en lugar de a usuarios individuales siempre que sea posible.
- Utiliza el principio de mínimo privilegio.
- Evita conceder **Control total** cuando no sea estrictamente necesario.
- Revisa periódicamente las ACL de carpetas compartidas.
- Limita el uso de permisos **Deny**, ya que pueden dificultar la administración.
- Documenta los cambios importantes en los permisos.

---

[⬆️ Volver al índice](#índice)

## Herencia de permisos

La **herencia de permisos** es un mecanismo que permite que archivos y carpetas reciban automáticamente los permisos definidos en su carpeta padre.

Su objetivo es simplificar la administración y mantener una estructura de permisos coherente en todo el sistema.

Gracias a la herencia:

- No es necesario configurar permisos manualmente en cada archivo.
- Los nuevos archivos reciben automáticamente los permisos adecuados.
- La administración de grandes estructuras de directorios resulta mucho más sencilla.

Aunque Linux y Windows implementan este concepto de forma diferente, ambos permiten automatizar la asignación de permisos.

---

### Herencia en Linux

En Linux, los permisos tradicionales **no se heredan**.

Por ejemplo:

```text
/proyectos
```

con permisos:

```text
drwxrwx---
```

Si se crea un archivo nuevo:

```text
/proyectos/informe.txt
```

sus permisos dependerán de:

- La **umask** del usuario.
- El programa que crea el archivo.

No heredará automáticamente los permisos del directorio.

---

### Herencia mediante ACL

Para conseguir un comportamiento similar se utilizan las **ACL por defecto**.

Ejemplo:

```bash
setfacl -d -m u:juan:rwx proyectos
```

Comprobar:

```bash
getfacl proyectos
```

Resultado:

```text
default:user:juan:rwx
```

Todo archivo creado dentro del directorio heredará esa ACL.

---

### Herencia del grupo mediante SGID

Otra forma de herencia consiste en utilizar el permiso especial **SGID** sobre un directorio.

Ejemplo:

```bash
chmod g+s proyectos
```

Ahora todos los archivos creados heredarán automáticamente el grupo propietario del directorio.

---

### Herencia en Windows

En Windows la herencia forma parte del propio sistema NTFS.

Cuando una carpeta tiene permisos configurados:

```text
C:\Empresa
```

todas las subcarpetas y archivos pueden heredarlos automáticamente.

Ejemplo:

```text
C:\Empresa
    ↓
C:\Empresa\Ventas
    ↓
C:\Empresa\Ventas\Informes
```

Si la herencia está activada:

- **Ventas** heredará los permisos de **Empresa**.
- **Informes** heredará los permisos de **Ventas**.

---

### Consultar la herencia

Desde el Explorador:

```text
Propiedades
    ↓
Seguridad
    ↓
Opciones avanzadas
```

Aparecerá un indicador similar a:

```text
Heredado de:
C:\Empresa
```

---

### Desactivar la herencia

En las opciones avanzadas puede seleccionarse:

```text
Deshabilitar herencia
```

Windows ofrecerá dos opciones:

- Convertir los permisos heredados en permisos explícitos.
- Eliminar los permisos heredados.

---

### Convertir permisos heredados

Si se elige:

```text
Convertir permisos heredados en permisos explícitos
```

Los permisos actuales se mantienen, pero dejan de depender de la carpeta superior.

Desde ese momento podrán modificarse independientemente.

---

### Eliminar permisos heredados

También puede eliminarse toda la herencia.

Resultado:

```text
Carpeta sin permisos heredados
```

Será necesario asignar manualmente los permisos deseados.

---

### Consultar la herencia mediante PowerShell

Consultar la ACL:

```powershell
Get-Acl C:\Datos
```

Mostrar las entradas:

```powershell
(Get-Acl C:\Datos).Access
```

Entre las propiedades puede encontrarse:

```text
IsInherited
```

Ejemplo:

```text
True
```

Significa que ese permiso procede de la carpeta padre.

---

### Permisos heredados y explícitos

Windows diferencia claramente ambos tipos.

### Permisos heredados

Proceden de una carpeta superior.

Ejemplo:

```text
Usuarios → Lectura

(Heredado)
```

---

### Permisos explícitos

Han sido asignados directamente al recurso.

Ejemplo:

```text
Soporte → Modificar

(Explícito)
```

Los permisos explícitos suelen tener prioridad sobre los heredados cuando existe un conflicto.

---

### Ventajas de la herencia

- Reduce el tiempo de administración.
- Mantiene una estructura coherente.
- Facilita la incorporación de nuevos usuarios.
- Evita errores al crear nuevas carpetas.
- Simplifica el mantenimiento de grandes servidores de archivos.

---

### Inconvenientes

- Puede conceder permisos no deseados si no se revisa correctamente.
- Romper la herencia dificulta la administración si se hace de forma excesiva.
- Es recomendable documentar cualquier excepción.

---

### Comparativa

| Característica | Linux | Windows |
|----------------|--------|----------|
| Herencia en permisos tradicionales | No | Sí |
| Herencia mediante ACL | Sí | Sí |
| Herencia del grupo | SGID | Integrada |
| Herencia de permisos NTFS | No aplica | Integrada |

---

### Buenas prácticas

- Mantén activada la herencia siempre que sea posible.
- Rompe la herencia únicamente cuando exista una necesidad real.
- Revisa periódicamente los permisos heredados.
- Evita crear demasiadas excepciones.
- Documenta cualquier cambio importante en la herencia.
- Utiliza grupos en lugar de usuarios individuales para simplificar la administración.

---

[⬆️ Volver al índice](#índice)

### Permisos efectivos

Los **permisos efectivos** representan los permisos reales que un usuario posee sobre un archivo o carpeta después de evaluar todos los permisos aplicables.

No siempre coinciden con los permisos asignados directamente, ya que pueden verse afectados por factores como:

- Pertenencia a varios grupos.
- Permisos heredados.
- Permisos explícitos.
- Permisos de denegación.
- ACL.

Conocer los permisos efectivos es fundamental para resolver problemas de acceso y verificar si un usuario puede realizar una determinada acción sobre un recurso.

---

### Permisos efectivos en Linux

En Linux, los permisos efectivos se determinan teniendo en cuenta:

1. El propietario del archivo.
2. El grupo propietario.
3. Los grupos a los que pertenece el usuario.
4. Las ACL, si existen.
5. Los permisos tradicionales del archivo.

---

### Consultar los grupos de un usuario

Para comprobar a qué grupos pertenece un usuario:

```bash
groups usuario
```

Ejemplo:

```bash
groups juan
```

Salida:

```text
juan : juan ventas informatica
```

---

### Consultar propietario y permisos

```bash
ls -l informe.txt
```

Ejemplo:

```text
-rw-r----- 1 admin ventas informe.txt
```

Interpretación:

- Propietario (**admin**) → lectura y escritura.
- Grupo (**ventas**) → lectura.
- Otros usuarios → sin acceso.

---

### Consultar ACL

Si el archivo utiliza ACL:

```bash
getfacl informe.txt
```

Ejemplo:

```text
user::rw-
user:juan:rwx
group::r--
mask::rwx
other::---
```

En este caso, aunque **juan** no sea el propietario, tendrá permisos de lectura, escritura y ejecución gracias a la ACL.

---

### Permisos efectivos en Windows

En Windows el cálculo de permisos es más complejo debido a las ACL.

Los permisos efectivos tienen en cuenta:

- Permisos heredados.
- Permisos explícitos.
- Pertenencia a grupos.
- Permisos de denegación.
- Propiedad del recurso.

---

### Consultar permisos efectivos

Desde el Explorador:

```text
Propiedades
    ↓
Seguridad
    ↓
Opciones avanzadas
    ↓
Acceso efectivo
```

Seleccionando un usuario, Windows calcula automáticamente qué permisos posee realmente.

---

### Ejemplo

Supongamos el usuario:

```text
Juan
```

Pertenece a:

```text
Usuarios

Ventas
```

Permisos asignados:

```text
Usuarios → Lectura

Ventas → Modificar
```

Resultado:

```text
Juan podrá modificar el recurso.
```

---

### Influencia de Deny

Los permisos de denegación tienen prioridad sobre los permisos de concesión.

Ejemplo:

```text
Ventas → Modificar

Juan → Denegar escritura
```

Resultado:

```text
Juan no podrá escribir aunque pertenezca al grupo Ventas.
```

---

### Consultar permisos mediante PowerShell

Consultar ACL:

```powershell
Get-Acl C:\Datos
```

Mostrar entradas:

```powershell
(Get-Acl C:\Datos).Access
```

Resultado simplificado:

```text
IdentityReference : Ventas

FileSystemRights : Modify

AccessControlType : Allow
```

Aunque PowerShell permite consultar las ACL, el cálculo exacto de los permisos efectivos depende de la combinación de todas las entradas y suele resultar más sencillo utilizar la herramienta gráfica de **Acceso efectivo** cuando se necesita analizar un caso concreto.

---

### Orden de evaluación

### Linux

El sistema evalúa los permisos en este orden:

1. ¿El usuario es el propietario?
2. ¿Existe una ACL específica para el usuario?
3. ¿Pertenece al grupo propietario?
4. ¿Existe una ACL para alguno de sus grupos?
5. Se aplican los permisos de "otros".

---

### Windows

Windows evalúa principalmente:

1. Permisos explícitos.
2. Permisos heredados.
3. Permisos procedentes de grupos.
4. Permisos de denegación.
5. Resultado final (permisos efectivos).

---

### Comparativa

| Característica | Linux | Windows |
|----------------|--------|----------|
| Propietario | Sí | Sí |
| Grupos | Sí | Sí |
| ACL | Opcional | Integrada en NTFS |
| Herencia | Solo mediante ACL | Integrada |
| Permisos de denegación | No existen como tal | Sí (`Deny`) |
| Cálculo automático | Manual | Herramienta de "Acceso efectivo" |

---

### Buenas prácticas

- Comprueba siempre los permisos efectivos cuando un usuario tenga problemas de acceso.
- Asigna permisos preferentemente a grupos y no a usuarios individuales.
- Evita utilizar permisos de denegación salvo que sea imprescindible.
- Revisa periódicamente las ACL en recursos compartidos.
- Documenta cualquier excepción en la asignación de permisos.
- Aplica siempre el principio de mínimo privilegio.

---

[⬆️ Volver al índice](#índice)

## Delegación de permisos

La **delegación de permisos** consiste en conceder a un usuario o grupo la capacidad de realizar determinadas tareas administrativas sin otorgarle privilegios completos sobre el sistema.

Su objetivo es aplicar el **principio de mínimo privilegio**, permitiendo que cada usuario disponga únicamente de los permisos necesarios para desempeñar su trabajo.

La delegación es habitual en entornos empresariales para:

- Administrar carpetas compartidas.
- Gestionar impresoras.
- Reiniciar servicios.
- Administrar usuarios concretos.
- Ejecutar tareas específicas.
- Gestionar determinados recursos sin ser administrador del sistema.

---

### Delegación en Linux

Linux permite delegar permisos de diferentes formas dependiendo de la tarea que se quiera realizar.

Las más habituales son:

- Cambiar propietarios y grupos.
- Utilizar ACL.
- Configurar **sudo**.
- Asignar capacidades (*Linux Capabilities*).

---

### Delegación mediante grupos

La forma más sencilla consiste en utilizar grupos.

Ejemplo:

```text
Grupo: backup
```

Todos los usuarios pertenecientes a ese grupo podrán acceder a los recursos asociados.

Añadir un usuario:

```bash
sudo usermod -aG backup juan
```

Comprobar:

```bash
groups juan
```

---

### Delegación mediante ACL

También pueden delegarse permisos únicamente sobre determinados recursos.

Ejemplo:

```bash
setfacl -m u:juan:rwx /datos
```

Juan podrá administrar esa carpeta sin convertirse en propietario.

---

##### Delegación mediante sudo

La herramienta **sudo** permite ejecutar determinados comandos con privilegios elevados.

El archivo de configuración es:

```text
/etc/sudoers
```

Debe modificarse mediante:

```bash
visudo
```

---

### Permitir todos los comandos

Ejemplo:

```text
juan ALL=(ALL) ALL
```

El usuario podrá utilizar:

```bash
sudo
```

para ejecutar cualquier comando autorizado.

---

### Permitir un único comando

También es posible limitar los comandos disponibles.

Ejemplo:

```text
juan ALL=(ALL) /usr/bin/systemctl restart apache2
```

El usuario únicamente podrá reiniciar el servicio Apache.

---

### Linux Capabilities

Linux también permite asignar privilegios concretos a programas sin utilizar SUID.

Consultar capacidades:

```bash
getcap archivo
```

Asignar una capacidad:

```bash
setcap cap_net_bind_service=+ep programa
```

Este mecanismo permite aplicar permisos muy específicos de forma más segura que SUID.

---

### Delegación en Windows

Windows ofrece múltiples mecanismos para delegar tareas administrativas.

Los más habituales son:

- Grupos locales.
- Grupos de Active Directory.
- ACL.
- Políticas de seguridad.
- Delegación administrativa en Active Directory.

---

### Delegación mediante grupos

La recomendación general consiste en asignar permisos a grupos y no a usuarios individuales.

Ejemplo:

```text
Grupo:

Soporte IT
```

Permisos:

```text
Modificar

Carpeta Compartida
```

Todos los miembros del grupo heredarán dichos permisos.

---

### Delegación sobre carpetas

Desde:

```text
Propiedades
    ↓
Seguridad
```

pueden concederse permisos como:

- Lectura.
- Escritura.
- Modificación.
- Control total.

A un grupo determinado.

---

### Delegación mediante Active Directory

En entornos con Active Directory es posible delegar tareas concretas.

Ejemplos:

- Restablecer contraseñas.
- Crear usuarios.
- Desbloquear cuentas.
- Administrar una OU específica.
- Gestionar grupos.

Esto se realiza mediante el asistente de **Delegación de control**.

Ruta:

```text
Usuarios y equipos de Active Directory

↓

Unidad organizativa

↓

Delegar control
```

---

### Delegación mediante GPO

Las **Directivas de Grupo (GPO)** permiten delegar determinadas configuraciones sin otorgar privilegios administrativos completos.

Ejemplos:

- Instalar software.
- Configurar impresoras.
- Ejecutar scripts.
- Configurar el escritorio.
- Administrar políticas de seguridad.

---

### Delegación mediante PowerShell

PowerShell permite administrar permisos mediante cmdlets como:

```powershell
Get-Acl
```

```powershell
Set-Acl
```

También puede utilizarse junto con módulos específicos como:

```powershell
ActiveDirectory
```

Ejemplo:

```powershell
Get-ADUser

New-ADUser

Set-ADUser
```

Siempre que el usuario disponga de los permisos delegados correspondientes.

---

### Comparativa

| Método | Linux | Windows |
|---------|--------|----------|
| Grupos | Sí | Sí |
| ACL | Sí | Sí |
| Permisos elevados | `sudo` | Grupos administrativos / UAC |
| Delegación parcial | `sudoers`, ACL, Capabilities | ACL, GPO, Active Directory |
| Administración centralizada | Limitada | Active Directory |

---

### Buenas prácticas

- Aplica siempre el **principio de mínimo privilegio**.
- Asigna permisos a grupos antes que a usuarios individuales.
- Limita el uso de cuentas con privilegios administrativos.
- Revisa periódicamente las delegaciones existentes.
- Documenta todas las delegaciones importantes.
- Utiliza `sudo` o la delegación de Active Directory en lugar de otorgar permisos de administrador completos.
- Elimina permisos delegados cuando ya no sean necesarios.

---

[⬆️ Volver al índice](#índice)

## Auditoría de permisos

La **auditoría de permisos** consiste en revisar y supervisar quién tiene acceso a un recurso, qué acciones puede realizar y quién ha accedido realmente a dicho recurso.

Su objetivo es:

- Detectar permisos excesivos.
- Identificar accesos no autorizados.
- Cumplir requisitos de seguridad y normativas.
- Facilitar investigaciones tras un incidente.
- Mantener un control sobre los recursos críticos.

La auditoría puede centrarse en:

- Permisos asignados.
- Cambios en los permisos.
- Accesos realizados.
- Modificaciones de archivos.
- Eliminaciones.

---

### Auditoría en Linux

Linux dispone de varias herramientas para auditar permisos y accesos.

Las más utilizadas son:

- `ls`
- `getfacl`
- `find`
- `auditd`
- Registros del sistema.

---

### Revisar permisos

Consultar permisos tradicionales:

```bash
ls -l
```

Ejemplo:

```bash
ls -l /datos
```

---

### Revisar ACL

Consultar las ACL:

```bash
getfacl archivo
```

Ejemplo:

```bash
getfacl informe.txt
```

---

### Buscar archivos con permisos especiales

Buscar archivos con SUID:

```bash
find / -perm -4000 2>/dev/null
```

Buscar archivos con SGID:

```bash
find / -perm -2000 2>/dev/null
```

Buscar Sticky Bit:

```bash
find / -perm -1000 2>/dev/null
```

Estos comandos ayudan a localizar posibles riesgos de seguridad.

---

### Buscar archivos con permisos 777

Los permisos:

```text
777
```

permiten acceso completo a cualquier usuario y suelen representar un riesgo.

Buscar:

```bash
find / -type f -perm 777 2>/dev/null
```

---

### Auditd

Linux dispone del sistema de auditoría:

```text
auditd
```

Permite registrar:

- Accesos a archivos.
- Cambios de permisos.
- Ejecución de comandos.
- Cambios de configuración.
- Eventos de seguridad.

Comprobar estado:

```bash
systemctl status auditd
```

Consultar registros:

```bash
ausearch
```

Ejemplo:

```bash
ausearch -k permisos
```

---

### Auditoría en Windows

Windows integra un completo sistema de auditoría mediante:

- Auditoría de seguridad.
- Directivas de Grupo (GPO).
- Visor de eventos.
- PowerShell.

---

### Visor de eventos

Ruta:

```text
Visor de eventos

↓

Registros de Windows

↓

Seguridad
```

Aquí pueden consultarse eventos relacionados con:

- Inicio de sesión.
- Acceso a archivos.
- Cambios de permisos.
- Creación de usuarios.
- Eliminación de objetos.

---

### Activar auditoría

La auditoría de objetos puede habilitarse mediante:

```text
Directiva de seguridad local

↓

Directivas locales

↓

Directiva de auditoría
```

O mediante GPO.

---

### Auditoría sobre una carpeta

Pasos:

```text
Propiedades

↓

Seguridad

↓

Opciones avanzadas

↓

Auditoría
```

Desde esta pestaña es posible definir:

- Qué usuarios serán auditados.
- Qué acciones se registrarán.
- Sobre qué operaciones.

Ejemplo:

- Lectura.
- Escritura.
- Eliminación.
- Cambio de permisos.

---

### Consultar permisos mediante PowerShell

Obtener ACL:

```powershell
Get-Acl C:\Datos
```

Mostrar únicamente las entradas:

```powershell
(Get-Acl C:\Datos).Access
```

---

### Revisar eventos

PowerShell permite consultar eventos del sistema.

Ejemplo:

```powershell
Get-WinEvent -LogName Security
```

Consultar los últimos eventos:

```powershell
Get-WinEvent -LogName Security -MaxEvents 20
```

---

### ¿Qué conviene revisar?

Una auditoría periódica debería comprobar:

- Usuarios con privilegios elevados.
- Recursos compartidos.
- ACL innecesarias.
- Permisos heredados incorrectos.
- Archivos con permisos especiales.
- Cuentas inactivas con acceso.
- Carpetas accesibles por "Todos" o "Everyone".

---

### Comparativa

| Acción | Linux | Windows |
|---------|--------|----------|
| Revisar permisos | `ls -l` | Propiedades → Seguridad |
| Revisar ACL | `getfacl` | `Get-Acl` |
| Auditoría integrada | `auditd` | Auditoría NTFS |
| Consultar eventos | `/var/log` | Visor de eventos |
| Buscar permisos especiales | `find` | PowerShell |

---

### Buenas prácticas

- Realiza auditorías de permisos de forma periódica.
- Revisa especialmente los recursos compartidos.
- Elimina permisos que ya no sean necesarios.
- Controla el uso de permisos especiales como **SUID**, **SGID** y **Control total**.
- Supervisa los cambios realizados sobre recursos críticos.
- Registra las modificaciones importantes para facilitar futuras investigaciones.
- Automatiza la revisión de permisos mediante scripts cuando sea posible.
- Aplica siempre el principio de mínimo privilegio.

---

[⬆️ Volver al índice](#índice)

## Buenas prácticas

Una correcta gestión de permisos es esencial para proteger la información, reducir riesgos de seguridad y facilitar la administración de sistemas.

Una configuración incorrecta puede provocar:

- Accesos no autorizados.
- Pérdida o modificación de datos.
- Escaladas de privilegios.
- Dificultades para administrar recursos compartidos.
- Incumplimiento de políticas o normativas de seguridad.

Aplicar buenas prácticas ayuda a mantener un entorno más seguro, ordenado y fácil de mantener.

---

### Aplicar el principio de mínimo privilegio

Cada usuario debe disponer únicamente de los permisos necesarios para realizar su trabajo.

Evita conceder permisos adicionales "por si acaso".

✔ Correcto:

```text
Usuario de contabilidad

↓

Lectura y modificación únicamente en la carpeta Contabilidad
```

✘ Incorrecto:

```text
Usuario de contabilidad

↓

Control total sobre todo el servidor
```

---

### Asignar permisos a grupos

Siempre que sea posible, asigna permisos a grupos en lugar de a usuarios individuales.

Ejemplo:

```text
Grupo:

Finanzas
```

En lugar de:

```text
Juan

María

Pedro

Laura
```

Ventajas:

- Administración más sencilla.
- Menor número de errores.
- Incorporación rápida de nuevos usuarios.
- Eliminación más sencilla de accesos.

---

### Evitar permisos excesivos

Los permisos como:

```text
777
```

en Linux o:

```text
Control total
```

en Windows solo deben utilizarse cuando sean realmente necesarios.

Concede siempre el menor nivel de acceso posible.

---

### Revisar periódicamente los permisos

Es recomendable realizar auditorías periódicas para detectar:

- Usuarios que ya no necesitan acceso.
- Permisos duplicados.
- ACL innecesarias.
- Recursos compartidos demasiado abiertos.
- Archivos con permisos especiales.

---

### Utilizar la herencia correctamente

Siempre que sea posible:

- Mantén activada la herencia.
- Evita romperla salvo que exista una necesidad concreta.
- Documenta cualquier excepción.

Una estructura coherente facilita enormemente la administración.

---

### Limitar el uso de permisos especiales

En Linux:

- Revisa periódicamente los archivos con **SUID**.
- Utiliza **SGID** únicamente en directorios compartidos cuando sea necesario.
- Aplica **Sticky Bit** en directorios públicos como `/tmp`.

En Windows:

- Evita utilizar **Deny** salvo que sea imprescindible.
- Limita el uso de **Control total**.

---

### Documentar los cambios

Cualquier modificación importante en los permisos debería quedar registrada.

Por ejemplo:

- Fecha.
- Administrador responsable.
- Recurso afectado.
- Motivo del cambio.

Esto facilita futuras auditorías y la resolución de incidencias.

---

### Auditar los recursos críticos

Los recursos más sensibles deberían revisarse con mayor frecuencia.

Ejemplos:

- Servidores de archivos.
- Copias de seguridad.
- Bases de datos.
- Carpetas de recursos humanos.
- Información financiera.
- Documentación técnica.

---

### Automatizar las comprobaciones

Siempre que sea posible, utiliza scripts para revisar permisos de forma periódica.

Ejemplos:

Linux:

```bash
find /datos -perm -777
```

Windows:

```powershell
Get-Acl C:\Compartido
```

La automatización ayuda a detectar problemas antes de que afecten al entorno.

---

### Eliminar permisos innecesarios

Cuando un usuario cambia de departamento o abandona la organización:

- Elimina sus permisos.
- Revisa los grupos a los que pertenece.
- Comprueba las ACL asociadas.

No es recomendable conservar permisos que ya no sean necesarios.

---

### Utilizar cuentas administrativas únicamente cuando sea necesario

Las tareas diarias deberían realizarse con cuentas estándar.

Las cuentas con privilegios elevados deben utilizarse únicamente para:

- Instalaciones.
- Cambios de configuración.
- Administración del sistema.
- Resolución de incidencias.

Esto reduce el riesgo de errores y mejora la seguridad.

---

### Resumen de recomendaciones

| Recomendación | Beneficio |
|---------------|-----------|
| Aplicar el principio de mínimo privilegio | Reduce la superficie de ataque. |
| Utilizar grupos | Simplifica la administración. |
| Revisar permisos periódicamente | Detecta configuraciones incorrectas. |
| Auditar recursos críticos | Mejora la trazabilidad. |
| Documentar cambios | Facilita el mantenimiento y las investigaciones. |
| Automatizar revisiones | Reduce errores y ahorra tiempo. |
| Limitar permisos especiales | Disminuye riesgos de seguridad. |
| Eliminar permisos obsoletos | Evita accesos innecesarios. |

---

[⬆️ Volver al índice](#índice)