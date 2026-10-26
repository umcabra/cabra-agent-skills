# Pontuação de Completude e de Prontidão

A mesma fórmula é usada nas duas pontuações do processo: a **Pontuação de Completude**, calculada na Fase 3 (Análise de Lacunas) e recalculada a cada rodada da Fase 4, e a **Pontuação de Prontidão**, que é o valor final dela, congelado e exibido na seção 13 do documento entregue.

Em cada cálculo existem dois números:

- **Score da etapa**: considera só as seções avaliadas na etapa-alvo (ver `etapas.md`). É o que decide a liberação.
- **Score global**: considera as 11 seções avaliáveis. É informativo — mostra o todo — e só decide a liberação na etapa E4, onde as duas listas coincidem.

## Como calcular o score de uma seção

Para cada seção, use o checklist de `secoes.md`:

```
score_da_seção = (itens preenchidos + 0.5 × itens parciais) / total de itens do checklist
```

Um item é **parcial** quando existe alguma informação, mas ela é vaga, não verificável, ou depende de uma suposição não confirmada pelo usuário.

## Pesos das seções

Seções que sustentam a confiabilidade do documento (as marcadas como "seção crítica" em `secoes.md`) pesam o dobro das demais:

| Peso 2 (críticas)         | Peso 1 (demais)              |
| -------------------------- | ----------------------------- |
| Regras de Negócio          | Resumo Executivo - Descoberta |
| Requisitos Funcionais      | Meta SMART                    |
| Critérios de Aceitação     | Processos de Negócio          |
| Riscos                     | Detalhes do Projeto           |
|                             | Histórias de Usuário          |
|                             | Requisitos Não Funcionais     |
|                             | Dependências                  |

(Matriz de Rastreabilidade e Pontuação de Prontidão não entram no cálculo — são derivadas/geradas, não levantadas.)

## Score da etapa e score global

```
score = Σ(score_da_seção × peso_da_seção) / Σ(pesos)
```

- **Score da etapa:** a soma percorre apenas as seções avaliadas na etapa-alvo.
  - E1: seções 1, 2, 3, 4 (todas com peso 1).
  - E2: seções 5 e 6 (peso 2 cada).
  - E3: seção 7 (peso 2), 8 e 9 (peso 1 cada).
  - E4: as 11 seções.
- **Score global:** a soma percorre as 11 seções, em toda etapa.

Expresse sempre como percentual (0–100%). Seções fora da etapa nunca puxam o score da etapa para baixo — essa é a razão de existirem etapas.

## Limiares e gate de liberação

Os limiares por etapa estão em `etapas.md`: **E1 70%, E2 70%, E3 75%, E4 80%**. Para alterar um limiar, mude lá e nos lugares que repetem a tabela (`SKILL.md`, `README.md` e `copilot/spec-descoberta-scrum.md`).

O **gate de liberação** da etapa está satisfeito quando:

1. o score da etapa é maior ou igual ao limiar dela; **e**
2. não há nenhuma lacuna crítica da etapa pendente.

Se o gate não estiver satisfeito, o documento da etapa não deve ser gerado sem passar pela Fase 4, a não ser que o usuário assuma explicitamente as lacunas restantes como risco aceito.

**Lacuna crítica (da etapa):** é crítica a lacuna listada como bloqueante para a etapa em `etapas.md`, ou que pertence a uma seção de peso 2 avaliada na etapa, ou que torne uma regra, requisito ou critério não verificável (ex.: um RF sem nenhum CA associado é sempre crítico, mesmo que a seção Histórias de Usuário esteja em 90%). Lacunas fora da etapa são registradas como "a definir", nunca bloqueiam e não são perguntadas.

**Bounded loop:** no máximo 3 rodadas de Questionamento Crítico (Fase 4) **por etapa**. Na 3ª rodada, se ainda houver lacuna crítica, ofereça ao usuário a opção explícita de assumir a lacuna como premissa em vez de continuar indefinidamente. O contador volta a zero quando a etapa muda.

## O que vai na seção 13 (Pontuação de Prontidão) do documento entregue

- Tabela com o score de cada uma das 11 seções avaliáveis (peso, score, e a etapa em que ela é avaliada)
- Score da etapa, com o limiar dela
- Score global — sempre exibido, mesmo quando baixo
- Se a versão foi liberada por atingir o limiar da etapa, ou por decisão explícita do usuário de aceitar lacunas restantes — deixe isso claro, não esconda
- Lista de premissas assumidas (se houver), cada uma com a seção e o motivo de não ter sido confirmada
- Lista de itens marcados como "a definir" que não são bloqueantes, para acompanhamento futuro
- Mapa das próximas etapas e histórico de versões (formato em `etapas.md`)

Nunca omita um score baixo, nem o global, para deixar o documento "parecer mais pronto" do que está — a transparência dessa seção é o ponto central da skill, e é o que torna seguro entregar uma versão parcial.
