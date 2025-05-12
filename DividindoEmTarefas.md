# Prompt Chaining: Dividindo Tarefas para Maior Controle e Confiabilidade

Uma técnica importante de engenharia de prompt é dividir uma tarefa em subtarefas menores. Ao fazer isso, você pode criar uma **cadeia de prompts** (prompt chaining), onde a saída de um prompt serve como entrada para o próximo.

Isso é especialmente útil quando lidamos com **tarefas complexas**, nas quais um único prompt grande não é suficiente para produzir resultados confiáveis. Cada prompt da cadeia pode realizar transformações ou processamentos adicionais até que o resultado final seja alcançado.

---

## Benefícios do Prompt Chaining

✅ Maior confiabilidade  
✅ Melhoria no desempenho  
✅ Transparência no fluxo de raciocínio  
✅ Facilidade para **debug** e melhorias graduais  
✅ Melhor **personalização** e experiência do usuário  

Prompt chaining é particularmente eficaz em **assistentes conversacionais LLM-powered**.

---

## Exemplo: Prompt Chaining para QA com Documentos

Imagine que queremos responder a uma pergunta baseada em um documento longo. Em vez de tentar fazer tudo com um único prompt, dividimos a tarefa:

1. **Prompt 1:** extrai as citações relevantes do documento.
2. **Prompt 2:** responde à pergunta usando essas citações e o conteúdo original.

---

### Prompt 1: Extração de Citações Relevantes

```text
Você é um assistente prestativo. Sua tarefa é ajudar a responder a uma pergunta com base em um documento.  
O primeiro passo é extrair citações relevantes do documento, delimitado por ####.  
Forneça a lista de citações usando a tag <quotes></quotes>.  
Responda com "No relevant quotes found!" se nenhuma citação for encontrada.

####
{{document}}
####
```

> **Exemplo de Saída de Prompt 1:**

```xml
<quotes>
- Chain-of-thought (CoT) prompting[27]
- Generated knowledge prompting[37]
- Least-to-most prompting[38]
- Self-consistency decoding[39]
- Complexity-based prompting[41]
- Self-refine[42]
- Tree-of-thought prompting[43]
- Maieutic prompting[45]
- Directional-stimulus prompting[46]
- Textual inversion and embeddings[59]
- Using gradient descent to search for prompts[61][62][63][64]
- Prompt injection[65][66][67]
</quotes>
```

---

### Prompt 2: Gerar Resposta com Base nas Citações

```text
Dado um conjunto de citações relevantes (delimitado por <quotes></quotes>) extraídas de um documento e o documento original (delimitado por ####), componha uma resposta à pergunta.  
Certifique-se de que a resposta seja precisa, com tom amigável e útil.

####
{{document}}
####
<quotes>
- Chain-of-thought (CoT) prompting[27]
- Generated knowledge prompting[37]
- Least-to-most prompting[38]
- Self-consistency decoding[39]
- Complexity-based prompting[41]
- Self-refine[42]
- Tree-of-thought prompting[43]
- Maieutic prompting[45]
- Directional-stimulus prompting[46]
- Textual inversion and embeddings[59]
- Using gradient descent to search for prompts[61][62][63][64]
- Prompt injection[65][66][67]
</quotes>
```

> **Exemplo de Saída de Prompt 2:**

```text
As técnicas de prompting mencionadas no documento incluem:
1. Chain-of-thought (CoT) prompting[27]
2. Generated knowledge prompting[37]
3. Least-to-most prompting[38]
4. Self-consistency decoding[39]
5. Complexity-based prompting[41]
6. Self-refine[42]
7. Tree-of-thought prompting[43]
8. Maieutic prompting[45]
9. Directional-stimulus prompting[46]
10. Textual inversion and embeddings[59]
11. Using gradient descent to search for prompts[61][62][63][64]
12. Prompt injection[65][66][67]

Cada uma dessas técnicas aplica estratégias únicas para melhorar ou orientar a interação com modelos de linguagem para produzir os resultados desejados.
```

---

## Exercício Sugerido

Como exercício adicional, você pode criar um prompt intermediário na cadeia que **remove as citações numéricas** (ex: [27]) da resposta antes de enviá-la ao usuário final.

---

## Conclusão

Prompt chaining é uma técnica poderosa e modular que:

- Aumenta a performance e confiabilidade de aplicações com LLMs
- Facilita o rastreamento e ajustes de erros
- Melhora a personalização e experiência do usuário final

Explore mais sobre essa abordagem e outros métodos avançados nos nossos cursos de IA.  
Use o código **PROMPTING20** para obter **20% de desconto** na inscrição!

