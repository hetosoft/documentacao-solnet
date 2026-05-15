# ❓ FAQ — Natureza de Operação

Perguntas frequentes sobre o **Cadastro de Natureza de Operação** (código `36`) do Sol.NET. Para a referência completa, abra a [Documentação da Natureza de Operação](documentacao_natureza_operacao.md).

---

## 📋 Conceito e estrutura

### ❓ O que é a Natureza de Operação no Sol.NET?

É o cadastro **central** dos parâmetros fiscais por tipo de operação. Cada registro consolida CFOP, regras de ICMS, regras de PIS/COFINS, regras de CBS/IBS (Reforma) e configurações específicas para importação de XML. A Natureza é o que diz para o sistema "essa operação tributa assim".

### ❓ Como a Natureza de Operação se relaciona com NCM e Região ICMS?

- O **NCM** (`21`) traz a tributação padrão do produto.
- A **Região ICMS Saída** (`93`) escolhe uma **Natureza** específica conforme o contexto da operação (UF do destinatário, regime, atividade, IE etc.).
- A **Natureza** define a regra fiscal final aplicada ao item.

Quem prevalece em caso de conflito depende das flags `Manter` da Natureza (que ignoram a Região) e dos flags `Manter` da própria Região (que sobrescrevem o NCM). Consulte a [Documentação da Região ICMS Saída](documentacao_regiao_icms.md) para os detalhes da hierarquia.

### ❓ A tela tem várias abas — em qual ordem devo preenchê-las?

Sugestão prática:

1. **Cabeçalho**: comece pelo CFOP (ele ajusta Tipo e Localização). Depois Descrição, ICMS (CST, Base, Aliq, Modalidade BC, CSOSN).
2. **Aba Pis/Confis**: CST PIS/COFINS, Aliq PIS, Aliq COFINS.
3. **Grupo CBS/IBS**: duplo clique em **Código Classificação** para autocompletar CST, código e Reduções.
4. **Aba Extras**: marcar Tipo Operação (SPED) e flags de Não Gerar Crédito quando aplicável.
5. **Aba Importar XML** (só se for Natureza de Entrada): CFOP Reverso, CFOP Consumo, CFOP Imobilizado.
6. **Aba Informações**: Informações Adicionais que vão no XML do documento fiscal.
7. **Flags Manter**: decidir se a Natureza prevalece sobre a Região ICMS.

---

## ⚡ Autocomplete inteligente do CFOP

### ❓ Por que o sistema mudou o Tipo e o Selecione quando escolhi o CFOP?

É o autocomplete inteligente. Ao escolher um CFOP, o sistema lê o primeiro dígito e ajusta automaticamente:

- `1` / `2` / `3` → Tipo = **Entrada**
- `5` / `6` / `7` → Tipo = **Saída**
- `1` / `5` → Selecione = **Dentro do Estado**
- `2` / `6` → Selecione = **Fora do Estado**
- `3` / `7` → Selecione = **Exterior**

Se você quer outro valor, ajuste **depois** de selecionar o CFOP — o sistema preserva qualquer mudança subsequente.

### ❓ Preciso preencher Descrição manualmente?

Quando você escolhe um CFOP e o campo **Descrição** está vazio, o sistema preenche com a descrição do CFOP. Você pode reescrever para algo mais específico do seu fluxo, mas o default já costuma servir.

---

## 🧮 Regras fiscais

### ❓ Quando devo preencher CSOSN?

Quando a empresa é optante pelo **Simples Nacional**. Para Lucro Real e Lucro Presumido, o CSOSN é ignorado — o CST é o que importa.

### ❓ Qual o efeito do `Modalidade BC ICMS`?

Define como a Base de Cálculo do ICMS é determinada para movimentos com esta Natureza:

- `0 = Margem Valor Agregado (%)`
- `1 = Pauta (Valor)`
- `2 = Preço Tabelado Máx. (Valor)`
- `3 = Valor da operação`

A escolha afeta o cálculo do imposto na emissão.

### ❓ O campo `ICMS ST Aliq.` é usado em quê?

**Atualmente nada.** Buscamos o uso desse campo em todo o código do `ProjetosSol.NET` e ele aparece apenas no `.dfm` do form — nenhum motor de cálculo o consome. No banco, 0 de 106 Naturezas tinham o campo preenchido. É um **campo legado** que sobreviveu na tela mas não é mais usado. A configuração atual de Substituição Tributária por região está na Região ICMS ST Saída (`94`), vinculada ao NCM do produto.

### ❓ E o campo `Tipo Operação` na aba Extras?

Combo opcional com `Material de Uso e Consumo` e `Ativo Imobilizado`. Serve **apenas para distinguir lançamentos no SPED** — não influencia o cálculo de imposto na emissão.

### ❓ Marcar "Não Gerar Crédito de ICMS" — onde vira efeito?

Na geração do **SPED Fiscal**: registros de movimentos lançados com esta Natureza saem com **Base, Alíquota e Valor de ICMS zerados**. Útil para entradas em que a empresa não tem direito a crédito (uso/consumo, imobilizado com restrição etc.). A NF-e em si continua sendo emitida com o destaque normal.

### ❓ E "Não Gerar Crédito de PIS/COFINS"?

Mesma lógica, mas no **SPED PIS/COFINS**: zera Base/Alíq/Valor de PIS e COFINS, e pula ajustes M220/M620 (créditos extemporâneos).

---

## 🔒 Flags "Manter"

### ❓ Para que servem as duas caixas "Manter" embaixo do cabeçalho?

Para forçar que a Natureza **ignore a Região ICMS Saída** do produto:

- **Manter (CFOP, CST ICMS, CSOSN, Base ICMS e Aliq. ICMS)** → `TP_FIXO`. Quando marcada, o motor de aplicação não sobrescreve esses valores via Região ICMS.
- **Manter (CST CBSIBS, Cód. Class, Aliq. CBS, Redução, Aliq. IBS, Redução)** → `MANTER_CBSIBS`. Mesma coisa, mas para os valores da Reforma.

Use em Naturezas que precisam ter regra própria, independentemente do contexto do destinatário.

### ❓ Marquei `TP_FIXO` mas mesmo assim a Região está sobrescrevendo

Verificar:

- A Natureza realmente está aplicada ao item? (não basta cadastrar — o item precisa apontar para ela)
- A flag está salva? Reabrir o cadastro e conferir.
- A Região ICMS pode estar aplicada num outro caminho (vinculação direta ao produto, por exemplo) que não passa pela Natureza.

---

## 📥 Importar XML

### ❓ O que é o campo "CFOP Reverso  Ex: (5102/5405)" na aba Importar XML?

É a lista (delimitada por `/`) dos **CFOPs de saída do fornecedor** que mapeiam para esta Natureza. Quando o `Importar XML` (`204`) recebe uma NF-e do fornecedor com um item que tem CFOP listado aqui (saída do fornecedor), ele atribui automaticamente esta Natureza à entrada correspondente no seu Sol.NET.

Por exemplo: se a Natureza é `1102 — Compra para Comercialização` e a maioria dos fornecedores emite `5102 / 5405`, você preenche `/5102/5405/` para que o XML deles caia direto nessa Natureza.

### ❓ Para que servem `CFOP - 07 Material de Uso e Consumo` e `CFOP - 08 Ativo Imobilizado`?

São **CFOPs alternativos** aplicados em lugar do CFOP principal quando o item importado é classificado como Material de Uso e Consumo (código SPED `07`) ou Ativo Imobilizado (`08`). Permite que a mesma Natureza atenda entradas diferentes com CFOPs corretos por categoria do item.

### ❓ Preciso preencher CFOP Reverso em Natureza de Saída?

Não — e o sistema impede. Se você tentar salvar uma Natureza de Saída com CFOP Reverso preenchido, aparece *"CFOP de Compra Reversa não permitido para Operação de Saída!"*. A aba **Importar XML** só faz sentido para entradas.

---

## 🆕 Reforma Tributária (CBS/IBS)

### ❓ Onde configuro CBS e IBS na Natureza?

No grupo **CBS/IBS** que fica abaixo das abas (não é uma aba — é um grupo fixo). Os campos principais:

- **CST** — Código de Situação Tributária CBS/IBS
- **Código Classificação** — `cClassTrib` (6 caracteres) que vai no XML
- **Alíquota CBS** + **Redução**
- **Alíquota IBS UF** + **Redução**
- **Alíquota IBS Mun.** + **Redução**

### ❓ Posso autocompletar todos os campos CBS/IBS de uma vez?

Sim. Duplo clique no **Código Classificação** abre a **Tabela de Classificação Tributária**. Ao escolher uma classificação, o sistema autocompleta o **CST CBS/IBS**, o **Código Classificação** e as **Reduções** (CBS, IBS UF e IBS Mun.) em sequência. Você só precisa preencher as alíquotas cheias.

---

## 🔄 Aplicação no movimento

### ❓ De quantas formas a Natureza chega até um item de movimento?

Três:

1. **Escolha manual** do operador no lançamento.
2. **Por Região ICMS Saída** (`93`) — a Região aponta a Natureza conforme o contexto.
3. **Por Tipo de Movimento** (`37`) — alguns Tipos definem Natureza padrão.

### ❓ Posso ter duas Naturezas idênticas em cenários diferentes?

Pode, e é comum. Cada Natureza é independente. O que diferencia o uso é:

- Onde ela está vinculada (Região, Tipo de Movimento, produto)
- O CFOP e os parâmetros fiscais específicos

Para evitar conflito com a Região ICMS, lembre que **cada Natureza só pode estar em uma Região ICMS Saída** — validação que vive na tela `93`.

---

## 🚫 Campos não documentados

### ❓ Onde está o campo `Natureza de Operação Reversa`?

Esse campo existe no código da tela (campos `txtCadNatOpRevDescricao` e `txtCadCFOPDescricaoRev`), mas está posicionado **fora da área visível** do painel de cadastro (Top = 457 e 493 em um painel de altura 193). Na prática, **o campo não aparece** na tela atual do Sol.NET — é um recurso legado que não pode mais ser preenchido. Pode ignorar.

---

## 🔗 Telas e documentos relacionados

- **[Documentação da Natureza de Operação](documentacao_natureza_operacao.md)** — referência completa
- **[Guia Rápido — Natureza de Operação](guia_rapido_natureza_operacao.md)** — checklist da rotina
- **[Cadastro de NCM](documentacao_ncm.md)** (`21`) — outra fonte de valores fiscais
- **[Região ICMS Saída](documentacao_regiao_icms.md)** (`93`) — mapeia contextos para escolher a Natureza
- **Região ICMS ST Saída** (`94`) — análogo para Substituição Tributária (em fila)
- **[Reforma Tributária](documentacao_reforma_tributaria.md)** — contexto completo da CBS/IBS
- **Cadastro de CFOP** — fonte das pesquisas de CFOP
- **Tabela de Classificação Tributária** — autocomplete do Código Classificação
- **Importar XML** (`204`) — consumidor do CFOP Reverso
- **Tipos de Movimento** (`37`) — pode definir Natureza padrão
- **Cadastro de Produtos** (`32`) — produto pode apontar para uma Natureza ou Região

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Configuradores fiscais, contadores e equipe de suporte
