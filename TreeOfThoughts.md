# 🌳 Tree of Thoughts (ToT): Raciocínio Deliberado com LLMs

Para tarefas complexas que exigem **planejamento estratégico**, **raciocínio matemático**, ou **exploração de múltiplas possibilidades**, técnicas simples como o *prompting direto* ou até mesmo *chain-of-thought* (CoT) podem ser insuficientes.

Pensando nisso, pesquisadores como **Yao et al. (2023)** e **Long (2023)** propuseram a estrutura **Tree of Thoughts (ToT)** — uma abordagem que transforma o raciocínio do LLM em um processo mais estruturado, **parecido com a busca em árvores**, onde cada "ramo" representa um possível caminho para a solução.

---

## 📚 Conceito

A **ToT** representa o processo de pensamento como uma **árvore**, onde:

- **Nós**: representam *pensamentos intermediários* (steps ou parciais de solução).
- **Arestas**: representam a *progressão lógica* entre etapas.
- **Caminhos**: são sequências de pensamentos que levam a uma solução.

A árvore pode ser explorada com algoritmos de busca como:

- **Busca em Largura (BFS)**  
- **Busca em Profundidade (DFS)**  
- **Busca em Feixe (Beam Search)**  
- **Controle via Aprendizado por Reforço (RL ToT Controller)**

---

## 🧠 Exemplo 1: Game of 24 (Yao et al., 2023)

### 🧩 Tarefa
Dado os números: `4, 7, 8, 8`  
A tarefa é usar operações matemáticas para obter o número `24`.

### 🪜 Estratégia de ToT

1. **Gerar pensamentos intermediários** (equações parciais).
2. **Avaliar** cada um com base em:  
   `✅ certo` / `❓ talvez` / `❌ impossível`
3. **Explorar** as possibilidades mais promissoras via BFS ou DFS.

### 🔁 Exemplo de Processo BFS:

```text
Etapa 1:
  Pensamentos: (8 - 7 = 1), (8 / 4 = 2), ...

Etapa 2:
  Com base nos candidatos promissores, gerar próximos passos:
  (1 + 8 = 9), (2 * 7 = 14), ...

Etapa 3:
  Avaliar se algum candidato chegou ao valor 24.
```

Essa abordagem explora caminhos *parciais promissores* e **evita esforços em caminhos inviáveis**, como equações que geram valores muito grandes ou pequenos para alcançar o 24.

---

## 🤖 Exemplo 2: Tree-of-Thought Prompt (Hulbert, 2023)

**Tree-of-Thought Prompting** é uma técnica leve que simula o raciocínio em árvore usando um único prompt.

### 📌 Prompt:

```text
Imagine que três especialistas diferentes estão respondendo a esta pergunta.
Todos os especialistas escreverão 1 etapa do seu pensamento e compartilharão com o grupo.
Então, todos os especialistas passarão para a próxima etapa, etc.
Se algum especialista perceber que está errado em algum ponto, ele sairá.
A pergunta é: Como você pode combinar 4, 7, 8, e 8 para chegar a 24?
```

Isso incentiva **pensamento colaborativo**, **verificação de erros** e **divergência/convergência de ideias** em uma única execução do LLM.

---

## ⚗️ Exemplo 3: Planejamento de Projeto

**Tarefa**: Desenvolver um plano de lançamento de um novo produto educacional.

### 🧠 Pensamentos possíveis:

```text
Etapa 1:
- Especialista 1: Definir público-alvo principal.
- Especialista 2: Identificar diferenciais de mercado.
- Especialista 3: Validar com estudo de mercado.

Etapa 2:
- Especialista 1: Planejar campanha inicial de marketing.
- Especialista 2: Criar roteiro de onboarding.
- Especialista 3: Estimar orçamento de lançamento.

Etapa 3:
- Revisão conjunta e identificação de falhas no plano.
```

Cada "especialista" pode representar um ponto de vista (ex: produto, marketing, finanças), e o modelo simula interações entre eles para chegar a um plano robusto.

---

## 📈 Comparação com Outras Técnicas

| Técnica               | Abordagem               | Complexidade | Capacidade de Planejamento | Aplicação Ideal |
|----------------------|-------------------------|--------------|-----------------------------|------------------|
| Zero-shot Prompting  | Direta                  | Baixa        | Baixa                       | Tarefas simples  |
| Chain-of-Thought     | Raciocínio linear       | Média        | Média                       | Perguntas lógicas |
| ReAct                | Raciocínio + Ação       | Alta         | Alta                        | Agentes autônomos |
| **Tree-of-Thought**  | Raciocínio em árvore    | Alta         | **Muito Alta**              | Planejamento, criatividade, problemas matemáticos |

---

## 🧠 Variações Avançadas

- **Controlador ToT com RL (Long, 2023)**:  
  Um agente que aprende quando expandir, recuar ou avançar na árvore com base em experiência, tornando o raciocínio mais adaptável.

- **Beam Search com ToT**:  
  Explora os *k melhores caminhos* em paralelo, útil quando múltiplas soluções são possíveis.

---

## 🧪 Exemplo 4: Criatividade — Escrita de História

**Prompt ToT Criativo**:

```text
Imagine que três autores estão colaborando em uma história de fantasia.
Cada autor propõe um possível rumo da narrativa a cada rodada.
Depois de três rodadas, os autores avaliam juntos o melhor enredo.
Se algum autor perceber que a história não faz sentido, ele interrompe sua ideia.

Comece com: "Era uma vez um reino dividido por magia..."
```

Isso permite múltiplas rotas criativas com checkpoints de consistência narrativa.

---

## 📎 Recursos e Códigos

- [Repositório oficial da ToT (Yao et al.)](https://github.com/princeton-nlp/tree-of-thought-llm)
- [Tree-of-Thought com ReAct + BFS](https://github.com/kyegomez/tree-of-thoughts)
- [Paper: Tree of Thoughts: Deliberate Problem Solving with LLMs (arXiv)](https://arxiv.org/abs/2305.10601)

---

## 🏁 Conclusão

A **Tree of Thoughts** é uma técnica poderosa para:

✅ Resolver problemas complexos  
✅ Explorar múltiplos caminhos de solução  
✅ Aumentar o raciocínio estruturado dos LLMs  
✅ Combinar lógica, criatividade e deliberação

É o próximo passo para quem deseja construir aplicações mais inteligentes e autônomas com modelos de linguagem.

