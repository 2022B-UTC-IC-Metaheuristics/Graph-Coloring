# Graph-Coloring
## Definicion del Problema

En la teoría de grafos, el problema de 'Graph Coloring' es la tarea de asignar colores a los vértices de un grafo de modo que a los pares de vértices adyacentes se les asignan diferentes colores, y el número de colores diferentes utilizados en el gráfico es mínimo.

**El problema Graph Coloring es un problema NP-completo.**

## Número Crómatico

El número más pequeño de colores necesarios para colorear un gráfico G se llama su número cromático.
 
## Aplicaciones

1) Elaboración de un horario o tabla de tiempos.
2) Asignación de frecuencias de radio móvil.
3) Sudoku.
4) Asignación de registros.
5) Grafos bipartitos.
6) Colorear mapas.

## Grafo de Ejemplo

El siguiente gráfico ha sido coloreado usando solo cuatro colores (rojo, azul, verde y amarillo). Este es en realidad el número mínimo de colores necesarios para este grafo en particular, es decir, no podemos colorear este grafo usando menos de cuatro colores mientras nos aseguramos de que los vértices adyacentes tengan un color diferente.

![Grafo de ejemplo](Imagen_GC.png)

Así que el número cromático de este gráfico es 4 y se denota x(G), significa x(G)=4.

## Solucion del Grafo de Ejemplo

### Vector de Solución
**[1, 3, 2, 4, 3, 4, 3, 2, 2]**

1. Amarrilo
2. Azul
3. Verde
4. Rojo

### Matriz de Costos

|  |S |H |P |C |I |L |G |A |M |
|--|--|--|--|--|--|--|--|--|--|
|**S** |0 |1 |0 |1 |1 |1 |0 |0 |0 |
|**H** |1 |0 |0 |0 |0 |1 |1 |1 |0 |
|**P** |0 |0 |0 |0 |0 |1 |1 |0 |0 |
|**C** |1 |0 |0 |0 |0 |0 |0 |1 |0 |
|**I** |1 |0 |0 |0 |0 |1 |0 |0 |1 |
|**L** |1 |1 |1 |0 |1 |0 |1 |0 |1 |
|**G** |0 |1 |1 |0 |0 |1 |0 |1 |1 |
|**A** |0 |0 |0 |1 |0 |0 |1 |0 |1 |
|**M** |0 |0 |0 |0 |1 |1 |1 |1 |0 |


## Función de costo
``` python
def Costo(sol):
  ncolores=len(Counter(sol))
  return ncolores
```

## Funcion generar vecino
``` python
def Genera_Vecino(size,graph,color):
  sol = [0 for i in range(size)]
  ncolor=random.uniform(1, size+1)
  for i in range(size):
    r = int(random.uniform(1, ncolor))
    sol[i] = r
  #verfifica que la solucion sea valida  
  if (isSafe(graph, sol,size))==-1:
    sol=Genera_Vecino(size,graph,color)
  return sol
```
##  Instancias a ejecutar 

 1. 10    con al menos tres vertices en promedio
 2. 50    con al menos tres vertices en promedio
 3. 500  con al menos tres vertices en promedio

Los archivos se encuentran disponibles como 10grafos.csv...

A continuacion el codigo para leer el arhivo csv y guardarlo en una matriz.

``` python
import csv
newMatrix = []
with open('nombre.csv', 'r', newline='') as file:
  myreader = csv.reader(file, delimiter=',')
  for rows in myreader:
   newMatrix.append(rows)
newMatrix = np.array(newMatrix)

```
