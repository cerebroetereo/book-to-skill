<h1 align="center">📚 Creación de skills basados en libros</h1>

<p align="center">
  <strong>Convierte cualquier libro o documento técnico en una skill de Claude Code — lista para estudiar, consultar y usar mientras trabajas.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Claude_Code-Skill-blueviolet?style=for-the-badge" alt="Claude Code Skill">
  <img src="https://img.shields.io/badge/PDF%20%E2%80%A2%20EPUB%20%E2%80%A2%20DOCX%20%E2%80%A2%20MD%20%E2%80%A2%20HTML%20%E2%80%A2%20RTF%20%E2%80%A2%20MOBI-supported-green?style=for-the-badge" alt="Formatos soportados">
  <img src="https://img.shields.io/badge/esfuerzo-alto-orange?style=for-the-badge" alt="Esfuerzo: alto">
  <img src="https://img.shields.io/badge/License-MIT-blue?style=for-the-badge" alt="Licencia MIT">
</p>

> ## 🔱 Fork de [`virgiliojr94/book-to-skill`](https://github.com/virgiliojr94/book-to-skill)
>
> **Autor original:** [@virgiliojr94](https://github.com/virgiliojr94) · **Este fork:** [@cerebroetereo](https://github.com/cerebroetereo)
>
> Este repositorio es una **copia del proyecto original** (con su historial completo). La **única modificación** es añadir **soporte de idioma de salida** en `SKILL.md`: ahora la skill generada puede escribirse en español (u otro idioma) aunque el libro esté en inglés. El resto de archivos (`scripts/extract.py`, etc.) son **idénticos al original**.
>
> 👉 Detalle de los cambios: [Cambios en este fork](#-cambios-en-este-fork-modifications) · *Esto es un fork — trabajo original de [@virgiliojr94](https://github.com/virgiliojr94); el único cambio es el soporte de idioma de salida añadido en `SKILL.md`.*

<p align="center">
  <a href="#-por-qué">Por qué</a> ·
  <a href="#-qué-genera">Qué genera</a> ·
  <a href="#-uso">Uso</a> ·
  <a href="#-requisitos">Requisitos</a> ·
  <a href="#-cómo-funciona">Cómo funciona</a> ·
  <a href="#-cambios-en-este-fork-modifications">Modificaciones</a> ·
  <a href="#-preguntas-frecuentes">FAQ</a> ·
  <a href="#-instalación">Instalación</a>
</p>

---

## 🤔 Por qué

Compras un gran libro técnico. Lo lees una vez. Tres meses después ni recuerdas que existía el capítulo 7.

Los apaños habituales no ayudan:
- 📄 "Voy a buscar en el PDF" → obtienes una lista de páginas, no respuestas
- 🧠 "Le pregunto a Claude sobre el libro" → o alucina o dice que no tiene el contenido
- 📝 "Tomaré notas mientras leo" → acabas con un documento de 200 líneas que no vuelves a abrir

**book-to-skill resuelve esto convirtiendo el libro en una skill estructurada que Claude carga bajo demanda.**

Una vez instalada, basta con escribir `/tu-libro-slug replication` y Claude lee el capítulo adecuado y responde con el contenido real. Sin alucinaciones. Sin rebuscar en PDFs. El libro pasa a formar parte de tu flujo de trabajo.

---

## 📦 Qué genera

Ejecutar `/book-to-skill tu-libro.pdf` (o `.epub`) crea una skill completa en `~/.claude/skills/<slug>/`:

| Archivo | Para qué sirve | Tamaño |
|---------|----------------|--------|
| `SKILL.md` | Modelos mentales clave + índice de capítulos | ~4.000 tokens |
| `chapters/ch01-*.md` … | Un archivo por capítulo, cargado bajo demanda | ~1.000 tokens cada uno |
| `glossary.md` | Todos los términos clave, ordenados alfabéticamente con referencias de capítulo | ~1.500 tokens |
| `patterns.md` | Todas las técnicas, algoritmos y patrones de diseño | ~2.000 tokens |
| `cheatsheet.md` | Tablas de decisión y reglas de referencia rápida | ~1.000 tokens |

**Los archivos de capítulo se cargan bajo demanda** — no cuentan contra el presupuesto de la skill hasta que preguntas por ese tema.

---

## 🚀 Uso

```
/book-to-skill <ruta-al-documento> [slug-nombre-skill]
```

Formatos de documento soportados: PDF, EPUB, DOCX, TXT, Markdown, reStructuredText, AsciiDoc, HTML, RTF, MOBI/AZW/AZW3.

**Ejemplos:**

```bash
# PDF — deriva el nombre de la skill del nombre del archivo
/book-to-skill ~/Downloads/designing-data-intensive-applications.pdf

# EPUB — especifica un slug personalizado
/book-to-skill ~/books/clean-code.epub clean-code

# Ruta completa con nombre explícito
/book-to-skill /tmp/ddd-evans.pdf domain-driven-design
```

Una vez creada la skill, úsala como cualquier otra skill de Claude Code:

```bash
/designing-data-intensive-apps                  # carga los modelos mentales principales
/designing-data-intensive-apps replication      # busca y explica un tema
/designing-data-intensive-apps ch05             # entra en el capítulo 5
/designing-data-intensive-apps "¿qué capítulos tienes?"
```

---

## 🔧 Requisitos

El extractor prueba las herramientas en orden para cada formato y usa la primera disponible. Si no hay ninguna instalada, te dice qué comando ejecutar. El texto plano, Markdown, reStructuredText y AsciiDoc no necesitan dependencias adicionales.

**PDF — elige según el tipo de libro:**

| Tipo de libro | Herramienta | Instalación | Velocidad |
|---------------|-------------|-------------|-----------|
| Mucho texto (prosa, pocas tablas) | `pdftotext` (poppler) | `sudo apt install poppler-utils` | ⚡ instantáneo |
| Reserva para texto | `PyPDF2` | `pip3 install PyPDF2` | ⚡ instantáneo |
| Reserva para texto | `pdfminer.six` | `pip3 install pdfminer.six` | ⚡ instantáneo |
| **Técnico (código, tablas, fórmulas)** | **`docling`** | `pip3 install docling` | ~1,5 s/página |

> Antes de empezar la extracción, la skill te pregunta si el libro es **técnico** o **de mucho texto** y elige la herramienta adecuada automáticamente. Docling conserva tablas y bloques de código en markdown; pdftotext es más rápido para libros solo de prosa.

**EPUB:**

| Herramienta | Instalación | Calidad |
|-------------|-------------|---------|
| `ebooklib` + `beautifulsoup4` | `pip3 install ebooklib beautifulsoup4` | ⭐⭐⭐ La mejor |
| `zipfile` (stdlib) | incluido — no requiere instalación | ⭐⭐ Siempre disponible |

**Otros formatos:**

| Formato | Herramienta | Instalación |
|---------|-------------|-------------|
| DOCX | `python-docx` (reserva: ZIP/XML de stdlib) | `pip3 install python-docx` |
| HTML | `beautifulsoup4` (reserva: `html.parser` de stdlib) | `pip3 install beautifulsoup4` |
| RTF | `striprtf` (reserva: regex) | `pip3 install striprtf` |
| MOBI / AZW / AZW3 | Calibre `ebook-convert` (app externa, no pip) | https://calibre-ebook.com/download |
| TXT / Markdown / reStructuredText / AsciiDoc | incluido | — |

---

## ⚙️ Cómo funciona

```
PDF o EPUB
     │
     ▼
Step 1.5 — "¿Libro técnico o de mucho texto?"
     │
     ├── técnico → Docling  (tablas + bloques de código como markdown, ~1,5 s/página)
     └── texto   → pdftotext → PyPDF2 → pdfminer  (instantáneo)
     │
     ▼
scripts/extract.py --mode <technical|text>
  EPUB → ebooklib → zipfile (stdlib)
     │
     ├── /tmp/book_skill_work/full_text.txt
     └── /tmp/book_skill_work/metadata.json
               │
               ▼
          Claude analiza la estructura
          (título, autor, capítulos, índice)
               │
               ▼
          Genera resúmenes por capítulo  (800–1.200 tokens cada uno)
          técnico → incluye secciones de Ejemplos de código + Tablas de referencia
          Genera glossary, patterns, cheatsheet
          Genera el SKILL.md maestro con los modelos mentales clave
               │
               ▼
          ~/.claude/skills/<slug>/  ✅ escrito
          /tmp/book_skill_work/     🗑️  limpiado
```

**Benchmark de extracción** (libro técnico de 103 páginas, solo CPU):

| Método | Tiempo | Tokens | Tablas | Bloques de código |
|--------|--------|--------|--------|-------------------|
| pdftotext | 0,1 s | 27K | 0 | 0 |
| Docling | 164 s | 27K (+1,2 %) | 48 | 36 |

<details>
<summary>Principios de diseño (clic para desplegar)</summary>

1. **Densidad sobre exhaustividad** — un resumen de 1.000 tokens supera a un extracto de 10.000
2. **Voz de practicante** — "Usa X cuando Y", no "El libro explica X"
3. **SKILL.md con lo importante delante** — la compactación conserva los primeros ~5.000 tokens; lo más importante va primero
4. **Capítulos bajo demanda** — el índice de temas le dice a Claude qué archivo leer; los capítulos se cargan solo cuando hacen falta
5. **Nunca texto en bruto** — siempre sintetizar, resumir, extraer la señal de la fuente

</details>

---

## ❓ Preguntas frecuentes

**"¿No puedo simplemente meter el PDF/EPUB en el contexto de mi proyecto de Claude?"**

Puedes — pero cada conversación gastará ese presupuesto de tokens por adelantado. Un libro de 400 páginas son ~200K tokens. Con una skill, solo se cargan los capítulos relevantes para tu pregunta. El resto se queda en disco hasta que lo necesitas.

Más importante aún: inyectar texto en bruto es *recuperación*. Una skill es *razonamiento*. Cuando cargas un archivo de capítulo, Claude no busca coincidencias de palabras clave — trabaja con marcos, principios y modelos mentales ya extraídos y nombrados, estructurados para aplicarlos, no para leerlos.

---

**"¿Esto no es simplemente RAG?"**

RAG funciona en el momento de la consulta: trocea el libro → lo incrusta todo → busca vectores similares → lo inyecta en el prompt. Está optimizado para "encuéntrame la parte que habla de X".

book-to-skill funciona en el momento de la compilación: una única pasada de análisis profundo extrae los marcos reales del autor, los nombra, describe cuándo usar cada uno y captura los antipatrones. El resultado es la estructura que el autor tardó años en construir — no una búsqueda por similitud sobre sus frases.

RAG responde: *"aquí tienes fragmentos cercanos a tu consulta."*  
Una skill responde: *"aquí tienes los 12 marcos que construyó este autor, listos para razonar con ellos."*

Para buscar entre más de 50 libros, gana RAG. Para profundizar en un libro y usar sus marcos mientras trabajas, gana una skill.

---

**"Los libros populares ya están en los datos de entrenamiento de Claude. ¿Para qué molestarse?"**

Para libros muy conocidos (Clean Code, DDIA, Pragmatic Programmer), Claude tiene conocimiento general — pero está comprimido, promediado entre toda la discusión de internet sobre el libro, y puede alucinar citas concretas o ubicaciones de capítulos.

book-to-skill funciona a partir de tu copia real. Cada nombre de marco, cada lista de antipatrones, cada número de capítulo está anclado en el texto que proporcionaste. Sin deriva de los datos de entrenamiento, sin títulos de capítulo alucinados.

También brilla con libros que Claude no conoce en absoluto: referencias técnicas de nicho, documentación interna de empresa, publicaciones recientes, obras traducidas.

---

**"NotebookLM gestiona mejor varios libros."**

Totalmente cierto — si tu flujo es "tengo 80 libros y quiero buscar en todos a la vez", NotebookLM es la herramienta adecuada.

book-to-skill está hecho para otro trabajo: quieres profundizar en un libro y tener sus marcos integrados en tu flujo de programación o escritura, no en una pestaña aparte del navegador. Es menos "búsqueda en biblioteca" y más "el autor sentado a tu lado mientras trabajas".

---

## 📥 Instalación

> 🇪🇸 **Guías en español:**
> - [**Guía de instalación paso a paso (para principiantes)**](GUIA-INSTALACION.md) — instalar Claude Code, Python y las herramientas de extracción, un ejemplo de uso y dónde aparecen las skills generadas.
> - [**Guía de prompts: cómo exprimir una skill-libro**](GUIA_PROMPTS_SKILL.md) — plantillas de preguntas para sacar el máximo a una skill ya generada.

Pega esto en tu sesión de Claude Code:

```
Instala book-to-skill (este fork): https://raw.githubusercontent.com/cerebroetereo/book-to-skill/main/SKILL.md
```

O manualmente:

```bash
mkdir -p ~/.claude/skills/book-to-skill/scripts

curl -o ~/.claude/skills/book-to-skill/SKILL.md \
  https://raw.githubusercontent.com/cerebroetereo/book-to-skill/main/SKILL.md

curl -o ~/.claude/skills/book-to-skill/scripts/extract.py \
  https://raw.githubusercontent.com/cerebroetereo/book-to-skill/main/scripts/extract.py
```

> Estos comandos instalan **este fork** — `SKILL.md` incluye el soporte de idioma de salida; `extract.py` es idéntico al original. Para instalar el **original**, reemplaza `cerebroetereo/book-to-skill/main` por `virgiliojr94/book-to-skill/master`.

Después, en cualquier sesión de Claude Code:

```bash
/book-to-skill ~/ruta/a/tu-libro.pdf
# o
/book-to-skill ~/ruta/a/tu-libro.epub
```

---

## 🔀 Cambios en este fork (modifications)

Respecto al original de [@virgiliojr94](https://github.com/virgiliojr94), este fork añade **soporte de idioma de salida** en `SKILL.md`. Son **5 adiciones** (46 líneas, 0 borrados); ningún otro archivo cambia.

| # | Dónde | Qué añade |
|---|-------|-----------|
| 1 | Nuevo **Step 4.5 — Ask output language** | Pregunta (vía `AskUserQuestion`) en qué idioma debe escribirse la skill resultante y fija ese **TARGET LANGUAGE** como instrucción permanente para toda la tarea. |
| 2 | **Step 7** (capítulos) | Recordatorio de escribir cada capítulo en el idioma destino y **propagarlo a los subagentes** (no lo heredan). |
| 3 | **Step 8** (glossary / patterns / cheatsheet) | Misma regla de idioma para los archivos de apoyo. |
| 4 | **Step 9** (SKILL.md generado) | El cuerpo y el `description:` se escriben en el idioma destino; `name`, rutas y `allowed-tools` quedan en inglés/ASCII. |
| 5 | **Quality Rules → regla 9** | *"Honor the target language"*: traduce la prosa y las cabeceras, pero preserva nombres de frameworks, código y rutas. |

**Por qué:** el original generaba la skill en inglés (o en el idioma del libro). Con estos cambios puedes leer un libro en inglés y obtener una skill **íntegramente en español**, evitando que los subagentes reviertan en silencio al inglés — la causa más común de traducciones incompletas.

Lo que **no** cambia: `scripts/extract.py`, el flujo de extracción, los formatos soportados y el resto del comportamiento del original.

---

## 📁 Estructura del repositorio

```
book-to-skill/
├── SKILL.md              # Definición de la skill + instrucciones paso a paso
├── scripts/
│   └── extract.py        # Extracción (pdftotext / PyPDF2 / pdfminer / ebooklib / zipfile / Calibre)
├── GUIA-INSTALACION.md   # Guía de instalación para principiantes (español)
├── GUIA_PROMPTS_SKILL.md # Guía de prompts para exprimir las skills (español)
├── LICENSE.md            # Licencia MIT
└── README.md             # Este archivo
```

---

## 🙏 Créditos

- **Proyecto y autor original:** [book-to-skill](https://github.com/virgiliojr94/book-to-skill) de [@virgiliojr94](https://github.com/virgiliojr94).
- **Este fork:** [@cerebroetereo](https://github.com/cerebroetereo) — añade únicamente el soporte de idioma de salida descrito arriba.

El mérito del diseño original corresponde a su autor; este fork se limita a una mejora puntual sobre `SKILL.md`.

## Licencia

MIT — ver [LICENSE.md](LICENSE.md). El copyright original pertenece al autor upstream ([@virgiliojr94](https://github.com/virgiliojr94)); este fork mantiene la misma licencia MIT.

## Historial de estrellas

<a href="https://www.star-history.com/?repos=virgiliojr94%2Fbook-to-skill&type=date&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=virgiliojr94/book-to-skill&type=date&theme=dark&legend=top-left" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=virgiliojr94/book-to-skill&type=date&legend=top-left" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=virgiliojr94/book-to-skill&type=date&legend=top-left" />
 </picture>
</a>
