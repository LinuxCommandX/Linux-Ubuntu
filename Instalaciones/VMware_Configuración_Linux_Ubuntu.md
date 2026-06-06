# Guía Completa: Instalación de VMware y Configuración de Linux Ubuntu

Esta guía te guiará paso a paso para instalar el hipervisor VMware y posteriormente configurar una máquina virtual con el sistema operativo Linux Ubuntu.

---

## Parte 1: Instalación de VMware Workstation Player

VMware Workstation Player es una herramienta excelente para virtualizar sistemas operativos de forma gratuita para uso personal.

### Enlaces de Acceso Rápido
* [Descargar VMware Workstation Player](https://www.vmware.com/products/workstation-player.html)

### Paso a Paso
1. **Descargar el instalador:** Ve al enlace oficial de VMware y descarga la versión más reciente para tu sistema operativo principal (normalmente Windows o Linux).
2. **Ejecutar el archivo:** Abre el instalador descargado (`.exe` en Windows) con permisos de administrador.
3. **Asistente de instalación:** * Haz clic en *Next* (Siguiente) y acepta los términos de la licencia.
   * En la sección de configuración de características avanzadas, se recomienda marcar la opción **"Enhanced Keyboard Driver"** (Controlador de teclado mejorado) para una mejor experiencia.
4. **Configuración de actualizaciones:** Elige si deseas buscar actualizaciones automáticamente al iniciar y si quieres unirte al programa de mejora de la experiencia del usuario (puedes desmarcarlas si prefieres).
5. **Accesos directos:** Selecciona si deseas accesos directos en el Escritorio y en el Menú Inicio.
6. **Finalizar:** Haz clic en *Install*. Una vez terminado el proceso, presiona *Finish*. Si el instalador te solicita reiniciar la computadora, hazlo para asegurar que todos los controladores se carguen correctamente.

---

## Parte 2: Preparación de Ubuntu

Antes de abrir VMware, necesitamos el archivo que contiene el sistema operativo Ubuntu.

### Enlaces de Acceso Rápido
* [Descargar ISO de Ubuntu Desktop](https://ubuntu.com/download/desktop)

### Paso a Paso
1. Ingresa al enlace de descarga de Ubuntu.
2. Descarga la versión **LTS** más reciente (por ejemplo, Ubuntu 24.04 LTS o 26.04 LTS). Las versiones LTS (Long Term Support) garantizan estabilidad y soporte por varios años.
3. El archivo que se descargará tendrá una extensión `.iso`. **No lo extraigas ni lo abras**, guárdalo en una carpeta localizada (como *Descargas* o *Documentos*).

---

## Parte 3: Creación de la Máquina Virtual en VMware

Ahora uniremos ambas herramientas para instalar Ubuntu dentro de VMware.

### Paso a Paso

1. **Crear nueva máquina:** Abre VMware Workstation Player y haz clic en la opción **"Create a New Virtual Machine"** (Crear una nueva máquina virtual).
2. **Seleccionar la ISO:** * Selecciona la opción *Installer disc image file (iso)*.
   * Haz clic en *Browse* (Examinar) y busca el archivo `.iso` de Ubuntu que descargaste en la Parte 2.
   * VMware detectará automáticamente que se trata de Ubuntu y activará la "Instalación fácil" (Easy Install). Haz clic en *Next*.
3. **Información de personalización (Easy Install):**
   * **Full name:** Tu nombre completo.
   * **User name:** Tu nombre de usuario (en minúsculas, sin espacios ni caracteres especiales).
   * **Password:** Elige una contraseña segura y confírmala (la necesitarás siempre para iniciar sesión y usar comandos de administrador). Haz clic en *Next*.
4. **Nombre y Ubicación:**
   * **Virtual machine name:** Puedes dejarlo como "Ubuntu" o renombrarlo.
   * **Location:** La ruta donde se guardarán los archivos de la máquina virtual (se recomienda dejar la por defecto o elegir un disco con suficiente espacio). Haz clic en *Next*.
5. **Especificar capacidad de disco:**
   * **Maximum disk size:** Se recomiendan mínimo **25 GB** o **30 GB** para trabajar cómodamente.
   * Selecciona la opción **"Split virtual disk into multiple files"** (Dividir el disco virtual en múltiples archivos), ya que hace que sea más fácil mover la máquina virtual a otra computadora si fuera necesario. Haz clic en *Next*.
6. **Personalizar Hardware (Opcional pero Recomendado):**
   * Haz clic en el botón **"Customize Hardware..."**.
   * **Memory (RAM):** Si tu computadora tiene 8 GB de RAM, asígnale 2 GB (2048 MB) o 4 GB (4096 MB) a la máquina virtual si tienes 16 GB o más en total.
   * **Processors:** Asígnale **2 núcleos** (cores) para que el sistema emulado funcione con fluidez.
   * Haz clic en *Close* (Cerrar) y luego en *Finish* (Finalizar).

---

## Parte 4: Instalación Automática y Configuración Final

1. **Encendido:** La máquina virtual se encenderá automáticamente. Verás una pantalla negra con comandos de carga de Ubuntu.
2. **Proceso de instalación:** Gracias al asistente *Easy Install* de VMware, el sistema configurará las particiones, el idioma y los componentes de fondo sin que tengas que intervenir. Esto puede tomar entre 10 y 20 minutos dependiendo de la velocidad de tu disco (es mucho más rápido en un SSD).
3. **Instalación de VMware Tools:** Durante o al finalizar la instalación, VMware instalará automáticamente las *"VMware Tools"*. Esto es crucial porque permite:
   * Cambiar la resolución de la pantalla de Ubuntu dinámicamente al redimensionar la ventana.
   * Copiar y pegar archivos o texto directamente entre tu sistema operativo principal (Anfitrión) y Ubuntu (Invitado).
4. **Inicio de sesión:** Una vez que el proceso termine por completo, aparecerá la pantalla de bloqueo de Ubuntu con el nombre de usuario que creaste. Haz clic en él, introduce tu contraseña y presiona `Enter`.

> ¡Listo! Ya tienes Linux Ubuntu corriendo de forma segura y aislada dentro de VMware.