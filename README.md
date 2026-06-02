# QuantumMind – Agentic RAG Quantum Physics Tutor

An AI-powered quantum physics study assistant built with LangGraph, LangChain, and ChromaDB. Features a 9-node agentic StateGraph with retrieval-augmented generation, self-reflection evaluation loops, a quantum physics calculator, and persistent sliding-window memory.

---

## Demo

> *"What is the Heisenberg uncertainty principle?"*
> *"Calculate the de Broglie wavelength of an electron at 2×10⁶ m/s"*
> *"I'm confused about wave-particle duality, can you explain again?"*

The agent detects the intent, retrieves relevant knowledge, runs a faithfulness evaluation, and responds as **Quanta** — a friendly quantum physics tutor.

---

## Architecture

```
User Input
    │
    ▼
[Memory Node]      ← sliding window, name detection, confusion/analogy flags
    │
    ▼
[Router Node]      ← LLM classifies: retrieve / tool / memory_only
    │
    ├──► [Retrieval Node]     ← ChromaDB semantic search, top-3 chunks
    ├──► [Tool Node]          ← quantum calculator (10 formulas, 0% hallucination)
    └──► [Skip Node]          ← no retrieval needed
    │
    ▼
[Viz Selector Node]   ← maps topic → HTML visualization file
    │
    ▼
[Answer Node]         ← LLM generates grounded response (Quanta persona)
    │
    ▼
[Eval Node]           ← faithfulness scoring, 2-retry self-reflection loop
    │
    ├──► RETRY → [Answer Node]
    └──► PASS  → [Save Node] → END
```

**9 nodes · 3 conditional routing paths · 2-retry self-reflection loop**

---

## Features

| Feature | Details |
|---|---|
| Agentic StateGraph | 9-node LangGraph graph with conditional routing |
| RAG Knowledge Base | 20 documents across 5 quantum physics topic layers |
| Semantic Retrieval | Top-3 chunks per query using ChromaDB + SentenceTransformer |
| Quantum Calculator | 10 physics formulas with step-by-step solutions |
| Self-Reflection | Faithfulness eval loop with up to 2 retries |
| Sliding Window Memory | Last 6 messages preserved across unlimited turns |
| Confusion Detection | Simplifies explanation when student signals confusion |
| RAGAS Evaluation | Faithfulness 0.85+ across 5 benchmark question pairs |

---

## Quantum Calculator — Supported Formulas

| # | Formula | Description |
|---|---|---|
| 1 | E = hf | Photon energy from frequency |
| 2 | E = hc/λ | Photon energy from wavelength |
| 3 | λ = h/mv | de Broglie wavelength |
| 4 | Eₙ = -13.6/n² eV | Hydrogen energy levels |
| 5 | ΔE = E_upper - E_lower | Energy level transitions |
| 6 | KE = hf - Φ | Photoelectric effect |
| 7 | Δx·Δp ≥ ℏ/2 | Heisenberg uncertainty principle |
| 8 | f = c/λ | Frequency from wavelength |
| 9 | E = hf | Planck energy |
| 10 | L = nℏ | Bohr angular momentum |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Agentic Framework | LangGraph, LangChain |
| LLM | Groq (llama-3.3-70b-versatile) |
| Vector Database | ChromaDB |
| Embeddings | SentenceTransformer (all-MiniLM-L6-v2) |
| Frontend | Streamlit |
| Evaluation | RAGAS (Faithfulness, AnswerRelevancy, ContextPrecision) |
| Language | Python 3.12 |

---

## Knowledge Base — Topics Covered

- What is Quantum Physics and Why It Exists
- History and Timeline of Quantum Physics
- Key Scientists of Quantum Physics
- Quantum Physics in Modern Technology
- Blackbody Radiation and the Ultraviolet Catastrophe
- The Photoelectric Effect
- Wave-Particle Duality — Concept and Experiments
- Wave-Particle Duality — de Broglie Hypothesis and Maths
- Bohr Model of the Atom — Concept and Revolution
- Bohr Model — Energy Formula and Calculations
- Schrödinger Equation — What It Means Simply
- Schrödinger Equation — Time Dependent and Independent Forms
- Wave Function and Probability — What ψ Really Means
- Wave Function — Normalisation and Common Misconceptions
- Heisenberg Uncertainty Principle — Intuition and Meaning
- Heisenberg Uncertainty Principle — Formula and Calculations
- Quantum Superposition — What It Really Means
- Quantum Superposition — Measurement, Collapse and Interpretations
- Quantum Tunnelling — Concept and Intuition
- Quantum Tunnelling — Applications and Real World Impact

---

## Getting Started

### Prerequisites

```bash
pip install langchain langchain-groq langgraph chromadb sentence-transformers streamlit ragas datasets langchain-huggingface python-dotenv
```

### Environment Setup

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
```

Get a free Groq API key at [console.groq.com](https://console.groq.com)

### Run

```bash
# Run the Jupyter notebook
jupyter notebook quantummind.ipynb

# Or launch the Streamlit app
streamlit run app.py
```

---

## Evaluation Results

Evaluated using RAGAS on 5 benchmark quantum physics questions:

| Metric | Score |
|---|---|
| Faithfulness | 0.85+ |
| Answer Relevancy | ~0.80-0.90 |
| Context Precision | ~0.75-0.85 |

The self-reflection eval loop targets a faithfulness threshold of **0.70** with up to **2 retries** before saving the answer.

---

## Project Structure

```
QuantumMind/
├── quantummind.ipynb     # Main notebook — full pipeline
├── app.py                # Streamlit frontend (if applicable)
├── .env                  # API keys (not committed)
├── .gitignore
├── requirements.txt
└── README.md
```

---

## Author

**Shivam Prasad**
B.Tech CSE
[GitHub](https://github.com/Shin001-dot) · shivampr2004@gmail.com

*NOTE: This is project is underdevelopment it just need 3-D model for the topics so that it can provide better understanding to students
