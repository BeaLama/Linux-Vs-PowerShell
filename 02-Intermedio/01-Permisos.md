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
- [Permisos recursivos](#permisos-recursivos)
- [Permisos especiales](#permisos-especiales)
- [Resumen de equivalencias](#resumen-de-equivalencias)

---

## Consultar permisos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `ls -l` | `Get-Acl <ruta>` |
| **Ejemplo** | `ls -l informe.txt` | `Get-Acl .\informe.txt` |

> 💡 **Diferencia clave** — 🐧 `ls -l` muestra los permisos mediante la notación `rwx`. · 🪟 `Get-Acl` utiliza listas de control de acceso (ACL).

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | *(no aplica)* | `Get-Acl .\archivo.txt` |
| **Ejemplo** | *(no aplica)* | *(no aplica)* |

> 💡 **Diferencia clave** — 🐧 Utiliza permisos POSIX representados mediante `rwx`. · 🪟 Utiliza listas de control de acceso (ACL).

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `chmod <permisos> <archivo>` | `icacls <ruta> /grant <usuario>:<permisos>` |
| **Ejemplo** | `chmod 600 informe.txt` | `icacls .\informe.txt /grant Usuario:M` |

> 💡 **Diferencia clave** — 🐧 `chmod` modifica permisos POSIX (`rwx`). · 🪟 `icacls` modifica permisos NTFS mediante ACL.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `chown <propietario> <archivo>` | `takeown /F <ruta>` |
| **Ejemplo** | `sudo chown usuario Documentos` | `takeown /F .\Documentos` |

> 💡 **Diferencia clave** — 🐧 `chown` cambia el propietario de archivos y directorios. · 🪟 `takeown` asigna la propiedad del recurso al usuario actual o al administrador.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `chmod -R <permisos> <directorio>` | `icacls <ruta> /grant <usuario>:<permisos> /T` |
| **Ejemplo** | `sudo chown -R usuario Proyecto` | `takeown /F .\Proyecto /R` |

> 💡 **Diferencia clave** — 🐧 La opción `-R` aplica los cambios a todos los archivos y subdirectorios. · 🪟 La opción `/T` aplica los cambios de permisos de forma recursiva.

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

| Permiso Linux | Octal | Función | Equivalente PowerShell |
|---|---|---|---|
| SUID | `4` | Ejecuta con permisos del propietario | *(no existe; usa ACL/NTFS)* |
| SGID | `2` | Ejecuta con permisos del grupo / hereda grupo | Herencia de permisos vía ACL |
| Sticky Bit | `1` | Solo el propietario puede borrar en un directorio | *(no existe)* |

**Ejemplo** — `chmod g+s Proyecto` / `chmod 2775 Proyecto`

> 💡 **Diferencia clave** — 🐧 Linux tiene 3 bits especiales (SUID/SGID/Sticky) además de `rwx`. · 🪟 Windows resuelve estos casos con ACL/NTFS (herencia, permisos explícitos, propietario).

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