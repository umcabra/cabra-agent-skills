# Como questionar as lacunas críticas

O público desta skill é sênior e ocupado. O questionamento existe para proteger a qualidade do documento, não para parecer minucioso — cada pergunta feita deveria ser uma que, se não respondida, deixaria uma Regra de Negócio, um Requisito Funcional, um Critério de Aceitação ou um Risco crítico não verificável.

## Escopo da rodada: só a etapa-alvo

Pergunte apenas sobre lacunas **críticas da etapa-alvo** (lista de bloqueantes em `etapas.md`). Lacunas de seções que só serão avaliadas em etapas futuras são registradas como "a definir" e ficam para quando a etapa chegar — o usuário ocupado não precisa decidir hoje o que só será aprovado depois. O limite de 3 rodadas vale por etapa e o contador volta a zero quando a etapa muda.

## Ordem de prioridade

Dentro da etapa-alvo:

1. Lacunas em **Regras de Negócio** e **Requisitos Funcionais** primeiro — sem elas, nada mais no documento tem em que se apoiar.
2. Lacunas em **Critérios de Aceitação** de RFs já definidos — um RF sem CA verificável é uma promessa vaga.
3. Lacunas em **Riscos** de impacto alto (quando Riscos faz parte da etapa-alvo, ou seja, no E4).
4. Só depois, lacunas críticas de qualquer outra seção da etapa. No E1, onde nenhuma seção tem peso 2, a ordem é: problema e resultado esperado, depois métrica e valor-alvo, depois escopo dentro e fora.

Nunca pergunte sobre uma lacuna não crítica na mesma rodada que as críticas — isso dilui a atenção do usuário no que realmente importa. Lacunas não críticas ficam registradas como "a definir" e aparecem só na Pontuação de Prontidão.

## Formato

- Agrupe por seção, com um cabeçalho curto por grupo, não uma lista corrida misturando tudo.
- Cada pergunta deve ser específica o bastante para ser respondida em uma frase. Prefira perguntas fechadas ou de múltipla escolha quando a resposta provável tiver um conjunto pequeno de opções (ex.: "Esse desconto se aplica por pedido ou por item?"); reserve perguntas abertas para quando a resposta genuinamente não tem como ser antecipada.
- Quando fizer sentido dar contexto sobre por que a pergunta importa, faça em uma frase curta antes dela — não um parágrafo de justificativa.
- Limite a leitura de uma rodada: se houver muitas lacunas críticas, priorize as 5–8 mais importantes na primeira rodada em vez de despejar quinze perguntas de uma vez; o resto pode vir na rodada seguinte se a primeira não for suficiente.

## Exemplo de uma rodada bem formada

```
Antes de fechar as Regras de Negócio, preciso confirmar 3 pontos:

1. Existe um valor máximo de crédito por cliente, ou o limite é só o score de análise?
2. O desconto de fidelidade acumula com cupons promocionais, ou é substituído pelo maior dos dois?
3. Clientes inadimplentes ainda podem fazer novos pedidos, ou ficam bloqueados até regularizar?

E em Riscos, um ponto de alto impacto:

4. Esse fluxo novo depende da API do parceiro de pagamento que vocês mencionaram — existe
   um plano B se ela estiver indisponível no lançamento, ou o lançamento fica bloqueado por ela?
```

## O que não fazer

- Não repita uma pergunta cuja resposta já está em `.descoberta/<slug>/descoberta.md` ou no Bloco de Estado — isso é sinal de que a Fase 2 não foi lida com atenção antes de questionar. O mesmo vale ao avançar de etapa: o que foi respondido numa etapa anterior não se pergunta de novo.
- Não transforme a pergunta em uma aula sobre o próprio framework ("preciso disso para calcular a Pontuação de Completude da seção 5") — o usuário não precisa da mecânica interna, só da pergunta de negócio.
- Não aceite uma resposta vaga como se fosse suficiente ("mais ou menos", "acho que sim") para uma lacuna crítica — se a resposta não for verificável, ela continua sendo lacuna; ou peça precisão, ou registre como premissa assumida na próxima rodada.
