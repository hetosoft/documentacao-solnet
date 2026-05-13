# 📄 Movimentos de Vendas - Sol.NET

## 🎯 Visão Geral

`Movimentos de Vendas` concentra os Tipos de Movimento **acessados por vendedores** na retaguarda: venda balcão, orçamentos, pedidos de venda, ordens de serviço com faturamento, faturamentos parciais. É o conjunto de operações que um vendedor encontra no dia-a-dia para registrar uma saída comercial com cliente.

> ℹ️ **O que NÃO fica aqui:** devoluções de venda e transferências entre filiais — embora envolvam saída de mercadoria — **não** são fluxos de vendedor. Elas ficam em [Outros Movimentos](outros_movimentos.md) (`203`). A regra simples: se o Tipo de Movimento é tipicamente operado pela retaguarda/almoxarifado e não por um vendedor, ele vai para `203`.

> ℹ️ **PDV é separado.** Vendas em frente de caixa (cupom, NFC-e, comanda) acontecem em uma aplicação à parte, o **PDV**, que será documentada em outra seção. Tipos de Movimento marcados como `PDV` em [Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) **não aparecem** no combo `Tipo` desta tela — são exclusivos da aplicação PDV. Movimentos lançados no PDV ficam visíveis aqui apenas em modo de **consulta/edição complementar**.

A tela compartilha o mesmo formulário operacional usado em `Movimentos de Compras` (`201`) e `Outros Movimentos` (`203`), mas **filtra os Tipos de Movimento disponíveis** para aqueles configurados como vendas de vendedor em [Cadastro de Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) (`37`). Comportamento `Saída` é necessário mas não suficiente — outras flags (especialmente a exclusividade PDV) também filtram.

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
- **Financeiro** — Tipos de venda costumam gerar contas a receber. As parcelas são derivadas da `Condição de Pagamento` do Cabeçalho e ficam visíveis/editáveis na sub-aba `Financeiro → Parcelas`. (A aba `Vencimento`, à parte, é controle de **lote/data de validade dos produtos** — não de parcelas.)
- **Caixa aberto** — Tipos configurados para exigir Caixa só finalizam se o Caixa do usuário estiver **aberto**; sem isso o sistema bloqueia: *"Caixa Aberto. Fechamento Nº: ( ... )"*.
- **Vendas vindas do PDV** — vendas que se originaram no PDV (aplicação à parte) aparecem nas listas desta tela e podem ser consultadas/auditadas aqui. Filtros específicos estão na sub-aba `Pesquisa PDV` da área de Consulta. Cashback aplicado/gerado nessas vendas fica visível nas sub-abas `Crédito Pessoa - Usado` / `Crédito Pessoa - Gerado`.

---

## 💡 Exemplos práticos

### Venda balcão à vista

1. Pesquisa `F1` → `202` → **Novo**.
2. **Cabeçalho**: `Tipo` = `VENDA BALCÃO`, `Pessoa` = cliente (ou genérico/consumidor final), `Condição de Pagamento` = `À VISTA`, `Portador` = `Caixa`.
3. **Itens**: bipe ou digite cada produto; ajuste quantidade e desconto.
4. **Descontos/Outras Despesas**: se necessário, lance desconto no total.
5. `F6` (Finalizar) → estoque baixa, conta a receber é criada e imediatamente quitada (porque é à vista), NF-e/NFS-e é emitida conforme o Tipo.

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
- [Regras Cashback](../documentacao_regras_cashback.md) (`124`) — regras de cashback (uso/geração) configuradas por Tipo; movimentos do PDV chegam aqui com o cashback já aplicado.
- [Histórico de Movimentações](../documentacao_historico_de_movimentacoes.md) (`205`) — trilha de auditoria.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Vendedores de balcão / Retaguarda comercial / Suporte
