# Taller — Pilas, colas y listas enlazadas

**SD1004 · Estructura de Datos** — Institución Universitaria Pascual Bravo  
Docente: Juan Duque · Semestre 2026-II  
**Fecha límite de entrega: domingo 11 de octubre de 2026**

## Propósito

Representar y resolver operaciones básicas con pilas, colas, listas enlazadas simples, circulares y dobles. En cada ejercicio explica cómo cambia la estructura y justifica por qué esa estructura es adecuada para el caso.

## Instrucciones generales

- Responde en este documento o en un archivo aparte de Word, Markdown o PDF.
- No necesitas programar en un lenguaje específico. Usa pseudocódigo, diagramas y explicaciones con tus propias palabras.
- En los diagramas, identifica el inicio y el final de cada estructura, los enlaces entre nodos y, cuando aplique, el tope, el frente y el final.
- Justifica tus respuestas. Una respuesta final sin mostrar el razonamiento no obtiene el puntaje completo.
- Si dibujas a mano, toma una foto legible e inclúyela en la entrega.
- Fecha y plataforma de entrega: domingo 11 de octubre de 2026, por el medio indicado en el aula del curso.

---

## Parte 1 — Reconocer la estructura adecuada

Para cada situación, selecciona una estructura entre **pila**, **cola**, **lista simple**, **lista circular** y **lista doble**. Explica qué operación o propiedad de la estructura hace que sea adecuada.

1. Un editor de texto guarda las acciones recientes para permitir deshacer primero la última acción realizada.
2. Las personas esperan su turno en una fila de atención y se atiende primero a quien llegó primero.
3. Una aplicación recorre las canciones de una lista y, al terminar la última, vuelve automáticamente a la primera.
4. Un sistema necesita recorrer una colección de registros en un único sentido y agregar elementos al comienzo con frecuencia.
5. Un reproductor permite pasar a la canción siguiente y a la anterior desde cualquier canción.

---

## Parte 2 — Pilas (LIFO)

Una pila sigue la regla **último en entrar, primero en salir**. Considera que `push(x)` agrega `x` al tope, `pop()` retira y devuelve el elemento del tope, y `peek()` consulta el tope sin retirarlo.

### 2.1 Sigue las operaciones

La pila inicia vacía. Ejecuta las operaciones en orden y dibuja el contenido después de cada una. Indica el resultado de cada `pop()` y de cada `peek()`.

```text
push(4)
push(9)
push(2)
pop()
push(7)
peek()
pop()
pop()
```

Al terminar, indica qué elemento queda en la pila y cuál es el tope. Usa un dibujo que deje claro cuál extremo corresponde al tope.

### 2.2 Casos límite

1. ¿Qué debería ocurrir si se ejecuta `pop()` sobre una pila vacía? Describe una forma de manejarlo.
2. ¿Qué debería devolver `peek()` cuando la pila está vacía? Describe una forma de manejarlo.
3. Escribe pseudocódigo para una operación `deshacer(pila)` que retire y devuelva la última acción, controlando el caso de pila vacía.

### 2.3 Aplicación: deshacer acciones

Un usuario realiza, en este orden, las acciones `escribir`, `borrar` y `pegar`. Luego presiona “deshacer” dos veces.

- Dibuja la pila de acciones antes y después de cada deshacer.
- ¿Qué acción se deshace primero? Explica por qué una pila representa este comportamiento.

---

## Parte 3 — Colas (FIFO)

Una cola sigue la regla **primero en entrar, primero en salir**. En esta actividad, `encolar(x)` agrega al final y `desencolar()` retira desde el frente.

### 3.1 Simula la fila de atención

La cola empieza vacía. Ejecuta las operaciones en orden y dibuja la cola después de cada operación, marcando **frente** y **final**. Anota qué persona devuelve cada `desencolar()`.

```text
encolar("Ana")
encolar("Luis")
encolar("Sol")
desencolar()
encolar("Mia")
desencolar()
encolar("Teo")
```

¿Qué personas quedan esperando y en qué orden?

### 3.2 Operaciones y casos límite

1. Escribe pseudocódigo para `atender(cola)`, que retire y devuelva a la persona del frente.
2. ¿Qué debería ocurrir si se intenta desencolar una cola vacía? Describe cómo lo manejarías.
3. Explica por qué agregar al frente y retirar desde el final no representa correctamente una fila FIFO si se mantienen esas mismas operaciones.

---

## Parte 4 — Listas enlazadas simples

En una lista simple, cada nodo guarda un dato y una referencia `siguiente`. El último nodo apunta a `nulo`.

### 4.1 Construye y modifica una lista

Parte de la lista vacía y aplica en orden estas operaciones:

1. Insertar `18` al final.
2. Insertar `7` al comienzo.
3. Insertar `24` al final.
4. Insertar `13` después del nodo que contiene `7`.
5. Eliminar el nodo que contiene `18`.

Dibuja la lista después de cada operación. En el último dibujo, muestra explícitamente que el nodo final apunta a `nulo`.

### 4.2 Diseña operaciones

Escribe pseudocódigo para:

1. Recorrer la lista e imprimir todos sus datos.
2. Buscar un valor y devolver si está presente.
3. Insertar un nodo al comienzo, actualizando correctamente la referencia `cabeza`.

### 4.3 Comprueba los bordes

Explica cómo se comporta tu operación de insertar al comienzo cuando:

- La lista está vacía.
- La lista ya tiene uno o más nodos.

¿Qué referencias deben actualizarse al eliminar el primer nodo? Apóyate con un diagrama antes y después.

---

## Parte 5 — Listas circulares

En una lista circular simple, cada nodo tiene una referencia `siguiente`, pero el último nodo apunta de nuevo al primero. No hay un enlace final a `nulo`.

### 5.1 Reproduce un recorrido circular

Tres procesos, `P1`, `P2` y `P3`, esperan recibir turnos en una lista circular. Cada turno dura una unidad de tiempo. Se atiende un proceso por turno; al terminar su turno, si sigue activo, se pasa al siguiente. `P2` termina en el segundo turno que recibe.

1. Dibuja la lista circular inicial, incluyendo el enlace del último nodo al primero.
2. Registra los primeros siete turnos: indica qué proceso recibe cada uno y cuál será el siguiente.
3. Dibuja la lista después de retirar `P2`. Verifica que el último nodo siga apuntando al primero.
4. ¿Qué condición usarías para detener un recorrido de todos los nodos, dado que no se llega a `nulo`?

### 5.2 Casos especiales

Explica qué enlaces se deben actualizar al eliminar un nodo en cada caso:

1. La lista está vacía.
2. La lista contiene un solo nodo.
3. Se elimina el nodo que actualmente se considera primero.
4. Se elimina el último nodo.

Incluye un pequeño diagrama para los casos de un nodo y de dos o más nodos.

---

## Parte 6 — Listas doblemente enlazadas

En una lista doble, cada nodo tiene referencias `anterior` y `siguiente`. El primer nodo no tiene anterior (`nulo`) y el último no tiene siguiente (`nulo`).

### 6.1 Recorrido en ambos sentidos

Construye esta lista:

```text
Lunes ⇄ Martes ⇄ Miércoles ⇄ Jueves
```

1. Dibuja cada nodo con su dato, su enlace `anterior` y su enlace `siguiente`.
2. Recorre la lista desde el comienzo hasta el final y escribe el orden de los datos.
3. Recorre desde el final hasta el comienzo y escribe el orden inverso.

### 6.2 Inserta y elimina

Parte de la lista anterior.

1. Inserta `Domingo` antes de `Lunes`.
2. Inserta `Viernes` después de `Jueves`.
3. Elimina `Miércoles`.

Dibuja el resultado después de cada operación. Para la eliminación, señala qué referencias `anterior` y `siguiente` cambian en los nodos vecinos.

### 6.3 Compara los enlaces

En 3–5 líneas, explica una ventaja y un costo de usar una lista doble en lugar de una lista simple. Usa el recorrido hacia atrás del ejercicio anterior en tu explicación.

---

## Parte 7 — Análisis y elección

Completa la tabla. Indica **O(1)** u **O(n)** bajo los supuestos de la columna “Representación”. Si necesitas hacer un supuesto adicional, escríbelo junto a la respuesta.

| Estructura y representación | Operación | Complejidad | Justificación breve |
|---|---|---|---|
| Pila enlazada con referencia al tope | Insertar en el tope |  |  |
| Pila enlazada con referencia al tope | Retirar del tope |  |  |
| Cola enlazada con referencias al frente y al final | Encolar al final |  |  |
| Cola enlazada con referencias al frente y al final | Desencolar del frente |  |  |
| Lista simple sin referencia al último nodo | Insertar al comienzo |  |  |
| Lista simple sin referencia al último nodo | Insertar al final |  |  |
| Lista doble con referencia a un nodo conocido | Desconectar ese nodo |  |  |

Responde además:

1. ¿Por qué una cola enlazada que solo guarda la referencia al frente podría tardar más en encolar al final que una que también guarda la referencia al último nodo?
2. Para una aplicación que necesita volver repetidamente al primer elemento al llegar al final, ¿qué ventaja ofrece la lista circular?
3. ¿Qué información adicional almacena una lista doble frente a una simple, y qué permite hacer esa información?

---

## Parte 8 — Reflexión

En un párrafo de 5 a 8 líneas, explica cómo se relacionan la forma de conectar los nodos y el orden en que se insertan o retiran datos. Menciona al menos tres de estas estructuras: pila, cola, lista simple, lista circular y lista doble.

---

## Criterios de evaluación

| Criterio | Peso |
|---|---:|
| Comprensión de las reglas de cada estructura | 20% |
| Trazas y diagramas correctos, con referencias identificadas | 25% |
| Pseudocódigo y actualización de enlaces | 25% |
| Manejo de casos límite y análisis de complejidad | 20% |
| Claridad, orden y explicación propia | 10% |

*Se evalúa el razonamiento y la justificación, además de los resultados.*
