# Creación de Ficheros y Editores de Texto en Linux

## Creación de ficheros vacíos

### Comando `touch`

El método más común para crear ficheros vacíos o actualizar timestamp.

    touch archivo.txt
    touch archivo1.txt archivo2.txt archivo3.txt
    touch ~/Descargas/imagen.jpg
    touch Documentos/nota.txt

### Redirección `>`

Crear fichero vacío usando redirección.

    > nuevo_archivo.txt
    echo -n > archivo_vacio.txt

## Editores de texto en terminal

### 1. Nano - El editor amigable para principiantes

Instalación:

    sudo apt install nano

Comandos básicos:

| Comando | Acción |
|---------|--------|
| `nano archivo.txt` | Abrir o crear archivo |
| `Ctrl + O` | Guardar |
| `Ctrl + X` | Salir |
| `Ctrl + W` | Buscar |
| `Ctrl + K` | Cortar línea |
| `Ctrl + U` | Pegar |

Ejemplo:

    nano mi_script.sh

Dentro de nano escribir:

    #!/bin/bash
    echo "Hola mundo"

Luego: `Ctrl+O`, `Enter`, `Ctrl+X`

### 2. Vim - El editor potente

Instalación:

    sudo apt install vim

Modos de Vim:

| Modo | Cómo entrar |
|------|-------------|
| Normal | `Esc` |
| Insert | `i` |
| Comando | `:` |

Comandos esenciales:

    vim archivo.txt
    i                    # Insertar texto
    Esc                  # Volver a modo normal
    :w                   # Guardar
    :q                   # Salir
    :wq                  # Guardar y salir
    :q!                  # Salir sin guardar
    dd                   # Borrar línea
    yy                   # Copiar línea
    p                    # Pegar
    /palabra             # Buscar palabra

### 3. Otros editores

| Editor | Instalación |
|--------|-------------|
| `emacs` | `sudo apt install emacs` |
| `gedit` | `sudo apt install gedit` |
| `neovim` | `sudo apt install neovim` |
| `micro` | `sudo snap install micro` |

## Crear ficheros con contenido directamente

### Usando `echo`

    echo "Hola mundo" > saludo.txt
    echo "Segunda línea" >> saludo.txt
    echo -e "Línea 1\nLínea 2\nLínea 3" > multiples.txt

### Usando `cat` con here document

    cat > script.sh << 'EOF'
    #!/bin/bash
    echo "Inicio del script"
    for i in {1..5}; do
        echo "Número: $i"
    done
    echo "Fin del script"
    EOF

    chmod +x script.sh

### Usando `printf`

    printf "Nombre: %s\nEdad: %d\n" "Ana" 25 > datos.txt
    printf "Línea 1\nLínea 2\nLínea 3\n" > lineas.txt

## Crear múltiples ficheros rápidamente

### Con llaves `{}`

    touch archivo_{1,2,3,4,5}.txt
    touch archivo_{01..10}.txt
    touch {enero,febrero,marzo}.log
    touch {admin,user}_{config,log,backup}.txt
    touch nota_{a,b,c}.md

### Con bucles en terminal

    for i in {1..5}; do touch "fichero_$i.md"; done
    for mes in enero febrero marzo; do echo "Reporte de $mes" > "$mes.txt"; done
    for i in {01..10}; do echo "Contenido $i" > "archivo_$i.txt"; done

## Editores gráficos (si tienes GUI)

    gedit documento.txt &
    mousepad notas.txt &
    code proyecto.py &
    subl archivo.html &
    geany script.sh &

## Buenas prácticas

### Elegir editor según nivel:

| Nivel | Editor |
|-------|--------|
| Principiante | `nano` |
| Intermedio | `nano` o `vim` |
| Avanzado | `vim` |
| Gráfico | `gedit` o VS Code |

### Extensiones sugeridas:

| Extensión | Tipo de archivo |
|-----------|-----------------|
| `.sh` | Script bash |
| `.py` | Python |
| `.md` | Markdown |
| `.txt` | Texto plano |
| `.yml` / `.yaml` | Configuración YAML |
| `.json` | Datos JSON |
| `.csv` | Datos tabulares |
| `.log` | Archivo de registro |

## Ejercicios prácticos

### Ejercicio 1: Crear ficheros de diferentes formas

    touch ejercicio1.txt
    > ejercicio2.txt
    echo "Hola" > ejercicio3.txt
    printf "Línea única\n" > ejercicio4.txt

### Ejercicio 2: Usar nano para crear una lista de tareas

    nano tareas.md

Dentro de nano escribir:

    # Lista de tareas
    - [ ] Aprender Linux
    - [ ] Practicar comandos
    - [ ] Crear scripts
    - [ ] Leer documentación

Guardar: `Ctrl+O`, `Enter`, luego `Ctrl+X`

### Ejercicio 3: Usar vim para crear un script simple

    vim saludar.sh

Dentro de vim:

1. Presionar `i` para insertar
2. Escribir:

    #!/bin/bash
    echo "Hola, este es mi primer script"
    echo "Fecha: $(date)"
    echo "Usuario: $(whoami)"

3. Presionar `Esc`
4. Escribir `:wq` y `Enter`
5. Ejecutar: `bash saludar.sh`

### Ejercicio 4: Crear múltiples ficheros con llaves

    touch clase_{1..15}_notas.txt
    touch informe_{enero,febrero,marzo}.md
    touch config_{dev,prod,test}.yml

### Ejercicio 5: Crear fichero multilínea con cat

    cat > receta.txt << 'EOF'
    Ingredientes:
    - 2 huevos
    - 1 taza de harina
    - 1/2 taza de leche
    - Una pizca de sal

    Preparación:
    1. Mezclar todos los ingredientes
    2. Batir hasta obtener masa homogénea
    3. Cocinar en sartén caliente
    EOF

### Ejercicio 6: Crear ficheros con diferentes formatos

    echo "nombre,edad,ciudad" > datos.csv
    echo "Ana,25,Madrid" >> datos.csv
    echo "Juan,30,Barcelona" >> datos.csv

    echo '{"nombre": "Ana", "edad": 25}' > usuario.json
    echo '{"nombre": "Juan", "edad": 30}' >> usuario.json

### Ejercicio 7: Verificar los ficheros creados

    ls -la
    file *.txt
    file *.sh
    cat tareas.md
    head -5 datos.csv