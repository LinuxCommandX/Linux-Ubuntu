# Visualización de Ficheros y Directorios en Linux

## Visualización de directorios

### Comando `ls` - El básico fundamental

Opciones principales:

| Opción | Descripción |
|--------|-------------|
| `ls` | Listado simple |
| `ls -l` | Formato largo (detalles) |
| `ls -a` | Muestra archivos ocultos |
| `ls -la` | Todo, detallado |
| `ls -lh` | Tamaños legibles (humanos) |
| `ls -ltr` | Ordenado por fecha inversa |
| `ls -R` | Listado recursivo |
| `ls -S` | Ordenar por tamaño |
| `ls -i` | Mostrar inodo |

Ejemplos:

    ls
    ls -la
    ls -lh /home
    ls -ltr
    ls -R
    ls --color=auto

### Comando `tree` - Estructura jerárquica

Instalación:

    sudo apt install tree

Uso:

    tree
    tree /home
    tree -L 2
    tree -d
    tree -a
    tree -h

### Otros comandos

    pwd        # Muestra directorio actual
    dir        # Alternativa a ls

## Visualización de ficheros

### Ver contenido completo

| Comando | Descripción |
|---------|-------------|
| `cat` | Muestra todo el contenido |
| `tac` | Muestra en orden inverso |
| `nl` | Muestra con números de línea |

Ejemplos:

    cat /etc/passwd
    cat archivo1.txt archivo2.txt
    cat -n archivo.txt
    tac archivo.txt
    nl script.py

### Paginación (archivos grandes)

| Comando | Descripción | Navegación |
|---------|-------------|-------------|
| `less` | Paginador avanzado | Espacio(bajar), b(subir), q(salir) |
| `more` | Paginador básico | Espacio(bajar), q(salir) |

Comandos dentro de less:

    /patron        # Buscar hacia adelante
    ?patron        # Buscar hacia atrás
    n              # Siguiente coincidencia
    N              # Coincidencia anterior
    g              # Ir al principio
    G              # Ir al final
    v              # Abrir en editor

Ejemplos:

    less /var/log/syslog
    more archivo.txt

### Ver partes del fichero

| Comando | Descripción |
|---------|-------------|
| `head` | Primeras líneas |
| `tail` | Últimas líneas |
| `tail -f` | Sigue el fichero en tiempo real |

Ejemplos:

    head /etc/passwd
    head -20 archivo.log
    tail -50 archivo.log
    tail -f /var/log/syslog

Ver líneas específicas (combinando comandos):

    head -30 archivo.txt | tail -11

## Visualización avanzada

### sed (mostrar rangos)

    sed -n '10,20p' archivo.txt
    sed -n '/error/p' log.txt

### awk (formatear y filtrar)

    awk '{print $1, $3}' /etc/passwd
    awk '/bash$/ {print $1}' /etc/passwd

### Ver archivos comprimidos

    zcat archivo.gz
    zless archivo.gz
    bzcat archivo.bz2

### Ver caracteres especiales

    cat -v archivo_colores.log
    cat -A archivo.txt

## Filtrar y buscar contenido

### grep (buscar dentro)

    grep "error" log.txt
    grep -i "error" log.txt
    grep -v "debug" log.txt
    grep -n "error" log.txt
    grep -r "function" ./src/
    grep -E "error|warning" log.txt

### wc (contar líneas, palabras, bytes)

    wc archivo.txt
    wc -l archivo.txt
    wc -w archivo.txt
    wc -c archivo.txt
    wc -L archivo.txt

### sort y uniq

    sort lista.txt
    sort -r lista.txt
    sort -n numeros.txt
    sort lista.txt | uniq
    sort lista.txt | uniq -c
    sort lista.txt | uniq -d

## Ejemplos prácticos

### Ver estructura completa de un proyecto

    tree -L 3 proyecto/
    ls -laR proyecto/

### Monitorear logs en tiempo real

    tail -f /var/log/nginx/access.log
    tail -f /var/log/syslog | grep "error"

### Buscar archivos grandes en el sistema

    find / -type f -size +100M 2>/dev/null | head -20

### Ver estadísticas de un archivo

    wc -l archivo.txt
    ls -lh archivo.txt
    stat archivo.txt

### Filtrar y contar ocurrencias

    grep "ERROR" app.log | wc -l
    cat access.log | awk '{print $1}' | sort | uniq -c | sort -rn | head -10

### Ver primeras y últimas líneas de múltiples archivos

    head -5 *.log
    tail -10 *.txt

## Comandos útiles adicionales

| Comando | Función |
|---------|---------|
| `ls -la | less` | Listar con paginación |
| `ls -la | grep "^-"` | Solo ficheros |
| `ls -la | grep "^d"` | Solo directorios |
| `cat /dev/null > archivo.txt` | Vaciar archivo |
| `tail -f archivo.txt | grep palabra` | Filtrar en tiempo real |