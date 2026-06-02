# Guía exhaustiva: cómo exprimir cualquier *skill-libro* en Claude Code

> Plantilla de *prompts* (instrucciones) reutilizable para **cualquier libro y cualquier temática** que hayas convertido en skill con `book-to-skill`.
> Sirve igual para un ensayo de historia, un manual técnico, un libro de cocina, una biografía o un tratado de filosofía.

---

## 0. Antes de empezar: las 3 reglas del juego

Piensa en tu skill-libro como **un becario superdotado que se ha leído el libro entero, lo tiene subrayado y con post-its en cada capítulo**. Tú no le pides que "te lo cuente": lo *interrogas* como a un colega que acaba de cerrar el libro.

**Regla 1 — El prefijo corto es su nombre.** En esta guía uso `/lib` como prefijo de ejemplo (de "libro"). Sustitúyelo por el prefijo real de tu skill:

```
/lib            →  el prefijo que elegiste al generar la skill
```

Si tienes varios libros, dales prefijos cortos y memorables (2-4 letras): `/hist`, `/cook`, `/sap`, `/zen`… Así puedes llamar a cada becario por su nombre.

**Regla 2 — Los corchetes son huecos que rellenas.** Todo lo que veas entre `[corchetes]` es un *placeholder* (marcador de posición): cámbialo por tu dato concreto antes de enviar. Por ejemplo `[concepto]`, `[capítulo NN]`, `[tu situación]`.

**Regla 3 — Encadenar > preguntar suelto.** Mantén la sesión (*session*) abierta. Claude Code conserva el contexto, así que repreguntar ("amplía el punto 3", "compara con lo anterior") rinde más que disparar preguntas aisladas. Es la diferencia entre **una conversación** y **enviar mensajes sueltos por WhatsApp**.

---

## Tabla maestra de modos

| Modo | Cuándo usarlo |
|------|---------------|
| 🗺️ Exploración inicial | Primer contacto con el libro |
| 📖 Lectura dirigida | Profundizar en un capítulo concreto |
| 🎯 Crítico / abogado del diablo | Desafiar y cuestionar |
| 🛠️ Aplicación práctica | Llevarlo a tu situación real |
| 🔄 Síntesis comparativa | Diálogo entre varios libros |
| 🃏 Flashcards y aprendizaje activo | Memorizar y autoevaluarte |
| ⚡ Ejecutivo (TL;DR) | Velocidad máxima |
| 🧠 Encadenado con otras skills | Combinar entrevistador, modelos-mentales, bibliotecario |

---

## 🗺️ Modo 1 — Exploración inicial

**Cuándo:** los primeros 5 minutos con un libro nuevo. Quieres el mapa antes que el detalle.

**Analogía:** es como dar la vuelta al libro en la librería — leer solapa, contraportada e índice — antes de decidir si te lo llevas.

```
/lib

/lib "dame el mapa del libro: tesis o propósito central, estructura y a quién va dirigido"

/lib "¿qué capítulos tienes? Lístame el índice (table of contents) con una frase por capítulo"

/lib "¿cuál es la idea más importante de todo el libro en una sola frase?"

/lib "si solo pudiera leer 3 capítulos, ¿cuáles y por qué?"

/lib "¿qué da por sentado el autor que debería saber yo antes de leerlo?"

/lib "¿de qué año es y qué partes pueden estar desactualizadas o ser polémicas hoy?"

/lib "¿qué tipo de libro es: divulgación, manual práctico, ensayo argumentativo, narrativo…? ¿Cómo conviene leerlo?"
```

**Tips:**
- Empieza siempre con el comando pelado (`/lib`) para que "abra el libro" y se sitúe.
- La pregunta "*¿qué partes pueden estar desactualizadas?*" es útil en cualquier campo que evolucione (tecnología, medicina, ciencia, normativa).
- Saber **qué tipo de libro es** cambia cómo lo interrogas: un manual práctico pide "pasos", un ensayo pide "argumentos", una narración pide "claves".

---

## 📖 Modo 2 — Lectura dirigida

**Cuándo:** quieres entender a fondo un capítulo o concepto concreto.

**Analogía:** es sentarte con el becario y decirle "*explícame este capítulo como si me estuvieras dando una clase particular*", y poder cortarle para repreguntar.

```
/lib ch[NN]
/lib "capítulo [NN]"
/lib "[nombre del concepto o tema]"

/lib "explícame el capítulo [NN]: idea central, argumentos o pasos, ejemplos y conclusión"

/lib "explícame [concepto] como si tuviera 12 años, con una analogía cotidiana"

/lib "ahora explícamelo de nuevo pero a nivel experto, sin simplificar"

/lib "dame la cita verbatim (literal) donde el autor explica o define [concepto]"

/lib "¿qué ejemplo, caso o historia usa el autor para ilustrar [concepto]? Reprodúcelo"

/lib "resume el capítulo [NN] en: 1 frase / 1 párrafo / 5 bullets. Las tres versiones"

/lib "indica capítulo y sección de cada afirmación que hagas"

/lib "¿cómo conecta el capítulo [NN] con lo que el autor explicó antes?"
```

**Tips:**
- **Doble pasada** (*double pass*): pide la versión "para 12 años" y luego la "nivel experto". El contraste fija el concepto mejor que cualquiera de las dos por separado.
- **"Verbatim" / "literal"** fuerza transcripción exacta del texto en vez de paráfrasis — útil para subrayar el original.
- **"Indica capítulo y sección"** convierte al becario en tu índice analítico vivo: luego verificas en el PDF/libro físico.
- Técnica de embudo (*funnel*): general → detalle → ejemplo → matiz.
  ```
  /lib "háblame del capítulo sobre [tema amplio]"
  /lib "céntrate en la parte de [subtema]"
  /lib "dame un ejemplo concreto de eso"
  ```

---

## 🎯 Modo 3 — Crítico / abogado del diablo

**Cuándo:** ya entiendes la tesis y quieres ponerla a prueba. Útil en cualquier libro que defienda una postura o método.

**Analogía:** es contratar a un segundo becario *escéptico* cuya única misión es buscarle las cosquillas al primero.

```
/lib "¿cuáles son los puntos débiles del argumento del capítulo [NN]?"

/lib "lista las asunciones implícitas (implicit assumptions) que el autor da por demostradas sin probarlas"

/lib "hazme el steel-man (versión más fuerte) y el straw-man (versión más débil) de la tesis principal"

/lib "¿qué pensaría alguien que defiende la postura contraria sobre el capítulo [NN]?"

/lib "¿qué crítica conocida existe contra esta tesis? Si no está en el libro, dímelo explícitamente"

/lib "¿en qué contexto, época o situación falla este consejo o argumento?"

/lib "distingue claramente: ¿qué dice el libro y qué estás añadiendo tú?"

/lib "dame el contraargumento más incómodo para alguien que ya está convencido de esta tesis"

/lib "¿el autor confunde correlación con causalidad en algún punto? ¿Dónde?"
```

**Tips:**
- **El "no me mientas":** *"si no está en el libro, dímelo explícitamente"* y *"distingue entre lo que dice el autor y lo que añades tú"* reducen la confabulación (*hallucination* — cuando el modelo se inventa contenido).
- **Steel-man antes que straw-man:** pide siempre primero la versión más fuerte del argumento. Te protege de descartar una idea por una caricatura.
- Pregunta por **el contexto donde el consejo falla**: casi ningún libro avisa de sus propios límites.

---

## 🛠️ Modo 4 — Aplicación práctica

**Cuándo:** quieres bajar la teoría a tu vida, tu trabajo o tu proyecto. Aquí el becario deja de ser bibliotecario y se vuelve **consultor**.

**Analogía:** es como llevarle al fisioterapeuta no "el manual de anatomía" sino *tu* espalda concreta y decirle "aplícame esto a mí".

```
/lib "aplica los principios del capítulo [NN] a mi caso: [describe tu situación]"

/lib "traduce las recomendaciones del libro a alguien con [tu perfil/contexto]"

/lib "haz una checklist práctica del capítulo [NN] para [tu objetivo]"

/lib "¿qué pensaría el autor de mi plan de [describe tu plan]?"

/lib "convierte el capítulo [NN] en una regla de decisión que pueda seguir yo solo"

/lib "dame 3 errores que el autor advierte y que probablemente yo esté cometiendo"

/lib "diseña un plan de acción de [30/60/90] días basado en este libro, paso a paso"

/lib "¿qué es lo primero que debería hacer mañana tras leer este capítulo?"
```

**Tips:**
- Dale **contexto real y concreto** (tu situación, tu objetivo, tus limitaciones). Cuanto más específico el dato, más útil el consejo.
- **"Convierte en regla de decisión"** es oro: transforma prosa en un *if/then* (si pasa X, hago Y) que puedes ejecutar sin releer el libro.
- Recuerda: el becario te aplica *la lógica del autor*. En temas sensibles (salud, dinero, legal) verifica siempre con un profesional.

---

## 🔄 Modo 5 — Síntesis comparativa

**Cuándo:** tienes varias skills-libro y quieres un debate entre ellas. Lo más potente y lo que casi nadie usa.

**Analogía:** es montar una **mesa redonda** (*panel*) y sentar a varios autores en la misma sala a discutir el mismo tema.

```
/lib "resume tu postura sobre [tema]"
/lib2 "ahora dame la postura de este otro autor sobre lo mismo"
/lib "¿en qué coinciden y en qué difieren? Hazme una tabla"

/lib "tu enfoque sobre [tema], en 5 bullets"
/lib2 "contrasta con el enfoque de este libro"

/lib2 "¿qué pregunta o ángulo plantea este libro que el otro no aborda?"

/lib "construye un mapa de consensos y disputas entre estos libros sobre: [aspecto 1], [aspecto 2], [aspecto 3]"
```

**Tips:**
- **Un libro por turno:** pregunta primero a uno, luego a otro, y solo al final pides la síntesis. Si mezclas en un solo prompt, los becarios se pisan.
- **Tabla de consenso/disputa:** terminar con *"¿en qué coinciden y en qué difieren? Tabla."* es la forma más rápida de ver el mapa intelectual completo.
- **Una skill por libro, no una mega-skill.** Diez libros en una sola = becario confundido. Mejor 10 prefijos cortos y los encadenas a mano.
- Funciona aunque los libros sean de **temáticas distintas**: a veces el cruce más fértil es entre un libro de biología y uno de gestión de equipos.

---

## 🃏 Modo 6 — Flashcards y aprendizaje activo

**Cuándo:** quieres *retener*, no solo entender. Recuperación activa (*active recall*) + repetición espaciada (*spaced repetition*).

**Analogía:** es pedirle al becario que te prepare las **chuletas de examen** y luego te tome la lección.

```
/lib "genera 10 flashcards (pregunta → respuesta) sobre el capítulo [NN], formato apto para Anki"

/lib "hazme 5 preguntas tipo test de opción múltiple sobre [concepto], con la respuesta al final"

/lib "tómame la lección: hazme una pregunta, espera mi respuesta y corrígeme"

/lib "dame los términos clave del libro con su definición en una línea (glosario)"

/lib "explícame [concepto] con el método Feynman: como si yo se lo tuviera que enseñar a otro"

/lib "crea un quiz progresivo de 5 preguntas, de fácil a difícil, sobre el libro entero"

/lib "dame una pregunta de repaso del capítulo [NN] cada vez que te escriba 'siguiente'"
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
/lib "TL;DR del libro en 5 frases, sin relleno"

/lib "dame solo los 3 puntos accionables (actionable) o ideas más importantes, nada más"

/lib "una frase por capítulo, lista numerada, cero explicación"

/lib "si tuvieras que tatuarte una sola idea de este libro, ¿cuál?"

/lib "resumen ejecutivo: problema → tesis → evidencia → conclusión. Máximo 8 líneas"

/lib "modo telegrama: solo sustantivos y verbos clave"
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
/entrevistador + /lib  →  "hazle una entrevista simulada al autor sobre [tema/sección]"

/lib "dame el contenido del capítulo [NN]"
/entrevistador "ahora conviértelo en una entrevista al autor: prólogo + cuestionario + respuestas en su voz"
```
*Extrae el "zumo inferencial" del libro en formato conversacional, no en resumen plano.*

### Con `modelos-mentales`

```
/lib "resume la tesis del capítulo [NN]"
/modelos-mentales modo estándar "analiza esta tesis con primeros principios (first principles) e inversión (inversion)"

/lib "dame la recomendación o conclusión principal del libro"
/modelos-mentales "aplícale el modelo de clase de referencia (reference class) y falsificación (falsifiability): ¿se sostiene?"
```
*Pasas de "qué dice el libro" a "qué resiste el escrutinio de varios modelos de razonamiento".*

### Con `bibliotecario`

```
/lib "¿qué temas menciona el autor pero no desarrolla en profundidad?"
/bibliotecario "construye una bibliografía para profundizar en [esos temas], secuenciada por dificultad"
```
*El libro te marca las lagunas; el bibliotecario te traza la ruta para llenarlas.*

**Tips:**
- **Orden importa:** primero extrae contenido con la skill-libro, *luego* pásalo a la skill de método. Es la cadena de montaje (*pipeline*): materia prima → procesado.
- **Cierre del ciclo:** termina una sesión de estudio con `/bibliotecario` para que el final de un libro sea el comienzo del siguiente. Así tu ecosistema lector se autoalimenta.

---

## 📌 Chuleta rápida (*cheat sheet*) — los 12 prompts que más usarás

```
1.  /lib                                          → abrir y situarse
2.  /lib "índice con una frase por capítulo"      → mapa
3.  /lib "TL;DR en 5 frases"                       → esencia
4.  /lib "explica [X] para 12 años + nivel experto" → entender de verdad
5.  /lib "cita verbatim donde explica [X]"         → texto original
6.  /lib "asunciones implícitas del cap [NN]"      → ver lo no dicho
7.  /lib "steel-man y straw-man de la tesis"       → poner a prueba
8.  /lib "aplícalo a [mi situación concreta]"      → llevarlo a la práctica
9.  /lib "convierte el cap [NN] en regla de decisión" → if/then accionable
10. /lib "10 flashcards formato Anki del cap [NN]" → memorizar
11. /lib "indica capítulo y sección de todo"       → verificable
12. /lib + /otra-skill                             → encadenar
```

---

## 🧭 Filosofía de fondo

Lo que estás construyendo no es una colección de resúmenes: es una **biblioteca conversacional** (*conversational library*). Un equipo de becarios especialistas, cada uno experto en un libro, a los que llamas por su nombre corto.

Cuando esto funciona, dejas de **leer libros en línea recta** y empiezas a **interrogarlos** según lo que necesitas en cada momento — manteniendo intacta la riqueza del texto original, pero con la velocidad de una conversación.

> *Regla de oro:* un libro bien convertido en skill no sustituye leerlo; lo que hace es que puedas **volver a él mil veces sin releerlo entero**.

---

### Cómo adaptar esta guía a *tu* libro

1. Abre este archivo en tu editor.
2. Busca y reemplaza (*find & replace*) `/lib` por el prefijo real de tu skill.
3. Rellena los `[corchetes]` con los datos de tu libro y tu situación.
4. Guarda tu versión personalizada junto al `SKILL.md` correspondiente.
5. (Opcional) Borra los modos que no uses para tener una chuleta más ligera.
