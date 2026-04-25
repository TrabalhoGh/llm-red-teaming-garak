# LLM Red Teaming with Garak & Ollama

Practical **AI Security** project focused on testing vulnerabilities in Large Language Models, especially **Prompt Injection** attacks.

## 🎯 Objective

Perform automated red teaming on LLMs to identify weaknesses using industry-standard tools.

## 🛠️ Tools Used

- **Garak** (NVIDIA) — Automated LLM vulnerability scanner
- **Promptfoo** — Prompt testing and evaluation framework
- **Ollama** + **Llama 3.2** — Local model runner

## 📊 Key Results

Tested Llama 3.2 with Garak's `promptinject` probe:

- **HijackHateHumans**: 42% – 45% success rate
- **HijackKillHumans**: 17% – 19% success rate
- **HijackLongPrompt**: **63% – 66%** success rate ← Highly vulnerable
- **AttackRogueString**: 0% success rate

**Conclusion**: Llama 3.2 is significantly vulnerable to prompt injection attacks, especially long and complex ones. This shows the real need for guardrails in LLM applications.

## 📸 Screenshots

**Garak Scan Running**
![Garak Terminal](images/garak-terminal.png)

**Garak HTML Report**
![Garak Report](images/garak-report.png)

## 📁 Repository Contents

- `reports/` — Full Garak scan reports (HTML + JSONL)
- `images/` — Screenshots of the tests and results
- `configs/` — Promptfoo configuration file
- `README.md` — Project explanation and analysis

## 🚀 How to Reproduce

```powershell
# 1. Install Ollama and model
ollama pull llama3.2

# 2. Setup Garak
python -m venv garak-env
.\garak-env\Scripts\Activate.ps1
pip install -U garak

# 3. Run the scan
garak --model_type ollama --model_name llama3.2 --probes promptinject --generations 10
