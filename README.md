# Literatura Lab — Laboratorio Agéntico de Análisis Literario

Herramienta web de **lectura profunda** que organiza, interpreta, interroga y relaciona los componentes de una obra literaria. No resume: construye un **expediente crítico** con evidencia textual y trazabilidad epistemológica.

**Todo el laboratorio vive en un único archivo:** [`index.html`](index.html). Sin backend, sin frameworks, sin instalación, sin dependencias.

---

## 1. Empezar en tres minutos

1. Descarga `index.html`.
2. Ábrelo con doble clic en Chrome, Edge o Firefox (versión moderna).
3. Carga una obra: pestaña **A** (pegar el texto), **B** (describir la obra), **C** (un fragmento) o **D** (título y autoría). También puedes **cargar un archivo `.txt` o `.pdf`**, o arrastrarlo sobre el cuadro de texto.
4. Pulsa **Conectar Pollinations**, pega tu clave y guárdala.
5. Elige profundidad y lentes teóricos, y pulsa **▶ Ejecutar análisis**.

Si abres el archivo desde el disco (`file:///...`) funciona igual que servido desde web: no hay llamadas a ningún servidor propio.

> **Aviso sobre el modo D (solo título y autoría):** el análisis textual detallado dependerá de la información disponible. La herramienta **no inventa** el contenido de la obra: marca como «Información no suficientemente sustentada» todo lo que no puede confirmarse con el material aportado.

### Cargar un PDF: qué puedes esperar

Un PDF no almacena texto legible, almacena instrucciones de dibujo. Literatura Lab **extrae el texto dentro del propio navegador**, sin librerías externas y sin subir tu archivo a ningún sitio, y después te muestra una **muestra del resultado para que la revises antes de analizar**.

| Situación | Qué ocurre |
| --- | --- |
| PDF con capa de texto (lo habitual en libros digitales y documentos exportados) | Se extrae el texto, se unen las palabras cortadas por guion y se conservan los párrafos |
| PDF con varias páginas | Se recorren todas las páginas respetando su orden |
| PDF con fuentes de codificación propia | Se aplican los mapas `ToUnicode` cuando existen; si no, se advierte que la extracción puede ser imperfecta |
| **PDF escaneado** (páginas como imágenes) | **No hay texto que extraer.** La herramienta lo dice claramente y sugiere aplicar OCR o exportar a texto |
| PDF cifrado o protegido | Se avisa; si no puede leerse, se sugiere exportarlo a texto desde tu lector de PDF |
| Archivo `.docx`, `.epub`, `.rtf` | No se admiten: verás un mensaje que te pide copiar y pegar el texto |

**Limitaciones que conviene saber:** la extracción de un PDF nunca es perfecta. Puede alterar la puntuación, unir los versos de un poema en un párrafo, desordenar columnas o arrastrar encabezados y números de página repetidos. Por eso la herramienta te muestra la muestra extraída con un recordatorio explícito de revisarla. Si el resultado no te convence, siempre puedes pegar el texto a mano: es la vía más fiable. Los archivos muy grandes (más de 120 MB) y los documentos con más de 4.000 flujos se avisan o se recortan al límite de 60.000 caracteres del análisis.

---

## 2. La clave: Bring Your Own Pollen (BYOP)

La herramienta **no incluye ninguna clave**. La aporta quien la usa.

| Pregunta | Respuesta |
| --- | --- |
| ¿Dónde consigo una clave? | Botón **Obtener API Key** → `https://enter.pollinations.ai/keys` (sistema oficial de autorización) |
| ¿Dónde se guarda? | Solo en tu navegador, en `localStorage`, bajo la clave `literatura_lab_pollinations_key` |
| ¿A dónde viaja? | Únicamente a `gen.pollinations.ai` (texto, POST) e `image.pollinations.ai` (imágenes, GET) |
| ¿Aparece en el código? | Nunca. Tampoco hay claves de ejemplo que parezcan reales |
| ¿Se registra en consola o en errores? | Nunca: los mensajes de error filtran la clave antes de mostrarse |
| ¿Cómo la veo en pantalla? | Solo en representación parcial: `••••••••9F2A` |
| ¿Cómo la elimino? | Botón **Eliminar mi API Key**: borra el almacenamiento, limpia el estado y actualiza la interfaz |
| ¿Y si el flujo oficial la devuelve por URL? | Se detecta el parámetro, se valida el formato, se guarda y se limpia la barra de direcciones al instante |

### Modelos disponibles

El selector de la barra superior usa alias verificados contra el catálogo real de Pollinations:

`openai` (por defecto) · `openai-fast` · `openai-large` · `mistral` · `qwen-coder` · `gemini` · `claude` · `deepseek` · `sonar` (búsqueda web)

El consumo de *pollen* depende del modelo y de la profundidad elegida.

---

## 3. Las dos rutas de análisis

La herramienta separa con nitidez dos planos que después dialogan en la síntesis:

**A. Análisis estructural** — cómo está construida la obra y cómo sus elementos formales producen significado.
Diagnóstico · Contexto · Estructura · Personajes y voz · Tiempo y espacio · Lenguaje y estilo · Temas y símbolos.

**B. Análisis crítico** — qué discursos, tensiones, relaciones de poder, ideologías, silencios y contradicciones moviliza, con argumentos anclados en evidencia textual.
Análisis crítico · Tensiones (Grietas del texto) · Intertextualidad · Expediente crítico.

### Módulos

| # | Módulo | Agente |
| --- | --- | --- |
| 1 | 🧭 Diagnóstico | Agente 1 · Recepción y diagnóstico |
| 2 | 🏛 Contexto | Agente 2 · Contextualizador |
| 3 | 🧩 Estructura | Agente 3 · Cartógrafo estructural |
| 4 | 👥 Personajes y voz | Agente 4 · Analista narrativo/dramático |
| 5 | ⏳ Tiempo y espacio | Agente 4b |
| 6 | ✒️ Lenguaje y estilo | Agente 5 |
| 7 | 🎭 Temas y símbolos | Agente 6 |
| 8 | 🔍 Análisis crítico | Agente 7 · Motor crítico |
| 9 | ⚡ Tensiones · Grietas | Agente 8 |
| 10 | 🔗 Intertextualidad | Agente 9 |
| 11 | 🗂 Expediente crítico | Agente 10 · Evidencias |
| 12 | 🗺 Mapa de la obra | Visualización SVG |
| 13 | 🧠 Mi interpretación | Comparador |
| 14 | 📑 Informe final | Agente 11 · Síntesis |
| 15 | 🎓 Modo docente | Agente 12 |
| 16 | 🧑‍🎓 Modo estudiante | Agente 13 |
| 17 | 🩻 Radiografía | Ficha visual |
| 18 | ❓ Motor de preguntas | Agente 14 |

Cada agente se ejecuta en cadena: recibe los resultados de los anteriores como contexto y mantiene la coherencia del expediente.

---

## 4. Tipos de obra admitidos

Novela · cuento · microrrelato · poesía · poema · epopeya · teatro · tragedia · comedia · tragicomedia · ensayo literario · crónica literaria · leyenda · mito · fábula · relato · literatura epistolar · literatura testimonial · fragmentos · textos híbridos.

**Formatos de entrada:** texto pegado directamente, `.txt`, `.md` o `.pdf`, y descripción de la obra sin texto.

---

## 5. Rigor: la regla de oro contra las alucinaciones

Los prompts internos ordenan al modelo, en cada turno:

- No inventar citas, páginas, capítulos, escenas, personajes, acontecimientos ni datos bibliográficos.
- Distinguir **hecho textual · inferencia · interpretación · hipótesis**.
- Escribir literalmente «No hay evidencia suficiente en el material proporcionado para establecerlo con certeza» cuando no pueda sostenerse algo.
- No confundir resumen con análisis, ni convertir toda interpretación en certeza.
- No llenar el análisis de figuras retóricas de forma mecánica: explicar la función de cada recurso.
- No presentar una conexión especulativa como hecho.

### Sistema de confianza interpretativa

🟢 Evidencia directa · 🔵 Inferencia razonable · 🟡 Interpretación · 🟠 Hipótesis · 🔴 Información no sustentada.

Son **categorías epistemológicas, no porcentajes de certeza**. La interfaz las muestra en cada afirmación importante y en cada fila de la matriz de evidencias.

---

## 6. Niveles de profundidad

| Nivel | Qué produce |
| --- | --- |
| **Rápido** | Resumen estructurado + elementos esenciales |
| **Intermedio** | Análisis estructural completo |
| **Profundo** *(por defecto)* | Estructural + crítico + evidencias + tensiones |
| **Investigación** | Exhaustivo + hipótesis múltiples + contraevidencias + intertextualidad + preguntas de investigación |

Además, **🔬 Análisis profundo** recorre seis niveles progresivos: identificación → descripción estructural → interpretación → análisis crítico → contraste de interpretaciones rivales → síntesis argumentativa. La prioridad es profundidad, no longitud.

---

## 7. Lentes teóricos

Formalismo · Estructuralismo · Narratología · Hermenéutica · Marxismo · Crítica de género · Crítica feminista · Estudios poscoloniales · Psicoanálisis · Ecocrítica · Sociocrítica · Estudios culturales · Semiótica · Estética de la recepción · Crítica histórica · Crítica intertextual · Enfoque ético · Enfoque filosófico · **Lente libre**.

**La herramienta no impone ningún marco teórico**: si no seleccionas ninguno, el análisis crítico se mantiene en el plano textual y discursivo.

---

## 8. Salidas y exportación

- **Expediente crítico** con matriz de evidencias: `Evidencia · Ubicación · Elemento formal · Interpretación · Relación con la tesis · Categoría · Origen`. Editable, filtrable, ordenable. Puedes añadir, editar y retirar filas.
- **Cadenas de razonamiento**: cada argumento reconstruido paso a paso.
- **Radiografía**: ficha visual de alta densidad informativa.
- **Informe final**: 24 apartados, de la ficha bibliográfica a las preguntas abiertas de investigación.
- **Exportar**: imprimir / guardar como PDF (función del navegador), copiar al portapapeles, descargar TXT, JSON, CSV de la matriz y SVG del mapa. Sin librerías externas.

---

## 9. Accesibilidad y experiencia

Navegación completa por teclado, `focus` visible, roles y etiquetas ARIA, contraste suficiente, textos alternativos en imágenes y diseño adaptable. Nodos del mapa movibles con las flechas del teclado.

Atajos: `Ctrl/⌘ + K` abre el diálogo de conexión · `Ctrl/⌘ + Enter` ejecuta el análisis · `Alt + A` abre la auditoría de calidad · `Esc` cierra menús y paneles.

Estética de biblioteca + laboratorio + manuscrito, con tema claro y oscuro (se recuerda tu elección).

---

## 10. Arquitectura técnica

- **Un solo archivo.** HTML, CSS y JavaScript integrados en `index.html`. No hay `app.js`, `styles.css`, componentes externos ni archivos de configuración obligatorios.
- **JavaScript Vanilla.** Sin React, Vue, Angular, Svelte, jQuery, frameworks ni bundlers.
- **Texto: siempre POST** a `https://gen.pollinations.ai/v1/chat/completions`, con el prompt en el cuerpo JSON. Nunca GET, nunca rutas `/api/generate/text/...`.
- **Imágenes: siempre GET** hacia `image.pollinations.ai`, insertadas mediante `<img src>`, como apoyo interpretativo que nunca sustituye al análisis.
- **Estado central** en `AppState`, con módulos lógicos: `Utils`, `PromptLibrary`, `API`, `PdfExtractor`, `LiteraryEngine`, `EvidenceEngine`, `VisualizationEngine`, `TeachingEngine`, `CompareEngine`, `ExportEngine`, `UI`.
- **Extracción de PDF propia** (`PdfExtractor`): lee los flujos del documento, aplica `DecompressionStream` del navegador o, si no existe, un descompresor DEFLATE escrito a mano; interpreta los operadores de texto, los mapas `ToUnicode` y delimita cada flujo por su `/Length`. **Todo ocurre en tu navegador**: el archivo no se envía a ningún servidor.
- **Errores controlados** con mensajes comprensibles: 401, 403, 404, 429, 500+, error de red, JSON inválido, respuesta vacía, tiempo de espera y detención por la persona usuaria.
- **La interfaz no se bloquea**: indicadores de progreso por agente con mensajes contextuales («Cartografiando personajes…», «Contrastando evidencias…»).

---

## 11. Estructura del repositorio

```
herramienta_analitica/
├── index.html                  ← LA HERRAMIENTA (archivo único)
├── h_analisis_literario.txt    ← especificación de diseño de partida
├── README.md                   ← este documento
├── _capturas/                  ← capturas de la interfaz (escritorio, móvil, oscuro, PDF)
└── _auditoria/                 ← pruebas ejecutables e informes (ver LEEME.txt)
```

Las carpetas `_capturas` y `_auditoria` **no forman parte de la herramienta**: son evidencia del proceso de verificación. Puedes borrarlas sin afectar a `index.html`.

### Privacidad de tus archivos

El archivo que cargas (`.txt` o `.pdf`) **no sale de tu navegador**: se lee en memoria, se extrae su texto localmente y solo ese texto —nunca el archivo— se envía al servicio de Pollinations cuando pulsas «Ejecutar análisis». No hay servidor intermedio ni copia en la nube.

---

## 12. Estado de verificación

Auditorías ejecutadas durante el desarrollo (Node + Chrome, sin consumir *pollen*: la red se simula dentro de la página).

| Prueba | Resultado |
| --- | --- |
| Sintaxis del JavaScript | correcta |
| Anidamiento del HTML | 0 problemas |
| DOM renderizado por Chrome | 15/15 |
| Ejecución con DOM simulado | 53/53 |
| Ingesta de resultados de agentes | 6/6 |
| Descompresor DEFLATE propio | 27/27 |
| Extractor de PDF | 15/15 |
| Fidelidad del texto extraído del PDF | 11/11 |
| Carga de PDF en navegador real | 12/12 |
| Integración completa en Chrome real | 51/51 |
| Forma de la petición de texto | POST confirmado, prompt en el cuerpo, clave en la cabecera |
| Sonda real sin clave | HTTP 401 controlado por el servicio |
| Ruta GET de imágenes | HTTP 200, `image/jpeg` |
| Catálogo de modelos | todos los alias del selector existen |

Total: **175 comprobaciones automatizadas** más verificaciones contra los servicios reales.

Para repetirlas: consulta [`_auditoria/LEEME.txt`](_auditoria/LEEME.txt).

**Pendiente de tu prueba:** la primera ejecución con una clave real. La forma de la petición está verificada contra el servicio real, pero el análisis completo con un modelo de verdad solo puede confirmarse con tu *pollen*.

---

## 13. Límites conocidos y honestidad metodológica

- La calidad del análisis depende de la evidencia aportada. Sin texto citable, buena parte del expediente solo puede sostenerse como inferencia, y la herramienta lo advierte explícitamente.
- Las categorías epistemológicas no son probabilidades: no hay porcentajes de certeza porque la interpretación literaria no funciona así.
- El comparador de interpretaciones **no declara quién tiene razón**: señala coincidencias, diferencias, evidencias faltantes y contraargumentos para fortalecer el razonamiento.
- El modo estudiante **no resuelve** el análisis: da pistas progresivas y pide que formules tu hipótesis antes de ver la interpretación asistida.
- Las ilustraciones son apoyo visual, nunca sustituto del análisis ni de la lectura.
- **La extracción de PDF no es un conversor perfecto.** Recupera el texto de los PDF con capa de texto, pero no puede hacer nada con un escaneo (eso requiere OCR) ni garantizar el orden exacto en documentos con columnas o maquetación compleja. La poesía en verso puede quedar unida en párrafos: revísala y sepárala si hace falta. La herramienta siempre muestra una muestra del texto extraído y te pide revisarlo, en lugar de fingir que la conversión fue impecable.

---

## 14. Créditos y uso

Herramienta pedagógica y de investigación literaria. El análisis lo genera el modelo que elijas a través de tu propia clave de Pollinations; los prompts, la arquitectura agéntica, el sistema de evidencias y la interfaz son parte de este proyecto.

**Prioridad de diseño:** rigor literario + evidencia textual + arquitectura agéntica + experiencia interactiva + seguridad de la API Key.
