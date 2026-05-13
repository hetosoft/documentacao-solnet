# 📄 Movimentos de Compras - Sol.NET

## 🎯 Visão Geral

`Movimentos de Compras` é o ponto de entrada da operação **fiscal e de estoque de chegada**: notas fiscais de fornecedor, devoluções para fornecedor, recebimentos, importações. Toda mercadoria que **entra** com documento fiscal de compra é lançada aqui.

> ℹ️ **Transferências entre filiais** não ficam aqui — mesmo o lado da entrada de uma transferência. Transferências são operadas como movimentos auxiliares pela retaguarda e vivem em [Outros Movimentos](outros_movimentos.md) (`203`).

A tela compartilha o mesmo formulário operacional usado em `Movimentos de Vendas` (`202`) e `Outros Movimentos` (`203`), mas **filtra os Tipos de Movimento disponíveis** para aqueles configurados em [Cadastro de Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) (`37`) como entrada fiscal de compra.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Movimentos de Compras |
| **Código (`F1`)** | `201` |

Abra a pesquisa universal (`F1`) e digite `201` ou parte do nome **Movimentos de Compras**.

---

## 🧭 Particularidades do modo Compras

Tudo o que diferencia esta tela das outras duas vem do **Tipo de Movimento** selecionado no Cabeçalho. Os Tipos de Compras tipicamente trazem:

- **CFOPs de Entrada** (faixa `1xxx` para operações dentro do estado, `2xxx` para operações interestaduais, `3xxx` para importação). Tipo com CFOP fora da faixa é bloqueado ao gravar: *"CFOP não é de entrada!"*.
- **Transações de Estoque que somam Físico/Disponível** — a entrada adiciona saldo, não consome.
- **Tipos com Emissão = Terceiro** — a NF é de **outra** empresa (o fornecedor); o Sol.NET registra **Série** e **Número do Documento** vindos do papel/XML recebido, não numera localmente como faz nas Vendas.
- **`Atualizar Custo Automático` válido** — em Compras, o custo informado **atualiza** o custo do produto (FIFO, médio ponderado ou último custo, conforme a configuração). É o lançamento de entrada que define o custo no Sol.NET. Vendas não atualizam custo (regra global validada em `37`).
- **Devoluções para fornecedor** — Tipos como `DEVOLUÇÃO COMPRA` ficam aqui também (saída fiscal, mas categoricamente "compra ao contrário"). O fluxo exige **Movimento Referenciado** com a NF de compra original.
- **Importação de XML** — fluxos de importação automática de NF-e de fornecedor (a partir do XML recebido) entram nesta tela; abrem o formulário com cabeçalho e itens já preenchidos a partir do XML.

> 💡 **Não confunda com Pedido de Compra (`64`).** O `Pedido de Compra` é um documento **interno** (pré-compra) que **não** entra estoque nem gera financeiro definitivo. Ele apenas reserva e, ao ser convertido em entrada, **dispara** um movimento que aparece aqui em `201`. O efeito real de estoque/financeiro está no movimento de `201`, não no pedido.

---

## 💡 Exemplos práticos

### Recebimento de NF-e do fornecedor (com XML)

1. Pesquisa `F1` → `201` → **Importar XML** (botão; o caminho exato depende da personalização do menu).
2. Selecione o XML da NF-e recebida. O Sol.NET preenche Cabeçalho e Itens automaticamente.
3. Confira `Tipo de Movimento` proposto, `Local de Estoque` de entrada e as parcelas em `Financeiro`.
4. **Gravar** + **Finalizar** (`F6`) → estoque entra, conta a pagar é gerada.

### Devolução para fornecedor

1. Pesquisa `F1` → `201` → **Novo**.
2. `Tipo` = `DEVOLUÇÃO COMPRA`.
3. **Referenciar Nota** = NF de compra original (obrigatório — sem isso a validação bloqueia).
4. **Itens** = produtos devolvidos com as mesmas quantidades.
5. `F6` → estoque sai, fiscal de saída é emitido, conta a pagar original é abatida (conforme configuração do Tipo).

---

## 🔗 Documentação completa

O detalhamento do formulário — sub-abas, fluxos, atalhos, validações, exemplos comuns, FAQ — está em [Movimentos](documentacao_movimentos.md). Esta página descreve apenas o que diferencia o modo `Compras`.

Outras referências úteis:

- [Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) (`37`) — onde os Tipos de Entrada são configurados.
- [Transações de Estoque](../documentacao_transacoes_de_estoque.md) (`33`) — efeito da entrada nas camadas de saldo.
- [Histórico de Movimentações](../documentacao_historico_de_movimentacoes.md) (`205`) — trilha de auditoria.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de recebimento / Retaguarda fiscal / Suporte
