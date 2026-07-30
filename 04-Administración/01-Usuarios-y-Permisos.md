# Usuarios y permisos

## Introducción


La gestión de usuarios y permisos es una de las tareas más importantes dentro de la administración de sistemas.

Los sistemas operativos necesitan mecanismos que permitan identificar a los usuarios, controlar sus accesos y limitar las acciones que pueden realizar sobre los recursos disponibles.

Cada usuario dentro de un sistema posee una identidad asociada, la cual determina cómo será reconocido por el sistema y qué permisos tendrá asignados. Estos permisos permiten controlar el acceso a archivos, carpetas, aplicaciones, servicios y otros recursos.

En entornos empresariales, la correcta administración de usuarios es fundamental para mantener la seguridad de la infraestructura. La creación de cuentas, asignación de permisos, pertenencia a grupos y gestión de privilegios deben realizarse siguiendo criterios de organización y seguridad.

Una mala configuración de usuarios o permisos puede provocar problemas como:

- Accesos no autorizados.
- Exposición de información sensible.
- Escaladas de privilegios.
- Pérdida de control sobre los recursos.
- Dificultad para realizar auditorías.

Por este motivo, los administradores de sistemas deben conocer cómo funcionan los usuarios, grupos y permisos tanto en sistemas Windows como Linux, además de aplicar principios como el mínimo privilegio y la correcta separación de funciones.

En este apartado se estudiará la gestión completa del ciclo de vida de los usuarios, desde su creación y configuración inicial hasta su modificación, auditoría y eliminación.

---

## Índice

- [Concepto de identidad digital](#concepto-de-identidad-digital)
- [Usuarios en sistemas operativos](#usuarios-en-sistemas-operativos)
- [Tipos de usuarios](#tipos-de-usuarios)
- [Grupos de usuarios](#grupos-de-usuarios)
- [Identificadores de usuario](#identificadores-de-usuario)
- [Autenticación y autorización](#autenticación-y-autorización)
- [Gestión de usuarios en Windows](#gestión-de-usuarios-en-windows)
- [Gestión de usuarios en Linux](#gestión-de-usuarios-en-linux)
- [Active Directory y usuarios empresariales](#active-directory-y-usuarios-empresariales)
- [Permisos de archivos y recursos](#permisos-de-archivos-y-recursos)
- [Listas de control de acceso (ACL)](#listas-de-control-de-acceso-acl)
- [Herencia de permisos](#herencia-de-permisos)
- [Roles y privilegios administrativos](#roles-y-privilegios-administrativos)
- [Cuentas de servicio](#cuentas-de-servicio)
- [Gestión del ciclo de vida de usuarios](#gestión-del-ciclo-de-vida-de-usuarios)
- [Auditoría de usuarios y permisos](#auditoría-de-usuarios-y-permisos)
- [Buenas prácticas de seguridad](#buenas-prácticas-de-seguridad)

--- 

## Concepto de identidad digital

### ¿Qué es una identidad digital?

Una identidad digital es la representación de una persona, aplicación o sistema dentro de un entorno informático.

Los sistemas operativos necesitan una forma de identificar quién está intentando acceder a un recurso para poder decidir si ese acceso está permitido o no.

Una identidad digital está formada por diferentes elementos que permiten reconocer y gestionar una entidad dentro del sistema.

Ejemplo:

```text
Persona física

↓

Cuenta de usuario

↓

Identificador único

↓

Permisos asignados

↓

Acceso a recursos
```

---

### Diferencia entre persona, cuenta e identidad

Aunque están relacionadas, una persona y una cuenta de usuario no son exactamente lo mismo.

Una misma persona puede tener varias identidades digitales dependiendo del entorno donde trabaje.

Ejemplo:

```text
usuario (persona)

├── Cuenta corporativa
│
├── Cuenta administrativa
│
└── Cuenta personal
```

Cada cuenta puede tener diferentes permisos y funciones.

---

### Elementos que forman una identidad digital

Una identidad digital dentro de un sistema suele estar formada por:

#### Nombre de usuario

Es el identificador utilizado normalmente por el usuario para iniciar sesión.

Ejemplo:

```text
usuario:

usuario.apellido
```

---

#### Identificador único

Los sistemas no utilizan únicamente el nombre visible del usuario.

También asignan un identificador interno único.

Ejemplos:

Windows:

```text
SID
```

Linux:

```text
UID
```

Esto permite diferenciar usuarios aunque tengan nombres similares.

---

#### Credenciales de autenticación

Son los elementos utilizados para demostrar la identidad.

Ejemplos:

- Contraseña.
- Llave de seguridad.
- Certificado digital.
- Token.
- Autenticación multifactor (MFA).

Ejemplo:

```text
Usuario introduce contraseña

↓

Sistema valida credenciales

↓

Identidad confirmada
```

---

#### Grupos asociados

Las identidades pueden pertenecer a grupos que determinan sus permisos.

Ejemplo:

```text
Usuario:

juan


Grupo:

Contabilidad


Permisos:

Acceso carpeta Finanzas
```

---

#### Permisos asignados

Los permisos indican qué acciones puede realizar una identidad sobre un recurso.

Ejemplo:

```text
Usuario:

empleado


Recurso:

Servidor archivos


Permiso:

Lectura
```

---

### Identidad digital en entornos empresariales

En una empresa, las identidades digitales permiten administrar el acceso de empleados, equipos y servicios.

Ejemplo:

```text
Empleado nuevo

↓

Creación de cuenta

↓

Asignación a departamento

↓

Asignación de permisos

↓

Acceso a recursos necesarios
```

Normalmente esta gestión se realiza mediante sistemas centralizados como:

- Active Directory.
- LDAP.
- Microsoft Entra ID.
- Sistemas IAM.

---

### Identidades de usuarios, equipos y servicios

Una identidad no pertenece únicamente a personas.

Los sistemas también utilizan identidades para:

#### Usuarios

Representan personas.

Ejemplo:

```text
maria.garcia
```

---

#### Equipos

Representan dispositivos dentro de una red.

Ejemplo:

```text
PC-VENTAS-01
```

---

#### Servicios

Representan aplicaciones o procesos que necesitan autenticarse.

Ejemplo:

```text
svc_backup

↓

Servicio de copias de seguridad
```

---

### Importancia de la identidad digital

La gestión correcta de identidades permite:

- Controlar quién accede a los sistemas.
- Aplicar permisos adecuados.
- Detectar accesos no autorizados.
- Realizar auditorías.
- Mantener la seguridad de la infraestructura.

Sin una correcta gestión de identidades, un sistema no puede determinar quién tiene acceso a sus recursos ni qué acciones puede realizar.

---

### Ejemplo práctico

Una empresa contrata a un nuevo empleado del departamento de administración.

Proceso:

```text
Empleado contratado

↓

Crear identidad digital

↓

Asignar usuario

↓

Añadir a grupo Administración

↓

Conceder acceso a recursos necesarios
```

El usuario podrá acceder únicamente a los recursos permitidos según su función.

---

[⬆️ Volver al índice](#índice)

## Usuarios en sistemas operativos

### ¿Qué es un usuario dentro de un sistema operativo?

Un usuario es una cuenta creada dentro de un sistema operativo que permite identificar a una persona, aplicación o servicio y controlar el acceso a los recursos del equipo.

Cuando un usuario inicia sesión, el sistema comprueba su identidad y carga la configuración asociada a esa cuenta.

Ejemplo:

```text
Usuario inicia sesión

↓

Sistema valida identidad

↓

Carga perfil del usuario

↓

Aplica permisos asignados
```

Un usuario no es simplemente un nombre y una contraseña, sino un conjunto de información que el sistema utiliza para gestionar accesos y privilegios.

---

### Información asociada a un usuario

Cada cuenta de usuario contiene diferentes datos dependiendo del sistema operativo.

Entre la información más habitual se encuentra:

- Nombre de usuario.
- Identificador único.
- Contraseña o método de autenticación.
- Grupo o grupos asociados.
- Permisos.
- Directorio personal.
- Configuración del perfil.
- Registro de actividad.

Ejemplo:

```text
Usuario:

juan.perez


Información:

Nombre:
juan.perez

Grupo:
Ventas

Directorio:
C:\Users\juan.perez

Permisos:
Lectura / Escritura
```

---

### Perfil de usuario

El perfil de usuario contiene la configuración personal asociada a una cuenta.

Incluye elementos como:

- Escritorio.
- Documentos.
- Preferencias del sistema.
- Configuración de aplicaciones.
- Archivos personales.

Ejemplo en Windows:

```text
C:\Users\usuario
```

Ejemplo en Linux:

```bash
/home/usuario
```

---

### Usuarios locales

Un usuario local es una cuenta almacenada directamente en el propio equipo.

La información del usuario existe únicamente en ese sistema.

Ejemplo:

```text
Ordenador local

↓

Usuario administrador

↓

Cuenta almacenada en el equipo
```

Características:

- Solo existe en ese dispositivo.
- Puede iniciar sesión únicamente en ese equipo.
- Se administra localmente.

Ejemplo:

Windows:

```text
PC01

↓

Usuario:
Administrador
```

Linux:

```text
Servidor01

↓

Usuario:
root
```

---

### Usuarios de dominio

En entornos empresariales, los usuarios suelen gestionarse mediante un sistema centralizado.

Un usuario de dominio es una cuenta almacenada en un servidor de identidad, como Active Directory.

Ejemplo:

```text
Dominio:

empresa.local


Usuario:

juan.perez


↓

Puede iniciar sesión en diferentes equipos
```

Ventajas:

- Administración centralizada.
- Aplicación de políticas.
- Gestión sencilla de permisos.
- Control de accesos.

---

### Usuarios del sistema

Los sistemas operativos crean usuarios internos para ejecutar servicios y procesos.

Estos usuarios normalmente no pertenecen a personas.

Ejemplo:

```text
Servicio

↓

Usuario del sistema

↓

Ejecuta proceso
```

Se utilizan para:

- Ejecutar servicios.
- Separar privilegios.
- Mejorar seguridad.

Ejemplos en Linux:

```text
www-data

↓

Servidor web Apache


mysql

↓

Servicio base de datos
```

Ejemplos en Windows:

```text
SYSTEM

LOCAL SERVICE

NETWORK SERVICE
```

---

### Usuarios interactivos y no interactivos

Los usuarios pueden clasificarse según su forma de uso.

---

### Usuarios interactivos

Son usuarios utilizados por personas.

Permiten:

- Inicio de sesión.
- Uso de aplicaciones.
- Acceso a recursos.

Ejemplo:

```text
Empleado

↓

Cuenta corporativa

↓

Equipo de trabajo
```

---

### Usuarios no interactivos

Son utilizados por servicios o procesos automáticos.

No están pensados para que una persona inicie sesión.

Ejemplo:

```text
svc_backup

↓

Ejecuta copias de seguridad automáticamente
```

---

### Creación de usuarios

Los administradores pueden crear usuarios mediante herramientas gráficas o comandos.

Ejemplo Windows:

```text
Usuarios y grupos locales

↓

Nuevo usuario
```

Ejemplo Linux:

```bash
useradd usuario
```

---

### Eliminación y deshabilitación de usuarios

Cuando una cuenta deja de ser necesaria, debe gestionarse correctamente.

Existen dos opciones:

---

### Eliminación

La cuenta se elimina completamente.

Ejemplo:

```text
Usuario eliminado

↓

Ya no existe en el sistema
```

---

### Deshabilitación

La cuenta permanece almacenada pero no puede utilizarse.

Ejemplo:

```text
Empleado abandona empresa

↓

Cuenta bloqueada

↓

Información conservada
```

En entornos empresariales suele ser preferible deshabilitar primero antes de eliminar.

---

### Usuarios y seguridad

Las cuentas de usuario son uno de los elementos principales de seguridad de un sistema.

Una mala gestión puede provocar:

- Accesos indebidos.
- Robo de información.
- Escaladas de privilegios.
- Uso de cuentas abandonadas.

Ejemplo:

```text
Cuenta antigua activa

↓

Contraseña comprometida

↓

Acceso no autorizado
```

Por ello es importante revisar periódicamente las cuentas existentes y sus permisos asociados.

---

[⬆️ Volver al índice](#índice)

## Tipos de usuarios

### Introducción

No todos los usuarios dentro de un sistema tienen las mismas funciones ni los mismos permisos.

Dependiendo de su finalidad, los usuarios pueden tener diferentes niveles de acceso y privilegios.

La correcta clasificación de usuarios permite aplicar el principio de mínimo privilegio, evitando que una cuenta tenga más permisos de los necesarios para realizar su trabajo.

Ejemplo:

```text
Empleado de contabilidad

↓

Necesita acceso a documentos financieros

NO

↓

Permisos de administrador del sistema
```

---

## Usuario estándar

Un usuario estándar es una cuenta destinada al uso habitual por parte de una persona.

Normalmente tiene permisos limitados y puede utilizar aplicaciones y acceder a los recursos autorizados, pero no modificar configuraciones críticas del sistema.

Ejemplos:

- Empleados.
- Usuarios finales.
- Personal administrativo.

Características:

- Puede ejecutar aplicaciones.
- Puede modificar su propia configuración.
- No puede realizar cambios importantes del sistema.
- Tiene acceso limitado a recursos.

Ejemplo:

```text
Usuario:

maria.garcia


Permisos:

✔ Abrir documentos

✔ Usar aplicaciones

✘ Instalar drivers

✘ Modificar sistema
```

---

## Usuario administrador

Un usuario administrador es una cuenta con permisos elevados para realizar tareas de configuración y mantenimiento del sistema.

Puede modificar elementos críticos como:

- Usuarios.
- Servicios.
- Configuración del sistema.
- Software instalado.
- Permisos.

Ejemplos:

Windows:

```text
Administrador local
```

Linux:

```text
Usuario con permisos sudo
```

---

### Riesgos de los usuarios administradores

Las cuentas administrativas deben estar protegidas porque una cuenta comprometida puede permitir el control completo del sistema.

Ejemplo:

```text
Cuenta administrador comprometida

↓

Atacante obtiene privilegios elevados

↓

Control del equipo
```

Por este motivo se recomienda:

- No utilizar cuentas administrativas para tareas diarias.
- Activar MFA cuando sea posible.
- Auditar su uso.
- Proteger sus credenciales.

---

## Usuario root

En sistemas Linux existe una cuenta especial llamada **root**.

Es el usuario con máximo nivel de privilegios dentro del sistema.

Puede:

- Modificar cualquier archivo.
- Gestionar usuarios.
- Instalar software.
- Cambiar configuraciones críticas.
- Controlar servicios.

Ejemplo:

```bash
root@servidor
```

---

### Riesgos de utilizar root

El uso directo de root puede ser peligroso.

Un error ejecutando un comando puede afectar completamente al sistema.

Ejemplo:

```bash
rm -rf /
```

Podría eliminar archivos esenciales.

Por ello, en entornos profesionales se suele utilizar:

```bash
sudo
```

para ejecutar acciones administrativas de forma controlada.

Ejemplo:

```bash
sudo apt update
```

---

## Usuario invitado

Un usuario invitado es una cuenta creada para proporcionar acceso temporal y limitado.

Características:

- Permisos reducidos.
- Acceso restringido.
- Sin capacidad administrativa.

Ejemplo:

```text
Ordenador compartido

↓

Usuario invitado

↓

Acceso limitado
```

Actualmente muchas organizaciones deshabilitan estas cuentas por motivos de seguridad.

---

## Usuario temporal

Un usuario temporal es una cuenta creada durante un periodo concreto.

Se utiliza para situaciones como:

- Personal externo.
- Técnicos.
- Pruebas.
- Proyectos temporales.

Ejemplo:

```text
Proveedor externo

↓

Cuenta temporal

↓

Trabajo realizado

↓

Cuenta eliminada
```

---

## Cuenta de servicio

Una cuenta de servicio es una cuenta utilizada por aplicaciones o servicios para ejecutarse en un sistema.

No pertenece normalmente a una persona.

Ejemplos:

```text
svc_backup

↓

Servicio de copias


svc_sql

↓

Base de datos SQL
```

---

### Características de las cuentas de servicio

Normalmente:

- No tienen inicio de sesión interactivo.
- Tienen permisos específicos.
- Ejecutan procesos automáticos.
- Deben estar protegidas.

---

### Riesgos de las cuentas de servicio

Una cuenta de servicio con demasiados permisos puede convertirse en un riesgo.

Ejemplo:

```text
Servicio backup

↓

Cuenta con permisos administrador

↓

Compromiso del servicio

↓

Control del sistema
```

---

## Usuario de sistema

Los sistemas operativos utilizan usuarios internos para ejecutar componentes propios.

Estos usuarios permiten separar procesos y reducir privilegios.

Ejemplos Windows:

```text
SYSTEM

LOCAL SERVICE

NETWORK SERVICE
```

Ejemplos Linux:

```text
www-data

mysql

sshd
```

---

## Usuario privilegiado

Un usuario privilegiado es cualquier cuenta con permisos superiores a los usuarios normales.

Incluye:

- Administradores.
- Root.
- Cuentas de servicio privilegiadas.
- Usuarios con permisos especiales.

Estas cuentas requieren controles adicionales.

Ejemplo:

```text
Usuario privilegiado

↓

Mayor capacidad

↓

Mayor riesgo
```

---

## Cuentas compartidas

Una cuenta compartida es utilizada por varias personas.

Ejemplo:

```text
usuario:

almacen

contraseña:

compartida por empleados
```

Aunque pueden parecer cómodas, presentan problemas:

- No permiten saber quién realizó una acción.
- Dificultan auditorías.
- Aumentan riesgos de seguridad.

En entornos empresariales deben evitarse siempre que sea posible.

---

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

## Ejemplo práctico

Una empresa tiene diferentes usuarios:

```text
Empleado administración

↓

Usuario estándar


Administrador IT

↓

Usuario administrador


Servidor SQL

↓

Cuenta de servicio


Sistema operativo

↓

Usuario interno
```

Cada identidad tiene únicamente los permisos necesarios para cumplir su función.

---

[⬆️ Volver al índice](#índice)

## Grupos de usuarios

### Introducción

Los grupos de usuarios son conjuntos de cuentas que comparten características comunes o necesitan acceder a los mismos recursos.

En lugar de asignar permisos usuario por usuario, los administradores pueden asignar permisos a un grupo y añadir usuarios dentro de él.

Esto facilita la administración y permite gestionar grandes cantidades de cuentas de forma más eficiente.

Ejemplo:

```text
Grupo:

Contabilidad


Usuarios:

├── Ana

├── Juan

└── Marta


Permisos:

Acceso carpeta financiera
```

---

### ¿Por qué utilizar grupos?

La utilización de grupos proporciona varias ventajas:

- Simplifica la asignación de permisos.
- Reduce errores administrativos.
- Facilita la incorporación de nuevos usuarios.
- Permite aplicar políticas comunes.
- Mejora la organización.

Ejemplo:

Sin grupos:

```text
Usuario 1 → Permiso carpeta Finanzas

Usuario 2 → Permiso carpeta Finanzas

Usuario 3 → Permiso carpeta Finanzas
```

Con grupos:

```text
Grupo Contabilidad

↓

Permiso carpeta Finanzas

↓

Usuarios incluidos
```

---

# Tipos de grupos

Los grupos pueden clasificarse según dónde se gestionen y su finalidad.

---

## Grupos locales

Un grupo local existe únicamente dentro de un equipo concreto.

Los permisos asignados al grupo solo afectan a ese sistema.

Ejemplo:

```text
Equipo:

PC-VENTAS-01


Grupo local:

Administradores


Usuarios:

Administrador
```

Características:

- Se almacenan en el propio equipo.
- No se sincronizan con otros equipos.
- Habituales en equipos independientes.

---

## Grupos de dominio

Los grupos de dominio son gestionados desde un sistema centralizado como Active Directory.

Permiten administrar usuarios y permisos en toda una organización.

Ejemplo:

```text
Dominio:

empresa.local


Grupo:

Usuarios_Ventas


Usuarios:

├── Carlos

├── Laura

└── Pedro
```

Ventajas:

- Administración centralizada.
- Aplicación de políticas.
- Gestión de grandes entornos.

---

## Grupos integrados del sistema

Los sistemas operativos incluyen grupos creados por defecto.

Estos grupos tienen funciones específicas.

---

### Windows

Ejemplos:

#### Administradores

Usuarios con permisos administrativos completos.

```text
Administrators
```

---

#### Usuarios estándar

Usuarios con permisos limitados.

```text
Users
```

---

#### Usuarios de escritorio remoto

Permite acceso mediante RDP.

```text
Remote Desktop Users
```

---

### Linux

Linux utiliza principalmente grupos para gestionar permisos.

Ejemplos:

```text
sudo

↓

Usuarios con permisos administrativos
```

```text
www-data

↓

Servidor web
```

---

# Gestión de pertenencia a grupos

Un usuario puede pertenecer a uno o varios grupos.

Ejemplo:

```text
Usuario:

juan


Grupos:

├── Usuarios

├── Contabilidad

└── VPN
```

Cada grupo puede aportar diferentes permisos.

---

## Usuario perteneciente a varios grupos

Cuando un usuario pertenece a varios grupos, puede acumular permisos.

Ejemplo:

```text
Grupo Ventas

↓

Acceso documentos comerciales


Grupo Administración

↓

Acceso herramientas internas


Usuario:

Ana

↓

Pertenece a ambos grupos
```

---

# Grupos y asignación de permisos

La forma recomendada de administrar permisos es asignarlos a grupos en lugar de usuarios individuales.

Ejemplo:

Incorrecto:

```text
Usuario Juan

↓

Permiso carpeta Finanzas
```

Usuario María

↓

Permiso carpeta Finanzas


Usuario Pedro

↓

Permiso carpeta Finanzas
```

Correcto:

```text
Grupo Finanzas

↓

Permiso carpeta Finanzas

↓

Usuarios del grupo
```

---

# Grupos en Active Directory

Active Directory utiliza grupos para organizar usuarios y recursos dentro de un dominio.

Los grupos permiten:

- Gestionar departamentos.
- Asignar permisos.
- Aplicar políticas.
- Delegar administración.

Ejemplo:

```text
Empresa.local


Usuarios

↓

Grupos

↓

Permisos

↓

Recursos
```

---

# Tipos de grupos en Active Directory

Active Directory utiliza dos clasificaciones principales:

---

## Grupos de seguridad

Se utilizan para asignar permisos.

Ejemplo:

```text
Grupo:

RRHH


Permiso:

Acceso carpeta empleados
```

---

## Grupos de distribución

Se utilizan principalmente para listas de correo.

Ejemplo:

```text
Grupo:

todos@empresa.com


Uso:

Enviar comunicaciones internas
```

---

# Ámbitos de grupo en Active Directory

Los grupos de seguridad tienen diferentes ámbitos.

---

## Dominio local

Se utilizan principalmente para asignar permisos sobre recursos del dominio.

Ejemplo:

```text
Grupo:

DL_Finanzas_RW

↓

Permiso carpeta financiera
```

---

## Global

Contienen usuarios del mismo dominio con una función común.

Ejemplo:

```text
GG_Contabilidad

↓

Usuarios departamento contable
```

---

## Universal

Permiten agrupar usuarios y grupos de diferentes dominios.

Se utilizan principalmente en estructuras grandes.

---

# Grupos anidados

Un grupo puede contener otros grupos.

Ejemplo:

```text
Grupo:

Empleados_España


Incluye:

├── Ventas

├── Marketing

└── Administración
```

Esto permite crear estructuras organizativas más complejas.

---

# Problemas habituales con grupos

Una mala gestión de grupos puede provocar:

- Usuarios con demasiados permisos.
- Accesos innecesarios.
- Dificultad para auditar permisos.
- Confusión administrativa.

Ejemplo:

```text
Usuario cambia de departamento

↓

Sigue en grupos antiguos

↓

Mantiene accesos incorrectos
```

---

# Ejemplo práctico

Una empresa tiene una carpeta compartida:

```text
\\servidor\finanzas
```

Configuración:

```text
Grupo:

GG_Finanzas


Permiso:

Modificar


Usuarios:

Ana

Juan

Marta
```

Si entra un nuevo empleado:

```text
Nuevo usuario

↓

Añadir al grupo Finanzas

↓

Obtiene permisos automáticamente
```

---

[⬆️ Volver al índice](#índice)

## Identificadores de usuario

### Introducción

Los sistemas operativos necesitan una forma única de identificar cada cuenta de usuario internamente.

Aunque los usuarios suelen trabajar con nombres como:

```text
juan.perez
```

el sistema no utiliza únicamente ese nombre para identificar la cuenta.

Para evitar conflictos y permitir una gestión más precisa, los sistemas asignan identificadores únicos a cada usuario.

Estos identificadores permiten al sistema saber exactamente qué usuario está realizando una acción y qué permisos debe aplicar.

Ejemplo:

```text
Nombre visible:

juan.perez


Identificador interno:

SID / UID


Permisos asociados:

Lectura y escritura
```

---

# Identificadores en Windows

Windows utiliza principalmente los **SID (Security Identifier)** para identificar usuarios y grupos.

---

## SID (Security Identifier)

El SID es un identificador único asignado a cada usuario, grupo o equipo dentro de Windows.

Tiene una estructura similar a:

```text
S-1-5-21-xxxxxxxxxx-xxxxxxxxxx-xxxxxxxxxx-1001
```

Cada parte del SID tiene un significado concreto.

Ejemplo:

```text
S-1-5-21-123456789-987654321-456789123-1001
```

---

## Componentes del SID

Un SID está formado por:

### Autoridad de seguridad

Indica qué entidad creó el identificador.

Ejemplo:

```text
S-1-5
```

---

### Identificador del dominio o equipo

Permite diferenciar sistemas distintos.

Ejemplo:

```text
S-1-5-21-xxxxxxxxxx
```

---

### RID (Relative Identifier)

Es la parte final del SID y diferencia usuarios dentro del mismo dominio o equipo.

Ejemplo:

```text
S-1-5-21-xxxxx-xxxxx-xxxxx-1001
                                  ↑
                                  RID
```

---

# RID (Relative Identifier)

El RID identifica una cuenta concreta dentro de un sistema.

Algunos valores conocidos:

| RID | Cuenta |
|-|-|
| 500 | Administrador integrado |
| 501 | Invitado |
| 502 | Krbtgt |
| 1000+ | Usuarios creados posteriormente |

Ejemplo:

```text
Usuario:

Administrador


SID:

S-1-5-21-xxxxx-500
```

---

# Importancia del SID en Windows

El SID permite que Windows gestione permisos correctamente.

Los permisos de archivos y recursos no se asignan realmente al nombre del usuario, sino a su SID.

Ejemplo:

```text
Archivo:

Informe.pdf


Permiso:

SID del usuario


Windows consulta:

¿A qué usuario pertenece este SID?

↓

Aplica permisos
```

---

# Cambio de nombre de usuario en Windows

Modificar el nombre visible de una cuenta no cambia su SID.

Ejemplo:

Antes:

```text
Usuario:

juan
```

Después:

```text
Usuario:

juan.perez
```

El SID permanece igual:

```text
S-1-5-21-xxxxx-1005
```

Esto permite mantener permisos existentes.

---

# Identificadores en Linux

Linux utiliza principalmente dos identificadores:

- UID.
- GID.

---

# UID (User Identifier)

El UID es un número único asignado a cada usuario del sistema.

Ejemplo:

```text
Usuario:

juan


UID:

1001
```

El sistema utiliza este número internamente para identificar al propietario de archivos y procesos.

---

## Consultar UID

Comando:

```bash
id usuario
```

Ejemplo:

```bash
id juan
```

Resultado:

```text
uid=1001(juan)
gid=1001(juan)
```

---

# Tipos de UID en Linux

Linux utiliza diferentes rangos de UID.

---

## Usuario root

El usuario root siempre tiene:

```text
UID:

0
```

Ejemplo:

```text
root:x:0:0
```

---

## Usuarios del sistema

Normalmente utilizan UID bajos.

Ejemplo:

```text
www-data

UID:

33
```

Son utilizados por servicios.

---

## Usuarios normales

Habitualmente comienzan desde:

```text
1000
```

Ejemplo:

```text
juan

UID:

1001
```

---

# GID (Group Identifier)

El GID identifica un grupo dentro del sistema.

Cada usuario tiene asociado un grupo principal.

Ejemplo:

```text
Usuario:

juan


UID:

1001


Grupo:

ventas


GID:

1005
```

---

# Relación entre UID, GID y permisos

Linux utiliza UID y GID para decidir quién puede acceder a un archivo.

Ejemplo:

```text
Archivo:

documento.txt


Propietario:

UID 1001


Grupo:

GID 1005


Permisos:

rw-r-----
```

Interpretación:

```text
Propietario:

Lectura + escritura


Grupo:

Lectura


Otros:

Sin acceso
```

---

# Archivos donde se almacenan identificadores Linux

Linux guarda información de usuarios y grupos en diferentes archivos.

---

## /etc/passwd

Contiene información básica de usuarios.

Ejemplo:

```bash
cat /etc/passwd
```

Formato:

```text
usuario:x:UID:GID:comentario:home:shell
```

Ejemplo:

```text
juan:x:1001:1001:Juan:/home/juan:/bin/bash
```

---

## /etc/group

Contiene información sobre grupos.

Ejemplo:

```bash
cat /etc/group
```

Formato:

```text
grupo:x:GID:usuarios
```

---

## /etc/shadow

Contiene información relacionada con contraseñas cifradas.

Ejemplo:

```bash
cat /etc/shadow
```

Normalmente solo accesible por root.

---

# Comparación Windows y Linux

| Windows | Linux |
|-|-|
| SID | UID |
| RID | GID / identificadores internos |
| Dominio | Sistema local |
| Active Directory | /etc/passwd, LDAP |
| ACL basadas en SID | Permisos basados en UID/GID |

---

# Importancia de los identificadores

Los identificadores permiten:

- Diferenciar usuarios con nombres similares.
- Mantener permisos correctamente.
- Realizar auditorías.
- Gestionar accesos.
- Evitar conflictos de identidad.

Ejemplo:

```text
Usuario eliminado

↓

Nuevo usuario con mismo nombre

↓

Nuevo SID / UID

↓

No hereda permisos anteriores
```

---

# Ejemplo práctico

Un administrador elimina una cuenta:

```text
usuario:

carlos
```

Posteriormente crea otra:

```text
usuario:

carlos
```

Aunque el nombre sea igual:

```text
Cuenta antigua:

SID:
S-1-5-21-xxx-1005


Cuenta nueva:

SID:
S-1-5-21-xxx-1012
```

El sistema las considera identidades diferentes.

---

[⬆️ Volver al índice](#índice)

## Autenticación y autorización

### Introducción

La autenticación y la autorización son dos conceptos fundamentales dentro de la seguridad informática y la administración de sistemas.

Ambos procesos están relacionados con el control de acceso, pero cumplen funciones diferentes:

- La autenticación determina quién es un usuario.
- La autorización determina qué acciones puede realizar ese usuario.

Un sistema seguro debe verificar primero la identidad de una persona antes de permitirle acceder a recursos.

Ejemplo:

```text
Usuario intenta acceder

↓

Autenticación

¿Quién eres?

↓

Autorización

¿Qué puedes hacer?

↓

Acceso permitido
```

---

# Autenticación

### ¿Qué es la autenticación?

La autenticación es el proceso mediante el cual un sistema verifica la identidad de un usuario, dispositivo o servicio.

Su objetivo es responder a la pregunta:

```text
¿Quién eres?
```

Para ello se utilizan diferentes métodos de identificación.

---

# Factores de autenticación

Los métodos de autenticación se clasifican en diferentes factores.

---

## Algo que sabes

Es información que únicamente debería conocer el usuario.

Ejemplos:

- Contraseña.
- PIN.
- Preguntas de seguridad.

Ejemplo:

```text
Usuario:

beatriz


Contraseña:

********
```

---

## Algo que tienes

Es un elemento físico que posee el usuario.

Ejemplos:

- Token.
- Tarjeta inteligente.
- Llave de seguridad.
- Teléfono móvil.

Ejemplo:

```text
Usuario introduce contraseña

↓

Recibe código en móvil

↓

Acceso permitido
```

---

## Algo que eres

Utiliza características biométricas del usuario.

Ejemplos:

- Huella dactilar.
- Reconocimiento facial.
- Iris.

Ejemplo:

```text
Sensor biométrico

↓

Comparación

↓

Identidad confirmada
```

---

# Autenticación multifactor (MFA)

La autenticación multifactor combina dos o más factores diferentes para aumentar la seguridad.

Ejemplo:

```text
Contraseña

+

Código móvil

↓

Acceso permitido
```

La ventaja principal es que si un atacante obtiene una contraseña, todavía necesita el segundo factor.

---

# Métodos habituales de autenticación

## Usuario y contraseña

Es el método más común.

Funcionamiento:

```text
Usuario introduce credenciales

↓

Sistema comprueba información almacenada

↓

Permite o rechaza acceso
```

---

## Certificados digitales

Utilizan certificados criptográficos para verificar identidades.

Ejemplo:

- Acceso VPN.
- Servicios empresariales.
- Firmas digitales.

---

## Llaves SSH

En Linux, SSH permite autenticarse mediante pares de claves.

Funcionamiento:

```text
Clave privada

↓

Usuario


Clave pública

↓

Servidor
```

Ventajas:

- Mayor seguridad.
- Evita contraseñas.
- Permite automatización segura.

---

# Autorización

### ¿Qué es la autorización?

La autorización es el proceso mediante el cual el sistema determina qué recursos puede utilizar un usuario y qué acciones puede realizar.

Responde a la pregunta:

```text
¿Qué puedes hacer?
```

Ejemplo:

```text
Usuario autenticado:

juan


Sistema comprueba:

Grupo Ventas


Resultado:

Puede leer documentos comerciales
```

---

# Elementos utilizados en la autorización

La autorización depende principalmente de:

- Usuarios.
- Grupos.
- Roles.
- Permisos.
- Políticas de seguridad.

Ejemplo:

```text
Usuario

↓

Grupo

↓

Permisos

↓

Recurso
```

---

# Diferencia entre autenticación y autorización

| Autenticación | Autorización |
|-|-|
| Verifica identidad | Controla permisos |
| Responde "¿Quién eres?" | Responde "¿Qué puedes hacer?" |
| Ocurre primero | Ocurre después |
| Usa credenciales | Usa permisos y roles |

Ejemplo:

```text
1. Usuario introduce contraseña

↓

Autenticación correcta


2. Sistema revisa permisos

↓

Autorización


3. Acceso al recurso
```

---

# Modelos de autorización

Los sistemas utilizan diferentes modelos para gestionar permisos.

---

## DAC (Discretionary Access Control)

Control de acceso basado en el propietario del recurso.

El propietario decide quién tiene acceso.

Ejemplo:

```text
Usuario crea carpeta

↓

Decide quién puede acceder
```

Utilizado habitualmente en sistemas Windows y Linux.

---

## MAC (Mandatory Access Control)

Control de acceso obligatorio basado en políticas de seguridad.

Los usuarios no pueden modificar libremente los permisos.

Ejemplo:

- Sistemas militares.
- Entornos de alta seguridad.

---

## RBAC (Role Based Access Control)

Control basado en roles.

Los permisos se asignan a roles y los usuarios reciben esos roles.

Ejemplo:

```text
Rol:

Contabilidad


Permisos:

Acceso financiero


Usuario:

Ana
```

Muy utilizado en empresas.

---

## ABAC (Attribute Based Access Control)

Control basado en atributos.

Las decisiones dependen de características del usuario, recurso o contexto.

Ejemplo:

```text
Usuario:

Administrador


Ubicación:

Oficina


Horario:

Laboral


↓

Acceso permitido
```

---

# Proceso completo de acceso

Cuando un usuario intenta acceder a un recurso ocurre lo siguiente:

```text
Usuario solicita acceso

↓

Sistema identifica usuario

↓

Autenticación

↓

Consulta grupos y roles

↓

Comprueba permisos

↓

Autorización

↓

Acceso permitido o denegado
```

---

# Ejemplo práctico

Un empleado intenta acceder a una carpeta compartida:

```text
Usuario:

maria


Paso 1:

Introduce contraseña


Paso 2:

Sistema valida identidad


Paso 3:

Comprueba grupo:

RRHH


Paso 4:

Revisa permisos carpeta


Resultado:

Acceso permitido
```

---

# Fallos habituales

Una mala configuración de autenticación o autorización puede provocar problemas de seguridad.

---

## Contraseñas débiles

Ejemplo:

```text
Usuario:

admin

Contraseña:

123456
```

Riesgo:

- Acceso no autorizado.
- Robo de cuentas.

---

## Exceso de permisos

Ejemplo:

```text
Usuario estándar

↓

Permisos administrador
```

Riesgo:

- Escalada de privilegios.
- Daños accidentales.

---

## Cuentas compartidas

Ejemplo:

```text
Usuario:

administrador

Usado por varias personas
```

Problemas:

- No existe trazabilidad.
- Dificulta auditorías.

---

# Importancia en administración de sistemas

Una correcta gestión de autenticación y autorización permite:

- Proteger recursos.
- Controlar accesos.
- Detectar actividades sospechosas.
- Cumplir requisitos de seguridad.
- Aplicar mínimo privilegio.

---

[⬆️ Volver al índice](#índice)

## Gestión de usuarios en Windows

### Introducción

Windows ofrece diferentes herramientas para crear, modificar y administrar cuentas de usuario.

Dependiendo de la edición del sistema operativo y del entorno de trabajo, la gestión puede realizarse de forma local o mediante un dominio.

Las tareas más habituales son:

- Crear usuarios.
- Modificar cuentas.
- Restablecer contraseñas.
- Bloquear o desbloquear usuarios.
- Eliminar cuentas.
- Gestionar grupos.
- Asignar permisos.

---

# Usuarios locales y usuarios de dominio

Windows permite trabajar con dos tipos principales de cuentas.

---

## Usuarios locales

Las cuentas locales existen únicamente en un equipo.

Toda la información se almacena en el propio sistema operativo.

Ejemplo:

```text
Equipo:

PC-VENTAS-01

↓

Usuario:

beatriz
```

Características:

- Solo pueden iniciar sesión en ese equipo.
- No dependen de un servidor.
- Son habituales en ordenadores personales o pequeños entornos.

---

## Usuarios de dominio

Las cuentas de dominio son administradas desde un servidor, normalmente mediante Active Directory.

Ejemplo:

```text
Dominio:

empresa.local

↓

Usuario:

beatriz.lama

↓

Puede iniciar sesión en varios equipos
```

Ventajas:

- Administración centralizada.
- Políticas comunes.
- Gestión simplificada.
- Mayor control de seguridad.

---

# Herramientas gráficas

Windows incorpora varias herramientas para administrar usuarios.

---

## Configuración

Ruta:

```text
Configuración

↓

Cuentas
```

Permite:

- Cambiar contraseña.
- Modificar información del usuario.
- Administrar cuentas de Microsoft.
- Gestionar opciones de inicio de sesión.

---

## Usuarios y grupos locales

Herramienta:

```text
lusrmgr.msc
```

Permite administrar:

- Usuarios.
- Grupos.
- Contraseñas.
- Deshabilitación de cuentas.
- Pertenencia a grupos.

> **Nota:** Disponible únicamente en las ediciones Professional, Enterprise y Server de Windows.

---

## Administración de equipos

Herramienta:

```text
compmgmt.msc
```

Ruta:

```text
Administración de equipos

↓

Usuarios y grupos locales
```

Desde aquí también es posible gestionar usuarios locales.

---

# Administración mediante CMD

Windows permite gestionar usuarios desde el Símbolo del sistema.

---

## Mostrar usuarios

Comando:

```cmd
net user
```

Ejemplo:

```cmd
C:\> net user
```

Muestra todas las cuentas locales existentes.

---

## Crear un usuario

Sintaxis:

```cmd
net user nombre contraseña /add
```

Ejemplo:

```cmd
net user prueba Password123 /add
```

---

## Eliminar un usuario

Sintaxis:

```cmd
net user nombre /delete
```

Ejemplo:

```cmd
net user prueba /delete
```

---

## Cambiar contraseña

Sintaxis:

```cmd
net user nombre nueva_contraseña
```

Ejemplo:

```cmd
net user beatriz NuevaPassword123
```

---

# Administración mediante PowerShell

PowerShell proporciona cmdlets específicos para gestionar usuarios locales.

---

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

Ejemplo:

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

# Administración de grupos

Los usuarios pueden añadirse o eliminarse de grupos locales.

---

## Mostrar grupos

CMD:

```cmd
net localgroup
```

PowerShell:

```powershell
Get-LocalGroup
```

---

## Añadir usuario a un grupo

CMD:

```cmd
net localgroup Administradores beatriz /add
```

PowerShell:

```powershell
Add-LocalGroupMember `
-Group "Administradores" `
-Member "beatriz"
```

---

## Eliminar usuario de un grupo

CMD:

```cmd
net localgroup Administradores beatriz /delete
```

PowerShell:

```powershell
Remove-LocalGroupMember `
-Group "Administradores" `
-Member "beatriz"
```

---

# Restablecimiento de contraseñas

Un administrador puede cambiar la contraseña de otro usuario.

Desde interfaz gráfica:

```text
lusrmgr.msc

↓

Usuario

↓

Establecer contraseña
```

Desde CMD:

```cmd
net user usuario NuevaPassword123
```

Desde PowerShell:

```powershell
Set-LocalUser
```

---

# Bloqueo y deshabilitación de cuentas

No siempre es recomendable eliminar una cuenta.

En muchas ocasiones es preferible deshabilitarla.

Ejemplo:

```text
Empleado deja la empresa

↓

Cuenta deshabilitada

↓

Información conservada
```

Ventajas:

- Mantiene el historial.
- Conserva permisos.
- Permite reactivarla posteriormente.

---

# Eliminación de cuentas

Cuando una cuenta ya no es necesaria puede eliminarse.

Antes de hacerlo es recomendable:

- Revisar archivos personales.
- Transferir información si es necesario.
- Comprobar permisos asignados.
- Verificar que no sea una cuenta de servicio.

---

# Gestión de perfiles de usuario

Cada usuario dispone de un perfil donde se almacena su configuración.

Ubicación habitual:

```text
C:\Users\
```

Ejemplo:

```text
C:\Users\beatriz
```

Contiene:

- Escritorio.
- Documentos.
- Descargas.
- Configuración de aplicaciones.
- Datos personales.

---

# Auditoría de usuarios

Windows registra eventos relacionados con las cuentas de usuario.

Los registros pueden consultarse mediante:

```text
eventvwr.msc
```

Registros habituales:

- Inicio de sesión.
- Cierre de sesión.
- Creación de usuarios.
- Eliminación de cuentas.
- Cambios de contraseña.
- Modificación de grupos.

---

# Ejemplo práctico

Un nuevo empleado se incorpora al departamento de ventas.

Proceso:

```text
Crear usuario

↓

Asignar contraseña

↓

Añadir al grupo Ventas

↓

Configurar perfil

↓

Verificar acceso

↓

Usuario listo para trabajar
```

---

[⬆️ Volver al índice](#índice)

## Gestión de usuarios en Linux

### Introducción

Linux gestiona los usuarios mediante un sistema basado en identificadores únicos (UID), grupos (GID) y permisos sobre archivos y recursos.

Toda la información de las cuentas se almacena en archivos del sistema, lo que permite administrar usuarios tanto mediante herramientas gráficas como, principalmente, desde la línea de comandos.

La mayoría de tareas de administración en Linux se realizan utilizando comandos específicos ejecutados por el usuario **root** o mediante **sudo**.

Las tareas más habituales son:

- Crear usuarios.
- Modificar cuentas.
- Cambiar contraseñas.
- Eliminar usuarios.
- Gestionar grupos.
- Bloquear cuentas.
- Configurar permisos.

---

# Archivos relacionados con los usuarios

Linux almacena la información de usuarios y grupos en varios archivos importantes.

---

## /etc/passwd

Contiene la información básica de cada usuario.

Consultar:

```bash
cat /etc/passwd
```

Formato:

```text
usuario:x:UID:GID:comentario:home:shell
```

Ejemplo:

```text
beatriz:x:1001:1001:Beatriz:/home/beatriz:/bin/bash
```

---

## /etc/shadow

Almacena las contraseñas cifradas y la información relacionada con ellas.

Consultar:

```bash
sudo cat /etc/shadow
```

Este archivo únicamente puede ser leído por usuarios con privilegios.

---

## /etc/group

Contiene la información sobre los grupos existentes.

Consultar:

```bash
cat /etc/group
```

Formato:

```text
grupo:x:GID:usuarios
```

Ejemplo:

```text
ventas:x:1005:juan,ana,pedro
```

---

# Crear usuarios

El comando más habitual es:

```bash
useradd
```

Sintaxis:

```bash
sudo useradd usuario
```

Ejemplo:

```bash
sudo useradd beatriz
```

Este comando crea la cuenta, aunque normalmente es necesario configurar una contraseña y el directorio personal.

---

## Crear usuario con directorio personal

```bash
sudo useradd -m beatriz
```

La opción:

```text
-m
```

crea automáticamente:

```text
/home/beatriz
```

---

## Crear usuario con shell específica

```bash
sudo useradd -m -s /bin/bash beatriz
```

---

# Establecer contraseña

Después de crear un usuario, normalmente se asigna una contraseña.

Comando:

```bash
sudo passwd beatriz
```

El sistema solicitará introducir la nueva contraseña dos veces.

---

# Modificar usuarios

Linux permite modificar diferentes propiedades de una cuenta mediante:

```bash
usermod
```

---

## Cambiar nombre

```bash
sudo usermod -l nuevo_nombre usuario
```

Ejemplo:

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

---

# Eliminar usuarios

Eliminar únicamente la cuenta:

```bash
sudo userdel usuario
```

Ejemplo:

```bash
sudo userdel beatriz
```

---

## Eliminar usuario y directorio personal

```bash
sudo userdel -r beatriz
```

La opción:

```text
-r
```

también elimina:

```text
/home/beatriz
```

---

# Bloquear y desbloquear cuentas

En muchas ocasiones es preferible bloquear una cuenta antes que eliminarla.

---

## Bloquear contraseña

```bash
sudo passwd -l usuario
```

Ejemplo:

```bash
sudo passwd -l beatriz
```

---

## Desbloquear cuenta

```bash
sudo passwd -u beatriz
```

---

# Gestión de grupos

Linux utiliza grupos para organizar permisos.

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

La opción:

```text
-aG
```

significa:

- Añadir.
- Mantener los grupos existentes.

---

## Consultar grupos de un usuario

```bash
groups beatriz
```

O bien:

```bash
id beatriz
```

Ejemplo:

```text
uid=1001(beatriz)

gid=1001(beatriz)

groups=1001(beatriz),1005(ventas)
```

---

# Información sobre usuarios

Consultar información de la cuenta actual:

```bash
whoami
```

---

Consultar el identificador:

```bash
id
```

---

Ver usuarios conectados:

```bash
who
```

---

Ver actividad reciente:

```bash
last
```

---

# Directorio personal

Cada usuario posee normalmente un directorio personal.

Ubicación habitual:

```text
/home/usuario
```

Ejemplo:

```text
/home/beatriz
```

Este directorio suele contener:

- Documentos.
- Descargas.
- Configuración personal.
- Archivos ocultos.
- Configuración del shell.

---

# Shell de usuario

La shell es el programa que se ejecuta al iniciar sesión.

Consultar la shell actual:

```bash
echo $SHELL
```

Shells habituales:

```text
/bin/bash

/bin/zsh

/bin/sh
```

---

# Uso de sudo

En la mayoría de distribuciones Linux no se trabaja directamente como **root**.

En su lugar se utiliza:

```bash
sudo
```

Ejemplo:

```bash
sudo apt update
```

Ventajas:

- Mayor seguridad.
- Registro de acciones.
- Menor riesgo de errores.

---

# Auditoría de usuarios

Linux registra información relacionada con accesos y autenticación.

Archivos habituales:

```text
/var/log/auth.log
```

o

```text
journalctl
```

Consultar accesos:

```bash
last
```

Consultar autenticaciones:

```bash
sudo journalctl -u ssh
```

---

# Ejemplo práctico

Se incorpora un nuevo empleado al departamento de ventas.

Proceso:

```text
Crear usuario

↓

Asignar contraseña

↓

Crear directorio personal

↓

Añadir al grupo Ventas

↓

Verificar acceso

↓

Usuario operativo
```

Comandos:

```bash
sudo useradd -m beatriz

sudo passwd beatriz

sudo usermod -aG ventas beatriz
```

---

[⬆️ Volver al índice](#índice)

## Active Directory y usuarios empresariales

### Introducción

En entornos empresariales es habitual que los usuarios no se gestionen de forma individual en cada equipo, sino de manera centralizada.

**Active Directory (AD)** es el servicio de directorio desarrollado por Microsoft que permite administrar usuarios, equipos, grupos y recursos desde un único punto.

Gracias a Active Directory, un usuario puede utilizar las mismas credenciales para acceder a distintos equipos y recursos de la organización, simplificando la administración y mejorando la seguridad.

Ejemplo:

```text
Administrador

↓

Active Directory

↓

Usuarios

Equipos

Grupos

Recursos
```

---

# ¿Qué es Active Directory?

Active Directory es un servicio de directorio que almacena información sobre los objetos de una red y permite administrarlos de forma centralizada.

Entre los objetos más habituales se encuentran:

- Usuarios.
- Equipos.
- Grupos.
- Impresoras.
- Carpetas compartidas.
- Unidades Organizativas (OU).
- Políticas de grupo (GPO).

---

# Ventajas de Active Directory

Implementar Active Directory aporta numerosas ventajas.

Permite:

- Centralizar la administración.
- Gestionar usuarios desde un único servidor.
- Aplicar políticas comunes.
- Administrar permisos de forma sencilla.
- Facilitar el inicio de sesión en cualquier equipo del dominio.
- Mejorar la seguridad de la infraestructura.

Ejemplo:

```text
Usuario

↓

Inicia sesión

↓

Accede a cualquier equipo del dominio

↓

Obtiene su configuración automáticamente
```

---

# Componentes principales

Un entorno de Active Directory está formado por varios elementos.

---

## Dominio

El dominio es la unidad principal de administración.

Agrupa usuarios, equipos y recursos bajo una misma base de datos.

Ejemplo:

```text
empresa.local
```

Todos los equipos unidos al dominio comparten la misma autenticación.

---

## Controlador de dominio (Domain Controller)

El controlador de dominio es el servidor que almacena la base de datos de Active Directory.

Funciones principales:

- Autenticar usuarios.
- Autorizar accesos.
- Gestionar políticas.
- Administrar objetos del dominio.

Ejemplo:

```text
Usuario inicia sesión

↓

Controlador de dominio

↓

Autenticación correcta
```

---

## Objetos

Todo elemento administrado dentro de Active Directory recibe el nombre de objeto.

Ejemplos:

- Usuario.
- Grupo.
- Equipo.
- Impresora.
- Unidad Organizativa.

---

# Usuarios del dominio

Los usuarios del dominio pueden iniciar sesión en cualquier equipo unido al dominio, siempre que tengan permisos.

Ejemplo:

```text
Dominio:

empresa.local

↓

Usuario:

beatriz.lama

↓

Acceso a PC01

↓

Acceso a PC02

↓

Acceso a SERVIDOR01
```

---

# Equipos del dominio

Los equipos también son objetos dentro de Active Directory.

Cada ordenador unido al dominio dispone de su propia cuenta.

Ejemplo:

```text
PC-VENTAS-01

↓

Objeto en Active Directory
```

Esto permite aplicar políticas específicas a cada equipo.

---

# Unidades Organizativas (OU)

Las OU permiten organizar los objetos del dominio de forma lógica.

Ejemplo:

```text
empresa.local

│

├── Dirección

├── Administración

├── Ventas

└── Informática
```

Dentro de cada OU pueden almacenarse:

- Usuarios.
- Equipos.
- Grupos.
- Otras OU.

---

# Grupos en Active Directory

Los grupos facilitan la asignación de permisos.

Ejemplo:

```text
Grupo:

Ventas

↓

Usuarios:

Ana

Juan

Pedro
```

En lugar de asignar permisos a cada usuario, se asignan al grupo.

---

# Políticas de Grupo (GPO)

Las **Group Policy Objects (GPO)** permiten aplicar configuraciones automáticamente a usuarios y equipos.

Ejemplos de configuraciones:

- Fondo de pantalla.
- Restricciones del Panel de control.
- Configuración del firewall.
- Instalación automática de software.
- Políticas de contraseña.

Ejemplo:

```text
Administrador

↓

GPO

↓

Usuarios del dominio

↓

Configuración aplicada automáticamente
```

---

# Administración mediante Active Directory Users and Computers

La herramienta principal para administrar usuarios es:

```text
Active Directory Users and Computers
```

Comando:

```text
dsa.msc
```

Permite:

- Crear usuarios.
- Eliminar cuentas.
- Gestionar grupos.
- Mover objetos.
- Restablecer contraseñas.
- Deshabilitar usuarios.

---

# Ciclo de vida de un usuario

En un entorno empresarial, las cuentas siguen normalmente un ciclo de vida.

```text
Alta

↓

Asignación de grupos

↓

Asignación de permisos

↓

Cambios de departamento

↓

Deshabilitación

↓

Eliminación
```

Una correcta gestión evita cuentas huérfanas y accesos innecesarios.

---

# Delegación de administración

No siempre es necesario que un único administrador gestione todo el dominio.

Active Directory permite delegar tareas concretas.

Ejemplos:

- Restablecer contraseñas.
- Crear usuarios.
- Administrar una OU específica.

Esto permite distribuir responsabilidades sin conceder privilegios de administrador del dominio.

---

# Auditoría de usuarios

Las acciones realizadas sobre los usuarios pueden registrarse para su posterior revisión.

Ejemplos de eventos:

- Inicio de sesión.
- Cambio de contraseña.
- Bloqueo de cuenta.
- Creación de usuarios.
- Eliminación de cuentas.
- Cambios de pertenencia a grupos.

Esta información es fundamental para auditorías y análisis de incidentes.

---

# Buenas prácticas en Active Directory

Algunas recomendaciones son:

- Organizar correctamente las OU.
- Utilizar grupos para asignar permisos.
- Aplicar el principio de mínimo privilegio.
- Revisar periódicamente las cuentas inactivas.
- Deshabilitar cuentas antes de eliminarlas.
- Evitar utilizar cuentas administrativas para tareas diarias.
- Documentar los cambios importantes.

---

# Ejemplo práctico

Una nueva empleada se incorpora al departamento de ventas.

Proceso:

```text
Crear usuario

↓

Añadir a la OU Ventas

↓

Agregar al grupo GG_Ventas

↓

Aplicar GPO del departamento

↓

Asignar permisos compartidos

↓

Usuario operativo
```

Gracias a Active Directory, toda la configuración se aplica automáticamente sin necesidad de configurar manualmente cada equipo.

---

[⬆️ Volver al índice](#índice)

## Permisos de archivos y recursos

### Introducción

Los permisos son el mecanismo utilizado por los sistemas operativos para controlar qué acciones puede realizar un usuario sobre un recurso determinado.

Un recurso puede ser:

- Un archivo.
- Una carpeta.
- Una impresora.
- Una unidad de red.
- Un servicio.
- Una base de datos.
- Un dispositivo.

Cuando un usuario intenta acceder a un recurso, el sistema comprueba los permisos asociados a su identidad antes de permitir o denegar la operación.

Ejemplo:

```text
Usuario

↓

Solicita acceso

↓

Sistema comprueba permisos

↓

Acceso permitido o denegado
```

---

# ¿Qué son los permisos?

Un permiso es una autorización que permite realizar una acción concreta sobre un recurso.

Los permisos determinan qué usuarios pueden:

- Leer información.
- Modificar archivos.
- Ejecutar programas.
- Eliminar contenido.
- Cambiar permisos.
- Tomar posesión de recursos.

Ejemplo:

```text
Archivo

↓

Permisos

↓

Usuario autorizado
```

---

# Tipos de recursos

Los permisos pueden aplicarse sobre diferentes tipos de recursos.

Ejemplos:

```text
Archivo

Carpeta

Unidad compartida

Impresora

Servicio

Base de datos

Aplicación
```

Cada tipo de recurso puede disponer de un sistema de permisos específico.

---

# Permisos en Windows (NTFS)

Windows utiliza el sistema de archivos **NTFS**, que incorpora un modelo avanzado de permisos.

Los permisos pueden asignarse a:

- Usuarios.
- Grupos.
- Cuentas del sistema.

---

## Permisos básicos

Los permisos básicos más habituales son:

### Control total

Permite realizar cualquier acción sobre el recurso.

Incluye:

- Leer.
- Escribir.
- Modificar.
- Eliminar.
- Cambiar permisos.
- Tomar posesión.

---

### Modificar

Permite:

- Leer.
- Escribir.
- Ejecutar.
- Eliminar.

No permite modificar permisos ni cambiar el propietario.

---

### Lectura y ejecución

Permite:

- Abrir archivos.
- Ejecutar programas.
- Leer información.

---

### Lectura

Permite visualizar el contenido, pero no modificarlo.

---

### Escritura

Permite crear y modificar archivos sin eliminarlos.

---

# Permisos avanzados de NTFS

Además de los permisos básicos, NTFS dispone de permisos avanzados.

Ejemplos:

- Crear archivos.
- Crear carpetas.
- Eliminar subcarpetas.
- Leer atributos.
- Escribir atributos.
- Cambiar permisos.
- Tomar posesión.

Estos permisos permiten un control mucho más preciso sobre los recursos.

---

# Permisos compartidos

Cuando una carpeta se comparte por red, Windows aplica dos niveles de permisos.

```text
Permisos compartidos

+

Permisos NTFS
```

El permiso efectivo será siempre el más restrictivo.

Ejemplo:

```text
Compartido:

Lectura

NTFS:

Control total

↓

Resultado:

Lectura
```

---

# Permisos en Linux

Linux utiliza un sistema de permisos mucho más simple basado en tres tipos de usuarios.

```text
Propietario

Grupo

Otros usuarios
```

Cada uno puede tener tres permisos básicos.

---

## Lectura (Read)

Representado por:

```text
r
```

Permite visualizar el contenido de un archivo.

Valor:

```text
4
```

---

## Escritura (Write)

Representado por:

```text
w
```

Permite modificar archivos.

Valor:

```text
2
```

---

## Ejecución (Execute)

Representado por:

```text
x
```

Permite ejecutar programas o scripts.

Valor:

```text
1
```

---

# Representación de permisos

Ejemplo:

```text
-rwxr-xr--
```

Interpretación:

```text
-

Archivo


rwx

Propietario


r-x

Grupo


r--

Otros
```

---

# Permisos numéricos

Linux también permite representar permisos mediante números.

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

Ejemplo:

```bash
chmod 755 archivo.sh
```

Equivale a:

```text
rwx

r-x

r-x
```

---

# Modificación de permisos

Linux utiliza el comando:

```bash
chmod
```

Ejemplo:

```bash
chmod 644 documento.txt
```

Otro ejemplo:

```bash
chmod +x script.sh
```

---

# Cambio de propietario

El propietario puede modificarse mediante:

```bash
chown
```

Ejemplo:

```bash
sudo chown beatriz documento.txt
```

Cambiar propietario y grupo:

```bash
sudo chown beatriz:ventas documento.txt
```

---

# Cambio de grupo

Comando:

```bash
chgrp
```

Ejemplo:

```bash
sudo chgrp ventas informe.xlsx
```

---

# Permisos efectivos

El permiso efectivo es el resultado final de combinar:

- Identidad del usuario.
- Grupo.
- Permisos asignados.
- Herencia.
- ACL (si existen).

Ejemplo:

```text
Usuario

↓

Grupo

↓

Permisos

↓

Acceso final
```

---

# Principio del mínimo privilegio

Uno de los principios fundamentales de seguridad consiste en conceder únicamente los permisos necesarios para realizar una tarea.

Ejemplo correcto:

```text
Empleado

↓

Lectura carpeta RRHH
```

Ejemplo incorrecto:

```text
Empleado

↓

Control total servidor
```

Cuantos más permisos tenga una cuenta, mayor será el riesgo en caso de compromiso.

---

# Problemas habituales

Una mala gestión de permisos puede provocar:

- Accesos no autorizados.
- Modificación accidental de información.
- Eliminación de archivos.
- Robo de datos.
- Escalada de privilegios.

Ejemplo:

```text
Carpeta compartida

↓

Todos tienen Control total

↓

Borrado accidental
```

---

# Ejemplo práctico

Una empresa dispone de una carpeta compartida para el departamento de Finanzas.

Configuración:

```text
Grupo:

GG_Finanzas

↓

Permiso NTFS:

Modificar

↓

Usuarios:

Ana

Pedro

Marta
```

Cuando un nuevo empleado se incorpora:

```text
Nuevo usuario

↓

Añadir al grupo GG_Finanzas

↓

Obtiene permisos automáticamente
```

No es necesario modificar los permisos de la carpeta.

---

[⬆️ Volver al índice](#índice)

## Listas de Control de Acceso (ACL)

### Introducción

Las **Listas de Control de Acceso** o **ACL (Access Control List)** son un mecanismo utilizado por los sistemas operativos para definir de forma detallada qué usuarios o grupos pueden acceder a un recurso y qué acciones pueden realizar sobre él.

Mientras que los permisos básicos permiten un control general, las ACL ofrecen una administración mucho más granular y flexible.

Las ACL son ampliamente utilizadas en:

- Sistemas Windows (NTFS).
- Sistemas Linux compatibles con POSIX ACL.
- Servidores de archivos.
- NAS.
- Recursos compartidos.

---

# ¿Qué es una ACL?

Una ACL es una lista formada por una o varias entradas que especifican los permisos de distintos usuarios o grupos sobre un recurso.

Cada entrada recibe el nombre de **ACE (Access Control Entry)**.

Ejemplo:

```text
Archivo

↓

ACL

├── Ana → Lectura

├── Pedro → Modificar

└── Administradores → Control total
```

---

# Componentes de una ACL

Una ACL está formada por diferentes elementos.

---

## Recurso

Es el objeto sobre el que se aplican los permisos.

Ejemplos:

- Archivo.
- Carpeta.
- Impresora.
- Unidad compartida.

---

## Identidad

Indica quién recibirá los permisos.

Puede ser:

- Usuario.
- Grupo.
- Cuenta del sistema.

Ejemplo:

```text
Usuario:

beatriz
```

---

## Permiso

Define qué acciones podrá realizar la identidad.

Ejemplos:

- Lectura.
- Escritura.
- Modificación.
- Control total.

---

## Tipo de acceso

Cada entrada puede permitir o denegar permisos.

Ejemplo:

```text
Permitir

↓

Lectura
```

o

```text
Denegar

↓

Eliminar archivos
```

---

# Funcionamiento de una ACL

Cuando un usuario intenta acceder a un recurso, el sistema sigue un proceso similar al siguiente:

```text
Usuario solicita acceso

↓

Sistema identifica usuario

↓

Consulta la ACL

↓

Comprueba permisos

↓

Permite o deniega acceso
```

---

# ACL en Windows

Windows utiliza ACL en el sistema de archivos **NTFS**.

Cada archivo y carpeta dispone de una lista de permisos propia.

Ejemplo:

```text
Carpeta

↓

Propiedades

↓

Seguridad

↓

Usuarios y permisos
```

---

## Entradas de la ACL

Cada usuario o grupo tiene su propia entrada.

Ejemplo:

| Usuario o grupo | Permisos |
|-----------------|----------|
| Administradores | Control total |
| Ventas | Modificar |
| Invitados | Lectura |

---

## Permitir y denegar

Windows permite definir permisos de dos tipos.

---

### Permitir

Autoriza una acción.

Ejemplo:

```text
Usuario:

Ana

↓

Permitir lectura
```

---

### Denegar

Bloquea una acción incluso si otro permiso pudiera concederla.

Ejemplo:

```text
Usuario:

Pedro

↓

Denegar eliminación
```

Las entradas de denegación deben utilizarse con precaución, ya que pueden generar conflictos difíciles de administrar.

---

# ACL en Linux

Linux dispone de permisos tradicionales (propietario, grupo y otros), pero también puede utilizar ACL para asignar permisos más específicos.

Esto permite conceder permisos individuales sin modificar los permisos generales del archivo.

---

## Consultar ACL

Comando:

```bash
getfacl archivo.txt
```

Ejemplo:

```bash
getfacl informe.pdf
```

---

## Asignar ACL

Comando:

```bash
setfacl
```

Ejemplo:

```bash
setfacl -m u:beatriz:rwx informe.pdf
```

Significado:

- **u** → Usuario.
- **beatriz** → Usuario.
- **rwx** → Permisos.

---

## Eliminar una ACL

Ejemplo:

```bash
setfacl -x u:beatriz informe.pdf
```

---

# Ventajas de utilizar ACL

Las ACL ofrecen numerosas ventajas frente a los permisos tradicionales.

Permiten:

- Asignar permisos a usuarios concretos.
- Evitar crear grupos innecesarios.
- Gestionar permisos complejos.
- Adaptarse mejor a entornos empresariales.

Ejemplo:

```text
Archivo

↓

Permisos generales

↓

ACL específica

↓

Usuario adicional autorizado
```

---

# Desventajas de las ACL

Una mala gestión puede provocar:

- Configuraciones difíciles de entender.
- Mayor complejidad administrativa.
- Conflictos entre permisos.
- Problemas durante auditorías.

Por ello es recomendable documentar correctamente su uso.

---

# ACL y herencia

Las ACL pueden heredarse desde carpetas superiores.

Ejemplo:

```text
Empresa

↓

Finanzas

↓

Facturas

↓

Archivo.xlsx
```

Si la carpeta **Finanzas** tiene permisos heredables, el archivo también los recibirá automáticamente.

La herencia se estudiará con mayor detalle en el siguiente apartado.

---

# ACL y permisos efectivos

El permiso final de un usuario depende de varios factores:

- Permisos directos.
- Pertenencia a grupos.
- ACL.
- Herencia.
- Entradas de denegación.

Ejemplo:

```text
Usuario

↓

Grupo

↓

ACL

↓

Permiso efectivo
```

---

# Buen uso de las ACL

Las ACL deben utilizarse cuando los permisos tradicionales no sean suficientes.

Ejemplos adecuados:

- Permitir acceso a un único usuario.
- Compartir un archivo entre departamentos.
- Conceder permisos temporales.
- Gestionar excepciones concretas.

Si muchos usuarios necesitan los mismos permisos, suele ser preferible utilizar grupos.

---

# Ejemplo práctico

Una carpeta contiene información confidencial.

Configuración inicial:

```text
Grupo RRHH

↓

Modificar
```

Posteriormente un auditor necesita acceso únicamente durante una semana.

En lugar de modificar el grupo:

```text
Carpeta

↓

ACL

↓

Usuario auditor

↓

Lectura
```

Una vez finalizada la auditoría, la entrada de la ACL puede eliminarse sin afectar al resto de usuarios.

---

[⬆️ Volver al índice](#índice)

## Herencia de permisos

### Introducción

La herencia de permisos es un mecanismo que permite que archivos y carpetas reciban automáticamente los permisos definidos en un recurso superior.

Su objetivo es simplificar la administración y garantizar que la estructura de permisos se mantenga uniforme sin necesidad de configurar cada elemento individualmente.

La herencia está presente en sistemas como **Windows (NTFS)** y también puede encontrarse en determinados entornos Linux mediante ACL.

Ejemplo:

```text
Empresa

↓

Finanzas

↓

Facturas

↓

2026.xlsx
```

Si la carpeta **Empresa** tiene permisos configurados para el grupo *Finanzas*, estos podrán heredarse automáticamente por las carpetas y archivos contenidos en ella.

---

# ¿Cómo funciona la herencia?

Cuando se crea un nuevo archivo o carpeta dentro de otra carpeta, el sistema puede copiar automáticamente los permisos del elemento padre.

Ejemplo:

```text
Carpeta principal

↓

Permisos definidos

↓

Nueva carpeta creada

↓

Permisos heredados
```

Esto evita tener que configurar manualmente los permisos de cada nuevo recurso.

---

# Elemento padre y elemento hijo

En la herencia existen dos conceptos principales.

---

## Elemento padre

Es el recurso que contiene otros elementos y desde el que se heredan los permisos.

Ejemplo:

```text
Empresa
```

---

## Elemento hijo

Es el recurso que recibe automáticamente los permisos del elemento superior.

Ejemplo:

```text
Empresa

↓

Finanzas

↓

Presupuestos.xlsx
```

En este caso:

- **Empresa** es el elemento padre.
- **Finanzas** y **Presupuestos.xlsx** son elementos hijos.

---

# Herencia en Windows (NTFS)

Windows utiliza la herencia de permisos de forma predeterminada en el sistema de archivos NTFS.

Cuando una carpeta tiene habilitada la herencia, todos los archivos y subcarpetas creados dentro de ella reciben automáticamente los mismos permisos.

Ejemplo:

```text
Carpeta Recursos Humanos

↓

Grupo RRHH

↓

Modificar

↓

Todos los documentos heredan ese permiso
```

---

## Visualizar la herencia

Ruta:

```text
Propiedades

↓

Seguridad

↓

Opciones avanzadas
```

Desde esta ventana es posible comprobar:

- Qué permisos son heredados.
- Qué permisos son explícitos.
- Desde qué carpeta proceden.

---

# Permisos heredados y permisos explícitos

Windows diferencia entre dos tipos de permisos.

---

## Permisos heredados

Proceden de una carpeta superior.

Ejemplo:

```text
Empresa

↓

Ventas

↓

Clientes.xlsx

↓

Permisos heredados
```

---

## Permisos explícitos

Son permisos configurados directamente sobre un recurso concreto.

Ejemplo:

```text
Clientes.xlsx

↓

Usuario Director

↓

Control total
```

Este permiso solo afecta a ese archivo.

---

# Deshabilitar la herencia

En determinadas situaciones puede ser necesario impedir que un recurso continúe heredando permisos.

Ejemplo:

```text
Carpeta General

↓

Carpeta Dirección

↓

Información confidencial
```

En este caso puede romperse la herencia para que únicamente determinados usuarios puedan acceder.

---

## Opciones al romper la herencia

Windows ofrece dos posibilidades.

### Convertir permisos heredados en permisos explícitos

Los permisos actuales se mantienen, pero dejan de depender del elemento padre.

Ejemplo:

```text
Permisos heredados

↓

Convertir

↓

Permisos propios
```

---

### Eliminar permisos heredados

El recurso deja de tener los permisos recibidos del elemento padre.

Posteriormente deberán asignarse nuevos permisos manualmente.

---

# Ventajas de la herencia

La herencia facilita enormemente la administración.

Permite:

- Reducir trabajo administrativo.
- Mantener configuraciones uniformes.
- Evitar errores humanos.
- Simplificar la creación de nuevos recursos.

Ejemplo:

```text
Nueva carpeta

↓

Permisos heredados automáticamente

↓

Lista para utilizar
```

---

# Inconvenientes de la herencia

Si la estructura no está correctamente diseñada pueden aparecer problemas.

Ejemplos:

- Accesos innecesarios.
- Usuarios con permisos excesivos.
- Dificultad para localizar permisos incorrectos.
- Propagación de errores de configuración.

---

# Herencia y Active Directory

Aunque Active Directory administra objetos distintos a los archivos, también utiliza el concepto de herencia.

Ejemplos:

- Políticas de Grupo (GPO).
- Delegación de permisos.
- Configuración de Unidades Organizativas (OU).

Ejemplo:

```text
Empresa

↓

OU Ventas

↓

Usuarios

↓

Aplicación automática de políticas
```

---

# Herencia en Linux

Linux no utiliza un sistema de herencia tan completo como NTFS para los permisos tradicionales.

Sin embargo, cuando se emplean **ACL**, es posible definir permisos por defecto que heredarán los nuevos archivos y carpetas.

Ejemplo:

Consultar ACL:

```bash
getfacl carpeta
```

Asignar ACL por defecto:

```bash
setfacl -d -m u:beatriz:rwx carpeta
```

Los nuevos archivos creados dentro de esa carpeta heredarán dicha configuración.

---

# Buenas prácticas

Para utilizar correctamente la herencia se recomienda:

- Diseñar correctamente la estructura de carpetas.
- Utilizar grupos en lugar de usuarios individuales.
- Evitar romper la herencia salvo cuando sea necesario.
- Revisar periódicamente los permisos heredados.
- Documentar las excepciones.

---

# Ejemplo práctico

Una empresa dispone de la siguiente estructura:

```text
Empresa

├── Administración

├── Finanzas

└── RRHH
```

Cada carpeta tiene asignados permisos específicos para su departamento.

Cuando se crea un nuevo archivo:

```text
Empresa

↓

Finanzas

↓

Balance2026.xlsx
```

El archivo recibe automáticamente los permisos de la carpeta **Finanzas**, sin necesidad de configurarlos manualmente.

---

[⬆️ Volver al índice](#índice)

## Roles y privilegios administrativos

### Introducción

No todos los usuarios de un sistema necesitan el mismo nivel de acceso. Mientras que un usuario estándar puede trabajar con aplicaciones y documentos, un administrador necesita permisos adicionales para configurar el sistema, gestionar usuarios o instalar software.

Los **roles** permiten asignar responsabilidades concretas a los usuarios, mientras que los **privilegios** determinan las acciones que esos usuarios pueden realizar.

Una correcta asignación de roles y privilegios es fundamental para mantener la seguridad de una infraestructura y reducir el riesgo de accesos no autorizados.

---

# ¿Qué es un rol?

Un rol es un conjunto de funciones y responsabilidades asignadas a un usuario o grupo de usuarios.

En lugar de conceder permisos individuales a cada persona, se asigna un rol con los permisos necesarios para desempeñar una determinada función.

Ejemplos de roles:

- Administrador de sistemas.
- Técnico de soporte.
- Responsable de Recursos Humanos.
- Administrador de bases de datos.
- Usuario estándar.

Ejemplo:

```text
Usuario

↓

Rol

↓

Permisos asociados
```

---

# ¿Qué es un privilegio?

Un privilegio es una autorización especial que permite realizar determinadas acciones administrativas sobre el sistema.

Algunos ejemplos son:

- Crear usuarios.
- Instalar software.
- Cambiar configuraciones del sistema.
- Modificar permisos.
- Gestionar servicios.
- Reiniciar servidores.

Ejemplo:

```text
Usuario administrador

↓

Privilegio

↓

Instalar software
```

---

# Diferencia entre permisos y privilegios

Aunque suelen confundirse, no son lo mismo.

| Permisos | Privilegios |
|----------|-------------|
| Controlan el acceso a recursos | Permiten realizar acciones administrativas |
| Se aplican sobre archivos, carpetas o recursos | Se aplican sobre el sistema operativo |
| Ejemplo: leer un archivo | Ejemplo: crear un usuario |

---

# Tipos de roles

Dependiendo de la organización, pueden existir diferentes roles.

---

## Usuario estándar

Es el rol utilizado por la mayoría de empleados.

Características:

- Utiliza aplicaciones.
- Accede a documentos.
- No modifica configuraciones críticas.

---

## Administrador local

Tiene control completo sobre un único equipo.

Puede:

- Crear usuarios locales.
- Instalar aplicaciones.
- Configurar dispositivos.
- Administrar servicios.

No puede administrar otros equipos del dominio salvo que disponga de permisos adicionales.

---

## Administrador del dominio

Gestiona toda la infraestructura de Active Directory.

Puede administrar:

- Usuarios.
- Equipos.
- Grupos.
- GPO.
- Controladores de dominio.

Es uno de los roles con mayor nivel de privilegios.

---

## Administrador de servidores

Gestiona uno o varios servidores concretos.

Sus funciones pueden incluir:

- Administración de servicios.
- Actualizaciones.
- Copias de seguridad.
- Monitorización.
- Gestión del almacenamiento.

---

## Administrador de bases de datos

Se encarga de administrar sistemas gestores de bases de datos.

Ejemplos:

- Microsoft SQL Server.
- Oracle.
- PostgreSQL.
- MySQL.

---

## Operador o técnico de soporte

Dispone de permisos limitados para realizar tareas de soporte.

Ejemplos:

- Restablecer contraseñas.
- Desbloquear cuentas.
- Unir equipos al dominio.
- Configurar impresoras.

Normalmente no dispone de privilegios administrativos completos.

---

# Principio de mínimo privilegio

Uno de los principios fundamentales de la seguridad informática consiste en conceder únicamente los privilegios necesarios para realizar una tarea.

Ejemplo correcto:

```text
Empleado RRHH

↓

Acceso únicamente a recursos de RRHH
```

Ejemplo incorrecto:

```text
Empleado RRHH

↓

Administrador del dominio
```

Aplicar este principio reduce considerablemente el impacto de errores humanos y ataques informáticos.

---

# Separación de funciones

La separación de funciones consiste en dividir las responsabilidades administrativas entre diferentes personas o equipos.

Ejemplo:

```text
Administrador de red

↓

Configura infraestructura


Administrador de bases de datos

↓

Gestiona SQL Server


Administrador de sistemas

↓

Gestiona servidores
```

Esto evita que una única cuenta tenga control absoluto sobre toda la infraestructura.

---

# Elevación de privilegios

En determinadas ocasiones un usuario necesita realizar una acción administrativa de forma puntual.

En lugar de trabajar siempre con privilegios elevados, los sistemas permiten elevar temporalmente los permisos.

Ejemplos:

Windows:

```text
Ejecutar como administrador
```

Linux:

```bash
sudo
```

Este mecanismo reduce el uso continuo de cuentas privilegiadas.

---

# Riesgos de los privilegios elevados

Las cuentas con privilegios administrativos son uno de los principales objetivos de los atacantes.

Si una de estas cuentas se ve comprometida, el impacto puede ser muy elevado.

Riesgos habituales:

- Instalación de malware.
- Robo de información.
- Modificación de configuraciones.
- Creación de nuevos usuarios.
- Escalada de privilegios.

Ejemplo:

```text
Cuenta administrativa comprometida

↓

Control completo del sistema
```

---

# Gestión de cuentas privilegiadas

Las organizaciones suelen aplicar medidas específicas para proteger estas cuentas.

Algunas de ellas son:

- Contraseñas robustas.
- Autenticación multifactor (MFA).
- Auditoría de accesos.
- Uso exclusivo para tareas administrativas.
- Revisión periódica de privilegios.
- Deshabilitación de cuentas que ya no sean necesarias.

---

# Delegación de privilegios

No siempre es necesario convertir a un usuario en administrador.

En muchos casos es preferible delegar únicamente una tarea concreta.

Ejemplos:

- Restablecer contraseñas.
- Crear usuarios.
- Gestionar una Unidad Organizativa.
- Administrar impresoras.

La delegación permite distribuir responsabilidades sin conceder privilegios excesivos.

---

# Ejemplo práctico

Una empresa cuenta con los siguientes roles:

```text
Empleado

↓

Usuario estándar


Técnico IT

↓

Administrador local


Administrador de sistemas

↓

Administrador de servidores


Administrador AD

↓

Administrador del dominio
```

Cada rol dispone únicamente de los privilegios necesarios para desempeñar sus funciones.

---

[⬆️ Volver al índice](#índice)

## Cuentas de servicio

### Introducción

Además de las cuentas utilizadas por personas, los sistemas operativos y las aplicaciones necesitan identidades propias para ejecutar procesos de forma automática.

Estas identidades reciben el nombre de **cuentas de servicio** (*Service Accounts*).

Su función es permitir que aplicaciones, servicios y tareas programadas puedan autenticarse y acceder a los recursos necesarios sin depender de la cuenta personal de un usuario.

Ejemplos habituales:

- Servicios de bases de datos.
- Servidores web.
- Aplicaciones empresariales.
- Sistemas de copias de seguridad.
- Tareas programadas.
- Agentes de monitorización.

---

# ¿Qué es una cuenta de servicio?

Una cuenta de servicio es una cuenta diseñada para ser utilizada por una aplicación, un servicio o un proceso automático.

A diferencia de una cuenta de usuario, normalmente:

- No pertenece a una persona.
- No se utiliza para iniciar sesión de forma interactiva.
- Tiene permisos limitados a la función que desempeña.

Ejemplo:

```text
Servicio SQL Server

↓

Cuenta:

svc_sql

↓

Acceso a la base de datos
```

---

# ¿Por qué utilizar cuentas de servicio?

Asignar una cuenta específica a un servicio aporta varias ventajas:

- Permite controlar sus permisos.
- Facilita la auditoría.
- Reduce riesgos de seguridad.
- Evita utilizar cuentas personales.
- Permite identificar qué servicio realiza una acción.

Ejemplo:

```text
Aplicación ERP

↓

Cuenta propia

↓

Acceso únicamente a los recursos necesarios
```

---

# Tipos de cuentas de servicio en Windows

Windows dispone de varios tipos de cuentas para ejecutar servicios.

---

## Local System

Es una cuenta integrada con privilegios muy elevados sobre el equipo local.

Características:

- Control total sobre el sistema.
- Acceso completo a recursos locales.
- No debe utilizarse salvo cuando sea estrictamente necesario.

Ejemplo:

```text
Cuenta:

Local System

↓

Control total del equipo
```

---

## Local Service

Cuenta integrada con privilegios limitados.

Características:

- Acceso reducido al sistema.
- Se utiliza para servicios que no requieren permisos elevados.
- Mejora la seguridad frente a Local System.

---

## Network Service

Cuenta integrada utilizada por servicios que necesitan acceder a recursos de red.

Características:

- Permisos limitados en el equipo local.
- Puede autenticarse frente a otros equipos utilizando la identidad del equipo.

---

## Cuenta de usuario específica

Es una cuenta creada exclusivamente para ejecutar un servicio.

Ejemplo:

```text
svc_backup

↓

Servicio de copias

↓

Acceso NAS
```

Este es el método más habitual en entornos empresariales.

---

# Managed Service Accounts (MSA)

Microsoft introdujo las **Managed Service Accounts (MSA)** para facilitar la gestión de servicios.

Ventajas:

- Cambio automático de contraseña.
- Gestión centralizada.
- Mayor seguridad.
- Reduce errores administrativos.

Ejemplo:

```text
Servicio IIS

↓

MSA

↓

Contraseña administrada automáticamente
```

---

# Group Managed Service Accounts (gMSA)

Las **Group Managed Service Accounts (gMSA)** amplían el concepto anterior.

Permiten que una misma cuenta pueda ser utilizada por varios servidores.

Se utilizan habitualmente en:

- Balanceadores.
- Granjas IIS.
- Servicios distribuidos.
- Clústeres.

Ejemplo:

```text
Servidor WEB01

↓

gMSA

↓

Servidor WEB02
```

La contraseña continúa siendo administrada automáticamente por Active Directory.

---

# Cuentas de servicio en Linux

Linux también utiliza cuentas específicas para ejecutar servicios.

Ejemplos:

```text
www-data

↓

Servidor Apache
```

```text
mysql

↓

Base de datos MySQL
```

```text
postgres

↓

PostgreSQL
```

Estas cuentas suelen:

- No disponer de shell interactiva.
- Tener UID propios.
- Ejecutar únicamente su servicio.

---

# Permisos de una cuenta de servicio

Una cuenta de servicio debe disponer únicamente de los permisos necesarios para realizar su función.

Ejemplo:

```text
Servicio de copias

↓

Lectura servidores

↓

Escritura NAS

↓

Sin permisos administrativos
```

Conceder privilegios innecesarios aumenta el riesgo de seguridad.

---

# Riesgos de las cuentas de servicio

Las cuentas de servicio son un objetivo frecuente para los atacantes.

Algunos riesgos habituales son:

- Contraseñas que nunca cambian.
- Permisos excesivos.
- Uso compartido entre varias aplicaciones.
- Falta de supervisión.
- Credenciales almacenadas en texto plano.

Ejemplo:

```text
Cuenta svc_sql

↓

Administrador del dominio

↓

Aplicación comprometida

↓

Compromiso de toda la infraestructura
```

---

# Buenas prácticas

Se recomienda seguir estas medidas:

- Crear una cuenta distinta para cada servicio.
- Aplicar el principio de mínimo privilegio.
- Utilizar gMSA o MSA cuando sea posible.
- Cambiar periódicamente las contraseñas.
- No utilizar cuentas personales.
- Auditar el uso de las cuentas.
- Deshabilitar las cuentas que ya no sean necesarias.

---

# Auditoría de cuentas de servicio

Las organizaciones deben revisar periódicamente:

- Servicios asociados.
- Último inicio de sesión.
- Permisos asignados.
- Contraseñas.
- Recursos utilizados.

Esto permite detectar:

- Cuentas abandonadas.
- Permisos innecesarios.
- Configuraciones inseguras.

---

# Ejemplo práctico

Una empresa dispone de un servidor de copias de seguridad.

Configuración:

```text
Cuenta:

svc_backup

↓

Servicio Veeam

↓

Acceso:

Lectura servidores

↓

Escritura NAS

↓

Sin permisos administrativos
```

Gracias a esta configuración, aunque el servicio se vea comprometido, el atacante no obtiene privilegios elevados sobre el dominio.

---

[⬆️ Volver al índice](#índice)

## Buenas prácticas en la gestión de usuarios y permisos

### Introducción

La gestión de usuarios y permisos constituye uno de los pilares fundamentales de la seguridad informática.

Una mala administración de las identidades puede provocar accesos no autorizados, pérdida de información o comprometer toda una infraestructura.

Aplicar buenas prácticas permite reducir riesgos, facilitar la administración y cumplir con normativas y estándares de seguridad.

---

# Aplicar el principio de mínimo privilegio

El **principio de mínimo privilegio (Principle of Least Privilege, PoLP)** establece que un usuario únicamente debe disponer de los permisos estrictamente necesarios para realizar su trabajo.

Esto reduce la superficie de ataque y limita el impacto de posibles errores o compromisos.

Ejemplo correcto:

```text
Empleado de ventas

↓

Acceso a carpeta Ventas

↓

Sin acceso a Recursos Humanos
```

Ejemplo incorrecto:

```text
Empleado de ventas

↓

Administrador del dominio
```

---

# Utilizar grupos en lugar de permisos individuales

Siempre que sea posible, los permisos deben asignarse a **grupos** y no directamente a usuarios.

Ventajas:

- Administración más sencilla.
- Menor riesgo de errores.
- Facilita altas y bajas de empleados.
- Permite mantener una estructura organizada.

Ejemplo:

```text
Grupo:

GG_Ventas

↓

Permiso carpeta Ventas

↓

Usuarios añadidos al grupo
```

---

# Evitar utilizar cuentas administrativas para el trabajo diario

Las cuentas con privilegios elevados deben utilizarse únicamente para tareas administrativas.

Para el trabajo habitual es recomendable utilizar una cuenta estándar.

Ejemplo:

```text
Cuenta personal

↓

Correo electrónico

Documentos

Aplicaciones


Cuenta administrativa

↓

Configuración del sistema

↓

Instalación de software

↓

Administración de usuarios
```

---

# Proteger las cuentas privilegiadas

Las cuentas con permisos elevados deben contar con medidas de protección adicionales.

Se recomienda:

- Contraseñas robustas.
- Autenticación multifactor (MFA).
- Auditoría de accesos.
- Uso exclusivo para tareas administrativas.
- Supervisión continua.

Estas cuentas son uno de los principales objetivos de los atacantes.

---

# Revisar periódicamente usuarios y grupos

Con el paso del tiempo pueden quedar:

- Cuentas sin uso.
- Usuarios duplicados.
- Permisos innecesarios.
- Grupos obsoletos.

Es recomendable realizar revisiones periódicas para mantener una estructura limpia y segura.

Ejemplo:

```text
Auditoría trimestral

↓

Usuarios inactivos

↓

Revisión

↓

Deshabilitación o eliminación
```

---

# Deshabilitar antes de eliminar

Cuando un usuario deja la organización, normalmente es preferible **deshabilitar la cuenta** antes de eliminarla.

Ventajas:

- Conserva el historial.
- Facilita auditorías.
- Permite recuperar información si es necesario.
- Evita eliminaciones accidentales.

Ejemplo:

```text
Empleado abandona empresa

↓

Cuenta deshabilitada

↓

Periodo de revisión

↓

Eliminación definitiva
```

---

# Evitar cuentas compartidas

Cada usuario debe disponer de su propia cuenta.

Las cuentas compartidas dificultan:

- La auditoría.
- La trazabilidad.
- La identificación de responsables.

Ejemplo incorrecto:

```text
Usuario:

almacen

↓

Utilizado por cinco personas
```

Ejemplo correcto:

```text
Usuario:

juan

Usuario:

ana

Usuario:

pedro
```

---

# Utilizar contraseñas seguras

Las contraseñas deben cumplir una política de seguridad adecuada.

Recomendaciones:

- Longitud mínima de 12 caracteres.
- Combinar mayúsculas, minúsculas, números y símbolos.
- No reutilizar contraseñas.
- Evitar información personal.

Ejemplo:

```text
Incorrecto:

Empresa123


Correcto:

7M!v9@R2#LpQ
```

---

# Implementar autenticación multifactor (MFA)

Siempre que sea posible, debe utilizarse un segundo factor de autenticación.

Ejemplo:

```text
Contraseña

+

Aplicación Authenticator

↓

Acceso concedido
```

Esto reduce considerablemente el riesgo derivado del robo de credenciales.

---

# Controlar las cuentas de servicio

Las cuentas de servicio deben:

- Tener únicamente los permisos necesarios.
- Utilizar contraseñas robustas o cuentas administradas (MSA/gMSA).
- Revisarse periódicamente.
- Documentarse correctamente.

Nunca deben utilizarse cuentas personales para ejecutar servicios.

---

# Documentar los cambios

Las modificaciones relacionadas con usuarios y permisos deberían quedar registradas.

Ejemplos:

- Creación de usuarios.
- Eliminación de cuentas.
- Cambios de grupo.
- Asignación de permisos.
- Elevación de privilegios.

Esto facilita las auditorías y la resolución de incidencias.

---

# Aplicar el ciclo de vida de las cuentas

Toda cuenta debería seguir un proceso claramente definido.

Ejemplo:

```text
Alta

↓

Asignación de permisos

↓

Modificaciones

↓

Deshabilitación

↓

Eliminación
```

Esto evita cuentas huérfanas y accesos innecesarios.

---

# Auditar accesos

Es recomendable revisar periódicamente:

- Inicios de sesión.
- Cambios de contraseña.
- Modificaciones de permisos.
- Creación de usuarios.
- Uso de cuentas privilegiadas.

La auditoría permite detectar comportamientos anómalos y responder con mayor rapidez ante incidentes.

---

# Formar a los usuarios

La seguridad no depende únicamente de la tecnología.

Los usuarios deben conocer aspectos básicos como:

- Protección de contraseñas.
- Riesgos del phishing.
- Uso adecuado de las cuentas corporativas.
- Importancia de bloquear el equipo al ausentarse.
- No compartir credenciales.

Una buena formación reduce significativamente el riesgo de incidentes.

---

# Ejemplo práctico

Una empresa incorpora un nuevo empleado.

Proceso recomendado:

```text
Crear cuenta

↓

Añadir al grupo correspondiente

↓

Aplicar MFA

↓

Asignar permisos mínimos

↓

Registrar la creación

↓

Revisión periódica de la cuenta
```

Cuando el empleado abandona la empresa:

```text
Deshabilitar cuenta

↓

Revocar accesos

↓

Revisar recursos asignados

↓

Eliminar cuenta tras el periodo establecido
```

---

[⬆️ Volver al índice](#índice)

## Casos prácticos

### Introducción

A continuación se presentan varios escenarios habituales relacionados con la gestión de usuarios y permisos en entornos empresariales.

---

# Caso práctico 1: Alta de un nuevo empleado

### Situación

Una empresa incorpora a un nuevo trabajador al departamento de Ventas.

Debe disponer de acceso a:

- Su equipo.
- Correo corporativo.
- Carpeta compartida de Ventas.
- Impresoras del departamento.

---

### Procedimiento

```text
Crear cuenta de usuario

↓

Asignar contraseña temporal

↓

Obligar cambio de contraseña

↓

Añadir al grupo GG_Ventas

↓

Asignar licencia de correo

↓

Verificar acceso

↓

Documentar la creación
```

---

### Resultado

El usuario dispone únicamente de los permisos necesarios para realizar su trabajo.

---

# Caso práctico 2: Cambio de departamento

### Situación

Un empleado pasa del departamento de Ventas al departamento de Administración.

---

### Procedimiento

```text
Eliminar usuario del grupo GG_Ventas

↓

Añadir al grupo GG_Administracion

↓

Actualizar permisos

↓

Comprobar acceso

↓

Documentar cambios
```

---

### Resultado

El empleado pierde el acceso a los recursos antiguos y obtiene únicamente los necesarios para su nuevo puesto.

---

# Caso práctico 3: Baja de un empleado

### Situación

Un trabajador abandona la empresa.

---

### Procedimiento

```text
Deshabilitar cuenta

↓

Cerrar sesiones activas

↓

Revocar VPN

↓

Revocar MFA

↓

Deshabilitar correo

↓

Revisar recursos asignados

↓

Eliminar cuenta tras el periodo establecido
```

---

### Resultado

La cuenta deja de poder utilizarse sin perder inicialmente la información necesaria para posibles auditorías o recuperaciones.

---

# Caso práctico 4: Acceso denegado a una carpeta

### Situación

Un usuario informa de que no puede acceder a una carpeta compartida.

---

### Comprobaciones

```text
Verificar identidad

↓

Comprobar grupo

↓

Revisar permisos NTFS

↓

Comprobar permisos compartidos

↓

Verificar herencia

↓

Comprobar ACL
```

---

### Posibles causas

- Usuario fuera del grupo correcto.
- Permiso eliminado.
- ACL incorrecta.
- Herencia deshabilitada.
- Permiso de denegación.

---

# Caso práctico 5: Servicio que deja de funcionar

### Situación

El servicio de copias de seguridad deja de iniciarse.

---

### Comprobaciones

```text
Revisar cuenta de servicio

↓

Verificar contraseña

↓

Comprobar permisos

↓

Consultar visor de eventos

↓

Probar inicio manual
```

---

### Posibles causas

- Contraseña caducada.
- Cuenta deshabilitada.
- Permisos insuficientes.
- Servicio mal configurado.

---

# Caso práctico 6: Usuario con demasiados permisos

### Situación

Durante una auditoría se detecta que un empleado pertenece al grupo **Administradores del dominio**.

---

### Procedimiento

```text
Verificar necesidad real

↓

Eliminar privilegios innecesarios

↓

Asignar grupo adecuado

↓

Documentar modificación

↓

Auditar accesos recientes
```

---

### Resultado

Se aplica nuevamente el principio de mínimo privilegio.

---

# Caso práctico 7: Carpeta compartida para un nuevo departamento

### Situación

Se crea el departamento de Marketing.

---

### Procedimiento recomendado

```text
Crear grupo GG_Marketing

↓

Crear carpeta compartida

↓

Asignar permisos al grupo

↓

Añadir usuarios

↓

Probar acceso
```

---

### Configuración recomendada

```text
Grupo

↓

Permisos

↓

Usuarios
```

En lugar de:

```text
Usuario

↓

Permisos individuales
```

---

# Caso práctico 8: Auditoría de cuentas inactivas

### Situación

La empresa realiza una revisión anual de usuarios.

---

### Procedimiento

```text
Obtener listado usuarios

↓

Revisar último inicio de sesión

↓

Detectar cuentas inactivas

↓

Contactar con responsables

↓

Deshabilitar cuentas

↓

Eliminar cuando corresponda
```

---

### Beneficios

- Reduce superficie de ataque.
- Elimina cuentas olvidadas.
- Mejora la seguridad.
- Facilita auditorías.

---

[⬆️ Volver al índice](#índice)

## Buenas prácticas de seguridad

### Introducción

La gestión de usuarios y permisos constituye uno de los pilares fundamentales de la seguridad informática.

Una configuración incorrecta puede provocar accesos no autorizados, pérdida de información o comprometer completamente una infraestructura.

Aplicar buenas prácticas permite reducir riesgos, facilitar la administración y proteger los recursos de la organización frente a amenazas internas y externas.

---

# Aplicar el principio de mínimo privilegio

Todo usuario debe disponer únicamente de los permisos necesarios para realizar su trabajo.

Nunca deben concederse privilegios "por si acaso".

Ejemplo correcto:

```text
Empleado de Ventas

↓

Acceso únicamente a:

- Carpeta Ventas
- ERP Comercial
```

Ejemplo incorrecto:

```text
Empleado de Ventas

↓

Administrador del dominio
```

---

# Utilizar grupos para asignar permisos

Siempre que sea posible, los permisos deben asignarse a grupos y no directamente a usuarios.

Ventajas:

- Administración más sencilla.
- Menor número de errores.
- Facilita altas y bajas.
- Permite mantener una estructura organizada.

Ejemplo:

```text
Grupo:

GG_Finanzas

↓

Permisos carpeta Finanzas

↓

Usuarios añadidos al grupo
```

---

# Proteger las cuentas administrativas

Las cuentas con privilegios elevados son uno de los principales objetivos de los atacantes.

Se recomienda:

- Utilizar contraseñas robustas.
- Habilitar MFA.
- No utilizarlas para tareas cotidianas.
- Supervisar su uso.
- Auditar los inicios de sesión.

---

# Evitar utilizar cuentas personales para servicios

Los servicios deben ejecutarse mediante cuentas específicas.

Incorrecto:

```text
Servicio SQL

↓

Cuenta:

juan.perez
```

Correcto:

```text
Servicio SQL

↓

Cuenta:

svc_sql
```

Esto facilita la auditoría y evita problemas cuando un empleado abandona la empresa.

---

# Revisar periódicamente usuarios y permisos

Con el tiempo pueden aparecer:

- Usuarios inactivos.
- Grupos sin utilizar.
- Permisos innecesarios.
- Cuentas duplicadas.

Es recomendable realizar revisiones periódicas.

Ejemplo:

```text
Revisión trimestral

↓

Usuarios

↓

Grupos

↓

Permisos

↓

Corrección
```

---

# Deshabilitar antes de eliminar

Cuando un empleado abandona la organización, normalmente es recomendable:

```text
Deshabilitar cuenta

↓

Revisar recursos

↓

Conservar información

↓

Eliminar definitivamente
```

Esto permite recuperar información si fuera necesario.

---

# Utilizar contraseñas seguras

Las políticas de contraseñas deberían exigir:

- Longitud mínima de 12 caracteres.
- Complejidad.
- Historial de contraseñas.
- Caducidad cuando proceda.
- Bloqueo tras varios intentos fallidos.

Ejemplo:

```text
Incorrecto:

Empresa123


Correcto:

4V!n$8#LmP2@
```

---

# Implementar autenticación multifactor (MFA)

Siempre que sea posible debe utilizarse un segundo factor de autenticación.

Ejemplo:

```text
Contraseña

+

Código Microsoft Authenticator

↓

Acceso permitido
```

El MFA reduce considerablemente el riesgo derivado del robo de credenciales.

---

# Documentar todos los cambios

Las modificaciones importantes deben quedar registradas.

Ejemplos:

- Creación de usuarios.
- Eliminación de cuentas.
- Cambios de permisos.
- Incorporación a grupos.
- Elevación de privilegios.

Esto facilita las auditorías y la resolución de incidencias.

---

# Auditar regularmente

Es recomendable revisar periódicamente:

- Inicios de sesión.
- Cambios de contraseña.
- Uso de cuentas privilegiadas.
- Modificaciones de grupos.
- Cambios en permisos.

La auditoría ayuda a detectar comportamientos anómalos y posibles incidentes de seguridad.

---

# Evitar cuentas compartidas

Cada usuario debe disponer de una cuenta individual.

Incorrecto:

```text
Usuario:

almacen
```

Utilizado por varias personas.

Correcto:

```text
juan.garcia

ana.lopez

pedro.sanchez
```

De esta forma todas las acciones quedan correctamente registradas.

---

# Eliminar privilegios innecesarios

Con el paso del tiempo algunos usuarios acumulan permisos que ya no necesitan.

Es recomendable revisar periódicamente:

- Grupos administrativos.
- Permisos especiales.
- Accesos temporales.
- Delegaciones.

El objetivo es mantener únicamente los permisos realmente necesarios.

---

# Formar a los usuarios

La seguridad también depende del comportamiento de las personas.

Los usuarios deberían conocer aspectos como:

- No compartir contraseñas.
- Detectar correos de phishing.
- Bloquear el equipo al ausentarse.
- Utilizar MFA.
- Informar de cualquier actividad sospechosa.

Una formación adecuada reduce significativamente los incidentes de seguridad.

---

# Ejemplo práctico

Una empresa incorpora un nuevo trabajador.

Procedimiento recomendado:

```text
Crear usuario

↓

Asignar contraseña temporal

↓

Obligar cambio de contraseña

↓

Añadir al grupo correspondiente

↓

Aplicar MFA

↓

Asignar permisos mínimos

↓

Registrar la operación
```

Cuando el empleado abandona la empresa:

```text
Deshabilitar cuenta

↓

Revocar accesos

↓

Revisar recursos asignados

↓

Eliminar cuenta tras el periodo establecido
```

---

[⬆️ Volver al índice](#índice)