# Búsqueda de Ficheros y Directorios en Linux

## Comando `find` - El más potente

### Sintaxis básica

    find [ruta] [opciones] [expresión]

### Búsqueda por nombre

    find /home -name "*.txt"
    find /var -name "config.conf"
    find . -name "*.jpg"
    find /etc -iname "*.conf"    # Ignora mayúsculas/minúsculas

### Búsqueda por tipo

    find /home -type f           # Solo ficheros
    find /home -type d           # Solo directorios
    find /home -type l           # Solo enlaces simbólicos

### Búsqueda por tamaño

    find /var -type f -size +10M      # Mayor a 10MB
    find /var -type f -size -1M       # Menor a 1MB
    find /var -type f -size 100k      # Exactamente 100KB
    find . -type f -size +100M -size -500M   # Entre 100MB y 500MB

Unidades de tamaño:
- `c` bytes
- `k` kilobytes
- `M` megabytes
- `G` gigabytes

### Búsqueda por tiempo

    find ~ -mtime -7             # Modificados últimos 7 días
    find ~ -mtime +30            # Modificados hace más de 30 días
    find ~ -atime -1             # Accedidos últimas 24 horas
    find ~ -ctime -3             # Cambiados últimos 3 días
    find ~ -mmin -60             # Modificados últimos 60 minutos

### Búsqueda por permisos

    find . -perm 755             # Permisos exactos 755
    find . -perm -644            # Al menos permisos 644
    find . -perm /u+x            # Ejecutable por propietario
    find . -not -perm 644        # No tienen permiso 644

### Búsqueda por usuario/grupo

    find /home -user usuario
    find /var -group www-data
    find / -nouser               # Archivos sin propietario

### Ejecutar comandos sobre lo encontrado

    find . -name "*.txt" -exec ls -la {} \;
    find . -name "*.log" -exec rm {} \;
    find . -type f -exec grep "error" {} \;
    find /tmp -name "temp*" -delete

### Combinar condiciones

    find . -name "*.txt" -and -size +1M
    find . -name "*.jpg" -or -name "*.png"
    find . -not -name "*.txt"

## Comando `locate` - Búsqueda rápida

### Uso básico

    sudo updatedb               # Actualizar base de datos
    locate archivo.txt
    locate -i "*.jpg"           # Ignorar mayúsculas
    locate -l 10 config.conf    # Limitar a 10 resultados

### Comandos útiles

    locate /etc/*.conf
    locate -c "*.py"            # Contar resultados
    locate -r ".*\.md$"         # Usar expresión regular

## Comando `grep` - Buscar dentro de ficheros

### Sintaxis básica

    grep "patrón" archivo.txt
    grep -r "patrón" ./directorio/

### Opciones principales

| Opción | Descripción |
|--------|-------------|
| `-i` | Ignorar mayúsculas/minúsculas |
| `-v` | Mostrar líneas que NO contienen el patrón |
| `-n` | Mostrar números de línea |
| `-c` | Contar coincidencias |
| `-l` | Mostrar solo nombres de archivo |
| `-L` | Mostrar archivos sin coincidencias |
| `-r` | Buscar recursivamente |
| `-w` | Buscar palabra completa |
| `-A 3` | Mostrar 3 líneas después |
| `-B 3` | Mostrar 3 líneas antes |
| `-C 3` | Mostrar 3 líneas antes y después |
| `-E` | Usar expresiones regulares extendidas |

### Ejemplos

    grep "error" /var/log/syslog
    grep -i "warning" app.log
    grep -v "debug" log.txt
    grep -n "function" script.py
    grep -c "ERROR" log.txt
    grep -l "TODO" *.py
    grep -r "main" ./src/
    grep -w "if" script.sh
    grep -A 5 "Exception" log.txt
    grep -E "error|warning|critical" log.txt

## Comandos para encontrar comandos

### `which`

    which python3
    which ls
    which nano

### `whereis`

    whereis ls
    whereis python3
    whereis -b nginx      # Solo binarios
    whereis -m ls         # Solo manuales

### `type`

    type ls
    type cd
    type -a python3

## Ejemplos prácticos

### Ejemplo 1: Buscar archivos por nombre y extensión

    # Buscar todos los .txt en home
    find ~ -name "*.txt"
    
    # Buscar archivos de configuración
    find /etc -name "*.conf"
    
    # Buscar scripts bash
    find /usr/bin -name "*.sh"

### Ejemplo 2: Buscar archivos por tamaño

    # Encontrar archivos mayores a 100MB
    find / -type f -size +100M 2>/dev/null
    
    # Encontrar archivos vacíos
    find . -type f -size 0
    
    # Encontrar y eliminar archivos vacíos
    find . -type f -size 0 -delete

### Ejemplo 3: Buscar archivos modificados recientemente

    # Archivos modificados hoy
    find . -type f -mtime -1
    
    # Archivos modificados en la última hora
    find . -type f -mmin -60
    
    # Archivos accedidos hoy
    find . -type f -atime -1

### Ejemplo 4: Buscar y ejecutar acciones

    # Buscar y mostrar detalles
    find . -name "*.log" -exec ls -lh {} \;
    
    # Buscar y eliminar
    find /tmp -name "temp_*" -exec rm {} \;
    
    # Buscar y mover
    find . -name "*.jpg" -exec mv {} ~/Imagenes/ \;

### Ejemplo 5: Buscar dentro de archivos con grep

    # Buscar texto en archivos .py
    grep -r "def main" --include="*.py"
    
    # Buscar en toda la carpeta excluyendo .log
    grep -r "error" --exclude="*.log"
    
    # Buscar con contexto
    grep -C 3 "Exception" app.log

### Ejemplo 6: Combinar find con grep

    # Buscar "ERROR" en archivos .log recientes
    find . -name "*.log" -mtime -1 -exec grep "ERROR" {} \;
    
    # Buscar archivos grandes que contengan "password"
    find . -type f -size +1M -exec grep -l "password" {} \;

### Ejemplo 7: Usar locate para búsqueda rápida

    # Actualizar base de datos
    sudo updatedb
    
    # Buscar archivos de configuración
    locate "*.conf"
    
    # Buscar archivos ignorando mayúsculas
    locate -i "README"

## Comandos útiles adicionales

| Comando | Función |
|---------|---------|
| `find . -empty` | Encontrar archivos vacíos |
| `find . -type f -executable` | Encontrar archivos ejecutables |
| `find . -type d -empty` | Encontrar directorios vacíos |
| `find . -name "*.tmp" -delete` | Eliminar archivos temporales |
| `grep -r "TODO" --color` | Buscar TODOs con colores |
| `locate -r ".*\.md$"` | Expresión regular en locate |

## Búsqueda con expresiones regulares

### Ejemplos con find y regex

    find . -regex ".*\.txt$"
    find . -regex ".*\.\(jpg\|png\|gif\)$"
    find . -iregex ".*\.\(pdf\|doc\)$"

### Ejemplos con grep y regex

    grep "^[0-9]" archivo.txt
    grep "[A-Za-z]\+@[A-Za-z]\+\.com" emails.txt
    grep "^[0-9]\{3\}-[0-9]\{3\}-[0-9]\{4\}" telefonos.txt

## Buenas prácticas

### Antes de buscar

1. **Especificar la ruta lo más precisa posible:**
   - `find /home` es más rápido que `find /`
   - `find .` busca desde el directorio actual

2. **Redirigir errores para evitar permisos:**
   - `find / -name "*.txt" 2>/dev/null`

3. **Usar `-maxdepth` para limitar profundidad:**
   - `find . -maxdepth 3 -name "*.txt"`

### Consejos de rendimiento

1. **`locate` es mucho más rápido que `find`** (pero necesita `updatedb`)
2. **Usar `-type f` cuando solo buscas archivos** (no directorios)
3. **Combinar condiciones con `-and` / `-or`**

## Ejercicios para practicar

### Ejercicio 1: Buscar por nombre

    mkdir -p prueba/{docs,imagenes,scripts}
    touch prueba/docs/nota.txt
    touch prueba/docs/documento.pdf
    touch prueba/imagenes/foto.jpg
    touch prueba/scripts/script.sh
    
    find prueba -name "*.txt"
    find prueba -name "*.jpg"
    find prueba -name "*.sh"

### Ejercicio 2: Buscar por tamaño

    truncate -s 1M prueba/docs/archivo1.txt
    truncate -s 10M prueba/docs/archivo2.txt
    truncate -s 100M prueba/imagenes/imagen_grande.jpg
    
    find prueba -size +5M
    find prueba -size -50M
    find prueba -size +50M

### Ejercicio 3: Buscar por tiempo

    touch -t 202401011200 prueba/docs/antiguo.txt
    touch prueba/docs/nuevo.txt
    
    find prueba -mtime -1
    find prueba -mtime +30

### Ejercicio 4: Buscar dentro de archivos

    echo "Error: algo falló" > prueba/docs/error.log
    echo "Todo correcto" > prueba/docs/ok.log
    echo "Error crítico" > prueba/scripts/error.log
    
    grep -r "Error" prueba/
    grep -r -l "Error" prueba/
    grep -r -c "Error" prueba/

### Ejercicio 5: Buscar y ejecutar

    find prueba -name "*.log" -exec ls -lh {} \;
    find prueba -name "*.txt" -exec cat {} \;
    find prueba -size +50M -exec rm -i {} \;

### Ejercicio 6: Limpiar resultados

    find prueba -type f -name "*.txt" -delete
    find prueba -type d -empty -delete
    ls -la prueba/