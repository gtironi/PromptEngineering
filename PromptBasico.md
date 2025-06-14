# Noções Básicas de Prompt

## Prompts Básicos

Você pode conseguir muito com prompts simples, mas a qualidade dos resultados depende da quantidade de informações que você fornece e de quão bem elaboradas são. Um prompt pode conter informações como instrução ou pergunta que você está passando para o modelo e incluir outros detalhes como contexto, entradas ou exemplos. Você pode usar esses elementos para instruir melhor o modelo e, como resultado, obter melhores resultados.

Vamos começar analisando um exemplo básico de um prompt simples:

**Prompt:**
```
O céu é
```

**Saída:**
```
azul
O céu é azul em um dia claro. Em um dia nublado, o céu pode ser cinza ou branco.
```

Como você pode ver, o modelo de linguagem gera uma continuação de strings que fazem sentido no contexto "O céu é". A saída pode ser inesperada ou distante da tarefa que queremos realizar.

Este exemplo básico também destaca a necessidade de fornecer mais contexto ou instruções sobre o que especificamente queremos alcançar.

Vamos tentar melhorar um pouco:

**Prompt:**
```
Complete a sentença:
O céu é
```

**Saída:**
```
tão lindo.
```

Isso é melhor? Bem, dissemos ao modelo para completar a frase para que o resultado fique muito melhor, pois segue exatamente o que dissemos para fazer ("complete a frase"). Essa abordagem de projetar prompts ideais para instruir o modelo a executar uma tarefa é chamada de **engenharia de prompt**.

O exemplo acima é uma ilustração básica do que é possível com LLMs hoje. Os LLMs de hoje são capazes de executar todos os tipos de tarefas avançadas que variam de resumo de texto a raciocínio matemático e geração de código.

---

## Formatação de Prompt

Tentamos um prompt muito simples acima. Um prompt padrão tem o seguinte formato:

```
<Pergunta>?
```

ou

```
<Instrução>
```

Isso pode ser formatado em um formato de resposta a perguntas (QA), que é padrão em muitos conjuntos de dados de QA, como segue:

```
Q: <Pergunta>?
A:
```

Ao solicitar como o acima, também chamado de **prompt de tiro zero** (*zero-shot*), você está solicitando diretamente ao modelo uma resposta sem nenhum exemplo ou demonstração sobre a tarefa que deseja realizar. Alguns modelos de linguagem grandes têm a capacidade de executar prompts zero-shot, mas isso depende da complexidade e do conhecimento da tarefa em questão.

---

## Prompt de Poucos Tiros (*Few-shot*)

Dado o formato padrão acima, uma técnica popular e eficaz para solicitação é chamada de **prompt de poucos tiros**, onde fornecemos exemplos (ou seja, demonstrações). Os prompts de poucos tiros podem ser formatados da seguinte maneira:

```
<Pergunta>?
<Resposta>
<Pergunta>?
<Resposta>
<Pergunta>?
<Resposta>
<Pergunta>?
```

A versão no formato QA ficaria assim:

```
Q: <Pergunta>?
A: <Resposta>
Q: <Pergunta>?
A: <Resposta>
Q: <Pergunta>?
A: <Resposta>
Q: <Pergunta>?
A:
```

Lembre-se de que não é necessário usar o formato QA. O formato do prompt depende da tarefa em mãos. Por exemplo, você pode executar uma tarefa de classificação simples e fornecer exemplares que demonstrem a tarefa da seguinte forma:

**Prompt:**
```
Isso é incrível! // Positivo
Isto é mau! // Negativo
Uau, esse filme foi radical! // Positivo
Que espetáculo horrível! //
```

**Saída:**
```
Negativo
```

Os prompts de poucos tiros permitem o **aprendizado no contexto**, que é a capacidade dos modelos de linguagem de aprender tarefas dadas algumas demonstrações.

---

## Elementos de um Prompt

À medida que abordamos mais e mais exemplos e aplicativos possíveis com a engenharia de prompt, você notará que existem certos elementos que compõem um prompt.

Um prompt pode conter qualquer um dos seguintes componentes:

- **Instrução** – uma tarefa ou instrução específica que você deseja que o modelo execute.
- **Contexto** – pode envolver informações externas ou contexto adicional que pode direcionar o modelo para melhores respostas.
- **Dados de entrada** – é a entrada ou pergunta para a qual estamos interessados em encontrar uma resposta.
- **Indicador de saída** – indica o tipo ou formato da saída.

Nem todos os componentes são necessários para um prompt e o formato depende da tarefa em questão. Abordaremos exemplos mais concretos nos próximos guias.

# -------------------------- Colocar sobre as Tips
