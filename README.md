# Graph-Coloring
### Definicion del problema ###

En la teoría de grafos, la coloración de grafos es un caso especial de etiquetado de grafos; es una asignación de etiquetas tradicionalmente llamadas "colores" a los elementos de un grafo sujeta a ciertas restricciones. En su forma más simple, es una forma de colorear los vértices de un grafo de manera que **no haya dos vértices adyacentes del mismo color**; esto se llama colorear vértices.

En términos de teoría de grafos, una coloración adecuada de vértices con k colores es un mapeo.
 
 ![](https://github.com/TranquilinoHG/Metaheuristicas/blob/main/formula1.png)
 
 tal que
 
 ![](https://github.com/TranquilinoHG/Metaheuristicas/blob/main/formula2.png)
 
 ### Número cromatico
 
 El número mínimo de colores para el que existe una coloración de vértices adecuada para un grafo G dado se conoce como el **número cromático** del grafo G y se denota por   **_χ(G)._**

Para cual grafo **_G_** no igual **_Kn_** o **_En_** entonces  **_χ(G)>1_**

**El problema de colorear vértices es NP-completo.** 
 
### Aplicaciones ###
1) Elaboración de un horario o tabla de tiempos: Supongamos que queremos hacer un calendario de exámenes para una universidad. Tenemos una lista de diferentes asignaturas y estudiantes matriculados en cada una de ellas. Muchas asignaturas tendrían alumnos comunes (de la misma hornada, algunos alumnos atrasados, etc). ¿Cómo podemos programar el examen para que no haya dos exámenes con un mismo alumno a la misma hora? ¿Cuántas franjas horarias mínimas se necesitan para programar todos los exámenes? Este problema se puede representar como un grafo en el que cada vértice es una asignatura y una arista entre dos vértices significa que hay un alumno común. Por tanto, se trata de un problema de coloreado de grafos en el que el número mínimo de franjas horarias es igual al número cromático del grafo.

2) Asignación de frecuencias de radio móvil: Cuando se asignan frecuencias a las torres, las frecuencias asignadas a todas las torres en la misma ubicación deben ser diferentes. ¿Cómo se asignan las frecuencias con esta restricción? ¿Cuál es el número mínimo de frecuencias necesario? Este problema es también una instancia del problema de coloreado de grafos donde cada torre representa un vértice y una arista entre dos torres representa que están en el rango de la otra.

3) Sudoku: El sudoku es también una variación del problema de coloreado de grafos donde cada celda representa un vértice. Hay una arista entre dos vértices si están en la misma fila o en la misma columna o en el mismo bloque.

4) Asignación de registros: En la optimización del compilador, la asignación de registros es el proceso de asignar un gran número de variables del programa objetivo a un pequeño número de registros de la CPU. Este problema es también un problema de coloreado de grafos.

5) Grafos bipartitos: Podemos comprobar si un gráfico es bipartito o no coloreando el gráfico con dos colores. Si un grafo dado es coloreable con dos colores, entonces es bipartito, de lo contrario no. Vea esto para más detalles.

6) Colorear mapas: Mapas geográficos de países o estados en los que no se puede asignar el mismo color a dos ciudades adyacentes. Cuatro colores son suficientes para colorear cualquier mapa

### Ejemplo ### 
**Grafo de ejemplo**

![Grafo de ejemplo.](https://github.com/TranquilinoHG/Metaheuristicas/blob/main/grafoSinResolver.png)  

Para este ejemplo tenemos que el numero de grafos es de 

N = 9


### Solucion del grafo de ejemplo.

![Solucion de Grafo de ejemplo.](https://github.com/TranquilinoHG/Metaheuristicas/blob/main/grafo.png)

#### Vector de solución.
**[1, 2, 2, 3, 3, 4, 3, 4, 2]**

1. Amarrilo  
2. Azul 
3. Verde
4. Rojo

En este ejemplo el numero cromatico es

**_χ(G) = 4_**


### Matriz de costo ####


|  |S |H |P |C |I |L |G |A |M |
|--|--|--|--|--|--|--|--|--|--|
|**S** |0 |1 |0 |1 |1 |1 |0 |0 |0 |
|**H** |1 |0 |0 |0 |0 |1 |1 |1 |0 |
|**P** |0 |0 |0 |0 |0 |1 |1 |0 |0 |
|**C** |1 |0 |0 |0 |0 |0 |0 |1 |0 |
|**I** |1 |0 |0 |0 |0 |1 |0 |0 |1 |
|**L** |1 |1 |1 |0 |0 |1 |1 |0 |1 |
|**G** |0 |1 |1 |0 |0 |1 |0 |1 |1 |
|**A** |0 |0 |0 |1 |0 |0 |1 |0 |1 |
|**M** |0 |0 |0 |0 |1 |1 |1 |1 |0 |


## Función objetivo

**_min de χ(G)._**


 
