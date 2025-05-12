# Autoconsistência (Self-Consistency)

> Fonte: Wang et al. (2022)

Talvez uma das técnicas mais avançadas disponíveis para engenharia de prompts seja a **autoconsistência**. Proposta por Wang et al. (2022), essa abordagem visa **substituir a decodificação ingênua e gananciosa** usada na solicitação de Cadeia de Pensamento (Chain-of-Thought - CoT).

## O que é Autoconsistência?

A ideia é **experimentar múltiplos caminhos de raciocínio** por meio de CoT few-shot e, a partir dessas gerações variadas, **selecionar a resposta mais comum (mais consistente)**.

Isso ajuda a:
- Aumentar o desempenho do modelo em tarefas que envolvem **raciocínio aritmético** e de **bom senso**.
- **Reduzir erros ocasionais** provocados por raciocínios incorretos.

---

## Exemplo: Raciocínio Aritmético com e sem Autoconsistência

### Prompt:

```
Quando eu tinha 6 anos, minha irmã tinha metade da minha idade.  
Agora tenho 70 anos, quantos anos tem minha irmã?
```

### Saída **sem autoconsistência**:

```
35
```

> ❌ A resposta está incorreta!

---

## Aplicando Autoconsistência com Exemplos (Few-Shot)

Baseado nos exemplos da **Tabela 17** de Wang et al. (2022), utilizamos múltiplos exemplos de raciocínio aritmético para estimular o modelo.

### Exemplos usados no prompt (few-shot):

- **Quantas árvores foram plantadas?**
- **Quantos carros há no estacionamento?**
- **Quantos chocolates sobraram?**
- **Quantos pirulitos foram dados?**
- **Quantos brinquedos Shawn tem agora?**
- **Quantos computadores estão na sala do servidor?**
- **Quantas bolas de golfe restaram?**
- **Quanto dinheiro Olivia tem sobrando?**

### Novo Prompt com Autoconsistência:

```
P: Quando eu tinha 6 anos, minha irmã tinha metade da minha idade. Agora tenho 70 anos, quantos anos tem minha irmã?
A:
```

### Múltiplas Saídas Geradas:

1. **Saída 1**  
   Quando eu tinha 6 anos, minha irmã tinha metade da minha idade, então ela tinha 3.  
   Agora eu tenho 70, então ela tem 70 - 3 = 67.  
   **A resposta é 67.**

2. **Saída 2**  
   Quando o narrador tinha 6 anos, sua irmã tinha metade da sua idade, ou seja, 3.  
   Agora, com 70 anos, a diferença de idade se manteve, então ela tem 70 - 3 = 67.  
   **A resposta é 67.**

3. **Saída 3 (errada)**  
   Quando eu tinha 6 anos, minha irmã tinha metade da minha idade, então ela tinha 3.  
   Agora eu tenho 70, então ela tem 70 / 2 = 35.  
   **A resposta é 35.**

---

### Conclusão com Autoconsistência

> ✅ **Resposta majoritária: 67**  
> ❌ Resposta incorreta descartada: 35

A autoconsistência permite que o modelo **gere múlt**
