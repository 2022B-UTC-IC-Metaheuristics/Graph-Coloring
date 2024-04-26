# Graph-Coloring
update by CorvoHyatt (Raul Ruvalcaba)
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

![Grafo de ejemplo](/imagenes/Imagen_GC.png)

Así que el número cromático de este gráfico es 4 y se denota x(G), significa x(G)=4.



### Vector de Solución
**[S H P C I L G A M]**

**[1,2,2,3,3,4,3,4,2]**

1. Amarrilo
2. Azul
3. Verde
4. Rojo

### Matriz de adyacencia

|       | S | H | P | C | I | L | G | A | M |
|-------|---|---|---|---|---|---|---|---|---|
| **S** | 0 | 1 | 0 | 1 | 1 | 1 | 0 | 0 | 0 |
| **H** | 1 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | 0 |
| **P** | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 0 |
| **C** | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 |
| **I** | 1 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 |
| **L** | 1 | 1 | 1 | 0 | 1 | 0 | 1 | 0 | 1 |
| **G** | 0 | 1 | 1 | 0 | 0 | 1 | 0 | 1 | 1 |
| **A** | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 0 | 1 |
| **M** | 0 | 0 | 0 | 0 | 1 | 1 | 1 | 1 | 0 |

# Implementación

## Leer el grafo
Es importante señalar que el csv debe tener solamente números enteros [0,1] separados con una **","** ya que si no se cumple con estas especificaciones el código de enseguida no se ejecutará correctamente.
``` python
import networkx as nx
import numpy as np
import matplotlib.pyplot as plt
import csv
graph = []
with open('10nodos.csv', 'r', newline='') as file:
    myreader = csv.reader(file, delimiter=',')
    for row in myreader:
        # Convierte cada elemento de la fila en un entero
        int_row = [int(cell) for cell in row]
        graph.append(int_row)
graph = np.array(graph)
G = nx.from_numpy_array(graph)
nx.draw(G, with_labels=True, node_color='orange', font_weight='bold')
plt.show()
```
![Grafo de ejemplo](/imagenes/grafo_10nodos.png)

## Especificación
Se considera que **el tamaño de la solución es de tamaño igual a la cantidad de nodos.** También no nos preocupamos por generar una solución que cumpla con las restricciones, ya que la función objetivo se encarga de penalizar las soluciones con conflictos en el coloreado de los nodos adyacentes.

Se busca **Minimizar** el costo.

## Representación de la solución
La solución tiene codificacion de **combinación** con un tamaño igual a la cantidad de nodos. Para este ejemplo de implementación se utilizan 10 nodos por lo que el tamaño del arreglo será $n=10$. Cada elemento del arrelo es un número aleatorio entre y la cantidad de nodos que hay en el grafo:  $[1 , n]$
``` python
actual_solution = [3,10,2,1,5,9,4,1,3,2]
```
## Generación de una solución vecina
Para generar una solución vecina se genera un nuevo arreglo de tamaño igual al tamaño de nodos. No se toma en cuenta si la solución cumple con la restricción de adyacencias ya que la función objetivo se encarga de ello. Para este ejemplo de implementación **se utilizarón 10 nodos** por lo que el arreglo debe ser de tamaño $n=10$. Cada elemento del arrelo es un número aleatorio entre y la cantidad de nodos que hay en el grafo: [1,n]
``` python
actual_vecina = [10,5,2,7,5,6,1,9,2,8]
```

## Función de costo
La función de costo recibe el arreglo de la solución y el grafo con el que se esta trabajando. Calcula los conflictos que presenta la solucion con respecto a la restricción de los colores adyacentes y devuelve el costo. El costo es la suma de la cantidad de conflictos más la cantidad de colores.
``` python
def graph_coloring(solucion, graph):
    ncolores=len(set(solucion))
    conflicts = 0
    for u, v in graph.edges():
        if solucion[u] == solucion[v]:
            conflicts += 1
    return conflicts + ncolores
```

##  Instancias a ejecutar
``` python
parametros = {
	"graph": G,
    "problem_type": "COP",
    "codification": "combination",
    "cooling": "geometric",
    "min_or_max":"min",
    "limits": (1, 10),
    "precision": 1,
    "variables":1,
    "alpha": 0.99,
    "beta": 0.8,
    "time": 1,
    "equilibrium": 15,
    "temperature": 600,
    "final_temperature": 0.01,
}
sa = SimulatedAnnealing(**parametros)
colors = sa.fit(graph_coloring)
print(colors)
```
[10 nodos](csv/10nodos.csv)
[50 nodos](csv/50nodos.csv)
[125 nodos](csv/125nodos.csv)
[300 nodos](csv/300nodos.csv)
[450 nodos](csv/450nodos.csv)
[500 nodos](csv/500nodos.csv)
[500 nodos HellDive Mode](csv/500nodosHard.csv)
[1000 nodos](csv/1000nodos.csv)


### 10 Nodos

| 0 | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 0 | 0 | 1 | 0 | 1 | 0 | 1 | 1 | 0 |
| 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 1 |
| 0 | 1 | 1 | 0 | 1 | 1 | 0 | 0 | 1 | 0 |
| 0 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 0 | 0 |
| 0 | 1 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 1 |
| 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 | 0 |
| 1 | 1 | 0 | 1 | 0 | 0 | 1 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 | 0 | 1 | 0 | 0 | 0 | 0 |

Solución:  [4, 10, 8, 4, 10, 5, 10, 8, 8, 4]

Número Crómatico:  4

![Grafo de ejemplo 2](/imagenes/solucion_10nodos.png)

### 50 Nodos

Solución: [50 42 12 24 42 40  8  6 21 32 24 43 13  8 49 32 21 34 24 49  6 18 43 39
 10 38 27 16 32 20 30 24 27 28 50 47  6  8  7 24 50 12 43 12 32  8  9 39
 40 38]

Número Crómatico:  25

### 125 Nodos

Solución:  [ 11 17  69  64  89  47 124 109  82 104  84 119  58  70 106  79   1  74
   9  88 106  26  91  69  57  84  91  79 116  49  30  81  48  60  99  30
  38 116  80  18  52  11  42  42   5  91  52  96 105  84  67 118  17  57
  53 118  94 113 125  76  53 110  90  15 110 125  46  82  34  57 110  89
  93 124 100  53  80  25  24  79  65  52  65  13  57  47 118  50  11  65
  58  24  71  93 120 102  69  93  21  53  36 119  34  89 103  49  50  47
 107 116  90  79  37  22  84  95 102   3  26   1  81  81  38 120  46]

Número Crómatico:  71

### 300 Nodos

Solución:  [103  60 192 226 225 287  43 280  96 246 288 144 225 168 186 246 167 147
 300 103 216  19 118 235 160 192 257 100 104 163 129  11  76 123 288 132
 257 151 292  47 295 213 111  88 167 223 279  50  51 189  29 199  83 180
 186 200 248  14  16 111 219 269  54  93 255 298  25 253 276  73 235 169
 136 186 185 233  85 145  47 132 192   2 172  73 201 145  98   3  13 232
  36 223 115 201 115  41 269  72 239 115 214 204 269 274 262 102  17  26
  17  33  60 190 195 124   6 224 222 286 266 175  35 186  93  88 155  63
 299 266 213 157 199  26 209 102 247 273 272  95  31 106   8 263   3  98
  36 212  82  44  11 118 131  88 137 154 284  24 224 184 138 152 234 270
  74 252  44 136 129 150 131 261   6 220 190  29 192 172 129  58  73 190
 280  96 221  23 150 123 203 224 247 266 196   2 245 114 182  16 255 242
  98 213  52 114 246 219 234  58 155  87 108 151 178  85 233 214 217 241
 187 105  44 142 289 147 168  17  86 172 201  59 253 241 175  54  23 144
 229 124 119 261   7  86 142 260 105 216 227  70 197 217 175 243  61 213
 174  14 225  89  64 260  23 128 286 210 138 128  65  81 202 261 278 219
 206  98 201 266  32 290  36 101 139 123 261 197 101 253 237 295 225 121
  45   2 135  63 219 172 136 261 146 217 156  53]

Número Crómatico:  238
