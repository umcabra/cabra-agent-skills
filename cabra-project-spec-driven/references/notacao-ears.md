# Notação EARS (em português) para Requisitos Funcionais e Critérios de Aceitação

EARS (Easy Approach to Requirements Syntax) força cada requisito funcional a ser verificável, sem ambiguidade sobre quando ele se aplica. Todo `RF-xxx` usa um dos cinco padrões abaixo. Se não encaixar, ainda está vago: volte ao questionamento em vez de forçar a redação.

Critério de aceitação não usa EARS. `CA-xxx` usa Dado/Quando/Então, amarrado a um RF, como na seção seguinte.

## Os cinco padrões

**1. Ubíquo** (sempre verdadeiro, sem gatilho)
`O sistema deve sempre <comportamento>.`
Exemplo: `RF-004 — O sistema deve sempre registrar o usuário responsável por cada alteração de status do pedido.`

**2. Orientado a evento** (dispara quando algo acontece)
`Quando <evento>, o sistema deve <comportamento>.`
Exemplo: `RF-012 — Quando o pagamento for confirmado pela adquirente, o sistema deve liberar o pedido para separação.`

**3. Orientado a estado** (válido enquanto uma condição persiste)
`Enquanto <estado>, o sistema deve <comportamento>.`
Exemplo: `RF-018 — Enquanto o cadastro estiver com status "em análise", o sistema deve bloquear novas transações do usuário.`

**4. Opcional/característica** (só se aquela feature estiver presente)
`Onde <característica presente>, o sistema deve <comportamento>.`
Exemplo: `RF-021 — Onde o cliente tiver plano corporativo ativo, o sistema deve aplicar o desconto de volume automaticamente.`

**5. Indesejado** (tratamento de erro/exceção)
`Se <condição indesejada>, então o sistema deve <comportamento>.`
Exemplo: `RF-009 — Se a validação de CPF falhar, então o sistema deve exibir a mensagem de erro específica e impedir o avanço para a próxima etapa.`

## Critérios de Aceitação: Dado/Quando/Então

Critérios de Aceitação usam Gherkin simplificado, sempre amarrado a um RF:

```
CA-009 (valida RF-009)
Dado que o usuário está na etapa de cadastro
Quando ele informa um CPF inválido
Então o sistema exibe "CPF inválido, verifique e tente novamente"
E o botão "Avançar" permanece desabilitado
```

## Erros comuns a evitar

- **Vago demais para ser verificável**: "O sistema deve ser rápido" → não é RF nem CA; é sintoma de que falta uma RNF com número (ver seção 9).
- **Dois requisitos disfarçados de um**: "Quando o pagamento for confirmado, o sistema deve liberar o pedido e enviar e-mail e atualizar o estoque" → quebre em três RFs, cada um rastreável e testável separadamente.
- **Critério que testa implementação, não comportamento**: "O sistema deve chamar a função `liberarPedido()`" → isso não é um CA, é um detalhe de código. O CA correto é sobre o resultado observável: pedido muda de status, cliente recebe confirmação, etc.
- **Requisito sem gatilho claro**: se você não consegue dizer em qual dos cinco padrões ele se encaixa, ainda não está pronto — volte para a Fase de Questionamento em vez de forçar um encaixe.
