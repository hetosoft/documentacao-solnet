# 📄 Cadastro de Região ICMS Saída — Sol.NET

## 🎯 Visão Geral

O **Cadastro de Região ICMS Saída** (`93`) é onde o Sol.NET define **qual Natureza de Operação aplicar** em cada item de uma venda, dependendo do contexto da operação: empresa que está emitindo, estado do destinatário, regime tributário, atividade comercial, indicador de inscrição estadual e tipo de item.

Diferente do que o nome pode sugerir, a tela **não armazena alíquotas, CSTs ou CFOPs** — ela é um **mapa de regras**:

> *"Para este conjunto de filtros (Tipo, CST do produto, Operação) e sub-filtros por linha (empresas, estados, regime, atividade, IE, tipo de item), use **esta Natureza de Operação**."*

Os valores fiscais (CST, alíquota, CSOSN, CFOP, CBS, IBS) que aparecem no detalhe **vêm da Natureza de Operação vinculada**, exibidos para conferência.

### Principais características

- ✅ Centraliza a decisão de **qual Natureza de Operação** se aplica em cada cenário
- ✅ Avalia filtros do contexto (UF do destinatário, regime, IE, atividade…) **automaticamente** durante a emissão
- ✅ Permite **fixar valores** (CST/CSOSN, Base/Alíq, CBS/IBS) para que prevaleçam sobre a configuração do NCM
- ✅ Tem **vigência por data** — ativa ou inativa uma regra sem precisar excluir o cadastro

---

## 🔧 Como acessar

Abra a pesquisa universal (`F1`), digite `Região ICMS Saída` ou o código `93`, e abra a tela.

---

## 📋 Cabeçalho do cadastro

Identifica a regra como um todo. Os filtros aqui valem para todas as linhas de detalhe abaixo.

| Campo | O que define |
|---|---|
| **Tipo** | `PESSOA` (regra aplicada pelo perfil do destinatário) ou `PRODUTO` (regra aplicada pelo produto / NCM) |
| **Descrição** | Texto livre, obrigatório, até 80 caracteres |
| **CST ICMS Prod.** | Lista de CSTs do produto que esta regra cobre, formato `/CST1/CST2/CST3/`. Ex.: `/000/010/060/`. O sistema adiciona barras automaticamente ao sair do campo. |
| **Operação** | Combo: `Venda`, `Devolução`, `Transferência`, `Compra`, e `Regra 5` a `Regra 10` (casos genéricos pré-configurados, referenciados pelas configurações do Tipo de Movimento) |
| **Data Inicial / Data Final** | Vigência. Datas vazias significam "sem limite". O sistema só aplica a regra se a data corrente estiver dentro da janela. |

> 🚫 **Validações para Tipo `PESSOA`**: não aceita `CST ICMS Prod.` nem `Operação` preenchidos — esses campos só fazem sentido em regras baseadas em produto.

---

## 🧮 Configurações — linhas de detalhe

A área de configurações é um **sub-cadastro** com seus próprios botões `Inserir`, `Atualizar`, `Deletar` e `Cancelar`. Cada linha define uma regra específica dentro da Região.

### Filtros de contexto (quando a linha se aplica)

Todos os filtros são **curingas**: deixar vazio ou em `-1` significa "qualquer valor".

| Campo | O que filtra |
|---|---|
| **Nº Lojas** | Códigos de filial separados por `/`, ex.: `/1/2/`. A linha só vale para essas lojas. Vazio = todas. |
| **Sigla Estados** | UFs do destinatário separadas por `/`, ex.: `/BA/SP/`. Vazio = todas. |
| **Regime Tributário** | `Simples Nacional`, `Lucro Real`, `Lucro Presumido` ou qualquer (vazio/-1). |
| **Atividade Comercial** | `Consumidor`, `Revenda`, `Indústria` ou qualquer (vazio/-1). |
| **Indicador IE** | `Contribuinte`, `Isento`, `Não Contribuinte` ou qualquer (vazio/-1). |
| **Tipo de Item** | Códigos SPED `00 – Mercadoria para Revenda`, `01 – Matéria-Prima`, `02 – Embalagem`, `03 – Produto em Processo`, `04 – Produto Acabado`, `05 – Subproduto`, `06 – Produto Intermediário`, `07 – Material de Uso e Consumo`, `08 – Ativo Imobilizado`, `09 – Serviços`, `10 – Outros Insumos`, `99 – Outras`, ou qualquer (vazio/-1). |

> 💡 **Especificidade ganha**: quando várias linhas combinam, o sistema ordena pela linha **mais específica** (menos curingas) e usa a primeira. Por isso, uma linha com `/BA/SP/` ganha de uma linha com Estado em branco.

### Natureza de Operação (pivô da regra)

O campo central do detalhe é a **Natureza de Operação** (`36`). Duplo clique no campo `Descrição CFOP` abre a tela `Natureza de Operação` para escolher. Ao selecionar, o sistema **autocompleta** na linha:

- CFOP e Descrição CFOP
- Tipo (Saída / Entrada) — radio
- Selecione (Dentro do Estado / Fora do Estado / Exterior) — radio
- Base ICMS, ICMS Aliq., CST ICMS, CSOSN
- CBS Aliq., Red. CBS, IBS UF Aliq., Red. IBS UF, IBS Mun. Aliq., Red. IBS Mun., CST CBS/IBS, Código Classificação

Esses campos são **somente leitura** — eles refletem a Natureza escolhida. Quem decide qual valor vai para o documento fiscal são as **flags "Manter"**.

> 🔒 **Uma Natureza só em uma Região**: o sistema impede vincular a mesma Natureza de Operação em mais de uma Região ICMS. Ao salvar, aparece a mensagem *"Não Permitido! Natureza de Operação Já Usada em outra Região ICMS"*.

### Flags "Manter" (override)

Três checkboxes definem o que a Região ICMS **força** sobre o item no momento da emissão, prevalecendo sobre a configuração do NCM:

| Flag | O que copia para o item ao emitir |
|---|---|
| **Manter CST/CSOSN** (`TP_FIXO`) | CST ICMS e CSOSN da Natureza |
| **Manter Base/Aliq.** (`TP_FIXO_ALIQ`) | Base de Cálculo e Alíquota ICMS da Natureza |
| **Manter Red/Aliq. IBS/CBS** (`TP_FIXO_ALIQ_IBSCBS`) | CST CBS/IBS, alíquotas CBS / IBS UF / IBS Mun. e respectivas reduções |

O CFOP da Natureza **sempre** sobrescreve o do item quando a Região ICMS é aplicada (não depende de flag).

### Validações ao salvar uma linha

- **CFOP obrigatório** no detalhe.
- **Coerência CFOP × Tipo (Entrada/Saída)**:
  - Tipo Saída → CFOP deve começar com `5`, `6` ou `7`
  - Tipo Entrada → CFOP deve começar com `1`, `2` ou `3`
- **Coerência CFOP × Localização (Selecione)**:
  - Dentro do Estado → CFOP começa com `1` ou `5`
  - Fora do Estado → CFOP começa com `2` ou `6`
  - Exterior → CFOP começa com `3` ou `7`

Se a Natureza de Operação escolhida tem CFOP que viola essas regras, o sistema rejeita o salvamento.

---

## 🔁 Como a Região ICMS é aplicada no movimento

Durante a emissão de um movimento (venda, devolução, etc.), para cada item:

1. O Sol.NET verifica o **Tipo de Movimento** (`37`). Se o Tipo de Movimento tem a flag `EXECUTAR_REGIAO_ICMS` ou se o tipo da movimentação aceita Região ICMS por padrão, e não há `NAO_EXECUTAR_REGIAO_ICMS`, segue.
2. **Busca da Região aplicável (em ordem):**
   - **Direta pelo produto**: se o produto tem uma `Região ICMS` vinculada no cadastro, o sistema usa essa.
   - **Fallback pelo CST do NCM**: se o produto não aponta uma Região, o sistema busca uma Região cujo `CST ICMS Prod.` inclua o CST do NCM do produto.
3. Dentro da Região encontrada, o sistema **filtra as linhas de detalhe** pelo contexto da operação (loja emissora, UF do destinatário, IE, atividade comercial, regime tributário, tipo de item) e seleciona a linha mais específica.
4. Da linha vencedora, o CFOP da Natureza é copiado para o item.
5. As flags **Manter CST/CSOSN**, **Manter Base/Aliq.** e **Manter Red/Aliq. IBS/CBS** decidem se também são copiados os valores correspondentes — sobrescrevendo o que veio do NCM.

> 🛑 **Exceção — Natureza com "TP_FIXO" global**: se a Natureza de Operação aplicada ao movimento já está configurada com `TP_FIXO`, ela **mantém tudo** e a Região ICMS é ignorada para esse item.

---

## 💡 Exemplos Práticos

### Exemplo 1 — Vendas tributadas dentro do estado

Uma Região com:
- Tipo `PRODUTO`
- CST ICMS Prod. `/000/010/020/030/040/041/050/051/090/`
- Operação `Venda`
- Sem vigência fixa

Linha de detalhe:
- Sigla Estados `/BA/`
- Regime Tributário `Lucro Real`
- Natureza de Operação `5102 — Venda de mercadoria adquirida ou recebida de terceiros`
- Manter CST/CSOSN: **desmarcado** (deixa o CST do NCM prevalecer)
- Manter Base/Aliq.: **marcado** (força a alíquota da Natureza)

Resultado: para todo produto tributado vendido na BA por uma empresa Lucro Real, o CFOP 5102 e a alíquota da Natureza serão aplicados. O CST continua vindo do NCM.

### Exemplo 2 — Devoluções fora do estado

Outra Região com:
- Tipo `PRODUTO`
- Operação `Devolução`
- Linha de detalhe com Sigla Estados `/SP/MG/RJ/`, Natureza `5202 — Devolução de compra para comercialização`

Funciona como o exemplo 1, mas só dispara quando o movimento é classificado como Devolução pelo Tipo de Movimento.

### Exemplo 3 — Tipo `PESSOA` para destinatário Não Contribuinte

Região com:
- Tipo `PESSOA`
- Sem CST e sem Operação (validação proíbe)

Linha de detalhe:
- Indicador IE `Não Contribuinte`
- Natureza específica para venda a consumidor final

Resultado: independente do CST do produto, qualquer venda para destinatário não contribuinte cai nessa regra.

---

## ❓ FAQ / Problemas Comuns

Para o FAQ completo, abra [FAQ — Região ICMS Saída](faq_regiao_icms.md). Três perguntas recorrentes:

### ❓ Por que a Região ICMS não está sendo aplicada nas minhas vendas?

Verifique nesta ordem:
1. O Tipo de Movimento usado tem a flag `EXECUTAR_REGIAO_ICMS` (ou é um tipo que aceita Região por padrão)?
2. O produto tem `Região ICMS` vinculada **ou** o NCM do produto tem CST que está listado em `CST ICMS Prod.` de alguma Região?
3. A vigência (Data Inicial / Data Final) está válida hoje?
4. Existe alguma linha de detalhe que combine com loja + UF + regime + atividade + IE + tipo de item do movimento?

### ❓ Posso usar a mesma Natureza de Operação em duas Regiões ICMS diferentes?

Não. O sistema impede no salvamento: *"Não Permitido! Natureza de Operação Já Usada em outra Região ICMS"*. Se precisa, crie uma cópia da Natureza com outro CFOP equivalente.

### ❓ As flags "Manter" prevalecem sobre o quê?

Sobre a configuração do **NCM do produto**, que é a fonte padrão dos valores fiscais. Quando marcadas, o valor da Natureza vinculada à Região é copiado para o item da movimentação no lugar do que viria do NCM.

---

## 🔗 Telas relacionadas

- **[Cadastro de NCM](documentacao_ncm.md)** (`21`) — fonte padrão de CST/alíquotas; o `CST ICMS Prod.` da Região mapeia esses CSTs
- **Natureza de Operação** (`36`) — pivô das linhas de detalhe; ainda em fila para documentação
- **Região ICMS ST Saída** (`94`) — análoga, mas para Substituição Tributária; ainda em fila
- **Tipos de Movimento** (`37`) — controla com `EXECUTAR_REGIAO_ICMS` / `NAO_EXECUTAR_REGIAO_ICMS` se a Região é aplicada
- **Cadastro de Produtos** (`32`) — onde a Região ICMS é opcionalmente vinculada direto ao produto

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Configuradores fiscais, contadores e equipe de suporte Sol.NET
