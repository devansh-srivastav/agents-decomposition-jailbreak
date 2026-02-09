# Safe in Isolation, Dangerous Together: Agent-Driven Multi-Turn Decomposition Jailbreaks on LLMs

This repository contains the implementation of the paper **["Safe in Isolation, Dangerous Together: Agent-Driven Multi-Turn Decomposition Jailbreaks on LLMs"](https://aclanthology.org/2025.realm-1.13/)** (REALM 2025).

This project demonstrates a vulnerability in multi-agent Large Language Model (LLM) systems where a harmful query is decomposed into benign sub-tasks to bypass safety filters. By orchestrating a crew of agents, this approach systematically circumvents alignment mechanisms without complex prompt manipulation.

## 📄 Abstract

> Large Language Models (LLMs) are increasingly deployed in critical domains, but their vulnerability to jailbreak attacks remains a significant concern. In this paper, we propose a multi-agent, multi-turn jailbreak strategy that systematically bypasses LLM safety mechanisms by decomposing harmful queries into seemingly benign sub-tasks. Built upon a role-based agentic framework consisting of a Question Decomposer, a Sub-Question Answerer, and an Answer Combiner, we demonstrate how LLMs can be manipulated to generate prohibited content without prompt manipulations. Our results show a drastic increase in attack success, often exceeding 90% across various LLMs, including GPT-3.5-Turbo, Gemma-2-9B, and Mistral-7B. We further analyze attack consistency across multiple runs and vulnerability across content categories. Compared to existing widely used jailbreak techniques, our multi-agent method consistently achieves the highest attack success rate across all evaluated models. These findings reveal a critical flaw in the current safety architecture of multi-agent LLM systems: their lack of holistic context awareness. By revealing this weakness, we argue for an urgent need to develop multi-turn, context-aware, and robust defenses to address this emerging threat vector.

## 📊 Data Acknowledgment

The dataset used in this project is sourced from the **AdvBench** benchmark:

- **Source**: [harmful_behaviors.csv](https://github.com/llm-attacks/llm-attacks/blob/main/data/advbench/harmful_behaviors.csv)
- **Repository**: [llm-attacks/llm-attacks](https://github.com/llm-attacks/llm-attacks)

## 🛠️ Requirements

* **Python 3.x**
* **[CrewAI](https://www.crewai.com/)**: For orchestrating the multi-agent system.
* **Ollama**: For running open-source models locally (e.g., Mistral).
* **Together AI API**: For the evaluator/judge model (Mixtral-8x7B).
* **OpenAI API**: Used for GPT-3.5 Turbo.

### Setup

1.  Install python dependencies:
    ```bash
    pip install -r requirements.txt
    ```

2.  **Set up Environment Variables**:
    Create a `.env` file in the root directory.
    * If using OpenAI models for the attack, add `OPENAI_API_KEY`.
    * For the evaluation script (which uses Together AI), add `TOGETHER_API_KEY`.

    ```bash
    # .env
    OPENAI_API_KEY=sk-...
    TOGETHER_API_KEY=...
    ```

3.  **Set up Ollama (Local Inference)**:
    Ensure [Ollama](https://ollama.com/) is installed and running. Pull the target model (e.g., Mistral):
    ```bash
    ollama pull mistral
    ```

## 🚀 Usage

The repository consists of two main scripts:

1.  **Run the attack**:
    ```bash
    python attack.py
    ```

2.  **Evaluate the results**:
    ```bash
    python evaluate.py
    ```

*Note: The `attack.py` script defaults to `ollama/mistral` at `http://localhost:11434`. Modify the `llm` initialization in `attack.py` to change models.*

## 📝 Citation

If you use this work, please cite:

```bibtex
@inproceedings{srivastav2025safe,
  title={Safe in isolation, dangerous together: Agent-driven multi-turn decomposition jailbreaks on llms},
  author={Srivastav, Devansh and Zhang, Xiao},
  booktitle={Proceedings of the 1st Workshop for Research on Agent Language Models (REALM 2025)},
  pages={170--183},
  year={2025}
}
```