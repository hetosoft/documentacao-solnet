# 📄 Cadastro de Tabela de Preços - Sol.NET

## 🎯 Visão Geral

A **Tabela de Preço** é o **principal mecanismo de precificação** do Sol.NET. Cada tabela define uma **regra de preço** — quanto cobrar de um determinado conjunto de produtos, para um determinado conjunto de pessoas (clientes), em uma ou mais empresas — combinando:

- um **valor de partida** (a Base de Cálculo — pode ser Preço Base, Custo de Venda, Custo Médio, ou outra tabela),
- um **percentual de acréscimo ou desconto** geral à vista (e outro a prazo, se a operação for parcelada),
- listas de **inclusão por Produto** (individual, marca, fabricante, fornecedor, família, grupo, sub-grupo),
- listas de **inclusão por Pessoa** (cliente individual, status, tipo, ramo, região),
- regras de **valor mínimo de venda** e de **troca automática** de tabela ao atingir um valor.

Na hora de uma venda, o Sol.NET combina os filtros do movimento (empresa, cliente, produto, à vista × a prazo) com todas as tabelas elegíveis e aplica a regra correspondente. As Tabelas de Preço também controlam **onde o preço aparece** — PDV, mobile, e-commerce, etiqueta, carga para balança — pelo painel `Configurações`.

> ℹ️ **Como o preço é decidido na venda.** Quando há mais de uma tabela elegível, o Sol.NET tem regras de prioridade (granularidade — produto individual ganha de grupo, que ganha de família, que ganha de "todos os produtos") e regras de fallback (buscar `Preço Venda 1` se o preço base está zerado; cair na `Base de Cálculo` se nenhuma tabela for elegível). Os detalhes estão no guia cross-tela "Preço de Venda" e em "Tabela de Preço — Fallback".

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Tabela de Preços |
| **Código (`F1`)** | `27` |

Abra a pesquisa universal (atalho `F1`) e digite **`27`** ou parte do nome **`Tabela de Preço`**.

---

## 🧭 Sub-abas do formulário

O formulário tem **cinco sub-abas principais**. Cada tabela é uma combinação válida das cinco — o sistema valida no `Gravar` que pelo menos um critério em **Produtos** e um em **Pessoas** estejam definidos, e que pelo menos uma **Empresa** esteja marcada.

| Aba | Para quê serve |
|------|----------------|
| **Empresas** | Em quais empresas (lojas) esta tabela vale. Multi-seleção. |
| **Produtos** | Filtros de produto — define para **quais** SKUs / categorias a regra se aplica. Sub-abas internas: `Individual`, `Fabricante/Fornecedor`, `Marca/Fabricante`, `Família/Grupo/Sub Grupo`, `Marca/Grupos`. |
| **Pessoas** | Filtros de pessoa — define para **quem** a regra se aplica. Sub-abas: `Pessoas` (individual), `Status`, `Tipo Cliente/Fornecedor`, `Ramo de Atividade`, `Região`. |
| **Valores** | Regras de valor mínimo, troca automática de tabela e fallback. |
| **Configurações** | Onde a tabela é exibida (Carga / PDV / Promoção / Integração / Etiquetas). |

---

## 📝 Campos do cabeçalho

O cabeçalho fica visível em todas as sub-abas.

| Campo | Para quê serve |
|-------|----------------|
| **Descrição** | Nome livre da tabela (até 80 caracteres). Use algo descritivo: `VAREJO LOJA`, `ATACADO 10%`, `PROMOCIONAL CARTÃO`. |
| **Código** | Código identificador curto da tabela (até 10 caracteres). |
| **% Acrésc/Desc** | Percentual padrão aplicado à Base de Cálculo. Positivo = acréscimo (preço sobe), negativo = desconto (preço cai). Exemplo: `-10` aplica 10 % de desconto sobre a base. |
| **% A Prazo** | Percentual alternativo aplicado quando a venda é **a prazo** (parcelada). Permite cobrar mais a prazo do que à vista. |
| **Base de Cálculo** | A partir de quê o preço é calculado. O combo carrega as tabelas-base cadastradas no sistema (entre as comuns: `CUSTO INICIAL`, `CUSTO DE VENDA`, `CUSTO MÉDIO INICIAL`, `CUSTO MÉDIO UNITÁRIO`, `CUSTO MÉDIO UNITÁRIO POR EMPRESA`) **ou** outra Tabela de Preço cadastrada — permitindo o encadeamento (esta tabela é calculada em cima do resultado da outra). A lista completa varia conforme as tabelas cadastradas e aparece direto no combo. |
| **Comissão A Vista (%)** | Percentual de comissão para vendedores quando a venda usa esta tabela à vista. |
| **Comissão A Prazo (%)** | Idem para a prazo. |
| **Tipo Venda** | Classifica a tabela (Varejo / Atacado / Promoção etc.). Filtra na escolha no PDV. |
| **A Vista / A Prazo** | Define se a tabela diferencia preço à vista de preço a prazo (quando ligada, os campos `% A Prazo` e `Vl Fixo A Prazo` ficam ativos). |
| **Mobile** | Indica se a tabela é levada para dispositivos móveis (força de vendas, coletor). |
| **Inativo** | Quando marcado, a tabela deixa de ser elegível para novas vendas. |

> 💡 **Encadeamento.** Quando a Base de Cálculo aponta para **outra Tabela de Preço**, o cálculo é feito *em cima do resultado* daquela tabela — útil para criar variações ("Atacado = Varejo - 8 %"). A tela impede que uma tabela aponte para ela mesma (regra `cbxTabelaPreco ≠ ID atual`).

---

## 🏢 Aba `Empresas`

Lista as empresas onde a tabela vale. **Pelo menos uma** precisa estar marcada — caso contrário, ao gravar o sistema mostra *"Escolha uma Empresa!"* e direciona o foco para esta aba.

A multi-seleção pode usar `Selecionar Todos` ou `Desmarcar Todos` quando a tabela for global.

---

## 📦 Aba `Produtos`

Define o **escopo de produtos** afetados. Pelo menos um critério precisa estar definido, ou um dos checkboxes `Todos os Produtos` / `Todos os Serviços` precisa estar marcado.

### Sub-aba `Individual`

Produto a produto. Para cada linha:

| Campo | O que faz |
|-------|-----------|
| **Descrição** (Produto) | Dois cliques abrem a pesquisa de produtos. |
| **% Acrésc/Desc** | Percentual específico aplicado a este produto, em vez do percentual padrão do cabeçalho. |
| **Valor Fixo** | Preço fixo para este produto (substitui o cálculo Base × %). Não pode ser usado junto com `% Acrésc/Desc` na mesma linha — *"Não permitido valor em Porcentagem e Valor fixo!"*. |
| **% A Prazo** / **Vl. Fixo A Prazo** | Versões a prazo de cada um. |

Botões: **Inserir**, **Atualizar**, **Deletar**, **Cancelar**, **Filtrar** (busca dentro da lista), **Limpar Filtro**, **Deletar Todos**.

### Sub-aba `Fabricante/Fornecedor`

Aplica a regra a produtos de um determinado **fabricante** ou **fornecedor**. Mesmos campos de `% Acrésc/Desc`, `% A Prazo` e botões da sub-aba Individual.

### Sub-aba `Marca/Fabricante`

Filtro por **marca**.

### Sub-aba `Família/Grupo/Sub Grupo`

Filtro por hierarquia de catálogo. Permite combinar:
- Apenas Família
- Família + Grupo
- Família + Grupo + Sub Grupo

### Sub-aba `Marca/Grupos`

Combina Família/Grupo/Sub Grupo **com** uma Marca/Fabricante — filtros mais finos para regras híbridas.

### Checkboxes `Todos os Produtos` / `Todos os Serviços`

Ligados, dispensam a inclusão linha a linha — a tabela passa a valer para todos os produtos (ou serviços) **sem** estar em nenhuma das listas acima.

---

## 👥 Aba `Pessoas`

Define **para quem** a tabela vale. Pelo menos um critério em uma das sub-abas, ou o checkbox `Todas as Pessoas` marcado.

| Sub-aba | Filtra por |
|---------|-----------|
| **Pessoas** | Cliente / Fornecedor individual (lista de IDs específicos). |
| **Status** | Status do cliente (Ativo, VIP, Inadimplente etc. — conforme cadastro). |
| **Tipo Cliente/Fornecedor** | Tipo do cadastro (Cliente, Fornecedor, Funcionário etc.). |
| **Ramo de Atividade** | Ramo do cliente PJ. |
| **Região** | Região cadastrada para o cliente. |

Cada sub-aba aceita `% Acrésc/Desc` próprio (sobrepõe o do cabeçalho) e versão a prazo, mesma estrutura de inserir/atualizar/deletar/cancelar.

---

## 💰 Aba `Valores`

Regras adicionais de preço.

| Campo | Para quê serve |
|-------|----------------|
| **Valor Mínimo — Venda** | Preço mínimo que cada item pode atingir. O Sol.NET impede que a aplicação de descontos manuais ou regras automáticas leve o preço abaixo desse mínimo. |
| **Se alcançar o valor, perguntar se deseja trocar a tabela de preço — Valor** | Quando o **subtotal** da venda atinge este valor, o sistema **pergunta** se quer trocar a tabela aplicada por outra (definida abaixo). Mecanismo de "atingiu R$ X, libera tabela de atacado". |
| **Tabela de Preço — Mudar** | A tabela para a qual o Sol.NET sugere trocar. Validações: não pode ser a **própria** tabela; se a tabela estiver preenchida, o `Valor` precisa ser > 0; se o `Valor` estiver preenchido, a tabela precisa ser escolhida. |
| **Extra — Buscar Preço Venda1 se Preço Base Zerado(0)** | Fallback: quando o produto tem preço base zerado, busca o `Preço Venda 1` em vez de aplicar o cálculo (evita preço 0 acidental). |
| **Extra — Buscar Preço Base Cálculo se Tabela de Preço inelegível** | Quando esta tabela não se aplica a um produto/pessoa específico, em vez de barrar a venda, o sistema cai no preço da Base de Cálculo (preço base, custo de venda etc.). |

---

## ⚙️ Aba `Configurações` — Mostrar em

Define **onde** a tabela aparece para escolha do operador. Quatro checkboxes:

| Onde | O que controla |
|------|----------------|
| **Carga (Balança / Busca Preço / Coletor de Dados)** | Inclui a tabela nas cargas enviadas para balança, terminal de consulta de preço e coletores. |
| **Empresas / PDV** | Inclui a tabela como opção no PDV das empresas marcadas. |
| **Promoção** | Habilita o uso desta tabela como tabela promocional (Agenda de Promoções). |
| **Integração (Web / Mobile / E-commerce)** | Inclui a tabela nos pacotes enviados para integrações externas. |
| **Impressão Etiquetas** | Inclui a tabela no rol de tabelas que geram etiqueta de prateleira. |

> 💡 **Por que não marcar tudo.** Diferenciar onde a tabela aparece evita poluição de combos no PDV / coletor e impede que regras internas vazem para integrações externas (e-commerce, marketplace).

---

## ✅ Validações automáticas ao salvar

| Quando você grava | O sistema verifica |
|-------------------|--------------------|
| Sempre | A `Descrição` é **única** — duplicar é bloqueado. |
| Sempre | O `Código` é **único** — duplicar é bloqueado. |
| Sempre | A `Base de Cálculo` é obrigatória. |
| Sempre | Pelo menos uma **Empresa** está marcada na aba `Empresas`. |
| Sempre | Pelo menos **uma regra em Produtos** existe (linha em alguma sub-aba **ou** `Todos os Produtos` / `Todos os Serviços` marcado). |
| Sempre | Pelo menos **uma regra em Pessoas** existe (linha em alguma sub-aba **ou** `Todas as Pessoas` marcado). |
| Aba `Valores` | A `Tabela de Preço — Mudar` não pode ser a **própria** tabela. |
| Aba `Valores` | Se a `Tabela de Preço — Mudar` está preenchida, o `Valor` precisa ser > 0. |
| Aba `Valores` | Se o `Valor` está preenchido, a `Tabela de Preço — Mudar` precisa ser escolhida (não dá para deixar valor sem destino). |
| Linha de produto | Não pode haver `% Acrésc/Desc` **e** `Valor Fixo` preenchidos na mesma linha. |
| Em clonagem | Pede confirmação antes de clonar. |

---

## 🚫 Exclusão

A exclusão é bloqueada quando a tabela já foi referenciada:

- ❌ **Há movimento que usou a tabela** — *"Não permitido, Existe Movimento com esta Tabela de Preço!"*. Resolva inativando a tabela (marcando `Inativo`) em vez de excluir.
- ❌ **Há Agenda de Promoção que usa a tabela** — *"Não permitido, Existe Agenda de Promoção com esta Tabela de Preço!"*. Remova a tabela das promoções ativas antes de excluir, ou inative.

> ⚠️ **Boa prática.** Tabelas que já foram usadas em vendas históricas **devem permanecer cadastradas** (mesmo inativadas), porque os relatórios e o `Histórico de Movimentações` continuam referenciando a tabela original para auditoria de preço.

---

## 📋 Clonar tabela

Use o item **Clonar Registros** no menu de contexto da grid de busca para gerar uma cópia de uma tabela existente. O sistema pede confirmação e abre a cópia em modo de edição — ajuste descrição, código e o que precisar antes de gravar.

> 💡 **Caso típico.** Clonar é o caminho rápido para criar uma **variação** (`VAREJO PROMO BLACK FRIDAY` a partir de `VAREJO`), uma **réplica multi-loja** (mesma regra para outra empresa), ou um **espelho a prazo** (mudando só os percentuais).

---

## 💡 Exemplos práticos

### Exemplo 1 — Tabela de varejo com 30 % de margem sobre o custo

1. Pesquisa `F1` → `27` → abre `Cadastro de Tabela de Preços`.
2. Clique em **Novo**.
3. Cabeçalho:
   - `Descrição`: `VAREJO 30%`.
   - `Código`: `VAR30`.
   - `% Acrésc/Desc`: `30`.
   - `Base de Cálculo`: `CUSTO DE VENDA`.
4. Aba **Empresas** → marque as lojas que usam essa tabela.
5. Aba **Produtos** → marque `Todos os Produtos`.
6. Aba **Pessoas** → marque `Todas as Pessoas`.
7. Aba **Configurações** → marque `Empresas / PDV`, `Impressão Etiquetas` e o que mais fizer sentido.
8. **Gravar**.

### Exemplo 2 — Tabela de atacado: 10 % de desconto sobre o varejo, mas só para clientes PJ

1. Pesquisa `F1` → `27` → **Novo**.
2. Cabeçalho:
   - `Descrição`: `ATACADO PJ`.
   - `% Acrésc/Desc`: `-10`.
   - `Base de Cálculo`: a tabela `VAREJO 30%` cadastrada antes (encadeamento).
3. Aba **Empresas** → mesmas lojas do varejo.
4. Aba **Produtos** → marque `Todos os Produtos`.
5. Aba **Pessoas** → sub-aba `Tipo Cliente/Fornecedor` → **Inserir** → escolha `PJ` (ou o tipo cadastrado) → `% Acrésc/Desc` 0 → **Atualizar**.
6. **Gravar**.

Resultado: o preço de atacado é calculado em cima do varejo (que já calculou 30 % sobre o custo), descontando 10 %. Só clientes do tipo PJ acessam.

### Exemplo 3 — Troca automática de tabela ao atingir valor

Cenário: na loja, qualquer venda que ultrapasse R$ 1.000 deve usar `ATACADO PJ` em vez de `VAREJO 30%`.

1. Pesquisa `F1` → `27` → abra `VAREJO 30%` → **Alterar**.
2. Aba **Valores** → em `Se alcançar o valor, perguntar se deseja trocar a tabela de preço`:
   - `Valor`: `1000`.
   - `Tabela de Preço — Mudar`: `ATACADO PJ`.
3. **Gravar**.

Quando o operador lança uma venda que cruza os R$ 1.000, o sistema **pergunta** se deseja trocar — se o operador aceita, refaz os preços dos itens já lançados pela tabela ATACADO PJ.

### Exemplo 4 — Tabela promocional só para uma família de produtos

1. Pesquisa `F1` → `27` → **Novo**.
2. Cabeçalho:
   - `Descrição`: `PROMO REFRIGERANTES`.
   - `% Acrésc/Desc`: `-15`.
   - `Base de Cálculo`: `VAREJO 30%` (encadeada).
3. Aba **Empresas** → marque as lojas.
4. Aba **Produtos** → sub-aba `Família/Grupo/Sub Grupo` → **Inserir** → escolha a `Família` = `BEBIDAS`, `Grupo` = `REFRIGERANTES` → **Atualizar**.
5. Aba **Pessoas** → `Todas as Pessoas`.
6. Aba **Configurações** → marque `Empresas / PDV` e `Promoção`.
7. **Gravar**.

A promoção fica disponível para escolha no PDV e na Agenda de Promoções, sem afetar produtos fora do filtro.

### Exemplo 5 — Clonar a tabela de uma loja para outra

1. Na grid de busca, localize `VAREJO 30%` → clique-direito → **Clonar Registros** → confirme.
2. A cópia abre em modo de inclusão.
3. Cabeçalho: ajuste `Descrição` (ex.: `VAREJO 30% — FILIAL 2`) e `Código`.
4. Aba **Empresas** → desmarque a loja original e marque a nova.
5. **Gravar**.

---

## ❓ FAQ / Problemas comuns

**Cadastrei a tabela mas o preço no PDV não saiu o esperado.**
Confira nesta ordem: (1) a aba `Configurações` tem `Empresas / PDV` marcado? (2) a aba `Empresas` inclui a loja onde a venda está sendo feita? (3) o produto e o cliente da venda batem com os critérios de `Produtos` e `Pessoas`? (4) há **outra** tabela mais específica elegível e prevalecendo sobre a sua? (5) o cliente tem regra individual em `Pessoas` que desempata? Use o `Histórico de Movimentações` (código `205`) → aba `Tabela de Preço` para ver qual tabela foi efetivamente aplicada.

**Recebi "Obrigatório ter pelo menos uma(1) regra em Produtos!" ao gravar.**
Você criou a tabela sem definir o escopo de produtos. Vá na aba **Produtos** e escolha entre: marcar `Todos os Produtos` / `Todos os Serviços` ou adicionar pelo menos uma linha em qualquer sub-aba (Individual, Marca, Família etc.).

**A tabela aparece duas vezes no combo do PDV.**
Você provavelmente clonou e esqueceu de inativar a original. Inative a versão antiga marcando `Inativo` no cabeçalho — ela some das telas operacionais mas o histórico continua referenciando.

**Quero proibir um produto de receber qualquer desconto.**
Não é configuração desta tela isoladamente — o produto tem um `Valor Mínimo de Venda` no próprio `Cadastro de Produtos` (código `32`) que serve de piso, e a aba `Valores` desta tabela também define um piso por tabela. Use os dois em conjunto.

**Posso aplicar tabela diferente por canal (PDV × E-commerce × Mobile)?**
Sim — use a aba `Configurações` para liberar uma tabela só para o canal desejado. A integração com e-commerce / mobile só recebe as tabelas que tiverem `Integração` marcado; o coletor de balança só pega as que tiverem `Carga`.

**A regra com `Tabela de Preço — Mudar` está em loop.**
A validação impede que a tabela aponte para ela mesma, mas é possível criar **ciclo entre duas tabelas** (A → B, B → A). O Sol.NET aplica a troca apenas **uma vez** por venda quando o operador aceita — não há loop em runtime. Mesmo assim, é boa prática evitar ciclos por clareza.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Como se relaciona |
|------|---------------|--------------------|
| `Cadastro de Produtos` | `32` | Origem dos produtos referenciados. O preço base e o preço de venda 1 vêm do cadastro. |
| `Cadastro de Pessoas` | `1` | Origem dos clientes/fornecedores listados na aba `Pessoas`. |
| `Tipos de Movimento` | `37` | Define quais tabelas estão **habilitadas** para cada tipo de operação (sub-aba `Tabela de Preço` do Tipo de Movimento). |
| `Movimentos de Compras` | `201` | Onde a tabela aparece em movimentos de compra. |
| `Movimentos de Vendas` | `202` | Onde a tabela é efetivamente aplicada na venda. |
| `Outros Movimentos` | `203` | Mesma tabela em operações fora de compra/venda (ajuste, transferência, etc.). |
| `Histórico de Movimentações` | `205` | Tem aba `Tabela de Preço` que mostra qual tabela foi usada em cada movimento. |
| `Cadastro de Empresas` | — | Origem das empresas marcadas na aba `Empresas`. |

---

## ⚠️ Limites desta documentação

- Não cobre a **prioridade** entre tabelas concorrentes (quando duas tabelas se aplicam à mesma venda) — esse comportamento é detalhado em "Preço de Venda — Guia" e "Tabela de Preço — Fallback".
- Não detalha a **Agenda de Promoções** (data de início/fim, prioridade promocional) — apenas indica que tabelas com `Promoção` marcado em `Configurações` ficam aptas a entrar na agenda.
- O cálculo de **comissão** depende de configurações do Cargo do vendedor e do Tipo de Comissão da empresa — esta tela apenas oferece os percentuais base.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de Suporte / Comercial / Administradores Sol.NET
