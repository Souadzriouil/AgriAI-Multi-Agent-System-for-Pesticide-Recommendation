# 🌱 AgriAI — Multi-Agent System for Smart Pesticide Recommendation

> An AI-powered pipeline that analyzes pesticide products, assesses health and environmental risks, and recommends safer biological alternatives — built with Google Gemini, SerpAPI, LangChain, and Streamlit.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Problem Statement](#-problem-statement)
- [Multi-Agent Architecture](#-multi-agent-architecture)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Environment Variables](#-environment-variables)
- [Usage](#-usage)
- [Example Output](#-example-output)
- [Tests](#-tests)
- [Limitations](#-limitations)
- [Future Improvements](#-future-improvements)
- [Author](#-author)

---

## 🚀 Overview

**AgriAI** is an AI-powered multi-agent system designed to help farmers, agronomists, and decision-makers make smarter choices around pesticide use.

Given a pesticide name, the system automatically:
1. Searches for product information on the web
2. Extracts key product details
3. Analyzes health and environmental risks using an LLM
4. Finds biological or eco-friendly alternatives
5. Generates a structured recommendation report saved to `outputs/`

---

## 🎯 Problem Statement

Choosing the right pesticide is a complex, time-consuming, and potentially dangerous task. Farmers often face:

- Lack of clear and accessible information about pesticide composition
- Difficulty understanding health and environmental risks
- Limited knowledge of safer biological alternatives
- No centralized tool to automate this research

---

## 🧠 Multi-Agent Architecture

The system is composed of **5 specialized agents**, each responsible for a distinct step in the pipeline:

| Agent | File | Role |
|---|---|---|
| 🔎 **Product Lookup Agent** | `product_lookup.py` | Searches for pesticide info via SerpAPI |
| 📊 **Data Extraction Agent** | `data_extraction.py` | Parses and structures raw search results |
| ⚠️ **Risk Analysis Agent** | `risk_analysis.py` | Uses Google Gemini to assess health & environmental risks |
| 🌿 **Alternative Search Agent** | `alternative_search.py` | Finds biological or safer substitutes |
| 📝 **Report Generation Agent** | `report_generation.py` | Compiles all outputs into a final report |

### Pipeline Flow

```
User Input (Pesticide Name)
        ↓
Product Lookup Agent       ← SerpAPI (google_search.py)
        ↓
Data Extraction Agent
        ↓
Risk Analysis Agent        ← Google Gemini (LLM)
        ↓
Alternative Search Agent   ← SerpAPI (google_search.py)
        ↓
Report Generation Agent
        ↓
outputs/report_<name>.txt
```

---

## ⚙️ Tech Stack

| Technology | Package | Purpose |
|---|---|---|
| Python 3.x | — | Core language |
| Google Gemini | `google-generativeai` | LLM for risk analysis |
| SerpAPI | `google-search-results` | Web search for product & alternative lookup |
| LangChain | `langchain` | Agent orchestration |
| Streamlit | `streamlit` | Interactive web dashboard |
| python-dotenv | `python-dotenv` | Secure API key management |
| Pandas | `pandas` | Data handling |
| Matplotlib | `matplotlib` | Visualization |

---

## 📁 Project Structure

```
AgriAI/
│
├── config/
│   └── settings.py                  # API keys and global configuration
│
├── dashboard/
│   └── dashboard.py                 # Streamlit web UI
│
├── src/
│   ├── agents/
│   │   ├── product_lookup.py        # Agent 1: Search pesticide via SerpAPI
│   │   ├── data_extraction.py       # Agent 2: Extract & structure product details
│   │   ├── risk_analysis.py         # Agent 3: LLM-based risk assessment (Gemini)
│   │   ├── alternative_search.py    # Agent 4: Search for biological alternatives
│   │   └── report_generation.py     # Agent 5: Generate and save final report
│   │
│   └── utils/
│       └── google_search.py         # SerpAPI search utility
│
├── outputs/
│   └── report_glyphosate.txt        # Example generated report
│
├── tests/
│   ├── test_alternative_search.py
│   ├── test_data_extraction.py
│   ├── test_product_lookup.py
│   └── test_risk_analysis.py
│
├── .env                             # API keys (do NOT commit this)
├── .gitignore
├── main.py                          # CLI entry point
├── requirements.txt
└── README.md
```

---

## ⚡ Installation

**Prerequisites:** Python 3.8+

```bash
# 1. Clone the repository
git clone https://github.com/Souadzriouil/AgriAI-Multi-Agent-System-for-Pesticide-Recommendation.git
cd AgriAI-Multi-Agent-System-for-Pesticide-Recommendation

# 2. Create and activate a virtual environment
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt
```

---

## 🔐 Environment Variables

Create a `.env` file at the project root with the following keys:

```env
SERP_API_KEY=your_serpapi_key_here
GEMINI_API_KEY=your_gemini_api_key_here
```

> ⚠️ **Important:** Never commit your `.env` file. It is already listed in `.gitignore`. Get your keys at:
> - SerpAPI → [https://serpapi.com/](https://serpapi.com/)
> - Gemini API → [https://ai.google.dev/](https://ai.google.dev/)

---

## ▶️ Usage

### Run the CLI pipeline

```bash
python main.py
```

To analyze a different pesticide, edit `main.py`:

```python
product = "Glyphosate"  # Replace with any pesticide name
```

### Run the Streamlit dashboard

```bash
streamlit run dashboard/dashboard.py
```

Open `http://localhost:8501` in your browser.

---

## 📊 Example Output

The system was tested with **Glyphosate**. The generated report is saved at `outputs/report_glyphosate.txt`.

```
🔎 Searching for product: Glyphosate
✅ Product found: Glyphosate

⚠️  Risk Analysis:
  - Classified as a probable human carcinogen (IARC Group 2A)
  - Disrupts soil microbiome and aquatic ecosystems
  - Long-term exposure linked to kidney and liver stress

🌿 Recommended Alternatives:
  - Neem oil
  - Acetic acid-based herbicides
  - Corn gluten meal (natural pre-emergent)

📝 Report saved to: outputs/report_glyphosate.txt
✅ Report generated successfully!
```

---

## 🧪 Tests

Unit tests are available for the 4 core agents:

```bash
# Run all tests
python -m pytest tests/

# Run a specific test
python -m pytest tests/test_risk_analysis.py
```

| Test File | Covers |
|---|---|
| `test_product_lookup.py` | SerpAPI search and result retrieval |
| `test_data_extraction.py` | Product detail parsing logic |
| `test_risk_analysis.py` | Gemini LLM risk assessment output |
| `test_alternative_search.py` | Biological alternative search results |

---

## ⚠️ Limitations

- Output quality depends on SerpAPI search result relevance
- Gemini LLM responses may occasionally be imprecise — always verify with a qualified agronomist
- Not intended to replace professional agricultural or toxicological advice
- Currently only supports CLI input (single pesticide name at a time)

---

## 🧭 Future Improvements

- [ ] Add RAG (Retrieval-Augmented Generation) over a curated pesticide knowledge base
- [ ] Build a structured database of pesticides approved/banned by country
- [ ] Export reports as PDF
- [ ] Deploy as a public web app (Streamlit Cloud or HuggingFace Spaces)
- [ ] Support multilingual input/output (Arabic, French, English)
- [ ] Improve LLM explainability with cited sources

---

## 🤝 Contributing

Contributions are welcome!

```bash
git checkout -b feature/your-feature-name
git commit -m "feat: describe your change"
git push origin feature/your-feature-name
# Then open a Pull Request
```

---

## 📜 License

This project is for **educational and portfolio purposes**.

---

## 👩‍💻 Author

**Souad Zriouil**  
AI Engineer | Data Scientist | Machine Learning | NLP | LLM  

[![GitHub](https://img.shields.io/badge/GitHub-Souadzriouil-black?logo=github)](https://github.com/Souadzriouil)

---

⭐ If this project was useful or interesting, consider starring the repo!
