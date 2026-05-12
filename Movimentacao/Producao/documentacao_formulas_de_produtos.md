# 📄 Cadastro de Fórmula de Produtos - Sol.NET

## 🎯 Visão Geral

A **Fórmula de Produto** é a *receita* que ensina ao Sol.NET **o que entra** (ingredientes) e **o que sai** (produto acabado + perdas) na produção interna. Cada fórmula amarra um **produto acabado** a uma lista de **ingredientes** com quantidade e unidade de medida, mais um cálculo de **proporção** (Fator de Conversão × Total Produzido) que diz quantas unidades do acabado a fórmula gera a partir do total dos insumos.

A fórmula sozinha não consome estoque nem gera produto — ela é só o **plano**. Quem executa a receita é a tela `Produção de Produtos` (código `144`), que parte de uma fórmula, ajusta as quantidades para a produção do dia, e gera os três movimentos automáticos: saída dos ingredientes, entrada do acabado e (quando há) registro da perda.

> 💡 **Quem usa.** Indústrias, padarias, manipulação, açougues e qualquer operação que **transforma** insumos em um produto final cuja unidade ou natureza muda no caminho.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Fórmula de Produtos |
| **Código (`F1`)** | `143` |

Abra a pesquisa universal (atalho `F1`) e digite **`143`** ou parte do nome **`Fórmula de Produtos`**.

> 💡 **Atalho a partir do produto.** A tela `Cadastro de Produtos` (código `32`) tem um botão / opção `Cadastrar Fórmula` que abre esta tela já preenchida com o produto acabado selecionado. Útil quando você está editando o cadastro do produto e quer criar a fórmula sem voltar à pesquisa.

---

## 📝 Campos do cabeçalho

### Filtros da consulta (lista de fórmulas)

A tela abre com filtros de busca no topo:

| Filtro | O que faz |
|--------|-----------|
| **Inicial / Final** | Período de cadastro das fórmulas listadas. |
| **Produto Acabado** | Filtra fórmulas pelo produto final (dois cliques abrem a pesquisa de produtos). |
| **Status (Ativo / Inativo)** | Inclui ou exclui fórmulas inativadas. |

### Dados da fórmula

| Campo | Para quê serve |
|-------|----------------|
| **Descrição** | Nome livre da fórmula (até 120 caracteres). Use algo que descreva produção + variação: `PÃO FRANCÊS — RECEITA BASE`, `BISCOITO COCO 500G`. |
| **Data Cadastro** | Data da criação da fórmula. Preenchida automaticamente com a data de hoje. |
| **Produto Acabado** | O produto que sai da produção. Dois cliques (ou `F1`) abrem a pesquisa de produtos para selecionar. Ao escolher o produto, a unidade de medida do acabado é carregada automaticamente. |
| **Inativo** | Quando marcado, a fórmula deixa de aparecer no `Cadastro de Produção` (código `144`) sem precisar excluí-la. |

### Proporção

A proporção amarra a quantidade total que a fórmula produz à quantidade de itens (unidades do acabado) que isso representa.

| Campo | Para quê serve |
|-------|----------------|
| **Fator Conversão** | Quantos itens cabem em uma unidade base do total produzido. Ex.: se a receita produz `2 kg` e cada item é `200 g`, o fator é `0,2`. |
| **Total Produzido** | Quantidade total que a fórmula gera, na unidade de produção (ex.: `2 kg`). |
| **Itens Produzidos** | Quantos itens do produto acabado a fórmula gera. **Calculado** automaticamente: `Total Produzido ÷ Fator Conversão`. |
| **UN** (ao lado do Total Produzido) | Unidade de produção (a unidade do `Total Produzido` — pode ser diferente da unidade do produto acabado). |
| **UN** (ao lado do Itens Produzidos) | Unidade do produto acabado — preenchida automaticamente a partir do produto escolhido. |

> ⚠️ **Unidade fracionável.** Se a unidade do produto acabado **não** é fracionável (por exemplo, `UN`, `PEÇA`), o sistema arredonda `Itens Produzidos` para cima e ajusta `Total Produzido` correspondente, exibindo a mensagem *"A quantidade de itens produzidos deve ser um número inteiro, a unidade de medida não é fracionável"*. Em unidades fracionáveis (`KG`, `L`), o cálculo aceita decimais.

---

## 🔧 Painel `Ingredientes`

O painel inferior do formulário recebe **uma linha por ingrediente** (ou perda). É aqui que a "receita" de fato é montada.

### Campos da linha

| Campo | Para quê serve |
|-------|----------------|
| **Tipo Item** | Define o papel da linha: **Composição** (ingrediente que entra no produto) ou **Perda** (insumo que se perde no processo — encolhimento, evaporação, refugo). O Sol.NET separa os totais conforme o tipo. |
| **Produto Acabado** (= ingrediente) | O produto consumido nesta linha. Dois cliques abrem a pesquisa de produtos. Ao selecionar, código, descrição e unidade são carregados automaticamente. |
| **Qtd. Ingrediente** | Quantidade necessária deste ingrediente, na unidade do ingrediente. |
| **UN** | Unidade do ingrediente (preenchida automaticamente). |

### Botões

| Botão | O que faz |
|-------|-----------|
| **Inserir** | Inicia uma nova linha de ingrediente. |
| **Atualizar** | Grava as alterações feitas na linha selecionada. |
| **Deletar** | Remove a linha selecionada. |
| **Cancelar** | Cancela a inclusão/edição em andamento (pede confirmação). |
| **Deletar Todos** | Apaga todos os ingredientes da fórmula. |
| **Deletar Selecionados** | Apaga apenas os ingredientes marcados na grade. |

### Totais calculados

O painel exibe dois totais agregados, quando faz sentido (todos os itens estão na mesma unidade):

| Campo | O que mostra |
|-------|--------------|
| **Total Qtd. Ingredientes** | Soma das quantidades das linhas tipo **Composição**, exibida com a unidade correspondente. Aparece apenas se todas as linhas de composição estiverem na mesma unidade. |
| **Total Perdas** | Soma das quantidades das linhas tipo **Perda**, exibida com a unidade correspondente. Mesma regra: só aparece se todas estiverem na mesma unidade. |

> ℹ️ **Quando os totais somem.** Se a fórmula mistura unidades diferentes (ex.: `KG` e `L`), o total agregado é ocultado — não há somatório que faça sentido. Os valores individuais continuam visíveis na grade.

---

## ✅ Validações automáticas ao salvar

| Quando você grava | O sistema verifica |
|-------------------|--------------------|
| Sempre | Os campos obrigatórios do cabeçalho estão preenchidos: `Descrição` e `Produto Acabado`. |
| Sempre | A fórmula tem **ao menos um ingrediente** — gravar uma fórmula vazia é recusado com a mensagem *"Fórmula não possui ingredientes!"*. |
| Sempre | Não pode haver um ingrediente em edição não confirmado — o `Inserir` precisa estar finalizado por `Atualizar` ou `Cancelar`. |
| Ao recalcular `Itens Produzidos` | Se a unidade do produto acabado **não é fracionável**, o valor é arredondado para inteiro automaticamente. |

---

## 🚫 Exclusão

A exclusão remove a fórmula e todos os seus ingredientes em uma única transação. **Não há bloqueio** mesmo que a fórmula já tenha sido usada em produções passadas — o histórico de produções (em `PRODUCAO_PRODUTOS`) tem suas próprias linhas e não é afetado.

> ⚠️ **Boa prática.** Se a fórmula já foi usada em produção, **prefira marcar como Inativo** em vez de excluir — preserva a referência histórica e evita confusão se alguém precisar recriar a fórmula original.

---

## 🔁 Atalhos da grade

| Ação | Como fazer |
|------|------------|
| Abrir uma fórmula da lista | Clique duplo na linha **ou** Enter sobre ela. |
| Ir ao cadastro do ingrediente | Clique-direito sobre uma linha de ingrediente → `Ir no Produto`. Abre o `Cadastro de Produtos` (código `32`) já posicionado no item. |

---

## 💡 Exemplos práticos

### Exemplo 1 — Fórmula simples: receita de pão (2 kg gera 20 unidades de 100 g)

1. Pesquisa `F1` → `143` → abre `Cadastro de Fórmula de Produtos`.
2. Clique em **Novo**.
3. Cabeçalho:
   - `Descrição`: `PÃO FRANCÊS — BASE`.
   - `Produto Acabado`: clique duplo, escolha `PÃO FRANCÊS 100G`. A unidade carrega como `UN`.
4. Proporção:
   - `Total Produzido`: `2`.
   - `UN` (ao lado do Total Produzido): `KG`.
   - `Fator Conversão`: `0,1` (cada item pesa 100 g = 0,1 kg).
   - `Itens Produzidos`: calculado automaticamente como `20`.
5. Painel **Ingredientes** → **Inserir**, para cada ingrediente:
   - `Tipo Item`: `Composição`.
   - `Produto Acabado`: o ingrediente (ex.: `FARINHA DE TRIGO`).
   - `Qtd. Ingrediente`: `1,2` em `KG`.
   - **Atualizar**.
   - Repita para `ÁGUA`, `FERMENTO`, `SAL` etc.
6. **Gravar**.

### Exemplo 2 — Fórmula com perda registrada

Cenário: a produção de uma carne moída perde 5 % do peso na limpeza.

1. Faça os passos 1-5 do Exemplo 1, com os ingredientes da composição.
2. No painel **Ingredientes**, clique **Inserir** novamente:
   - `Tipo Item`: `Perda`.
   - `Produto Acabado`: o mesmo insumo que sofre perda (ex.: `CARNE BOVINA — PEÇA`).
   - `Qtd. Ingrediente`: `0,05` por kg processado (ou o valor absoluto do desperdício esperado).
   - **Atualizar**.
3. **Gravar**.

> Na execução em `Produção de Produtos` (código `144`), a Perda gera um movimento de saída separado, com o respectivo Tipo de Movimento configurado para perda — útil para análise de custos.

### Exemplo 3 — Criar a fórmula a partir do cadastro do produto

1. Pesquisa `F1` → `32` → abre `Cadastro de Produtos`.
2. Localize e abra o produto acabado.
3. Use a opção `Cadastrar Fórmula` (no menu ou botão da própria tela de produtos).
4. A tela `Cadastro de Fórmula de Produtos` abre direto em modo **Novo**, com o produto acabado já preenchido e bloqueado para edição (não é possível trocar o produto neste fluxo).
5. Preencha proporção e ingredientes normalmente.
6. **Gravar**.

---

## ❓ FAQ / Problemas comuns

**O campo `Itens Produzidos` está vazio mesmo eu tendo preenchido Total Produzido e Fator.**
O cálculo dispara ao sair do campo. Clique fora do campo ou pressione `Tab` depois de digitar — o `Itens Produzidos` deve preencher automaticamente.

**Mudei o Fator Conversão e o sistema arredondou meu Total Produzido. Por quê?**
A unidade do produto acabado não é fracionável (ex.: `UN`, `PEÇA`). O sistema garante que `Itens Produzidos` seja inteiro e recalcula `Total Produzido` na mesma proporção. Se você precisa de itens fracionados, troque a unidade do produto acabado para uma fracionável (`KG`, `L`).

**Posso usar a mesma fórmula para empresas diferentes?**
Sim — a fórmula é global, não tem vínculo de empresa. O vínculo aparece só na execução, no `Cadastro de Produção` (código `144`).

**Posso ter mais de uma fórmula para o mesmo produto acabado?**
Sim. Cada fórmula tem sua própria `Descrição` e é selecionada manualmente na hora da produção. Útil para variações de receita (versão econômica, versão premium, batch grande × batch pequeno).

**Os totais `Total Qtd. Ingredientes` e `Total Perdas` sumiram do painel.**
Isso acontece quando os ingredientes (ou perdas) estão em **unidades diferentes**. O Sol.NET evita somar `KG` com `L`. Padronize a unidade dos itens daquele tipo para ver o total agregar; ou ignore o agregado e consulte os valores individualmente nas linhas.

**Por que `Deletar Todos` não pede confirmação detalhada?**
Pede sim — o sistema mostra a mensagem padrão de confirmação de exclusão antes de apagar. Em produções já executadas, lembre que as fórmulas históricas referenciadas pelas produções continuam guardadas no banco até a fórmula ser efetivamente excluída.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Como se relaciona |
|------|---------------|--------------------|
| `Cadastro de Produtos` | `32` | Fonte do `Produto Acabado` e dos ingredientes. Tem atalho `Cadastrar Fórmula` que abre esta tela. |
| `Produção de Produtos` | `144` | Executa a fórmula — consome os ingredientes, gera o acabado e a perda. |
| `Tipos de Movimento` | `37` | Cada produção depende de Tipos de Movimento configurados para saída de insumo, entrada de acabado e perda. |
| `Saldo Estoque` | `78` | Onde o efeito final da produção (queda dos insumos + entrada do acabado) é visível. |

---

## ⚠️ Limites desta documentação

- Não cobre a **execução** da fórmula — esse fluxo está em `Produção de Produtos` (código `144`).
- Não trata regras de **custo** (custo médio do acabado calculado a partir dos ingredientes consumidos) — esse cálculo é feito automaticamente na produção e está descrito no guia "Atualização de Custo Automática".
- Fórmulas de **produtos agronômicos formulados** (`FORMULADOS_AGRONOMICOS`) usam um cadastro próprio no módulo Agronômico, não esta tela.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de Suporte / Administradores / Setor de Produção
