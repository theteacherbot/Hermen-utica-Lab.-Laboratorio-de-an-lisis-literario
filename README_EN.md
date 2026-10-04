# Literatura Lab — Agentic Literary Analysis Laboratory

A web tool for **deep reading** that organizes, interprets, questions, and relates the components of a literary work. It does not summarize: it builds a **critical dossier** with textual evidence and epistemic traceability.

**The entire laboratory lives in a single file:** [`index.html`](index.html). No backend, no frameworks, no installation, no dependencies.

---

## 1. Get started in three minutes

1. Download `index.html`.
2. Open it by double-clicking it in Chrome, Edge, or Firefox (modern version).
3. Load a work: tab **A** (paste the text), **B** (describe the work), **C** (a fragment), or **D** (title and authorship). You can also **load a `.txt` or `.pdf` file**, or drag it onto the text box.
4. Click **Connect Pollinations**, paste your key, and save it.
5. Choose the depth and theoretical lenses, then click **▶ Run analysis**.

If you open the file directly from disk (`file:///...`), it works just as it does when served from the web: there are no calls to any proprietary server.

> **Notice about mode D (title and authorship only):** detailed textual analysis will depend on the available information. The tool does not invent the content of the work: it marks anything that cannot be confirmed from the supplied material as «Information not sufficiently supported».

### Loading a PDF: what to expect

A PDF does not store readable text; it stores drawing instructions. Literatura Lab **extracts the text inside the browser itself**, without external libraries and without uploading your file anywhere, and then shows you a sample of the result so you can review it before analysis.

| Situation | What happens |
| --- | --- |
| PDF with a text layer (common in digital books and exported documents) | The text is extracted, words split by hyphenation are joined, and paragraphs are preserved |
| PDF with multiple pages | All pages are processed in their original order |
| PDF with custom font encoding | `ToUnicode` maps are applied when available; otherwise, a warning indicates that extraction may be imperfect |
| **Scanned PDF** (pages as images) | **There is no text to extract.** The tool states this clearly and suggests applying OCR or exporting to text |
| Encrypted or protected PDF | A warning is displayed; if it cannot be read, the tool suggests exporting it to text from your PDF reader |
| `.docx`, `.epub`, `.rtf` file | Not supported: a message asks you to copy and paste the text |

**Limitations worth knowing:** PDF extraction is never perfect. It may alter punctuation, join the lines of a poem into a paragraph, scramble columns, or carry over repeated headers and page numbers. That is why the tool displays the extracted sample with an explicit reminder to review it. If the result is not satisfactory, you can always paste the text manually: this is the most reliable method. Very large files (over 120 MB) and documents with more than 4,000 streams are flagged or truncated to the 60,000-character analysis limit.

---

## 2. The key: Bring Your Own Pollen (BYOP)

The tool **does not include any key**. The person using it provides the key.

| Question | Answer |
| --- | --- |
| Where do I get a key? | **Get API Key** button → `https://enter.pollinations.ai/keys` (official authorization system) |
| Where is it stored? | Only in your browser, in `localStorage`, under the key `literatura_lab_pollinations_key` |
| Where does it travel? | Only to `gen.pollinations.ai` (text, POST) and `image.pollinations.ai` (images, GET) |
| Does it appear in the code? | Never. There are no example keys that look real either |
| Is it logged to the console or errors? | Never: error messages filter the key before displaying it |
| How is it shown on screen? | Only in partial form: `••••••••9F2A` |
| How do I delete it? | **Delete my API Key** button: clears storage, resets the state, and updates the interface |
| What if the official flow returns it in the URL? | The parameter is detected, its format is validated, it is stored, and the address bar is immediately cleaned |

### Available models

The top-bar selector uses aliases verified against the actual Pollinations catalog:

`openai` (default) · `openai-fast` · `openai-large` · `mistral` · `qwen-coder` · `gemini` · `claude` · `deepseek` · `sonar` (web search)

*Pollen* consumption depends on the selected model and depth.

---

## 3. The two analysis paths

The tool clearly separates two dimensions that later interact in the synthesis:

**A. Structural analysis** — how the work is constructed and how its formal elements produce meaning.  
Diagnosis · Context · Structure · Characters and voice · Time and space · Language and style · Themes and symbols.

**B. Critical analysis** — which discourses, tensions, power relations, ideologies, silences, and contradictions it mobilizes, with arguments anchored in textual evidence.  
Critical analysis · Tensions (Cracks in the text) · Intertextuality · Critical dossier.

### Modules

| # | Module | Agent |
| --- | --- | --- |
| 1 | 🧭 Diagnosis | Agent 1 · Reception and diagnosis |
| 2 | 🏛 Context | Agent 2 · Contextualizer |
| 3 | 🧩 Structure | Agent 3 · Structural cartographer |
| 4 | 👥 Characters and voice | Agent 4 · Narrative/dramatic analyst |
| 5 | ⏳ Time and space | Agent 4b |
| 6 | ✒️ Language and style | Agent 5 |
| 7 | 🎭 Themes and symbols | Agent 6 |
| 8 | 🔍 Critical analysis | Agent 7 · Critical engine |
| 9 | ⚡ Tensions · Cracks | Agent 8 |
| 10 | 🔗 Intertextuality | Agent 9 |
| 11 | 🗂 Critical dossier | Agent 10 · Evidence |
| 12 | 🗺 Work map | SVG visualization |
| 13 | 🧠 My interpretation | Comparator |
| 14 | 📑 Final report | Agent 11 · Synthesis |
| 15 | 🎓 Teacher mode | Agent 12 |
| 16 | 🧑‍🎓 Student mode | Agent 13 |
| 17 | 🩻 X-ray | Visual profile |
| 18 | ❓ Question engine | Agent 14 |

Each agent runs in sequence: it receives the results of previous agents as context and maintains the coherence of the dossier.

---

## 4. Types of works supported

Novel · short story · flash fiction · poetry · poem · epic · drama · tragedy · comedy · tragicomedy · literary essay · literary chronicle · legend · myth · fable · narrative · epistolary literature · testimonial literature · fragments · hybrid texts.

**Input formats:** text pasted directly, `.txt`, `.md`, or `.pdf`, and a description of the work without the full text.

---

## 5. Rigor: the golden rule against hallucinations

The internal prompts instruct the model, on every turn, to:

- Never invent quotations, pages, chapters, scenes, characters, events, or bibliographic data.
- Distinguish **textual fact · inference · interpretation · hypothesis**.
- Write literally «There is not enough evidence in the provided material to establish this with certainty» whenever something cannot be supported.
- Do not confuse summary with analysis, or turn every interpretation into certainty.
- Do not mechanically fill the analysis with rhetorical devices: explain the function of each device.
- Do not present a speculative connection as a fact.

### Interpretive confidence system

🟢 Direct evidence · 🔵 Reasonable inference · 🟡 Interpretation · 🟠 Hypothesis · 🔴 Unsupported information.

These are **epistemological categories, not percentages of certainty**. The interface displays them for each important claim and in every row of the evidence matrix.

---

## 6. Depth levels

| Level | What it produces |
| --- | --- |
| **Quick** | Structured summary + essential elements |
| **Intermediate** | Complete structural analysis |
| **Deep** *(default)* | Structural + critical + evidence + tensions |
| **Research** | Exhaustive + multiple hypotheses + counterevidence + intertextuality + research questions |

In addition, **🔬 Deep analysis** progresses through six levels: identification → structural description → interpretation → critical analysis → comparison of competing interpretations → argumentative synthesis. The priority is depth, not length.

---

## 7. Theoretical lenses

Formalism · Structuralism · Narratology · Hermeneutics · Marxism · Gender criticism · Feminist criticism · Postcolonial studies · Psychoanalysis · Ecocriticism · Sociocriticism · Cultural studies · Semiotics · Reception aesthetics · Historical criticism · Intertextual criticism · Ethical approach · Philosophical approach · **Free lens**.

**The tool does not impose any theoretical framework**: if you select none, the critical analysis remains at the textual and discursive level.

---

## 8. Outputs and export

- **Critical dossier** with evidence matrix: `Evidence · Location · Formal element · Interpretation · Relation to thesis · Category · Origin`. Editable, filterable, sortable. You can add, edit, and remove rows.
- **Reasoning chains**: each reconstructed argument step by step.
- **X-ray**: high-density visual profile.
- **Final report**: 24 sections, from the bibliographic profile to open research questions.
- **Export**: print / save as PDF (browser function), copy to clipboard, download TXT, JSON, CSV of the matrix, and SVG of the map. No external libraries.

---

## 9. Accessibility and experience

Full keyboard navigation, visible `focus`, ARIA roles and labels, sufficient contrast, alternative text for images, and responsive design. Map nodes can be moved with the keyboard arrows.

Shortcuts: `Ctrl/⌘ + K` opens the connection dialog · `Ctrl/⌘ + Enter` runs the analysis · `Alt + A` opens the quality audit · `Esc` closes menus and panels.

Library + laboratory + manuscript aesthetic, with light and dark themes (your choice is remembered).

---

## 10. Technical architecture

- **Single file.** HTML, CSS, and JavaScript integrated into `index.html`. No `app.js`, `styles.css`, external components, or mandatory configuration files.
- **Vanilla JavaScript.** No React, Vue, Angular, Svelte, jQuery, frameworks, or bundlers.
- **Text: always POST** to `https://gen.pollinations.ai/v1/chat/completions`, with the prompt in the JSON body. Never GET, never `/api/generate/text/...` routes.
- **Images: always GET** to `image.pollinations.ai`, inserted through `<img src>`, as interpretive support that never replaces the analysis.
- **Central state** in `AppState`, with logical modules: `Utils`, `PromptLibrary`, `API`, `PdfExtractor`, `LiteraryEngine`, `EvidenceEngine`, `VisualizationEngine`, `TeachingEngine`, `CompareEngine`, `ExportEngine`, `UI`.
- **Own PDF extraction** (`PdfExtractor`): reads the document streams, uses the browser's `DecompressionStream` or, if unavailable, a hand-written DEFLATE decompressor; interprets text operators, `ToUnicode` maps, and delimits each stream using its `/Length`. **Everything happens in your browser**: the file is not sent to any server.
- **Controlled errors** with understandable messages: 401, 403, 404, 429, 500+, network error, invalid JSON, empty response, timeout, and user-initiated stop.
- **The interface does not lock up**: progress indicators by agent with contextual messages («Mapping characters…», «Cross-checking evidence…»).

---

## 11. Repository structure

```text
literature_analysis_tool/
├── index.html                  ← THE TOOL (single file)
├── h_literary_analysis.txt    ← initial design specification
├── README.md                   ← this document
├── _screenshots/              ← interface screenshots (desktop, mobile, dark, PDF)
└── _audit/                     ← executable tests and reports (see README.txt)
```

The `_screenshots` and `_audit` folders **are not part of the tool**: they are evidence of the verification process. You can delete them without affecting `index.html`.

### Privacy of your files

The file you load (`.txt` or `.pdf`) **does not leave your browser**: it is read in memory, its text is extracted locally, and only that text —never the file itself— is sent to the Pollinations service when you click «Run analysis». There is no intermediary server or cloud copy.

---

## 12. Verification status

Audits performed during development (Node + Chrome, without consuming *pollen*: the network is simulated inside the page).

| Test | Result |
| --- | --- |
| JavaScript syntax | correct |
| HTML nesting | 0 problems |
| DOM rendered by Chrome | 15/15 |
| Execution with simulated DOM | 53/53 |
| Agent result ingestion | 6/6 |
| Custom DEFLATE decompressor | 27/27 |
| PDF extractor | 15/15 |
| Fidelity of extracted PDF text | 11/11 |
| PDF loading in a real browser | 12/12 |
| Full integration in real Chrome | 51/51 |
| Text request format | POST confirmed, prompt in body, key in header |
| Real probe without a key | HTTP 401 controlled by the service |
| Image GET route | HTTP 200, `image/jpeg` |
| Model catalog | all selector aliases exist |

Total: **175 automated checks** plus verification against the real services.

To repeat them: see [`_audit/README.txt`](_audit/README.txt).

**Pending your test:** the first execution with a real key. The request format has been verified against the real service, but full analysis with an actual model can only be confirmed with your *pollen*.

---

## 13. Known limitations and methodological honesty

- Analysis quality depends on the evidence provided. Without citable text, much of the dossier can only be supported as inference, and the tool explicitly warns you about this.
- Epistemological categories are not probabilities: there are no certainty percentages because literary interpretation does not work that way.
- The interpretation comparator **does not declare who is right**: it identifies similarities, differences, missing evidence, and counterarguments in order to strengthen reasoning.
- Student mode **does not solve** the analysis: it provides progressive clues and asks you to formulate your hypothesis before seeing the assisted interpretation.
- Illustrations are visual support, never a substitute for analysis or reading.
- **PDF extraction is not a perfect converter.** It retrieves text from PDFs with a text layer, but it cannot do anything with a scan (that requires OCR), nor can it guarantee exact order in documents with columns or complex layouts. Poetry in verse may be joined into paragraphs: review it and separate it if necessary. The tool always displays a sample of the extracted text and asks you to review it rather than pretending the conversion was flawless.

---

## 14. Credits and use

Pedagogical and literary research tool. The analysis is generated by the model you choose through your own Pollinations key; the prompts, agentic architecture, evidence system, and interface are part of this project.

**Design priority:** literary rigor + textual evidence + agentic architecture + interactive experience + API Key security.
