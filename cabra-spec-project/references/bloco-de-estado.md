# Bloco de Estado

O Bloco de Estado é o estado portátil do projeto: um resumo em texto que o usuário pode copiar e colar numa conversa nova para retomar de onde parou. Use-o quando o ambiente não guarda arquivos entre sessões (ver "Onde guardar o estado" em `SKILL.md`). Em ambiente com arquivos persistentes, o mesmo conteúdo vive em `.descoberta/<slug>/descoberta.md` e `lacunas.md`, e o bloco é dispensável.

Avise o usuário **uma vez**, em uma frase, que ele pode copiar o bloco para continuar em outra conversa. Não repita o aviso.

## Quando imprimir

- **Bloco completo** (com "Fatos levantados"): sempre que o estado tiver mudado de forma relevante — fatos novos, scores recalculados, etapa entregue, decisão do usuário.
- **Bloco compacto** (sem "Fatos levantados"): em respostas que não alteram o estado, como tirar uma dúvida sobre o framework.
- Quando entregar o documento de uma etapa, imprima o bloco compacto depois dele; os fatos já estão no documento.

## Formato

Preencha este template, substituindo os valores entre `< >`. Mantenha a ordem e os nomes dos campos; assim o bloco pode ser lido de volta sem ambiguidade.

```
### ESTADO DO PROJETO — <nome do projeto> (<slug>)
Solicitante: <papel> | Porte: <Simples | Médio | Complexo>
Etapa-alvo: <E1 | E2 | E3 | E4> | Fase atual: <Triagem | Descoberta | Análise de Lacunas | Questionamento Crítico | Documento da Etapa>
Rodada de questionamento (nesta etapa): <0 a 3>
Versão entregue mais recente: <nenhuma | v0.1 | v0.2 | v0.3 | v1.0>
Score da etapa: <XX%> (limiar <YY%>) | Score global: <ZZ%>

| # | Seção                           | Peso | Etapa | Score |
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
- <seção — item, ou "nenhuma">

Premissas assumidas:
- <lista, ou "nenhuma">

Últimos IDs usados: RN-<nnn> | RF-<nnn> | CA-<nnn> | HU-<nnn> | RNF-<nnn> | DEP-<nnn> | RISCO-<nnn>

Fatos levantados (só no bloco completo):
S1 — <fato> [origem: usuário | documento X | conector Y | web]
S2 — <fato> [origem]
...
```

Notas sobre o preenchimento:

- **Fatos levantados** carregam só o que foi dito ou confirmado, uma linha por fato, citando a origem. Se uma regra, requisito ou critério já tiver ID, use o ID no lugar de reescrever o texto inteiro (`RN-003 — desconto não acumula com cupom`). Sem fatos, quem retoma o projeto não tem como escrever o documento.
- **Últimos IDs usados** garantem que os IDs continuem estáveis entre versões e sessões (regra em `etapas.md`). Se nenhum ID foi criado ainda, escreva `nenhum`.
- Se o estado já gerou um documento de etapa, sugira ao usuário colar também a versão mais recente do documento ao retomar; ele é a fonte mais fiel do que foi aprovado.
- Na primeira mensagem do processo, todos os scores começam em 0%, a fase é Triagem e a versão entregue é `nenhuma`.

## Retomando a partir de um bloco

Quando o usuário colar um Bloco de Estado de uma sessão anterior:

1. Trate o bloco como o estado salvo: use os scores, fatos e IDs dele como ponto de partida, sem recalcular do zero e sem repetir perguntas já respondidas.
2. Se o que o usuário disser agora contradizer o bloco, o que ele diz agora prevalece — atualize o estado e siga.
3. Se o bloco não trouxer "Fatos levantados" (bloco compacto) e não houver documento colado, avise que os fatos das seções não estão disponíveis e peça o documento da última versão ou um resumo dos pontos principais antes de avançar.
4. Continue da fase indicada em "Fase atual".
