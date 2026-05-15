# 📄 Cadastro de NCM — Sol.NET

## 🎯 Visão Geral

O **NCM (Nomenclatura Comum do Mercosul)** é o código que classifica cada mercadoria comercializada pela empresa. No Sol.NET, o **Cadastro de NCM** é onde você define **como o sistema deve tributar cada NCM** — ICMS, ICMS-ST, FCP, PIS/COFINS, IPI e, com a Reforma Tributária, também CBS e IBS.

Existem **duas telas** que tratam de NCM e é importante não confundir:

- **Cadastro de NCM** (código `21`) — sua **lista local**: os NCMs que a empresa de fato usa, já com toda a parametrização tributária preenchida pelo configurador. É o NCM que o cadastro de Produtos aponta.
- **Cadastro Tabela NCM** (código `121`) — a **base federal**: a tabela oficial publicada pela Receita, atualizada periodicamente. Funciona como **fonte de consulta** e alimenta automaticamente a descrição/tipo quando você adiciona um NCM novo no cadastro `21`.

### Principais características

- ✅ Concentra toda a regra tributária associada ao código NCM
- ✅ Cobre **três blocos de impostos**: ICMS / ICMS-ST / FCP, Tributação Federal (PIS, COFINS, IPI) e Reforma Tributária (CBS, IBS)
- ✅ Permite registrar se um NCM foi **rejeitado pela SEFAZ** e ler o retorno da NF-e/NFC-e
- ✅ Pode ser atualizado a partir da Tabela NCM oficial sem perder a parametrização local

---

## 🔧 Como acessar

Abra a pesquisa universal (`F1`), digite `NCM` ou o código `21`, e abra a tela.

Para a base federal, abra `Cadastro Tabela NCM` (código `121`) da mesma forma.

---

## 📋 Cabeçalho do cadastro

Ao incluir ou editar um NCM, os campos do topo são os de identificação. Eles aparecem acima das abas e valem para o registro inteiro.

| Campo | O que é | Observações |
|---|---|---|
| **NCM** | Código numérico, até 8 dígitos | Chave fiscal — abre a pesquisa da Tabela NCM federal (`121`) com duplo clique |
| **EX** | Código de exceção do NCM (até 3 dígitos numéricos) | Usado quando o NCM tem desdobramento por finalidade |
| **CNI - Código Não Incidência** | Até 3 dígitos numéricos | Aplicado em produtos com tributação zerada, monofásica ou suspensão — **preenchido manualmente pelo configurador** |
| **Descrição NCM** | Texto descritivo do código | Preenchido automaticamente ao puxar da Tabela NCM (`121`) |
| **Tipo** | Produto ou Serviço (campo somente leitura) | Preenchido automaticamente ao carregar o NCM da Tabela NCM |
| **Tributação Federal** | Combo que aponta para um perfil de PIS/COFINS/IPI já cadastrado | Ao selecionar, o sistema **copia** os valores do perfil (CST PIS/COFINS Entrada/Saída/Entrada Dev., Alíq. PIS/COFINS interna e externa, CST IPI, Alíq. IPI) para os campos correspondentes da aba `Principal`. Limpar o combo **zera** esses campos. |
| **Região Tributária ICMS ST** | Combo que aponta para uma `Região ICMS ST` (código `94`) | Define a regra de Substituição Tributária aplicada nas saídas |

### Caixa `SEFAZ REJEITOU`

Identifica um NCM que a SEFAZ rejeitou na transmissão de NF-e/NFC-e:

- **NCM Inválido** — checkbox preenchido **automaticamente pelo sistema** quando a SEFAZ rejeita uma emissão com aquele NCM. Quando você corrige o código do NCM e salva, o flag é **desmarcado automaticamente**, permitindo nova emissão.
- **Retorno da NF-e/NFC-e** — campo **somente leitura**. O sistema grava aqui o motivo técnico devolvido pela SEFAZ durante a transmissão, para o configurador entender o que precisa ajustar.

---

## 🧮 Aba `Principal` — tributação clássica

A aba `Principal` reúne todas as regras tributárias **anteriores à Reforma**. Cada bloco é um grupo independente, preenchido conforme o regime da empresa e o tipo de operação.

### 🔵 Grupo `ICMS Normal — Saída`

Define como o ICMS é calculado nas saídas:

| Campo | O que define |
|---|---|
| **Base de Cálculo ICMS — Interno** | Base usada nas vendas dentro do estado |
| **ICMS Aliq. — Interno** | Alíquota aplicada na operação interna |
| **Base de Cálculo ICMS — Externo** | Base usada nas vendas interestaduais |
| **ICMS Aliq. — Externo** | Alíquota aplicada na operação interestadual |
| **CST — Saída** | Código de Situação Tributária aplicado nas saídas (3 dígitos) |
| **CST — Ent.** | CST aplicado na entrada / retorno de devolução (3 dígitos) |
| **CSOSN** | Código equivalente para empresas do Simples Nacional |
| **MVA** | Margem de Valor Agregado (substituição tributária) |
| **Modalidade BC ICMS** | Combo: `0 = Margem Valor Agregado (%)`, `1 = Pauta (Valor)`, `2 = Preço Tabelado Máx. (valor)`, `3 = Valor da operação` |
| **Redução BC ICMS** | Calculado automaticamente como `100 − Base ICMS Interno` ao sair do campo de Base — somente leitura |
| **Código de Desoneração** | Identifica o motivo de desoneração quando aplicável |

> 💡 Os campos CSOSN, MVA e Modalidade BC só fazem sentido em certas combinações de regime tributário e CST. Em uma empresa do Lucro Real, por exemplo, o CSOSN não é usado.

> 🔒 **Validações ao salvar:**
> - Quando o **CST Saída = `000`**, é obrigatório preencher **Alíq. Interno** e **Alíq. Externo** (não podem ficar em zero).
> - Quando o **CST Entrada = `060`** (ICMS-ST), é obrigatório preencher **MVA** — exceto se a empresa estiver configurada para não usar Substituição Tributária.

### 🟠 Grupo `Fundo Combate Pobreza`

Configura o **FCP**, adicional de ICMS destinado ao combate à pobreza, cobrado em alguns estados:

- **FCP Aliq.** — alíquota interna
- **MVA FCP** — margem agregada quando o FCP entra na ST
- **FCP Aliq. Externa** — alíquota interestadual

### 🟢 Grupo `ICMS Crédito Outorgado — Saída`

Para estados/atividades que concedem **crédito presumido** na saída:

- **Crédito — Interno** — percentual aplicável em operações dentro do estado
- **Crédito — Externo** — percentual aplicável em operações interestaduais
- **Código do Crédito** — código fiscal que identifica o benefício

### 🔴 Grupo `Tributação Federal`

Subdividido em quatro blocos. Cada um trata de uma situação distinta:

- **Pis/Cofins (Entrada)** — `CST - PIS/COFINS (E)`, `Aliq PIS (E)`, `Aliq COFINS (E)` — aplicado nas compras
- **Pis/Cofins (Saída)** — `CST - PIS/COFINS (S)`, `Aliq PIS (S)`, `Aliq COFINS (S)` — aplicado nas vendas
- **Pis/Cofins (Entrada Dev.)** — `CST - PIS/COFINS (E.D)` — aplicado nas devoluções de venda
- **IPI** — `CST - IPI`, `Aliq IPI`

> 💡 **Sobre o combo `Tributação Federal` do cabeçalho:** ele é um atalho de preenchimento. Ao selecionar um perfil, o sistema **copia** os valores correspondentes (CSTs e alíquotas) para os campos deste grupo. Limpar o combo **zera** os campos. Depois de carregar, você ainda pode ajustar os valores manualmente — os valores finais nos campos são o que vai para a emissão.

---

## 🆕 Aba `IVA` — Reforma Tributária (CBS e IBS)

**IVA** quer dizer **Imposto sobre Valor Agregado** — o conceito que está por trás da Reforma Tributária brasileira (EC 132/2023). A aba reúne os parâmetros dos dois novos tributos que vão substituir parte da tributação atual:

- **CBS** — Contribuição sobre Bens e Serviços (federal, substitui PIS/COFINS)
- **IBS** — Imposto sobre Bens e Serviços (estadual + municipal, substitui ICMS e ISS)

### Identificação

- **CST** — Código de Situação Tributária CBS/IBS
- **Código Classificação** — código de Classificação Tributária (`cClassTrib`) que vai nos novos documentos fiscais

> 💡 Duplo clique no campo **Código Classificação** abre a tabela de classificações tributárias. Ao selecionar uma linha, o sistema autocompleta o **CST**, o próprio **Código Classificação** e as **Reduções de Alíquota** (CBS, IBS UF e IBS Mun.).

### Grupo `CBS`

- **Alíquota CBS** — alíquota cheia
- **Redução Aliq. CBS** — percentual de redução (regimes específicos, cesta básica etc.)

### Grupo `IBS`

- **Alíquota IBS UF** — parte estadual da alíquota
- **Alíquota IBS Mun.** — parte municipal da alíquota
- **Redução Aliq. IBS UF** — redução sobre a parte estadual
- **Redução Aliq. IBS Mun.** — redução sobre a parte municipal

> 💡 Os campos da aba `IVA` passam a valer conforme a Reforma entra em vigor (cronograma 2026–2033). Até lá, a aba `Principal` continua sendo o que de fato é usado nas emissões. Veja a [Documentação da Reforma Tributária](documentacao_reforma_tributaria.md) para o cronograma completo e os impactos por tipo de empresa.

---

## 🔁 Bases mestras que alimentam o Cadastro de NCM

O Sol.NET usa **duas bases mestras** complementares para apoiar o preenchimento do Cadastro de NCM (`21`):

### Tabela NCM (`121`) — descrição e identificação

Cobre **todos os NCMs publicados** com descrição oficial, EX, Tipo (Produto/Serviço) e — para a Reforma Tributária — alíquotas CBS/IBS por vigência (`VIGENCIA_INICIO`, `VIGENCIA_FIM`, `VERSAO`). É a tabela que aparece ao dar duplo clique no campo **NCM** do cadastro.

Quando você seleciona um NCM na Tabela NCM, o cadastro `21` recebe automaticamente:
- **Código NCM**
- **Descrição NCM**
- **EX**
- **Tipo** (Produto / Serviço)

> 🔎 O campo **CNI** **não** é preenchido por essa tabela — é digitação manual do configurador quando aplicável.

### Tabela NCM Tributos — referência de MVA

Tabela separada usada apenas para encontrar **MVA por NCM**. Quando o NCM é selecionado, o sistema busca o MVA com fallback sucessivo (8 → 7 → 6 → 5 → 4 dígitos do NCM) até achar uma correspondência:

- **Se acha MVA > 0** (NCM com ST): o cadastro recebe automaticamente CST Entrada/Saída = `060`, CSOSN = `500`, alíquota externa vinda da tela `Empresas`, e a Base Externa fica `100%`.
- **Se MVA = 0 ou não encontrado**: o cadastro recebe CST Entrada/Saída = `000`, CSOSN vindo da empresa, e alíquotas internas e externas também vindas da empresa.

Para esse autocomplete funcionar, a tela `Empresas` (código `1`) precisa ter os parâmetros `CSOSN_EXCEL`, `ICMS_ALIQ_I`, `ICMS_ALIQ_E` (e `ICMS_ALIQ_STE` quando aplicável) preenchidos. Se faltar, o sistema avisa: *"Configure os Parâmetros dos Impostos em Empresa! Aba Fiscal/SPED/Imp. Excel"*.

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Empresas` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nesta tela.

> 🚧 NCM que existe no cadastro `21` mas não aparece na Tabela NCM `121` é sinal de desatualização — abra um chamado para a Hetosoft revisar.

---

## 💡 Exemplos Práticos

### Exemplo 1 — Cadastrar um NCM novo de mercadoria interna

1. Abrir a pesquisa (`F1`) e digitar `NCM` (código `21`).
2. Incluir um novo registro.
3. No campo **NCM**, dar duplo clique para abrir a Tabela NCM federal e selecionar o código (ex.: `2204.21.00` — vinho engarrafado). O sistema preenche **Descrição**, **EX** e **Tipo**.
4. Em seguida, o sistema consulta a Tabela NCM Tributos para o MVA e pré-preenche CST, CSOSN e alíquotas da aba `Principal` com base nos parâmetros da empresa.
5. Conferir / ajustar os valores carregados (Base e Alíq. interno e externo, CST entrada, CST saída).
6. Preencher o **CNI** se o produto tiver tributação zerada, monofásica ou suspensão.
7. Selecionar a **Tributação Federal** apropriada para puxar o perfil de PIS/COFINS/IPI; ajustar manualmente se necessário.
8. Se o produto tem ST, escolher a **Região Tributária ICMS ST** e conferir o MVA.
9. Conferir os campos da aba `IVA` se a empresa já estiver operando sob a Reforma — usar o duplo clique no **Código Classificação** para puxar CST CBS/IBS e reduções automaticamente.
10. Salvar.

### Exemplo 2 — NCM rejeitado pela SEFAZ

Cenário: a SEFAZ rejeitou uma NF-e com motivo de NCM inválido. O próprio sistema marca a caixa **NCM Inválido** e registra o retorno no campo `Retorno da NF-e/NFC-e` quando isso acontece.

1. Localizar o NCM marcado como inválido no cadastro `21`.
2. Ler o **Retorno da NF-e/NFC-e** para entender o motivo apontado pela SEFAZ.
3. Conferir o código na Tabela NCM `121`. Se não existir, é desatualização da base. Se existir, geralmente o que está faltando é a **EX** correspondente.
4. Ajustar o que for necessário (EX, CST, CNI, parametrização tributária).
5. Salvar — ao mudar o `CODIGO` do NCM, o sistema desmarca automaticamente o flag **NCM Inválido**, liberando o uso em novas emissões.

### Exemplo 3 — Produto com tributação CBS/IBS reduzida (cesta básica)

1. Localizar o NCM no cadastro `21` e editar.
2. Abrir a aba **IVA**.
3. Preencher **CST** com o código CBS/IBS que indica redução.
4. Em **Alíquota CBS**, lançar a alíquota cheia; em **Redução Aliq. CBS**, lançar o percentual de redução.
5. Repetir o procedimento para IBS UF e IBS Mun. conforme o enquadramento.
6. Salvar.

---

## ❓ FAQ / Problemas Comuns

Para o conjunto completo, consulte [FAQ — Cadastro de NCM](faq_ncm.md). Três dúvidas que aparecem com mais frequência:

### ❓ Onde devo configurar a alíquota CBS — no Tributação Federal ou na aba IVA?

Sempre na aba **IVA**. O combo **Tributação Federal** continua sendo usado apenas para PIS/COFINS e IPI (regime antigo). Misturar os dois é um erro comum em quem está começando a operar sob a Reforma.

### ❓ Por que minha NF-e está retornando "NCM inválido" se o código está na tabela da Receita?

A causa mais frequente é a **EX** (exceção do NCM). Sem ela, a SEFAZ rejeita produtos que exigem desdobramento. Confira a coluna EX da tabela oficial e preencha o campo correspondente no cadastro.

### ❓ Posso ter dois registros com o mesmo NCM no cadastro `21`?

Pode — desde que a parametrização tributária seja **diferente** em pelo menos um dos campos da chave de unicidade (NCM, EX, CST Entrada, CST Saída, CSOSN, Tributação Federal, MVA, Base e Alíq. ICMS Interno/Externo). Um NCM com EX `00` e outro com EX `01`, por exemplo, são registros distintos.

---

## 🔗 Telas relacionadas

- **Cadastro Tabela NCM** (código `121`) — base federal de consulta e fonte para autocompletar
- **Região ICMS Saída** (código `93`) — regras de ICMS por região
- **Região ICMS ST Saída** (código `94`) — regras de Substituição Tributária por região
- **Natureza de Operação** (código `36`) — classificação fiscal de cada movimento
- **[Reforma Tributária — Documentação](documentacao_reforma_tributaria.md)** — contexto completo da CBS/IBS
- **Cadastro de Produtos** (código `32`) — onde cada produto aponta para um NCM cadastrado aqui

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Configuradores fiscais, contadores e equipe de suporte Sol.NET
