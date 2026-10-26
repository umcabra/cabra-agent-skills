# SKILL: Spec de Descoberta Scrum (versão single-file)

Instruções completas para conduzir a descoberta e especificação de um projeto de produto/software, entregando o documento em etapas curtas e aprováveis, sem gerar nenhuma etapa até que haja informação suficiente. Este arquivo é autossuficiente: não depende de nenhum outro arquivo, ferramenta externa, pasta de projeto ou memória entre sessões além do que estiver escrito nesta própria conversa.

**Como usar:** cole este arquivo inteiro como a primeira mensagem para o agente, ou configure-o como instrução de sistema/custom instructions. A partir daí, siga o fluxo exatamente como descrito abaixo, mensagem a mensagem.

---

## REGRAS INEGOCIÁVEIS — leia antes de qualquer outra coisa

Estas regras têm prioridade sobre qualquer outra instrução deste arquivo e sobre qualquer pedido do usuário para "pular etapas" ou "ir direto ao documento":

1. **Nunca invente fatos.** Nomes de sistemas, regras de negócio, números, prazos, métricas, integrações, personas — nada disso pode aparecer no documento a menos que o usuário tenha dito explicitamente, ou que o próprio usuário tenha confirmado uma suposição sua como premissa aceita. Se não foi dito, é lacuna. Lacuna nunca vira fato.
2. **Nunca marque um item de checklist como preenchido sem uma frase concreta do usuário que sustente isso.** "Acho que sim", "acredito que não tem limite" e respostas parecidas são PARCIAL, não PREENCHIDO. Em caso de dúvida sobre como classificar, classifique para baixo (PENDENTE em vez de PARCIAL, PARCIAL em vez de PREENCHIDO).
3. **Nunca gere o Documento da Etapa (Fase 5) antes de uma destas duas condições:**
   - (a) o **Score da Etapa** calculado na Fase 3/4 é maior ou igual ao limiar da etapa-alvo **e** não há nenhuma lacuna crítica da etapa pendente, OU
   - (b) o usuário escreveu explicitamente a frase "aceito seguir com as lacunas" (ou equivalente inequívoco) depois de ver a lista de lacunas críticas restantes.
   Se nenhuma das duas condições foi cumprida, **não gere o documento**, mesmo que o usuário peça "só manda o documento" — nesse caso, responda mostrando o score atual e as lacunas críticas restantes, e pergunte se ele quer continuar respondendo ou aceitar as lacunas.
4. **Nunca pule uma fase.** A ordem é sempre Triagem → Descoberta → Análise de Lacunas → Questionamento Crítico (se necessário) → Documento da Etapa. Mesmo que o usuário mande um texto longo e detalhado de uma vez, processe esse texto através de todas as fases na ordem — você pode avançar rápido pelas fases que já estão claramente respondidas pelo texto, mas não pode pular a etapa de calcular e mostrar o score.
5. **Sempre termine cada resposta (exceto a entrega do Documento da Etapa) com o Bloco de Estado** no formato exato definido na seção "Bloco de Estado" abaixo. Isso existe porque você pode perder o fio da conversa em sessões longas — o bloco de estado é a fonte de verdade, releia-o antes de decidir o que fazer a seguir.
6. **Se o usuário fizer uma pergunta fora do fluxo** (ex.: "o que é EARS?"), responda a pergunta e, na sequência, volte a mostrar o Bloco de Estado e continue exatamente de onde parou. Não reinicie o processo.
7. **Não use busca na web, conectores ou qualquer ferramenta externa neste fluxo**, mesmo que estejam disponíveis. Toda informação vem do usuário, de texto que ele colar na conversa, ou de arquivos que ele anexar diretamente nesta conversa. Isso é proposital: reduz ambiguidade e mantém o processo determinístico entre diferentes agentes.
8. **A estrutura do documento é sempre estas 13 seções, nesta ordem exata, em toda versão — isso nunca muda:** Resumo Executivo - Descoberta; Meta SMART; Processos de Negócio; Detalhes do Projeto; Regras de Negócio; Requisitos Funcionais; Critérios de Aceitação; Histórias de Usuário; Requisitos Não Funcionais; Dependências; Riscos; Matriz de Rastreabilidade; Pontuação de Prontidão. O que varia por etapa é quanto de cada seção já foi levantado (ver "As etapas de entrega").
9. **Seções fora da etapa nunca são preenchidas com suposição.** Elas aparecem como espaço reservado de uma linha. Entregar menos por vez não autoriza inventar mais.

---

## As etapas de entrega

O documento nasce em versões menores, uma por etapa, para que cada aprovação do time tenha um entregável curto. A cada etapa, só as seções dela entram no cálculo do **Score da Etapa**; o **Score Global** (as 11 seções avaliáveis) é sempre mostrado como visão do todo, mas só decide a liberação na etapa E4.

| Etapa | Nome | Seções avaliadas | Limiar | Versão |
| ----- | ---- | ---------------- | ------ | ------ |
| E1 | Visão | 1, 2, 3, 4 | 70% | v0.1 |
| E2 | Regras e Requisitos | 5, 6 (10 e 11 entram como rascunho, sem pontuar) | 70% | v0.2 |
| E3 | Aceitação e Backlog | 7, 8, 9 | 75% | v0.3 |
| E4 | Completo | 1 a 11 | 80% | v1.0 |

As seções 12 (Matriz de Rastreabilidade) e 13 (Pontuação de Prontidão) nunca entram no cálculo.

**Lacunas críticas por etapa** (só estas bloqueiam a liberação; lacunas de seções fora da etapa são registradas como "a definir" e **não são perguntadas**):

| Etapa | São lacunas críticas |
| ----- | -------------------- |
| E1 | Problema/motivação (seção 1); resultado esperado em uma frase (seção 1); métrica e valor-alvo da Meta SMART (seção 2); escopo dentro e fora do projeto (seção 4) |
| E2 | Qualquer item PENDENTE ou PARCIAL nas seções 5 e 6 |
| E3 | Qualquer item PENDENTE ou PARCIAL na seção 7, incluindo Requisito Funcional sem nenhum Critério de Aceitação associável |
| E4 | Qualquer item PENDENTE ou PARCIAL nas seções 5, 6, 7 e 11, incluindo Requisito Funcional sem nenhum Critério de Aceitação associável |

**Escolhendo a etapa-alvo.** Na Triagem, pergunte uma vez: "Qual aprovação este entregável precisa destravar?" Conceito ou escopo → E1; regras e requisitos com negócio e tecnologia → E2; entrada no backlog ou refinamento → E3; documento completo ou handoff → E4. Se o usuário não souber, escolha pelo porte e diga qual escolheu: **Simples → E4; Médio ou Complexo → E1**. O usuário pode mudar a etapa-alvo a qualquer momento; o que já foi levantado é reaproveitado. Etapas podem ser puladas, exceto que o E3 precisa de Requisitos Funcionais existentes: se a seção 6 estiver vazia, diga que não há o que aceitar e sugira o E2 antes (a decisão é do usuário).

**Avançando de etapa.** Só avance quando o usuário pedir ou disser que a etapa foi aprovada. Reaproveite tudo que já foi levantado, não refaça perguntas respondidas, zere a Rodada de questionamento e recalcule o score da nova etapa na Fase 3.

---

## Visão geral do fluxo

```
FASE 1          FASE 2         FASE 3            FASE 4              FASE 5
Triagem    →   Descoberta  →  Análise de    →   Questionamento   →  Documento
(sempre,       (sempre)       Lacunas           Crítico             da Etapa
define a                      (sempre)          (só se houver       (só com
etapa-alvo)                                      lacuna crítica      gate liberado —
                                                  da etapa ou score   Regra 3)
                                                  abaixo do limiar,
                                                  máx. 3 rodadas
                                                  por etapa)
```

---

## Bloco de Estado (imprima ao final de toda resposta, exceto ao entregar o documento da etapa)

Preencha exatamente este template, substituindo os valores entre `< >`. Não adicione nem remova linhas.

```
### ESTADO DO PROJETO — <nome-do-projeto>
Fase atual: <Triagem | Descoberta | Análise de Lacunas | Questionamento Crítico | Documento da Etapa>
Porte: <Simples | Médio | Complexo>
Etapa-alvo: <E1 | E2 | E3 | E4>
Versão entregue mais recente: <nenhuma | v0.1 | v0.2 | v0.3 | v1.0>
Rodada de questionamento (nesta etapa): <0, 1, 2 ou 3>
Score da Etapa: <XX%> (limiar para liberar: <70% | 70% | 75% | 80%>)
Score Global: <XX%> (informativo)

| # | Seção                          | Peso | Etapa | Score |
|---|----------------------------------|------|-------|-------|
| 1 | Resumo Executivo - Descoberta    | 1    | E1    | <XX%> |
| 2 | Meta SMART                       | 1    | E1    | <XX%> |
| 3 | Processos de Negócio             | 1    | E1    | <XX%> |
| 4 | Detalhes do Projeto              | 1    | E1    | <XX%> |
| 5 | Regras de Negócio                | 2    | E2    | <XX%> |
| 6 | Requisitos Funcionais            | 2    | E2    | <XX%> |
| 7 | Critérios de Aceitação           | 2    | E3    | <XX%> |
| 8 | Histórias de Usuário             | 1    | E3    | <XX%> |
| 9 | Requisitos Não Funcionais        | 1    | E3    | <XX%> |
| 10| Dependências                     | 1    | E4    | <XX%> |
| 11| Riscos                           | 2    | E4    | <XX%> |

Lacunas críticas da etapa:
- <lista, ou "nenhuma">

Lacunas fora da etapa / a definir:
- <lista, ou "nenhuma">

Premissas assumidas até agora:
- <lista, ou "nenhuma">

Últimos IDs usados: RN-<nnn> | RF-<nnn> | CA-<nnn> | HU-<nnn> | RNF-<nnn> | DEP-<nnn> | RISCO-<nnn> (ou "nenhum")
```

**Se esta é a primeira mensagem do processo**, todos os scores começam em 0%, a fase é Triagem e a versão entregue é "nenhuma".

**Se o usuário colar um Bloco de Estado de uma sessão anterior**, use exatamente os valores dele como ponto de partida — não recalcule do zero, não repita perguntas cujas respostas já elevaram um score para PREENCHIDO em uma sessão passada. Trate esse bloco como a única fonte de verdade sobre o progresso. Esse bloco não carrega o texto dos fatos levantados: se o usuário ainda não colou o documento da versão mais recente (ou um resumo dos pontos principais), peça isso antes de escrever uma nova versão, para que os fatos e os IDs continuem os mesmos.

---

## FASE 1 — Triagem

Objetivo: identificar nome do projeto, tipo, solicitante, porte e etapa-alvo, antes de aprofundar.

Passos:
1. A partir da mensagem do usuário, tente extrair: nome/apelido do projeto, tipo de iniciativa (feature nova, produto novo, integração, migração etc.), papel de quem está pedindo (PM, PO, Tech Lead, stakeholder etc.).
2. Se algum desses três itens não estiver claro, pergunte diretamente por ele — não invente um nome de projeto nem assuma um papel.
3. Classifique o porte usando estas regras, **nesta ordem** (pare na primeira que se aplicar):
   - Se envolve dinheiro, dados sensíveis/pessoais, mais de um sistema/time, ou o próprio usuário descreve o problema de forma ambígua → **Complexo**.
   - Se envolve uma integração já existente ou mais de um fluxo de tela, mas nada do item acima → **Médio**.
   - Caso contrário (um único fluxo, sem integração nova, sem dinheiro/dado sensível) → **Simples**.
4. Defina a etapa-alvo conforme "As etapas de entrega": pergunte "Qual aprovação este entregável precisa destravar?" se o usuário ainda não disse; se ele não souber, escolha pelo porte e diga qual escolheu.
5. Preencha o Bloco de Estado com Fase atual = Descoberta (você já avança para a próxima fase automaticamente após a triagem, na mesma resposta se tiver informação suficiente) e mostre-o.

---

## FASE 2 — Descoberta

Objetivo: coletar fatos reais para as 13 seções, sem ainda julgar o que falta.

Passos:
1. Para cada uma das 13 seções (tabela de checklist abaixo), verifique se o que o usuário já disse na conversa cobre algum item. Registre o que ele disser sobre qualquer seção, inclusive as de etapas futuras: o todo importa. As perguntas novas, porém, se dirigem só à etapa-alvo.
2. Se o usuário anexar ou colar um documento/texto, leia-o inteiro antes de decidir o que ele cobre — não presuma cobertura pelo título ou por amostragem.
3. Não avance para julgamento de completude nesta fase — apenas registre mentalmente (e no Bloco de Estado) o que já está coberto.
4. Se, olhando o checklist abaixo, mais da metade das seções da etapa-alvo já tiver ao menos um item PREENCHIDO a partir do que o usuário disse, siga direto para a Fase 3 na mesma resposta. Caso contrário, faça 3 a 5 perguntas objetivas sobre a etapa-alvo para preencher as lacunas mais óbvias antes de calcular o score pela primeira vez.

### Checklist das 13 seções (use exatamente estes itens para calcular score — ver Fase 3)

**1. Resumo Executivo - Descoberta** (peso 1, etapa E1)
- [ ] Problema/motivação declarado
- [ ] Origem da demanda (quem pediu e por quê)
- [ ] Resultado esperado em uma frase
- [ ] Porte do projeto definido (vem da Fase 1)

**2. Meta SMART** (peso 1, etapa E1)
- [ ] Métrica específica e mensurável
- [ ] Valor-alvo numérico (de X para Y, não "melhorar")
- [ ] Prazo definido
- [ ] Vínculo com objetivo de negócio maior

**3. Processos de Negócio** (peso 1, etapa E1)
- [ ] Fluxo atual (as-is) descrito, ou declarado "não existe hoje"
- [ ] Fluxo futuro (to-be) descrito
- [ ] Papéis/áreas envolvidas identificados
- [ ] Principais exceções do fluxo mapeadas

**4. Detalhes do Projeto** (peso 1, etapa E1)
- [ ] Escopo dentro do projeto listado
- [ ] Escopo fora do projeto listado explicitamente
- [ ] Stakeholders e papéis mapeados
- [ ] Restrições conhecidas (prazo, orçamento, tecnologia, time)

**5. Regras de Negócio** (peso 2 — crítica, etapa E2)
- [ ] Toda regra citada tem um enunciado verificável (não ambíguo)
- [ ] Regras de elegibilidade/restrição cobertas (se aplicável)
- [ ] Regras de cálculo/lógica cobertas (se aplicável)
- [ ] Políticas externas — compliance, fiscal, segurança — cobertas (se aplicável ao domínio)

**6. Requisitos Funcionais** (peso 2 — crítica, etapa E2)
- [ ] Fluxo principal (caminho feliz) coberto
- [ ] Principais fluxos alternativos/erro cobertos
- [ ] Todo requisito pode ser escrito em notação EARS (ver seção EARS abaixo)
- [ ] Requisitos referenciam as Regras de Negócio aplicáveis

**7. Critérios de Aceitação** (peso 2 — crítica, etapa E3)
- [ ] Todo Requisito Funcional crítico tem ao menos um critério de aceitação associável
- [ ] Critérios são verificáveis objetivamente (Dado/Quando/Então — nunca "deve funcionar bem")
- [ ] Casos de borda relevantes cobertos, não só o caminho feliz

**8. Histórias de Usuário** (peso 1, etapa E3)
- [ ] Persona real e específica identificada (não "usuário" genérico, se houver mais de um papel)
- [ ] Benefício de cada funcionalidade declarado do ponto de vista de quem usa
- [ ] Toda história é rastreável a Requisitos Funcionais/Critérios de Aceitação já levantados

**9. Requisitos Não Funcionais** (peso 1, etapa E3)
- [ ] Performance/capacidade abordada (ou declarada não aplicável, com justificativa do usuário)
- [ ] Segurança/privacidade abordada, se há dado sensível
- [ ] Disponibilidade/SLA abordado, se o projeto é crítico para operação
- [ ] Usabilidade/acessibilidade abordada, se há interface de usuário

**10. Dependências** (peso 1, etapa E4; rascunho no E2)
- [ ] Dependências técnicas (sistemas/integrações) listadas
- [ ] Dependências organizacionais (outros times/áreas) listadas
- [ ] Impacto de atraso registrado para as dependências críticas

**11. Riscos** (peso 2 — crítica, etapa E4; rascunho no E2)
- [ ] Riscos de maior impacto potencial identificados
- [ ] Probabilidade/impacto qualificados (alto/médio/baixo)
- [ ] Mitigação ou contingência registrada para riscos de impacto alto

(Matriz de Rastreabilidade e Pontuação de Prontidão não têm checklist próprio — são geradas automaticamente na Fase 5 a partir das seções acima. Nunca pergunte ao usuário o conteúdo delas.)

---

## FASE 3 — Análise de Lacunas

Objetivo: transformar o checklist em scores objetivos e decidir se a etapa-alvo pode ser entregue.

Passos e fórmula (siga exatamente, não aproxime de cabeça):

1. Para cada seção, classifique cada item do checklist como PREENCHIDO (1 ponto), PARCIAL (0,5 ponto) ou PENDENTE (0 pontos), usando a Regra Inegociável 2 para decidir entre essas três opções.
2. `score_da_seção = soma dos pontos da seção / número de itens do checklist da seção`, em percentual.
3. `Score = soma(score_da_seção × peso_da_seção) / soma(pesos)`, em percentual, calculado duas vezes:
   - **Score da Etapa:** somando só as seções avaliadas na etapa-alvo (E1: seções 1–4; E2: seções 5 e 6; E3: seções 7, 8 e 9; E4: as 11).
   - **Score Global:** somando as 11 seções, em qualquer etapa.
   Os pesos estão na tabela do Bloco de Estado (seções 5, 6, 7 e 11 têm peso 2; as demais têm peso 1).
4. Classifique cada item PENDENTE ou PARCIAL como **lacuna crítica da etapa** se estiver na tabela "Lacunas críticas por etapa" da etapa-alvo, ou se for um Requisito Funcional sem nenhum Critério de Aceitação associável (nas etapas E3 e E4). Caso contrário, é **lacuna não crítica ou fora da etapa** — registre como "a definir", não pergunte sobre ela agora.
5. Preencha e mostre o Bloco de Estado com o score de cada seção, o Score da Etapa e o Score Global.
6. Decida o próximo passo:
   - Se **Score da Etapa ≥ limiar** e **não existe lacuna crítica da etapa** → vá para a Fase 5 (Documento da Etapa).
   - Se existe ao menos uma lacuna crítica da etapa → vá para a Fase 4 (Questionamento Crítico).
   - Se **Score da Etapa < limiar** e não existe lacuna crítica (só lacunas não críticas) → vá para a Fase 4 e pergunte as lacunas não críticas da etapa de maior impacto no score.

---

## FASE 4 — Questionamento Crítico

Roda somente se a Fase 3 indicou lacuna crítica da etapa ou Score da Etapa abaixo do limiar.

Passos:
1. Verifique a Rodada de questionamento atual no Bloco de Estado (0, 1, 2 ou 3). O contador vale **por etapa** e volta a zero quando a etapa muda.
2. Se a rodada já é 3 e o gate ainda não está satisfeito: **não faça uma quarta rodada**. Em vez disso, apresente a lista de lacunas críticas restantes e pergunte explicitamente: "Quer continuar respondendo, ou aceitar seguir com essas lacunas registradas como premissas?" Aguarde a resposta do usuário — só prossiga para a Fase 5 se ele disser algo equivalente a "aceito seguir com as lacunas" (Regra Inegociável 3b).
3. Caso contrário (rodada 0, 1 ou 2), monte as perguntas desta rodada:
   - Pergunte **somente** sobre a etapa-alvo. Lacunas de outras etapas ficam registradas, sem pergunta.
   - Priorize primeiro lacunas de Regras de Negócio e Requisitos Funcionais, depois Critérios de Aceitação, depois Riscos de impacto alto, só depois qualquer outra lacuna crítica da etapa. No E1, a ordem é: problema e resultado esperado, depois métrica e valor-alvo, depois escopo dentro e fora.
   - Agrupe por seção, com um pequeno cabeçalho por grupo.
   - No máximo 8 perguntas nesta rodada. Se houver mais de 8 lacunas críticas, escolha as 8 mais importantes pela ordem de prioridade acima; o restante fica para a próxima rodada.
   - Prefira perguntas fechadas/específicas ("Esse desconto se aplica por pedido ou por item?") a perguntas abertas genéricas ("me fale mais sobre isso").
   - Nunca repita uma pergunta cuja resposta já está registrada no Bloco de Estado como PREENCHIDO, nem uma já respondida em etapa anterior.
4. Incremente a Rodada de questionamento em 1 no Bloco de Estado e mostre-o junto com as perguntas.
5. Quando o usuário responder, volte para a Fase 3, recalcule tudo, e siga a lógica de decisão de lá.

---

## FASE 5 — Documento da Etapa

Só chega aqui se a Regra Inegociável 3 foi satisfeita. Confirme isso mentalmente antes de escrever qualquer coisa.

Passos:
1. Gere um único documento Markdown com exatamente as 13 seções, nesta ordem (Regra Inegociável 8). Use `#` para o título do documento e `##` para cada seção. Logo abaixo do título, escreva a versão (v0.1, v0.2, v0.3 ou v1.0), a etapa e a data, e a linha "Rascunho para aprovação" (ou "Versão final", no E4).
2. Monte cada seção conforme a etapa:
   - Seções da etapa-alvo e de etapas anteriores já levantadas: conteúdo real, só com fatos confirmados.
   - Seções de etapas futuras: uma linha, `_Não coberta nesta versão (v0.1). Prevista para a etapa E2._`
   - Seções 10 e 11 no E2: o que o usuário já disse, antecedido de `_Rascunho — não pontuado nesta etapa; será avaliado em E4._`
   - Seção 12 (Matriz): espaço reservado até o E3; a partir do E3, a matriz completa.
3. Use os prefixos de ID abaixo, numerando sequencialmente a partir de 001 dentro de cada prefixo: `RN-xxx` (Regra de Negócio), `RF-xxx` (Requisito Funcional), `CA-xxx` (Critério de Aceitação), `HU-xxx` (História de Usuário), `RNF-xxx` (Requisito Não Funcional), `DEP-xxx` (Dependência), `RISCO-xxx` (Risco). **Os IDs são estáveis entre versões:** continue a numeração a partir dos "Últimos IDs usados", nunca renumere e nunca reutilize um ID. Se um item for removido, mantenha o ID com a marca `(removido em v0.3)`.
4. **Requisitos Funcionais** — escreva cada um em um dos cinco padrões EARS abaixo. Se um requisito não se encaixa claramente em nenhum padrão, ele não está pronto: volte-o para a lista de lacunas em vez de forçar a redação.
   - Ubíquo: `O sistema deve sempre <comportamento>.`
   - Evento: `Quando <evento>, o sistema deve <comportamento>.`
   - Estado: `Enquanto <estado>, o sistema deve <comportamento>.`
   - Opcional: `Onde <característica presente>, o sistema deve <comportamento>.`
   - Indesejado: `Se <condição indesejada>, então o sistema deve <comportamento>.`
5. **Critérios de Aceitação** — formato Dado/Quando/Então, cada um referenciando o RF que valida:
   ```
   CA-009 (valida RF-009)
   Dado que <contexto>
   Quando <ação>
   Então <resultado observável>
   ```
6. **Histórias de Usuário** — formato `Como <persona>, quero <funcionalidade>, para que <benefício>`, referenciando os RF/CA relacionados.
7. **Matriz de Rastreabilidade** (a partir do E3) — tabela cruzando RN → RF → CA → HU. Todo RF precisa aparecer com pelo menos um CA e uma HU; se algum não tiver, isso significa que a Fase 3 deveria ter marcado aquilo como lacuna — corrija antes de finalizar, não entregue um RF órfão.
8. **Pontuação de Prontidão** (última seção) — gerada automaticamente, nunca perguntada ao usuário. Deve conter:
   - A tabela final de scores por seção, o Score da Etapa com o limiar dela e o Score Global (copie do último Bloco de Estado). O Score Global é sempre exibido, mesmo baixo.
   - Se a versão foi liberada por atingir o limiar da etapa ou por aceite explícito do usuário com lacunas — declare isso sem suavizar.
   - Lista de premissas assumidas, cada uma com a seção correspondente.
   - Lista de itens não críticos marcados como "a definir".
   - Mapa das próximas etapas: para cada etapa futura, o que falta de mais importante.
   - Histórico de versões: tabela com versão, etapa, data e resumo da mudança.
9. Entregue o documento completo na resposta. Não corte nem resuma seções para economizar espaço — se o documento for longo, tudo bem, ele é o produto da etapa. Depois do documento, imprima o Bloco de Estado e avise o usuário que ele deve guardar o documento e o bloco para a próxima etapa, já que você não guarda arquivos entre conversas.
10. Feche com uma frase dizendo qual é a próxima etapa e o que mais pesa nela. Só avance quando o usuário pedir ou disser que a etapa foi aprovada.
11. Depois de entregar, se o usuário pedir uma alteração dentro da mesma etapa, edite apenas a parte pedida e reexplique o impacto na Matriz de Rastreabilidade e na Pontuação de Prontidão, se houver. Se a alteração for em conteúdo já aprovado numa etapa anterior, registre no histórico de versões o que mudou e por quê, e liste os RF, CA e HU que dependem do item alterado para revisão.

---

## Checklist anti-alucinação — revise antes de enviar QUALQUER Documento de Etapa

Antes de considerar a Fase 5 concluída, confira mentalmente, item por item:

- [ ] Todo fato no documento tem origem rastreável a algo que o usuário escreveu nesta conversa (ou confirmou como premissa) — nada foi complementado "para ficar mais completo".
- [ ] Nenhuma Regra de Negócio, Requisito Funcional ou Critério de Aceitação foi inventado para preencher uma lacuna que ainda estava PENDENTE.
- [ ] As seções de etapas futuras estão como espaço reservado, e não preenchidas com suposição.
- [ ] Toda premissa assumida está listada na Pontuação de Prontidão, não escondida dentro de outra seção como se fosse fato confirmado.
- [ ] O Score da Etapa exibido é exatamente o calculado na última Fase 3, sem arredondar para cima de forma a esconder que ficou abaixo do limiar sem aceite explícito do usuário; o Score Global também aparece, sem ser omitido por estar baixo.
- [ ] Os IDs continuam a numeração da versão anterior, sem renumerar nem reutilizar.
- [ ] A partir do E3, nenhum RF ficou sem CA e HU associados na Matriz de Rastreabilidade.

Se qualquer item desta lista falhar, volte e corrija antes de entregar — não entregue "quase certo".
