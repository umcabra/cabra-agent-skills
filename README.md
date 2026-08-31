# Spec de Descoberta Scrum

Uma skill de IA para conduzir a **descoberta e especificação de projetos de produto/software** — para Gerentes de Produto, Product Owners, Líderes Técnicos, Stakeholders, Engenheiros de Requisitos e Gerentes de Projeto.

Em vez de gerar um documento bonito na primeira resposta, a skill segue um framework de **descoberta progressiva**: pesquisa o que já foi dito, identifica lacunas seção por seção, calcula uma pontuação de completude, questiona apenas os pontos críticos e só produz o documento final quando há informação suficiente para que ele seja confiável.

O resultado é um documento único, rastreável, com IDs cruzados entre regras de negócio, requisitos, critérios de aceitação e histórias de usuário — pronto para virar backlog Scrum.

## Por que isso importa

É comum um agente de IA, ao ser pedido para "especificar" um projeto, preencher lacunas com suposições plausíveis só para entregar algo completo rápido. Isso passa uma falsa sensação de prontidão: regras de negócio inventadas, critérios de aceitação genéricos, riscos que ninguém validou. Esta skill inverte a prioridade — ela resiste a gerar o documento até que o score de completude comprove que há substância real por trás de cada seção, e nunca esconde uma lacuna: ela aparece explicitamente na última seção do documento, a Pontuação de Prontidão.

## Estrutura do documento gerado

Sempre estas 13 seções, nesta ordem:

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
Triagem → Descoberta → Análise de Lacunas → Questionamento Crítico → Documento Final
(sempre)   (sempre)     (sempre)             (só se houver          (só libera com
                                              lacuna crítica,         score ≥ 80%, ou
                                              máx. 3 rodadas)         aceite explícito
                                                                      do usuário)
```

- **Seções críticas** (peso dobrado no score): Regras de Negócio, Requisitos Funcionais, Critérios de Aceitação e Riscos — são as que sustentam a confiabilidade do resto do documento.
- **IDs rastreáveis**: `RN-xxx`, `RF-xxx`, `CA-xxx`, `HU-xxx`, `RNF-xxx`, `DEP-xxx`, `RISCO-xxx`, cruzados na Matriz de Rastreabilidade — nenhum requisito funcional fica sem critério de aceitação e história de usuário associados.
- **Limiar de liberação**: 80% de completude ponderada. Ajustável em `references/pontuacao.md`.

## Duas versões neste repositório

### 1. Skill completa (`SKILL.md` + `references/`)

Formato de skill em camadas (progressive disclosure), pensado para agentes com boa capacidade de seguir instruções longas e carregar arquivos de referência sob demanda — Claude (claude.ai, Claude Code, Claude Cowork), Cursor, e agentes equivalentes.

```
.
├── SKILL.md                      # fluxo principal das 5 fases
└── references/
    ├── secoes.md                 # definição e checklist das 13 seções
    ├── notacao-ears.md           # notação EARS para requisitos e critérios
    ├── pontuacao.md              # fórmula de score, pesos e limiares
    └── perguntas.md              # como priorizar e formular as perguntas críticas
```

**Instalação:** copie a pasta inteira (ou o arquivo `.skill` empacotado, se você gerou um) para o diretório de skills do seu agente. Em Claude, isso normalmente significa adicionar a skill ao seu perfil/organização e deixar o agente descobri-la pela `description` do `SKILL.md`.

### 2. Versão para Copilot / agentes leves (`copilot/spec-descoberta-scrum.md`)

Arquivo único e autossuficiente, sem dependência de arquivos externos, ferramentas de busca ou memória persistente de arquivos — pensado para agentes com contexto mais curto ou maior tendência a alucinar (ex.: GitHub Copilot Chat na versão gratuita), onde múltiplos arquivos de referência viram risco em vez de organização.

Principais diferenças em relação à skill completa:
- Todo o conteúdo (checklist, EARS, fórmula de score, regras de questionamento) está inline em um único arquivo.
- O estado do processo (fase atual, scores, lacunas, premissas) é impresso como um **Bloco de Estado** em texto ao final de cada resposta, em vez de salvo em arquivo — o usuário pode colar esse bloco de volta em uma nova conversa para retomar de onde parou.
- Nenhuma ferramenta externa (busca na web, conectores) é usada — toda informação vem do que o usuário escreve na conversa.
- As regras de negócio da skill viraram condições SE/ENTÃO explícitas e um checklist anti-alucinação obrigatório antes de qualquer entrega do documento final.

**Instalação:** cole o conteúdo de `copilot/spec-descoberta-scrum.md` como a primeira mensagem da conversa, ou configure-o como instrução de sistema/custom instructions do seu agente.

## Uso típico

1. Descreva o projeto/feature que você quer especificar, com o máximo de contexto que já tiver à mão.
2. O agente classifica o porte (Simples/Médio/Complexo) e começa a mapear o que já foi coberto nas 13 seções.
3. Ele mostra a pontuação de completude e, se houver lacunas críticas, faz perguntas objetivas agrupadas por prioridade — nunca uma lista genérica de tudo que falta.
4. Depois de respondidas as lacunas críticas (ou de você aceitar explicitamente seguir com elas em aberto), o documento final é gerado com IDs rastreáveis e a Pontuação de Prontidão como última seção, mostrando exatamente o que é fato confirmado e o que é premissa assumida.

## Contribuindo

Sugestões, ajustes de peso/limiar para outros contextos de domínio, traduções e melhorias de clareza são bem-vindos via issues ou pull requests.

## Licença

[MIT](./LICENSE) — livre para uso, modificação e redistribuição pela comunidade.
