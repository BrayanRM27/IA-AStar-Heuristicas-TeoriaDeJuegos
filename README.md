# Inteligencia Artificial: Algoritmo A\*, Heurísticas y Teoría de Juegos

## Abrir Notebook en Google Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BrayanRM27/IA-AStar-Heuristicas-TeoriaDeJuegos/blob/main/CODIGOS.ipynb)


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

-   $g(n)$ → costo real desde el nodo inicial hasta el nodo actual\
-   $h(n)$ → estimación heurística desde el nodo actual hasta el
    objetivo\
-   $f(n)$ → costo total estimado

El algoritmo siempre selecciona el nodo con el menor valor de $f(n)$.

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

El algoritmo utiliza dos estructuras principales.

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

-   **b** → factor de ramificación
-   **d** → profundidad de la solución

### Complejidad temporal

$$
O(b^d)
$$

Esto significa que el tiempo de ejecución puede crecer exponencialmente
dependiendo del número de nodos generados.

### Complejidad espacial

$$
O(b^d)
$$

El algoritmo debe almacenar todos los nodos generados para garantizar
encontrar la ruta óptima.

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

Esto transforma una búsqueda exhaustiva en una **búsqueda informada**.

------------------------------------------------------------------------

## Tipos de heurísticas

### Distancia Manhattan

$$
h(n) = |x_1 - x_2| + |y_1 - y_2|
$$

La distancia Manhattan se utiliza cuando el movimiento se limita a
cuatro direcciones.

Esta heurística es **admisible**, ya que en una cuadrícula donde el
movimiento es horizontal o vertical, la distancia en forma de "L"
representa el número mínimo de pasos necesarios para llegar al objetivo.

------------------------------------------------------------------------

### Distancia Euclidiana

$$
h(n) = \sqrt{(x_2-x_1)^2 + (y_2-y_1)^2}
$$

Se utiliza cuando el movimiento puede realizarse en cualquier dirección.

------------------------------------------------------------------------

### Distancia Chebyshev

$$
h(n) = \max(|x_1-x_2|, |y_1-y_2|)
$$

Se utiliza cuando el movimiento permite diagonales.

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

## Árboles de juego

Los juegos pueden representarse mediante **árboles de decisión**, donde:

-   cada nodo representa un estado del juego
-   cada rama representa una acción posible

Los niveles del árbol alternan entre:

-   jugador MAX
-   jugador MIN

------------------------------------------------------------------------

## Algoritmo Minimax

El algoritmo Minimax permite determinar la mejor estrategia posible en
juegos de dos jugadores.

Principio:

-   MAX intenta maximizar su utilidad
-   MIN intenta minimizar la utilidad de MAX

------------------------------------------------------------------------

## Poda Alpha-Beta

La poda Alpha-Beta optimiza el algoritmo Minimax eliminando ramas que no
afectan la decisión final.

Valores utilizados:

-   α → mejor valor para MAX
-   β → mejor valor para MIN

Cuando α ≥ β se detiene la exploración de esa rama.

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

Interpretación:

Dependiendo de las decisiones tomadas por los robots, la distribución de
energía cambia. Este ejemplo ilustra cómo las decisiones de un agente
afectan el resultado del otro.

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

Interpretación:

Cuando ambos servidores intentan usar demasiado ancho de banda se
produce congestión.\
Si cooperan utilizando menos ancho de banda pueden lograr un equilibrio
beneficioso para ambos.

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

Interpretación:

Cuando los drones patrullan separados logran cubrir mayor territorio.
Esto representa un escenario de cooperación donde la estrategia
colectiva mejora el rendimiento del sistema.

------------------------------------------------------------------------

# Conclusión

En este trabajo se estudiaron tres conceptos fundamentales de la
inteligencia artificial:

-   el algoritmo A\*
-   las heurísticas
-   la teoría de juegos

El algoritmo A\* permite encontrar rutas óptimas combinando el costo
real recorrido con una estimación heurística.

Las heurísticas reducen el espacio de búsqueda y mejoran la eficiencia
de los algoritmos.

La teoría de juegos permite analizar escenarios donde múltiples agentes
toman decisiones estratégicas.

Los ejemplos implementados en Python permiten comprender de forma
práctica cómo estos conceptos se aplican en sistemas de inteligencia
artificial.
