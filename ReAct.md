# 📚 ReAct: Raciocínio + Ação com LLMs (Yao et al., 2022)

Yao et al., 2022 introduziram uma estrutura chamada **ReAct**, onde modelos de linguagem de larga escala (LLMs) são utilizados para gerar tanto *raciocínios* quanto *ações específicas da tarefa* de maneira intercalada.

---

## 💡 Motivação

* **Raciocínios (Thoughts)** permitem que o modelo induza, acompanhe e atualize planos de ação, além de lidar com exceções.
* **Ações (Actions)** permitem a interação com fontes externas, como bases de conhecimento e ambientes.

O ReAct permite que LLMs:

* Interajam com ferramentas externas para recuperar informações adicionais.
* Produzam respostas mais confiáveis e factuais.
* Sejam mais interpretáveis e confiáveis por humanos.

> 🔍 A melhor abordagem, segundo os autores, é a combinação de **ReAct com Chain-of-Thought (CoT)**, pois permite o uso do conhecimento interno e da informação externa adquirida ao longo do raciocínio.

---

## ⚙️ Como Funciona?

ReAct inspira-se nas sinergias entre **agir** e **raciocinar**, como os humanos fazem ao aprender novas tarefas e tomar decisões.

* **CoT** mostrou que LLMs conseguem realizar raciocínios aritméticos e de senso comum, mas sua falta de acesso ao mundo externo limita sua eficácia.
* **ReAct** é uma abordagem geral que **combina raciocínio e ação**.

Com ReAct:

1. O modelo gera traços de raciocínio (*Thoughts*).
2. Executa ações (*Actions*).
3. Recebe observações (*Observations*) do ambiente externo.
4. Revisa o raciocínio com base nessas observações.

---

## 🧠 Exemplo: HotPotQA

```text
Pergunta:
Aside from the Apple Remote, what other devices can control the program Apple Remote was originally designed to interact with?

Trajetória:

Thought 1: I need to search Colorado orogeny...
Action 1: Search[Colorado orogeny]
Observation 1: The Colorado orogeny was an episode of mountain building...
Thought 2: It does not mention the eastern sector...
Action 2: Lookup[eastern sector]
Observation 2: The eastern sector extends into the High Plains...
Thought 3: ...I need to search High Plains and find its elevation range.
...
Final Thought: ...so the answer is 1,800 to 7,000 ft.
Action 5: Finish[1,800 to 7,000 ft]
```

---

## 📊 Resultados: Tarefas de Conhecimento

Avaliação em tarefas como:

* 🔎 **HotPotQA** (perguntas complexas com múltiplos contextos)
* ✅ **FEVER** (verificação de fatos)

> Base model: **PaLM-540B**

### 🟢 Resultados:

* ReAct supera *Act* puro em ambas as tarefas.
* Supera o *CoT* em **FEVER**.
* Fica atrás de *CoT* em **HotPotQA** (devido à rigidez estrutural).

---

## 🎯 Resultados: Tarefas de Tomada de Decisão

ReAct também foi avaliado em:

* 🕹️ **ALFWorld** (jogo baseado em texto)
* 🛒 **WebShop** (ambiente de e-commerce)

> Esses ambientes exigem decomposição de metas e exploração.

ReAct teve melhor desempenho que *Act* por permitir:

* Raciocínio durante a decomposição de metas.
* Melhor alinhamento com ações necessárias no ambiente.

---

## ✏️ Exemplo de Prompt ReAct (HotPotQA)

```text
Question: What is the elevation range for the area that the eastern sector of the Colorado orogeny extends into?

Thought 1: I need to search Colorado orogeny...
Action 1: Search[Colorado orogeny]
Observation 1: The Colorado orogeny was...
...
Final Answer: 1,800 to 7,000 ft.
```

---

## 🛠️ Exemplo Prático com LangChain + ReAct

```python
!pip install --upgrade openai langchain python-dotenv google-search-results

# Importação
import openai, os
from langchain.llms import OpenAI
from langchain.agents import load_tools, initialize_agent
from dotenv import load_dotenv
load_dotenv()

# Configuração
os.environ["OPENAI_API_KEY"] = os.getenv("OPENAI_API_KEY")
os.environ["SERPER_API_KEY"] = os.getenv("SERPER_API_KEY")

llm = OpenAI(model_name="text-davinci-003", temperature=0)
tools = load_tools(["google-serper", "llm-math"], llm=llm)
agent = initialize_agent(tools, llm, agent="zero-shot-react-description", verbose=True)

# Execução
agent.run("Who is Olivia Wilde's boyfriend? What is his current age raised to the 0.23 power?")
```

### 🔗 Resultado:

```text
Final Answer: Harry Styles, Olivia Wilde's boyfriend, is 29 years old and his age raised to the 0.23 power is 2.169459462491557.
```

---

## 📌 Conclusão

* ReAct melhora **precisão factual**, **interpretação** e **interação com ambientes**.
* A estrutura Thought → Action → Observation é útil para decompor problemas complexos.
* Ideal para tarefas que exigem **pesquisa externa**, **planejamento iterativo** ou **resolução em múltiplas etapas**.
