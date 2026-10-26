---
name: spec-descoberta-scrum
description: >-
  Conduz a descoberta e especificação de projetos de produto/software para PMs, POs, Líderes Técnicos, Stakeholders, Engenheiros de Requisitos e Gerentes de Projeto seniores, com um framework de descoberta progressiva compatível com Scrum. NÃO gera o documento final de imediato — pesquisa, mapeia lacunas por seção, calcula uma Pontuação de Completude, questiona só os pontos críticos e só produz o documento final (Resumo Executivo, Meta SMART, Processos de Negócio, Detalhes do Projeto, Regras de Negócio, Requisitos Funcionais, Critérios de Aceitação, Histórias de Usuário, Requisitos Não Funcionais, Dependências, Riscos, Matriz de Rastreabilidade, Pontuação de Prontidão) quando não há lacuna crítica, ou quando o usuário aceita as que restarem. Use sempre que o usuário pedir para especificar, documentar, escopar ou levantar requisitos de um projeto, feature, produto ou iniciativa — mesmo sem citar "descoberta", "backlog" ou "spec", inclusive para "documentar essa ideia" ou "preciso de um PRD".
---

# Spec de Descoberta Scrum

Framework de descoberta progressiva para especificação de produto. Transforma uma ideia de projeto, por mais vaga que seja, num documento rastreável e pronto para virar backlog Scrum — mas só entrega esse documento depois de garantir que existe informação suficiente para que ele seja confiável.

```
┌───────────┐   ┌────────────┐   ┌───────────────┐   ┌────────────────┐   ┌───────────┐
│ TRIAGEM   │ → │ DESCOBERTA │ → │ ANÁLISE DE     │ → │ QUESTIONAMENTO │ → │ DOCUMENTO │
│           │   │            │   │ LACUNAS        │   │ CRÍTICO        │   │ FINAL     │
└───────────┘   └────────────┘   └───────────────┘   └────────────────┘   └───────────┘
  obrigatória     obrigatória       obrigatória         condicional*        condicional**

* Só roda enquanto existir lacuna crítica sem aceite do usuário. No máximo 3 levas;
  depois disso, só o aceite explícito libera. Ver pontuacao.md.
** Sem lacuna crítica, escreva o documento mesmo abaixo de 80%.
   Com lacuna crítica, só depois de "aceito seguir com as lacunas" (ou equivalente inequívoco).
   Score ≥ 80% não libera lacuna crítica.
```

## Regra de ouro

**Nunca escreva o documento final na primeira interação.** O valor desta skill está em resistir ao impulso de produzir algo bonito rápido demais. Um documento gerado sobre suposições não verificadas é pior do que nenhum documento — ele passa confiança que a informação não sustenta. Cada seção do documento final só deve conter fatos declarados pelo usuário ou encontrados em documentos que ele forneceu. Nunca invente regras de negócio, métricas ou critérios de aceitação para preencher uma seção.

Pesquisa web e conector trazem contexto externo (mercado, norma pública, sistema já documentado). Cite a origem nas notas de trabalho. Esse achado não vira meta numérica, regra, requisito, critério ou risco até o usuário confirmar.

## Antes de começar: carregue as referências certas

- `references/secoes.md` — definição, perguntas-guia, checklist das seções 1 a 11 e profundidade por porte. Leia antes da Descoberta.
- `references/notacao-ears.md` — EARS para Requisitos Funcionais e Dado/Quando/Então para Critérios de Aceitação. Leia antes de redigir essas duas seções.
- `references/pontuacao.md` — fórmula, pesos, o que é lacuna crítica e o portão de liberação. Leia antes da Análise de Lacunas.
- `references/perguntas.md` — prioridade, formato e teto de rodadas. Leia antes do Questionamento.

Carregue cada referência na fase correspondente. `utils/` é nota de autoria, não faz parte do fluxo.

## Fase 1 — Triagem (obrigatória)

Objetivo: entender o pedido e classificar o porte. As 13 seções do documento não mudam. O porte só muda quando "não há" conta como item preenchido (`secoes.md`, Profundidade por porte).

1. Da primeira mensagem, extraia nome ou apelido do projeto, tipo (feature nova, produto novo, integração, migração) e papel de quem pede (PM, PO, Tech Lead, stakeholder).
2. Classifique o porte, parando na primeira regra que couber:
   - **Complexo**: dinheiro, dado sensível, mais de um sistema ou time, compliance, ou o problema ainda está ambíguo.
   - **Médio**: mais de um fluxo, ou uma integração já existente, sem nada do item acima.
   - **Simples**: um único fluxo ou tela, sem integração nova, sem dinheiro e sem dado sensível.
3. Infira o que já estiver dito e pergunte só o que faltar. Não invente nome de projeto nem papel.
4. Crie ou atualize `.descoberta/<slug-do-projeto>/descoberta.md` com nome, porte, solicitante e data. Se o workspace for um repositório git, garanta a linha `.descoberta/` no `.gitignore` (acrescente se o arquivo existir; se não existir, crie um `.gitignore` só com essa linha).

Não pule a triagem quando o usuário já mandou um texto longo. Use o texto para preenchê-la e registre o porte.

## Fase 2 — Descoberta (obrigatória)

Objetivo: coletar fato, organizado pelas seções 1 a 11, antes de julgar completude. As seções 12 e 13 não se descobrem: são produzidas na Fase 5.

1. Leia `references/secoes.md` e marque quais perguntas-guia das seções 1 a 11 o usuário já respondeu.
2. Fontes, nesta ordem:
   1. O que ele escreveu na conversa.
   2. Documentos que ele anexar ou apontar. Leia o arquivo inteiro antes de tratar uma seção como coberta.
   3. Conector (Jira, Confluence, Drive, Slack), se houver um conectado e o dado for do projeto. Contexto externo, até ele confirmar o que entra no spec.
   4. Pesquisa web, só para contexto externo (mercado, concorrência, norma pública, prática do setor). Não pesquise para adivinhar regra, meta ou critério que só o time define.
3. Registre em `.descoberta/<slug>/descoberta.md`, por seção, com a origem de cada achado (usuário / documento / conector / web). Achado de web ou conector fica marcado como não confirmado até o usuário assumir.
4. Não calcule score aqui.

## Fase 3 — Análise de Lacunas (obrigatória)

Objetivo: Pontuação de Completude seção a seção. A conta está em `references/pontuacao.md`; siga-a, não aproxime.

1. Para cada item das seções 1 a 11, marque PREENCHIDO, PARCIAL ou PENDENTE.
2. Calcule o score de cada seção e o Score Global (denominador 15).
3. Separe lacuna crítica e lacuna não crítica como em `pontuacao.md`.
4. Grave `.descoberta/<slug>/lacunas.md` com o status de cada item, o score por seção, o global, a rodada atual, as lacunas críticas, as não críticas e as premissas. O status do item é a fonte; o percentual se recalcula a partir dele.
5. Mostre ao usuário o global, o que está crítico e uma linha com a quantidade de itens "a definir". Sem checklist burocrático do que já está preenchido.
6. Decida:
   - Há lacuna crítica sem aceite: Fase 4.
   - Não há lacuna crítica: Fase 5, mesmo abaixo de 80%.
   - Rodada já em 3 com lacuna crítica: não pergunte de novo por conta própria; peça o aceite, como na Fase 4.

## Fase 4 — Questionamento Crítico (condicional)

Roda só com lacuna crítica ainda não aceita. O percentual não dispara esta fase.

1. Leia `references/perguntas.md`.
2. Se a rodada já é 3, não faça a quarta leva. Mostre as lacunas críticas e pergunte se ele continua respondendo ou aceita seguir com elas. Uma leva extra só acontece se ele pedir para continuar; em seguida volte à Fase 3. Sem "aceito seguir com as lacunas" (ou equivalente inequívoco, dito depois de ver a lista), não vá à Fase 5.
3. Se a rodada é 0, 1 ou 2, agrupe até 8 perguntas por seção, na prioridade de `perguntas.md`. Ao apresentá-las, some 1 na rodada (a primeira leva sai como rodada 1).
4. Com as respostas, volte à Fase 3 e recalcule. Não promova resposta vaga a PREENCHIDO.

Nunca escolha o aceite no lugar do usuário. Se ele pedir "só manda o documento" com lacuna crítica aberta, mostre score e lista e faça a mesma pergunta.

## Fase 5 — Documento Final

Só entra aqui pelo portão de `pontuacao.md`: zero lacuna crítica, ou aceite explícito das que restam.

1. Consolide o que está em `.descoberta/<slug>/`. Não reescreva do zero e não complemente com fato novo.
2. Redija as seções 2 a 12 primeiro. A seção 1 (Resumo Executivo) é escrita por último e colocada no topo.
3. O Markdown tem exatamente estas 13 seções, nesta ordem, com `#` no título e `##` em cada seção:
   1. Resumo Executivo - Descoberta
   2. Meta SMART
   3. Processos de Negócio
   4. Detalhes do Projeto
   5. Regras de Negócio
   6. Requisitos Funcionais
   7. Critérios de Aceitação
   8. Histórias de Usuário
   9. Requisitos Não Funcionais
   10. Dependências
   11. Riscos
   12. Matriz de Rastreabilidade
   13. Pontuação de Prontidão
4. IDs como em `secoes.md`. Requisitos Funcionais em EARS; Critérios de Aceitação em Dado/Quando/Então (`notacao-ears.md`).
5. A matriz cruza RN → RF → CA → HU. Todo RF precisa de ao menos um CA e uma HU já sustentados por fato ou por premissa aceita. Se faltar, não invente: volte à Fase 4 se ainda houver rodada, ou, com o aceite já dado, deixe a célula como pendência e liste a premissa na seção 13.
6. A seção 13 copia o último cálculo, diz se a liberação foi sem lacuna crítica ou por aceite, lista premissas e itens "a definir", e registra se o global ficou abaixo da referência de 80%.
7. Grave `.descoberta/<slug>/spec.md` no workspace e mostre o documento na resposta. Se o ambiente tiver ferramenta de artifact, apresente esse mesmo arquivo. Não use caminho de sandbox de outro produto.
8. Pedido de alteração depois da entrega: edite o `spec.md` existente. Se mudar RN, RF, CA ou HU, atualize a matriz e a Pontuação de Prontidão. Mudança que reabre lacuna crítica volta à Fase 3 antes de regravar o spec.

## Retomando um projeto em andamento

Se já existir `.descoberta/<slug>/`, leia `descoberta.md` e `lacunas.md` antes de perguntar. Não repita pergunta cujo item já está PREENCHIDO. Recalcule os percentuais a partir do status dos itens e do que o usuário disser agora. O que ele diz agora prevalece sobre o arquivo.

## Comportamento de saída

Conduza cada fase sem anunciar o nome da fase. Mostre achado, lacuna, pergunta ou o documento. O usuário sênior quer avançar com qualidade, não acompanhar a mecânica interna.
