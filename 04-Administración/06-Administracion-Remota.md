# Administración remota 

## Introducción

La administración remota permite gestionar equipos, servidores y dispositivos sin necesidad de acceder físicamente a ellos.

## Índice

- [Concepto de administración remota](#concepto-de-administracion-remota)
- [Ventajas e inconvenientes](#ventajas-e-inconvenientes)
- [Protocolos de administración remota](#protocolos-de-administracion-remota)
- [Escritorio remoto en Windows (RDP)](#escritorio-remoto-en-windows-rdp)
- [PowerShell Remoting (WinRM)](#powershell-remoting-winrm)
- [SSH en Linux](#ssh-en-linux)
- [Transferencia remota de archivos (SCP y SFTP)](#transferencia-remota-de-archivos-scp-y-sftp)
- [Herramientas de administración remota](#herramientas-de-administracion-remota)
- [Administración remota en entornos empresariales](#administracion-remota-en-entornos-empresariales)
- [Seguridad en la administración remota](#seguridad-en-la-administracion-remota)
- [Resolución de problemas habituales](#resolucion-de-problemas-habituales)

---

## Concepto de administración remota

*La administración remota consiste en gestionar un equipo, servidor o dispositivo desde otra ubicación utilizando una red de comunicaciones.*

**Conceptos clave:**

- **¿Qué es la administración remota?:** La administración remota permite controlar un sistema informático desde otro dispositivo conectado a través de una red.
- **Funcionamiento básico:** El proceso de administración remota puede representarse de la siguiente forma.
- **Requisitos para la administración remota:** Para poder administrar un equipo de forma remota normalmente se necesita: Conectividad de red.
- **Tipos de administración remota:** Existen diferentes formas de administrar un sistema de manera remota.
- **Administración gráfica:** Permite visualizar el escritorio remoto del equipo y utilizarlo como si el administrador estuviera físicamente delante de él.
- **Administración mediante consola:** Consiste en administrar el sistema utilizando únicamente comandos.
- **Ámbitos de utilización:** La administración remota se utiliza en numerosos escenarios.
- **Ventajas generales:** Entre las principales ventajas destacan: Ahorro de tiempo.
- **Riesgos:** Como cualquier acceso remoto, también presenta algunos riesgos.

---

## Ventajas e inconvenientes

*La administración remota ofrece numerosas ventajas para la gestión de infraestructuras informáticas, permitiendo administrar equipos y servidores desde cualquier ubicación.*

**Conceptos clave:**

- **Ventajas de la administración remota:** La administración remota aporta múltiples beneficios tanto para pequeñas empresas como para grandes organizaciones.
- **Ahorro de tiempo:** Al no ser necesario desplazarse físicamente hasta el equipo, muchas incidencias pueden resolverse en pocos minutos.
- **Reducción de costes:** La administración remota disminuye los costes asociados a: Desplazamientos.
- **Mayor productividad:** Los administradores pueden gestionar varios equipos consecutivamente sin cambiar de ubicación.
- **Administración de infraestructuras distribuidas:** Muchas empresas disponen de: Varias sedes.
- **Disponibilidad del servicio:** Los problemas pueden solucionarse en cualquier momento sin esperar a que un técnico llegue físicamente al equipo.
- **Inconvenientes:** A pesar de sus ventajas, también existen algunas limitaciones.
- **Dependencia de la red:** La administración remota requiere que exista conectividad entre el administrador y el equipo remoto.
- **Riesgos de seguridad:** Los accesos remotos pueden convertirse en un objetivo para los atacantes.
- **Rendimiento:** En conexiones lentas o con alta latencia pueden aparecer problemas como: Lentitud en el escritorio remoto.

### Comparativa

| Ventajas | Inconvenientes |
|----------|----------------|
| Acceso desde cualquier lugar. | Dependencia de la red. |
| Menor tiempo de respuesta. | Riesgos de seguridad. |
| Reducción de costes. | Posibles problemas de rendimiento. |
| Administración centralizada. | Configuración inicial más compleja. |
| Mayor productividad. | Necesidad de proteger los accesos remotos. |

---

## Protocolos de administración remota

*La administración remota se basa en protocolos de comunicación que permiten establecer una conexión entre el equipo del administrador y el sistema remoto.*

**Conceptos clave:**

- **¿Qué es un protocolo de administración remota?:** Un protocolo de administración remota es un conjunto de normas que define cómo dos equipos intercambian información para permitir la gestión de un sistema a través de una red.
- **Principales protocolos:** Los protocolos más utilizados son: RDP (Remote Desktop Protocol).
- **RDP (Remote Desktop Protocol):** RDP es el protocolo desarrollado por Microsoft para acceder gráficamente a equipos Windows.
- **SSH (Secure Shell):** SSH permite administrar equipos mediante una consola de comandos cifrada.
- **WinRM (Windows Remote Management):** WinRM es el protocolo utilizado por Windows para la administración remota mediante PowerShell.
- **VNC (Virtual Network Computing):** VNC permite acceder al escritorio gráfico de un equipo independientemente del sistema operativo.

### SCP (Secure Copy Protocol)

*SCP se utiliza para copiar archivos entre equipos utilizando SSH.*

```bash
scp archivo.txt usuario@servidor:/home/usuario/
```

---

**Conceptos clave:**

- **SFTP (SSH File Transfer Protocol):** SFTP es un protocolo de transferencia de archivos basado en SSH.

### Comparativa de protocolos

| Protocolo | Tipo de acceso | Sistema habitual | Puerto |
|-----------|----------------|------------------|--------:|
| RDP | Escritorio gráfico | Windows | 3389 |
| SSH | Línea de comandos | Linux / Windows | 22 |
| WinRM | PowerShell remoto | Windows | 5985 / 5986 |
| VNC | Escritorio gráfico | Multiplataforma | Variable |
| SCP | Transferencia de archivos | Linux / Windows | 22 |
| SFTP | Transferencia de archivos | Linux / Windows | 22 |

---

**Conceptos clave:**

- **Criterios de elección:** La elección del protocolo dependerá de factores como: Sistema operativo.

---

## Escritorio remoto en Windows (RDP)

*El Escritorio remoto (*Remote Desktop Protocol* o RDP) es la tecnología desarrollada por Microsoft que permite acceder al escritorio de un equipo Windows desde otro dispositivo a través de una red.*

**Conceptos clave:**

- **¿Qué es RDP?:** RDP es un protocolo de comunicación que permite establecer una sesión gráfica remota entre dos equipos.
- **Funcionamiento:** El proceso de conexión puede representarse así.
- **Puerto utilizado:** Por defecto, RDP utiliza el siguiente puerto.
- **Requisitos para utilizar RDP:** Para utilizar Escritorio remoto es necesario: Que el equipo remoto tenga habilitado el acceso remoto.
- **Habilitar Escritorio remoto:** En Windows puede habilitarse desde.
- **Conectarse mediante RDP:** El cliente de Escritorio remoto puede abrirse ejecutando.
- **Funciones disponibles:** Durante una sesión RDP pueden realizarse tareas como: Administrar el sistema.
- **Ventajas:** Entre las principales ventajas de RDP destacan: Integración nativa con Windows.
- **Limitaciones:** RDP también presenta algunas limitaciones.

---

## PowerShell Remoting (WinRM)

*PowerShell Remoting es una característica de Windows que permite ejecutar comandos y scripts de PowerShell en equipos remotos sin necesidad de acceder a su escritorio.*

**Conceptos clave:**

- **¿Qué es PowerShell Remoting?:** PowerShell Remoting permite establecer sesiones remotas entre equipos Windows utilizando PowerShell.
- **¿Qué es WinRM?:** WinRM (*Windows Remote Management*) es el servicio que hace posible la comunicación remota entre equipos Windows.
- **Funcionamiento:** El proceso de administración puede representarse así.
- **Puertos utilizados:** WinRM utiliza por defecto los siguientes puertos.

### Habilitar PowerShell Remoting

*Para habilitar la administración remota se ejecuta.*

```powershell
Enable-PSRemoting
```

---

### Ejecutar un comando remoto

*Para ejecutar un único comando en un equipo remoto.*

```powershell
Invoke-Command -ComputerName SERVIDOR01 -ScriptBlock {
Get-Service
}
```

---

### Abrir una sesión remota

*También es posible establecer una sesión interactiva.*

```powershell
Enter-PSSession -ComputerName SERVIDOR01
```
```powershell
Exit-PSSession
```

---

### Administrar varios equipos

*PowerShell Remoting permite ejecutar un mismo comando en varios equipos simultáneamente.*

```powershell
Invoke-Command -ComputerName SERVIDOR01,SERVIDOR02 -ScriptBlock {
Get-Process
}
```

---

**Conceptos clave:**

- **Ventajas:** Entre las principales ventajas destacan: Administración desde línea de comandos.
- **Limitaciones:** PowerShell Remoting también presenta algunas limitaciones.

---

## SSH en Linux

*SSH (Secure Shell) es el protocolo de administración remota más utilizado en sistemas Linux y Unix.*

**Conceptos clave:**

- **¿Qué es SSH?:** SSH es un protocolo de comunicación que permite acceder de forma remota a un equipo mediante una conexión cifrada.
- **Funcionamiento:** El proceso de conexión puede representarse de la siguiente forma.
- **Puerto utilizado:** Por defecto, SSH utiliza el siguiente puerto.

### Servicio SSH

*En la mayoría de distribuciones Linux, el acceso remoto depende del servicio OpenSSH Server.*

```bash
systemctl status ssh
```
```bash
systemctl start ssh
```

---

### Conectarse a un servidor

*La conexión básica se realiza mediante.*

```bash
ssh usuario@servidor
```
```bash
ssh administrador@192.168.1.20
```

---

**Conceptos clave:**

- **Autenticación:** SSH permite diferentes métodos de autenticación.

### Ejecución remota de comandos

*SSH permite ejecutar un comando concreto sin iniciar una sesión interactiva.*

```bash
ssh usuario@servidor "uptime"
```

---

**Conceptos clave:**

- **Ventajas de SSH:** Entre las principales ventajas destacan: Comunicación cifrada.
- **Limitaciones:** SSH también presenta algunas limitaciones.

---

## Transferencia remota de archivos (SCP y SFTP)

*Además de administrar equipos de forma remota, los administradores necesitan transferir archivos entre sistemas de manera segura.*

**Conceptos clave:**

- **¿Qué es SCP?:** SCP (Secure Copy Protocol) es un protocolo utilizado para copiar archivos entre dos equipos mediante una conexión SSH.
- **Funcionamiento de SCP:** El proceso puede representarse de la siguiente forma.

### Copiar un archivo

*Para copiar un archivo desde el equipo local a un servidor remoto.*

```bash
scp archivo.txt usuario@servidor:/home/usuario/
```

---

### Copiar un directorio

*Para copiar un directorio completo se utiliza la opción.*

```bash
scp -r carpeta usuario@servidor:/home/usuario/
```

---

**Conceptos clave:**

- **¿Qué es SFTP?:** SFTP (SSH File Transfer Protocol) es un protocolo de transferencia de archivos que también utiliza SSH como mecanismo de comunicación.

### Conectarse mediante SFTP

*Para iniciar una sesión.*

```bash
sftp usuario@servidor
```

---

### Comandos habituales de SFTP

*Algunos comandos básicos son.*

| Comando | Función |
|----------|---------|
| `ls` | Mostrar archivos del servidor. |
| `pwd` | Mostrar el directorio actual. |
| `cd` | Cambiar de directorio remoto. |
| `put` | Subir un archivo al servidor. |
| `get` | Descargar un archivo del servidor. |
| `mkdir` | Crear un directorio remoto. |
| `rm` | Eliminar un archivo remoto. |

---

### Diferencias entre SCP y SFTP

| SCP | SFTP |
|-----|------|
| Copia archivos. | Gestiona archivos y directorios. |
| Más sencillo. | Más flexible. |
| No permite navegación interactiva. | Permite navegar por el sistema remoto. |
| Adecuado para copias rápidas. | Adecuado para administración de archivos. |

---

**Conceptos clave:**

- **Ventajas:** SCP y SFTP ofrecen numerosas ventajas.

---

## Herramientas de administración remota

*Además de los protocolos de administración remota, existen numerosas herramientas que facilitan el acceso y la gestión de equipos y servidores.*

**Conceptos clave:**

- **Tipos de herramientas:** Las herramientas de administración remota pueden clasificarse en varios grupos.
- **Escritorio remoto de Windows:** Es la solución integrada de Microsoft para acceder gráficamente a equipos Windows.
- **OpenSSH:** OpenSSH es la implementación más utilizada del protocolo SSH.
- **AnyDesk:** AnyDesk es una herramienta de acceso remoto multiplataforma.
- **TeamViewer:** TeamViewer permite controlar equipos remotos mediante una interfaz gráfica.
- **VNC:** VNC (Virtual Network Computing) es una tecnología que permite acceder al escritorio de un equipo independientemente del sistema operativo.
- **PsExec:** PsExec, incluido en la suite Sysinternals, permite ejecutar procesos y comandos de forma remota en equipos Windows.
- **Consolas web de administración:** Muchos dispositivos incorporan interfaces web para su administración.

### Comparativa

| Herramienta | Tipo de acceso | Sistemas compatibles |
|-------------|----------------|----------------------|
| Escritorio remoto | Gráfico | Windows |
| OpenSSH | Consola | Linux / Windows |
| AnyDesk | Gráfico | Multiplataforma |
| TeamViewer | Gráfico | Multiplataforma |
| VNC | Gráfico | Multiplataforma |
| PsExec | Línea de comandos | Windows |

---

**Conceptos clave:**

- **Criterios de elección:** Al seleccionar una herramienta conviene valorar: Sistema operativo.

---

## Administración remota en entornos empresariales

*En las empresas es habitual administrar de forma remota cientos o incluso miles de equipos distribuidos entre diferentes oficinas, centros de datos o servicios en la nube.*

**Conceptos clave:**

- **Administración centralizada:** En lugar de gestionar cada equipo de forma individual, las organizaciones suelen centralizar la administración desde uno o varios servidores.
- **Active Directory:** En entornos Windows, la administración remota suele apoyarse en Active Directory.
- **Administración de servidores:** Los servidores suelen administrarse de forma remota mediante herramientas como: Escritorio remoto (RDP).
- **Soporte remoto a usuarios:** Los departamentos de IT utilizan herramientas de acceso remoto para ayudar a los usuarios cuando surge un problema.
- **Administración de equipos en varias sedes:** Las empresas con múltiples oficinas pueden gestionar todos sus equipos mediante conexiones remotas.
- **Administración en la nube:** Cada vez es más habitual administrar recursos alojados en servicios cloud.
- **Automatización:** En grandes infraestructuras muchas tareas se automatizan mediante scripts y herramientas de administración.
- **Supervisión remota:** Además de administrar equipos, también es necesario supervisar su estado.
- **Ventajas en la empresa:** La administración remota proporciona numerosos beneficios.

---

## Seguridad en la administración remota

*La administración remota proporciona un acceso muy potente a equipos y servidores, pero también representa uno de los principales objetivos para los atacantes.*

**Conceptos clave:**

- **Importancia de la seguridad:** Los servicios de administración remota suelen ofrecer acceso con privilegios elevados.
- **Utilizar conexiones cifradas:** Siempre que sea posible deben utilizarse protocolos que cifren la comunicación.
- **Autenticación robusta:** La autenticación constituye la primera barrera de protección.
- **Limitar los usuarios autorizados:** No todos los usuarios deben poder administrar equipos remotamente.
- **Utilizar VPN:** Cuando la administración se realiza desde Internet, es recomendable establecer primero una conexión VPN.
- **Configurar el Firewall:** El cortafuegos debe limitar el acceso únicamente a los equipos autorizados.
- **Mantener el software actualizado:** Las herramientas de administración remota deben mantenerse siempre actualizadas.
- **Registrar las conexiones:** Todas las conexiones administrativas deberían quedar registradas.
- **Supervisar los accesos:** Es recomendable revisar periódicamente los registros para detectar: Intentos fallidos de autenticación.
- **Riesgos habituales:** Algunos de los riesgos más frecuentes son: Ataques por fuerza bruta.

---

## Resolución de problemas habituales

*Durante la administración remota pueden aparecer incidencias que impidan establecer la conexión o dificulten el acceso a los equipos.*

### Comprobar la conectividad

*El primer paso consiste en verificar que existe comunicación entre ambos equipos.*

```bash
ping servidor
```
```powershell
ping servidor
```

---

### Verificar el servicio remoto

*Es importante asegurarse de que el servicio correspondiente está iniciado.*

```bash
systemctl status ssh
```
```powershell
Get-Service WinRM
```

---

**Conceptos clave:**

- **Revisar el Firewall:** El cortafuegos puede bloquear los puertos utilizados por los servicios remotos.
- **Comprobar credenciales:** Muchos problemas de acceso están relacionados con errores de autenticación.

### Verificar la resolución de nombres

*Si la conexión se realiza mediante el nombre del equipo, es recomendable comprobar que la resolución DNS funciona correctamente.*

```bash
nslookup servidor
```
```powershell
nslookup servidor
```

---

### Revisar los registros

*Los registros del sistema suelen proporcionar información muy útil para localizar la causa de una incidencia.*

```bash
journalctl
```
```bash
tail -f /var/log/syslog
```

---

**Conceptos clave:**

- **Comprobar los permisos:** Es posible que el usuario tenga acceso al sistema pero no disponga de permisos para realizar determinadas acciones.

### Reiniciar el servicio

*Cuando un servicio remoto presenta un funcionamiento incorrecto, puede ser suficiente con reiniciarlo.*

```bash
systemctl restart ssh
```
```powershell
Restart-Service WinRM
```

---

**Conceptos clave:**

- **Procedimiento de diagnóstico:** Un método ordenado para localizar incidencias puede representarse así.

---

[⬆️ Volver al índice](#índice)
