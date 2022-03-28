# Graph-Coloring
# Sequential-Ordering-Problem



### 1.-Definicion del problema ###

El problema de ordenamiento secuencial consiste en encontrar un camino hamiltonanio de costo minimo, esto quiere decir que se debe encontrar el camino con los menores costos. El grafo con el que se debe representar debe ser un grafo dirigido con costos asociados a los ejes y relaciones de precedencia entre los nodos. Al hablar de relaciones de presedencia, nos referimos a una o mas reglas en el grafo que indican que nodos se deben visitar primero.Este problema puede verse como una variante del TSP, la diferencia principal recae en que el grafo debe ser asincrono debido a la presedencia. Pero tampoco podemos decir que se trata de un problema ATSP.
De manera formal el problema se define de la siguiente forma;

Sea G=(V,E) un grafo dirigido completo, donde V= {0,1,2,3...} es el conjunto de nodos y E= {(i,j)| i,j E V,/=j}. Cada eje (i,j) E E tiene un costo asociado Cij >= 0. Ademas, se define el grafo de precedencias P = (V, R) con el mismo conjunto de nodos V .

Un camino que recorre todos los nodos sin repetirlos, comenzando en el 0 y terminando en n, y satisface todas las condiciones de precedencia es una solucion factible del SOP. El objetivo del SOP es encontrar una solucion factible de mınimo costo, donde el costo esta dado por la sumatoria de los costos de los ejes que componen el camino.


### 2.2 Aplicaciones ###
Algunas aplicaciones de este problema cuando encontramos alguna situacion como mejoramientos en cadenas de produccion, planificacion y ruteo por ejemplo:

**Planificacion de produccion:** Minimizar tiempo de ejecucion de varios trabajos, que deben ser proceso en cierto orden por una maquina.

**Optimizacion:** En el uso de una grua portuaria eliminando cuellos de botella.

**Problemas de transporte** por ejemplo minimizar la distancia recorrida por un helicoptero que debe transportar personal tecnico entre diferentes plataformas en una compañia petrolera.

**Optimizaciones en fabricas** por ejemplo en manufactura del automotor, en el sistema de pintado de los autos, para minimizar costos de cambio de color de la pintura.

### 2.3 Ejemplo ### 
**GRAFO DE EJEMPLO**

![Grafo de ejemplo.](https://github.com/TranquilinoHG/Metaheuristicas/blob/main/grafoSinResolver.png)  

**SOLUCION DE GRAFO DE EJEMPLO**

![Solucion de Grafo de ejemplo.](https://github.com/TranquilinoHG/Metaheuristicas/blob/main/grafo.png)

**Vector Solucion**

[0, 2, 3, 4, 5, 6, 1, 7]

**Matriz de costo**


| |0 |1 |2 |3 |4 |5 |6 |7 |
|--|--|--|--|--|--|--|--|--|
|**0** |0 |1 |7 |2 |6 |7 |1 |5 |
|**1** |8 |0 |2 |3 |8 |4 | 6 | 7 |
|**2** |9 |-1 |0 |4 |1 |6 |9 |1 |
|**3** |6 |3 |3 |0 |3 |5 |4 |3 |
|**4** |8 |2 |3 |5 |0 |3 |7 |5 |
|**5** |1 |5 |6 |3 |8 |0 |6 |1 |
|**6** |7 |-1 |3 |8 |3 |6 |0 |9 |
|**7** |4 |6 |7 |8 |3 |2 |1 |0 |


## 3.- Modelo
### Función objetivo
La función objetivo para el problema de ordenamiento secuencial es la siguiente: **$\sum$ $C_{ij}$ + (n * penalización)**

Donde la **penalización** será igual al costo mayor de toda la matriz de costos y **n** representa el número de reglas de precedencia que no se cumplen.

El siguiente fragmento de código indica el proceso para calcular el valor de la función objetivo.
