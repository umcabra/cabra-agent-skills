# As 13 seções — definição, perguntas-guia e checklist de completude

Para cada seção: o que ela precisa conter, as perguntas-guia usadas na Descoberta (Fase 2) para saber se está coberta, e o checklist usado na Análise de Lacunas (Fase 3) para calcular o score da seção. Um item do checklist conta como preenchido só se houver um fato concreto por trás — não uma frase vaga.

IDs usados nas seções que geram itens rastreáveis: `RN-xxx` (Regra de Negócio), `RF-xxx` (Requisito Funcional), `CA-xxx` (Critério de Aceitação), `HU-xxx` (História de Usuário), `RNF-xxx` (Requisito Não Funcional), `DEP-xxx` (Dependência), `RISCO-xxx` (Risco). Numere sequencialmente a partir de 001 dentro de cada prefixo, por projeto.

---

## 1. Resumo Executivo - Descoberta

O que é: uma síntese de meia página do que o projeto é, por que existe agora, e o que foi levantado na descoberta — escrita por último, depois que todo o resto estiver definido, mas listada primeiro no documento.

Perguntas-guia: Qual problema motivou este projeto? Por que agora? Quem pediu? Qual é o resultado esperado em uma frase?

Checklist:
- [ ] Problema/motivação declarado
- [ ] Origem da demanda (quem pediu, e por quê)
- [ ] Resultado esperado em uma frase
- [ ] Porte do projeto (Simples/Médio/Complexo) e principais fontes de descoberta usadas

## 2. Meta SMART

O que é: o objetivo do projeto formatado como Specific, Measurable, Achievable, Relevant, Time-bound.

Perguntas-guia: Qual métrica prova que o projeto funcionou? Qual é o valor-alvo? Até quando? Isso é realista dado o time/orçamento disponível? Por que essa meta importa para o negócio agora?

Checklist:
- [ ] Métrica específica e mensurável definida
- [ ] Valor-alvo numérico (não "melhorar", mas "de X para Y")
- [ ] Prazo definido
- [ ] Vínculo explícito com um objetivo de negócio maior

## 3. Processos de Negócio

O que é: o(s) fluxo(s) de negócio, atual (as-is) e futuro (to-be), que o projeto afeta.

Perguntas-guia: Como esse processo funciona hoje, passo a passo? Quem participa de cada etapa (papéis/áreas)? O que muda com o projeto? Existe um fluxo alternativo ou exceção relevante?

Checklist:
- [ ] Fluxo as-is descrito (ou declarado como "não existe hoje", se for processo novo)
- [ ] Fluxo to-be descrito
- [ ] Papéis/áreas envolvidas identificados
- [ ] Principais exceções ou desvios do fluxo mapeados

## 4. Detalhes do Projeto

O que é: ficha técnica do projeto — escopo, fora de escopo, stakeholders, prazos macro, restrições.

Perguntas-guia: O que está explicitamente fora de escopo? Quem são os stakeholders e qual o papel de cada um (aprovador, consultado, informado)? Existe uma data-limite real (regulatória, contratual, sazonal)? Há restrições de orçamento, time ou tecnologia já dadas?

Checklist:
- [ ] Escopo dentro do projeto listado
- [ ] Escopo fora do projeto listado explicitamente (não deixar implícito)
- [ ] Stakeholders e papéis mapeados
- [ ] Restrições conhecidas (prazo, orçamento, tecnologia, time) registradas

## 5. Regras de Negócio

O que é: as regras que restringem ou determinam o comportamento do sistema/processo, independentes de uma tela ou fluxo específico — coisas como limites, elegibilidade, cálculos, políticas. Cada regra vira um item `RN-xxx`.

Perguntas-guia: Existem limites de valor, quantidade ou tentativas? Existe critério de elegibilidade (quem pode/não pode)? Existe uma fórmula ou lógica de cálculo definida? Existe uma política (fiscal, de segurança, contratual) que o sistema precisa respeitar?

Checklist (por regra identificada, e no agregado da seção):
- [ ] Toda regra tem um ID `RN-xxx` e um enunciado verificável (não ambíguo)
- [ ] Regras de elegibilidade/restrição cobertas
- [ ] Regras de cálculo/lógica cobertas (se aplicável ao domínio)
- [ ] Políticas externas (compliance, fiscal, segurança) cobertas, se relevantes ao domínio

Esta é uma **seção crítica** — ver `pontuacao.md`.

## 6. Requisitos Funcionais

O que é: o que o sistema deve fazer, em notação EARS (ver `notacao-ears.md`). Cada requisito vira `RF-xxx` e deve referenciar as `RN-xxx` que o restringem, quando aplicável.

Perguntas-guia: Quais ações o usuário/sistema realiza? O que dispara cada ação? O que o sistema deve fazer em cada evento e em cada condição de erro?

Checklist:
- [ ] Todo RF está em notação EARS e tem um ID
- [ ] Fluxo principal (caminho feliz) coberto
- [ ] Principais fluxos alternativos/erro cobertos
- [ ] RFs referenciam as RN aplicáveis

Esta é uma **seção crítica**.

## 7. Critérios de Aceitação

O que é: condições binárias e verificáveis que provam que um RF foi implementado corretamente. Cada critério vira `CA-xxx` e referencia o(s) `RF-xxx` que valida.

Perguntas-guia: Como alguém, olhando o sistema pronto, saberia que este requisito funciona? O que é sucesso e o que é falha, de forma objetiva?

Checklist:
- [ ] Todo RF crítico tem pelo menos um CA associado
- [ ] Todo CA é verificável objetivamente (dado/quando/então — sem "deve funcionar bem")
- [ ] CAs cobrem também casos de borda relevantes (não só o caminho feliz)

Esta é uma **seção crítica**.

## 8. Histórias de Usuário

O que é: "Como [persona], quero [funcionalidade], para que [benefício]", cada uma como `HU-xxx`, ligada aos `RF-xxx`/`CA-xxx` que ela cobre — pronta para virar item de Product Backlog no Scrum.

Perguntas-guia: Quem são as personas/papéis reais que usam isso? Qual o benefício de cada funcionalidade do ponto de vista de quem usa, não do sistema?

Checklist:
- [ ] Toda HU segue o formato Como/Quero/Para que
- [ ] Toda HU referencia os RF/CA relacionados
- [ ] Personas usadas são reais/específicas (não "usuário" genérico, quando o projeto tem mais de um papel)

## 9. Requisitos Não Funcionais

O que é: performance, segurança, disponibilidade, escalabilidade, usabilidade, conformidade — tudo que não é "o que o sistema faz" mas "como ele deve se comportar". Cada um vira `RNF-xxx`.

Perguntas-guia: Existe expectativa de tempo de resposta, volume de usuários simultâneos ou pico de uso? Há exigência de disponibilidade (SLA)? Há dado sensível/pessoal envolvido (LGPD)? Há exigência de acessibilidade ou idiomas?

Checklist:
- [ ] Performance/capacidade abordada (ou declarada como não aplicável, com justificativa)
- [ ] Segurança/privacidade abordada quando há dado sensível
- [ ] Disponibilidade/SLA abordado quando o projeto é crítico para operação
- [ ] Usabilidade/acessibilidade abordada quando há interface de usuário

## 10. Dependências

O que é: sistemas, times, integrações, decisões externas ou entregas de terceiros dos quais o projeto depende para funcionar. Cada uma vira `DEP-xxx`.

Perguntas-guia: Este projeto depende de outro sistema/API já existente? Depende de outro time entregar algo antes? Depende de uma decisão de negócio ainda não tomada? Depende de fornecedor externo?

Checklist:
- [ ] Dependências técnicas (sistemas/integrações) listadas
- [ ] Dependências organizacionais (outros times/áreas) listadas
- [ ] Para cada dependência crítica, o impacto de atraso está registrado

## 11. Riscos

O que é: o que pode dar errado, sua probabilidade/impacto e o plano de mitigação. Cada um vira `RISCO-xxx`.

Perguntas-guia: O que, se acontecer, compromete o prazo ou a meta SMART? Existe risco regulatório, de segurança, de adoção pelo usuário, técnico? Qual a mitigação ou plano de contingência para os riscos mais relevantes?

Checklist:
- [ ] Ao menos os riscos de maior impacto potencial identificados
- [ ] Probabilidade/impacto qualificados (mesmo que de forma simples: alto/médio/baixo)
- [ ] Mitigação ou contingência registrada para os riscos de impacto alto

Esta é uma **seção crítica**.

## 12. Matriz de Rastreabilidade

O que é: uma tabela que cruza `RN` → `RF` → `CA` → `HU`, mostrando que nada foi especificado sem sustentação e nada foi implementado sem exigência. Não é levantada por perguntas — é **derivada** das seções 5 a 8 depois que elas existem.

Checklist:
- [ ] Todo RF tem RN de origem (quando aplicável) e ao menos um CA
- [ ] Todo CA está vinculado a um RF
- [ ] Toda HU está vinculada a pelo menos um RF/CA
- [ ] Nenhum ID órfão (criado mas nunca referenciado, ou referenciado mas nunca criado)

## 13. Pontuação de Prontidão

O que é: a seção que expõe o resultado do processo de descoberta ao leitor — não é conteúdo de negócio, é a "nota fiscal" da qualidade do documento. Ver `pontuacao.md` para a fórmula. Contém: score por seção, score global, premissas assumidas (se a Fase 4 foi encerrada sem 100% de resolução) e itens explicitamente marcados como "a definir".

Esta seção é sempre gerada automaticamente pela skill na Fase 5 — nunca pergunte ao usuário o que colocar nela.
