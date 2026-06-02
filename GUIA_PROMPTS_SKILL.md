# Guía exhaustiva: cómo exprimir una *skill-libro* en Claude Code

> Plantilla de *prompts* (instrucciones) reutilizable para cualquier libro que hayas convertido en skill con `book-to-skill`.
> Pensada para tu ecosistema de inversión y educación financiera.

---

## 0. Antes de empezar: las 3 reglas del juego

Piensa en tu skill-libro como **un becario superdotado que se ha leído el libro entero, lo tiene subrayado y con post-its en cada capítulo**. Tú no le pides que "te lo cuente": lo *interrogas* como a un colega que acaba de cerrar el libro.

**Regla 1 — El prefijo corto es su nombre.** A lo largo de esta guía uso ejemplos reales:

| Skill | Libro | Autor |
|-------|-------|-------|
| `/rw` | *A Random Walk Down Wall Street* (*Un Paseo Aleatorio por Wall Street*) | Burton Malkiel |
| `/bg` | *The Behavior Gap* (*La Brecha del Comportamiento*) | Carl Richards |
| `/ia` | *The Investment Answer* (*La Respuesta de la Inversión*) | Goldie & Murray |

Sustituye `/rw` por el prefijo de tu skill.

**Regla 2 — Los corchetes son huecos que rellenas.** Todo lo que veas entre `[corchetes]` es un *placeholder* (marcador de posición): cámbialo por tu dato concreto antes de enviar.

**Regla 3 — Encadenar > preguntar suelto.** Mantén la sesión (*session*) abierta. Claude Code conserva el contexto, así que repreguntar ("amplía el punto 3", "compara con lo anterior") rinde más que disparar preguntas aisladas. Es la diferencia entre **una conversación** y **enviar mensajes sueltos por WhatsApp**.

---

## Tabla maestra de modos

| Modo | Cuándo usarlo |
|------|---------------|
| 🗺️ Exploración inicial | Primer contacto con el libro |
| 📖 Lectura dirigida | Profundizar en un capítulo concreto |
| 🎯 Crítico / abogado del diablo | Desafiar y cuestionar |
| 🛠️ Aplicación práctica | Llevarlo a tu cartera real |
| 🔄 Síntesis comparativa | Diálogo entre varios libros |
| 🃏 Flashcards y aprendizaje activo | Memorizar y autoevaluarte |
| ⚡ Ejecutivo (TL;DR) | Velocidad máxima |
| 🧠 Encadenado con otras skills | Combinar entrevistador, modelos-mentales, bibliotecario |

---

## 🗺️ Modo 1 — Exploración inicial

**Cuándo:** los primeros 5 minutos con un libro nuevo. Quieres el mapa antes que el detalle.

**Analogía:** es como dar la vuelta al libro en la librería — leer solapa, contraportada e índice — antes de decidir si te lo llevas.

```
/rw

/rw "dame el mapa del libro: tesis central, estructura y a quién va dirigido"

/rw "¿qué capítulos tienes? Lístame el índice (table of contents) con una frase por capítulo"

/rw "¿cuál es la idea más importante de todo el libro en una sola frase?"

/rw "si solo pudiera leer 3 capítulos, ¿cuáles y por qué?"

/rw "¿qué da por sentado el autor que debería saber yo antes de leerlo?"

/rw "¿de qué año es y qué partes pueden estar desactualizadas hoy?"
```

**Tips:**
- Empieza siempre con el comando pelado (`/rw`) para que "abra el libro" y se sitúe.
- La pregunta "*¿qué partes pueden estar desactualizadas?*" es clave en finanzas: muchos clásicos se escribieron antes de los ETF de bajo coste o las cripto.

---

## 📖 Modo 2 — Lectura dirigida

**Cuándo:** quieres entender a fondo un capítulo o concepto concreto.

**Analogía:** es sentarte con el becario y decirle "*explícame este capítulo como si me estuvieras dando una clase particular*", y poder cortarle para repreguntar.

```
/rw ch[NN]
/rw "capítulo [NN]"
/rw "[nombre del concepto, ej. hipótesis del mercado eficiente]"

/rw "explícame el capítulo [NN]: idea central, argumentos, ejemplos y conclusión"

/rw "explícame [concepto] como si tuviera 12 años, con una analogía cotidiana"

/rw "ahora explícamelo de nuevo pero a nivel experto, sin simplificar"

/rw "dame la cita verbatim (literal) donde el autor define [concepto]"

/rw "¿qué ejemplo numérico usa el autor para ilustrar [concepto]? Reprodúcelo paso a paso"

/rw "resume el capítulo [NN] en: 1 frase / 1 párrafo / 5 bullets. Las tres versiones"

/rw "indica capítulo y sección de cada afirmación que hagas"
```

**Tips:**
- **Doble pasada** (*double pass*): pide la versión "para 12 años" y luego la "nivel experto". El contraste fija el concepto mejor que cualquiera de las dos por separado.
- **"Verbatim" / "literal"** fuerza transcripción exacta del texto en vez de paráfrasis — útil para subrayar el original.
- **"Indica capítulo y sección"** convierte al becario en tu índice analítico vivo: luego verificas en el PDF/libro físico.
- Técnica de embudo (*funnel*): general → detalle → ejemplo → matiz.
  ```
  /rw "háblame del capítulo de renta fija (bonos)"
  /rw "céntrate en la parte de duration (duración)"
  /rw "dame un ejemplo numérico de cómo afecta una subida de tipos"
  ```

---

## 🎯 Modo 3 — Crítico / abogado del diablo

**Cuándo:** ya entiendes la tesis y quieres ponerla a prueba. Imprescindible en inversión, donde el consenso de un libro puede ser el sesgo de otro.

**Analogía:** es contratar a un segundo becario *escéptico* cuya única misión es buscarle las cosquillas al primero.

```
/rw "¿cuáles son los puntos débiles del argumento del capítulo [NN]?"

/rw "lista las asunciones implícitas (implicit assumptions) que el autor da por demostradas sin probarlas"

/rw "hazme el steel-man (versión más fuerte) y el straw-man (versión más débil) de la tesis principal"

/rw "¿qué diría un value investor como Graham sobre el capítulo [NN]?"

/rw "¿qué crítica académica conocida existe contra esta tesis? Si no está en el libro, dímelo explícitamente"

/rw "¿en qué contexto histórico o de mercado falla este consejo?"

/rw "distingue claramente: ¿qué dice el libro y qué estás añadiendo tú?"

/rw "dame el contraargumento más incómodo para alguien que ya está convencido de esta tesis"
```

**Tips:**
- **El "no me mientas":** *"si no está en el libro, dímelo explícitamente"* y *"distingue entre lo que dice el autor y lo que añades tú"* reducen la confabulación (*hallucination* — cuando el modelo se inventa contenido).
- **Steel-man antes que straw-man:** pide siempre primero la versión más fuerte del argumento. Te protege de descartar una idea por una caricatura.
- Enfrenta autores: *"¿qué le objetaría [otro autor] a este capítulo?"* saca tensiones que el libro solo no muestra.

---

## 🛠️ Modo 4 — Aplicación práctica

**Cuándo:** quieres bajar la teoría a tu cartera (*portfolio*) real. Aquí el becario deja de ser bibliotecario y se vuelve **consultor**.

**Analogía:** es como llevarle al fisioterapeuta no "el manual de anatomía" sino *tu* espalda concreta y decirle "aplícame esto a mí".

```
/rw "aplica los principios del capítulo [NN] a una cartera de [80.000 €] a [20] años"

/rw "traduce las recomendaciones del libro a un inversor español de [45] años, perfil [moderado], horizonte [20a]"

/rw "haz una checklist práctica del capítulo [NN] para revisar mi cartera trimestralmente"

/rw "¿qué pensaría el autor de mi tesis de [invertir en small caps value]?"

/rw "convierte el capítulo de asset allocation (asignación de activos) en una regla de decisión que pueda seguir yo solo"

/rw "dame 3 errores que el autor advierte y que probablemente yo esté cometiendo"

/rw "diseña un plan de acción de 90 días basado en este libro, paso a paso"

/rw "¿cómo encaja esto con la fiscalidad y los vehículos españoles (IIC, fondos indexados, ETF)?"
```

**Tips:**
- Dale **contexto numérico real** (edad, capital, horizonte, perfil de riesgo). Cuanto más concreto el dato, más útil el consejo.
- **"Convierte en regla de decisión"** es oro: transforma prosa en un *if/then* (si pasa X, hago Y) que puedes ejecutar sin releer el libro.
- Recuerda: el becario te aplica *la lógica del autor*, no asesoramiento financiero personalizado. Verifica siempre con tu propia cabeza (y, para decisiones reales, con un profesional).

---

## 🔄 Modo 5 — Síntesis comparativa

**Cuándo:** tienes varias skills-libro y quieres un debate entre ellas. Lo más potente y lo que casi nadie usa.

**Analogía:** es montar una **mesa redonda** (*panel*) y sentar a Malkiel, Richards y Goldie en la misma sala a discutir el mismo tema.

```
/rw "resume tu postura sobre market timing (anticiparse al mercado)"
/bg "ahora dame la postura de Carl Richards sobre lo mismo"
/ia "y la de Goldie & Murray"
/rw "¿en qué coinciden los tres y en qué difieren? Hazme una tabla"

/rw "tu postura sobre gestión activa vs pasiva, en 5 bullets"
/bg "contrasta con el enfoque conductual (behavioral) de este libro"

/ia "¿qué pregunta clave plantea este libro que Malkiel no aborda?"

/rw "construye un mapa de consensos y disputas entre estos 3 libros sobre: comisiones, diversificación, riesgo y comportamiento"
```

**Tips:**
- **Un libro por turno:** pregunta primero a uno, luego a otro, y solo al final pides la síntesis. Si mezclas en un solo prompt, los becarios se pisan.
- **Tabla de consenso/disputa:** terminar con *"¿en qué coinciden y en qué difieren? Tabla."* es la forma más rápida de ver el mapa intelectual completo.
- **Una skill por libro, no una mega-skill.** Diez libros en una sola = becario confundido. Mejor 10 prefijos cortos (`rw`, `bg`, `ia`, `ib`…) y los encadenas a mano.

---

## 🃏 Modo 6 — Flashcards y aprendizaje activo

**Cuándo:** quieres *retener*, no solo entender. Recuperación activa (*active recall*) + repetición espaciada (*spaced repetition*).

**Analogía:** es pedirle al becario que te prepare las **chuletas de examen** y luego te tome la lección.

```
/rw "genera 10 flashcards (pregunta → respuesta) sobre el capítulo [NN], formato apto para Anki"

/rw "hazme 5 preguntas tipo test de opción múltiple sobre [concepto], con la respuesta al final"

/rw "tómame la lección: hazme una pregunta, espera mi respuesta y corrígeme"

/rw "dame los 7 términos clave del libro con su definición en una línea (glosario)"

/rw "explícame [concepto] con el método Feynman: como si yo se lo tuviera que enseñar a otro"

/rw "crea un quiz progresivo de 5 preguntas, de fácil a difícil, sobre el libro entero"

/rw "dame una pregunta de repaso del capítulo [NN] cada vez que te escriba 'siguiente'"
```

**Tips:**
- **"Formato Anki"** te da el par pregunta/respuesta listo para exportar a tu sistema de tarjetas.
- **"Tómame la lección"** activa el modo socrático: el becario pregunta, tú respondes, él corrige. Aprendes el doble que leyendo.
- **Método Feynman** (explicar como si enseñaras): si no puedes, has encontrado tu laguna exacta.

---

## ⚡ Modo 7 — Ejecutivo (TL;DR)

**Cuándo:** tienes 2 minutos y necesitas lo esencial. *TL;DR* = "too long, didn't read" (demasiado largo, no lo leí).

**Analogía:** es pedirle al becario el **resumen de ascensor** (*elevator pitch*): lo que cabe entre la planta baja y tu piso.

```
/rw "TL;DR del libro en 5 frases, sin relleno"

/rw "dame solo los 3 consejos accionables (actionable) más importantes, nada más"

/rw "una frase por capítulo, lista numerada, cero explicación"

/rw "si tuvieras que tatuarte una sola idea de este libro, ¿cuál?"

/rw "resumen ejecutivo: problema → tesis → evidencia → recomendación. Máximo 8 líneas"

/rw "modo telegrama: solo sustantivos y verbos clave"
```

**Tips:**
- Sé **brutal con la restricción de longitud**: "5 frases", "máximo 8 líneas", "nada más". El becario obedece el límite si se lo pones explícito.
- **"Sin relleno" / "cero explicación"** elimina el preámbulo cortés y va al grano.
- Guarda el TL;DR como nota: es tu "índice de recuerdo" para cuando vuelvas al libro meses después.

---

## 🧠 Modo 8 — Encadenado con otras skills

**Cuándo:** quieres combinar la skill-libro con tus otras skills (`entrevistador`, `modelos-mentales`, `bibliotecario`) para multiplicar el resultado.

**Analogía:** es como tener un **equipo multidisciplinar**: el becario (skill-libro) aporta el contenido, y cada otra skill aporta un método distinto de trabajarlo.

### Con `entrevistador`

```
/entrevistador + /rw  →  "hazle una entrevista simulada al autor sobre la sección de [criptoactivos / fondos indexados]"

/rw "dame el contenido del capítulo [NN]"
/entrevistador "ahora conviértelo en una entrevista al autor: prólogo + cuestionario + respuestas en su voz"
```
*Extrae el "zumo inferencial" del libro en formato conversacional, no en resumen plano.*

### Con `modelos-mentales`

```
/rw "resume la tesis del capítulo [NN]"
/modelos-mentales modo estándar "analiza esta tesis con primeros principios (first principles) e inversión (inversion)"

/rw "dame la recomendación principal del libro"
/modelos-mentales "aplícale el modelo de clase de referencia (reference class) y falsificación (falsifiability): ¿se sostiene?"
```
*Pasas de "qué dice el libro" a "qué resiste el escrutinio de varios modelos de razonamiento".*

### Con `bibliotecario`

```
/rw "¿qué temas menciona el autor pero no desarrolla en profundidad?"
/bibliotecario "construye una bibliografía para profundizar en [esos temas], secuenciada por dificultad"
```
*El libro te marca las lagunas; el bibliotecario te traza la ruta para llenarlas.*

**Tips:**
- **Orden importa:** primero extrae contenido con la skill-libro, *luego* pásalo a la skill de método. Es la cadena de montaje (*pipeline*): materia prima → procesado.
- **Cierre del ciclo:** termina una sesión de estudio con `/bibliotecario` para que el final de un libro sea el comienzo del siguiente. Así tu ecosistema lector se autoalimenta.

---

## 📌 Chuleta rápida (*cheat sheet*) — los 12 prompts que más usarás

```
1.  /rw                                          → abrir y situarse
2.  /rw "índice con una frase por capítulo"      → mapa
3.  /rw "TL;DR en 5 frases"                       → esencia
4.  /rw "explica [X] para 12 años + nivel experto" → entender de verdad
5.  /rw "cita verbatim donde define [X]"          → texto original
6.  /rw "asunciones implícitas del cap [NN]"      → ver lo no dicho
7.  /rw "steel-man y straw-man de la tesis"       → poner a prueba
8.  /rw "aplícalo a [mi cartera concreta]"        → llevarlo a la práctica
9.  /rw "convierte el cap [NN] en regla de decisión" → if/then accionable
10. /rw "10 flashcards formato Anki del cap [NN]" → memorizar
11. /rw "indica capítulo y sección de todo"       → verificable
12. /rw + /otra-skill                             → encadenar
```

---

## 🧭 Filosofía de fondo

Lo que estás construyendo no es una colección de resúmenes: es una **biblioteca conversacional** (*conversational library*). Un equipo de becarios especialistas, cada uno experto en un libro, a los que llamas por su nombre corto.

Cuando esto funciona, dejas de **leer libros en línea recta** y empiezas a **interrogarlos** según lo que necesitas en cada momento — manteniendo intacta la riqueza del texto original, pero con la velocidad de una conversación.

> *Regla de oro:* un libro bien convertido en skill no sustituye leerlo; lo que hace es que puedas **volver a él mil veces sin releerlo entero**.
