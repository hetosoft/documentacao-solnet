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

### Orçamento → Pedido → NFC-e (cupom fiscal)

Cenário comum em loja de balcão. **Não é um comportamento automático da tela `202`** — todas as etapas dependem da configuração dos três [Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) envolvidos. O fluxo abaixo descreve o que acontece quando os Tipos estão configurados no padrão típico de loja.

1. **Lance um Tipo `ORÇAMENTO`** em `202`. O orçamento **não baixa estoque** e **não gera financeiro** — serve apenas para registrar a proposta ao cliente. *Configuração-chave do Tipo `ORÇAMENTO`*: `Itens → Estoque` sem Transação que afete saldo; `Financeiro → Financeiro 1` com `Gerar Lançamento` desligado; `Finalizar/Mudar → Mudar` apontando para o Tipo `PEDIDO`.
2. **Cliente aprova → `F7` (Mudar)** transforma o `ORÇAMENTO` em `PEDIDO`. Neste momento, o **estoque é baixado** e o **financeiro é gerado** (conta a receber em aberto, com as parcelas da Condição de Pagamento escolhida). *Configuração-chave do Tipo `PEDIDO`*: `Itens → Estoque` com `Transação de Estoque` que subtrai `Físico` e `Disponível`; `Financeiro → Financeiro 1` com `Gerar Lançamento` ligado, Plano de Contas, Centro de Custo e Tipo de Documento Padrão definidos; `Finalizar/Mudar → Mudar` apontando para `NFC-E CUPOM FISCAL` (ou outro Tipo fiscal).
3. **Faturar → `F7` novamente** transforma o `PEDIDO` em `NFC-E CUPOM FISCAL`. Neste momento, o sistema **dispara a quitação** dos títulos gerados na etapa anterior e, em sequência, **inicia a emissão do documento fiscal** (NFC-e enviada à SEFAZ, retorno com protocolo, cupom impresso). *Configuração-chave do Tipo `NFC-E CUPOM FISCAL`*: `Cabeçalho → Fiscal` com Modelo de Documento `NFC-e`, Série fiscal padrão e CFOPs `5xxx`; `Finalizar` configurado para quitar automaticamente; o efeito de estoque/financeiro **não se duplica** porque o `PEDIDO` já fez essa parte (o Tipo de mudança herda referência ao movimento-pai).

Variações comuns: um único Tipo `VENDA` que junta os passos 2 e 3 (para vendas sem orçamento prévio); pedido que termina em `NF-E` em vez de `NFC-e` (vendas com cliente identificado e fiscal completo); pedido que vira `OS` (ordem de serviço aberta) e só depois vira nota fiscal.

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
