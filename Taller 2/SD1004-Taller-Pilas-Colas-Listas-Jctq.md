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

   **R/** Pila. Su regla LIFO permite retirar primero la última acción realizada mediante `pop()`, que es el comportamiento esperado al deshacer.

2. Las personas esperan su turno en una fila de atención y se atiende primero a quien llegó primero.

   **R/** Cola. Aplica la regla FIFO, donde las personas se agregan al final y se atienden desde el frente en orden de llegada.

3. Una aplicación recorre las canciones de una lista y, al terminar la última, vuelve automáticamente a la primera.

   **R/** Lista circular. El último nodo apunta al primero, lo que permite repetir el recorrido de las canciones sin reiniciar la lista manualmente.

4. Un sistema necesita recorrer una colección de registros en un único sentido y agregar elementos al comienzo con frecuencia.

   **R/** Lista simple. Cada nodo apunta al siguiente y permite insertar al comienzo actualizando la cabeza y el enlace del nuevo nodo, sin recorrer toda la lista.

5. Un reproductor permite pasar a la canción siguiente y a la anterior desde cualquier canción.

   **R/** Lista doble. Cada nodo tiene una referencia al anterior y al siguiente, lo que permite avanzar o retroceder directamente cuando existe una canción en esa dirección.

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

**R/** La pila cambia de la siguiente manera. En los diagramas, el tope está a la izquierda y la base a la derecha.

```text
Inicio:    tope → nulo (pila vacía)

push(4):  tope → [4] → nulo
push(9):  tope → [9] → [4] → nulo
push(2):  tope → [2] → [9] → [4] → nulo
pop():    tope → [9] → [4] → nulo       Devuelve: 2
push(7):  tope → [7] → [9] → [4] → nulo
peek():   tope → [7] → [9] → [4] → nulo Devuelve: 7
pop():    tope → [9] → [4] → nulo       Devuelve: 7
pop():    tope → [4] → nulo             Devuelve: 9
```

**R/** Al terminar, queda únicamente el elemento `4`, que representa tanto el tope como la base de la pila. `peek()` no modifica la estructura, mientras que `push()` y `pop()` agregan y retiran elementos desde el tope.

```text
     Tope
       ↓
    ┌─────┐
    │  4  │
    └─────┘
      Base
```

### 2.2 Casos límite

1. ¿Qué debería ocurrir si se ejecuta `pop()` sobre una pila vacía? Describe una forma de manejarlo.

   **R/** Se debe evitar retirar un elemento inexistente (desbordamiento inferior o *underflow*). Una forma de manejarlo es comprobar si la pila está vacía antes de retirar, mostrar un mensaje y devolver `nulo` sin modificarla.

2. ¿Qué debería devolver `peek()` cuando la pila está vacía? Describe una forma de manejarlo.

   **R/** Puede devolver `nulo` para indicar que no existe un elemento en el tope. Antes de consultar, se verifica si la pila está vacía y, si es necesario, se informa mediante un mensaje. Se supone que `nulo` no es un valor almacenado válido.

3. Escribe pseudocódigo para una operación `deshacer(pila)` que retire y devuelva la última acción, controlando el caso de pila vacía.

   **R/**

   ```text
   función deshacer(pila):
       si pila.estaVacia():
           imprimir "No hay acciones para deshacer"
           retornar nulo
       fin si

       retornar pila.pop()
   fin función
   ```

   Se utiliza `pop()` porque retira y devuelve la acción más reciente. La validación evita intentar retirar una acción cuando no existe ninguna.

### 2.3 Aplicación: deshacer acciones

Un usuario realiza, en este orden, las acciones `escribir`, `borrar` y `pegar`. Luego presiona “deshacer” dos veces.

- Dibuja la pila de acciones antes y después de cada deshacer.

  R/

<img width="991" height="150" alt="image" src="https://github.com/user-attachments/assets/475f8188-8e38-4b29-b7ef-3a548204715c" />


  En los tres diagramas, `escribir` permanece en la base de la pila.

- ¿Qué acción se deshace primero? Explica por qué una pila representa este comportamiento.

  R/ Se deshace primero `pegar`, ya que fue la última acción realizada. Después se deshace `borrar`. La pila es adecuada porque su regla LIFO permite retirar las acciones en el orden inverso al que fueron realizadas.

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

R/ Las operaciones modifican la cola así:

```text
Inicio: frente = final = nulo

encolar("Ana"):
frente = final → [Ana] → nulo

encolar("Luis"):
frente → [Ana] → [Luis] → nulo
                  ↑
                 final

encolar("Sol"):
frente → [Ana] → [Luis] → [Sol] → nulo
                           ↑
                          final

desencolar(): devuelve Ana
frente → [Luis] → [Sol] → nulo
                   ↑
                  final

encolar("Mia"):
frente → [Luis] → [Sol] → [Mia] → nulo
                           ↑
                          final

desencolar(): devuelve Luis
frente → [Sol] → [Mia] → nulo
                  ↑
                 final

encolar("Teo"):
frente → [Sol] → [Mia] → [Teo] → nulo
                          ↑
                         final
```

R/ Quedan esperando `Sol`, `Mia` y `Teo`, en ese orden. Sol está en el frente y será la próxima persona atendida; Teo está al final porque fue la última persona en llegar.

### 3.2 Operaciones y casos límite

1. Escribe pseudocódigo para `atender(cola)`, que retire y devuelva a la persona del frente.

   R/

   ```text
   función atender(cola):
       si cola.estaVacia():
           imprimir "No hay personas esperando"
           retornar nulo
       fin si

       retornar cola.desencolar()
   fin función
   ```

   La operación retira desde el frente para respetar el orden de llegada.

2. ¿Qué debería ocurrir si se intenta desencolar una cola vacía? Describe cómo lo manejarías.

   R/ Se debe comprobar si la cola está vacía antes de retirar un elemento. Si lo está, se devuelve `nulo` y se informa que no hay personas esperando, sin modificar las referencias de la cola.

3. Explica por qué agregar al frente y retirar desde el final no representa correctamente una fila FIFO si se mantienen esas mismas operaciones.

   R/ Si se mantienen las definiciones del taller, agregar al frente y retirar desde el final contradice el funcionamiento establecido de `encolar()` y `desencolar()`. Sin embargo, invertir ambos extremos sí puede conservar la regla FIFO: el primero que entra sigue siendo el primero que sale. Por ejemplo, si se agregan Ana y luego Luis al frente, la cola queda `[Luis, Ana]` y al retirar desde el final sale Ana primero. Por lo tanto, lo que cambia es la orientación de la cola, no necesariamente el orden de atención.

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

R/ Estado inicial: `cabeza → nulo`. Cada flecha entre nodos representa la referencia `siguiente`.

R/ 1. Insertar 18 al final.

```text
cabeza = último → [18] → nulo
```

Como la lista estaba vacía, el nuevo nodo se convierte en la cabeza y el último nodo.

R/ 2. Insertar 7 al comienzo.

```text
cabeza → [7] → [18] → nulo
                ↑
              último
```

El nodo `7` apunta a `18` y se convierte en la nueva cabeza.

R/ 3. Insertar 24 al final.

```text
cabeza → [7] → [18] → [24] → nulo
                       ↑
                     último
```

Se cambia el enlace siguiente de `18` para que apunte a `24`.

R/ 4. Insertar 13 después de 7.

```text
cabeza → [7] → [13] → [18] → [24] → nulo
                              ↑
                            último
```

El nodo `13` apunta a `18` y el nodo `7` pasa a apuntar a `13`, conservando el resto de la lista.

R/ 5. Eliminar 18.

```text
cabeza → [7] → [13] → [24] → nulo
                       ↑
                     último
```

Se modifica el enlace siguiente de `13` para que apunte directamente a `24`. El nodo `18` queda desconectado y `24` sigue apuntando a `nulo`.

### 4.2 Diseña operaciones

Escribe pseudocódigo para:

1. Recorrer la lista e imprimir todos sus datos.

   R/

   ```text
   función recorrer(cabeza):
       actual ← cabeza

       mientras actual ≠ nulo:
           imprimir actual.dato
           actual ← actual.siguiente
       fin mientras
   fin función
   ```

   Se empieza desde la cabeza y se avanza por los enlaces siguientes hasta llegar a `nulo`. Con la lista del punto 4.1, se imprime `7, 13, 24`.

2. Buscar un valor y devolver si está presente.

   R/

   ```text
   función buscar(cabeza, valor):
       actual ← cabeza

       mientras actual ≠ nulo:
           si actual.dato = valor:
               retornar verdadero
           fin si
           actual ← actual.siguiente
       fin mientras

       retornar falso
   fin función
   ```

   Se compara el valor con cada nodo hasta encontrarlo o llegar al final de la lista.

3. Insertar un nodo al comienzo, actualizando correctamente la referencia `cabeza`.

   R/

   ```text
   función insertarAlComienzo(cabeza, valor):
       nuevo ← crearNodo(valor)
       nuevo.siguiente ← cabeza
       cabeza ← nuevo

       retornar cabeza
   fin función
   ```

   La cabeza anterior se conserva como el siguiente nodo del nuevo. Se debe guardar la referencia retornada como la nueva cabeza: `cabeza ← insertarAlComienzo(cabeza, valor)`.

### 4.3 Comprueba los bordes

Explica cómo se comporta tu operación de insertar al comienzo cuando:

- La lista está vacía.

  R/ El nuevo nodo apunta a `nulo` y la cabeza pasa a referenciarlo. Este nodo queda como el primero y el último de la lista.

  ```text
  Antes:   cabeza → nulo
  Después: cabeza = último → [7] → nulo
  ```

- La lista ya tiene uno o más nodos.

  R/ El nuevo nodo apunta a la cabeza anterior y luego la cabeza se actualiza para apuntar al nuevo nodo. Los demás enlaces permanecen iguales.

  ```text
  Antes:   cabeza → [13] → [24] → nulo
                            ↑
                          último

  Después: cabeza → [7] → [13] → [24] → nulo
                                   ↑
                                 último
  ```

¿Qué referencias deben actualizarse al eliminar el primer nodo? Apóyate con un diagrama antes y después.

R/ La cabeza debe apuntar al siguiente nodo del que se elimina. Si la lista tiene un solo nodo, la cabeza pasa a ser `nulo`; si además existe una referencia al último nodo, también debe quedar en `nulo`. Si está vacía, no se realiza ninguna eliminación.

```text
Antes:
cabeza → [7] → [13] → [24] → nulo
                       ↑
                     último

Después:
cabeza → [13] → [24] → nulo
                 ↑
               último

Nodo retirado: [7] → nulo
```

El nodo `7` queda desconectado al cambiar la cabeza a `13` y limpiar el enlace del nodo retirado.

---

## Parte 5 — Listas circulares

En una lista circular simple, cada nodo tiene una referencia `siguiente`, pero el último nodo apunta de nuevo al primero. No hay un enlace final a `nulo`.

### 5.1 Reproduce un recorrido circular

Tres procesos, `P1`, `P2` y `P3`, esperan recibir turnos en una lista circular. Cada turno dura una unidad de tiempo. Se atiende un proceso por turno; al terminar su turno, si sigue activo, se pasa al siguiente. `P2` termina en el segundo turno que recibe.

1. Dibuja la lista circular inicial, incluyendo el enlace del último nodo al primero.

   R/ Se toma `P1` como el primer proceso en recibir un turno.

   ```text
   cabeza → [P1] → [P2] → [P3] ← último
              ↑             │
              └─────────────┘
   ```

   El enlace siguiente de `P3` apunta a `P1`, permitiendo que los turnos se repitan de forma circular.

2. Registra los primeros siete turnos: indica qué proceso recibe cada uno y cuál será el siguiente.

   R/ Se supone que `P1` y `P3` permanecen activos durante los siete turnos, ya que el enunciado solo indica que `P2` termina.

   | Turno | Proceso atendido | Siguiente proceso | Observación |
   |---:|---|---|---|
   | 1 | P1 | P2 | P1 continúa activo. |
   | 2 | P2 | P3 | Primer turno de P2. |
   | 3 | P3 | P1 | Se regresa al primer nodo. |
   | 4 | P1 | P2 | P1 continúa activo. |
   | 5 | P2 | P3 | Segundo turno de P2; termina y se retira. |
   | 6 | P3 | P1 | Continúa la rotación sin P2. |
   | 7 | P1 | P3 | P1 apunta directamente a P3. |

   El orden de atención es `P1, P2, P3, P1, P2, P3, P1`. Al finalizar el turno 7, el siguiente proceso será `P3`.

3. Dibuja la lista después de retirar `P2`. Verifica que el último nodo siga apuntando al primero.

   R/

   ```text
   cabeza → [P1] → [P3] ← último
              ↑      │
              └──────┘
   ```

   Al eliminar `P2`, se modifica el enlace siguiente de `P1` para que apunte directamente a `P3`. El enlace de `P3` a `P1` se mantiene, conservando la circularidad.

4. ¿Qué condición usarías para detener un recorrido de todos los nodos, dado que no se llega a `nulo`?

   R/ Guardaría la referencia al nodo inicial y detendría el recorrido cuando se vuelva a ese mismo nodo, comparando referencias y no los datos. Si la lista está vacía, no se inicia el recorrido.

   ```text
   si cabeza ≠ nulo:
       actual ← cabeza
       repetir:
           imprimir actual.dato
           actual ← actual.siguiente
       hasta que actual = cabeza
   fin si
   ```

### 5.2 Casos especiales

Explica qué enlaces se deben actualizar al eliminar un nodo en cada caso:

1. La lista está vacía.

   R/ No se modifica ningún enlace porque no existen nodos. La cabeza permanece en `nulo` y, si se guarda una referencia al último nodo, también permanece en `nulo`.

2. La lista contiene un solo nodo.

   R/ Se elimina el único nodo, que apuntaba a sí mismo. La cabeza y la referencia al último nodo (si existe) deben quedar en `nulo`, y se puede limpiar el enlace del nodo retirado.

   ```text
   Antes:
   cabeza = último → [A] ─┐
                      ↑   │
                      └───┘

   Después:
   cabeza = último = nulo
   ```

3. Se elimina el nodo que actualmente se considera primero.

   R/ Si existen dos o más nodos, la cabeza pasa al segundo nodo y el enlace siguiente del último debe apuntar a la nueva cabeza. Así se conserva el ciclo.

   ```text
   Antes:
   cabeza → [A] → [B] → [C] ← último
             ↑           │
             └───────────┘

   Después:
   cabeza → [B] → [C] ← último
             ↑     │
             └─────┘
   ```

4. Se elimina el último nodo.

   R/ Si existen dos o más nodos, se localiza el nodo anterior al último y se cambia su enlace siguiente para que apunte a la cabeza. Si se guarda una referencia al último, se actualiza para apuntar al nuevo último nodo.

   ```text
   Antes:
   cabeza → [A] → [B] → [C] ← último
             ↑           │
             └───────────┘

   Después:
   cabeza → [A] → [B] ← último
             ↑     │
             └─────┘
   ```

   En los casos anteriores, el nodo eliminado queda fuera del ciclo. Si se elimina el único nodo, se aplica el caso 2.

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

   R/ Cada flecha hacia la derecha representa `siguiente` y cada flecha hacia la izquierda representa `anterior`.

   ```text
   cabeza                                         último
     ↓                                               ↓
   [Lunes]    ⇄    [Martes]    ⇄    [Miércoles]    ⇄    [Jueves]

   Lunes.anterior   → nulo
   Jueves.siguiente → nulo
   ```

   Los campos de cada nodo quedan así:

   | Anterior | Dato | Siguiente |
   |---|---|---|
   | nulo | Lunes | Martes |
   | Lunes | Martes | Miércoles |
   | Martes | Miércoles | Jueves |
   | Miércoles | Jueves | nulo |

2. Recorre la lista desde el comienzo hasta el final y escribe el orden de los datos.

   R/ Siguiendo la referencia `siguiente` desde la cabeza:

   ```text
   Lunes → Martes → Miércoles → Jueves → nulo
   ```

3. Recorre desde el final hasta el comienzo y escribe el orden inverso.

   R/ Siguiendo la referencia `anterior` desde el último nodo:

   ```text
   Jueves → Miércoles → Martes → Lunes → nulo
   ```

### 6.2 Inserta y elimina

Parte de la lista anterior.

1. Inserta `Domingo` antes de `Lunes`.
2. Inserta `Viernes` después de `Jueves`.
3. Elimina `Miércoles`.

Dibuja el resultado después de cada operación. Para la eliminación, señala qué referencias `anterior` y `siguiente` cambian en los nodos vecinos.

R/ 1. Insertar Domingo antes de Lunes.

```text
cabeza → [Domingo] ⇄ [Lunes] ⇄ [Martes] ⇄ [Miércoles] ⇄ [Jueves] ← último
Domingo.anterior → nulo
Jueves.siguiente → nulo
```

`Domingo.siguiente` apunta a `Lunes`, `Lunes.anterior` apunta a `Domingo` y la cabeza pasa a ser `Domingo`.

R/ 2. Insertar Viernes después de Jueves.

```text
cabeza → [Domingo] ⇄ [Lunes] ⇄ [Martes] ⇄ [Miércoles] ⇄ [Jueves] ⇄ [Viernes] ← último
Domingo.anterior  → nulo
Viernes.siguiente → nulo
```

`Jueves.siguiente` apunta a `Viernes`, `Viernes.anterior` apunta a `Jueves` y el último nodo pasa a ser `Viernes`.

R/ 3. Eliminar Miércoles.

```text
cabeza → [Domingo] ⇄ [Lunes] ⇄ [Martes] ⇄ [Jueves] ⇄ [Viernes] ← último
Domingo.anterior  → nulo
Viernes.siguiente → nulo
```

Los enlaces de los nodos vecinos cambian de la siguiente manera:

| Referencia | Antes | Después |
|---|---|---|
| `Martes.siguiente` | Miércoles | Jueves |
| `Jueves.anterior` | Miércoles | Martes |

Se desconecta `Miércoles` y se pueden limpiar sus dos referencias. De esta manera, el recorrido sigue siendo posible en ambos sentidos sin pasar por el nodo eliminado.

### 6.3 Compara los enlaces

En 3–5 líneas, explica una ventaja y un costo de usar una lista doble en lugar de una lista simple. Usa el recorrido hacia atrás del ejercicio anterior en tu explicación.

R/ Una lista doble permite recorrer sus nodos en ambos sentidos.  
Por ejemplo, se puede pasar de Jueves a Miércoles directamente usando `anterior`.  
Su costo es que cada nodo necesita almacenar una referencia adicional.  
También se deben actualizar más enlaces al insertar o eliminar elementos.

---

## Parte 7 — Análisis y elección

Completa la tabla. Indica **O(1)** u **O(n)** bajo los supuestos de la columna “Representación”. Si necesitas hacer un supuesto adicional, escríbelo junto a la respuesta.

R/ La complejidad se analiza en el peor caso, suponiendo que acceder y actualizar una referencia toma tiempo constante.

| Estructura y representación | Operación | Complejidad | Justificación breve |
|---|---|---|---|
| Pila enlazada con referencia al tope | Insertar en el tope | **O(1)** | El nuevo nodo apunta al tope anterior y se actualiza el tope. |
| Pila enlazada con referencia al tope | Retirar del tope | **O(1)** | El tope pasa a apuntar al siguiente nodo, sin recorrer la pila. |
| Cola enlazada con referencias al frente y al final | Encolar al final | **O(1)** | Se accede directamente al último nodo y se actualiza el final; si está vacía, también el frente. |
| Cola enlazada con referencias al frente y al final | Desencolar del frente | **O(1)** | Se actualiza el frente y, si queda vacía, también el final. |
| Lista simple sin referencia al último nodo | Insertar al comienzo | **O(1)** | Se conecta el nuevo nodo con la cabeza y se actualiza esta referencia. |
| Lista simple sin referencia al último nodo | Insertar al final | **O(n)** | Se debe recorrer la lista desde la cabeza hasta encontrar el último nodo. |
| Lista doble con referencia a un nodo conocido | Desconectar ese nodo | **O(1)** | Se actualizan directamente los enlaces vecinos y, si corresponde, la cabeza o el último. Se supone acceso a las referencias de los extremos. |

Responde además:

1. ¿Por qué una cola enlazada que solo guarda la referencia al frente podría tardar más en encolar al final que una que también guarda la referencia al último nodo?

R/ Porque, si solo se conoce el frente, es necesario recorrer los nodos hasta encontrar el último, lo que tiene una complejidad de O(n). Si también se guarda el final, se accede directamente a él y se realiza la inserción en O(1).

2. Para una aplicación que necesita volver repetidamente al primer elemento al llegar al final, ¿qué ventaja ofrece la lista circular?

R/ Permite regresar directamente al primer nodo mediante el enlace siguiente del último. Así se continúa el recorrido de forma natural y sin tener que reiniciarlo manualmente.

3. ¿Qué información adicional almacena una lista doble frente a una simple, y qué permite hacer esa información?

R/ Almacena una referencia al nodo anterior, además de la referencia al siguiente. Esto permite avanzar y retroceder directamente, y facilita la eliminación de un nodo conocido al acceder a sus dos vecinos sin buscarlos desde la cabeza.

---

## Parte 8 — Reflexión

En un párrafo de 5 a 8 líneas, explica cómo se relacionan la forma de conectar los nodos y el orden en que se insertan o retiran datos. Menciona al menos tres de estas estructuras: pila, cola, lista simple, lista circular y lista doble.

R/ La forma de conectar los nodos influye directamente en cómo se accede a los datos y se modifican.  
En una pila, se utiliza el tope para insertar y retirar primero el último elemento agregado.  
En una cola, se agrega al final y se retira desde el frente para respetar el orden de llegada.  
La lista simple permite recorrer los nodos en un solo sentido y realizar inserciones al comienzo.  
En una lista circular, el último nodo apunta al primero y permite repetir el recorrido.  
Por su parte, la lista doble permite avanzar y retroceder gracias a sus dos referencias.  
Por eso, elegir una estructura adecuada depende de las operaciones que se necesiten realizar.

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
