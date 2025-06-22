# **Sudoku-con-Hadoop-MapReduce-en-Docker**


Este README detalla cómo utilizar un entorno Hadoop configurado con Docker para resolver sudokus mediante un ejemplo de MapReduce. El proceso incluye la descarga y copia de archivos necesarios, la ejecución del algoritmo y la visualización de los resultados.

**Resumen del Proyecto**

Este proyecto demuestra la capacidad de Hadoop para procesar tareas computacionalmente intensivas, como la resolución de sudokus, utilizando el framework MapReduce en un entorno Dockerizado. Se asume que ya tienes un clúster Hadoop básico levantado en Docker. El objetivo es guiarte paso a paso en la ejecución de un ejemplo de Sudoku MapReduce, desde la preparación de los archivos hasta la obtención de la solución.

**Requisitos Previos**

Antes de comenzar, asegúrate de tener:
Un entorno Hadoop levantado en Docker. Si aún no lo tienes configurado, consulta la documentación sobre cómo levantar un nodo Hadoop con Docker.
Docker Desktop o similar, funcionando correctamente en tu sistema.
Acceso a la terminal de tu máquina local.

**Pasos de Configuración y Ejecución**

Sigue estos pasos para resolver un sudoku con Hadoop MapReduce:

**1. Descargar Archivos Necesarios**

Necesitarás el archivo JAR de ejemplos de Hadoop y un archivo de texto que contenga el sudoku a resolver.

**Script de Ejemplo MapReduce:**
Descarga el archivo hadoop-examples-0.20.205.0.jar (o la versión compatible con tu configuración de Hadoop).
Mueve este archivo a la misma carpeta donde se encuentra tu repositorio docker-hadoop.

**Archivo de Sudoku para Procesar:**
Descarga el archivo puzzle1.dta (que contiene el sudoku).
Mueve este archivo a la misma carpeta donde se encuentra tu repositorio docker-hadoop.

**2. Copiar Archivos al Contenedor Hadoop**

Desde tu máquina local, copia ambos archivos al directorio /tmp del contenedor namenode.

**Copia del JAR de ejemplos:**
Bash
docker cp hadoop-examples-0.20.205.0.jar namenode:/tmp

Si ya tienes este archivo en tu nodo Hadoop, puedes omitir este paso.

**Copia del archivo de Sudoku:**
Bash
docker cp puzzle1.dta namenode:/tmp


**3. Ejecutar MapReduce para Resolver el Sudoku**

Accede al terminal del contenedor namenode para ejecutar el trabajo de MapReduce.
**Ingresar al contenedor namenode:**
Bash
docker exec -it namenode bash

**Navegar al directorio temporal:**
Una vez dentro del contenedor, dirígete al directorio donde copiaste los archivos:
Bash
cd /tmp


**Ejecutar el algoritmo Sudoku MapReduce:**
Este comando ejecutará el ejemplo de Sudoku incluido en el JAR, utilizando puzzle1.dta como entrada.
Bash
hadoop jar hadoop-examples-0.20.205.0.jar sudoku puzzle1.dta

La salida en la consola será extensa, pero esto indica que el proceso se está ejecutando correctamente.

**4. Ver y Guardar los Resultados**

Para capturar la solución del sudoku en un archivo y luego transferirlo a tu máquina local:

**Guardar la solución en un archivo dentro del contenedor:**
Ejecuta el mismo comando anterior, pero redirigiendo la salida a un archivo de texto:
Bash
hadoop jar hadoop-examples-0.20.205.0.jar sudoku puzzle1.dta > solucion_puzzle1.txt


**Salir del contenedor namenode:**
Bash
exit


**Copiar el archivo de solución a tu máquina local:**
Desde la terminal de tu máquina local (fuera del contenedor), copia el archivo de resultados desde el contenedor a la carpeta de tu repositorio docker-hadoop. Asegúrate de incluir el punto al final del comando, que representa el directorio actual.
Bash
docker cp namenode:/tmp/solucion_puzzle1.txt .

Ahora, el archivo solucion_puzzle1.txt debería estar en la carpeta de tu repositorio docker-hadoop.

**5. Visualizar la Solución**

Finalmente, abre el archivo solucion_puzzle1.txt que se encuentra en la carpeta de tu repositorio docker-hadoop para ver la solución del sudoku.



