# Spec de Descoberta Scrum

Uma skill de IA para conduzir a **descoberta e especificação de projetos de produto/software** — para Gerentes de Produto, Product Owners, Líderes Técnicos, Stakeholders, Engenheiros de Requisitos e Gerentes de Projeto.

Em vez de gerar um documento bonito na primeira resposta, a skill segue um framework de **descoberta progressiva**: pesquisa o que já foi dito, identifica lacunas seção por seção, calcula uma pontuação de completude, questiona apenas os pontos críticos e só produz o documento de cada etapa quando há informação suficiente para que ele seja confiável.

O resultado é um documento único, rastreável, com IDs cruzados entre regras de negócio, requisitos, critérios de aceitação e histórias de usuário — pronto para virar backlog Scrum. Ele é entregue **em etapas** (Visão, Regras e Requisitos, Aceitação e Backlog, Completo), para que cada aprovação do time tenha um entregável curto, sem abrir mão da visão do todo.

## Por que isso importa

É comum um agente de IA, ao ser pedido para "especificar" um projeto, preencher lacunas com suposições plausíveis só para entregar algo completo rápido. Isso passa uma falsa sensação de prontidão: regras de negócio inventadas, critérios de aceitação genéricos, riscos que ninguém validou. Esta skill inverte a prioridade — ela resiste a gerar o documento até que o score de completude comprove que há substância real por trás de cada seção, e nunca esconde uma lacuna: ela aparece explicitamente na última seção do documento, a Pontuação de Prontidão.

Em times onde cada etapa do projeto precisa ser aprovada mediante um entregável, exigir um score alto de tudo antes de mostrar qualquer coisa é caro. Por isso o gate de completude é aplicado **por etapa**: cada versão do documento é avaliada só nas seções dela, com um limiar próprio, e o score global aparece sempre para que ninguém perca a visão do todo.

## Etapas de entrega

| Etapa | Nome | Seções avaliadas | Limiar | Versão |
| ----- | ---- | ---------------- | ------ | ------ |
| E1 | Visão | 1, 2, 3, 4 | 70% | v0.1 |
| E2 | Regras e Requisitos | 5, 6 (10 e 11 como rascunho) | 70% | v0.2 |
| E3 | Aceitação e Backlog | 7, 8, 9 | 75% | v0.3 |
| E4 | Completo | 1 a 11 | 80% | v1.0 |

Na Triagem, a skill pergunta **qual aprovação o entregável precisa destravar** e escolhe a etapa a partir da resposta (ou do porte do projeto, se você não souber). Cada etapa tem seus próprios itens bloqueantes, seu limite de 3 rodadas de perguntas, e gera um arquivo versionado (`<slug>-spec-v0.1.md`, `v0.2`, ...). Os IDs (`RN-001`, `RF-001`...) são estáveis entre versões, e as versões anteriores ficam intactas como trilha do que cada aprovação viu.

## Estrutura do documento gerado

Sempre estas 13 seções, nesta ordem, em **toda versão** — as seções de etapas futuras aparecem como espaço reservado, nunca preenchidas com suposição:

1. Resumo Executivo - Descoberta
2. Meta SMART
3. Processos de Negócio
4. Detalhes do Projeto
5. Regras de Negócio
6. Requisitos Funcionais (notação EARS)
7. Critérios de Aceitação (Dado/Quando/Então)
8. Histórias de Usuário
9. Requisitos Não Funcionais
10. Dependências
11. Riscos
12. Matriz de Rastreabilidade
13. Pontuação de Prontidão

## Como funciona o fluxo

```
Triagem → Descoberta → Análise de Lacunas → Questionamento Crítico → Documento da Etapa
(sempre,   (sempre)     (sempre; score da     (só se houver lacuna    (só libera com score
 define a                etapa + global)       crítica da etapa,       da etapa ≥ limiar e sem
 etapa-alvo)                                   máx. 3 rodadas)         lacuna crítica, ou com
                                                                       aceite explícito do usuário)
```

- **Seções críticas** (peso dobrado no score): Regras de Negócio, Requisitos Funcionais, Critérios de Aceitação e Riscos — são as que sustentam a confiabilidade do resto do documento.
- **IDs rastreáveis**: `RN-xxx`, `RF-xxx`, `CA-xxx`, `HU-xxx`, `RNF-xxx`, `DEP-xxx`, `RISCO-xxx`, cruzados na Matriz de Rastreabilidade — nenhum requisito funcional fica sem critério de aceitação e história de usuário associados.
- **Limiar de liberação**: por etapa (70% / 70% / 75% / 80%, tabela acima), sobre a completude ponderada das seções da etapa. Ajustável em `references/etapas.md`; o score global é sempre exibido, mas só decide a liberação no E4.

## Duas versões neste repositório

### 1. Skill completa (`SKILL.md` + `references/`)

Formato de skill em camadas (progressive disclosure), pensado para agentes com boa capacidade de seguir instruções longas e carregar arquivos de referência sob demanda — Claude (claude.ai, Claude Code, Claude Cowork), Cursor, e agentes equivalentes.

```
.
├── SKILL.md                      # fluxo principal das 5 fases
└── references/
    ├── etapas.md                 # etapas E1–E4, limiares, bloqueantes e versionamento
    ├── secoes.md                 # definição e checklist das 13 seções
    ├── notacao-ears.md           # notação EARS para requisitos e critérios
    ├── pontuacao.md              # fórmula de score (etapa e global) e gate de liberação
    ├── perguntas.md              # como priorizar e formular as perguntas críticas
    └── bloco-de-estado.md        # estado portátil para ambientes sem arquivos persistentes
```

**Instalação:** copie a pasta inteira (ou o arquivo `.skill` empacotado, se você gerou um) para o diretório de skills do seu agente. Em Claude, isso normalmente significa adicionar a skill ao seu perfil/organização e deixar o agente descobri-la pela `description` do `SKILL.md`.

### 2. Versão para Copilot / agentes leves (`copilot/spec-descoberta-scrum.md`)

Arquivo único e autossuficiente, sem dependência de arquivos externos, ferramentas de busca ou memória persistente de arquivos — pensado para agentes com contexto mais curto ou maior tendência a alucinar (ex.: GitHub Copilot Chat na versão gratuita), onde múltiplos arquivos de referência viram risco em vez de organização.

Principais diferenças em relação à skill completa:
- Todo o conteúdo (etapas, checklist, EARS, fórmula de score, regras de questionamento) está inline em um único arquivo.
- O estado do processo (etapa-alvo, fase atual, scores, lacunas, premissas, últimos IDs) é impresso como um **Bloco de Estado** em texto ao final de cada resposta, em vez de salvo em arquivo — o usuário pode colar esse bloco de volta em uma nova conversa para retomar de onde parou.
- Nenhuma ferramenta externa (busca na web, conectores) é usada — toda informação vem do que o usuário escreve na conversa.
- As regras de negócio da skill viraram condições SE/ENTÃO explícitas e um checklist anti-alucinação obrigatório antes de qualquer entrega de documento.

**Instalação:** cole o conteúdo de `copilot/spec-descoberta-scrum.md` como a primeira mensagem da conversa, ou configure-o como instrução de sistema/custom instructions do seu agente.

## Uso típico

1. Descreva o projeto/feature que você quer especificar, com o máximo de contexto que já tiver à mão.
2. O agente classifica o porte (Simples/Médio/Complexo), pergunta qual aprovação o entregável precisa destravar para definir a etapa-alvo, e começa a mapear o que já foi coberto nas 13 seções.
3. Ele mostra a pontuação da etapa (e o score global em uma linha) e, se houver lacunas críticas da etapa, faz perguntas objetivas agrupadas por prioridade — nunca uma lista genérica de tudo que falta.
4. Depois de respondidas as lacunas críticas (ou de você aceitar explicitamente seguir com elas em aberto), o documento da etapa é gerado com IDs rastreáveis e a Pontuação de Prontidão como última seção, mostrando exatamente o que é fato confirmado, o que é premissa assumida e o que falta nas próximas etapas.
5. Quando a etapa for aprovada, peça a próxima: a skill reaproveita tudo que já foi levantado e gera a versão seguinte.

## Contribuindo

Sugestões, ajustes de peso/limiar para outros contextos de domínio, traduções e melhorias de clareza são bem-vindos via issues ou pull requests.

## Licença

[MIT](./LICENSE) — livre para uso, modificação e redistribuição pela comunidade.
