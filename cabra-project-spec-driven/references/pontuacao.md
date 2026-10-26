# Pontuação de Completude e de Prontidão

A mesma fórmula aparece duas vezes. A **Pontuação de Completude** é calculada na Fase 3 e recalculada a cada volta da Fase 4. A **Pontuação de Prontidão** é esse valor congelado na seção 13 do documento. Recalcule a partir do checklist. Não reaproveite um percentual antigo, nem um número que o usuário tenha colado.

## Como calcular o score de uma seção

Use o checklist das seções 1 a 11 em `secoes.md`. As seções 12 e 13 não entram na conta.

```
score_da_seção = (itens PREENCHIDOS + 0,5 × itens PARCIAIS) / total de itens do checklist
```

- **PREENCHIDO** (1): frase concreta do usuário, de um documento que ele forneceu, ou "não há" / "não se aplica" explícito quando o porte em `secoes.md` permitir.
- **PARCIAL** (0,5): existe informação, mas é vaga, não verificável, ou é suposição ainda não confirmada. "Acho que sim" e "não sei" ficam aqui, no máximo.
- **PENDENTE** (0): não há fato. Em dúvida, classifique para baixo.

Pesquisa web e conector não preenchem meta numérica, regra, requisito, critério ou risco. Esse achado fica como contexto externo nas notas até o usuário confirmar.

## Pesos

Seções de peso 2 sustentam a confiabilidade do documento. As demais pesam 1.

| Peso 2 | Peso 1 |
| --- | --- |
| Regras de Negócio | Resumo Executivo - Descoberta |
| Requisitos Funcionais | Meta SMART |
| Critérios de Aceitação | Processos de Negócio |
| Riscos | Detalhes do Projeto |
| | Histórias de Usuário |
| | Requisitos Não Funcionais |
| | Dependências |

```
Score Global = Σ(score_da_seção × peso_da_seção) / 15
```

A soma dos pesos é 15 (4 × 2 + 7 × 1). Expresse em percentual, sem arredondar para cima para mudar uma decisão.

## O que é lacuna crítica

Lacuna crítica é item PENDENTE ou PARCIAL em seção de peso 2, ou qualquer RF sem CA associável.

O resto é lacuna não crítica: registre como "a definir" e não pergunte na mesma rodada das críticas.

## Portão de liberação

O Score Global não abre nem fecha o documento sozinho. A referência de 80% é informativa: aparece na Pontuação de Prontidão para o leitor ver o quanto das seções de peso 1 ainda está fino.

1. Existe lacuna crítica e o usuário ainda não aceitou seguir com ela: Fase 4, qualquer que seja o percentual.
2. Não existe lacuna crítica: Fase 5, mesmo abaixo de 80%. As não críticas saem como "a definir".
3. A rodada de questionamento já está em 3 e ainda há lacuna crítica: não faça a quarta leva por conta própria. Mostre a lista e só avance se o usuário disser "aceito seguir com as lacunas" ou um equivalente inequívoco, depois de ver essa lista.
4. Se ele pedir o documento com lacuna crítica em aberto, mostre score e lista e pergunte se continua respondendo ou aceita as lacunas. Sem esse aceite, não gere.

A primeira leva de perguntas é a rodada 1. Ao apresentar cada leva, some 1. Três levas no máximo, salvo se ele pedir explicitamente para continuar; essa leva extra não se repete sozinha. Se a lacuna permanecer, exija o aceite de novo.

## Exemplo numérico

Não use estes números num projeto real. Servem para a conta não ser feita de cabeça.

**Ainda bloqueado, mesmo acima de 80%.** As sete seções de peso 1 estão em 100% (contribuição 7). Cada seção de peso 2 está com score 2/3 (contribuição 4 × 2/3 × 2 = 16/3). Total: 7 + 5,333 = 12,333. Global: 12,333 / 15 = **82%**. Há item pendente ou parcial em seção de peso 2. Não libere.

**Liberado abaixo de 80%.** As quatro seções de peso 2 estão em 100% (contribuição 8) e não há RF sem CA. As sete de peso 1 estão em 0% (contribuição 0). Global: 8 / 15 = **53%**. Não há lacuna crítica. Libere e liste as de peso 1 como "a definir".

## O que vai na seção 13

- Tabela com peso e score das seções 1 a 11, mais o Score Global, copiados do último cálculo.
- Se liberou sem lacuna crítica ou por aceite explícito. Diga isso sem suavizar. Se o global ficou abaixo de 80%, diga também.
- Premissas assumidas, cada uma com a seção e o motivo de não ter sido confirmada.
- Itens "a definir" que não bloqueiam.

Nunca omita um score baixo, nem uma lacuna crítica, para o documento parecer mais pronto.
