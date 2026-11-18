# Taller — Complejidad algorítmica y Arreglos

**SD1004 · Estructura de Datos** — Institución Universitaria Pascual Bravo
Docente: Juan Duque · Semestre 2026-II
Cubre: Clase 2 (Big O) · Clase 3 (Arreglos 1D) · Clase 4 (Arreglos 2D)

---

## Instrucciones generales

- Responde directamente en este documento (edítalo en Word, Markdown o entrégalo en PDF).
- No necesitas escribir código en ningún lenguaje: usa pseudocódigo, dibujos o explicaciones en tus propias palabras. Lo que se evalúa es el razonamiento, no la sintaxis.
- Donde se pida un dibujo (arreglos, memoria), puedes hacerlo a mano y adjuntar una foto, o usar draw.io.
- Justifica siempre tu respuesta — una respuesta correcta sin justificación no cuenta completa.
- Fecha y forma de entrega: la indicada en el aula/repositorio del curso.

---

## Parte 1 — Complejidad algorítmica (Big O)

### 1.1 Clasifica la complejidad

Para cada situación, indica si corresponde a **O(1)**, **O(log n)**, **O(n)** o **O(n²)**, y explica por qué usando tus propias palabras (no hace falta fórmula matemática).

1. Buscar una palabra en un diccionario físico, abriendo siempre por la mitad de las páginas que quedan.

R/ O(log n): En cada paso se reduce la búsqueda a la mitad de las páginas restantes, lo que permite encontrar la palabra sin necesidad de revisar todas las páginas del diccionario.

2. Revisar, uno por uno, cada carné en una caja de carnés de estudiantes hasta encontrar el que buscas.

R/ O(n): Al revisar las carnés uno por uno, la cantidad de comparaciones tiene un aumento considerable, a la cantidad de carnés que haya en la caja en el peor de los casos.

3. Sacar la primera carta de un mazo ya barajado.

R/ O(1): Sin importar la cantidad de cartas que tenga el mazo, siempre se realiza la misma operación para sacar la primera carta.

4. Comparar cada estudiante de un salón con cada uno de los demás estudiantes, para ver si algún par cumple años el mismo día.

R/ O(n²): Por cada estudiante se debe comparar su fecha de cumpleaños con la de los demás, haciendo que la cantidad de comparaciones crezca de forma cuadrática.

5. Consultar la hora en tu reloj.

R/ O(1): Mirar la hora requiere una acción directa que no depende de la cantidad de datos ni necesita operaciones adicionales.

### 1.2 De la vida real al análisis

Piensa en una tarea cotidiana (que no sea de las ya usadas en clase) que hagas de forma **O(n)** — es decir, que si la cantidad de elementos se duplica, el tiempo que tardas también se duplica.

- Descríbela en 2-3 líneas.
- Explica qué pasaría si la "entrada" (n) se hiciera 10 veces más grande.

R/ Por ejemplo lavar los platos después de comer, por cada plato sucio debo realizar el mismo proceso de lavado, por lo que el tiempo aumenta proporcionalmente a la cantidad de platos.

¿Qué pasaría si la entrada fuera 10 veces más grande? Si la cantidad de platos aumenta 10 veces, el tiempo necesario para lavarlos también aumentaría 10 veces masomenos.

### 1.3 ¿Cuál escalar mejor?

Tienes dos formas de resolver el mismo problema:

- Forma A: O(n²)
- Forma B: O(n log n)

Para un conjunto pequeño de datos (n = 5), la Forma A es más rápida en la práctica. Aun así, ¿cuál recomendarías usar si no sabes qué tan grande será n en el futuro? Justifica tu respuesta pensando en qué pasa a medida que n crece.

R/ De sugerencia utilizar la Forma B, ya que, aunque la Forma A sea más rápida con pocos datos, la Forma B aumenta su cantidad de operaciones de manera más moderada a medida que crece la cantidad de elementos, siendo más eficiente para grandes cantidades de datos.

### 1.4 Verdadero o falso (justifica siempre)

a. Un algoritmo O(1) siempre es más rápido en segundos reales que uno O(n).

R/Falso: Big O indica cómo aumenta la cantidad de operaciones, pero no da el tiempo exacto de ejecución de un algoritmo.
b. La notación Big O describe cómo crece el tiempo de ejecución a medida que crecen los datos, no el tiempo exacto en segundos.

R/ Verdadero: Big O permite identificar cómo aumenta el costo de ejecución de un algoritmo al incrementar la cantidad de datos, sin dar su duración exacta en segundos.
c. Buscar por índice en un arreglo (`arreglo[5]`) es O(n), porque hay que recorrer los primeros 5 elementos.

R/ Falso: Es O(1)Al conocer el índice del elemento, podemos acceder directamente a su posición en el arreglo sin necesidad de recorrer los elementos anteriores.
---

## Parte 2 — Arreglos 1D

### 2.1 Diseña el arreglo

Vas a guardar las calificaciones de 6 estudiantes de un curso en un arreglo llamado `notas`.

1. Dibuja el arreglo con sus 6 casillas, mostrando el índice de cada una (recuerda: empieza en 0).

<img width="1024" height="572" alt="image" src="https://github.com/user-attachments/assets/2181880d-e945-43ec-a5b9-91b58fbcc8e7" />


2. Si `notas = [3.5, 4.2, 2.8, 5.0, 3.9, 4.5]`, ¿qué valor y qué índice tiene la tercera nota que ingresaste?

R/ Valor 2.8 en el índice 2

3. ¿Cuál es la instrucción (en pseudocódigo) para acceder directamente a la nota del último estudiante sin recorrer el arreglo?

R/ notas[5]

### 2.2 Direcciones de memoria

Supón que el arreglo `notas` del punto anterior se guarda en memoria RAM empezando en la dirección **0x2000**, y cada valor ocupa **4 bytes**.

1. Calcula la dirección de memoria de `notas[0]`, `notas[3]` y `notas[5]`, usando la fórmula:

   `dirección = base + (índice × tamaño)`

R/notas[0]	0x2000 + (0 × 4)	0x2000
notas[3]	0x2000 + (3 × 4)	0x200C
notas[5]	0x2000 + (5 × 4)	0x2014
   

2. Explica en tus palabras por qué acceder a `notas[3]` es igual de rápido que acceder a `notas[0]` — no importa cuál pidas, es O(1).

R/ Al conocer la dirección inicial, el índice y el tamaño de cada elemento, podemos calcular directamente su ubicación en memoria sin necesidad de recorrer las posiciones anteriores.


### 2.3 Búsqueda lineal vs. binaria

Tienes el arreglo ordenado `edades = [15, 18, 20, 23, 27, 31, 35, 40]`.

1. Simula paso a paso una **búsqueda lineal** para encontrar el valor `31`. ¿Cuántas comparaciones hiciste?

R/ 6 Comparaciones 

1	15	No
2	18	No
3	20	No
4	23	No
5	27	No
6	31	Encontrado

2. Simula paso a paso una **búsqueda binaria** para encontrar el mismo valor `31`. ¿Cuántas comparaciones hiciste?

R/ 2 Comparaciones

1: índice 3 valor 23, 31 es mayor, se busca a la derecha 
2: índice 5 valor 31, encontrado

3. ¿Por qué la búsqueda binaria solo funciona si el arreglo ya está ordenado?

R/ Porque necesita que los elementos estén ordenados para determinar en qué mitad se encuentra el valor buscado y descartar la otra sin revisarla.

4. Si el arreglo tuviera 1 millón de elementos, ¿cuál de las dos búsquedas seguirías usando? Justifica con lo visto sobre O(n) vs. O(log n).

R/ Búsqueda binaria — O(log n), utilizaría la búsqueda binaria, ya que reduce a la mitad los elementos restantes en cada paso, necesitando muchas menos comparaciones que la búsqueda lineal, siempre que el arreglo esté ordenado.


### 2.4 Insertar un elemento

Tienes `edades = [15, 18, 20, 23, 27]` (5 casillas, sin espacio libre).

1. ¿Qué tan costoso es insertar un nuevo valor **al final**, si hay espacio disponible? ¿Y si no hay espacio y hay que crear un arreglo más grande?

R/ Con espacio disponible O(1): Si hay espacio disponible, se inserta el elemento directamente al final.
Sin espacio disponible O(n): Si no hay espacio, se debe crear un arreglo más grande y copiar todos los elementos anteriores antes de insertar el nuevo valor.

2. ¿Qué tan costoso es insertar el valor `21` **en la mitad** (para que quede ordenado)? Explica qué hay que hacer con los demás elementos.

R7 O(n) es costoso, se deben desplazar hacia la derecha los elementos posteriores a la posición donde se insertará el valor 21, para conservar el orden del arreglo. Si no hay espacio, también será necesario crear un arreglo más grande.

3. Compara ambos casos usando notación Big O.

R/Al final con espacio	O(1)	Se inserta directamente el elemento.
Al final sin espacio	O(n)	Se deben copiar todos los elementos.
En la mitad con espacio	O(n)	Se deben desplazar los elementos posteriores.
En la mitad sin espacio	O(n)	Se debe crear otro arreglo y copiar los elementos conservando el orden.


---

## Parte 3 — Arreglos 2D

### 3.1 Diseña la matriz

Vas a guardar la disposición de un salón de clase de 3 filas x 4 columnas, donde cada casilla indica si el puesto está ocupado (`1`) o libre (`0`).

1. Dibuja la matriz `salon` con sus 3 filas y 4 columnas, con los índices `[fila][columna]` de cada casilla.

R/ <img width="990" height="548" alt="image" src="https://github.com/user-attachments/assets/fa13dbf6-fd34-48f8-aa43-a19a1dd7d3c4" />


2. Escribe (en pseudocódigo) cómo accedes al puesto de la fila 2, columna 3.

R/ puesto = salon[2][3]

3. ¿Cuántas casillas tiene en total esta matriz? ¿Cómo lo calculas en general para `filas × columnas`?

R/ Para conocer la cantidad total de casillas, se multiplica el número de filas por el número de columnas.
tiene 3x4=12 Casillas


### 3.2 De 2D a memoria (row-major)

La memoria RAM es una sola fila continua de casillas — no existen "filas y columnas" físicamente en la RAM. Por eso una matriz se guarda "aplanada", fila por fila.

Supón que `salon` (3 filas x 4 columnas) se guarda empezando en la dirección **0x1000**, con cada valor ocupando **4 bytes**, en orden por filas (row-major).

1. Dibuja cómo quedarían las 12 casillas de `salon` en una sola fila de memoria (aplanadas).

R/ <img width="988" height="92" alt="image" src="https://github.com/user-attachments/assets/f78e9f53-5b35-43cc-b800-9f9743ee902e" />


2. Calcula la dirección de memoria de la casilla `[1][2]`, usando la fórmula:

   `dirección = base + ((fila × número_de_columnas + columna) × tamaño)`

R/ 0x1000 + ((1 * 4 + 2) * 4)

0x1000 + (6*4)

0x1000 + 24

Se convierte 24 en hexadecimal: 0x18

=0x1018

3. Calcula también la dirección de `[0][0]` y de `[2][3]` (la última casilla).

R/ Casilla [0][0]:  0x1000 + ((0*4+0)*4)
0x1000

Casilla [2][3]:  0x1000 + ((2*4+3)*4)
0x1000+(11*4)
0x1000+44


### 3.3 Recorrido con ciclos anidados

Quieres contar cuántos puestos están ocupados (`1`) en toda la matriz `salon`.

1. Describe en pseudocódigo el recorrido usando dos ciclos anidados (uno para filas, otro para columnas).
2. Si la matriz tiene `f` filas y `c` columnas, ¿cuál es la complejidad de este recorrido en notación Big O? Explica por qué.
3. ¿Qué pasaría con el tiempo de ejecución si `f` y `c` se duplican ambos a la vez?

### 3.4 Conectando todo

En un párrafo corto (5-8 líneas), explica con tus propias palabras la relación entre estos tres conceptos vistos en las últimas tres clases: **Big O**, **arreglos 1D** y **arreglos 2D**. Pista: piensa en por qué entender la complejidad te ayuda a decidir cuándo usar un arreglo 1D, cuándo una matriz, y cuándo buscar de forma lineal o binaria.

---

## Rúbrica sugerida

| Criterio | Peso |
|---|---|
| Parte 1 — Complejidad algorítmica | 30% |
| Parte 2 — Arreglos 1D | 35% |
| Parte 3 — Arreglos 2D | 35% |

*Se evalúa razonamiento y justificación, no solo la respuesta final.*
