# Prompt de Conhecimento Gerado (GENKNOW)

> Fonte: Liu et al. (2022)  
> ![Imagem de referência](Image Source: Liu et al. 2022)

Com o avanço dos Modelos de Linguagem de Grande Escala (LLMs), tornou-se popular **incorporar conhecimento externo** nos prompts para melhorar a precisão das respostas. 

Mas e se o modelo puder **gerar conhecimento antes de fazer uma previsão**?

Essa é a proposta de Liu et al. (2022): **gerar conhecimento como parte do processo de raciocínio**, especialmente útil em tarefas que exigem **raciocínio de senso comum**.

---

## Problema

### Prompt inicial:

```
Parte do golfe é tentar obter um total de pontos mais alto do que outros. Sim ou não?
```

### Resposta do modelo:

```
Sim.
```

> ❌ Errado! Esse erro revela limitações do modelo em entender o objetivo real do golfe.

---

## Solução com GENKNOW: Geração de Conhecimento

A técnica envolve **dois passos**:

1. **Gerar conhecimento factual relacionado à entrada**
2. **Usar esse conhecimento como parte do prompt final para melhorar a resposta**

---

### Exemplos de Geração de Conhecimento
**Prompt:**
```
Entrada: A Grécia é maior que o México.
Conhecimento: A Grécia tem aproximadamente 131.957 quilômetros quadrados, enquanto o México tem aproximadamente 1.964.375 quilômetros quadrados, tornando o México 1.389% maior que a Grécia.
Entrada: Os óculos sempre embaçam.
Conhecimento: A condensação ocorre nas lentes dos óculos quando o vapor de água do seu suor, respiração e umidade ambiente atinge uma superfície fria, esfria e então se transforma em minúsculas gotas de líquido, formando uma película que você vê como névoa. Suas lentes estarão relativamente frias em comparação com sua respiração, especialmente quando o ar externo estiver frio.
Entrada: Um peixe é capaz de pensar.
Conhecimento: Os peixes são mais inteligentes do que parecem. Em muitas áreas, como a memória, seus poderes cognitivos igualam ou excedem os dos vertebrados “superiores”, incluindo primatas não humanos. As memórias de longo prazo dos peixes os ajudam a acompanhar as relações sociais complexas.
Entrada: Um efeito comum de fumar muitos cigarros durante a vida é uma chance maior do que o normal de contrair câncer de pulmão.
Conhecimento: Aqueles que consumiram consistentemente menos de um cigarro por dia ao longo da vida tiveram nove vezes mais risco de morrer de câncer de pulmão do que os que nunca fumaram. Entre as pessoas que fumavam entre um e 10 cigarros por dia, o risco de morrer de câncer de pulmão era quase 12 vezes maior do que entre os que nunca fumaram.
Entrada: Uma pedra tem o mesmo tamanho de uma pedrinha.
Conhecimento: Um seixo é um clastro de rocha com um tamanho de partícula de 4 a 64 milímetros com base na escala de sedimentologia Udden-Wentworth. Os seixos são geralmente considerados maiores que os grânulos (2 a 4 milímetros de diâmetro) e menores que os seixos (64 a 256 milímetros de diâmetro).
Entrada: Parte do golfe é tentar obter um total de pontos mais alto do que outros.
Conhecimento:
```
---

**Conhecimento Gerado 1:**
```
O objetivo do golfe é jogar uma série de buracos com o menor número de tacadas. Uma partida de golfe normalmente consiste em 18 buracos. Cada buraco é jogado uma vez na rodada em um campo de golfe padrão. Cada tacada é contada como um ponto, e o número total de tacadas é usado para determinar o vencedor do jogo.
```
**Conhecimento Gerado 2:**
```
O golfe é um esporte de precisão com tacos e bolas no qual os jogadores concorrentes (ou golfistas) usam muitos tipos de tacos para acertar as bolas em uma série de buracos em um campo usando o menor número de tacadas. O objetivo é completar o percurso com a menor pontuação, que é calculada somando o número total de tacadas dadas em cada buraco. O jogador com a pontuação mais baixa ganha o jogo.
```
---

## Integração e Resposta

### Prompt Final:

```
Pergunta: Parte do golfe é tentar obter um total de pontos mais alto do que outros. Sim ou não?  
Conhecimento: O objetivo do golfe é jogar uma série de buracos com o menor número de tacadas. Uma partida de golfe normalmente consiste em 18 buracos. Cada buraco é jogado uma vez na rodada em um campo de golfe padrão. Cada tacada é contada como um ponto, e o número total de tacadas é usado para determinar o vencedor do jogo. 
Explique e responda:
```

### Resposta 1 (alta confiança):

```
Não, o objetivo do golfe não é obter um total de pontos mais alto do que os outros. Em vez disso, o objetivo é jogar uma série de buracos com o menor número de tacadas. O número total de tacadas é usado para determinar o vencedor do jogo, não o número total de pontos.
```


---

### Prompt Alternativo:

```
Pergunta: Parte do golfe é tentar obter um total de pontos mais alto do que outros. Sim ou não?  
Conhecimento: O golfe é um esporte de precisão com tacos e bolas no qual os jogadores concorrentes (ou golfistas) usam muitos tipos de tacos para acertar as bolas em uma série de buracos em um campo usando o menor número de tacadas. O objetivo é completar o percurso com a menor pontuação, que é calculada somando o número total de tacadas dadas em cada buraco. O jogador com a pontuação mais baixa ganha o jogo.
Explique e responda:
```

### Resposta 2 (menor confiança):

```
Sim, parte do golfe é tentar obter um total de pontos mais alto do que outros. Cada jogador tenta completar o percurso com a menor pontuação, que é calculada somando o total número de tacadas dadas em cada buraco. O jogador com a pontuação mais baixa ganha o jogo.
```

---

## Observações

- Quando o conhecimento **é claro e detalhado**, o modelo tende a dar respostas mais corretas.
- Quando o conhecimento é **ambíguo ou contraditório**, a resposta final pode ser inconsistente.
- A técnica GENKNOW ajuda a compensar **lacunas de conhecimento implícito** dos modelos.

---

## Conclusão

> 🧠 **Resumo**: O Prompt de Conhecimento Gerado (GENKNOW) melhora a precisão dos LLMs ao gerar e incorporar conhecimento relevante no prompt antes da previsão.  
> É particularmente eficaz em tarefas de **raciocínio de senso comum** ou que envolvem **conhecimento factual**.

