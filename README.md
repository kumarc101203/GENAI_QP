# GenAIQuestionGen

**Automatic Question Paper Generation using Large Language Models**

A browser-based AI-powered tool that generates VTU-pattern examination questions with Bloom's Taxonomy tagging and CO/PO mapping — no server, no installation, just open and use.

---

## What It Does

A student or faculty member enters:
- **Subject** (e.g., Machine Learning, Data Structures, Thermodynamics)
- **Unit/Module** (1–5)
- **Difficulty** (Easy / Medium / Hard)

The system generates:
- Questions of **different marks grades** (5, 7, 8, 10 marks)
- Each tagged with **Bloom's Taxonomy level** (L1–L6)
- Each mapped to a **Course Outcome (CO)**
- Phrased in authentic **VTU examination style**

---

## Features

| Feature | Description |
|---------|-------------|
| **Quick Generate** | Pick subject, unit, difficulty → get multi-mark questions instantly |
| **Full Paper Mode** | Generate a complete 10-question VTU paper (5 modules × 2 OR questions) |
| **Bloom's Taxonomy** | Every question tagged with cognitive level (Remember → Create) |
| **CO/PO Mapping** | Maps each question to relevant Course Outcome |
| **Syllabus-Grounded** | Upload or paste syllabus — AI generates strictly from that content |
| **Past Paper Style** | Upload previous VTU papers — AI mimics their phrasing and difficulty |
| **Multi-Subject** | Works for any subject: CSE, ECE, Mechanical, Civil, etc. |
| **PDF Export** | Print or save as PDF directly from browser |
| **Multi-Provider** | Supports multiple free LLM APIs (OpenCode Zen, Gemini, OpenRouter, Groq) |
| **No Backend** | Runs entirely in the browser — no server, no database, no installation |

---

## Gen AI Concepts Used

### 1. Prompt Engineering
- Carefully structured system prompts with VTU examiner persona
- Constraint-based generation (exact marks totals, Bloom level targeting, CO alignment)
- Few-shot learning via past paper style reference
- Structured JSON output enforcement for reliable parsing

### 2. LLM Customization
- Multi-provider abstraction (OpenAI-compatible, Anthropic, Gemini formats)
- Temperature-controlled generation for question diversity
- Model selection flexibility (free and paid options)
- Retry logic with tolerant JSON parsing for reliability

---

## Dataset Inputs

| Dataset | How to Provide | Purpose |
|---------|---------------|---------|
| **Syllabus Document** | Upload PDF/DOCX/TXT or paste text | Grounds questions in approved curriculum |
| **Previous VTU Papers** | Upload past paper file or paste questions | Style, tone, and difficulty calibration |
| **Course Outcomes** | Type in CO definitions (CO1, CO2, ...) | Enables CO mapping on generated questions |
| **Subject Metadata** | Fill in subject, branch, semester, code | Context for the AI examiner |

---

## How to Run

### Prerequisites
- A modern web browser (Chrome, Firefox, Edge)
- An API key from any supported provider (free options available)

### Steps

1. **Open** `demo.html` in your browser (double-click the file)

2. **Configure API** (one-time setup):
   - Click the ⚙️ icon (top-right corner, faint gray)
   - Select provider: **OpenCode Zen (Free)** is recommended
   - Paste your API key
   - Close the panel

3. **Generate Questions**:
   - Enter your subject name, branch, semester
   - Select the module/unit number
   - Choose difficulty level
   - Check which marks values you want (5, 7, 8, 10)
   - Paste or upload your syllabus content for that module
   - (Optional) Paste or upload past VTU questions as style reference
   - (Optional) Add Course Outcomes for CO mapping
   - Click **"⚡ Generate Questions"**

4. **View & Export**:
   - Generated questions appear on the right panel
   - Each question shows Marks, Bloom's Level (L1–L6), and CO code
   - Click **"🖨️ Print / PDF"** to save as PDF

---

## Getting a Free API Key

### Option 1: OpenCode Zen (Recommended)
- Go to [opencode.ai](https://opencode.ai)
- Sign up and get a free API key
- Select model: `grok-code` (free)

### Option 2: Google Gemini
- Go to [aistudio.google.com/apikey](https://aistudio.google.com/apikey)
- Click "Create API Key" (free, 1500 requests/day)
- Select model: `gemini-2.0-flash`

### Option 3: OpenRouter
- Go to [openrouter.ai](https://openrouter.ai)
- Sign up and get API key
- Select model: `deepseek/deepseek-chat-v3.1:free`

---

## Supported Subjects

This tool is subject-agnostic. It works for any VTU course by changing the subject field:

| Department | Example Subjects |
|-----------|-----------------|
| **CSE** | Machine Learning, Data Structures, DBMS, OS, CN |
| **ECE** | Network Analysis, Signals & Systems, VLSI, DSP |
| **Mechanical** | Thermodynamics, Mechanics of Materials, Heat Transfer, Design of Machine Elements |
| **Civil** | Strength of Materials, Structural Analysis, Fluid Mechanics |
| **ISE** | Software Engineering, Cloud Computing, Big Data |

---

## Two Modes of Operation

### ⚡ Quick Generate (Default)
For generating individual unit-wise questions:
- Input: Subject + Unit + Difficulty
- Output: One question each for 5, 7, 8, 10 marks
- Use case: CIE preparation, practice question banks, quick drafts

### 📄 Full Paper
For generating a complete VTU-format examination paper:
- Input: Full syllabus (all 5 modules) + paper metadata
- Output: 10 questions (2 per module, OR alternatives), 100 marks total
- Use case: Model papers, mock exams, CIE papers
- Follows authentic VTU CBCS layout with USN boxes, marks/Bloom/CO columns

---

## Output Format

### Quick Generate Output
```
Q.No | Label | Question Text                          | Marks | Bloom | CO
-----|-------|----------------------------------------|-------|-------|----
Q.1  |       | Define machine learning and list...    |   5   |  L1   | CO1
Q.2  | a     | Explain the bias-variance tradeoff...  |   4   |  L2   | CO1
     | b     | Illustrate with a diagram...           |   3   |  L3   | CO1
Q.3  | a     | Compare supervised and unsupervised... |   4   |  L4   | CO2
     | b     | Apply k-fold cross validation...       |   4   |  L3   | CO2
Q.4  | a     | Derive the gradient descent update...  |   5   |  L4   | CO3
     | b     | Implement for a given dataset...       |   5   |  L3   | CO3
```

### Full Paper Output
- Authentic VTU CBCS format with:
  - College name and affiliation
  - USN boxes and subject code
  - Semester and examination title
  - Time/marks header
  - Numbered instructions
  - Module-wise question table with M (Marks), L (Bloom Level), C (CO) columns
  - OR separators between alternative questions

---

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     BROWSER (Client-side)                 │
│                                                          │
│  ┌──────────┐  ┌───────────┐  ┌──────────────────────┐ │
│  │  UI Layer │  │  Prompt   │  │  Output Renderer     │ │
│  │  (HTML/   │──│  Engine   │──│  (VTU Paper Format)  │ │
│  │   CSS)    │  │           │  │                      │ │
│  └──────────┘  └─────┬─────┘  └──────────────────────┘ │
│                       │                                  │
│  ┌────────────────────┴──────────────────────────────┐  │
│  │          LLM Gateway (fetch API)                   │  │
│  │  Supports: OpenAI, Anthropic, Gemini, Groq, etc.  │  │
│  └────────────────────┬──────────────────────────────┘  │
└───────────────────────┼──────────────────────────────────┘
                        │ HTTPS
                        ▼
              ┌─────────────────────┐
              │   LLM API Provider  │
              │   (Cloud-hosted)    │
              └─────────────────────┘
```

**No backend server required.** The entire application runs in the browser. API calls go directly from the browser to the LLM provider.

---

## File Structure

```
qp/
├── demo.html       # Complete application (single file)
├── README.md       # This file
└── .gitignore      # Tracks only demo.html and README
```

---

## Technical Details

| Aspect | Detail |
|--------|--------|
| **Language** | HTML + CSS + Vanilla JavaScript (no framework) |
| **Dependencies** | mammoth.js (DOCX parsing), pdf.js (PDF parsing) — loaded from CDN |
| **Storage** | localStorage for API key persistence |
| **LLM Communication** | Direct browser fetch() to provider APIs |
| **Output Parsing** | Tolerant JSON parser (handles markdown fences, partial JSON) |
| **File Support** | PDF, DOCX, TXT, HTML, RTF, CSV, MD |
| **Print** | CSS @media print rules for clean PDF export |

---

## Bloom's Taxonomy Levels

The system classifies questions into VTU's standard cognitive levels:

| Level | Code | Typical Verbs | Example |
|-------|------|--------------|---------|
| Remember | L1 | Define, list, state, recall | "Define machine learning" |
| Understand | L2 | Explain, describe, classify | "Explain bias-variance tradeoff" |
| Apply | L3 | Calculate, solve, implement | "Apply KNN algorithm to classify..." |
| Analyze | L4 | Compare, derive, differentiate | "Analyze the effect of learning rate..." |
| Evaluate | L5 | Justify, assess, critique | "Evaluate SVM vs Random Forest for..." |
| Create | L6 | Design, formulate, propose | "Design a neural network architecture..." |

---

## Limitations

- Requires internet connection (for LLM API calls)
- API key must be configured before first use
- Generated questions should be reviewed by faculty before use in actual exams
- Free API tiers have rate limits (typically 1500 requests/day)
- No persistent question bank (each session is independent)
- No automated solvability verification for numerical questions

---

## Future Enhancements

- Question bank with history and favorites
- Automated validation (syllabus relevance scoring, similarity detection)
- Multi-language support
- Diagram/figure generation for engineering questions
- Answer key and marking scheme generation
- Constraint-based paper assembly (OR-Tools solver)
- Faculty review and approval workflow

---

## Credits

**Developed by:** Shramic Networks 
**Course:** BCS602 — Generative AI (NITTTR Assignment)  
**Primary Reference Subject:** BCS701 — Machine Learning  
**Target University:** Visvesvaraya Technological University (VTU), Belagavi

---

## License

Academic project — for educational and demonstration purposes.
