# Priorização Comercial por Probabilidade de Conversão (R1 → R2)
![Capa do projeto](assets/Imagem_Regressao.png)

Uso de modelagem estatística para identificar, entre os negócios que chegaram à primeira reunião, quais têm maior chance real de avançar para a segunda — e transformar essa leitura em priorização prática para o time comercial.

---

## O problema

Uma empresa com funil de vendas estruturado apresentava escape significativo logo após a primeira reunião (R1):

- **21,3%** das oportunidades eram perdidas por falta de resposta do decisor após R1
- **72,2%** das oportunidades que chegavam à segunda reunião (R2) nunca recebiam uma proposta formal
- Um atraso de apenas **24 horas** no follow-up pós-R1 reduzia a probabilidade de conversão em **21 vezes**

O time comercial tratava toda a carteira de R1 da mesma forma — sem distinção entre casos com alta e baixa chance de avançar. O problema não era volume de oportunidades. Era ausência de priorização orientada por dados.

---

## O que foi feito

Foi construído um modelo estatístico capaz de atribuir, para cada negócio em R1, uma probabilidade individual de avanço para R2 — usando apenas informações já disponíveis naquele momento do funil.

O cuidado central foi garantir que o modelo aprendesse apenas com sinais que o comercial realmente teria em mãos na hora de decidir onde focar. Nenhuma informação de etapas futuras foi usada, o que torna a probabilidade estimada confiável para uso real, não apenas para demonstração em papel.

Os sinais usados incluíam: nível de atividade no negócio, tempo de resposta nas etapas anteriores, origem do lead, responsável comercial e comportamento recente de engajamento.

A escolha pela regressão logística foi deliberada: com o volume de dados disponível, era o modelo que entregava ao mesmo tempo uma probabilidade bem calibrada e uma leitura clara de quais fatores mais influenciavam o resultado — algo essencial para que os gestores pudessem entender e agir, não apenas consumir um número.

---

## Resultados

### O modelo separou bem a carteira

Antes do modelo, a única referência disponível era a taxa histórica média de avanço: **65,85%** de todos os negócios em R1 chegavam a R2. Isso não criava priorização real, porque tratava todos os casos como igualmente promissores.

Com o modelo, a carteira passou a ser lida em três faixas com comportamentos muito diferentes:

| Faixa | O que significa | Taxa real de avanço para R2 |
|---|---|---|
| Alta propensão | Perfil próximo dos que historicamente avançam | **88,79%** |
| Média propensão | Casos intermediários, avançam com acompanhamento | 52,82% |
| Baixa propensão | Perfil distante dos que costumam avançar | 8,09% |

A diferença entre a faixa de alta e baixa propensão é de **80,7 pontos percentuais** na taxa real de conversão. Isso significa que o modelo não apenas previu melhor — ele criou grupos com comportamentos realmente distintos, o que é o que importa para uma priorização comercial funcionar na prática.

### O modelo estimou bem, não apenas classificou

A probabilidade média atribuída pelo modelo foi de **66,11%**, contra uma taxa real de avanço de **65,85%** no conjunto de teste. Essa proximidade mostra que a régua está bem ajustada à realidade — o modelo não inflou nem subestimou a chance média da carteira.

### Ganho em relação a não usar modelo

Para comparar o modelo com uma referência simples, foi usada uma baseline que atribui a mesma probabilidade para todos os negócios — exatamente a taxa histórica média de avanço (65,85%). Essa referência representa o que acontece quando não há priorização: todos os casos são tratados como igualmente promissores.

Uma baseline assim, por definição, não consegue separar nenhum caso do outro. Por isso sua capacidade de discriminação (ROC AUC) é 0,50 — equivalente a um critério aleatório — e sua qualidade de priorização (Average Precision) coincide com a própria taxa média da base.

| | Sem modelo | Com modelo |
|---|---|---|
| Capacidade de separar a carteira (ROC AUC) | 0,50 | **0,88** |
| Qualidade da priorização (Average Precision) | 65,85% | **91,96%** |

O modelo saiu de 65,85% para 91,96% na qualidade da priorização — um ganho absoluto de **26,1 pontos percentuais**.

Para entender o que isso representa em termos relativos: partindo de 65,85%, havia espaço máximo de melhoria de 34,15 pontos (o que faltava para chegar a 100%). O modelo aproveitou 26,1 desses 34,15 pontos disponíveis, o que equivale a **76,4% do ganho possível** a partir da baseline.

Outra forma de ler o mesmo resultado: o modelo melhorou a qualidade da priorização em **39,7% em relação ao ponto de partida** — calculado como a variação proporcional entre os dois valores (91,96% ÷ 65,85% − 1 = 39,7%).

Ambas as leituras confirmam o mesmo resultado: o modelo aproveitou bem o espaço disponível para melhorar a separação da carteira, com ganho expressivo em relação a não usar nenhum critério de priorização. O modelo foi obtido com baixo custo computacional e é diretamente aplicável ao fluxo comercial existente.

---

## Aplicação prática

As probabilidades estimadas foram organizadas em três faixas de prioridade para uso direto pelo time comercial:

- **Alta propensão:** foco prioritário — maior retorno esperado por hora investida
- **Média propensão:** acompanhamento seletivo — casos que avançam com atenção no momento certo
- **Baixa propensão:** menor prioridade imediata — abordagem diferente ou pausa estratégica

Essa leitura permitiu ao comercial distribuir esforço de forma mais inteligente, concentrando energia onde a probabilidade de retorno é maior — sem abandonar os casos intermediários e sem desperdiçar tempo em oportunidades com baixa chance real de avanço.

---

## Estrutura do repositório

```
├── assets/
│   └── Imagem_Regressao.png
├── 2f_modelagem_estatistica_r1_r2.ipynb
├── README.md
└── requirements.txt
```

---

## Stack utilizada

- Python 3
- pandas, numpy
- scikit-learn
- matplotlib

---

## Nota sobre confidencialidade

Os dados originais são proprietários e não estão disponíveis neste repositório. O notebook apresenta o código completo, a metodologia e os resultados, sem exposição de informações da empresa.

---

## Autor

Análise desenvolvida como parte de um projeto de aceleração comercial com foco em priorização orientada por dados.
