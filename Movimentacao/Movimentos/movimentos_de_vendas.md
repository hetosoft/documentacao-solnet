# 📄 Movimentos de Vendas - Sol.NET

## 🎯 Visão Geral

`Movimentos de Vendas` é o ponto operacional da **saída comercial** do Sol.NET: vendas balcão, vendas no PDV (frente de loja), orçamentos, pedidos de venda, ordens de serviço com faturamento, faturamentos parciais, transferências de saída para outras lojas. Toda mercadoria que **sai** com nota fiscal de venda (ou documento equivalente) é lançada aqui.

A tela compartilha o mesmo formulário operacional usado em `Movimentos de Compras` (`201`) e `Outros Movimentos` (`203`), mas **filtra os Tipos de Movimento disponíveis** apenas para aqueles com **Comportamento = Saída** no [Cadastro de Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) (`37`).

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Movimentos de Vendas |
| **Código (`F1`)** | `202` |

Abra a pesquisa universal (`F1`) e digite `202` ou parte do nome **Movimentos de Vendas**.

---

## 🧭 Particularidades do modo Vendas

- **CFOPs de Saída** (faixa `5xxx` para operações dentro do estado, `6xxx` para interestaduais, `7xxx` para exportação). CFOP fora da faixa é bloqueado: *"CFOP não é de saída!"*.
- **Transações de Estoque que subtraem Físico/Disponível** — a venda consome saldo. Tipos cuja Transação não subtrai disparam erro de configuração no momento de finalizar.
- **Emissão Própria** — a empresa emite o documento; `Série` e `Número do Documento` vêm da Série fiscal do Sol.NET, em sequência.
- **`Atualizar Custo Automático` proibido** — vendas **não** atualizam custo. Marcar essa flag em `37` para um Tipo de Saída é rejeitado: *"Atualizar Custo Automático, Somente para Compras/Outros!"*.
- **PDV** — Tipos marcados como PDV em `Outras Operações → Sistema` ativam a sub-aba `PDV` no formulário, otimizada para venda balcão rápida (teclado, código de barras, finalização em poucos passos).
- **Devolução de Venda** — quando um cliente devolve mercadoria, o Tipo `DEVOLUÇÃO DE VENDA` (configurado em `37` com `Devolução = Sim`) faz o movimento neste mesmo modo `202`, gerando Crédito de Pessoa quando configurado.
- **Vencimento** — Tipos de venda costumam gerar contas a receber. As parcelas são derivadas da `Condição de Pagamento` do Cabeçalho e ficam visíveis/editáveis na sub-aba `Vencimento`.
- **Caixa aberto** — para finalizar uma venda em modo PDV (ou em qualquer Tipo configurado para exigir Caixa), o Caixa do usuário precisa estar **aberto**; sem isso o sistema bloqueia: *"Caixa Aberto. Fechamento Nº: ( ... )"*.
- **Cashback** — Tipos PDV podem disparar geração/uso de [Cashback](../documentacao_regras_cashback.md) automaticamente ao finalizar, conforme as Regras de Cashback ativas para a empresa/cliente.

---

## 💡 Exemplos práticos

### Venda balcão à vista

1. Pesquisa `F1` → `202` → **Novo**.
2. **Cabeçalho**: `Tipo` = `VENDA BALCÃO`, `Pessoa` = cliente (ou genérico/consumidor final), `Condição de Pagamento` = `À VISTA`, `Portador` = `Caixa`.
3. **Itens**: bipe ou digite cada produto; ajuste quantidade e desconto.
4. **Outros Valores**: se necessário, lance desconto no total.
5. `F6` (Finalizar) → estoque baixa, conta a receber é criada e imediatamente quitada (porque é à vista), cupom/NFC-e é emitido.

### Venda no PDV com NFC-e

1. Pesquisa `F1` → `202` → **Novo** com Tipo PDV.
2. A sub-aba `PDV` toma o foco — operação otimizada para teclado.
3. Lance itens, escolha forma(s) de pagamento, conclua.
4. NFC-e é emitida automaticamente; cliente recebe cupom.

### Orçamento → Pedido → Venda

1. Lance um Tipo `ORÇAMENTO` em `202` — ele não baixa estoque nem gera financeiro (configurado assim em `37`).
2. Quando o cliente aprovar, `F7` (Mudar) → mudança automática para `PEDIDO` (conforme regra de `Tipos de Movimento → aba Mudar`).
3. Quando faturar, `F7` novamente → `VENDA`. Aí estoque desce e financeiro é gerado.

---

## 🔗 Documentação completa

O detalhamento do formulário — sub-abas, fluxos, atalhos, validações, exemplos comuns, FAQ — está em [Movimentos](documentacao_movimentos.md). Esta página descreve apenas o que diferencia o modo `Vendas`.

Outras referências úteis:

- [Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) (`37`) — onde os Tipos de Saída são configurados.
- [Tabela de Preço](../documentacao_tabela_de_preco.md) (`27`) — origem do preço aplicado a cada item.
- [Regras Cashback](../documentacao_regras_cashback.md) (`124`) — regras que disparam cashback em vendas PDV.
- [Histórico de Movimentações](../documentacao_historico_de_movimentacoes.md) (`205`) — trilha de auditoria.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Operadores de caixa e PDV / Vendedores / Retaguarda comercial / Suporte
