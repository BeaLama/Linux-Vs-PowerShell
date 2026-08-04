# Usuarios y permisos 

## Introducción

La gestión de usuarios y permisos es una de las tareas más importantes dentro de la administración de sistemas.

## Índice

- [Concepto de identidad digital](#concepto-de-identidad-digital)
- [Usuarios en sistemas operativos](#usuarios-en-sistemas-operativos)
- [Usuario administrador](#usuario-administrador)
- [Usuario root](#usuario-root)
- [Cuenta de servicio](#cuenta-de-servicio)
- [Comparación de tipos de usuarios](#comparacion-de-tipos-de-usuarios)
- [Grupos de usuarios](#grupos-de-usuarios)
- [Grupos integrados del sistema](#grupos-integrados-del-sistema)
- [Componentes del SID](#componentes-del-sid)
- [Consultar UID](#consultar-uid)
- [/etc/passwd](#etcpasswd)
- [/etc/group](#etcgroup)
- [/etc/shadow](#etcshadow)
- [Autenticación y autorización](#autenticacion-y-autorizacion)
- [Llaves SSH](#llaves-ssh)
- [Mostrar usuarios](#mostrar-usuarios)
- [Obtener información de un usuario](#obtener-informacion-de-un-usuario)
- [Crear un usuario](#crear-un-usuario)
- [Eliminar un usuario](#eliminar-un-usuario)
- [Deshabilitar una cuenta](#deshabilitar-una-cuenta)
- [Habilitar una cuenta](#habilitar-una-cuenta)
- [Mostrar grupos](#mostrar-grupos)
- [Añadir usuario a un grupo](#anadir-usuario-a-un-grupo)
- [Eliminar usuario de un grupo](#eliminar-usuario-de-un-grupo)
- [/etc/passwd](#etcpasswd)
- [/etc/shadow](#etcshadow)
- [/etc/group](#etcgroup)
- [Crear usuario con directorio personal](#crear-usuario-con-directorio-personal)
- [Crear usuario con shell específica](#crear-usuario-con-shell-especifica)
- [Cambiar nombre](#cambiar-nombre)
- [Cambiar directorio personal](#cambiar-directorio-personal)
- [Cambiar shell](#cambiar-shell)
- [Eliminar usuario y directorio personal](#eliminar-usuario-y-directorio-personal)
- [Bloquear contraseña](#bloquear-contrasena)
- [Desbloquear cuenta](#desbloquear-cuenta)
- [Crear grupo](#crear-grupo)
- [Eliminar grupo](#eliminar-grupo)
- [Añadir usuario a un grupo](#anadir-usuario-a-un-grupo)
- [Consultar grupos de un usuario](#consultar-grupos-de-un-usuario)
- [Permisos básicos](#permisos-basicos)
- [Ejecución (Execute)](#ejecucion-execute)
- [Entradas de la ACL](#entradas-de-la-acl)
- [Permitir y denegar](#permitir-y-denegar)
- [Consultar ACL](#consultar-acl)
- [Asignar ACL](#asignar-acl)
- [Eliminar una ACL](#eliminar-una-acl)
- [Opciones al romper la herencia](#opciones-al-romper-la-herencia)
- [Roles y privilegios administrativos](#roles-y-privilegios-administrativos)
- [Operador o técnico de soporte](#operador-o-tecnico-de-soporte)
- [Gestión del ciclo de vida de usuarios](#gestion-del-ciclo-de-vida-de-usuarios)
- [Auditoría de usuarios y permisos](#auditoria-de-usuarios-y-permisos)

---

## Concepto de identidad digital

**Conceptos clave:**

- **¿Qué es una identidad digital?:** Una identidad digital es la representación de una persona, aplicación o sistema dentro de un entorno informático.
- **Diferencia entre persona, cuenta e identidad:** Aunque están relacionadas, una persona y una cuenta de usuario no son exactamente lo mismo.
- **Elementos que forman una identidad digital:** Una identidad digital dentro de un sistema suele estar formada por.
- **Identidad digital en entornos empresariales:** En una empresa, las identidades digitales permiten administrar el acceso de empleados, equipos y servicios.
- **Identidades de usuarios, equipos y servicios:** Una identidad no pertenece únicamente a personas.
- **Importancia de la identidad digital:** La gestión correcta de identidades permite: Controlar quién accede a los sistemas.

## Usuarios en sistemas operativos

**Conceptos clave:**

- **¿Qué es un usuario dentro de un sistema operativo?:** Un usuario es una cuenta creada dentro de un sistema operativo que permite identificar a una persona, aplicación o servicio y controlar el acceso a los recursos del equipo.
- **Información asociada a un usuario:** Cada cuenta de usuario contiene diferentes datos dependiendo del sistema operativo.

### Perfil de usuario

*El perfil de usuario contiene la configuración personal asociada a una cuenta.*

```bash
/home/usuario
```

---

**Conceptos clave:**

- **Usuarios locales:** Un usuario local es una cuenta almacenada directamente en el propio equipo.
- **Usuarios de dominio:** En entornos empresariales, los usuarios suelen gestionarse mediante un sistema centralizado.
- **Usuarios del sistema:** Los sistemas operativos crean usuarios internos para ejecutar servicios y procesos.
- **Usuarios interactivos y no interactivos:** Los usuarios pueden clasificarse según su forma de uso.
- **Usuarios interactivos:** Son usuarios utilizados por personas.
- **Usuarios no interactivos:** Son utilizados por servicios o procesos automáticos.

### Creación de usuarios

*Los administradores pueden crear usuarios mediante herramientas gráficas o comandos.*

```bash
useradd usuario
```

---

**Conceptos clave:**

- **Eliminación y deshabilitación de usuarios:** Cuando una cuenta deja de ser necesaria, debe gestionarse correctamente.
- **Eliminación:** La cuenta se elimina completamente.
- **Deshabilitación:** La cuenta permanece almacenada pero no puede utilizarse.
- **Usuarios y seguridad:** Las cuentas de usuario son uno de los elementos principales de seguridad de un sistema.
- **Usuario estándar:** Un usuario estándar es una cuenta destinada al uso habitual por parte de una persona.

## Usuario administrador

*Un usuario administrador es una cuenta con permisos elevados para realizar tareas de configuración y mantenimiento del sistema.*

**Conceptos clave:**

- **Riesgos de los usuarios administradores:** Las cuentas administrativas deben estar protegidas porque una cuenta comprometida puede permitir el control completo del sistema.

## Usuario root

*En sistemas Linux existe una cuenta especial llamada root.*

### Riesgos de utilizar root

*El uso directo de root puede ser peligroso.*

```bash
rm -rf /
```
```bash
sudo
```

---

**Conceptos clave:**

- **Usuario invitado:** Un usuario invitado es una cuenta creada para proporcionar acceso temporal y limitado.
- **Usuario temporal:** Un usuario temporal es una cuenta creada durante un periodo concreto.

## Cuenta de servicio

*Una cuenta de servicio es una cuenta utilizada por aplicaciones o servicios para ejecutarse en un sistema.*

**Conceptos clave:**

- **Características de las cuentas de servicio:** Normalmente: No tienen inicio de sesión interactivo.
- **Riesgos de las cuentas de servicio:** Una cuenta de servicio con demasiados permisos puede convertirse en un riesgo.
- **Usuario de sistema:** Los sistemas operativos utilizan usuarios internos para ejecutar componentes propios.
- **Usuario privilegiado:** Un usuario privilegiado es cualquier cuenta con permisos superiores a los usuarios normales.
- **Cuentas compartidas:** Una cuenta compartida es utilizada por varias personas.

## Comparación de tipos de usuarios

| Tipo | Uso | Privilegios |
|-|-|-|
| Estándar | Usuario habitual | Bajos |
| Administrador | Gestión del sistema | Altos |
| Root | Administración Linux completa | Máximos |
| Invitado | Acceso temporal | Muy bajos |
| Temporal | Uso limitado | Variables |
| Servicio | Aplicaciones y procesos | Específicos |
| Sistema | Funcionamiento interno | Controlados |

---

**Conceptos clave:**

- **Ejemplo práctico:** Una empresa tiene diferentes usuarios.

## Grupos de usuarios

**Conceptos clave:**

- **¿Por qué utilizar grupos?:** La utilización de grupos proporciona varias ventajas: Simplifica la asignación de permisos.
- **Grupos locales:** Un grupo local existe únicamente dentro de un equipo concreto.
- **Grupos de dominio:** Los grupos de dominio son gestionados desde un sistema centralizado como Active Directory.

## Grupos integrados del sistema

*Los sistemas operativos incluyen grupos creados por defecto.*

**Conceptos clave:**

- **Windows:** Ejemplos.
- **Linux:** Linux utiliza principalmente grupos para gestionar permisos.
- **Usuario perteneciente a varios grupos:** Cuando un usuario pertenece a varios grupos, puede acumular permisos.
- **Grupos de seguridad:** Se utilizan para asignar permisos.
- **Grupos de distribución:** Se utilizan principalmente para listas de correo.
- **Dominio local:** Se utilizan principalmente para asignar permisos sobre recursos del dominio.
- **Global:** Contienen usuarios del mismo dominio con una función común.
- **Universal:** Permiten agrupar usuarios y grupos de diferentes dominios.
- **Identificadores de usuario:** Windows utiliza principalmente los SID (Security Identifier) para identificar usuarios y grupos.
- **SID (Security Identifier):** El SID es un identificador único asignado a cada usuario, grupo o equipo dentro de Windows.

## Componentes del SID

*Un SID está formado por.*

**Conceptos clave:**

- **Autoridad de seguridad:** Indica qué entidad creó el identificador.
- **Identificador del dominio o equipo:** Permite diferenciar sistemas distintos.

### RID (Relative Identifier)

*Es la parte final del SID y diferencia usuarios dentro del mismo dominio o equipo.*

| RID | Cuenta |
|-|-|
| 500 | Administrador integrado |
| 501 | Invitado |
| 502 | Krbtgt |
| 1000+ | Usuarios creados posteriormente |

---

## Consultar UID

*Comando.*

```bash
id usuario
```
```bash
id juan
```

---

**Conceptos clave:**

- **Usuario root:** El usuario root siempre tiene.
- **Usuarios del sistema:** Normalmente utilizan UID bajos.
- **Usuarios normales:** Habitualmente comienzan desde.

## /etc/passwd

*Contiene información básica de usuarios.*

```bash
cat /etc/passwd
```

---

## /etc/group

*Contiene información sobre grupos.*

```bash
cat /etc/group
```

---

## /etc/shadow

*Contiene información relacionada con contraseñas cifradas.*

| Windows | Linux |
|-|-|
| SID | UID |
| RID | GID / identificadores internos |
| Dominio | Sistema local |
| Active Directory | /etc/passwd, LDAP |
| ACL basadas en SID | Permisos basados en UID/GID |

```bash
cat /etc/shadow
```

---

## Autenticación y autorización

**Conceptos clave:**

- **¿Qué es la autenticación?:** La autenticación es el proceso mediante el cual un sistema verifica la identidad de un usuario, dispositivo o servicio.
- **Algo que sabes:** Es información que únicamente debería conocer el usuario.
- **Algo que tienes:** Es un elemento físico que posee el usuario.
- **Algo que eres:** Utiliza características biométricas del usuario.
- **Usuario y contraseña:** Es el método más común.
- **Certificados digitales:** Utilizan certificados criptográficos para verificar identidades.

## Llaves SSH

*En Linux, SSH permite autenticarse mediante pares de claves.*

### ¿Qué es la autorización?

*La autorización es el proceso mediante el cual el sistema determina qué recursos puede utilizar un usuario y qué acciones puede realizar.*

| Autenticación | Autorización |
|-|-|
| Verifica identidad | Controla permisos |
| Responde "¿Quién eres?" | Responde "¿Qué puedes hacer?" |
| Ocurre primero | Ocurre después |
| Usa credenciales | Usa permisos y roles |

---

**Conceptos clave:**

- **DAC (Discretionary Access Control):** Control de acceso basado en el propietario del recurso.
- **MAC (Mandatory Access Control):** Control de acceso obligatorio basado en políticas de seguridad.
- **RBAC (Role Based Access Control):** Control basado en roles.
- **ABAC (Attribute Based Access Control):** Control basado en atributos.
- **Contraseñas débiles:** Ejemplo.
- **Exceso de permisos:** Ejemplo.
- **Cuentas compartidas:** Ejemplo.
- **Gestión de usuarios en Windows:** Windows permite trabajar con dos tipos principales de cuentas.
- **Usuarios locales:** Las cuentas locales existen únicamente en un equipo.
- **Usuarios de dominio:** Las cuentas de dominio son administradas desde un servidor, normalmente mediante Active Directory.
- **Configuración:** Ruta.
- **Usuarios y grupos locales:** Herramienta.
- **Administración de equipos:** Herramienta.
- **Mostrar usuarios:** Comando.
- **Crear un usuario:** Sintaxis.
- **Eliminar un usuario:** Sintaxis.
- **Cambiar contraseña:** Sintaxis.

## Mostrar usuarios

```powershell
Get-LocalUser
```

---

## Obtener información de un usuario

```powershell
Get-LocalUser -Name "beatriz"
```

---

## Crear un usuario

```powershell
New-LocalUser
```
```powershell
$password = Read-Host "Contraseña" -AsSecureString

New-LocalUser `
-Name "prueba" `
-Password $password `
-FullName "Usuario de prueba"
```

---

## Eliminar un usuario

```powershell
Remove-LocalUser -Name "prueba"
```

---

## Deshabilitar una cuenta

```powershell
Disable-LocalUser -Name "beatriz"
```

---

## Habilitar una cuenta

```powershell
Enable-LocalUser -Name "beatriz"
```

---

## Mostrar grupos

*CMD.*

```powershell
Get-LocalGroup
```

---

## Añadir usuario a un grupo

*CMD.*

```powershell
Add-LocalGroupMember `
-Group "Administradores" `
-Member "beatriz"
```

---

## Eliminar usuario de un grupo

*CMD.*

```powershell
Remove-LocalGroupMember `
-Group "Administradores" `
-Member "beatriz"
```
```powershell
Set-LocalUser
```

---

**Conceptos clave:**

- **Gestión de usuarios en Linux:** Linux almacena la información de usuarios y grupos en varios archivos importantes.

## /etc/passwd

*Contiene la información básica de cada usuario.*

```bash
cat /etc/passwd
```

---

## /etc/shadow

*Almacena las contraseñas cifradas y la información relacionada con ellas.*

```bash
sudo cat /etc/shadow
```

---

## /etc/group

*Contiene la información sobre los grupos existentes.*

```bash
cat /etc/group
```
```bash
useradd
```

---

## Crear usuario con directorio personal

```bash
sudo useradd -m beatriz
```

---

## Crear usuario con shell específica

```bash
sudo useradd -m -s /bin/bash beatriz
```
```bash
sudo passwd beatriz
```

---

## Cambiar nombre

```bash
sudo usermod -l nuevo_nombre usuario
```
```bash
sudo usermod -l beatriz.lama beatriz
```

---

## Cambiar directorio personal

```bash
sudo usermod -d /home/nuevo_usuario usuario
```

---

## Cambiar shell

```bash
sudo usermod -s /bin/zsh usuario
```
```bash
sudo userdel usuario
```

---

## Eliminar usuario y directorio personal

```bash
sudo userdel -r beatriz
```

---

## Bloquear contraseña

```bash
sudo passwd -l usuario
```
```bash
sudo passwd -l beatriz
```

---

## Desbloquear cuenta

```bash
sudo passwd -u beatriz
```

---

## Crear grupo

```bash
sudo groupadd ventas
```

---

## Eliminar grupo

```bash
sudo groupdel ventas
```

---

## Añadir usuario a un grupo

```bash
sudo usermod -aG ventas beatriz
```

---

## Consultar grupos de un usuario

```bash
groups beatriz
```
```bash
id beatriz
```

---

**Conceptos clave:**

- **Active Directory y usuarios empresariales:** Active Directory es un servicio de directorio que almacena información sobre los objetos de una red y permite administrarlos de forma centralizada.
- **Dominio:** El dominio es la unidad principal de administración.
- **Controlador de dominio (Domain Controller):** El controlador de dominio es el servidor que almacena la base de datos de Active Directory.
- **Objetos:** Todo elemento administrado dentro de Active Directory recibe el nombre de objeto.
- **Permisos de archivos y recursos:** Un permiso es una autorización que permite realizar una acción concreta sobre un recurso.

## Permisos básicos

*Los permisos básicos más habituales son.*

**Conceptos clave:**

- **Control total:** Permite realizar cualquier acción sobre el recurso.
- **Modificar:** Permite: Leer.
- **Lectura y ejecución:** Permite: Abrir archivos.
- **Lectura:** Permite visualizar el contenido, pero no modificarlo.
- **Escritura:** Permite crear y modificar archivos sin eliminarlos.
- **Lectura (Read):** Representado por.
- **Escritura (Write):** Representado por.

## Ejecución (Execute)

*Representado por.*

| Valor | Permisos |
|--------|----------|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |
| 3 | -wx |
| 2 | -w- |
| 1 | --x |
| 0 | --- |

```bash
chmod 755 archivo.sh
```
```bash
chmod
```

---

**Conceptos clave:**

- **Listas de Control de Acceso (ACL):** Una ACL es una lista formada por una o varias entradas que especifican los permisos de distintos usuarios o grupos sobre un recurso.
- **Recurso:** Es el objeto sobre el que se aplican los permisos.
- **Identidad:** Indica quién recibirá los permisos.
- **Permiso:** Define qué acciones podrá realizar la identidad.
- **Tipo de acceso:** Cada entrada puede permitir o denegar permisos.

## Entradas de la ACL

*Cada usuario o grupo tiene su propia entrada.*

| Usuario o grupo | Permisos |
|-----------------|----------|
| Administradores | Control total |
| Ventas | Modificar |
| Invitados | Lectura |

---

## Permitir y denegar

*Windows permite definir permisos de dos tipos.*

**Conceptos clave:**

- **Permitir:** Autoriza una acción.
- **Denegar:** Bloquea una acción incluso si otro permiso pudiera concederla.

## Consultar ACL

*Comando.*

```bash
getfacl archivo.txt
```
```bash
getfacl informe.pdf
```

---

## Asignar ACL

*Comando.*

```bash
setfacl
```
```bash
setfacl -m u:beatriz:rwx informe.pdf
```

---

## Eliminar una ACL

*Ejemplo.*

```bash
setfacl -x u:beatriz informe.pdf
```

---

**Conceptos clave:**

- **Herencia de permisos:** Cuando se crea un nuevo archivo o carpeta dentro de otra carpeta, el sistema puede copiar automáticamente los permisos del elemento padre.
- **Elemento padre:** Es el recurso que contiene otros elementos y desde el que se heredan los permisos.
- **Elemento hijo:** Es el recurso que recibe automáticamente los permisos del elemento superior.
- **Visualizar la herencia:** Ruta.
- **Permisos heredados:** Proceden de una carpeta superior.
- **Permisos explícitos:** Son permisos configurados directamente sobre un recurso concreto.

## Opciones al romper la herencia

*Windows ofrece dos posibilidades.*

**Conceptos clave:**

- **Convertir permisos heredados en permisos explícitos:** Los permisos actuales se mantienen, pero dejan de depender del elemento padre.

### Eliminar permisos heredados

*El recurso deja de tener los permisos recibidos del elemento padre.*

```bash
getfacl carpeta
```
```bash
setfacl -d -m u:beatriz:rwx carpeta
```

---

## Roles y privilegios administrativos

*Un rol es un conjunto de funciones y responsabilidades asignadas a un usuario o grupo de usuarios.*

| Permisos | Privilegios |
|----------|-------------|
| Controlan el acceso a recursos | Permiten realizar acciones administrativas |
| Se aplican sobre archivos, carpetas o recursos | Se aplican sobre el sistema operativo |
| Ejemplo: leer un archivo | Ejemplo: crear un usuario |

---

**Conceptos clave:**

- **Usuario estándar:** Es el rol utilizado por la mayoría de empleados.
- **Administrador local:** Tiene control completo sobre un único equipo.
- **Administrador del dominio:** Gestiona toda la infraestructura de Active Directory.
- **Administrador de servidores:** Gestiona uno o varios servidores concretos.
- **Administrador de bases de datos:** Se encarga de administrar sistemas gestores de bases de datos.

## Operador o técnico de soporte

*Dispone de permisos limitados para realizar tareas de soporte.*

```bash
sudo
```

---

**Conceptos clave:**

- **Cuentas de servicio:** Una cuenta de servicio es una cuenta diseñada para ser utilizada por una aplicación, un servicio o un proceso automático.
- **Local System:** Es una cuenta integrada con privilegios muy elevados sobre el equipo local.
- **Local Service:** Cuenta integrada con privilegios limitados.
- **Network Service:** Cuenta integrada utilizada por servicios que necesitan acceder a recursos de red.
- **Cuenta de usuario específica:** Es una cuenta creada exclusivamente para ejecutar un servicio.

## Gestión del ciclo de vida de usuarios

**Conceptos clave:**

- **¿Qué es el ciclo de vida de un usuario?:** El ciclo de vida de un usuario comprende todas las fases por las que pasa una cuenta dentro de un sistema.
- **Alta de usuarios:** La primera fase consiste en la creación de la cuenta.
- **Modificación de cuentas:** A lo largo del tiempo pueden producirse cambios que requieran modificar la configuración de la cuenta.
- **Gestión de permisos:** Los permisos deben mantenerse actualizados durante toda la vida de la cuenta.
- **Suspensión o desactivación de cuentas:** Cuando un usuario deja de utilizar temporalmente una cuenta, suele ser preferible desactivarla en lugar de eliminarla.
- **Eliminación de cuentas:** Cuando una cuenta deja de ser necesaria debe eliminarse de forma controlada.
- **Gestión del ciclo de vida en Windows:** En Windows y Active Directory las tareas más habituales son: Crear usuarios.

### Gestión del ciclo de vida en Linux

*Linux dispone de distintos comandos para administrar las cuentas de usuario.*

```bash
sudo useradd usuario
```
```bash
sudo passwd usuario
```

---

**Conceptos clave:**

- **Automatización del ciclo de vida:** En organizaciones con un gran número de usuarios es habitual automatizar estas tareas.

## Auditoría de usuarios y permisos

**Conceptos clave:**

- **¿Qué es una auditoría de usuarios?:** Una auditoría de usuarios es el proceso mediante el cual se revisan las cuentas existentes, sus permisos y la actividad realizada por cada una de ellas.
- **Objetivos de la auditoría:** Las auditorías persiguen diversos objetivos: Detectar accesos no autorizados.
- **Información que debe revisarse:** Durante una auditoría es recomendable comprobar: Usuarios existentes.
- **Auditoría en Windows:** Windows incorpora diferentes herramientas para auditar usuarios y permisos.

### Auditoría mediante PowerShell

*PowerShell facilita la obtención de información sobre usuarios y grupos.*

```powershell
Get-LocalUser
```
```powershell
Get-LocalGroup
```

---

**Conceptos clave:**

- **Auditoría en Linux:** Linux almacena información sobre autenticación y actividad de los usuarios en diferentes archivos de registro.

### Comandos útiles en Linux

*Mostrar usuarios conectados.*

```bash
who
```
```bash
last
```

---

**Conceptos clave:**

- **Revisión de permisos:** Una auditoría también debe incluir la revisión de los permisos sobre archivos y carpetas.
- **Frecuencia de las auditorías:** La periodicidad dependerá del tamaño y las necesidades de la organización.
  
---

[⬆️ Volver al índice](#índice)
