# Manipulación de Ficheros y Directorios en Linux

## Operaciones básicas

### Copiar ficheros y directorios

| Comando | Descripción |
|---------|-------------|
| `cp origen destino` | Copiar fichero |
| `cp -r origen destino` | Copiar directorio recursivamente |
| `cp -i origen destino` | Preguntar antes de sobrescribir |
| `cp -v origen destino` | Mostrar lo que se copia |
| `cp -u origen destino` | Copiar solo si origen es más nuevo |
| `cp -a origen destino` | Copiar con todos los atributos |

Ejemplos:

    cp documento.txt copia.txt
    cp -r Documentos/ Backup/
    cp -i archivo.txt /home/usuario/
    cp -v *.txt carpeta_destino/
    cp -u config.yml ../config.yml

### Mover y renombrar ficheros

| Comando | Descripción |
|---------|-------------|
| `mv origen destino` | Mover o renombrar |
| `mv -i origen destino` | Preguntar antes de sobrescribir |
| `mv -v origen destino` | Mostrar lo que se mueve |
| `mv -u origen destino` | Mover solo si origen es más nuevo |

Ejemplos:

    mv viejo.txt nuevo.txt
    mv archivo.txt ../Documentos/
    mv -i documento.txt copia.txt
    mv *.log logs/
    mv carpeta1/ carpeta2/

### Eliminar ficheros y directorios

| Comando | Descripción |
|---------|-------------|
| `rm archivo` | Eliminar fichero |
| `rm -r carpeta` | Eliminar directorio recursivamente |
| `rm -f archivo` | Forzar eliminación sin preguntar |
| `rm -i archivo` | Preguntar antes de eliminar |
| `rm -rf carpeta` | Eliminar directorio forzosamente (peligroso) |
| `rmdir carpeta` | Eliminar directorio vacío |

Ejemplos:

    rm archivo.txt
    rm -r carpeta_vieja/
    rm -i documento.txt
    rm -f *.log
    rm -rf basura/          # ¡Cuidado! No se puede recuperar
    rmdir carpeta_vacia/

### Crear directorios

| Comando | Descripción |
|---------|-------------|
| `mkdir carpeta` | Crear directorio |
| `mkdir -p ruta/completa` | Crear directorios intermedios |
| `mkdir -v carpeta` | Mostrar lo que se crea |
| `mkdir -m 755 carpeta` | Crear con permisos específicos |

Ejemplos:

    mkdir nueva_carpeta
    mkdir -p proyecto/{src,docs,test}
    mkdir -v Documentos/Fotos
    mkdir -m 700 secreto

## Operaciones avanzadas

### Enlaces (accesos directos)

| Comando | Descripción |
|---------|-------------|
| `ln -s origen destino` | Enlace simbólico (soft link) |
| `ln origen destino` | Enlace duro (hard link) |

Ejemplos:

    ln -s /etc/passwd enlace_passwd
    ln -s /usr/bin/python3 python
    ln original.txt enlace_duro.txt

Diferencia entre enlaces:

    # Enlace simbólico (apunta por nombre)
    ln -s archivo.txt link_simbolico
    
    # Enlace duro (mismo inodo)
    ln archivo.txt link_duro

### Sincronización con rsync

    rsync -avz origen/ destino/
    rsync -avz --delete origen/ destino/
    rsync -avz --exclude="*.log" origen/ destino/

### Permisos (visto en módulo 3)

    chmod 755 script.sh
    chmod u+x archivo.txt
    chown usuario:grupo archivo.txt

## Ejemplos prácticos

### Ejemplo 1: Copiar archivos con diferentes opciones

    # Copia simple
    cp documento.txt backup.txt
    
    # Copia recursiva de directorio
    cp -r Documentos/ Documentos_backup/
    
    # Copiar solo archivos .txt
    cp *.txt carpeta_destino/
    
    # Copiar preservando atributos
    cp -a configuracion/ config_backup/

### Ejemplo 2: Mover y organizar archivos

    # Mover archivo a otro directorio
    mv imagen.jpg ~/Imagenes/
    
    # Renombrar archivo
    mv viejo_nombre.txt nuevo_nombre.txt
    
    # Mover múltiples archivos
    mv *.pdf Documentos/PDFs/
    mv *.log *.txt logs/

### Ejemplo 3: Eliminar archivos de forma segura

    # Preguntar antes de eliminar
    rm -i documento_importante.txt
    
    # Eliminar archivos .tmp
    rm *.tmp
    
    # Eliminar directorio vacío
    rmdir carpeta_vacia/
    
    # Eliminar directorio con contenido (con confirmación)
    rm -ri carpeta_con_contenido/

### Ejemplo 4: Crear estructura de proyecto

    # Crear directorios anidados
    mkdir -p proyecto/{src,docs,tests,data}
    
    # Crear archivos dentro de la estructura
    touch proyecto/README.md
    touch proyecto/src/{main.py,utils.py}
    touch proyecto/docs/manual.md
    touch proyecto/tests/test_main.py

### Ejemplo 5: Copia de seguridad con fecha

    # Crear backup con fecha actual
    cp archivo.txt "backup_$(date +%Y%m%d).txt"
    
    # Copiar directorio entero con timestamp
    cp -r proyecto/ "proyecto_backup_$(date +%Y%m%d_%H%M%S)/"

### Ejemplo 6: Trabajar con enlaces

    # Crear enlace simbólico a un script
    ln -s /usr/local/bin/mi_script.sh ~/mi_enlace
    
    # Crear enlace duro (mismo contenido físico)
    ln original.txt copia_duro.txt
    
    # Ver enlaces
    ls -li original.txt copia_duro.txt link_simbolico

### Ejemplo 7: Mover archivos por extensión

    # Mover todos los .jpg a Imagenes
    mv *.jpg ~/Imagenes/
    
    # Mover todos los .mp3 a Musica
    mv *.mp3 ~/Musica/
    
    # Mover archivos grandes (>100MB) a otra carpeta
    find . -type f -size +100M -exec mv {} ./archivos_grandes/ \;

## Comandos útiles adicionales

| Comando | Función |
|---------|---------|
| `cp -n origen destino` | No sobrescribir si destino existe |
| `cp -s origen destino` | Crear enlace simbólico en lugar de copiar |
| `mv -n origen destino` | No sobrescribir si destino existe |
| `rm -d carpeta` | Eliminar directorio vacío (como rmdir) |
| `rm -- -archivo.txt` | Eliminar archivo que empieza con - |
| `mkdir -p /tmp/{a,b,c}/{d,e}` | Crear múltiples directorios anidados |

## Buenas prácticas

### Antes de eliminar

1. **Siempre verificar qué se va a eliminar:**

    ls -la archivos_a_borrar*
    rm -i archivos_a_borrar*

2. **Usar `rm -i` para archivos importantes**
3. **No usar `rm -rf` a menos que estés seguro**
4. **Hacer respaldos antes de operaciones masivas**

### Antes de copiar/mover

1. **Verificar espacio en disco:**

    df -h

2. **Verificar que el destino existe:**

    ls -ld destino/

3. **Usar `-i` para no sobrescribir por accidente**

### Organización recomendada

    ~/
    ├── Documentos/
    │   ├── trabajo/
    │   ├── personal/
    │   └── backups/
    ├── Descargas/
    ├── Imagenes/
    ├── Musica/
    ├── Videos/
    ├── proyectos/
    │   ├── proyecto1/
    │   ├── proyecto2/
    │   └── scripts/
    └── tmp/

## Ejercicios para practicar

### Ejercicio 1: Crear y organizar

    mkdir -p practica/{fotos,documentos,backups}
    touch practica/documentos/nota1.txt
    touch practica/documentos/nota2.txt
    touch practica/fotos/imagen.jpg
    cp practica/documentos/nota1.txt practica/backups/
    mv practica/documentos/nota2.txt practica/backups/

### Ejercicio 2: Renombrar y mover

    touch archivo.txt
    mv archivo.txt documento.txt
    mkdir carpeta
    mv documento.txt carpeta/
    ls carpeta/

### Ejercicio 3: Copiar múltiples archivos

    touch file1.txt file2.txt file3.txt
    mkdir destino
    cp *.txt destino/
    ls destino/

### Ejercicio 4: Eliminar selectivamente

    touch temp1.log temp2.log temp3.log
    rm *.log
    mkdir carpeta_vacia carpeta_con_archivos
    touch carpeta_con_archivos/archivo.txt
    rmdir carpeta_vacia
    rm -r carpeta_con_archivos

### Ejercicio 5: Enlaces

    echo "Contenido original" > original.txt
    ln -s original.txt link_simbolico
    ln original.txt link_duro
    cat link_simbolico
    cat link_duro
    rm original.txt
    cat link_duro
    cat link_simbolico   # Esto falla (enlace roto)