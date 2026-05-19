# 📄 Departamento de Produtos - Sol.NET

## 🎯 Visão Geral

**Departamento de Produtos** é um cadastro auxiliar de classificação livre, paralelo à hierarquia Família → Grupo → Subgrupo. Cada produto pode ser vinculado a, no máximo, um Departamento, geralmente para refletir a estrutura interna da loja ou o setor responsável pela mercadoria.

A interpretação do Departamento depende da empresa. No varejo, costuma representar a seção física da loja (açougue, padaria, bazar, hortifrúti). No atacado e indústria, pode representar uma área de negócio, uma linha de produto ou um setor operacional. O sistema não impõe regra fixa — é um rótulo livre para separar produtos em relatórios e filtros sem alterar a classificação fiscal.

### Principais características

- ✅ **Cadastro mínimo** — apenas uma descrição por registro.
- ✅ **Campo livre** — sem regra fixa de uso; cada empresa define o significado.
- ✅ **Vinculável ao produto** pela aba `Principal` do `Cadastro de Produtos` (campo "Departamento").
- ✅ **Independente da hierarquia** Família/Grupo/Subgrupo — pode ser usado em conjunto ou no lugar dela, conforme a operação.

---

## 🚪 Como acessar

Abra a pesquisa universal (atalho `F1`) e digite **`104`** (ou parte do nome `Departamento`).

---

## 📝 Campo do cadastro

A tela tem um único campo na área de lançamento:

- **Descrição** — texto livre, obrigatório, gravado em maiúsculas. Aceita números, letras (sem acentos) e os caracteres especiais `_ - + % , . /`.

> 💡 A `Descrição` é o que aparece no combo `Departamento` da aba `Principal` do `Cadastro de Produtos` e nos relatórios que filtram por essa classificação. Use nomes objetivos que reflitam o setor ou a área (ex.: `ACOUGUE`, `PADARIA`, `INFORMATICA`, `LIMPEZA`).

---

## ⚙️ Regras de validação

- **Descrição obrigatória** — não é possível salvar com o campo vazio.
- **Descrição única** — dois Departamentos não podem ter a mesma descrição (comparação sem distinção de maiúsculas/minúsculas). Se tentar, o sistema avisa `(VALOR) Já Existe!`.

---

## 🔗 Relação com Produtos

O Departamento aparece no `Cadastro de Produtos` (código `32`), aba `Principal`, no combo "Departamento". Cada produto pode ser vinculado a, no máximo, um Departamento.

**Não é possível excluir** um Departamento que já esteja vinculado a algum produto. Antes de remover, retire o vínculo dos produtos que o usam (no `Cadastro de Produtos`, mude o campo `Departamento` para outro valor ou deixe em branco).

---

## 💡 Exemplos Práticos

### Cenário 1 — Setores físicos de uma loja de varejo

Um supermercado cria os Departamentos `ACOUGUE`, `PADARIA`, `MERCEARIA`, `HORTIFRUTI`, `LIMPEZA`, `BAZAR`. Cada produto recebe o Departamento que corresponde à sua seção. Os relatórios de venda por seção filtram por esse campo para entender o desempenho de cada área.

### Cenário 2 — Linhas de produto em uma indústria

Uma fábrica de móveis define Departamentos como `ESTOFADOS`, `MADEIRA`, `METAIS`, `ESTOFAMENTO TECIDO`. Os produtos são vinculados pela linha que representam. Os pedidos de compra e os relatórios fiscais separam o consumo de matéria-prima por linha.

### Cenário 3 — Áreas administrativas

Uma distribuidora separa Departamentos por área responsável: `VENDAS DIRETAS`, `VENDAS ONLINE`, `B2B`. Cada produto é classificado pela equipe que o comercializa, ajudando o gerenciamento de comissão e meta por equipe.

---

## ❓ FAQ / Problemas Comuns

### ❓ Preciso usar Departamento se já uso Família e Grupo?

Não. O Departamento é uma classificação **opcional e paralela** à hierarquia Família/Grupo/Subgrupo. Use quando precisar separar produtos por critério diferente do hierárquico (por exemplo, setor físico da loja em vez de natureza do produto). Em muitas empresas, Departamento e Grupo acabam sendo equivalentes — vale escolher um dos dois para não duplicar informação.

### ❓ Qual a diferença entre `Departamento` e `Lista de Produtos`?

Tecnicamente os dois são campos livres de classificação no `Cadastro de Produtos` (código `32`), sem regra fixa imposta pelo sistema. A convenção mais comum é usar `Departamento` para a divisão estrutural (setor ou área de negócio) e `Lista` para marcações soltas e temporárias (campanhas, curva ABC, itens pesáveis do Self-Checkout). Mas isso fica a critério da empresa.

### ❓ Tentei excluir um Departamento e o sistema bloqueou. Por quê?

O Departamento já está vinculado a um ou mais produtos. Abra o `Cadastro de Produtos` (código `32`), localize os produtos que o usam e mude o campo `Departamento` deles antes de excluir o registro.

### ❓ Posso ter o mesmo produto em dois Departamentos?

Não. O campo `Departamento` no `Cadastro de Produtos` aceita apenas um valor por produto. Para outras classificações em paralelo, use Família, Grupo, Subgrupo ou Lista.

### ❓ Onde o Departamento aparece nos relatórios?

A maioria dos relatórios de produto, venda, estoque e compras oferece o filtro `Departamento` no cabeçalho do relatório. Em telas de pedido e movimentação, o Departamento também é exibido nas listas auxiliares quando o produto está vinculado.

### ❓ A descrição aceita acento?

Não. O campo grava em maiúsculas e sem acentos — `ELETRÔNICOS` será salvo como `ELETRONICOS`. Isso uniformiza a busca textual nos relatórios e nos filtros.

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Equipe de suporte Hetosoft e usuários do Sol.NET
