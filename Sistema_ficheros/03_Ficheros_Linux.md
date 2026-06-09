# Ficheros en Linux

## Introducción

En Linux, **todo es un fichero**. Esto incluye no solo documentos y textos, sino también directorios, dispositivos, tuberías (pipes), sockets y enlaces. Comprender los tipos de ficheros es fundamental para administrar correctamente el sistema.

## Tipos de ficheros en Linux

### Identificación mediante `ls -l`

El primer carácter del listado `ls -l` indica el tipo de fichero:

| Símbolo | Tipo de fichero | Ejemplo | Descripción |
|---------|----------------|---------|-------------|
| `-` | Fichero regular | `texto.txt`, `script.sh`, `imagen.jpg` | Archivos normales: textos, binarios, imágenes, etc. |
| `d` | Directorio | `Documentos/`, `Descargas/` | Carpeta que contiene otros ficheros |
| `l` | Enlace simbólico | `link -> /ruta/original` | Acceso directo a otro fichero |
| `b` | Dispositivo de bloque | `/dev/sda` | Discos duros, USBs, particiones |
| `c` | Dispositivo de caracter | `/dev/tty`, `/dev/null` | Terminales, teclados, puertos serie |
| `p` | Tubería con nombre (FIFO) | `mi_pipe` | Comunicación entre procesos |
| `s` | Socket | `/var/run/docker.sock` | Comunicación entre procesos en red |

### Ejemplo práctico de `ls -l`

```bash
usuario@ubuntu:~$ ls -la /
total 209
drwxr-xr-x  20 root root  4096 jun  8 10:00 .
drwxr-xr-x  20 root root  4096 jun  8 10:00 ..
lrwxrwxrwx   1 root root     7 jun  1 00:00 bin -> usr/bin
drwxr-xr-x   4 root root  4096 jun  1 00:00 boot
drwxr-xr-x  19 root root  4080 jun  8 10:00 dev
drwxr-xr-x 133 root root 12288 jun  8 10:00 etc
drwxr-xr-x   3 root root  4096 jun  1 00:00 home
lrwxrwxrwx   1 root root     7 jun  1 00:00 lib -> usr/lib
drwx------   2 root root 16384 jun  1 00:00 lost+found
drwxr-xr-x   2 root root  4096 jun  1 00:00 media
drwxr-xr-x   2 root root  4096 jun  1 00:00 mnt
drwxr-xr-x   2 root root  4096 jun  1 00:00 opt
dr-xr-xr-x 275 root root     0 jun  8 10:00 proc
drwx------   5 root root  4096 jun  1 00:00 root
drwxr-xr-x  32 root root  1020 jun  8 10:00 run
lrwxrwxrwx   1 root root     8 jun  1 00:00 sbin -> usr/sbin
drwxr-xr-x   2 root root  4096 jun  1 00:00 srv
dr-xr-xr-x  13 root root     0 jun  8 10:00 sys
drwxrwxrwt  17 root root  4096 jun  8 10:00 tmp
drwxr-xr-x  12 root root  4096 jun  1 00:00 usr
drwxr-xr-x  12 root root  4096 jun  1 00:00 var
```

## Permisos en ficheros
### Estructura de permisos
```bash
-rwxr-xr--
│││││││││
││││││││└── Permiso de otros: lectura (r)
│││││││└── Permiso de otros: ejecución (x)
││││││└── Permiso de otros: escritura (w)
│││││└── Permiso de grupo: lectura (r)
││││└── Permiso de grupo: ejecución (x)
│││└── Permiso de grupo: escritura (w)
││└── Permiso de propietario: lectura (r)
│└── Permiso de propietario: ejecución (x)
└── Permiso de propietario: escritura (w)
```

### Tabla de permisos numéricos (modo octal)
| Número | Permiso | Significado |
|------------|-----------|-----------|
| 0 | `---` | Sin permisos |
| 1 | `--x` | Solo ejecución |
| 2 | `-w-` | Solo escritura |
| 3 | `-wx` | Escritura y ejecución |
| 4 | `r--` | Solo lectura |
| 5 | `r-x` | Lectura y ejecución |
| 6 | `rw-` | Lectura y escritura |
| 7 | `rwx` | Lectura, escritura y ejecución |

### Comandos para gestionar permisos
```bash
# Cambiar permisos con modo simbólico
chmod u+x script.sh        # Añade ejecución para propietario
chmod g-w documento.txt    # Quita escritura al grupo
chmod o+r informe.pdf      # Añade lectura para otros
chmod a+x programa         # Añade ejecución para todos

# Cambiar permisos con modo octal
chmod 755 script.sh        # rwxr-xr-x
chmod 644 documento.txt    # rw-r--r--
chmod 600 secreto.txt      # rw-------
chmod 777 todo.txt         # rwxrwxrwx (peligroso)

# Cambiar propietario y grupo
chown usuario archivo.txt
chown usuario:grupo archivo.txt
chgrp grupo archivo.txt
```

## Metadatos de ficheros
### Comando `stat` - Información detallada
```bash
usuario@ubuntu:~$ stat documento.txt
  File: documento.txt
  Size: 1024        Blocks: 8          IO Block: 4096   regular file
Device: 803h/2051d  Inode: 123456      Links: 1
Access: (0644/-rw-r--r--)  Uid: (1000/usuario)   Gid: (1000/usuario)
Access: 2024-06-08 10:30:00.000000000 +0200
Modify: 2024-06-08 09:15:00.000000000 +0200
Change: 2024-06-08 09:15:00.000000000 +0200
 Birth: 2024-06-07 20:00:00.000000000 +0200
```

### Comando `file` - Identificar tipo de fichero
```bash
file documento.txt      # ASCII text
file imagen.jpg         # JPEG image data
file script.sh          # Bash script, ASCII text executable
file /bin/ls            # ELF 64-bit LSB executable
file /dev/sda           # block special
```

## Ficheros especiales importantes
### Dispositivos comunes
| Ruta | Descripción |
|------------|-----------|
| `/dev/null` | Agujero negro: todo lo que se envía aquí se descarta |
| `/dev/zero` | Genera ceros infinitos |
| `/dev/random` | Genera números aleatorios (entrópicos) |
| `/dev/urandom` | Genera números aleatorios (no bloqueante) |
| `/dev/tty` | Terminal actual |
| `/dev/sda` | Primer disco duro SATA/SCSI |

### Ficheros de sistema
| Ruta | Contenido |
|------------|-----------|
| `/etc/passwd` | Usuarios del sistema |
| `/etc/shadow` | Contraseñas encriptadas |
| `/etc/group` | Grupos del sistema |
| `/var/log/syslog` | Logs del sistema |
| `/proc/cpuinfo` | Información del procesador |
| `/proc/meminfo` | Información de memoria |

### Comandos útiles para ficheros

| Comando | Función | Ejemplo |
|------------|-----------|-----------|
| `ls -l` | Listar con detalles | `ls -la /home` |
| `ls -i` | Mostrar inodo | `ls -i archivo.txt` |
| `stat` | Metadatos completos | `stat /etc/passwd` |
| `file` | Identificar tipo | `file descarga.iso` |
| `du` | Tamaño en disco | `du -sh carpeta/` |
| `wc` | Contar líneas/palabras | `wc -l archivo.txt` |
| `ln` | Crear enlaces | `ln -s original link` |
