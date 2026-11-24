# Explicación desde cero: Autómatas Finitos Deterministas y tu proyecto

Esta guía asume que **no sabes nada** del tema ni de programación. Léela en orden.

---

## 1. ¿Qué es un Autómata Finito Determinista (AFD)?

Es una **máquina imaginaria muy simple** que:

1. Lee una palabra **letra por letra**, de izquierda a derecha.
2. En todo momento está en **un único estado** (una "situación").
3. Al leer cada letra, **cambia de estado** siguiendo reglas fijas.
4. Cuando se acaba la palabra, mira en qué estado quedó: si es un estado "bueno" (final), dice **"ACEPTADA"**; si no, **"RECHAZADA"**.

### Ejemplos cotidianos

**El semáforo.** Estados: Verde, Amarillo, Rojo. Cada "tic" del reloj lo hace pasar al siguiente estado. Siempre sabes cuál sigue: no hay duda (eso es ser *determinista*).

**El torniquete del metro.** Estados: Cerrado y Abierto. Si metes una ficha estando Cerrado, pasa a Abierto. Si empujas estando Abierto, vuelve a Cerrado. Si empujas estando Cerrado, se queda Cerrado.

**La máquina expendedora.** Estados: "Tengo $0", "Tengo $500", "Tengo $1000". Cada moneda te cambia de estado. Si llegas a "Tengo $1000", la máquina entrega el producto (estado final).

**La palabra clave "ab".** Imagina que quieres detectar si un mensaje termina en "ab". La máquina recuerda solo lo último importante: ¿acabo de ver una "a"?, ¿acabo de ver "ab"? Eso es justo el autómata A2 de tu proyecto.

### ¿Por qué "finito"?
Porque tiene una cantidad **limitada** de estados. No tiene memoria infinita: solo "recuerda" en qué estado está.

### ¿Por qué "determinista"?
Porque, estando en un estado y leyendo un símbolo, **solo hay una opción** de a dónde ir. Nunca hay dos caminos posibles ni ninguno.

---

## 2. La 5-tupla M = (Q, Σ, δ, q₀, F), letra por letra

Una "tupla" es una lista ordenada. La definición formal de un AFD es una lista de 5 cosas:

| Letra | Se lee | Qué es | Ejemplo con A2 |
|-------|--------|--------|----------------|
| **Q** | "Q" | El conjunto de **todos los estados** | {s0, s1, s2} |
| **Σ** | "sigma" | El **alfabeto**: los símbolos permitidos | {a, b} |
| **δ** | "delta" | La **función de transición**: dice a qué estado se va desde cada estado leyendo cada símbolo | δ(s0, a) = s1 |
| **q₀** | "q cero" | El **estado inicial** (donde empieza siempre) | s0 |
| **F** | "F" | El conjunto de **estados finales** (los de aceptación) | {s2} |

### Más sobre δ
Si hay 3 estados y 2 símbolos, hay 3 × 2 = **6 transiciones**, y las 6 deben estar definidas. Por eso el simulador genera exactamente |Q|×|Σ| selectores. La tabla de A2:

| Estado | a | b |
|--------|---|---|
| → s0 | s1 | s0 |
| s1 | s1 | s2 |
| →* s2 | s1 | s0 |

(→ marca el estado inicial; * marca los finales.)

### Cómo se dibuja
- **Círculo** = estado.
- **Doble círculo** = estado final.
- **Flecha que llega de la nada** = estado inicial.
- **Flecha entre círculos** con una letra = transición.
- **Bucle** (flecha que sale y vuelve al mismo estado) = al leer esa letra, te quedas donde estabas.

### Ejemplo completo: ¿"aab" es aceptada por A2?
Empiezo en s0. Leo **a** → voy a s1. Leo **a** → sigo en s1. Leo **b** → voy a s2. Se acabó la palabra y estoy en s2, que está en F. **ACEPTADA.**
Se escribe: `s0 -a-> s1 -a-> s1 -b-> s2`.

---

## 3. ¿Qué es ε (épsilon)?

**ε es la palabra vacía**: una palabra con **cero letras**. Es como un mensaje en blanco.

- No es un símbolo del alfabeto; es "no escribir nada".
- Al leer ε no se hace ningún movimiento: el autómata se queda en q₀.
- Por eso **ε se acepta si y solo si q₀ está en F**.
- En el Módulo 3, dejar el campo vacío significa probar ε.

Ejemplo: en A1 (cantidad par de ceros) el estado inicial q0 también es final, porque "cero ceros" es una cantidad par. Entonces ε es aceptada y es la primera palabra de la lista.

---

## 4. El orden canónico

Para listar palabras "de forma justa" ordenamos así:

1. **Primero por longitud:** primero las de 0 letras, luego las de 1, luego 2, etc.
2. **Con igual longitud, por el orden del alfabeto** tal como lo escribió el usuario (como un diccionario).

Con Σ = {a, b}, el orden canónico es:

`ε, a, b, aa, ab, ba, bb, aaa, aab, aba, abb, baa, bab, bba, bbb, ...`

Para A2 filtramos las que son aceptadas (terminan en ab): `ab, aab, bab, aaab, abab`. Esas son las 5 más cortas **en ese orden**.

Fíjate: "bab" va antes que "aaab" porque tiene 3 letras y "aaab" tiene 4. Y "aab" va antes que "bab" porque, con la misma longitud, la "a" va antes que la "b" en Σ = {a, b}.

---

## 5. Explicación bloque por bloque de `index.html`

Un archivo `.html` es una página web. Tiene tres tipos de contenido: **HTML** (qué elementos hay), **CSS** (cómo se ven) y **JavaScript** (qué hacen).

### Bloque A · `<head>` y `<style>` (CSS)
- Define los colores en **variables** (`--brand`, `--ok`, `--bad`...). Cambiar un color ahí lo cambia en toda la página.
- Define el **diseño**: barra lateral oscura a la izquierda, contenido a la derecha, tarjetas blancas con sombra.
- Define la apariencia de la gráfica: líneas grises (`.edge`), líneas naranja cuando se resalta el recorrido (`.edge.hl`), estados (`.node`), doble círculo (`.inner`).
- La parte `@media (max-width:860px)` hace que en pantallas pequeñas la barra lateral pase arriba (diseño adaptable al celular).

### Bloque B · `<body>`: la estructura HTML
- `<aside class="side">`: barra lateral con navegación (Módulos 1, 2, 3), botones de **Carga rápida** A1 a A4, el estado actual y el botón de **Reiniciar**.
- `<section id="m1">`: Módulo 1 con los 5 pasos del formulario y la zona de resultados `out1`.
- `<section id="m2">`: Módulo 2, que se rellena desde JavaScript.
- `<section id="m3">`: Módulo 3 con el campo de palabra, el resultado, la gráfica con botones de animación y el historial.
- `<div id="toast">`: el mensajito flotante que dice "Autómata construido".

### Bloque C · `<script>`: la lógica pura
Esta parte está marcada con `LÓGICA PURA` y **no toca la pantalla**, solo hace cálculos. Sus piezas:

1. **`parseStates` y `parseAlphabet`**: leen el texto del usuario ("q0, q1, q2"), lo separan por comas, quitan espacios y revisan errores: texto vacío, elementos vacíos, repetidos y, en el alfabeto, símbolos de más de un carácter o el reservado ε.
2. **`makeAutomaton`**: arma el objeto autómata `{Q, S, delta, q0, F}`. `delta` es un diccionario doble: `delta[estado][símbolo]` da el estado siguiente.
3. **`PRESETS`**: las definiciones de A1, A2, A3 y A4, para la carga rápida.
4. **`runWord`**: simula el autómata. Empieza en q₀ y, por cada letra, avanza con `delta`. Guarda el camino recorrido y dice si el último estado está en F.
5. **`checkWord`**: antes de simular revisa que todos los símbolos pertenezcan a Σ y anota la **posición (desde 1)** de los que no. Si el usuario deja el campo vacío o escribe ε, evalúa la palabra vacía.
6. **`formatPath`**: convierte el camino en texto: `s0 -a-> s1 -b-> s2`.
7. **`shortestWords`**: encuentra las 5 palabras más cortas en orden canónico. Truco: primero construye `reach[k]` = los estados desde los cuales, leyendo exactamente k símbolos, se llega a un final. Luego, para cada longitud L = 0, 1, ..., 10, hace una búsqueda en profundidad recorriendo Σ **en su orden**, y solo avanza por transiciones que cumplan `reach`. Así no pierde tiempo en caminos que no llegan a un final y las palabras salen ya ordenadas.
8. **`buildSvg`**: dibuja la gráfica. Coloca los estados en círculo, **agrupa** las transiciones con mismo origen y destino (para escribir `a, b`), dibuja **bucles** con curvas de Bézier cúbicas, dibuja **dos curvas separadas** cuando hay ida y vuelta (curvas cuadráticas hacia lados opuestos), añade la **flecha de entrada** al estado inicial y el **doble círculo** a los finales.

### Bloque D · `<script>`: la interfaz
- **`form`**: guarda lo que el usuario ha elegido (destinos de δ, q₀, F) para no perderlo si cambia Q o Σ.
- **`applyQS`**: valida Q y Σ y genera los selectores de δ, el selector de q₀ y las casillas de F.
- **`doBuild`**: revisa que todas las transiciones y q₀ estén definidos, y construye el autómata. Si falta algo, muestra los errores en rojo, nunca se cae.
- **`renderOut1`**: muestra la 5-tupla, la tabla y la gráfica.
- **`renderM2`**: muestra las palabras del Módulo 2 (o el mensaje de 0 o menos de 5 palabras).
- **`evaluate`**: lee la palabra del Módulo 3, la comprueba y pinta la tarjeta verde, roja o amarilla (símbolo inválido).
- **`drawGraph3`, `playAnim`, `showStep`**: resaltan el recorrido y lo animan un paso por segundo.
- **`loadPreset` y `resetAll`**: carga rápida de A1-A4 y reinicio.
- **`safe(...)`**: envuelve cada acción en un `try/catch`; si algo inesperado pasa, muestra un aviso en vez de congelar la página.
- **`init()`**: conecta los botones con sus funciones.

---

## 6. Seis preguntas difíciles del profesor (con respuesta)

### 1) "¿Por qué su autómata es determinista? ¿Qué cambiaría si fuera no determinista?"
**Respuesta:** Es determinista porque δ es una **función total** de Q × Σ en Q: para cada pareja (estado, símbolo) hay **exactamente un** estado destino. Nuestro formulario obliga a elegir un destino para todas las |Q|×|Σ| parejas, así que no puede haber ninguna indefinida ni dos opciones. En un autómata no determinista (AFN), δ devolvería un *conjunto* de estados (posiblemente vacío) y una palabra se acepta si **existe algún camino** que llegue a un final. Se podría simular, pero habría que seguir varios caminos a la vez o convertirlo a AFD con la construcción de subconjuntos.

### 2) "¿Cómo garantizan el orden canónico sin generar todas las palabras?"
**Respuesta:** Recorremos las longitudes en orden creciente (0, 1, 2, ..., 10) y, dentro de cada longitud, hacemos una búsqueda en profundidad que prueba los símbolos **en el orden de Σ**. Eso produce las palabras de cada longitud en orden de diccionario, que es el orden canónico. Para no explorar todo (con 2 símbolos y longitud 10 hay 1024 palabras, y con alfabetos grandes muchísimas más) precalculamos `reach[k]`, la tabla de estados desde los que se llega a un final en exactamente k pasos, y solo avanzamos por transiciones que llevan a un estado de esa tabla. Así cada rama explorada termina en una palabra aceptada y paramos al reunir 5.

### 3) "¿Qué es el estado sumidero y por qué lo necesita A3?"
**Respuesta:** Es un estado **trampa**: una vez que se entra, todas las transiciones vuelven a él y nunca se llega a un final. A3 solo acepta `ab` y `ba`. Como un AFD **debe** tener una transición para cada símbolo en cada estado, ¿qué pasa si después de `a` llega otra `a`? No hay un camino "natural", así que mandamos esa palabra al sumidero `m` y queda rechazada para siempre. El sumidero completa la función δ sin aceptar nada nuevo.

### 4) "¿Por qué limitan la búsqueda a longitud 10? ¿Y si el lenguaje es infinito o vacío?"
**Respuesta:** Es el tope que pide el enunciado y garantiza que el programa **siempre termine**. Si el lenguaje es infinito (como "terminan en ab") siempre hay palabras cortas y las encontramos. Si es vacío no podemos concluir nada con la sola búsqueda, así que además comprobamos la **alcanzabilidad**: recorremos el grafo desde q₀ y vemos si algún final es alcanzable. En A4 ningún final es alcanzable, entonces afirmamos con certeza que L(M) = ∅. Si algún final sí es alcanzable pero a más de 10 símbolos, lo decimos con un mensaje distinto.

### 5) "¿Cómo dibujan las flechas curvas, los bucles y las etiquetas agrupadas?"
**Respuesta:** Todo se calcula en JavaScript y se escribe como texto SVG. Los estados se colocan sobre una circunferencia. Primero **agrupamos** las transiciones por pareja (origen, destino) y unimos los símbolos con coma. Un **bucle** es una curva de Bézier cúbica que sale y regresa al mismo círculo hacia afuera de la circunferencia. Si existen A→B **y** B→A, usamos una curva cuadrática para cada una con el punto de control desplazado a lados opuestos de la recta que une los estados, así no se superponen. Si solo hay una dirección, se dibuja una línea recta. La flecha de entrada al estado inicial es un segmento corto sin círculo de origen. Los finales llevan un segundo círculo interior.

### 6) "¿Cómo comprobaron que el programa es correcto y qué tan eficiente es?"
**Respuesta:** Con los cuatro autómatas de prueba, cuyos resultados conocemos de antemano: A1 debe dar `ε, 1, 00, 11, 001`; A2 `ab, aab, bab, aaab, abab`; A3 solo `ab, ba`; y A4 ninguna. También probamos casos límite: F vacío, un solo estado, símbolos fuera de Σ, palabra vacía, nombres repetidos. En eficiencia, evaluar una palabra de longitud n cuesta O(n), porque es un paso por símbolo. La búsqueda de las 5 palabras cuesta O(L·|Q|·|Σ|) para construir la tabla `reach` y luego una cantidad proporcional a (número de palabras × longitud × |Σ|) para extraerlas, muy pequeña frente a recorrer todas las palabras.
