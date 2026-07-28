# Usuarios y grupos

## Introducción

Los usuarios y grupos permiten organizar y controlar el acceso a los recursos del sistema.

Cada usuario dispone de una identidad propia, mientras que los grupos facilitan la asignación de permisos a varios usuarios de forma simultánea.

Administrar correctamente usuarios y grupos es una tarea esencial para mantener la seguridad, el orden y el correcto funcionamiento de equipos y servidores.

En este capítulo aprenderás a consultar, crear, modificar y eliminar usuarios y grupos tanto en Linux como en PowerShell.

---

## Índice

- [Listar usuarios](#listar-usuarios)
- [Consultar información de un usuario](#consultar-información-de-un-usuario)
- [Crear un usuario](#crear-un-usuario)
- [Eliminar un usuario](#eliminar-un-usuario)
- [Listar grupos](#listar-grupos)
- [Crear un grupo](#crear-un-grupo)
- [Agregar un usuario a un grupo](#agregar-un-usuario-a-un-grupo)
- [Eliminar un usuario de un grupo](#eliminar-un-usuario-de-un-grupo)
- [Resumen de equivalencias](#resumen-de-equivalencias)

---

## Listar usuarios

### Linux

```bash
cat /etc/passwd
```

También puede utilizarse:

```bash
getent passwd
```

**Descripción**

Permite mostrar todos los usuarios registrados en el sistema.

- `cat /etc/passwd` muestra el contenido del archivo donde se almacenan los usuarios locales.
- `getent passwd` consulta la base de datos de usuarios del sistema, incluyendo usuarios obtenidos mediante servicios como LDAP o NIS si están configurados.

---

### PowerShell

```powershell
Get-LocalUser
```

**Descripción**

Muestra todos los usuarios locales del equipo, indicando información como:

- Nombre.
- Estado de la cuenta.
- Descripción.
- Fecha de creación (según la versión de Windows).

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Listar usuarios locales | `cat /etc/passwd` / `getent passwd` | `Get-LocalUser` |

---

### Ejemplos

**Mostrar todos los usuarios del sistema**

Linux

```bash
cat /etc/passwd
```

PowerShell

```powershell
Get-LocalUser
```

---

**Buscar un usuario concreto**

Linux

```bash
cat /etc/passwd | grep beatriz
```

PowerShell

```powershell
Get-LocalUser beatriz
```

---

**Mostrar únicamente los nombres de usuario**

Linux

```bash
cut -d: -f1 /etc/passwd
```

PowerShell

```powershell
Get-LocalUser |
Select-Object Name
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Los usuarios se almacenan en `/etc/passwd`. | Los usuarios se almacenan en la base de datos de cuentas locales de Windows. |
| `getent` puede mostrar usuarios procedentes de otros servicios de autenticación. | `Get-LocalUser` únicamente muestra usuarios locales. |
| La salida es texto estructurado. | La salida son objetos que pueden filtrarse y ordenarse fácilmente. |

---

### Buenas prácticas

- Comprueba periódicamente qué usuarios existen en el sistema.
- Elimina o deshabilita las cuentas que ya no sean necesarias.
- Evita utilizar cuentas compartidas entre varios usuarios.
- Revisa que únicamente existan cuentas con privilegios administrativos cuando sea realmente necesario.

---

### Comandos relacionados

- [Consultar información de un usuario](#consultar-información-de-un-usuario)
- [Crear un usuario](#crear-un-usuario)
- [Eliminar un usuario](#eliminar-un-usuario)

---

[⬆️ Volver al índice](#índice)

## Consultar información de un usuario

### Linux

```bash
id <usuario>
```

También puede utilizarse:

```bash
finger <usuario>
```

(si está instalado)

**Descripción**

Permite consultar información detallada de un usuario, como:

- UID (Identificador de usuario).
- GID (Grupo principal).
- Grupos a los que pertenece.
- Nombre del usuario.

---

### PowerShell

```powershell
Get-LocalUser <usuario>
```

También puede utilizarse:

```powershell
Get-LocalGroupMember <grupo>
```

para comprobar la pertenencia a un grupo concreto.

**Descripción**

Permite consultar la información de un usuario local, incluyendo:

- Nombre.
- Estado de la cuenta.
- Descripción.
- Información básica de la cuenta.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Consultar información de un usuario | `id` | `Get-LocalUser` |

---

### Ejemplos

**Consultar un usuario concreto**

Linux

```bash
id beatriz
```

PowerShell

```powershell
Get-LocalUser beatriz
```

---

**Consultar el usuario actual**

Linux

```bash
id
```

PowerShell

```powershell
Get-LocalUser $env:USERNAME
```

---

**Consultar los grupos a los que pertenece un usuario**

Linux

```bash
id beatriz
```

PowerShell

```powershell
Get-LocalGroup |
ForEach-Object {
    Get-LocalGroupMember $_.Name -ErrorAction SilentlyContinue |
    Where-Object {$_.Name -like "*beatriz*"}
}
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `id` muestra el UID, GID y todos los grupos del usuario. | `Get-LocalUser` muestra únicamente la información de la cuenta. |
| Toda la información aparece en un único comando. | Para conocer los grupos suele ser necesario consultar los miembros de los grupos locales. |
| La salida es texto estructurado. | La salida son objetos que pueden filtrarse y procesarse mediante la tubería. |

---

### Buenas prácticas

- Comprueba siempre a qué grupos pertenece un usuario antes de modificar sus permisos.
- Verifica el UID y el grupo principal cuando administres usuarios en Linux.
- Revisa periódicamente las cuentas con privilegios administrativos.
- Mantén actualizada la información descriptiva de las cuentas cuando sea posible.

---

### Comandos relacionados

- [Listar usuarios](#listar-usuarios)
- [Crear un usuario](#crear-un-usuario)
- [Agregar un usuario a un grupo](#agregar-un-usuario-a-un-grupo)

---

[⬆️ Volver al índice](#índice)

## Crear un usuario

### Linux

```bash
sudo useradd <usuario>
```

También puede utilizarse:

```bash
sudo adduser <usuario>
```

**Descripción**

Permite crear un nuevo usuario en el sistema.

- `useradd` crea la cuenta con la configuración básica.
- `adduser` (disponible en muchas distribuciones) es un asistente interactivo que facilita la creación del usuario.

---

### PowerShell

```powershell
New-LocalUser -Name <usuario>
```

**Descripción**

Crea un nuevo usuario local en el equipo.

Es posible especificar una contraseña, una descripción y otras propiedades durante su creación.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Crear un usuario | `useradd` / `adduser` | `New-LocalUser` |

---

### Ejemplos

**Crear un usuario**

Linux

```bash
sudo adduser beatriz
```

PowerShell

```powershell
New-LocalUser -Name "beatriz"
```

---

**Crear un usuario con directorio personal**

Linux

```bash
sudo useradd -m beatriz
```

PowerShell

```powershell
New-LocalUser -Name "beatriz"
```

---

**Crear un usuario con una descripción**

Linux

```bash
sudo useradd -m -c "Usuario de desarrollo" beatriz
```

PowerShell

```powershell
New-LocalUser `
-Name "beatriz" `
-Description "Usuario de desarrollo"
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `useradd` crea la cuenta de forma básica. | `New-LocalUser` crea un usuario local de Windows. |
| `adduser` guía al administrador mediante un asistente interactivo. | La creación suele realizarse indicando los parámetros necesarios en el cmdlet. |
| Puede crearse automáticamente el directorio personal mediante `-m`. | El perfil del usuario se crea automáticamente cuando inicia sesión por primera vez. |

---

### Buenas prácticas

- Utiliza nombres de usuario claros y fáciles de identificar.
- Asigna una descripción cuando el usuario vaya a administrarse durante largo tiempo.
- Evita utilizar cuentas compartidas entre varias personas.
- Comprueba que el usuario se ha creado correctamente antes de asignarle permisos o grupos.

---

### Comandos relacionados

- [Listar usuarios](#listar-usuarios)
- [Eliminar un usuario](#eliminar-un-usuario)
- [Agregar un usuario a un grupo](#agregar-un-usuario-a-un-grupo)

---

[⬆️ Volver al índice](#índice)

## Eliminar un usuario

### Linux

```bash
sudo userdel <usuario>
```

También puede utilizarse:

```bash
sudo userdel -r <usuario>
```

**Descripción**

Permite eliminar un usuario del sistema.

- `userdel` elimina únicamente la cuenta.
- `userdel -r` elimina la cuenta y su directorio personal.

---

### PowerShell

```powershell
Remove-LocalUser -Name <usuario>
```

**Descripción**

Elimina un usuario local del equipo.

La eliminación de la cuenta no elimina automáticamente su perfil de usuario ni los archivos almacenados en su directorio personal.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Eliminar un usuario | `userdel` | `Remove-LocalUser` |

---

### Ejemplos

**Eliminar un usuario**

Linux

```bash
sudo userdel beatriz
```

PowerShell

```powershell
Remove-LocalUser -Name "beatriz"
```

---

**Eliminar un usuario y su directorio personal**

Linux

```bash
sudo userdel -r beatriz
```

PowerShell

```powershell
Remove-LocalUser -Name "beatriz"
```

---

**Comprobar que el usuario ha sido eliminado**

Linux

```bash
id beatriz
```

PowerShell

```powershell
Get-LocalUser beatriz
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `userdel` elimina la cuenta del usuario. | `Remove-LocalUser` elimina la cuenta local del usuario. |
| `userdel -r` también elimina el directorio personal. | El perfil del usuario y sus archivos no se eliminan automáticamente. |
| Generalmente requiere privilegios de administrador (`sudo`). | Requiere ejecutar PowerShell con permisos de administrador. |

---

### Buenas prácticas

- Verifica que el usuario ya no necesita acceder al sistema antes de eliminarlo.
- Realiza una copia de seguridad de la información importante del usuario si es necesario.
- Comprueba que el usuario no está ejecutando procesos antes de eliminar la cuenta.
- Elimina únicamente las cuentas que ya no vayan a utilizarse.

---

### Comandos relacionados

- [Listar usuarios](#listar-usuarios)
- [Crear un usuario](#crear-un-usuario)
- [Consultar información de un usuario](#consultar-información-de-un-usuario)

---

> **⚠️ Advertencia:** La eliminación de un usuario puede provocar la pérdida de acceso a archivos y recursos. Antes de eliminar una cuenta, asegúrate de conservar la información que pueda ser necesaria.

---

[⬆️ Volver al índice](#índice)

## Listar grupos

### Linux

```bash
cat /etc/group
```

También puede utilizarse:

```bash
getent group
```

**Descripción**

Permite mostrar todos los grupos registrados en el sistema.

- `cat /etc/group` muestra el contenido del archivo donde se almacenan los grupos locales.
- `getent group` consulta la base de datos de grupos del sistema, incluyendo grupos obtenidos mediante servicios como LDAP o NIS si están configurados.

---

### PowerShell

```powershell
Get-LocalGroup
```

**Descripción**

Muestra todos los grupos locales del equipo.

La salida incluye información como:

- Nombre del grupo.
- Descripción.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Listar grupos | `cat /etc/group` / `getent group` | `Get-LocalGroup` |

---

### Ejemplos

**Mostrar todos los grupos**

Linux

```bash
cat /etc/group
```

PowerShell

```powershell
Get-LocalGroup
```

---

**Buscar un grupo concreto**

Linux

```bash
cat /etc/group | grep desarrolladores
```

PowerShell

```powershell
Get-LocalGroup desarrolladores
```

---

**Mostrar únicamente el nombre de los grupos**

Linux

```bash
cut -d: -f1 /etc/group
```

PowerShell

```powershell
Get-LocalGroup |
Select-Object Name
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Los grupos se almacenan en `/etc/group`. | Los grupos se almacenan en la base de datos de grupos locales de Windows. |
| `getent` puede mostrar grupos procedentes de otros servicios de autenticación. | `Get-LocalGroup` únicamente muestra grupos locales. |
| La salida es texto estructurado. | La salida son objetos que pueden filtrarse y ordenarse fácilmente. |

---

### Buenas prácticas

- Utiliza grupos para administrar permisos en lugar de asignarlos directamente a cada usuario.
- Mantén una estructura de grupos clara y coherente.
- Elimina los grupos que ya no sean necesarios.
- Revisa periódicamente qué grupos existen en el sistema.

---

### Comandos relacionados

- [Crear un grupo](#crear-un-grupo)
- [Agregar un usuario a un grupo](#agregar-un-usuario-a-un-grupo)
- [Eliminar un usuario de un grupo](#eliminar-un-usuario-de-un-grupo)

---

[⬆️ Volver al índice](#índice)

## Crear un grupo

### Linux

```bash
sudo groupadd <grupo>
```

**Descripción**

Permite crear un nuevo grupo en el sistema.

Los grupos se utilizan para organizar usuarios y facilitar la asignación de permisos sobre archivos, directorios y otros recursos.

---

### PowerShell

```powershell
New-LocalGroup -Name <grupo>
```

**Descripción**

Crea un nuevo grupo local en el equipo.

Opcionalmente puede añadirse una descripción para facilitar su identificación.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Crear un grupo | `groupadd` | `New-LocalGroup` |

---

### Ejemplos

**Crear un grupo**

Linux

```bash
sudo groupadd desarrolladores
```

PowerShell

```powershell
New-LocalGroup -Name "desarrolladores"
```

---

**Crear un grupo con una descripción**

Linux

```bash
sudo groupadd administradores
```

PowerShell

```powershell
New-LocalGroup `
-Name "administradores" `
-Description "Grupo de administradores del sistema"
```

---

**Comprobar que el grupo se ha creado correctamente**

Linux

```bash
getent group desarrolladores
```

PowerShell

```powershell
Get-LocalGroup desarrolladores
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `groupadd` crea un nuevo grupo local. | `New-LocalGroup` crea un grupo local de Windows. |
| El grupo puede utilizarse posteriormente para asignar permisos y pertenencias. | El grupo puede utilizarse para administrar permisos y agregar usuarios. |
| Generalmente requiere privilegios de administrador (`sudo`). | Requiere ejecutar PowerShell con permisos de administrador. |

---

### Buenas prácticas

- Utiliza nombres descriptivos y coherentes para los grupos.
- Agrupa usuarios con funciones similares en lugar de crear grupos para cada usuario.
- Añade una descripción cuando el grupo vaya a utilizarse durante largo tiempo.
- Revisa periódicamente los grupos existentes para eliminar aquellos que ya no sean necesarios.

---

### Comandos relacionados

- [Listar grupos](#listar-grupos)
- [Agregar un usuario a un grupo](#agregar-un-usuario-a-un-grupo)
- [Eliminar un usuario de un grupo](#eliminar-un-usuario-de-un-grupo)

---

[⬆️ Volver al índice](#índice)

## Agregar un usuario a un grupo

### Linux

```bash
sudo usermod -aG <grupo> <usuario>
```

También puede utilizarse:

```bash
sudo gpasswd -a <usuario> <grupo>
```

**Descripción**

Permite agregar un usuario a uno o varios grupos existentes.

- `usermod -aG` añade el usuario al grupo indicado sin eliminar su pertenencia a otros grupos.
- `gpasswd -a` ofrece una forma alternativa de añadir usuarios a un grupo.

> **Importante:** La opción `-a` (append) debe utilizarse siempre junto con `-G`. Si se omite `-a`, el usuario dejará de pertenecer a los grupos secundarios que ya tuviera asignados.

---

### PowerShell

```powershell
Add-LocalGroupMember -Group <grupo> -Member <usuario>
```

**Descripción**

Agrega un usuario a un grupo local del sistema.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Agregar un usuario a un grupo | `usermod -aG` / `gpasswd -a` | `Add-LocalGroupMember` |

---

### Ejemplos

**Agregar el usuario `beatriz` al grupo `desarrolladores`**

Linux

```bash
sudo usermod -aG desarrolladores beatriz
```

PowerShell

```powershell
Add-LocalGroupMember `
-Group "desarrolladores" `
-Member "beatriz"
```

---

**Agregar el usuario a varios grupos**

Linux

```bash
sudo usermod -aG desarrolladores,docker beatriz
```

PowerShell

```powershell
Add-LocalGroupMember -Group "desarrolladores" -Member "beatriz"

Add-LocalGroupMember -Group "docker" -Member "beatriz"
```

---

**Comprobar que el usuario pertenece al grupo**

Linux

```bash
id beatriz
```

PowerShell

```powershell
Get-LocalGroupMember desarrolladores
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `usermod -aG` permite agregar uno o varios grupos en un único comando. | `Add-LocalGroupMember` agrega el usuario a un grupo cada vez. |
| `gpasswd -a` también permite añadir usuarios a grupos. | Solo existe un cmdlet específico para agregar miembros a grupos locales. |
| Normalmente es necesario cerrar y volver a iniciar sesión para que el usuario obtenga los nuevos permisos del grupo. | En algunos casos también será necesario cerrar sesión para aplicar completamente los cambios. |

---

### Buenas prácticas

- Utiliza siempre `-aG` con `usermod` para evitar eliminar otros grupos del usuario.
- Asigna los permisos mediante grupos en lugar de hacerlo usuario por usuario.
- Comprueba la pertenencia al grupo después de realizar el cambio.
- Agrega únicamente a los usuarios que realmente necesiten los permisos del grupo.

---

### Comandos relacionados

- [Consultar información de un usuario](#consultar-información-de-un-usuario)
- [Crear un grupo](#crear-un-grupo)
- [Eliminar un usuario de un grupo](#eliminar-un-usuario-de-un-grupo)

---

> **⚠️ Advertencia:** En Linux, ejecutar `usermod -G grupo usuario` **sin la opción `-a`** reemplaza todos los grupos secundarios del usuario por el grupo indicado. Es uno de los errores más comunes al administrar usuarios.

---

[⬆️ Volver al índice](#índice)

## Eliminar un usuario de un grupo

### Linux

```bash
sudo gpasswd -d <usuario> <grupo>
```

También puede utilizarse:

```bash
sudo deluser <usuario> <grupo>
```

(disponible en muchas distribuciones)

**Descripción**

Permite eliminar la pertenencia de un usuario a un grupo.

El usuario seguirá existiendo en el sistema, pero dejará de pertenecer al grupo indicado.

---

### PowerShell

```powershell
Remove-LocalGroupMember -Group <grupo> -Member <usuario>
```

**Descripción**

Elimina un usuario de un grupo local.

La cuenta del usuario no se elimina; únicamente deja de pertenecer al grupo especificado.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Eliminar un usuario de un grupo | `gpasswd -d` / `deluser usuario grupo` | `Remove-LocalGroupMember` |

---

### Ejemplos

**Eliminar el usuario `beatriz` del grupo `desarrolladores`**

Linux

```bash
sudo gpasswd -d beatriz desarrolladores
```

PowerShell

```powershell
Remove-LocalGroupMember `
-Group "desarrolladores" `
-Member "beatriz"
```

---

**Eliminar el usuario de varios grupos**

Linux

```bash
sudo gpasswd -d beatriz desarrolladores

sudo gpasswd -d beatriz docker
```

PowerShell

```powershell
Remove-LocalGroupMember -Group "desarrolladores" -Member "beatriz"

Remove-LocalGroupMember -Group "docker" -Member "beatriz"
```

---

**Comprobar que el usuario ya no pertenece al grupo**

Linux

```bash
id beatriz
```

PowerShell

```powershell
Get-LocalGroupMember desarrolladores
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `gpasswd -d` elimina la pertenencia a un grupo. | `Remove-LocalGroupMember` elimina al usuario del grupo indicado. |
| El usuario continúa existiendo en el sistema. | La cuenta del usuario también continúa existiendo. |
| Es posible utilizar `deluser usuario grupo` en muchas distribuciones. | Solo existe un cmdlet específico para eliminar miembros de grupos locales. |

---

### Buenas prácticas

- Comprueba que el usuario realmente ya no necesita los permisos del grupo.
- Verifica la pertenencia del usuario después de realizar el cambio.
- Evita eliminar usuarios de grupos críticos sin conocer el impacto.
- Mantén actualizada la pertenencia a grupos para aplicar correctamente el principio de mínimo privilegio.

---

### Comandos relacionados

- [Crear un grupo](#crear-un-grupo)
- [Agregar un usuario a un grupo](#agregar-un-usuario-a-un-grupo)
- [Consultar información de un usuario](#consultar-información-de-un-usuario)

---

> **⚠️ Advertencia:** Eliminar un usuario de un grupo puede provocar la pérdida inmediata de acceso a archivos, carpetas o servicios asociados a ese grupo. Comprueba siempre el impacto antes de realizar el cambio.

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|--------|--------|------------|
| Listar usuarios | `getent passwd` / `cat /etc/passwd` | `Get-LocalUser` |
| Consultar información de un usuario | `id` | `Get-LocalUser` |
| Crear un usuario | `adduser` / `useradd` | `New-LocalUser` |
| Eliminar un usuario | `userdel` | `Remove-LocalUser` |
| Listar grupos | `getent group` / `cat /etc/group` | `Get-LocalGroup` |
| Crear un grupo | `groupadd` | `New-LocalGroup` |
| Agregar un usuario a un grupo | `usermod -aG` / `gpasswd -a` | `Add-LocalGroupMember` |
| Eliminar un usuario de un grupo | `gpasswd -d` | `Remove-LocalGroupMember` |

---

### Buenas prácticas generales

- Utiliza grupos para asignar permisos en lugar de hacerlo directamente a los usuarios.
- Evita utilizar cuentas compartidas entre varias personas.
- Aplica siempre el principio de **mínimo privilegio**: cada usuario debe disponer únicamente de los permisos necesarios para realizar su trabajo.
- Revisa periódicamente los usuarios y grupos existentes para eliminar cuentas o grupos que ya no sean necesarios.
- Comprueba siempre los cambios realizados antes de asignar permisos sobre archivos, carpetas o servicios.
- Documenta las cuentas administrativas y los grupos con privilegios elevados.

---

### Comandos más utilizados

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver usuarios | `getent passwd` | `Get-LocalUser` |
| Ver grupos | `getent group` | `Get-LocalGroup` |
| Consultar un usuario | `id beatriz` | `Get-LocalUser beatriz` |
| Crear un usuario | `adduser beatriz` | `New-LocalUser -Name "beatriz"` |
| Eliminar un usuario | `userdel beatriz` | `Remove-LocalUser -Name "beatriz"` |
| Crear un grupo | `groupadd desarrolladores` | `New-LocalGroup -Name "desarrolladores"` |
| Agregar usuario a un grupo | `usermod -aG desarrolladores beatriz` | `Add-LocalGroupMember -Group "desarrolladores" -Member "beatriz"` |
| Eliminar usuario de un grupo | `gpasswd -d beatriz desarrolladores` | `Remove-LocalGroupMember -Group "desarrolladores" -Member "beatriz"` |

---

### Siguiente capítulo

➡️ **05-Permisos-Avanzados.md**

En el siguiente capítulo aprenderás a administrar permisos avanzados sobre archivos y directorios, modificar propietarios, gestionar ACL (Access Control Lists) y aplicar permisos de forma más precisa tanto en **Linux** como en **PowerShell**.

---

[⬆️ Volver al índice](#índice)