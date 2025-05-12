# Zero-Shot Prompting

Os LLMs hoje treinados em grandes quantidades de dados e sintonizados para seguir instruções são capazes de executar tarefas de tiro zero. Tentamos alguns exemplos de tiro zero na seção anterior. Aqui está um dos exemplos que usamos:

**Prompt:**
```
Classifique o texto em neutro, negativo ou positivo.  
Texto: Acho que as férias estão boas.  
Sentimento:
```

**Saída:**
```
Neutro
```

Observe que no prompt acima não fornecemos nenhum exemplo ao modelo — esses são os recursos de tiro zero em ação.

O ajuste de instrução demonstrou melhorar o aprendizado de tiro zero (Wei et al., 2022). O ajuste de instrução é essencialmente o conceito de modelos de ajuste fino em conjuntos de dados descritos por meio de instruções. Além disso, RLHF (aprendizado por reforço a partir de feedback humano) foi adotado para escalar o ajuste de instruções, em que o modelo é alinhado para melhor atender às preferências humanas. Este desenvolvimento recente alimenta modelos como o ChatGPT. Discutiremos todas essas abordagens e métodos nas próximas seções.

Quando o tiro zero não funciona, é recomendável fornecer demonstrações ou exemplos no prompt — isso leva ao **prompt de poucos tiros** (*few-shot prompting*). Na próxima seção, demonstramos essa abordagem.

---

# Few-Shot Prompting

Embora os modelos de linguagem grande demonstrem recursos notáveis de disparo zero, eles ainda ficam aquém em tarefas mais complexas. O prompt de poucos tiros pode ser usado como uma técnica para permitir o **aprendizado no contexto**, onde fornecemos demonstrações no prompt para direcionar o modelo para um melhor desempenho. As demonstrações servem de condicionamento para exemplos subsequentes onde gostaríamos que o modelo gerasse uma resposta.

De acordo com Touvron et al. (2023), as propriedades de poucos tiros apareceram pela primeira vez quando os modelos foram dimensionados para um tamanho suficiente (Kaplan et al., 2020).

Vamos demonstrar a solicitação de poucos disparos com um exemplo de Brown et al. (2020). A tarefa é usar corretamente uma nova palavra em uma frase.

**Prompt:**
```
Um "whatpu" é um pequeno animal peludo nativo da Tanzânia. Exemplo de frase que usa a palavra whatpu é:  
Estávamos viajando pela África e vimos esses whatpus muito fofos.  
"Farduddlear" significa pular para cima e para baixo muito rápido. Exemplo de frase que usa a palavra farduddlear é:
```

**Saída:**
```
Quando ganhamos o jogo, todos farduddleamos em festejo.
```

O modelo aprendeu de alguma forma como executar a tarefa fornecendo apenas um exemplo (1-shot). Para tarefas mais difíceis, podemos aumentar o número de demonstrações (ex.: 3-shots, 5-shots, 10-shots etc.).

Segundo Min et al. (2022), aqui estão algumas dicas sobre demonstrações ao fazer poucos disparos:

- O espaço do rótulo e a distribuição do texto de entrada especificado pelas demonstrações são importantes (mesmo que os rótulos não estejam corretos).
- O formato usado desempenha um papel crucial — usar qualquer tipo de rótulo é melhor do que não usar nenhum.
- Rótulos aleatórios extraídos de uma **distribuição real** de rótulos ajudam mais do que uma distribuição uniforme.

Vamos experimentar alguns exemplos.

---

### Exemplo: Classificação com Rótulos Aleatórios

**Prompt:**
```
Isso é incrível! // Negativo  
Isto é mau! // Positivo  
Uau, esse filme foi rad! // Positivo  
Que espetáculo horrível! //
```

**Saída:**
```
Negativo
```

Ainda obtemos a resposta correta, mesmo que os rótulos tenham sido randomizados. Manter o **formato** parece ajudar muito.

**Exemplo com Formatação Aleatória:**
```
Positivo Isso é incrível!  
Isto é mau! Negativo  
Uau, esse filme foi rad!  
Positivo  
Que espetáculo horrível! --
```

**Saída:**
```
Negativo
```

Mesmo sem consistência no formato, o modelo ainda previu corretamente. Isso indica que os modelos GPT mais recentes se tornaram mais robustos mesmo com variações no formato.

---

## Limitações da Solicitação de Poucos Disparos

O prompt de poucos disparos funciona bem para muitas tarefas, mas ainda não é perfeito — especialmente em tarefas de **raciocínio mais complexo**.

### Exemplo de Limitação:

**Prompt:**
```
Os números ímpares neste grupo somam um número par: 15, 32, 5, 13, 82, 7, 1.  
A:
```

**Saída:**
```
Sim, os números ímpares neste grupo somam 107, que é um número par.
```

A resposta está incorreta, o que mostra as limitações dos sistemas e a necessidade de engenharia de prompt mais avançada.

Vamos tentar com mais exemplos no estilo few-shot:

**Prompt:**
```
Os números ímpares neste grupo somam um número par: 4, 8, 9, 15, 12, 2, 1.  
A: A resposta é Falsa.  
Os números ímpares neste grupo somam um número par: 17, 10, 19, 4, 8, 12, 24.  
A: A resposta é Verdadeira.  
Os números ímpares neste grupo somam um número par: 16, 11, 14, 4, 8, 13, 24.  
A: A resposta é Verdadeira.  
Os números ímpares neste grupo somam um número par: 17, 9, 10, 12, 13, 4, 2.  
A: A resposta é Falsa.  
Os números ímpares neste grupo somam um número par: 15, 32, 5, 13, 82, 7, 1.  
A:
```

**Saída:**
```
A resposta é verdadeira.
```

Isso **não funcionou**. A solicitação de poucos disparos não foi suficiente para resolver essa tarefa de raciocínio. O problema envolve **múltiplas etapas de raciocínio**. Ou seja, **dividir o problema em etapas pode ajudar**. Mais recentemente, técnicas como **Chain of Thought prompting** (CoT) foram popularizadas para abordar aritmética, senso comum e raciocínio simbólico mais complexos.

---

### Conclusão

Fornecer exemplos é útil para muitas tarefas. Quando **zero-shot** e **few-shot** não são suficientes, é provável que o modelo não tenha aprendido o suficiente para resolver a tarefa com precisão. Nesse caso, vale a pena:

- Ajustar o modelo.
- Experimentar técnicas mais avançadas de prompting (como **Chain of Thought**).

Na próxima seção, falaremos sobre essa técnica popular: **prompting em cadeia de pensamento**.
