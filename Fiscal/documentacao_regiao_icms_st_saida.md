# 📄 Cadastro de Região ICMS ST Saída — Sol.NET

## 🎯 Visão Geral

O **Cadastro de Região ICMS ST Saída** (`94`) define as regras que o Sol.NET usa para calcular o **ICMS por Substituição Tributária (ICMS-ST)** em cada item da operação. A tela funciona como um conjunto de **filtros + percentuais**: quando o contexto da operação combina com uma linha (loja emissora, UF do destinatário, perfil do destinatário, etc.), o sistema aplica a `Base de cálculo ST`, a `MVA` (Margem de Valor Agregado) e a `Alíquota ICMS-ST` definidas naquela linha.

Diferente do Cadastro de Região ICMS Saída (`93`), que mapeia contexto → Natureza de Operação, a `Região ICMS ST` **armazena diretamente os percentuais** que entram na conta do ICMS-ST.

### Principais características

- ✅ Define **Base ST, MVA e Alíquota ICMS-ST** para cada cenário fiscal
- ✅ Permite múltiplas **linhas de detalhe** filtradas por loja, UF, CNAE, indicador de IE, atividade comercial e regime tributário do destinatário
- ✅ Modo `Usar MVA NCM` — ignora a MVA da linha e usa a registrada no NCM do item
- ✅ Funciona em dois modos de associação: por **Produto** (vinculada ao item) ou por **Pessoa** (vinculada ao destinatário)
- ✅ Bloqueia a exclusão se houver produtos vinculados a ela (somente para Tipo `PRODUTO`)

---

## 🚪 Como acessar

Abra a pesquisa universal (`F1`), digite `Região ICMS ST Saída` ou o código `94`, e abra a tela.

---

## 🧩 O que define uma Região ICMS-ST

O cabeçalho identifica a regra como um todo e decide **como ela será vinculada** aos movimentos.

| Campo | O que define |
|---|---|
| **Tipo** | Como a Região é encontrada durante a emissão: `PRODUTO` (vinculada ao cadastro do produto) ou `PESSOA` (vinculada ao cadastro do destinatário). |
| **Descrição** | Texto livre, obrigatório, até 80 caracteres. **Pode repetir** entre regiões de Tipos diferentes — ex.: pode existir uma `INDÚSTRIA SP` do tipo `PRODUTO` e outra `INDÚSTRIA SP` do tipo `PESSOA`. |

### Como cada Tipo é aplicado no movimento

- **`PRODUTO`** — a Região é apontada pelo cadastro do produto. Durante o movimento, o sistema lê a Região vinculada ao item, escolhe a linha cujos filtros casam com o contexto da operação e aplica os percentuais.
- **`PESSOA`** — a Região é apontada pelo cadastro da pessoa (cliente). O sistema usa a Região do destinatário do movimento, independentemente do produto.

> 💡 As duas formas convivem. O cliente pode preferir uma ou outra dependendo de como o cálculo do ICMS-ST varia mais — pela natureza do item ou pelo perfil de quem compra.

---

## 📋 Linhas de configuração

A área `Configurações` é um **sub-cadastro** com seus próprios botões `Inserir`, `Atualizar`, `Deletar` e `Cancelar`. Cada linha define um conjunto de filtros e os percentuais que serão usados quando aquele conjunto for atendido.

### Filtros — quando a linha se aplica

Os filtros são **curingas**: deixar vazio ou em `-1` significa "qualquer valor". O sistema escolhe a linha mais específica que combina com o contexto.

| Campo | O que filtra |
|---|---|
| **Nº Lojas** | Códigos de filial emissora separados por `/`, ex.: `/1/2/`. Vazio = todas as lojas. O sistema adiciona as barras automaticamente ao sair do campo. |
| **Sigla Estados** | UFs do destinatário separadas por `/`, ex.: `/BA/SP/`. Vazio = todas. As barras são acrescentadas automaticamente. |
| **CNAE - Fiscal** | CNAE do destinatário. Duplo clique ou tecla de busca abre a tela `Cadastro de CNAE`. O botão de lixeira (esquerdo) limpa o campo. |
| **Indicador IE** | Indicador de Inscrição Estadual do destinatário, conforme padrão SEFAZ: `1 — Contribuinte`, `2 — Isento`, `9 — Não Contribuinte`. Vazio/`-1` = qualquer. |
| **Atividade Comercial** | `Consumidor`, `Revenda` ou `Indústria`. Vazio/`-1` = qualquer. |
| **Regime Tributário** | Regime do destinatário: `Simples Nacional`, `Lucro Real` ou `Lucro Presumido`. Vazio/`-1` = qualquer. |
| **Cálculo** | Modo de cálculo do ICMS-ST. Veja `🧮 Modos de cálculo` abaixo. |
| **Tipo** (radio) | `Saída` ou `Entrada`. Define se a linha vale para operações que saem do estoque ou que entram. |
| **Selecione** (radio) | Onde a operação acontece: `Dentro do Estado`, `Fora do Estado` ou `Exterior`. |

### Percentuais — o que a linha aplica

| Campo | O que faz |
|---|---|
| **B.C. ICMS ST** | Percentual de **redução da base de cálculo** do ICMS-ST. Ex.: `100,00%` = sem redução; `60,00%` = aplicar sobre 60% da base. |
| **MVA** | Margem de Valor Agregado (%) usada para compor a base de cálculo do ICMS-ST. No modo de cálculo `Industria MT`, este mesmo campo é usado como **Margem de Lucro**. |
| **ICMS ST Aliq.** | Alíquota do ICMS-ST (%). No modo de cálculo `Industria MT`, este mesmo campo armazena a **Carga Média**. |
| **Usar MVA NCM** | Quando marcado, o sistema **ignora a MVA digitada na linha** e usa a MVA cadastrada no NCM do item. Útil quando a MVA varia produto a produto e já está mantida no NCM. |

---

## 🧮 Modos de cálculo

O combo `Cálculo` define como os percentuais da linha entram na conta do ICMS-ST.

| Modo | Quando usar |
|---|---|
| **Normal** | Cálculo padrão de ICMS-ST: base × MVA → aplicar redução de base (`B.C. ICMS ST`) → aplicar `ICMS ST Aliq.`. É o modo da maioria dos cenários. |
| **Industria MT** | Cálculo específico para clientes do tipo **indústria estabelecida em Mato Grosso**. Nesse modo, o campo `MVA` representa a **Margem de Lucro** e o campo `ICMS ST Aliq.` representa a **Carga Média**. A regra exata do cálculo varia conforme o regime estadual e deve ser confirmada com a contabilidade do cliente. |

---

## 🚫 Regras e restrições

### Exclusão bloqueada quando há produtos vinculados

Se o Tipo da Região é `PRODUTO` e houver pelo menos um produto apontando para ela, a tela impede a exclusão e exibe:

> *Não permitido, Existe Produto(s) com essa Região!*

Para excluir, é preciso primeiro desvincular ou trocar a Região nesses produtos. Para Tipo `PESSOA` não há essa checagem na exclusão — o usuário é responsável por manter o vínculo nas pessoas que apontavam para a Região excluída.

### Descrição pode duplicar

A tela **não valida unicidade da Descrição**. Duas regiões com o mesmo texto são permitidas, normalmente para combinar com a separação por Tipo (`PRODUTO` × `PESSOA`).

### Normalização de listas

Ao sair dos campos `Nº Lojas` e `Sigla Estados`, o Sol.NET insere automaticamente `/` no início e no final do conteúdo digitado. Ou seja, digitar `1,2` resulta em `/1,2/`, e digitar `BA/SP` resulta em `/BA/SP/`. Use **um item por par de barras** (`/1/2/`, `/BA/SP/`) para que o casamento de filtro funcione.

### Edição de detalhe em andamento

Se há uma linha de detalhe sendo inserida ou alterada (`Inserir` ou edição em curso) e o operador tenta sair da área `Configurações` sem confirmar, o sistema bloqueia a saída com a mensagem padrão de cadastro em edição e devolve o foco para o primeiro campo. Use **Atualizar** para gravar ou **Cancelar** para descartar antes de mudar de seção.

---

## 💡 Exemplos Práticos

### Exemplo 1 — Venda para revenda em SP, alíquota fixa

A loja `1` vende para revendedores no estado de SP, contribuintes de ICMS, regime Lucro Presumido. A MVA pactuada com o estado é 35%, sem redução de base, alíquota efetiva 18%.

| Campo | Valor |
|---|---|
| Tipo | `PRODUTO` |
| Descrição | `REVENDA SP — MVA 35%` |
| **Linha de detalhe** | |
| Nº Lojas | `/1/` |
| Sigla Estados | `/SP/` |
| Indicador IE | `Contribuinte` |
| Atividade Comercial | `Revenda` |
| Regime Tributário | `Lucro Presumido` |
| Cálculo | `Normal` |
| Tipo | `Saída` |
| Selecione | `Fora do Estado` |
| B.C. ICMS ST | `100,00%` |
| MVA | `35,00%` |
| ICMS ST Aliq. | `18,00%` |

Depois de salvar, vincule esta Região nos cadastros dos produtos que devem usar essa regra.

### Exemplo 2 — Mesmo cenário, mas com MVA variável por produto

Se a MVA muda produto a produto (e já está mantida nos cadastros de NCM), repita a configuração acima e marque **`Usar MVA NCM`** na linha. O percentual `MVA` da linha vira informativo — quem manda no cálculo é a MVA do NCM do item.

### Exemplo 3 — Regra pelo perfil do cliente (não pelo produto)

Um cliente atacadista compra produtos diversos, mas a regra de ICMS-ST que se aplica a ele é sempre a mesma. Em vez de configurar produto a produto:

1. Cadastre uma Região com Tipo `PESSOA` e descrição `ATACADO — REGRA ÚNICA`.
2. Configure as linhas de detalhe normalmente.
3. Aponte essa Região no cadastro do atacadista.

Em qualquer movimento desse cliente, o Sol.NET usa essa Região, independentemente do produto.

---

## ❓ FAQ / Problemas Comuns

### ❓ Posso ter duas Regiões com a mesma Descrição?

Sim. A tela não bloqueia duplicidade de Descrição. O uso mais comum é ter uma `PRODUTO` e uma `PESSOA` com o mesmo nome para cobrir os dois modos de associação.

### ❓ Qual a diferença para a tela Região ICMS Saída (`93`)?

A `93` é um **mapa de Natureza de Operação** — ela diz qual Natureza usar em cada contexto, e os valores fiscais vêm da Natureza. A `94` armazena diretamente os **percentuais de ICMS-ST** (Base, MVA, Alíquota) e os aplica em quem combina com os filtros. As duas convivem: a `93` cuida do ICMS normal/CFOP/CST; a `94` cuida especificamente do ICMS-ST.

### ❓ Marquei `Usar MVA NCM`, mas o sistema ainda usa a MVA da linha. Por quê?

Confirme que o NCM do item realmente tem MVA cadastrada. Se o NCM estiver com MVA em branco, o cálculo pode cair de volta no valor da linha. Verifique também se o produto está apontando para o NCM correto.

### ❓ Por que o combo `Cálculo` mostra um item em branco no final?

É um item descontinuado que sobrou no cadastro. Use somente `Normal` ou `Industria MT`.

### ❓ Quando devo usar `Industria MT`?

Quando o cliente é uma **indústria estabelecida no estado de Mato Grosso**, sujeita ao regime estadual específico que troca MVA por Margem de Lucro e alíquota por Carga Média. A fórmula exata depende da legislação estadual vigente e deve ser confirmada com a contabilidade. Para os demais cenários, use `Normal`.

### ❓ Tentei excluir uma Região e o sistema avisou "Existe Produto(s) com essa Região". O que fazer?

A Região está vinculada a um ou mais produtos. Abra o cadastro de produtos, localize os que apontam para essa Região e troque pela Região correta (ou deixe em branco). Depois disso a exclusão será liberada.

### ❓ Posso usar tanto Região `PRODUTO` quanto Região `PESSOA` no mesmo movimento?

Não simultaneamente para o mesmo item. O sistema usa a Região vinculada ao cadastro que dá origem ao cálculo (produto ou pessoa). A escolha entre os dois modos é definida no momento do cadastro da Região e do vínculo.

### ❓ Como faço para uma linha valer para qualquer estado?

Deixe `Sigla Estados` em branco. O mesmo vale para `Nº Lojas` (qualquer loja), `Indicador IE`, `Atividade Comercial`, `Regime Tributário` e `CNAE` — vazio significa "qualquer valor".

### ❓ Mudei os percentuais e o movimento já emitido continua com o valor antigo. É bug?

Não. O Sol.NET calcula o ICMS-ST no momento da emissão usando os percentuais válidos naquele instante. Movimentos já gravados mantêm os valores históricos. Para reprocessar, o movimento precisa ser refeito.

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Equipe de Suporte / Usuários do Sol.NET / Contabilidade
