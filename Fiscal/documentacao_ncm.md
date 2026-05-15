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
| **NCM** | Código numérico, formato `NN.NN.NN.NN` (até 8 dígitos) | Chave fiscal — o mesmo que está na tabela da Receita |
| **EX** | Código de exceção do NCM (até 3 caracteres) | Usado quando o NCM tem desdobramento por finalidade |
| **CNI** | Código de Não Incidência (até 3 caracteres) | Aplicado em produtos com tributação zerada, monofásica ou suspensão — geralmente vem preenchido a partir da Tabela NCM |
| **Descrição NCM** | Texto descritivo do código | Preenchido automaticamente ao puxar da Tabela NCM (`121`) |
| **Tipo** | Produto ou Serviço | Preenchido automaticamente ao carregar o NCM da Tabela NCM |
| **Tributação Federal** | Combo que aponta para um perfil de PIS/COFINS/IPI já cadastrado | Quando preenchido, **prevalece** sobre os campos de PIS/COFINS/IPI da aba `Principal` |
| **Região Tributária ICMS ST** | Combo que aponta para uma `Região ICMS ST` (código `94`) | Define a regra de Substituição Tributária aplicada nas saídas |

### Caixa `SEFAZ REJEITOU`

Identifica um NCM que a SEFAZ rejeitou na transmissão de NF-e/NFC-e:

- **NCM Inválido** — marcador que sinaliza o registro como inválido para novas emissões até a regularização
- **Retorno da NF-e/NFC-e** — texto do retorno técnico (motivo da rejeição) para o configurador conferir o que precisa ajustar

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
| **CST — Saída** | Código de Situação Tributária aplicado nas saídas |
| **CST — Ent.** | CST aplicado quando o produto retorna como devolução |
| **CSOSN** | Código equivalente para empresas do Simples Nacional |
| **MVA** | Margem de Valor Agregado (substituição tributária) |
| **Modalidade BC ICMS** | Como a base de cálculo é determinada |
| **Redução BC ICMS** | Percentual de redução aplicado sobre a base |
| **Código de Desoneração** | Identifica o motivo de desoneração quando aplicável |

> 💡 Os campos CSOSN, MVA e Modalidade/Redução BC só fazem sentido em certas combinações de regime tributário e CST. Em uma empresa do Lucro Real, por exemplo, o CSOSN não é usado.

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

> ⚠️ Esses campos só são usados quando o combo **Tributação Federal** do cabeçalho **não** está preenchido. Quando você aponta uma Tributação Federal pré-cadastrada, ela tem prioridade sobre o que estiver aqui.

---

## 🆕 Aba `IVA` — Reforma Tributária (CBS e IBS)

**IVA** quer dizer **Imposto sobre Valor Agregado** — o conceito que está por trás da Reforma Tributária brasileira (EC 132/2023). A aba reúne os parâmetros dos dois novos tributos que vão substituir parte da tributação atual:

- **CBS** — Contribuição sobre Bens e Serviços (federal, substitui PIS/COFINS)
- **IBS** — Imposto sobre Bens e Serviços (estadual + municipal, substitui ICMS e ISS)

### Identificação

- **CST** — Código de Situação Tributária CBS/IBS (combo com os códigos publicados pela Receita)
- **Código Classificação** — código de Classificação Tributária (`cClassTrib`) usado nos novos documentos fiscais

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

## 🔁 Atualização via Tabela NCM (`121`)

A **Tabela NCM** (`121`) é a base federal completa — contém todos os NCMs publicados pela Receita, com descrição oficial e marcações que ajudam a popular o cadastro local.

Fluxo típico:

1. A Hetosoft (ou a equipe interna) **atualiza a Tabela NCM `121`** quando há publicação nova da Receita.
2. No cadastro `21`, ao **incluir um NCM novo**, o sistema busca o código na Tabela NCM e preenche automaticamente:
   - **Descrição NCM**
   - **Tipo** (Produto / Serviço)
   - **CNI** (quando aplicável)
3. As parametrizações tributárias (ICMS, PIS/COFINS, CBS/IBS) continuam sendo definidas pelo configurador — a Tabela NCM **não sobrescreve** esses campos.

> 🚧 NCM que existe no cadastro `21` mas não aparece na Tabela NCM `121` é sinal de desatualização da base — abra um chamado para a Hetosoft revisar.

---

## 💡 Exemplos Práticos

### Exemplo 1 — Cadastrar um NCM novo de mercadoria interna

1. Abrir a pesquisa (`F1`) e digitar `NCM` (código `21`).
2. Incluir um novo registro.
3. Digitar o código NCM (ex.: `2204.21.00` — vinho engarrafado).
4. Se a Tabela NCM `121` estiver atualizada, **Descrição**, **Tipo** e **CNI** já vêm preenchidos.
5. Selecionar a **Tributação Federal** apropriada — quando existe um perfil pré-cadastrado, ele preenche PIS/COFINS/IPI.
6. Preencher o grupo **ICMS Normal — Saída**:
   - CST de saída conforme o regime fiscal da empresa
   - Alíquotas internas e externas conforme a UF da empresa
7. Se o produto tem ST, escolher a **Região Tributária ICMS ST** e preencher MVA.
8. Conferir os campos da aba `IVA` se a empresa já estiver operando sob a Reforma — alíquotas CBS e IBS conforme o anexo aplicável.
9. Salvar.

### Exemplo 2 — Tratar um NCM rejeitado pela SEFAZ

Cenário: a empresa transmitiu uma NF-e e a SEFAZ rejeitou com motivo "NCM inválido".

1. Localizar o NCM problemático na lista do cadastro `21`.
2. Editar o registro.
3. Marcar a caixa **NCM Inválido** dentro do grupo `SEFAZ REJEITOU`.
4. Colar o texto do retorno no campo **Retorno da NF-e/NFC-e**.
5. Salvar.
6. Conferir se o código existe na Tabela NCM `121`. Se não existir, é desatualização da base. Se existir, conferir **EX**, **CNI** e a parametrização tributária — geralmente o que está faltando é a EX correspondente.

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

### ❓ Posso usar o mesmo NCM com configurações diferentes por filial?

Não — o cadastro de NCM (`21`) é compartilhado entre todas as filiais. Para tratar regras tributárias que variam por estado, use as telas de **Região ICMS Saída** (`93`) e **Região ICMS ST Saída** (`94`) referenciadas pelo NCM.

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
