# Pontuação de Completude e de Prontidão

A mesma fórmula é usada nas duas pontuações que aparecem no processo: a **Pontuação de Completude**, calculada na Fase 3 (Análise de Lacunas) e recalculada a cada rodada da Fase 4, e a **Pontuação de Prontidão**, que é o valor final dela, congelado e exibido na seção 13 do documento entregue.

## Como calcular o score de uma seção

Para cada uma das 13 seções, use o checklist de `secoes.md`:

```
score_da_seção = (itens preenchidos + 0.5 × itens parciais) / total de itens do checklist
```

Um item é **parcial** quando existe alguma informação, mas ela é vaga, não verificável, ou depende de uma suposição não confirmada pelo usuário.

## Pesos das seções no score global

Nem toda seção pesa igual. Seções que sustentam a confiabilidade do documento (as marcadas como "seção crítica" em `secoes.md`) pesam o dobro das demais:

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

```
score_global = Σ(score_da_seção × peso_da_seção) / Σ(pesos)
```

Expresse sempre como percentual (0–100%).

## Limiares

- **Limiar de liberação para o documento final: 80%.** Abaixo disso, o documento não deve ser gerado sem passar pela Fase 4 primeiro.
- **Limiar de "lacuna crítica"**: uma lacuna é crítica se pertence a uma seção de peso 2, **ou** se pertence a qualquer seção mas o item ausente/parcial é algo que, sem ele, tornaria uma regra, requisito ou critério não verificável (ex.: um RF sem nenhum CA associado é sempre crítico, mesmo que a seção Histórias de Usuário como um todo esteja em 90%).
- **Bounded loop**: no máximo 3 rodadas de Questionamento Crítico (Fase 4). Na 3ª rodada, se ainda houver lacuna crítica, ofereça ao usuário a opção explícita de assumir a lacuna como premissa em vez de continuar indefinidamente.

## O que vai na seção 13 (Pontuação de Prontidão) do documento final

- Tabela com o score de cada uma das 11 seções avaliadas (peso e score)
- Score global final
- Se o documento foi liberado por atingir 80%, ou por decisão explícita do usuário de aceitar lacunas restantes — deixe isso claro, não esconda
- Lista de premissas assumidas (se houver), cada uma com a seção e o motivo de não ter sido confirmada
- Lista de itens marcados como "a definir" que não são bloqueantes, para acompanhamento futuro

Nunca omita um score baixo para deixar o documento "parecer mais pronto" do que está — a transparência dessa seção é o ponto central da skill.
