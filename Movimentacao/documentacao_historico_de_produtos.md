# 📄 Histórico de Produtos - Sol.NET

## 🎯 Visão Geral

O **Histórico de Produtos** é a tela de análise **item a item** das movimentações do Sol.NET. Onde o `Histórico de Movimentações` (código `205`) enxerga o cabeçalho de cada venda/compra, esta tela explode os movimentos em **linhas de item** e oferece análises que dependem dessa granularidade: margem por SKU, curva ABC, vendas por cliente × produto, comparação Compra × Venda, análise por Família / Grupo / Sub-grupo, evolução de saldo do produto, tributação aplicada, comissão por item, e geração de pedido de compra a partir de uma lista de produtos selecionados.

A consulta usa os mesmos filtros do Histórico de Movimentações com extensões específicas de produto (família, grupo, sub-grupo, fornecedor, marca/fabricante, código de barras). A tela não altera dados — é leitura e análise — mas tem **uma ação operacional**: o atalho **Pedido de Compra** gera um pedido pré-preenchido com os produtos selecionados na lista.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Histórico de Produtos |
| **Código (`F1`)** | `206` |

Abra a pesquisa universal (atalho `F1`) e digite **`206`** ou parte do nome **`Histórico de Produtos`**.

---

## ⌨️ Atalhos da tela

| Tecla | O que faz |
|-------|-----------|
| `F1` | Pesquisa universal. |
| `F3` | Abre o **Relatório** do resultado consultado. |
| `F5` | **Atualiza** a consulta com os filtros atuais. |

---

## 🎚️ Filtros

Os filtros principais são os mesmos do `Histórico de Movimentações` (Loja, datas, Tipo de Movimento, Status, Vendedor, Operador, Turno, PDV, Devolução, Tipo Documento etc.). Para detalhes, consulte aquele documento.

### Filtros específicos do produto

| Filtro | Para quê serve |
|--------|----------------|
| `Campo a pesquisar` | Inclui opções extras voltadas ao item: `Produto`, `Marca/Fabricante`, `Fornecedor Padrão`, `Fornecedor Vinculado`, `Atualização em Grupo`, `Grupo de Produtos`, `Família de Produtos`, `Sub Grupo de Produtos`, `Código de Barra`, `CST ICMS`, `Descrição X`. |
| **Agrupar** | Agrupa o resultado por Família, Grupo, Sub-grupo ou outra dimensão do cadastro. |
| `Tipo Produto / Serviço` | Filtra itens por classificação (mercadoria, matéria-prima, serviço etc.). |

### Validações da consulta

São as mesmas do `Histórico de Movimentações`: `Hora Inicial / Final` precisam estar preenchidas juntas, combinações `Devolução × Tipo Movimento × Movimento` precisam ser coerentes, aba `Comissão` exige Vendedor selecionado e configuração de comissão completa.

---

## 🧭 Sub-abas da tela

Cada aba mostra a **mesma busca** sob uma lente diferente. Trocar de aba **não** refaz a consulta — usa o resultado já carregado.

| Aba | O que mostra |
|-----|--------------|
| **Pesquisar** / **Outros 2** | Filtros. |
| **Pesquisa Salva** | Salvar / recuperar conjunto de filtros nomeado (mesmo recurso do `Histórico de Movimentações`). |
| **Produtos → Produto** | Listagem item a item dos movimentos. |
| **Produtos → Família/Grupo** | Agrupado por Família e Grupo de produtos. |
| **Produtos → Mês** | Evolução por mês do produto / família. |
| **Produtos → Totais** | Totais consolidados (quantidade, valor, custo, margem). |
| **Produtos → Estoque** | Saldo atual do produto cruzado com a consulta. |
| **Produtos → Histórico Estoque** | Evolução do saldo no período. |
| **Produtos → Códigos** | Códigos de barras e referências cruzadas. |
| **Produtos → Similares** | Produtos similares cadastrados ao item. |
| **Compra × Venda** | Compara o que foi comprado contra o que foi vendido — útil para identificar giro lento e excesso. |
| **Produto × Cliente** | Quem comprou o quê — análise de fidelização. |
| **Produtos Cancelados** | Itens cancelados no período. |
| **Produtos Linkado** | Itens com vínculos (kits, montagem). |
| **Margem** | Análise de margem item a item — base para a **Curva ABC**. |
| **Tabela de Preço** | Quais Tabelas de Preço foram usadas. |
| **Tributação → Estadual / Federal** | Impostos aplicados (ICMS, PIS, Cofins, IPI) item a item. |
| **Comissão → Vendas / Devolução** | Comissão calculada por item para o vendedor. |
| **Gráficos** | Visões gráficas. |

---

## 📈 Análise ABC (aba `Margem`)

A aba `Margem` oferece a classificação ABC dos produtos do resultado:

- Cada produto recebe uma classificação **A**, **B** ou **C** conforme sua participação no valor total (ou na quantidade) das vendas do período.
- Os **parâmetros** (percentual de corte entre A/B/C, base do cálculo, tipo de curva) são configurados na própria aba — o sistema valida (`ConferirParametrosABC`) e pede correção caso a soma das faixas não bata 100 % ou os limites estejam invertidos.
- Mensagem típica quando os parâmetros estão inconsistentes: *"Refaça os parâmetros."* — ajuste e rode novamente.

> 💡 **Usos típicos.** A análise A/B/C ajuda a focar política de estoque (faixa A → comprar com mais frequência, evitar ruptura), preços (faixa C → revisar margem ou retirar do catálogo) e atendimento (faixa A → priorizar prazo).

---

## 🛒 Gerar Pedido de Compra a partir da lista

Atalho exclusivo desta tela: a opção **`Pedido de Compra`** no menu de contexto da lista permite gerar um pedido pré-preenchido a partir dos produtos selecionados.

1. Selecione os produtos desejados na lista (use `Selecionar Todos` se for o caso, respeitando o limite de **1.500 registros por seleção**).
2. Clique-direito → `Pedido de Compra` (atalho).
3. O Sol.NET abre o `Cadastro de Pedido de Compra` (código `64`) já com os produtos lançados.
4. Ajuste quantidades, fornecedor e demais campos antes de gravar.

Se nenhum produto estiver selecionado, a operação é recusada com *"Nenhum produto selecionado!"*. Acima de 1.500 itens, a mensagem é *"Não permitido selecionar mais que 1.500 registros!"*.

### Copiar produtos selecionados

Outra opção do menu de contexto: **`Copiar Produtos Selecionados`** copia os códigos dos produtos selecionados para a Área de Transferência — útil para colar em planilhas, e-mails ou outras telas que aceitem lista de IDs. Sucesso: *"Códigos de Identificação dos Produtos Copiado para Área de Transferência!"*.

---

## 💡 Exemplos práticos

### Exemplo 1 — Margem do mês por produto

1. Pesquisa `F1` → `206`.
2. Filtros:
   - `Descrição da Loja`: a empresa.
   - `Inicial` / `Final`: o mês.
   - `Tipo Movimento`: `Vendas`.
3. `F5` → vá à aba **Margem**.
4. Cada produto aparece com Custo, Venda, Margem e classificação ABC.
5. Para ordenar pela maior margem absoluta, clique no cabeçalho da coluna.

### Exemplo 2 — Compra × Venda do trimestre

1. Pesquisa `F1` → `206`.
2. Filtros amplos: deixe `Tipo Movimento` em branco (vai trazer todos os tipos), defina datas do trimestre.
3. `F5` → vá à aba **Compra × Venda**.
4. Use a coluna de diferença para identificar produtos com excesso de compra ou ruptura.

### Exemplo 3 — Gerar pedido de compra dos produtos de giro alto

1. Pesquisa `F1` → `206` → filtros + `F5`.
2. Aba **Margem** com classificação ABC → ordene por classificação `A`.
3. Selecione os produtos desejados (Ctrl+clique ou `Selecionar Todos`).
4. Clique-direito → `Pedido de Compra`.
5. Ajuste fornecedor e quantidades em `Pedido de Compra` (código `64`).

### Exemplo 4 — Comissão por produto

1. Pesquisa `F1` → `206` → filtros incluindo `Vendedor`.
2. `F5` → vá à aba **Comissão → Vendas**.
3. Cada item da venda aparece com sua respectiva comissão calculada conforme a regra do Cargo / Tipo de Comissão da empresa.

---

## ❓ FAQ / Problemas comuns

**A curva ABC mostrou todos os produtos como "A". O que houve?**
Os parâmetros da curva (cortes percentuais A / B / C) estão muito largos. Ajuste a faixa A para um percentual menor (ex.: 70 % do valor) e rode novamente. O sistema bloqueia com *"Refaça os parâmetros"* quando os limites somam mais que 100 %.

**Cliquei em `Pedido de Compra` mas o sistema não abriu nada.**
Você não tinha produto selecionado, ou ultrapassou o limite de 1.500 itens. Selecione um conjunto menor e repita.

**A aba `Tributação` está vazia.**
Os filtros incluem operações que não geram tributação (transferências, ajustes). Restrinja a `Tipo Movimento = Vendas` ou `Compras` para popular a aba.

**O que aparece em `Produtos Linkado`?**
Itens vinculados — geralmente kits (um produto de venda que aciona a baixa de vários SKUs componentes). O vínculo é definido no `Cadastro de Produtos` (código `32`).

**Os totais dos itens não batem com os totais do `Histórico de Movimentações`.**
Diferenças costumam ser por: (1) itens com `cancelado = sim` que somam no histórico mas saem da contagem aqui dependendo do filtro; (2) movimentos sem itens (ajustes financeiros, por exemplo) aparecem só no Histórico de Movimentações. Confira filtros com o mesmo escopo.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Como se relaciona |
|------|---------------|--------------------|
| `Histórico de Movimentações` | `205` | Mesma análise pelo cabeçalho do movimento — útil para totais por venda, vendedor, portador. |
| `Cadastro de Movimentos` | `53` | Origem dos dados. |
| `Cadastro de Produtos` | `32` | Cadastro dos itens listados — atalho `Ir no Produto` no menu de contexto. |
| `Cadastro de Pedido de Compra` | `64` | Destino do atalho `Pedido de Compra` da seleção. |
| `Saldo Estoque` | `78` | Saldo atual dos produtos analisados. |
| `Tabela de Preço` | `27` | Tabela aplicada em cada venda — aparece na aba `Tabela de Preço`. |

---

## ⚠️ Limites desta documentação

- Não detalha a configuração da **Curva ABC** (qual base usar, como interpretar) — é assunto de gestão de estoque/comercial, complementar a esta tela.
- Não cobre a **tributação** em si (regras de cálculo de ICMS, PIS, Cofins) — a tela apenas exibe o que foi calculado nos movimentos.
- Operações fora do escopo do item (acertos manuais, lançamentos financeiros desvinculados de produto) não aparecem aqui — use o `Histórico de Movimentações`.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de Suporte / Gestores Comerciais / Compras / Administração
