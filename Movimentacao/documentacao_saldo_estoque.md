# 📄 Saldo Estoque - Sol.NET

## 🎯 Visão Geral

A tela de **Saldo Estoque** é a **consulta principal** do estoque no Sol.NET: lista o saldo de cada produto em uma combinação específica de **Empresa**, **Local de Estoque** e **Situação do Estoque**, com filtros para Produto, Marca, Fornecedor, Grupo, Família, Sub-grupo, código de barras, status (ativo/inativo) e mais.

Os totais — Custo Inicial, Custo Unitário, Custo de Venda, Preço de Venda e Saldo — são calculados automaticamente no rodapé com base nos itens listados, e podem incluir ou ignorar saldos negativos. A consulta pode ser feita **no momento atual** (saldo de hoje) ou **em uma data passada** (saldo retroativo, no estilo inventário) bastando alterar o campo `Data do Estoque`.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Saldo Estoque |
| **Código (`F1`)** | `78` |

Abra a pesquisa universal (atalho `F1`) e digite **`78`** ou parte do nome **`Saldo Estoque`**.

---

## ⌨️ Atalhos da tela

| Tecla | O que faz |
|-------|-----------|
| `F1` | Abre a pesquisa universal (em qualquer tela do Sol.NET). |
| `F3` | Abre a tela de **Relatórios** desta consulta. |
| `F5` | **Atualiza** a consulta — equivale a clicar em buscar com os filtros atuais. |

---

## 🎚️ Filtros

Os filtros ficam no topo da tela. O sistema **lembra** dos valores que você escolheu por último (por usuário) e abre na próxima vez já com eles preenchidos.

| Filtro | Para quê serve |
|--------|----------------|
| **Descrição da Loja** | Empresa cuja consulta será exibida. Carrega apenas as empresas a que o usuário tem acesso. |
| **Local de Estoque** | Limita a consulta a um Local específico (`LOJA`, `DEPÓSITO`, etc.). |
| **Situação do Estoque** | **Obrigatório.** Define qual camada de saldo será mostrada (`FISICO`, `DISPONIVEL`, `RESERVADO` etc.). |
| **Data do Estoque** | Data-alvo. Se for **hoje**, o sistema usa o saldo atual. Se for **passada**, recalcula o saldo retroativo somando/subtraindo todos os movimentos entre a data e hoje (modo inventário). Datas futuras não são permitidas. |
| **Data** | Define qual data dos movimentos é usada no cálculo retroativo (por exemplo, data de emissão, data de saída ou data do movimento). |
| **Campo a ser pesquisado** | Define em qual atributo do produto a busca da caixa de pesquisa age (`Produto`, `Marca/Fabricante`, `Fornecedor Padrão`, `Fornecedor Vínculado`, `Atualização em Grupo`, `Grupo de Produtos`, `Família de Produtos`, `Sub Grupo de Produtos`, `Descrição X`, `CST ICMS`, `Código de Barra X`). |
| **Condição** | Como o valor digitado é comparado (`INICIA COM`, `CONTÉM`, `IGUAL`, `ENTRE`, `LISTA`, `FORA DA LISTA`). |
| **Caixa de pesquisa** | Texto, código ou ID a procurar. Com `INICIA COM` ou `CONTÉM` aceita texto livre; com `IGUAL`, `LISTA` etc., abre uma pesquisa específica (Produtos, Pessoas, Grupos, etc.) ao clicar duas vezes. |
| **Saldo** | Filtro de saldo: tudo, só com saldo, só sem saldo, só negativos. |
| **Tipo de Item** | Filtra produtos por classificação industrial/comercial/serviço. |
| **Divergências** | Mostra apenas produtos com inconsistências apontadas pelo sistema (cadastros incompletos, custo zerado etc.). |
| **Calcular Negativos** | Quando marcado, **inclui** saldos negativos no cálculo dos totais. Desmarcado (padrão), os negativos são ignorados nos totais — mas continuam aparecendo no grid. |
| **Status (Ativo / Inativo)** | Mostra produtos ativos, inativos ou ambos. |

---

## 📊 Resultado da consulta

### Grid de produtos

O grid principal lista um produto por linha, com Saldo, Custo Inicial, Custo Unitário, Custo Venda e Preço de Venda **acumulados** para a combinação Empresa + Local + Situação selecionada. As colunas podem ser personalizadas (largura, ordem, quais aparecem) com clique-direito no grid → `Configurar Grid`.

> 💡 **Ir para o produto.** Selecione uma linha e use a opção `Ir para Produto` no menu de contexto (clique-direito) — abre o `Cadastro de Produtos` (código `32`) já posicionado no item.

### Painel de totais

Logo abaixo do grid, cinco campos somam o conteúdo exibido:

| Campo | O que representa |
|-------|------------------|
| **Custo Inicial Total** | Soma do custo inicial × saldo de cada item. |
| **Custo Unitário Total** | Soma do custo unitário × saldo de cada item. |
| **Custo Venda Total** | Soma do custo de venda × saldo de cada item. |
| **Preço de Venda Total** | Soma do preço de venda × saldo de cada item. |
| **Saldo Total** | Saldo somado de todos os itens listados. |

A regra de inclusão de negativos é controlada pelo filtro `Calcular Negativos`.

### Sub-aba `Similar` (aparece sob demanda)

Quando o produto selecionado tem **similares** cadastrados (no `Cadastro de Produtos`, aba de Similares), a sub-aba `Similar` aparece automaticamente e mostra o saldo dos similares na mesma combinação de Empresa + Local + Situação. É útil para responder *"Não tenho do produto X, tenho de algum equivalente?"* sem sair da tela.

### Painel `Localização de Estoque` (lateral)

Ao selecionar um produto, o sistema preenche um painel com a **localização física** dele (corredor, prateleira, posição), conforme cadastrado em `Localização de Estoque` (código `29`). Útil em armazéns que precisam guiar o operador até a gôndola.

---

## ✅ Validações da consulta

| Quando você aciona a busca | O sistema verifica |
|---------------------------|--------------------|
| Sempre | `Situação do Estoque` deve estar preenchida — sem ela, a busca é recusada com a mensagem *"Situação de Estoque Obrigatório!"*. |
| Sempre | A `Data do Estoque` **não** pode ser maior que a data de hoje. |

---

## 💡 Exemplos práticos

### Exemplo 1 — Quanto tenho disponível de um produto na loja agora?

1. Pesquisa `F1` → `78` → abre `Saldo Estoque`.
2. Filtros:
   - `Descrição da Loja`: a empresa desejada.
   - `Local de Estoque`: `LOJA`.
   - `Situação do Estoque`: `DISPONIVEL`.
   - `Data do Estoque`: hoje (padrão).
   - `Campo a ser pesquisado`: `Produto`.
   - `Condição`: `INICIA COM`.
   - Caixa de pesquisa: parte do nome do produto.
3. Pressione `F5` (ou clique no botão de buscar).
4. O grid mostra o saldo do produto e o `Saldo Total` no rodapé.

### Exemplo 2 — Tirar saldo retroativo de uma data passada (inventário)

1. Pesquisa `F1` → `78`.
2. Defina os filtros como no Exemplo 1.
3. Em `Data do Estoque`, escolha uma **data passada** (ex.: último dia do mês anterior).
4. Em `Data`, escolha qual data do movimento é considerada (geralmente `Data Movimento` ou `Data de Emissão`).
5. `F5` para atualizar.

O sistema recalcula o saldo na data informada, percorrendo todo o histórico de movimentos. O cálculo pode demorar mais que a consulta atual, especialmente em bases grandes.

### Exemplo 3 — Encontrar produtos com saldo negativo

1. Pesquisa `F1` → `78`.
2. Filtros:
   - `Descrição da Loja`, `Local de Estoque`, `Situação do Estoque` (`FISICO`, em geral).
   - `Saldo`: `Negativo` (ou equivalente — o nome exato vem do combo).
   - Marque `Calcular Negativos` se quiser ver o impacto nos totais.
3. `F5`.

Saldo negativo aponta erros de configuração (Transação de Estoque mal configurada, movimento gravado sem o saldo correspondente, etc.). Resolva trocando a transação no `Cadastro de Tipos de Movimento` (código `37`) ou ajustando o saldo em `Ajuste de Estoque` (código `79`).

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Tipos de Movimento` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nesta tela.

### Exemplo 4 — Imprimir relatório do saldo consultado

1. Aplique os filtros e rode `F5` para popular o grid.
2. Pressione `F3` (ou clique em `Relatório`).
3. A tela de Relatórios abre passando os filtros aplicados — escolha o modelo e imprima ou exporte.

---

## ❓ FAQ / Problemas comuns

**O grid está vazio mesmo eu sabendo que o produto existe.**
Confira nesta ordem: (1) `Status (Ativo/Inativo)` — produtos inativos só aparecem com o filtro correspondente; (2) `Local de Estoque` — o produto pode ter saldo só em outro Local; (3) `Situação do Estoque` — o saldo pode estar em outra camada (ex.: `RESERVADO` em vez de `DISPONIVEL`); (4) `Empresa` — o produto pode ter saldo só em outra empresa.

**Por que o `Saldo Total` no rodapé é diferente da soma do grid?**
O `Calcular Negativos` está desmarcado, então saldos negativos no grid não entram no total. Marque a opção se quiser vê-los somados.

**Mudei a `Data do Estoque` para o mês passado e a consulta ficou muito lenta.**
É esperado — o saldo retroativo é recalculado percorrendo o histórico de movimentos. Em bases grandes, prefira filtrar por um produto, marca ou família específica antes de mudar a data, ou rode em horário de menor uso.

**O painel `Similar` não aparece. O produto deveria ter similar.**
A aba só fica visível quando o produto selecionado **tem** Similares cadastrados em `Cadastro de Produtos` (código `32`). Confira no cadastro do produto se a aba de Similares está preenchida.

**Posso editar valores aqui?**
Não. Esta é uma tela **de consulta**. Para ajustar saldo manualmente, use o `Ajuste de Estoque` (código `79`). Para corrigir o cadastro do produto (custo, preço), use `Cadastro de Produtos` (código `32`).

**Onde aparece a localização física do produto?**
Ao clicar em uma linha do grid, o painel lateral `Localização de Estoque` carrega a posição cadastrada (corredor / prateleira / posição). Quem cadastra essas posições é a tela `Localização de Estoque` (código `29`).

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Como se relaciona |
|------|---------------|--------------------|
| `Locais de Estoque` | `28` | Define os locais que aparecem no filtro `Local de Estoque`. |
| `Localização de Estoque` | `29` | Posição física (corredor / prateleira) mostrada no painel lateral. |
| `Situação de Estoque` | `30` | Define as camadas que aparecem no filtro `Situação do Estoque`. |
| `Cadastro de Produtos` | `32` | Item de catálogo cujo saldo é consultado; o atalho `Ir para Produto` abre direto a partir do grid. |
| `Transações de Estoque` | `33` | Configura o efeito que cada movimento causa nas camadas — a origem do saldo que esta tela exibe. |
| `Tipos de Movimento` | `37` | Junta o Tipo de Movimento à Transação de Estoque; é onde se corrigem comportamentos quando o saldo aparece errado. |
| `Movimentos` | `53` | Onde os movimentos que geram o saldo são lançados. |
| `Ajuste de Estoque` | `79` | Tela para corrigir saldos manualmente quando há divergência. |
| `Histórico de Movimentações` | `205` | Lista os movimentos individuais que produziram o saldo atual. |
| `Histórico de Produtos` | `206` | Detalha o histórico de operações por produto. |

---

## ⚠️ Limites desta documentação

- Não detalha a montagem de **modelos de relatório** acionados pelo `F3` — esse é um tema de Report Builder, fora do escopo desta tela.
- Não cobre **divergências fiscais** ou regras de cálculo de custo médio — essas vivem no guia "Atualização de Custo Automática".
- A configuração de campos do grid (quais colunas aparecem, em que ordem) é por usuário e não está documentada aqui.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de Suporte / Operação de Estoque / Administradores Sol.NET
