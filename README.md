# Inteligencia Artificial: Algoritmo A\*, Heurísticas y Teoría de Juegos

## Presentación

**Estudiante:** Brayan R. M.  
**Asignatura:** Inteligencia Artificial  
**Trabajo:** Algoritmo A*, Heurísticas y Teoría de Juegos  
**Lenguaje utilizado:** Python  

Este repositorio presenta una investigación y ejemplos prácticos sobre tres conceptos fundamentales de la inteligencia artificial:

- Algoritmo de búsqueda A*
- Heurísticas en inteligencia artificial
- Teoría de juegos aplicada a sistemas multiagente

Además, se incluyen ejemplos implementados en Python y un notebook ejecutable en Google Colab.

## Abrir Notebook en Google Colab donde se encuentra los codigos de ejemplo

[![Open In
Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BrayanRM27/IA-AStar-Heuristicas-TeoriaDeJuegos/blob/main/CODIGOS.ipynb)


------------------------------------------------------------------------


## Contenido

1. Introducción  
2. Algoritmo A*  
3. Heurísticas en Inteligencia Artificial  
4. Teoría de Juegos  
5. Ejemplos en Python  
6. Conclusión  
7. Bibliografía

------------------------------------------------------------------------

# Introducción

La inteligencia artificial (IA) es una disciplina de la informática que
busca desarrollar sistemas capaces de resolver problemas de forma
autónoma mediante algoritmos y modelos computacionales.

Dentro de este campo, los algoritmos de búsqueda permiten explorar
grandes espacios de soluciones con el objetivo de encontrar el camino
óptimo hacia un objetivo.

Uno de los algoritmos más importantes es el **algoritmo A**\* (A-Star).
Este algoritmo combina el costo real del camino recorrido con una
estimación heurística del costo restante, permitiendo encontrar rutas
óptimas de manera eficiente.

Además, la inteligencia artificial también analiza la toma de decisiones
cuando múltiples agentes interactúan entre sí. Este tipo de problemas se
estudia mediante la **teoría de juegos**, que analiza situaciones de
cooperación y competencia entre agentes racionales.

En este trabajo se investigan tres conceptos fundamentales:

-   Algoritmo A\*
-   Heurísticas en inteligencia artificial
-   Teoría de juegos aplicada a sistemas multiagente

También se presentan **ejemplos prácticos implementados en Python**.

------------------------------------------------------------------------

# Algoritmo A\*

## ¿Qué es el algoritmo A\*?

El algoritmo **A**\* es un algoritmo de búsqueda informada utilizado
para encontrar el camino de menor costo entre un nodo inicial y un nodo
objetivo dentro de un grafo.

Este algoritmo se utiliza en diferentes áreas:

-   Videojuegos (pathfinding)
-   Robótica
-   Sistemas GPS
-   Optimización de redes

A diferencia de algoritmos de búsqueda no informados, A\* utiliza una
función heurística que estima la distancia restante hasta el objetivo.

------------------------------------------------------------------------

## Fundamento matemático

El algoritmo evalúa cada nodo utilizando la función:

$$
f(n) = g(n) + h(n)
$$

donde:

-   g(n) → costo real desde el nodo inicial hasta el nodo actual\
-   h(n) → estimación heurística desde el nodo actual hasta el objetivo\
-   f(n) → costo total estimado

El algoritmo siempre selecciona el nodo con el menor valor de f(n).

------------------------------------------------------------------------

## Propiedad de admisibilidad

Una heurística es **admisible** si nunca sobreestima el costo real de
llegar al objetivo.

$$
h(n) \leq h^*(n)
$$

Esto garantiza que el algoritmo A\* encontrará la ruta óptima.

------------------------------------------------------------------------

## Propiedad de consistencia

Para mejorar la eficiencia del algoritmo, la heurística también debe
cumplir la propiedad de consistencia:

$$
h(n) \leq cost(n,n') + h(n')
$$

Esto evita que el algoritmo tenga que reevaluar nodos ya explorados.

------------------------------------------------------------------------

## Estructuras de datos del algoritmo

### Open List

Contiene los nodos pendientes por explorar.

Se implementa generalmente mediante una **cola de prioridad basada en
Binary Heap**.

Complejidad:

O(log n)

### Closed List

Contiene los nodos ya explorados.

Se implementa mediante una **tabla hash**, permitiendo búsquedas
rápidas.

Complejidad:

O(1)

------------------------------------------------------------------------

## Complejidad del algoritmo A\*

La complejidad del algoritmo depende de dos factores:

-   b → factor de ramificación
-   d → profundidad de la solución

### Complejidad temporal

$$
O(b^d)
$$

### Complejidad espacial

$$
O(b^d)
$$

------------------------------------------------------------------------

## Comparación con otros algoritmos

  Algoritmo   Función          Característica
  ----------- ---------------- ----------------------
  Dijkstra    f(n)=g(n)        Solo costo recorrido
  Greedy      f(n)=h(n)        Solo estimación
  A\*         f(n)=g(n)+h(n)   Combina ambos

------------------------------------------------------------------------

# Heurísticas en Inteligencia Artificial

## ¿Qué es una heurística?

Una heurística es una técnica que permite estimar qué tan cerca se
encuentra un estado de la solución de un problema.

En lugar de explorar todas las combinaciones posibles, las heurísticas
permiten priorizar las rutas más prometedoras.

------------------------------------------------------------------------

## Tipos de heurísticas

### Distancia Manhattan

$$
h(n) = |x_1 - x_2| + |y_1 - y_2|
$$

Esta heurística es **admisible**, ya que nunca sobreestima el costo
real.

------------------------------------------------------------------------

### Distancia Euclidiana

$$
h(n) = \sqrt{(x_2-x_1)^2 + (y_2-y_1)^2}
$$

------------------------------------------------------------------------

### Distancia Chebyshev

$$
h(n) = \max(|x_1-x_2|, |y_1-y_2|)
$$

------------------------------------------------------------------------

# Ejemplo de heurística en Python

``` python
def heuristic_manhattan(a, b):
    return abs(a[0] - b[0]) + abs(a[1] - b[1])

start = (13, 27)
goal = (46, 59)

distance = heuristic_manhattan(start, goal)

print(distance)
```

------------------------------------------------------------------------

# Teoría de Juegos

## ¿Qué es la teoría de juegos?

La teoría de juegos estudia la toma de decisiones en situaciones donde
múltiples agentes interactúan entre sí.

Cada agente intenta maximizar su beneficio considerando las decisiones
de los demás.

------------------------------------------------------------------------

## Algoritmo Minimax

El algoritmo Minimax permite determinar la mejor estrategia posible en
juegos de dos jugadores.

------------------------------------------------------------------------

## Poda Alpha-Beta

La poda Alpha-Beta optimiza el algoritmo Minimax eliminando ramas
innecesarias.

------------------------------------------------------------------------

# Ejemplo 1: Robots buscando energía

``` python
decisiones = {
("Buscar energía","Buscar energía"):(2,2),
("Buscar energía","Esperar"):(5,1),
("Esperar","Buscar energía"):(1,5),
("Esperar","Esperar"):(3,3)
}

robot1 = "Buscar energía"
robot2 = "Esperar"

resultado = decisiones[(robot1,robot2)]

print("Robot1:",resultado[0])
print("Robot2:",resultado[1])
```

------------------------------------------------------------------------

# Ejemplo 2: Competencia por ancho de banda

``` python
red_game = {

("Mucho","Mucho"):(20,20),
("Mucho","Poco"):(80,10),
("Poco","Mucho"):(10,80),
("Poco","Poco"):(50,50)

}

s1,s2 = "Mucho","Mucho"

u1,u2 = red_game[(s1,s2)]

print("Servidor1:",u1)
print("Servidor2:",u2)
```

------------------------------------------------------------------------

# Ejemplo 3: Coordinación de drones

``` python
drones = {

("Patrullar juntos"):(4,4,4),
("Patrullar separados"):(6,6,6),
("Patrullar parcialmente"):(5,5,5)

}

decision = "Patrullar separados"

resultado = drones[decision]

print("Drone1:",resultado[0])
print("Drone2:",resultado[1])
print("Drone3:",resultado[2])
```

------------------------------------------------------------------------

# Conclusión

En este trabajo se estudiaron tres conceptos fundamentales de la
inteligencia artificial:

-   el algoritmo A\*
-   las heurísticas
-   la teoría de juegos


------------------------------------------------------------------------



# Bibliografía

Russell, S., & Norvig, P. (2020).  
*Artificial Intelligence: A Modern Approach*. Pearson Education.

DataCamp.  
A* Algorithm Tutorial.  
https://www.datacamp.com/es/tutorial/a-star-algorithm

The Decision Lab.  
Heuristics: Definition and Examples.  
https://thedecisionlab.com/es/biases/heuristics

PureAI.  
Strategy Understanding Guide.  
https://pureai.substack.com/p/strategy-understanding-guide
Los ejemplos implementados en Python permiten comprender cómo estos
conceptos se aplican en sistemas reales de inteligencia artificial.
