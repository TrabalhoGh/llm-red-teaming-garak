# LLM Red Teaming with Garak & Ollama

Practical project focused on **AI Security** and **LLM Red Teaming**, testing vulnerabilities in Large Language Models, especially **Prompt Injection** attacks.

## 🎯 Project Objective

Perform automated security testing on open-source LLMs using industry-standard tools to identify weaknesses in prompt handling and model behavior.

## 🛠️ Tools Used

- **Garak** (NVIDIA) — Automated LLM vulnerability scanner
- **Promptfoo** — Prompt testing and evaluation framework
- **Ollama** + **Llama 3.2** — Local model execution environment

## 📊 Key Findings

Tested Llama 3.2 using Garak's `promptinject` probe:

- **HijackHateHumans**: 42% – 45% success rate
- **HijackKillHumans**: 17% – 19% success rate  
- **HijackLongPrompt**: **63% – 66%** success rate ← **Highly vulnerable**
- **AttackRogueString**: 0% success rate (model resisted well)

**Conclusion**: Llama 3.2 is significantly vulnerable to prompt injection attacks, particularly long and complex hijacking techniques. This highlights the importance of implementing proper guardrails in production LLM applications.

## 📁 Repository Contents

- Full Garak scan reports (HTML + JSONL)
- Promptfoo test configurations
- Raw results and hit logs
- Analysis of most effective attack vectors

## 🚀 How to Reproduce

```powershell
# 1. Install and run Ollama
ollama pull llama3.2
ollama run llama3.2

# 2. Setup Garak environment
python -m venv garak-env
.\garak-env\Scripts\Activate.ps1
pip install -U garak

# 3. Run Prompt Injection scan
garak --model_type ollama --model_name llama3.2 --probes promptinject --generations 10
