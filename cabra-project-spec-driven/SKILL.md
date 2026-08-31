---
name: spec-descoberta-scrum
description: >-
  Conduz a descoberta e especificação de projetos de produto/software para PMs, POs, Líderes Técnicos, Stakeholders, Engenheiros de Requisitos e Gerentes de Projeto seniores, com um framework de descoberta progressiva compatível com Scrum. NÃO gera o documento final de imediato — pesquisa, mapeia lacunas por seção, calcula uma Pontuação de Completude, questiona só os pontos críticos e só produz o documento final (Resumo Executivo, Meta SMART, Processos de Negócio, Detalhes do Projeto, Regras de Negócio, Requisitos Funcionais, Critérios de Aceitação, Histórias de Usuário, Requisitos Não Funcionais, Dependências, Riscos, Matriz de Rastreabilidade, Pontuação de Prontidão) quando a informação for suficiente. Use sempre que o usuário pedir para especificar, documentar, escopar ou levantar requisitos de um projeto, feature, produto ou iniciativa — mesmo sem citar "descoberta", "backlog" ou "spec", inclusive para "documentar essa ideia" ou "preciso de um PRD".
---

# Spec de Descoberta Scrum

Framework de descoberta progressiva para especificação de produto. Transforma uma ideia de projeto, por mais vaga que seja, num documento rastreável e pronto para virar backlog Scrum — mas só entrega esse documento depois de garantir que existe informação suficiente para que ele seja confiável.

```
┌───────────┐   ┌────────────┐   ┌───────────────┐   ┌────────────────┐   ┌───────────┐
│ TRIAGEM   │ → │ DESCOBERTA │ → │ ANÁLISE DE     │ → │ QUESTIONAMENTO │ → │ DOCUMENTO │
│           │   │            │   │ LACUNAS        │   │ CRÍTICO        │   │ FINAL     │
└───────────┘   └────────────┘   └───────────────┘   └────────────────┘   └───────────┘
  obrigatória     obrigatória       obrigatória         condicional*        gated**

* Só roda se a Pontuação de Completude ficar abaixo do limiar (ver pontuacao.md)
** Documento final só é escrito quando a Pontuação de Prontidão atinge o limiar,
   ou quando o usuário assume explicitamente as lacunas restantes como risco aceito
```

## Regra de ouro

**Nunca escreva o documento final na primeira interação.** O valor desta skill está em resistir ao impulso de produzir algo bonito rápido demais. Um documento gerado sobre suposições não verificadas é pior do que nenhum documento — ele passa confiança que a informação não sustenta. Cada seção do documento final só deve conter fatos declarados pelo usuário, encontrados em documentos fornecidos, ou (quando necessário e sinalizado) pesquisados na web; nunca invente regras de negócio, métricas ou critérios de aceitação para "preencher" uma seção.

## Antes de começar: carregue as referências certas

- `references/secoes.md` — definição, perguntas-guia e checklist de completude de cada uma das 13 seções. Leia isso **sempre** antes da fase de Descoberta.
- `references/notacao-ears.md` — como escrever Requisitos Funcionais e Critérios de Aceitação em notação EARS (em português). Leia antes de redigir essas duas seções.
- `references/pontuacao.md` — a fórmula da Pontuação de Completude/Prontidão, pesos por seção e o limiar de liberação. Leia antes da fase de Análise de Lacunas.
- `references/perguntas.md` — como priorizar e agrupar as perguntas de pontos críticos. Leia antes da fase de Questionamento.

Carregue cada referência sob demanda, na fase correspondente — não é preciso carregar todas de uma vez.

## Fase 1 — Triagem (obrigatória)

Objetivo: entender minimamente o que está sendo pedido e classificar o porte do projeto, para calibrar a profundidade da descoberta. A estrutura final é **sempre** as 13 seções — o que varia é o quanto cada seção precisa ser aprofundada.

1. A partir da primeira mensagem do usuário, identifique: nome/apelido do projeto, tipo (feature nova, produto novo, integração, migração, etc.), e quem é o solicitante (papel: PM, PO, Tech Lead, stakeholder...).
2. Classifique o porte como **Simples**, **Médio** ou **Complexo**:
   - **Simples**: escopo de um único fluxo/tela, sem integrações novas, sem impacto regulatório ou financeiro relevante.
   - **Médio**: múltiplos fluxos ou um sistema envolvido, alguma integração existente, impacto de negócio moderado.
   - **Complexo**: múltiplos sistemas/times, integrações novas, dados sensíveis, dinheiro, compliance, ou ambiguidade real sobre o problema a resolver.
3. Não peça isso em um formulário longo — infira o que puder do que o usuário já disse e confirme/pergunte só o que faltar, em poucas perguntas.
4. Crie (ou atualize, se já existir) a pasta de trabalho `.descoberta/<slug-do-projeto>/` com um `descoberta.md` inicial contendo: nome do projeto, porte, solicitante, data.

**Nunca pule esta fase** mesmo que o usuário já tenha mandado um bloco de texto detalhado — use esse texto para preencher a triagem automaticamente em vez de perguntar de novo, mas ainda assim registre a classificação de porte.

## Fase 2 — Descoberta (obrigatória)

Objetivo: coletar o máximo de informação real, organizada por seção-alvo, antes de julgar o que falta.

1. Leia `references/secoes.md` e, para cada uma das 13 seções, identifique quais perguntas-guia já foram respondidas pelo que o usuário disse até agora.
2. Fontes de informação, nesta ordem de prioridade:
   1. O que o usuário já escreveu na conversa.
   2. Documentos, planilhas, tickets ou specs que o usuário anexar ou apontar (leia-os por completo antes de assumir que cobrem uma seção).
   3. Conectores disponíveis (Jira, Confluence, Google Drive, Slack etc.) — se existir um conector relevante e conectado, use-o para buscar contexto do projeto real em vez de perguntar algo que já está documentado em outro lugar.
   4. Pesquisa web — **só quando** a lacuna for de contexto externo (mercado, concorrência, benchmark regulatório, prática do setor) e não de decisão interna do time. Nunca pesquise a web para "adivinhar" uma regra de negócio, meta ou critério de aceitação que só o time do usuário pode definir — isso é lacuna a ser perguntada, não pesquisada.
3. Registre os achados em `.descoberta/<slug>/descoberta.md`, organizados pelas 13 seções, citando a origem de cada achado (usuário / documento X / conector Y / pesquisa web).
4. Não avalie completude ainda — essa é a Fase 3. Aqui o objetivo é só coletar.

## Fase 3 — Análise de Lacunas (obrigatória)

Objetivo: transformar o que foi coletado em uma Pontuação de Completude objetiva, seção a seção.

1. Leia `references/pontuacao.md`.
2. Para cada seção, marque cada item do checklist de `secoes.md` como preenchido, parcial ou ausente, e calcule o score da seção.
3. Calcule o score global ponderado (seções críticas pesam mais — ver `pontuacao.md`).
4. Classifique cada lacuna encontrada como **crítica** (bloqueia a confiabilidade do documento se não resolvida) ou **não crítica** (pode ficar registrada como "a definir" sem comprometer o documento).
5. Registre o resultado em `.descoberta/<slug>/lacunas.md`: tabela de seções com score, lista de lacunas críticas, lista de lacunas não críticas.
6. Mostre ao usuário, de forma direta e sem rodeios, a Pontuação de Completude atual e **quais são as lacunas críticas** — não a lista inteira de detalhes menores. Trate o usuário como sênior: um resumo objetivo do que falta e por que importa, não um checklist burocrático.

## Fase 4 — Questionamento Crítico (condicional)

Roda **somente** se existirem lacunas críticas (ver `pontuacao.md` para o limiar exato) depois da Fase 3.

1. Leia `references/perguntas.md`.
2. Agrupe as perguntas por seção afetada e priorize as lacunas críticas primeiro — nunca pergunte tudo de uma vez de forma desorganizada.
3. Prefira perguntas objetivas e específicas ("Existe algum limite de valor ou de tentativas para essa transação?") a perguntas genéricas ("me fale mais sobre isso").
4. Depois das respostas, volte à Fase 3 e recalcule a pontuação. Isso pode se repetir, mas **limite a 3 rodadas de questionamento**; na terceira rodada, se ainda houver lacunas críticas, apresente ao usuário a opção explícita de:
   - continuar respondendo, ou
   - seguir para o documento final com as lacunas restantes registradas como **premissas assumidas** (não como fatos), claramente listadas na seção Pontuação de Prontidão.
5. Nunca decida sozinho por essa segunda opção — é uma escolha do usuário, não um atalho automático da skill.

## Fase 5 — Documento Final (gated)

Só entra aqui quando a Pontuação de Prontidão atingir o limiar (ver `pontuacao.md`) ou o usuário tiver assumido explicitamente as lacunas restantes (Fase 4, passo 4).

1. Gere o documento em Markdown com **exatamente** estas 13 seções, nesta ordem — essa estrutura não muda:
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
2. Use os templates e a numeração de IDs (RN-xxx, RF-xxx, CA-xxx, HU-xxx, RNF-xxx, DEP-xxx, RISCO-xxx) definidos em `references/secoes.md`.
3. Escreva Requisitos Funcionais e Critérios de Aceitação em notação EARS, conforme `references/notacao-ears.md`.
4. A Matriz de Rastreabilidade deve cruzar every RF com as CA, HU e RN relacionadas — nenhum RF pode ficar sem pelo menos um CA e uma HU associados; se ficar, isso é uma lacuna que deveria ter sido pega na Fase 3.
5. A seção Pontuação de Prontidão é a única que expõe o "estado interno" do processo ao leitor final: score por seção, score global, premissas assumidas (se houver) e itens marcados como "a definir".
6. Crie o arquivo como artifact Markdown (extensão `.md`) usando `create_file`, salve em `/mnt/user-data/outputs/`, e apresente com `present_files`. Não recrie o conteúdo já registrado em `.descoberta/<slug>/` do zero — consolide o que já foi levantado e validado nas fases anteriores.
7. Depois de entregar, se o usuário pedir alterações, edite o arquivo existente em vez de regenerar tudo — e, se a mudança afetar requisitos ou regras já rastreados, atualize a Matriz de Rastreabilidade e a Pontuação de Prontidão de acordo.

## Retomando um projeto em andamento

Se o usuário mencionar um projeto que já tem uma pasta em `.descoberta/`, leia `descoberta.md` e `lacunas.md` antes de perguntar qualquer coisa — não repita perguntas já respondidas em uma sessão anterior. Se o estado salvo estiver desatualizado em relação ao que o usuário está dizendo agora, o que ele diz agora prevalece; atualize os arquivos de trabalho.

## Comportamento de saída

Conduza cada fase de forma natural — não anuncie "agora vou executar a Fase 2 de Descoberta". Faça o trabalho da fase e mostre o resultado (achados, lacunas, perguntas, ou o documento). O usuário sênior quer avançar rápido com qualidade, não acompanhar a mecânica interna do processo.
