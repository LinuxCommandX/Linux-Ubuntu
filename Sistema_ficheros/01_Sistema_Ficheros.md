# Sistema de ficheros de Linux (Ubuntu)

## Jerarquía del sistema de ficheros

En Linux, **todo es un fichero**. El sistema de ficheros comienza en la raíz identificada por `/`.

### Estructura estándar de directorios

| Directorio | Contenido |
|------------|-----------|
| `/` | Raíz del sistema |
| `/home` | Directorios personales de cada usuario |
| `/etc` | Archivos de configuración del sistema |
| `/var` | Datos variables (logs, correos, colas de impresión) |
| `/bin` | Comandos esenciales del sistema (binarios) |
| `/sbin` | Comandos de administración del sistema |
| `/usr` | Programas, librerías y documentación de usuario |
| `/tmp` | Archivos temporales (se borran al reiniciar) |
| `/boot` | Archivos necesarios para el arranque |
| `/dev` | Dispositivos del sistema (discos, USBs, etc.) |
| `/proc` | Información de procesos y del kernel (virtual) |

### Comandos para visualizar la estructura

```bash
# Listar contenido de la raíz
ls /

# Ver estructura jerárquica (instalar tree primero)
sudo apt install tree
tree /
tree -L 2 /   # Limitar a 2 niveles de profundidad
```

### Características principales
- Case sensitive: `Archivo.txt` ≠ `archivo.txt`

- Extensiones opcionales: A diferencia de Windows, Linux no depende de extensiones para identificar tipos de archivo

- Todo es un fichero: Incluye discos, directorios, procesos, sockets y tuberías

### Características principales
Los dispositivos (USB, discos duros adicionales) se montan en directorios vacíos:

```bash
# Montar un USB en /mnt/usb
sudo mount /dev/sdb1 /mnt/usb

# Ver dispositivos montados
df -h
lsblk
```

---
