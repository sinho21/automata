# Simulador de Autómatas Finitos Deterministas (AFD)

**Asignatura:** Estructuras Discretas
**Universidad:** _______________________________________
**Docente:** _______________________________________
**Fecha de entrega:** _______________________________________

## Integrantes

| # | Nombre completo | Código / Documento |
|---|-----------------|--------------------|
| 1 | ______________________ | ______________ |
| 2 | ______________________ | ______________ |
| 3 | ______________________ | ______________ |
| 4 | ______________________ | ______________ |

---

## 1. Descripción

Aplicación web que permite **construir, visualizar y probar** un Autómata Finito Determinista (AFD) definido formalmente por la 5-tupla

$$M = (Q, \Sigma, \delta, q_0, F)$$

El usuario introduce cada componente de la tupla; el programa valida los datos, dibuja el autómata, calcula las cinco palabras más cortas que reconoce y evalúa palabras cualquiera mostrando el recorrido estado por estado.

## 2. Tecnología utilizada

- **HTML5** para la estructura.
- **CSS3** moderno (variables, grid, flexbox, diseño tipo dashboard y adaptable a móviles).
- **JavaScript puro (ES6+)** para toda la lógica.
- **SVG nativo** generado dinámicamente para la gráfica del autómata.
- **Cero dependencias externas** y **sin librerías de autómatas**: todo el algoritmo está programado a mano.
- Se ejecuta en cualquier navegador moderno (Chrome, Edge, Firefox, Safari), **sin servidor y sin conexión a internet**.

## 3. Contenido del proyecto

| Archivo | Descripción |
|---------|-------------|
| `index.html` | Simulador completo (una sola página autocontenida). |
| `README.md` | Este documento. |
| `DIAPOSITIVAS_SUSTENTACION.md` | Estructura de 9 láminas con guion de exposición. |
| `EXPLICACION_DESDE_CERO.md` | Guía para entender el tema y el código desde cero. |

## 4. Instrucciones de uso paso a paso

1. Descomprime `Proyecto_Automatas_Finitos.zip`.
2. Haz doble clic en `index.html` (se abre en tu navegador).
3. **Prueba rápida:** en la barra lateral, pulsa **A1, A2, A3 o A4** para cargar un autómata de ejemplo con un solo clic.
4. **Para crear el tuyo (Módulo 1):**
   1. Escribe los estados `Q` separados por comas (ej. `s0, s1, s2`).
   2. Escribe el alfabeto `Σ` con símbolos de un solo carácter (ej. `a, b`).
   3. Pulsa **Aplicar Q y Σ**: aparecen los selectores de `δ`.
   4. Elige el destino de cada transición `δ(estado, símbolo)`.
   5. Elige el estado inicial `q₀`.
   6. Marca los estados finales `F` (si no marcas ninguno, se muestra una advertencia).
   7. Pulsa **Construir autómata**.
5. Cambia al **Módulo 2** para ver las 5 palabras más cortas reconocidas.
6. Cambia al **Módulo 3** para probar tus propias palabras y animar el recorrido en la gráfica.
7. Usa **Reiniciar / Nuevo autómata** para empezar de cero.

> Si entras al Módulo 2 o 3 sin haber construido un autómata, la aplicación te muestra un aviso amigable con un botón para ir al Módulo 1.

## 5. Los tres módulos

### Módulo 1 · Construir y Gráfica
Formulario guiado en el orden de la 5-tupla. Valida que `Q` tenga al menos un estado sin repetidos, que `Σ` tenga símbolos de 1 carácter sin repetidos, que todas las `|Q|×|Σ|` transiciones estén definidas y que `q₀ ∈ Q`. Muestra:

- La **5-tupla formal**.
- La **tabla de transiciones**, con `→` en el estado inicial y `*` en los finales.
- La **gráfica SVG** con: flecha entrante sin origen al estado inicial, doble círculo en finales, bucles para transiciones a sí mismo, dos flechas curvas separadas cuando hay ida y vuelta entre dos estados y etiquetas agrupadas (`a, b`) cuando varios símbolos van del mismo origen al mismo destino.

### Módulo 2 · Cinco palabras reconocidas
Lista las 5 palabras más cortas aceptadas, en **orden canónico** (longitud de 0 a 10; con igual longitud, según el orden de Σ). Empieza con `ε` si `q₀ ∈ F`. Cada palabra incluye su recorrido (`s0 -a-> s1 -b-> s2`). Si hay menos de 5 palabras o ninguna, lo explica con un mensaje claro.

### Módulo 3 · Probar palabras
Campo para probar palabras una tras otra (vacío = `ε`). Detecta símbolos fuera de Σ indicando su posición (desde 1), muestra el recorrido, el estado final y una tarjeta **verde** (aceptada) o **roja** (rechazada). **Bonificación:** el recorrido se resalta en la gráfica y puede animarse paso a paso.

## 6. Autómatas de prueba incluidos

| Autómata | Lenguaje | Primeras palabras reconocidas |
|----------|----------|-------------------------------|
| **A1** | Cantidad par de ceros, Σ = {0,1} | `ε, 1, 00, 11, 001` |
| **A2** | Terminan en `ab`, Σ = {a,b} | `ab, aab, bab, aaab, abab` |
| **A3** | Solo `ab` y `ba` (estado sumidero `m`) | `ab, ba` (solo 2) |
| **A4** | Estado final inalcanzable | ninguna (0 palabras) |

## 7. Ejemplo de salida con el autómata A2

**5-tupla:**

- Q = {s0, s1, s2}
- Σ = {a, b}
- q₀ = s0
- F = {s2}

**Tabla de transiciones:**

| Estado | a | b |
|--------|---|---|
| → s0 | s1 | s0 |
| s1 | s1 | s2 |
| →* s2 | s1 | s0 |

> En la aplicación, `s2` aparece marcado con `*` (final) y `s0` con `→` (inicial).

**Módulo 2: cinco palabras más cortas**

| # | Palabra | Recorrido |
|---|---------|-----------|
| 1 | `ab` | `s0 -a-> s1 -b-> s2` |
| 2 | `aab` | `s0 -a-> s1 -a-> s1 -b-> s2` |
| 3 | `bab` | `s0 -b-> s0 -a-> s1 -b-> s2` |
| 4 | `aaab` | `s0 -a-> s1 -a-> s1 -a-> s1 -b-> s2` |
| 5 | `abab` | `s0 -a-> s1 -b-> s2 -a-> s1 -b-> s2` |

**Módulo 3: pruebas**

| Palabra | Recorrido | Estado final | Resultado |
|---------|-----------|--------------|-----------|
| `abab` | `s0 -a-> s1 -b-> s2 -a-> s1 -b-> s2` | s2 | ✔ ACEPTADA |
| `abb` | `s0 -a-> s1 -b-> s2 -b-> s0` | s0 | ✘ RECHAZADA |
| _(vacía)_ `ε` | `s0` | s0 | ✘ RECHAZADA |
| `abc` | — | — | ⚠ Símbolo `c` en la posición 3 no pertenece a Σ |

## 8. Notas técnicas

- La búsqueda del Módulo 2 usa una tabla auxiliar (estados desde los que se llega a un final en exactamente *k* pasos) para no explorar ramas inútiles; por eso es rápida incluso con alfabetos grandes.
- El límite de longitud es 10, como pide el enunciado.
- La interfaz protege cada acción con control de errores para evitar cierres inesperados.
