# Etapas de entrega

O documento não precisa nascer completo. Num time em que cada etapa do projeto é aprovada mediante um entregável, exigir 80% de tudo antes de mostrar qualquer coisa atrasa a aprovação e cansa quem revisa. Por isso o documento é entregue em **quatro etapas**, cada uma com suas seções, seu limiar de completude e seus itens bloqueantes. A estrutura de 13 seções nunca muda — o que muda é quanto de cada seção já foi levantado e avaliado em cada versão.

Esta é a fonte de verdade para etapas, limiares e itens bloqueantes. A fórmula do score está em `pontuacao.md`.

## As quatro etapas

| Etapa | Nome | Seções avaliadas | Limiar | Versão | Aprovação que costuma destravar |
| ----- | ---- | ---------------- | ------ | ------ | -------------------------------- |
| **E1** | Visão | 1, 2, 3, 4 | 70% | v0.1 | Conceito e escopo do projeto |
| **E2** | Regras e Requisitos | 5, 6 (10 e 11 entram como rascunho, sem pontuar) | 70% | v0.2 | O que será construído e sob quais regras |
| **E3** | Aceitação e Backlog | 7, 8, 9 (12 é derivada) | 75% | v0.3 | Entrada no backlog e refinamento |
| **E4** | Completo | 1 a 11 (12 e 13 são derivadas/geradas) | 80% | v1.0 | Documento final, handoff |

Seções 12 (Matriz de Rastreabilidade) e 13 (Pontuação de Prontidão) nunca entram no cálculo: são derivadas do que foi levantado. A seção 13 aparece em toda versão.

Em E2, Dependências (10) e Riscos (11) entram no documento como **rascunho**: registre o que o usuário já tiver dito, mas não pergunte nada sobre elas e não pontue. Elas passam a ser avaliadas de verdade só em E4. Isso evita transformar o E2 num documento completo disfarçado.

## Escolhendo a etapa-alvo (na Triagem)

Pergunte uma vez, junto das demais perguntas da Triagem: **"Qual aprovação este entregável precisa destravar?"** A resposta define a etapa:

- aprovar conceito, escopo ou "se vale a pena seguir" → **E1**
- aprovar regras e requisitos com negócio e tecnologia → **E2**
- levar para refinamento ou backlog → **E3**
- documento completo, handoff, ou "tudo" → **E4**

Se o usuário não souber ou não responder, decida pelo porte e diga qual escolheu: **Simples → E4** (o projeto é pequeno o bastante para fechar de uma vez); **Médio ou Complexo → E1**. O usuário pode mudar a etapa-alvo a qualquer momento; o que já foi levantado é reaproveitado.

Etapas podem ser puladas (ir direto ao E2, por exemplo), com uma exceção: o E3 avalia critérios de aceitação sobre requisitos que precisam existir. Se a seção 6 estiver vazia, diga que não há o que aceitar e sugira passar pelo E2 antes — a decisão continua sendo do usuário.

## Itens bloqueantes (lacunas críticas da etapa)

Uma lacuna é **crítica para a etapa** quando impede que a pessoa que aprova julgue o entregável. Só essas lacunas bloqueiam a liberação e só elas são perguntadas primeiro; o resto fica como "a definir".

| Etapa | São lacunas críticas |
| ----- | -------------------- |
| **E1** | Problema/motivação (seção 1); resultado esperado em uma frase (seção 1); métrica e valor-alvo da Meta SMART (seção 2); escopo dentro e fora do projeto (seção 4) |
| **E2** | Qualquer item ausente ou parcial nas seções 5 e 6 (peso 2) |
| **E3** | Qualquer item ausente ou parcial na seção 7 (peso 2), incluindo RF sem nenhum CA associado |
| **E4** | Qualquer item ausente ou parcial nas seções 5, 6, 7 e 11 (peso 2), incluindo RF sem nenhum CA associado |

Lacunas de seções fora da etapa são **registradas, não perguntadas**. O usuário sênior com pouco tempo não precisa responder agora sobre algo que só será aprovado daqui a duas etapas.

## Como o documento de cada etapa é montado

Toda versão tem as **13 seções, na mesma ordem**. O que muda é o conteúdo:

- **Seções da etapa e de etapas anteriores já levantadas:** conteúdo real, só com fatos confirmados.
- **Seções de etapas futuras:** uma linha de espaço reservado, nunca preenchidas com suposição:
  `_Não coberta nesta versão (v0.1). Prevista para a etapa E2._`
- **Seções 10 e 11 em E2:** o que já se sabe, antecedido de `_Rascunho — não pontuado nesta etapa; será avaliado em E4._`
- **Seção 12 (Matriz):** espaço reservado até E3; a partir de E3 cruza RN → RF → CA → HU de tudo que já existe. Nenhum RF fica sem CA e HU a partir daí.
- **Seção 13 (Pontuação de Prontidão):** sempre completa, com:
  - score da etapa e o limiar dela;
  - score global, **sempre exibido**, mesmo baixo, como visão do todo;
  - como a versão foi liberada (limiar atingido, ou aceite explícito do usuário com lacunas, dito sem suavizar);
  - premissas assumidas e itens "a definir", cada um com a seção;
  - **mapa das próximas etapas**: para cada etapa futura, o que falta de mais importante;
  - **histórico de versões**: tabela com versão, etapa, data e resumo da mudança.

Cabeçalho do documento: título, versão (v0.1, v0.2, v0.3 ou v1.0), etapa, data e a linha "Rascunho para aprovação" (ou "Versão final", no E4).

## Versionamento e IDs

- Cada etapa gera uma versão nova, gravada como `<slug>-spec-v0.1.md`, `<slug>-spec-v0.2.md` e assim por diante. A nova versão nasce como cópia da anterior e é editada; as anteriores ficam intactas, porque são a trilha do que cada aprovação viu.
- **IDs são estáveis.** `RN-001` continua `RN-001` nas versões seguintes. Nunca renumere e nunca reutilize um ID. Se um item for removido, mantenha o ID com a marca `(removido em v0.3)`.
- Ajustes **dentro da mesma etapa**, antes da aprovação, editam o arquivo da versão atual sem trocar o número.
- Se algo **já aprovado** mudar numa etapa posterior, registre no histórico de versões o que mudou e por quê, e liste os RF, CA e HU que dependem do item alterado para revisão.

## Avançando de etapa

Só avance quando o usuário pedir ou disser que a etapa foi aprovada; não antecipe trabalho que ninguém pediu. Ao avançar:

1. Reaproveite tudo que já foi levantado — não refaça perguntas respondidas.
2. Zere o contador de rodadas de questionamento (o limite de 3 vale por etapa).
3. Reavalie as seções da nova etapa na Fase 3 e siga o fluxo normal.
4. Se o usuário já tinha dado informação suficiente sobre a próxima etapa em mensagens anteriores, diga isso e vá direto ao gate dela.
