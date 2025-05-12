# Reflexion Framework

Reflexion é uma estrutura para reforçar agentes baseados em linguagem por meio de feedback linguístico. Segundo **Shinn et al. (2023)**:

> *"Reflexion is a new paradigm for ‘verbal‘ reinforcement that parameterizes a policy as an agent’s memory encoding paired with a choice of LLM parameters."*

## Visão Geral

Reflexion converte feedback (em linguagem livre ou escalar) do ambiente em *linguistic feedback* (também chamado de *self-reflection*), que é fornecido como contexto para o agente LLM no próximo episódio. Isso ajuda o agente a aprender com erros anteriores de maneira rápida e eficaz, levando a melhorias de desempenho em tarefas avançadas.

### Reflexion Framework

Como mostrado na figura do artigo, Reflexion consiste em **três modelos distintos**:

- **Ator (Actor)**: Gera texto e ações com base nas observações do estado. Utiliza modelos como *Chain-of-Thought (CoT)* e *ReAct* para isso. Um componente de memória também é adicionado para fornecer contexto adicional ao agente.

- **Avaliador (Evaluator)**: Atribui pontuações às saídas geradas pelo ator. Recebe como entrada uma trajetória gerada (também chamada de *short-term memory*) e gera uma pontuação de recompensa. Usa diferentes funções de recompensa, incluindo LLMs e heurísticas baseadas em regras para tarefas de tomada de decisão.

- **Autorreflexão (Self-Reflection)**: Gera dicas de reforço verbal para auxiliar o ator a se autoaperfeiçoar. Essa função é realizada por um LLM que utiliza o sinal de recompensa, a trajetória atual e a memória persistente para gerar feedback relevante e específico. Essas experiências são armazenadas em uma *long-term memory*, que é utilizada para melhorar rapidamente a tomada de decisão do agente.

### Etapas do Processo

1. Definir a tarefa  
2. Gerar uma trajetória  
3. Avaliar  
4. Realizar reflexão  
5. Gerar a próxima trajetória  

A Reflexion estende o framework ReAct ao introduzir **autoavaliação, autorreflexão e componentes de memória**.

---

## Resultados

Os resultados experimentais mostram que agentes com Reflexion melhoram significativamente seu desempenho em:

- Tarefas de tomada de decisão (*AlfWorld*)
- Questões de raciocínio (*HotPotQA*)
- Tarefas de programação em Python (*HumanEval*)

### Exemplos de Resultados

- **AlfWorld**: ReAct + Reflexion supera significativamente ReAct ao completar **130 de 134 tarefas**, usando técnicas de autoavaliação com heurísticas e GPT para classificação binária.

- **HotPotQA**: Reflexion + CoT supera abordagens baseadas apenas em CoT, mesmo ao usar apenas a trajetória recente como memória episódica.

- **Programação**: Reflexion supera abordagens anteriores em benchmarks como *MBPP*, *HumanEval* e *Leetcode Hard*.

---

## Quando Usar Reflexion?

Reflexion é mais adequado quando:

- O agente precisa aprender com tentativa e erro.
- Métodos tradicionais de *reinforcement learning* são impraticáveis (por exigirem muitos dados e ajustes de modelo).
- É necessário um feedback mais específico e detalhado.
- A interpretabilidade e a memória explícita são importantes para a tarefa.

### Tarefas Eficazes com Reflexion

- **Tomada de decisão sequencial**: Melhora o desempenho em *AlfWorld*.
- **Raciocínio**: Desempenho aprimorado em *HotPotQA*.
- **Programação**: Melhora na qualidade do código gerado, atingindo SOTA em alguns benchmarks.

---

## Limitações do Reflexion

- **Dependência da autoavaliação**: A precisão do feedback depende da capacidade do agente de avaliar corretamente seu desempenho.
- **Limitações da memória de longo prazo**: Atualmente usa janela deslizante com capacidade máxima; pode se beneficiar de estruturas avançadas como embeddings vetoriais ou bancos de dados SQL.
- **Limitações em geração de código**: Testes automatizados podem não capturar todas as variações possíveis (ex: funções não determinísticas ou dependentes de hardware).
