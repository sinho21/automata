# Presentación de sustentación: Simulador de AFD (9 láminas)

> Duración sugerida: 10 a 12 minutos. Cada lámina trae: **Título**, **puntos clave** (lo que va escrito), **captura sugerida** y **guion exacto** (lo que se dice).
> Consejo: practica con el simulador abierto en A2 para poder cambiar de pantalla sin perder el hilo.

---

## Lámina 1 · Portada

**Título:** Simulador de Autómatas Finitos Deterministas (AFD)

**Puntos clave en la lámina:**
- Estructuras Discretas
- Integrantes: ______________________
- Docente y fecha

**Captura sugerida:** Pantalla completa del simulador con el autómata A2 cargado (barra lateral + gráfica).

**Guion exacto:**
"Buenos días, profesor. Somos [nombres de los integrantes] y hoy les presentamos nuestro proyecto de Estructuras Discretas: un Simulador de Autómatas Finitos Deterministas. Es una aplicación web que permite construir un autómata, ver su gráfica, descubrir qué palabras reconoce y probar palabras una por una. Todo está programado por nosotros desde cero, sin ninguna librería de autómatas."

---

## Lámina 2 · Objetivo y alcance

**Título:** ¿Qué problema resolvemos?

**Puntos clave:**
- Construir un AFD a partir de su definición formal
- Visualizarlo como grafo dirigido
- Obtener las 5 palabras más cortas que reconoce
- Verificar si una palabra es aceptada o rechazada

**Captura sugerida:** Barra lateral mostrando los tres módulos y los botones A1 a A4.

**Guion exacto:**
"El objetivo del proyecto es pasar de la teoría a la práctica. En clase vemos los autómatas como una definición matemática y como dibujos; nuestro simulador une las dos cosas. El usuario escribe la definición formal y el programa la valida, la dibuja, calcula las palabras más cortas del lenguaje y evalúa cualquier palabra. Está organizado en tres módulos: construir, listar palabras y probar palabras."

---

## Lámina 3 · Fundamento teórico

**Título:** La 5-tupla M = (Q, Σ, δ, q₀, F)

**Puntos clave:**
- Q: conjunto finito de estados
- Σ: alfabeto (símbolos)
- δ: Q × Σ → Q (función de transición total)
- q₀ ∈ Q: estado inicial
- F ⊆ Q: estados finales
- Determinista: exactamente un destino por (estado, símbolo)

**Captura sugerida:** Tarjeta "5-tupla formal" del Módulo 1 con A2 (Q = {s0, s1, s2}, Σ = {a, b}, q₀ = s0, F = {s2}).

**Guion exacto:**
"Un AFD se define con cinco elementos. Q es el conjunto finito de estados. Sigma es el alfabeto, o sea los símbolos que se pueden leer. Delta es la función de transición, que dice a qué estado se pasa desde cada estado al leer cada símbolo; es total, así que está definida para todas las parejas. q cero es el estado inicial y F es el conjunto de estados finales. Se llama determinista porque, para cada estado y cada símbolo, existe exactamente un estado siguiente: nunca hay dos opciones ni ninguna. Una palabra se acepta si, al leerla completa desde q cero, terminamos en un estado de F."

---

## Lámina 4 · Tecnología y arquitectura

**Título:** Una sola página, cero dependencias

**Puntos clave:**
- HTML5 + CSS3 + JavaScript puro (ES6+)
- Gráficos SVG generados dinámicamente
- Sin librerías externas ni de autómatas
- Se ejecuta con doble clic, sin internet
- Lógica separada de la interfaz

**Captura sugerida:** Esquema simple de 3 bloques: Lógica pura (validación, ejecución, búsqueda, SVG) → Interfaz (formularios y módulos) → Navegador.

**Guion exacto:**
"Decidimos hacer una sola página autocontenida: HTML5 para la estructura, CSS3 para el diseño tipo dashboard y JavaScript puro para la lógica. La gráfica no es una imagen ni usa una librería: la generamos como SVG, calculando nosotros las posiciones de los estados y las curvas de las flechas. Separamos la lógica pura, que valida datos, ejecuta palabras y busca las palabras más cortas, de la interfaz. Gracias a eso el programa abre con doble clic en cualquier navegador y funciona sin internet."

---

## Lámina 5 · Módulo 1: Construir y graficar

**Título:** Del formulario a la gráfica

**Puntos clave:**
- Formulario en el orden de la 5-tupla
- δ generada dinámicamente: |Q|×|Σ| selectores
- Validación completa (vacíos, repetidos, símbolos de 1 carácter)
- Advertencia si F = ∅
- Tabla con → inicial y * finales
- Gráfica con las 5 reglas visuales

**Captura sugerida:** Pantalla con los selectores δ(estado, símbolo) y debajo la gráfica de A2.

**Guion exacto:**
"En el Módulo 1 el usuario sigue el orden de la tupla. Escribe los estados y el alfabeto; el sistema revisa que no haya vacíos ni repetidos y que cada símbolo tenga un solo carácter. Luego genera automáticamente un selector por cada pareja estado-símbolo, así que si hay tres estados y dos símbolos aparecen seis selectores. Después se elige el estado inicial y los finales; si no se marca ninguno, avisamos que el autómata no aceptará nada. Al construir, mostramos la tupla, la tabla de transiciones y la gráfica. En la gráfica el estado inicial tiene una flecha que llega sin origen, los finales tienen doble círculo, las transiciones a sí mismo son bucles, si hay ida y vuelta entre dos estados dibujamos dos curvas separadas, y si varios símbolos van del mismo origen al mismo destino los agrupamos en una sola flecha con la etiqueta 'a, b'."

---

## Lámina 6 · Módulo 2: Palabras reconocidas y orden canónico

**Título:** Las cinco palabras más cortas

**Puntos clave:**
- Orden canónico: primero longitud, luego el orden de Σ
- Longitudes de 0 a 10
- ε aparece primero si q₀ ∈ F
- Recorrido paso a paso de cada palabra
- Casos: menos de 5 palabras, o ninguna

**Captura sugerida:** Módulo 2 con A2: ab, aab, bab, aaab, abab y sus recorridos.

**Guion exacto:**
"El Módulo 2 responde a la pregunta: ¿qué palabras acepta este autómata? Mostramos las cinco más cortas en orden canónico, es decir, primero las de menor longitud y, entre las de igual longitud, según el orden en que se escribió el alfabeto. Si el estado inicial es final, la primera palabra es epsilon, la palabra vacía. Con A2 obtenemos ab, aab, bab, aaab y abab, cada una con su recorrido, por ejemplo s0 con a a s1 con b a s2. No generamos todas las palabras posibles, porque serían demasiadas: usamos una tabla que nos dice desde qué estados se puede llegar a un final en exactamente k pasos, y así solo exploramos caminos que sí terminan aceptando. Si hay menos de cinco palabras, como en A3 que solo acepta ab y ba, lo informamos; y si no hay ninguna, como en A4, explicamos por qué."

---

## Lámina 7 · Módulo 3: Probar palabras y animación

**Título:** ¿Acepta o rechaza?

**Puntos clave:**
- Palabra vacía = ε
- Detecta símbolos fuera de Σ con su posición (desde 1)
- Recorrido, estado final y tarjeta verde o roja
- Bonificación: recorrido resaltado en la gráfica
- Animación paso a paso

**Captura sugerida:** Módulo 3 con la palabra `abb` rechazada (tarjeta roja) y el recorrido resaltado en naranja; otra captura con `abab` aceptada (verde).

**Guion exacto:**
"En el Módulo 3 se pueden probar palabras una tras otra. Si el campo está vacío se evalúa epsilon. Si la palabra tiene un símbolo que no pertenece al alfabeto, no la procesamos: indicamos qué símbolo es y en qué posición está, contando desde uno. Si es válida, mostramos el recorrido completo, el estado final y una tarjeta verde si se acepta o roja si se rechaza. Como bonificación, el recorrido queda resaltado en la gráfica y hay un botón que lo anima paso a paso: se ve cómo el autómata va pasando de un estado a otro leyendo cada símbolo, y al final el último estado se pinta de verde o de rojo."

---

## Lámina 8 · Validación con los autómatas A1 a A4

**Título:** Pruebas de corrección

**Puntos clave:**
- A1 (cantidad par de ceros): ε, 1, 00, 11, 001
- A2 (terminan en ab): ab, aab, bab, aaab, abab
- A3 (solo ab y ba, sumidero m): ab, ba
- A4 (final inalcanzable): ninguna palabra
- Carga con un clic desde la barra lateral

**Captura sugerida:** Cuatro miniaturas del Módulo 2, una por cada autómata.

**Guion exacto:**
"Para validar el programa usamos cuatro autómatas. A1 acepta las palabras con cantidad par de ceros y el simulador entrega epsilon, 1, 00, 11 y 001, justo en orden canónico. A2 acepta las palabras que terminan en ab y entrega ab, aab, bab, aaab y abab. A3 solo acepta ab y ba; tiene un estado sumidero llamado m, que es una trampa de la que no se puede salir, y por eso el Módulo 2 muestra solo dos palabras. A4 tiene un estado final que nunca se alcanza desde el inicial, así que el lenguaje es vacío y el programa lo explica. Los cuatro se cargan con un clic desde la barra lateral."

---

## Lámina 9 · Conclusiones y preguntas

**Título:** Conclusiones

**Puntos clave:**
- La teoría de AFD se puede implementar y visualizar
- Validación robusta: sin errores ni cierres inesperados
- Orden canónico con búsqueda eficiente
- Mejoras futuras: minimización de AFD, AFN, exportar la gráfica
- ¿Preguntas?

**Captura sugerida:** Imagen del simulador con A1 y el mensaje "Gracias".

**Guion exacto:**
"Para concluir: logramos convertir la definición matemática de un autómata finito determinista en una herramienta interactiva que valida, dibuja, lista y evalúa. Aprendimos que la función de transición total es lo que garantiza el determinismo y que un estado sumidero sirve para completar autómatas que, de otra forma, no estarían definidos para todos los símbolos. Como mejoras futuras se podrían agregar la minimización de autómatas, los autómatas no deterministas y la exportación de la gráfica. Muchas gracias por su atención; con gusto respondemos sus preguntas."
