# 📄 Outros Movimentos - Sol.NET

## 🎯 Visão Geral

`Outros Movimentos` é a porta de entrada para todos os documentos que **afetam estoque ou financeiro** mas **não são compra nem venda** em sentido comercial direto: transferências entre lojas/locais, ajustes de inventário, perdas, consumo interno, brindes, amostras grátis, entradas/saídas pelo Pedido de Compra ou pela Produção, devoluções neutras, doações.

A tela compartilha o mesmo formulário operacional usado em `Movimentos de Compras` (`201`) e `Movimentos de Vendas` (`202`), mas **filtra os Tipos de Movimento disponíveis** apenas para aqueles com **Comportamento = Outros** no [Cadastro de Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) (`37`).

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Outros Movimentos |
| **Código (`F1`)** | `203` |

Abra a pesquisa universal (`F1`) e digite `203` ou parte do nome **Outros Movimentos**.

---

## 🧭 Particularidades do modo Outros

A categoria `Outros` é a mais **heterogênea** das três — cada Tipo aqui costuma ter sua configuração própria em `37`, porque o que essas operações têm em comum é só **não serem nem compra nem venda direta**. Cenários típicos:

- **Transferências entre lojas/locais** — Comportamento `Outros` com `Tipo Empresa Destino` definido em `Cabeçalho → Origem/Destino` da configuração do Tipo. Estoque sai do `Local Origem` e entra no `Local Destino`, com ou sem documento fiscal próprio (NF de transferência) conforme a regra.
- **Ajuste de Estoque** — o cadastro auxiliar `Ajuste de Estoque` (`79`) **dispara** movimentos visíveis aqui em `203`. O Tipo amarrado define se o ajuste é de entrada (positivo) ou saída (negativa). Veja [Ajuste de Estoque](../documentacao_ajuste_de_estoque.md).
- **Produção de Produtos** — `Produção de Produtos` (`144`) também **dispara** movimentos em `203`: saída dos ingredientes, entrada do acabado, perda. Veja [Produção](../Producao/documentacao_producao_de_produtos.md).
- **Pedido de Compra** convertido — `Pedido de Compra` (`64`) pode ser configurado para gerar movimento aqui em vez de em `201`, dependendo do desenho do cliente.
- **Brindes, amostras, doações, consumo interno** — Tipos `Outros` que tipicamente saem do estoque sem financeiro, ou com financeiro de despesa.
- **Devolução neutra** — quando a devolução não se enquadra como compra (sem refazer estoque do fornecedor) nem como venda (sem cliente final), pode ser cadastrada como `Outros` com regras dedicadas.

> 💡 **CFOPs aceitos**: o validador do CFOP em `Outros` é mais flexível — não há restrição absoluta de faixa como em Entrada/Saída. Cada Tipo definirá em `Cabeçalho → Fiscal` quais CFOPs aceita.

> ⚠️ **Atualizar Custo Automático**: válido em `Outros` (assim como em Compras). É comum em ajustes de inventário positivos e em entradas de produção (o produto acabado precisa de custo).

---

## 💡 Exemplos práticos

### Transferência entre lojas

1. Pesquisa `F1` → `203` → **Novo**.
2. `Tipo` = `TRANSFERÊNCIA ENTRE EMPRESAS` (configurado em `37` com Comportamento `Outros`, `Tipo Empresa Destino` definido).
3. **Cabeçalho**: `Local Origem` = local da loja A; `Empresa Destino` + `Local Destino` = loja B.
4. **Itens**: produtos e quantidades.
5. `F6` (Finalizar) → estoque sai do Local Origem e entra no Local Destino. Se o Tipo tem fiscal configurado, NF de transferência é emitida.

### Lançar perda de estoque (quebra/avaria)

1. Pesquisa `F1` → `203` → **Novo**.
2. `Tipo` = `PERDA DE ESTOQUE`.
3. **Itens**: produtos perdidos com quantidades.
4. `F6` → estoque baixa, lançamento no Histórico fica disponível para auditoria.

> 💡 Em vez de ir direto na `203`, prefira disparar a perda pelo cadastro auxiliar [Ajuste de Estoque](../documentacao_ajuste_de_estoque.md) (`79`) — ele cria o movimento aqui automaticamente, mas a inserção fica registrada na tela específica.

### Entrada de produto acabado vindo da Produção

1. Use o cadastro [Produção de Produtos](../Producao/documentacao_producao_de_produtos.md) (`144`) — ele dispara os movimentos em `203`.
2. Para consultar/auditar: pesquisa `F1` → `203` → filtrar por Tipo (`PRODUÇÃO - ENTRADA ACABADO`, `PRODUÇÃO - SAÍDA INGREDIENTE`, `PRODUÇÃO - PERDA`).

---

## 🔗 Documentação completa

O detalhamento do formulário — sub-abas, fluxos, atalhos, validações, exemplos comuns, FAQ — está em [Movimentos](documentacao_movimentos.md). Esta página descreve apenas o que diferencia o modo `Outros`.

Outras referências úteis:

- [Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) (`37`) — onde os Tipos `Outros` são configurados.
- [Ajuste de Estoque](../documentacao_ajuste_de_estoque.md) (`79`) — telas auxiliares que disparam movimentos aqui.
- [Produção de Produtos](../Producao/documentacao_producao_de_produtos.md) (`144`) — idem.
- [Histórico de Movimentações](../documentacao_historico_de_movimentacoes.md) (`205`) — trilha de auditoria.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Retaguarda de estoque / Logística / Suporte
