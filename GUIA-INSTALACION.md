# 📚 Guía para principiantes: instalar y usar `book-to-skill` desde cero

Esta guía está pensada para alguien que **nunca** ha usado una terminal ni Claude Code.
Si sigues los pasos en orden, en unos 15 minutos podrás convertir un libro (PDF, EPUB, etc.)
en una "skill" que Claude consulta cuando tú quieras.

> **¿Qué es una skill?** Es una base de conocimiento estructurada que extraemos del libro
> (sus marcos, principios y técnicas). En lugar de releer el PDF, le preguntas a Claude
> y él lee el capítulo correcto y te responde con el contenido real del libro.

---

## 🗺️ Lo que vas a hacer (vista rápida)

1. Instalar **Claude Code** (el programa que ejecuta las skills).
2. Comprobar que tienes **Python 3** (lo necesita el extractor de texto).
3. Instalar las **herramientas de extracción** según el formato de tu libro.
4. Instalar la **skill `book-to-skill`** en tu equipo.
5. **Convertir** un libro → te genera la skill.
6. **Usar** la skill generada.

No hace falta saber programar. Solo copiar y pegar comandos.

---

## 0. Antes de empezar: abrir la terminal

- **macOS:** pulsa `⌘ + Espacio`, escribe **Terminal** y pulsa Enter.
- **Windows:** abre **PowerShell** (botón Inicio → escribe "PowerShell").
- **Linux:** abre tu aplicación de **Terminal**.

Cuando esta guía diga "ejecuta este comando", significa: **copiar la línea, pegarla en la
terminal y pulsar Enter**.

> 💡 Truco: si un comando te pide tu contraseña (por usar `sudo`), escríbela "a ciegas"
> (no se ven los caracteres) y pulsa Enter.

---

## 1. Instalar Claude Code

Claude Code necesita **Node.js**. Comprueba si ya lo tienes:

```bash
node --version
```

- Si te muestra algo como `v20.x` o superior → ya lo tienes, pasa al siguiente bloque.
- Si dice "command not found" → instala Node.js:
  - **macOS** (con [Homebrew](https://brew.sh)): `brew install node`
  - **Windows / Linux:** descarga el instalador desde <https://nodejs.org> (versión LTS).

Ahora instala Claude Code:

```bash
npm install -g @anthropic-ai/claude-code
```

Arráncalo (la primera vez te pedirá iniciar sesión con tu cuenta de Anthropic/Claude):

```bash
claude
```

> Existen también la app de escritorio (Mac/Windows), la web (<https://claude.ai/code>),
> extensiones para **VS Code** y **JetBrains**, y editores tipo VS Code como **Antigravity**,
> **Cursor** o **Windsurf**. El resto de la guía asume la terminal, pero los comandos `/...`
> funcionan igual en todas — mira el **apartado 1.5** para instalar y usar la skill desde un
> editor. Documentación oficial: <https://docs.claude.com/en/docs/claude-code>.

---

## 1.5 — Usarlo desde un editor de código (VS Code, Antigravity, Cursor…)

**Idea clave (léela primero):** la skill se instala **una sola vez en tu equipo**
(en `~/.claude/skills/`) y funciona en **cualquier sitio donde puedas ejecutar Claude Code**.
El editor es solo "la ventana"; el motor que ejecuta la skill siempre es **Claude Code**. Por
eso, instales como instales la skill (paso 4), estará disponible en todas las opciones de abajo.

> ⚠️ Importante: `book-to-skill` es una skill **de Claude Code**. El asistente de IA *propio* de
> algunos editores (por ejemplo, **Gemini** en Antigravity) **no** usa estas skills. Para
> aprovecharla necesitas **Claude Code** dentro de ese editor — y siempre lo tienes a mano a
> través de la **terminal integrada**.

### Opciones disponibles

| Dónde | Cómo se usa | Ideal para |
|-------|-------------|------------|
| **Terminal** | el comando `claude` (el del paso 1) | lo más simple; funciona siempre |
| **VS Code** | extensión oficial "Claude Code" | si ya usas VS Code |
| **JetBrains** (PyCharm, IntelliJ…) | plugin oficial "Claude Code" | usuarios de JetBrains |
| **App de escritorio** (Mac/Windows) | descarga oficial | sin terminal, ventana propia |
| **Web** | <https://claude.ai/code> | probar sin instalar nada |
| **Antigravity / Cursor / Windsurf** | terminal integrada → `claude` | editores tipo VS Code con su propia IA |

### A) VS Code (la integración más cómoda)

1. Abre **VS Code**.
2. Ve al icono de **Extensiones** (barra lateral izquierda, parece 4 cuadraditos) o pulsa
   `Ctrl/⌘ + Mayús + X`.
3. Busca **"Claude Code"** (de Anthropic) y pulsa **Install**.
4. Inicia sesión cuando te lo pida (la misma cuenta de Claude del paso 1).
5. Ábrelo desde el icono de Claude en la barra lateral (o con el atajo `Ctrl/⌘ + Esc`).
6. Escribe `/book-to-skill ~/ruta/a/tu-libro.epub`, igual que en la terminal.

> 💡 ¿No quieres instalar la extensión? En VS Code abre la **terminal integrada**
> (menú *Terminal → New Terminal*, o el atajo `` Ctrl + ` ``) y escribe `claude`. Funciona idéntico.

### B) Antigravity, Cursor, Windsurf (editores basados en VS Code)

Son "primos" de VS Code, cada uno con **su propio asistente de IA** (en Antigravity es Gemini).
Ese asistente propio **no** entiende las skills de Claude Code, pero puedes usar Claude Code
dentro de ellos así:

1. Ten Claude Code instalado (paso 1) y la skill instalada (paso 4).
2. Abre el editor y su **terminal integrada**: menú **Terminal → New Terminal**
   (o el atajo `` Ctrl + ` ``).
3. En esa terminal escribe:
   ```bash
   claude
   ```
4. Ya dentro, usa los comandos de siempre: `/book-to-skill ...` para generar y `/tu-skill ...` para usar.

> Algunos de estos editores también permiten instalar extensiones de VS Code. Si encuentras la
> extensión **"Claude Code"** en su tienda, instálala como en el apartado A. Si no aparece, la
> **terminal integrada** es el método que **siempre** funciona.

### ¿Hace falta "configurar" algo?

Muy poco:
- **Iniciar sesión** en Claude la primera vez (te lo pide solo).
- **Nada más para las skills**: se cargan automáticamente desde `~/.claude/skills/`. No hay que
  "activarlas" en el editor. Si acabas de instalar una y no aparece, **cierra y vuelve a abrir**
  el editor (o la terminal).

---

## 2. Comprobar Python 3

El extractor de texto (`extract.py`) usa Python. Comprueba:

```bash
python3 --version
```

- Si muestra `Python 3.x` → perfecto.
- Si no lo tienes:
  - **macOS:** `brew install python`
  - **Windows / Linux:** descárgalo de <https://www.python.org/downloads/>

---

## 3. Instalar las herramientas de extracción (según tu libro)

`book-to-skill` lee el archivo y extrae el texto. Cada formato usa una herramienta distinta.
**No necesitas instalarlas todas** — solo la de la fila de tu formato. Si no instalas nada,
funcionará igualmente con un método de reserva más básico (y te avisará).

| Tu archivo es… | Herramienta recomendada | Cómo instalarla |
|----------------|-------------------------|-----------------|
| **TXT / Markdown / RST / AsciiDoc** | *(ninguna)* | Ya funciona, no instales nada |
| **PDF** (texto, pocas tablas) | `pdftotext` (poppler) | macOS: `brew install poppler` · Linux: `sudo apt install poppler-utils` |
| **PDF** (técnico: código, tablas, fórmulas) | `docling` | `pip3 install docling` |
| **EPUB** | `ebooklib` + `beautifulsoup4` | `pip3 install ebooklib beautifulsoup4` |
| **DOCX** (Word) | `python-docx` | `pip3 install python-docx` |
| **HTML** | `beautifulsoup4` | `pip3 install beautifulsoup4` |
| **RTF** | `striprtf` | `pip3 install striprtf` |
| **MOBI / AZW / AZW3** (Kindle) | Calibre (app externa) | Descárgala de <https://calibre-ebook.com/download> |

> 💡 Si no sabes qué instalar, no te preocupes: lanza la skill (paso 5) y, si falta algo,
> te dirá exactamente qué comando ejecutar.

---

## 4. Instalar la skill `book-to-skill`

Tienes dos formas. La **A** es la más fácil.

### Opción A — Pídeselo a Claude Code (recomendada)

Abre Claude Code (comando `claude`) y pega esta frase tal cual:

```
Install book-to-skill: https://raw.githubusercontent.com/cerebroetereo/book-to-skill/main/SKILL.md
```

Claude descargará la skill y su script en la carpeta correcta.

### Opción B — Manual (copiar y pegar en la terminal)

```bash
mkdir -p ~/.claude/skills/book-to-skill/scripts

curl -o ~/.claude/skills/book-to-skill/SKILL.md \
  https://raw.githubusercontent.com/cerebroetereo/book-to-skill/main/SKILL.md

curl -o ~/.claude/skills/book-to-skill/scripts/extract.py \
  https://raw.githubusercontent.com/cerebroetereo/book-to-skill/main/scripts/extract.py
```

> **¿Dónde se instala?** En `~/.claude/skills/book-to-skill/`.
> (`~` es tu carpeta personal: en macOS es `/Users/tu-usuario`.)

---

## 5. Comprobar que la skill está instalada

En la terminal:

```bash
ls ~/.claude/skills/book-to-skill
```

Deberías ver `SKILL.md` y la carpeta `scripts`.

Dentro de Claude Code, al escribir `/` debería aparecer **`/book-to-skill`** en la lista.
Si no aparece, cierra y vuelve a abrir Claude Code.

---

## 6. Ejemplo de uso: convertir un libro en skill

Imagina que tienes un EPUB en tu carpeta de Descargas. Dentro de Claude Code escribe:

```
/book-to-skill ~/Downloads/mi-libro.epub
```

La skill te irá haciendo unas preguntas. Esto es lo que verás:

1. **¿Tipo de libro?** → *Técnico* (código/tablas) o *Texto* (prosa). Elige según tu libro.
2. **¿En qué idioma quieres la skill?** → elige **Español** y la skill se generará en
   español aunque el libro esté en inglés. *(Esta opción es la mejora propia de este fork.)*
3. **¿Para qué la quieres?** → aplicar los marcos del autor, pensar con sus modelos,
   consultar capítulos… (elige una o varias).
4. **Nombre de la skill** → te propondrá un nombre corto (un "slug"), p. ej. `cialdini-influence`.
5. Te mostrará una **estimación de coste y tiempo** y pedirá confirmación.

Al confirmar, Claude lee el libro y **genera todos los archivos de la skill**.

---

## 7. ¿Dónde están las skills generadas?

Cada libro convertido crea su propia carpeta en:

```
~/.claude/skills/<nombre-de-la-skill>/
├── SKILL.md          ← marcos clave + índice de capítulos
├── chapters/
│   ├── ch01-....md   ← un archivo por capítulo (se cargan solo cuando preguntas)
│   ├── ch02-....md
│   └── …
├── glossary.md       ← todos los términos clave
├── patterns.md       ← técnicas y patrones
└── cheatsheet.md     ← tablas de referencia rápida
```

Para verlas:

```bash
ls ~/.claude/skills
```

> 💡 Los archivos de capítulo **no consumen contexto** hasta que preguntas por ese tema.
> Por eso una skill puede cubrir un libro entero sin "ocupar" memoria de antemano.

---

## 8. ¿Cómo uso una skill generada?

Supón que la skill se llama `cialdini-influence`. En Claude Code:

```
/cialdini-influence
```
→ Carga los marcos principales para tenerlos a mano.

```
/cialdini-influence reciprocidad
```
→ Busca el tema "reciprocidad", abre el capítulo adecuado y te responde con el contenido real.

```
/cialdini-influence ch05
```
→ Entra directamente en el capítulo 5.

```
/cialdini-influence ¿qué capítulos tienes?
```
→ Te enseña el índice completo.

También puedes simplemente **escribirlo en lenguaje natural**: *"usa la skill
cialdini-influence para explicarme el principio de escasez"*.

---

## 9. Problemas frecuentes (FAQ)

**No aparece `/book-to-skill` en Claude Code.**
Cierra y vuelve a abrir Claude Code. Confirma que existe `~/.claude/skills/book-to-skill/SKILL.md`.

**Dice que falta una herramienta de extracción.**
Es normal: copia el comando `pip3 install …` que te indica y vuelve a lanzar la conversión.

**Mi PDF tarda mucho.**
Si elegiste modo *Técnico*, usa Docling (~1,5 s por página) para conservar tablas y código.
Para libros solo de prosa, elige *Texto*: es casi instantáneo.

**La skill me salió en inglés y la quería en español.**
Vuelve a generarla y, en la pregunta de idioma, elige **Español**. Esa pregunta es la
función añadida en este fork.

**Quiero usarlo en VS Code, Antigravity, Cursor…**
Se puede: la skill funciona en cualquier editor donde ejecutes Claude Code. Mira el
**apartado 1.5**. La vía que siempre funciona es abrir la **terminal integrada** del editor y
escribir `claude`. Ojo: la IA *propia* de esos editores (Gemini en Antigravity) no usa skills de
Claude Code.

**¿Puedo borrar una skill generada?**
Sí: borra su carpeta, p. ej. `rm -rf ~/.claude/skills/cialdini-influence`.

---

## 10. Chuleta (todo en 6 líneas)

```bash
# 1. Instalar Claude Code (necesita Node.js)
npm install -g @anthropic-ai/claude-code

# 2. Instalar la skill (ejemplo para EPUB; ajusta según tu formato)
pip3 install ebooklib beautifulsoup4
mkdir -p ~/.claude/skills/book-to-skill/scripts
curl -o ~/.claude/skills/book-to-skill/SKILL.md          https://raw.githubusercontent.com/cerebroetereo/book-to-skill/main/SKILL.md
curl -o ~/.claude/skills/book-to-skill/scripts/extract.py https://raw.githubusercontent.com/cerebroetereo/book-to-skill/main/scripts/extract.py
```

Luego, dentro de Claude Code:

```
/book-to-skill ~/ruta/a/tu-libro.epub      → genera la skill
/nombre-de-la-skill <tema>                 → la usas
```

---

*Esta guía pertenece al fork de [@cerebroetereo](https://github.com/cerebroetereo). Proyecto y
autor original: [book-to-skill](https://github.com/virgiliojr94/book-to-skill) de
[@virgiliojr94](https://github.com/virgiliojr94).*
