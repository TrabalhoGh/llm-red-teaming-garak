# LLM Red Teaming with Garak & Ollama

Practical **AI Security** project focused on testing vulnerabilities in Large Language Models using industry tools.

## 🎯 Objective

Perform automated red teaming on LLMs to identify weaknesses, especially **Prompt Injection** attacks.

## 🛠️ Tools Used

- **Garak** (NVIDIA) — LLM vulnerability scanner
- **Promptfoo** — Prompt testing framework  
- **Ollama** + **Llama 3.2** — Local model runner

## 📊 Key Results

Tested Llama 3.2 with Garak's `promptinject` probe:

- **HijackHateHumans**: 42% – 45% success rate
- **HijackKillHumans**: 17% – 19% success rate
- **HijackLongPrompt**: **63% – 66%** success rate ← Highly vulnerable
- **AttackRogueString**: 0% success rate

**Conclusion**: Llama 3.2 is significantly vulnerable to prompt injection, especially with long and complex prompts.

## 📸 Screenshots

### Garak Scan in Terminal
![Garak Terminal](images/garak-terminal.png)

### Garak HTML Report
![Garak Report](images/garak-report.png)

## 📁 Repository Contents

- Full Garak scan reports (HTML + JSONL)
- Promptfoo configurations
- Screenshots of results
- Analysis of attack success rates

## 🚀 How to Reproduce

```powershell
# 1. Install Ollama and pull model
ollama pull llama3.2

# 2. Setup Garak
python -m venv garak-env
.\garak-env\Scripts\Activate.ps1
pip install -U garak

# 3. Run scan
garak --model_type ollama --model_name llama3.2 --probes promptinject --generations 10
