---
name: "spec-descoberta-scrum"
description: "Conduz a descoberta e especificação de projetos de produto/software para PMs, POs, Líderes Técnicos, Stakeholders, Engenheiros de Requisitos e Gerentes de Projeto seniores, com descoberta progressiva compatível com Scrum, entregue em etapas curtas e aprováveis (E1 Visão, E2 Regras e Requisitos, E3 Aceitação e Backlog, E4 Completo). NÃO gera o documento de imediato — pesquisa, mapeia lacunas por seção, calcula uma Pontuação de Completude por etapa, questiona só os pontos críticos da etapa e só produz o documento de 13 seções (Meta SMART, Regras de Negócio, Requisitos Funcionais, Critérios de Aceitação, Histórias de Usuário, Riscos, Matriz de Rastreabilidade etc.) quando a informação da etapa for suficiente. Use sempre que o usuário pedir para especificar, documentar, escopar ou levantar requisitos de um projeto, feature, produto ou iniciativa — mesmo sem citar \"descoberta\", \"backlog\" ou \"spec\", inclusive para \"preciso de um PRD\" ou \"uma primeira versão para aprovar\"."
---

# Spec de Descoberta Scrum

Framework de descoberta progressiva para especificação de produto. Transforma uma ideia de projeto, por mais vaga que seja, num documento rastreável e pronto para virar backlog Scrum — entregue **em etapas**, cada uma curta o bastante para ser aprovada, e só depois de garantir que existe informação suficiente para que ela seja confiável.

```
┌───────────┐   ┌────────────┐   ┌───────────────┐   ┌────────────────┐   ┌───────────┐
│ TRIAGEM   │ → │ DESCOBERTA │ → │ ANÁLISE DE     │ → │ QUESTIONAMENTO │ → │ DOCUMENTO │
│ (+ etapa- │   │            │   │ LACUNAS        │   │ CRÍTICO        │   │ DA ETAPA  │
│  alvo)    │   │            │   │ (score etapa)  │   │                │   │           │
└───────────┘   └────────────┘   └───────────────┘   └────────────────┘   └───────────┘
  obrigatória     obrigatória       obrigatória         condicional*        gated**

* Só roda se o gate da etapa não estiver satisfeito: lacuna crítica da etapa pendente
  ou score da etapa abaixo do limiar (ver etapas.md e pontuacao.md)
** O documento da etapa só é escrito quando o gate é satisfeito, ou quando o usuário
   assume explicitamente as lacunas restantes como risco aceito

Aprovada uma etapa, o ciclo recomeça para a próxima, reaproveitando tudo que já foi levantado.
```

## As etapas de entrega

Exigir um documento completo antes de mostrar qualquer coisa não combina com times em que cada etapa do projeto precisa ser aprovada mediante um entregável. Por isso o documento nasce em versões menores. A estrutura de 13 seções **não muda em nenhuma versão**; o que muda é quanto de cada seção já foi levantado e avaliado.

| Etapa | Nome | Seções avaliadas | Limiar | Versão |
| ----- | ---- | ---------------- | ------ | ------ |
| E1 | Visão | 1, 2, 3, 4 | 70% | v0.1 |
| E2 | Regras e Requisitos | 5, 6 (10 e 11 como rascunho) | 70% | v0.2 |
| E3 | Aceitação e Backlog | 7, 8, 9 | 75% | v0.3 |
| E4 | Completo | 1 a 11 | 80% | v1.0 |

A fonte de verdade desta tabela, dos itens bloqueantes de cada etapa e das regras de versionamento é `references/etapas.md`. O todo nunca é esquecido: o score global aparece em toda versão, e a seção 13 traz o mapa do que falta nas próximas etapas.

## Regra de ouro

**Nunca escreva o documento de nenhuma etapa na primeira interação.** O valor desta skill está em resistir ao impulso de produzir algo bonito rápido demais. Um documento gerado sobre suposições não verificadas é pior do que nenhum documento — ele passa confiança que a informação não sustenta. Cada seção só deve conter fatos declarados pelo usuário, encontrados em documentos fornecidos, ou (quando necessário e sinalizado) pesquisados na web; nunca invente regras de negócio, métricas ou critérios de aceitação para "preencher" uma seção.

Entregar menos por vez não autoriza inventar mais: as seções fora da etapa ficam como espaço reservado explícito, nunca preenchidas com suposição.

## Antes de começar: carregue as referências certas

- `references/etapas.md` — as quatro etapas, limiares, itens bloqueantes, como o documento de cada etapa é montado e versionado. Leia **sempre** na Fase 1, antes de definir a etapa-alvo.
- `references/secoes.md` — definição, perguntas-guia e checklist de completude de cada uma das 13 seções. Leia isso **sempre** antes da fase de Descoberta.
- `references/notacao-ears.md` — como escrever Requisitos Funcionais e Critérios de Aceitação em notação EARS (em português). Leia antes de redigir essas duas seções.
- `references/pontuacao.md` — a fórmula do score da etapa e do score global, pesos por seção, o critério de lacuna crítica e o gate de liberação. Leia antes da fase de Análise de Lacunas.
- `references/perguntas.md` — como priorizar e agrupar as perguntas de pontos críticos. Leia antes da fase de Questionamento.
- `references/bloco-de-estado.md` — formato do estado portátil do projeto, usado quando o ambiente não guarda arquivos entre sessões. Leia na Fase 1, ao decidir onde registrar o estado.

Carregue cada referência sob demanda, na fase correspondente — não é preciso carregar todas de uma vez.

## Onde guardar o estado

O estado do projeto (porte, etapa-alvo, fatos levantados por seção, scores, lacunas, premissas, rodada de questionamento, versão entregue, últimos IDs usados) precisa sobreviver entre mensagens e, idealmente, entre sessões. Escolha o mecanismo logo na Fase 1:

- **Ambiente com arquivos persistentes** (pasta de trabalho gravável que continua existindo na próxima sessão): use `.descoberta/<slug>/` com `descoberta.md` e `lacunas.md`, como descrito nas fases abaixo.
- **Ambiente sem persistência confiável** (a pasta de trabalho some ao fim da sessão, ou não há ferramentas de arquivo): termine cada resposta com o Bloco de Estado definido em `references/bloco-de-estado.md`, que carrega o necessário para retomar o projeto depois. Avise o usuário uma vez, em uma frase, que ele pode copiar esse bloco para continuar em outra conversa.

Na dúvida sobre a persistência, faça os dois: o custo do bloco é baixo e perder o estado é caro.

## Fase 1 — Triagem (obrigatória)

Objetivo: entender minimamente o que está sendo pedido, classificar o porte do projeto e definir a **etapa-alvo** do entregável, para calibrar a profundidade da descoberta.

1. A partir da primeira mensagem do usuário, identifique: nome/apelido do projeto, tipo (feature nova, produto novo, integração, migração, etc.), e quem é o solicitante (papel: PM, PO, Tech Lead, stakeholder...).
2. Classifique o porte como **Simples**, **Médio** ou **Complexo**:
   - **Simples**: escopo de um único fluxo/tela, sem integrações novas, sem impacto regulatório ou financeiro relevante.
   - **Médio**: múltiplos fluxos ou um sistema envolvido, alguma integração existente, impacto de negócio moderado.
   - **Complexo**: múltiplos sistemas/times, integrações novas, dados sensíveis, dinheiro, compliance, ou ambiguidade real sobre o problema a resolver.
3. Defina a etapa-alvo perguntando uma vez: **"Qual aprovação este entregável precisa destravar?"** (mapeamento e padrões em `references/etapas.md`). Se o usuário já disse isso, não pergunte de novo. Se ele não souber, escolha pelo porte (Simples → E4; Médio ou Complexo → E1) e diga qual escolheu.
4. Não peça nada disso em um formulário longo — infira o que puder do que o usuário já disse e confirme/pergunte só o que faltar, em poucas perguntas.
5. Registre o estado inicial conforme "Onde guardar o estado": se o ambiente persiste arquivos, crie (ou atualize, se já existir) a pasta de trabalho `.descoberta/<slug-do-projeto>/` com um `descoberta.md` inicial contendo nome do projeto, porte, solicitante, etapa-alvo e data; caso contrário, use o Bloco de Estado.

**Nunca pule esta fase** mesmo que o usuário já tenha mandado um bloco de texto detalhado — use esse texto para preencher a triagem automaticamente em vez de perguntar de novo, mas ainda assim registre a classificação de porte e a etapa-alvo.

## Fase 2 — Descoberta (obrigatória)

Objetivo: coletar o máximo de informação real, organizada por seção-alvo, antes de julgar o que falta.

1. Leia `references/secoes.md` e, para cada uma das 13 seções, identifique quais perguntas-guia já foram respondidas pelo que o usuário disse até agora. Registre tudo que o usuário disser sobre qualquer seção, inclusive as de etapas futuras: o todo importa, e isso poupa perguntas mais adiante. As perguntas novas, porém, se dirigem à etapa-alvo.
2. Fontes de informação, nesta ordem de prioridade:
   1. O que o usuário já escreveu na conversa.
   2. Documentos, planilhas, tickets ou specs que o usuário anexar ou apontar (leia-os por completo antes de assumir que cobrem uma seção).
   3. Conectores disponíveis (Jira, Confluence, Google Drive, Slack etc.) — se existir um conector relevante e conectado, use-o para buscar contexto do projeto real em vez de perguntar algo que já está documentado em outro lugar.
   4. Pesquisa web — **só quando** a lacuna for de contexto externo (mercado, concorrência, benchmark regulatório, prática do setor) e não de decisão interna do time. Nunca pesquise a web para "adivinhar" uma regra de negócio, meta ou critério de aceitação que só o time do usuário pode definir — isso é lacuna a ser perguntada, não pesquisada.
3. Registre os achados (em `.descoberta/<slug>/descoberta.md` ou no Bloco de Estado, conforme "Onde guardar o estado"), organizados pelas 13 seções, citando a origem de cada achado (usuário / documento X / conector Y / pesquisa web).
4. Não avalie completude ainda — essa é a Fase 3. Aqui o objetivo é só coletar.

## Fase 3 — Análise de Lacunas (obrigatória)

Objetivo: transformar o que foi coletado em pontuações objetivas, seção a seção, e decidir se a etapa-alvo pode ser entregue.

1. Leia `references/pontuacao.md`.
2. Para cada seção, marque cada item do checklist de `secoes.md` como preenchido, parcial ou ausente, e calcule o score da seção.
3. Calcule o **score da etapa** (só as seções avaliadas na etapa-alvo, com seus pesos) e o **score global** (as 11 seções). O primeiro decide a liberação; o segundo é a visão do todo.
4. Classifique cada lacuna encontrada como **crítica para a etapa** (bloqueia a confiabilidade do entregável; lista de bloqueantes em `etapas.md`) ou **não crítica / fora da etapa** (fica registrada como "a definir" sem comprometer o documento e sem ser perguntada agora).
5. Registre o resultado em `.descoberta/<slug>/lacunas.md` (ou no Bloco de Estado): tabela de seções com score, lacunas críticas da etapa, lacunas não críticas e fora da etapa.
6. Mostre ao usuário, de forma direta e sem rodeios, o score da etapa com o limiar dela, o score global em uma linha, e **quais são as lacunas críticas da etapa** — não a lista inteira de detalhes menores. Trate o usuário como sênior: um resumo objetivo do que falta e por que importa, não um checklist burocrático.
7. Aplique o gate de liberação de `pontuacao.md` (score da etapa ≥ limiar **e** nenhuma lacuna crítica da etapa pendente): se estiver satisfeito, siga para a Fase 5; se não, siga para a Fase 4.

## Fase 4 — Questionamento Crítico (condicional)

Roda **somente** se o gate de liberação da etapa não estiver satisfeito depois da Fase 3: há lacuna crítica da etapa pendente ou o score da etapa está abaixo do limiar.

1. Leia `references/perguntas.md`.
2. Pergunte apenas sobre a etapa-alvo. Agrupe as perguntas por seção afetada e priorize as lacunas críticas primeiro — nunca pergunte tudo de uma vez de forma desorganizada. Se não houver lacuna crítica e só o score estiver abaixo do limiar, pergunte as lacunas não críticas da etapa de maior impacto no score. Lacunas de outras etapas são só registradas.
3. Prefira perguntas objetivas e específicas ("Existe algum limite de valor ou de tentativas para essa transação?") a perguntas genéricas ("me fale mais sobre isso").
4. Depois das respostas, volte à Fase 3 e recalcule a pontuação. Isso pode se repetir, mas **limite a 3 rodadas de questionamento por etapa**; na terceira rodada, se o gate de liberação ainda não estiver satisfeito, apresente ao usuário a opção explícita de:
   - continuar respondendo, ou
   - seguir para o documento da etapa com as lacunas restantes registradas como **premissas assumidas** (não como fatos), claramente listadas na seção Pontuação de Prontidão.
5. Nunca decida sozinho por essa segunda opção — é uma escolha do usuário, não um atalho automático da skill.

## Fase 5 — Documento da Etapa (gated)

Só entra aqui quando o gate de liberação da etapa (ver `pontuacao.md` e `etapas.md`) estiver satisfeito ou o usuário tiver assumido explicitamente as lacunas restantes (Fase 4, passo 4).

1. Gere o documento em Markdown com **exatamente** estas 13 seções, nesta ordem — essa estrutura não muda em nenhuma versão:
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
2. Monte cada seção conforme `references/etapas.md`: conteúdo real nas seções da etapa e das etapas anteriores; espaço reservado de uma linha nas seções de etapas futuras; rascunho sinalizado de Dependências e Riscos no E2. Cabeçalho com título, versão e etapa.
3. Use os templates e a numeração de IDs (RN-xxx, RF-xxx, CA-xxx, HU-xxx, RNF-xxx, DEP-xxx, RISCO-xxx) definidos em `references/secoes.md`. Os IDs são estáveis entre versões: nunca renumere nem reutilize.
4. Escreva Requisitos Funcionais e Critérios de Aceitação em notação EARS, conforme `references/notacao-ears.md`.
5. A partir do E3, a Matriz de Rastreabilidade deve cruzar cada RF com as CA, HU e RN relacionadas — nenhum RF pode ficar sem pelo menos um CA e uma HU associados; se ficar, isso é uma lacuna que deveria ter sido pega na Fase 3.
6. A seção Pontuação de Prontidão é a única que expõe o "estado interno" do processo ao leitor final: score por seção, score da etapa, score global (sempre), premissas assumidas (se houver), itens marcados como "a definir", mapa das próximas etapas e histórico de versões.
7. Entregue o documento como arquivo Markdown (`<slug>-spec-v<versão>.md`): grave-o no diretório de saída do ambiente e apresente-o ao usuário pela ferramenta de entrega de arquivos disponível. Se o ambiente não tiver ferramentas de arquivo, entregue o documento completo na própria resposta. Não recrie do zero o conteúdo já registrado (em `.descoberta/<slug>/` ou no Bloco de Estado) — consolide o que foi levantado e validado nas fases anteriores. Ao passar de uma etapa para outra, a nova versão nasce como cópia da anterior, que fica intacta como registro do que foi aprovado.
8. Depois de entregar, se o usuário pedir alterações dentro da mesma etapa, edite o arquivo existente em vez de regenerar tudo — e, se a mudança afetar requisitos ou regras já rastreados, atualize a Matriz de Rastreabilidade e a Pontuação de Prontidão de acordo. Mudanças em conteúdo já aprovado, numa etapa posterior, seguem a regra de `etapas.md`.
9. Feche com uma frase dizendo o que é a próxima etapa e o que mais pesa nela. Só avance quando o usuário pedir ou disser que a etapa foi aprovada.

## Retomando um projeto em andamento

Se o usuário mencionar um projeto que já tem uma pasta em `.descoberta/`, leia `descoberta.md` e `lacunas.md` antes de perguntar qualquer coisa — não repita perguntas já respondidas em uma sessão anterior. Se o estado salvo estiver desatualizado em relação ao que o usuário está dizendo agora, o que ele diz agora prevalece; atualize os arquivos de trabalho. Se o usuário colar um Bloco de Estado de uma sessão anterior (ver `references/bloco-de-estado.md`), trate-o como o estado salvo, no lugar dos arquivos de trabalho. Se ele disser que a etapa anterior foi aprovada e quer a próxima, siga "Avançando de etapa" em `references/etapas.md`.

## Comportamento de saída

Conduza cada fase de forma natural — não anuncie "agora vou executar a Fase 2 de Descoberta". Faça o trabalho da fase e mostre o resultado (achados, lacunas, perguntas, ou o documento). O usuário sênior quer avançar rápido com qualidade, não acompanhar a mecânica interna do processo.
