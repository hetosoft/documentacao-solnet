# 📄 Cadastro de Natureza de Operação — Sol.NET

## 🎯 Visão Geral

A **Natureza de Operação** é o cadastro **central** dos parâmetros fiscais por tipo de operação no Sol.NET. Cada Natureza consolida tudo o que define a tributação de um movimento:

- O **CFOP** principal e a direção da operação (Entrada/Saída × Dentro/Fora/Exterior)
- A regra de **ICMS** (CST, alíquota, base, modalidade BC, CSOSN)
- A regra de **PIS/COFINS** (CST, alíquotas)
- A regra de **CBS/IBS** da Reforma Tributária (CST, Código Classificação, alíquotas e reduções)
- **CFOPs alternativos** para importação de XML (CFOP do fornecedor, CFOP de Uso/Consumo, CFOP de Imobilizado)
- Flags que controlam se esta Natureza **prevalece sobre a Região ICMS** do produto

A Natureza de Operação é referenciada por outras telas fiscais e de movimentação: ela é o vértice que liga CFOP, NCM, [Região ICMS Saída](documentacao_regiao_icms.md), Tipos de Movimento e a importação de XML.

### Principais características

- ✅ Concentra ICMS, PIS/COFINS, CBS/IBS e CFOP em um único registro
- ✅ Autocomplete inteligente do CFOP ajusta automaticamente Tipo (Entrada/Saída) e Localização (Dentro/Fora/Exterior)
- ✅ Permite **forçar** os valores da Natureza sobre o NCM via flags `Manter`
- ✅ Suporta mapeamento de CFOP do fornecedor para a importação de XML
- ✅ Marca operações que **não geram crédito** tributário, com efeito direto na geração do SPED

---

## 🔧 Como acessar

Abra a pesquisa universal (`F1`), digite `Natureza de Operação` ou o código `36`, e abra a tela.

---

## 📋 Cabeçalho do cadastro

Os campos do topo definem a Natureza como um todo.

| Campo | O que é |
|---|---|
| **CFOP** | CFOP principal da operação. Duplo clique abre o cadastro de CFOP para escolha. **Obrigatório**. |
| **Tipo** | Radio: `Saída` ou `Entrada`. **Obrigatório**. |
| **Selecione** | Radio: `Dentro do Estado`, `Fora do Estado`, `Exterior`. **Obrigatório**. |
| **Descrição** | Texto livre, até 255 caracteres. |
| **ICMS Aliq.** | Alíquota interna de ICMS aplicada. |
| **CST - ICMS** | Código de Situação Tributária do ICMS (3 dígitos, zero-padded). |
| **Base de Cálculo ICMS** | Percentual base usada no cálculo. |
| **ICMS ST Aliq.** | Campo presente na tela mas **sem uso ativo** no motor de cálculo atual. A configuração de Substituição Tributária por região hoje vive na [Região ICMS ST Saída](../Fiscal/README.md) (`94`). |
| **Modalidade BC ICMS** | Combo: `0 = Margem Valor Agregado (%)`, `1 = Pauta (Valor)`, `2 = Preço Tabelado Máx.`, `3 = Valor da operação`. |
| **CSOSN** | Código equivalente ao CST para empresas do Simples Nacional. |
| **OBS** | Observação livre, até 150 caracteres. |

### ⚡ Autocomplete inteligente do CFOP

Ao escolher um CFOP pela pesquisa:

- O sistema preenche o ID e a descrição (`código - descrição`) no campo.
- Se **Descrição** ainda estiver vazia, ela é preenchida com a descrição do CFOP.
- O **Tipo** e o **Selecione** são **ajustados automaticamente** conforme o primeiro dígito do CFOP:
  - CFOP iniciando em `1` → Entrada / Dentro do Estado
  - CFOP iniciando em `2` → Entrada / Fora do Estado
  - CFOP iniciando em `3` → Entrada / Exterior
  - CFOP iniciando em `5` → Saída / Dentro do Estado
  - CFOP iniciando em `6` → Saída / Fora do Estado
  - CFOP iniciando em `7` → Saída / Exterior

---

## 🔒 Flags "Manter" — override sobre a Região ICMS

Logo abaixo do cabeçalho, dois checkboxes controlam se a Natureza **ignora a Região ICMS** do produto:

| Caption real do checkbox | Campo | O que faz |
|---|---|---|
| *"Manter (CFOP, CST ICMS, CSOSN, Base ICMS e Aliq. ICMS) Mesmo que o produto tenha 'Região ICMS'"* | `TP_FIXO` | Quando marcado, mantém o CFOP, CST ICMS, CSOSN, Base de Cálculo e Alíquota da Natureza no item do movimento, ignorando qualquer Região ICMS Saída (`93`) vinculada ao produto. |
| *"Manter (CST CBSIBS, Cód. Class, Aliq. CBS, Redução Aliq CBS, Aliq. IBS, Redução Aliq IBS) Mesmo que o produto tenha 'Região ICMS'"* | `MANTER_CBSIBS` | Idem, mas para os valores de CBS/IBS da Reforma Tributária. |

> 💡 Use essas flags em Naturezas que precisam ter regra fiscal própria, independente do contexto — por exemplo, operações específicas isentas ou com tributação diferenciada que não devem ser sobrescritas pela mecânica de Região ICMS.

---

## 🧾 Aba `Importar XML`

Configura a Natureza para o fluxo de importação de XML de NF-e (tela `Importar XML`, código `204`). Esses campos só fazem sentido em Naturezas de **Entrada** — a validação no salvamento impede preencher o CFOP Reverso em Naturezas de Saída.

| Campo | O que define |
|---|---|
| **CFOP Reverso  Ex: (5102/5405)** | Lista delimitada por `/` com os **CFOPs de saída do fornecedor** que mapeiam para esta Natureza no momento da importação. Ex.: `/5102/5405/` — quando o XML do fornecedor traz item com CFOP 5102 ou 5405 (saída deles), o sistema atribui esta Natureza à entrada correspondente. |
| **CFOP - 07 – Material de Uso e Consumo** | CFOP alternativo aplicado em **lugar do CFOP principal** quando o item importado é Material de Uso e Consumo. |
| **CFOP - 08 – Ativo Imobilizado** | CFOP alternativo aplicado em **lugar do CFOP principal** quando o item importado é Ativo Imobilizado. |

> 🔁 O par "CFOP Reverso × CFOP principal" reflete a lógica do fornecedor (saída) versus a sua (entrada): quem está vendendo usa um CFOP, quem está comprando usa o equivalente espelhado.

---

## 📝 Aba `Informações`

| Campo | O que define |
|---|---|
| **Informações Adicionais** | Texto livre (até 500 caracteres) inserido no campo "Informações Adicionais" do XML do documento fiscal gerado a partir de movimentos que usam esta Natureza. |

---

## ➕ Aba `Extras`

| Campo | O que define |
|---|---|
| **Tipo Operação** | Combo opcional: `Material de Uso e Consumo` ou `Ativo Imobilizado`. **Apenas para distinguir lançamentos no SPED** — não influencia o cálculo do imposto na emissão. |
| **Não Gerar Crédito de ICMS** | Checkbox. Quando marcado, a geração do SPED Fiscal **zera Base, Alíquota e Valor de ICMS** para movimentos lançados com esta Natureza. Útil para entradas que não geram direito a crédito (uso/consumo, imobilizado com restrição, etc.). |

---

## 💰 Aba `Pis/Confis`

| Campo | O que define |
|---|---|
| **CST - PIS/COFINS** | Código de Situação Tributária de PIS/COFINS. |
| **Aliq PIS** | Alíquota de PIS aplicada. |
| **Aliq COFINS** | Alíquota de COFINS aplicada. |
| **Não Gerar Crédito de PIS/COFINS** | Quando marcado, a geração do SPED PIS/COFINS **zera Base, Alíquota e Valor** das contribuições para movimentos lançados com esta Natureza, e pula os ajustes M220/M620 (créditos extemporâneos). |

---

## 🆕 Grupo `CBS/IBS` (Reforma Tributária)

Fora das abas, abaixo da área principal, fica o grupo com os parâmetros dos novos tributos da Reforma:

| Campo | O que define |
|---|---|
| **CST** | Código de Situação Tributária CBS/IBS. |
| **Código Classificação** | Código de Classificação Tributária (`cClassTrib`, 6 caracteres) que vai no XML dos novos documentos. Duplo clique abre a tabela de classificações e autocompleta CST, Código e Reduções (CBS, IBS UF e IBS Mun.) de uma vez. |
| **Alíquota CBS** / **Redução Aliq. CBS** | Alíquota cheia da CBS e percentual de redução. |
| **Alíquota IBS UF** / **Redução Aliq. IBS UF** | Parte estadual do IBS e sua redução. |
| **Alíquota IBS Mun.** / **Redução Aliq. IBS Mun.** | Parte municipal do IBS e sua redução. |

> 💡 Esses campos passam a valer conforme o cronograma da Reforma Tributária. Consulte a [Documentação da Reforma Tributária](documentacao_reforma_tributaria.md) para as fases de transição.

---

## 🔒 Validações ao salvar

- **CFOP obrigatório** — mensagem *"CFOP Obrigatório!"*.
- **Coerência CFOP × Tipo (Entrada/Saída)**:
  - Saída → CFOP precisa começar com `5`, `6` ou `7`.
  - Entrada → CFOP precisa começar com `1`, `2` ou `3`.
- **Coerência CFOP × Selecione (Localização)**:
  - Dentro do Estado → CFOP começa com `1` ou `5`.
  - Fora do Estado → CFOP começa com `2` ou `6`.
  - Exterior → CFOP começa com `3` ou `7`.
- **Saída não aceita CFOP Reverso** — Natureza marcada como Saída não pode ter `CFOP Reverso` (campo `CFOP_COMPRA`) preenchido. Mensagem: *"CFOP de Compra Reversa não permitido para Operação de Saída!"*.

---

## 🔁 Como a Natureza é aplicada nos movimentos

A Natureza pode chegar até um item de movimento por três caminhos:

1. **Escolha manual no movimento** — o operador seleciona a Natureza ao lançar o item.
2. **Pela [Região ICMS Saída](documentacao_regiao_icms.md) (`93`)** — a Região é configurada para o contexto (loja, UF, regime, atividade, IE, tipo de item) e aponta para a Natureza a aplicar.
3. **Pelo Tipo de Movimento (`37`)** — o Tipo de Movimento pode definir uma Natureza padrão, e flags como `EXECUTAR_REGIAO_ICMS` decidem se a Região tem permissão de sobrescrever.

Quando a Natureza tem **`TP_FIXO`** marcado, o motor de aplicação **ignora a Região ICMS** para o item e mantém os valores fiscais da própria Natureza. **`MANTER_CBSIBS`** faz o mesmo apenas para os valores CBS/IBS.

---

## 💡 Exemplos Práticos

### Exemplo 1 — Venda de mercadoria dentro do estado

1. Abrir `Natureza de Operação` (`36`) pela pesquisa (`F1`).
2. Incluir um novo registro.
3. Duplo clique no campo **CFOP** e selecionar `5102 — Venda de mercadoria adquirida ou recebida de terceiros`. O sistema preenche a Descrição automaticamente e marca **Tipo = Saída** + **Selecione = Dentro do Estado**.
4. Conferir: **CST ICMS** = `000` (tributado), **Base ICMS** = `100`, **Alíquota ICMS** conforme a UF da empresa.
5. Preencher CSOSN se a empresa for do Simples Nacional.
6. Na aba **Pis/Confis**, preencher CST e alíquotas de PIS/COFINS.
7. No grupo **CBS/IBS**, dar duplo clique no **Código Classificação** para puxar a classificação correta da Reforma e seus percentuais de redução.
8. Salvar.

### Exemplo 2 — Entrada de Compra com mapeamento de CFOP do fornecedor

1. Incluir um novo registro de Natureza.
2. Escolher **CFOP** `1102 — Compra para comercialização` (sistema marca **Tipo = Entrada** + **Selecione = Dentro do Estado**).
3. Preencher ICMS, CST, CSOSN conforme a regra da empresa.
4. Na aba **Importar XML**, em **CFOP Reverso Ex: (5102/5405)**, preencher `/5102/5405/6102/6108/` — os CFOPs de saída que fornecedores usam para o mesmo tipo de mercadoria.
5. Se quiser tratamento diferente para o mesmo item importado quando vier marcado como Uso/Consumo ou Imobilizado, preencher **CFOP Consumo** e **CFOP Imobilizado**.
6. Salvar.
7. Resultado: quando o **Importar XML** processar uma NF-e do fornecedor com CFOP `5102`, ele atribui automaticamente esta Natureza à entrada correspondente.

### Exemplo 3 — Entrada de Imobilizado sem direito a crédito de ICMS

1. Criar Natureza de Operação com **CFOP** `1551 — Compra de bem para o ativo imobilizado`.
2. Na aba **Extras**:
   - Marcar **Tipo Operação** = `Ativo Imobilizado` (para distinção no SPED).
   - Marcar **Não Gerar Crédito de ICMS**.
3. Na aba **Pis/Confis**, marcar **Não Gerar Crédito de PIS/COFINS** se for o caso.
4. Salvar.
5. Resultado: lançamentos com esta Natureza saem com valores de ICMS e PIS/COFINS zerados no SPED, refletindo que a empresa não tomou crédito daquela entrada.

---

## ❓ FAQ / Problemas Comuns

Para o FAQ completo, abra [FAQ — Natureza de Operação](faq_natureza_operacao.md). Três perguntas que aparecem com mais frequência:

### ❓ Por que o sistema mudou meu Tipo (Entrada/Saída) quando escolhi o CFOP?

Não é bug — é o autocomplete inteligente do CFOP. Ele inverte Tipo e Localização para refletir o primeiro dígito do CFOP escolhido (1/2/3 = Entrada, 5/6/7 = Saída). Se você quer Tipo manualmente, ajuste **depois** de selecionar o CFOP — o sistema preserva qualquer mudança subsequente.

### ❓ Para que serve o campo `ICMS ST Aliq.` no cabeçalho?

É um campo legado, presente na tela mas **sem uso ativo** no motor atual de cálculo de Substituição Tributária. A configuração de ST por região hoje vive na Região ICMS ST Saída (`94`), vinculada ao NCM do produto. Pode deixar em branco.

### ❓ Marquei "Não Gerar Crédito de ICMS" — onde isso vira efeito?

Na geração do **SPED Fiscal**: registros de movimentos lançados com esta Natureza saem com Base, Alíquota e Valor de ICMS **zerados**. A emissão da NF-e em si não é afetada — o destaque do ICMS no documento continua acontecendo normalmente. O flag mira apenas no que vai para o fisco como informação de crédito.

---

## 🔗 Telas relacionadas

- **[Cadastro de NCM](documentacao_ncm.md)** (`21`) — outra fonte de valores fiscais que pode ou não ser sobrescrita pela Natureza
- **[Região ICMS Saída](documentacao_regiao_icms.md)** (`93`) — mapeia contextos para escolher qual Natureza aplicar; flags `Manter` da Natureza fazem ela ignorar a Região
- **Região ICMS ST Saída** (`94`) — equivalente para Substituição Tributária (em fila)
- **Cadastro de CFOP** — usado nas buscas de CFOP, CFOP Consumo e CFOP Imobilizado
- **Tabela de Classificação Tributária** — fonte do autocomplete do `Código Classificação` no grupo CBS/IBS
- **Importar XML** (`204`) — consumidor do campo `CFOP Reverso (CFOP_COMPRA)`
- **Tipos de Movimento** (`37`) — pode definir uma Natureza padrão e controlar se a Região ICMS sobrescreve
- **Cadastro de Produtos** (`32`) — produto pode apontar para uma Natureza ou para uma Região ICMS

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Configuradores fiscais, contadores e equipe de suporte Sol.NET
