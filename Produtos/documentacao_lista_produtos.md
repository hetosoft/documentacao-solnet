# 📄 Lista de Produtos - Sol.NET

## 🎯 Visão Geral

**Lista de Produtos** é um cadastro auxiliar livre, usado para criar uma classificação extra do produto que não cabe nas outras categorias do Sol.NET (Família, Grupo, Subgrupo, Departamento, Marca, Fabricante).

A interpretação da `Lista` depende da empresa: pode ser uma campanha sazonal, um grupo de itens promocionais, um conjunto de produtos pesáveis para o Self-Checkout, uma marcação interna para relatórios — qualquer rótulo que ajude a separar produtos sem alterar a hierarquia oficial.

### Principais características

- ✅ **Cadastro mínimo** — apenas uma descrição por registro.
- ✅ **Campo livre** — sem regra fixa de uso; cada empresa decide o significado.
- ✅ **Vinculável ao produto** pela aba `Principal` do `Cadastro de Produtos` (campo "Lista").
- ✅ **Usado pelo Self-Checkout** para identificar itens pesáveis (frutas, verduras, padaria), quando essa operação está ativa.

---

## 🚪 Como acessar

Abra a pesquisa universal (atalho `F1`) e digite **`80`** (ou parte do nome `Lista de Produtos`).

---

## 📝 Campo do cadastro

A tela tem um único campo na área de lançamento:

- **Descrição** — texto livre, obrigatório, gravado em maiúsculas. Aceita números, letras (sem acentos) e os caracteres especiais `_ - + % , . /`.

> 💡 A `Descrição` é o que aparece no combo `Lista` da aba `Principal` do `Cadastro de Produtos` e nos relatórios que filtram por essa classificação. Escolha um nome curto e direto — o sistema converte automaticamente para maiúsculas.

---

## ⚙️ Regras de validação

- **Descrição obrigatória** — não é possível salvar com o campo vazio.
- **Descrição única** — duas Listas não podem ter a mesma descrição (comparação sem distinção de maiúsculas/minúsculas). Se tentar, o sistema avisa `(VALOR) Já Existe!`.

---

## 🔗 Relação com Produtos e Self-Checkout

A `Lista` aparece em dois lugares no sistema:

1. **Cadastro de Produtos** (código `32`) — aba `Principal`, campo "Lista". Cada produto pode pertencer a, no máximo, uma Lista.
2. **Self-Checkout — Itens Pesáveis** — quando o módulo Self-Checkout está habilitado, a Lista é o vínculo que identifica os itens que precisam de balança no terminal de autoatendimento.

**Não é possível excluir** uma Lista que já esteja vinculada a algum produto. Antes de remover, retire o vínculo dos produtos que a usam (no `Cadastro de Produtos`, mude o campo `Lista` para outro valor ou deixe em branco).

---

## 💡 Exemplos Práticos

### Cenário 1 — Marcação de produtos sazonais

Uma loja de varejo cadastra a Lista `NATAL 2026`. Cada produto que entra na campanha de Natal recebe essa Lista no cadastro. Depois, os relatórios de venda filtram por essa Lista para medir o desempenho da campanha sem mexer no Grupo ou Departamento do produto.

### Cenário 2 — Itens pesáveis no Self-Checkout

Um supermercado com Self-Checkout cria a Lista `PESAVEIS HORTI`. Todos os produtos vendidos a peso (banana, tomate, alface) recebem essa Lista. O terminal do Self-Checkout usa essa marcação para acionar a balança e pedir confirmação do peso.

### Cenário 3 — Curva ABC interna

Uma distribuidora cria três Listas: `CURVA A`, `CURVA B`, `CURVA C`. Os produtos são vinculados de acordo com o giro. Os compradores filtram a tela de pedido de compra pela Lista para priorizar reposição dos itens da curva A.

---

## ❓ FAQ / Problemas Comuns

### ❓ Qual a diferença entre `Lista de Produtos` e `Departamento de Produtos`?

Não há regra fixa imposta pelo sistema — os dois são **classificações livres** que ficam no `Cadastro de Produtos`. A escolha de qual usar depende da convenção interna da empresa. Em muitos varejos, `Departamento` é usado para a seção física da loja (açougue, padaria, mercearia) e `Lista` fica como rótulo livre para campanhas e agrupamentos paralelos.

### ❓ Posso ter o mesmo produto em duas Listas?

Não. O campo `Lista` no `Cadastro de Produtos` é único — cada produto pertence a uma Lista (ou a nenhuma). Para múltiplas marcações, considere usar outras classificações disponíveis (Família, Grupo, Departamento) em paralelo.

### ❓ Tentei excluir uma Lista e o sistema bloqueou. Por quê?

A Lista já está vinculada a um ou mais produtos. Abra o `Cadastro de Produtos` (código `32`), localize os produtos que usam essa Lista e mude o campo `Lista` deles antes de excluir o registro.

### ❓ Preciso cadastrar Listas antes de cadastrar produtos?

Não. A classificação é opcional. Você pode cadastrar produtos sem informar Lista e voltar depois para preencher o campo quando definir a categorização que faz sentido para o negócio.

### ❓ Onde a Lista aparece nos relatórios?

A maioria dos relatórios de produto, venda e estoque oferece o filtro `Lista` quando o produto está vinculado a uma. Os filtros aparecem no cabeçalho do relatório, lado a lado com Família, Grupo, Subgrupo e Departamento.

### ❓ A descrição aceita acento?

Não. O campo grava em maiúsculas e sem acentos — `ELETRÔNICOS` será salvo como `ELETRONICOS`. Isso facilita a busca textual nos relatórios e nos filtros.

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Equipe de suporte Hetosoft e usuários do Sol.NET
