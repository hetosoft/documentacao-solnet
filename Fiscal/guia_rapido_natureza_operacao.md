# ⚡ Guia Rápido — Natureza de Operação

## 🎯 Para que serve

Cartão de referência para cadastrar e diagnosticar Naturezas de Operação. Para a explicação completa, abra a [Documentação da Natureza de Operação](documentacao_natureza_operacao.md).

A Natureza concentra **CFOP + ICMS + PIS/COFINS + CBS/IBS** em um único registro. É o vértice fiscal que conecta NCM, [Região ICMS Saída](documentacao_regiao_icms.md), Tipos de Movimento e a importação de XML.

---

## 🚪 Como abrir

Pela pesquisa universal (`F1`), digite `Natureza de Operação` ou o código `36`.

---

## 📋 Checklist — cadastrar uma Natureza de Saída

1. ☐ Abrir `Natureza de Operação` (código `36`).
2. ☐ Incluir um novo registro.
3. ☐ Duplo clique em **CFOP** e selecionar (ex.: `5102`). O sistema preenche a Descrição, ajusta **Tipo** e **Selecione** automaticamente.
4. ☐ Ajustar **Descrição** se necessário (já preenchida com a do CFOP).
5. ☐ Preencher **CST - ICMS**, **Base de Cálculo ICMS**, **ICMS Aliq.**, **Modalidade BC ICMS** e **CSOSN** (se Simples).
6. ☐ Na aba **Pis/Confis**, preencher CST PIS/COFINS, Aliq PIS e Aliq COFINS.
7. ☐ No grupo **CBS/IBS**, dar duplo clique em **Código Classificação** para puxar a classificação da Reforma — autocompleta CST e Reduções.
8. ☐ Avaliar marcar **`Manter (CFOP, CST ICMS, CSOSN, Base ICMS e Aliq. ICMS)`** se a Natureza precisa ignorar Região ICMS.
9. ☐ Avaliar marcar **`Manter (CST CBSIBS, Cód. Class, Aliq. CBS, Redução…)`** para o mesmo efeito sobre CBS/IBS.
10. ☐ Salvar.

---

## 📋 Checklist — cadastrar uma Natureza de Entrada (Compra)

1. ☐ Incluir um novo registro.
2. ☐ Escolher um CFOP de entrada (ex.: `1102`). Sistema marca Tipo = Entrada / Selecione = Dentro do Estado.
3. ☐ Conferir / preencher os campos de ICMS, PIS/COFINS, CBS/IBS (mesmas regras de saída).
4. ☐ Na aba **Importar XML**:
    - Preencher **CFOP Reverso (Ex: /5102/5405/)** com os CFOPs de saída do fornecedor que mapeiam para esta entrada.
    - Preencher **CFOP - 07 Material de Uso e Consumo** se houver tratamento diferenciado.
    - Preencher **CFOP - 08 Ativo Imobilizado** se houver tratamento diferenciado.
5. ☐ Para entradas sem crédito (uso/consumo, imobilizado), marcar **Não Gerar Crédito de ICMS** (aba Extras) e/ou **Não Gerar Crédito de PIS/COFINS** (aba Pis/Confis).
6. ☐ Salvar.

---

## 🧮 Anatomia da tela

| Bloco | O que mora ali |
|---|---|
| **Cabeçalho** | CFOP, Tipo, Selecione, Descrição, ICMS Aliq., CST ICMS, Base ICMS, Modalidade BC ICMS, CSOSN, OBS |
| **Flags Manter** | Override da Natureza sobre a Região ICMS (`TP_FIXO` para ICMS, `MANTER_CBSIBS` para CBS/IBS) |
| **Aba Importar XML** | CFOP Reverso (CFOP_COMPRA), CFOP Consumo, CFOP Imobilizado |
| **Aba Informações** | Texto livre para o XML do documento fiscal |
| **Aba Extras** | Tipo Operação (SPED), Não Gerar Crédito de ICMS |
| **Aba Pis/Confis** | CST PIS/COFINS, Aliq PIS, Aliq COFINS, Não Gerar Crédito de PIS/COFINS |
| **Grupo CBS/IBS** | CST, Código Classificação, Alíquotas e Reduções de CBS e IBS (UF + Mun.) |

### Coerência CFOP × Tipo × Localização

| Tipo / Localização | CFOP começa com |
|---|---|
| Saída × Dentro do Estado | `5` |
| Saída × Fora do Estado | `6` |
| Saída × Exterior | `7` |
| Entrada × Dentro do Estado | `1` |
| Entrada × Fora do Estado | `2` |
| Entrada × Exterior | `3` |

O autocomplete do CFOP ajusta automaticamente Tipo e Localização — basta confirmar.

---

## 🔁 Como a Natureza é aplicada no movimento

1. **Escolha manual** pelo operador no lançamento do item.
2. **Por Região ICMS Saída (`93`)** — a Região aponta a Natureza conforme contexto (loja, UF, regime, atividade, IE, tipo de item).
3. **Por Tipo de Movimento (`37`)** — pode definir uma Natureza padrão e controlar se a Região sobrescreve.

Flags **Manter** da Natureza fazem ela **ignorar a Região** e preservar os próprios valores no item.

---

## 🔥 Problemas comuns — soluções rápidas

### ❌ "CFOP Obrigatório!"
Faltou escolher o CFOP no cabeçalho.

### ❌ "CFOP não é de saída!" / "CFOP não é de entrada!" / "CFOP não é dentro do estado!" / "CFOP não é fora do estado!" / "CFOP não é Exterior!"
O CFOP escolhido tem primeiro dígito incompatível com **Tipo** e/ou **Selecione** marcados. Reescolher o CFOP ou ajustar Tipo/Selecione.

### ❌ "CFOP de Compra Reversa não permitido para Operação de Saída!"
Natureza marcada como Saída não pode ter **CFOP Reverso (CFOP_COMPRA)** preenchido na aba Importar XML. Esvazie o campo ou troque o Tipo.

### ❌ Valores de ICMS continuam aparecendo no SPED mesmo com a Natureza marcada
Verificar se realmente é a Natureza usada no movimento. A flag **Não Gerar Crédito de ICMS** zera ICMS no SPED **somente** para movimentos que apontam esta Natureza.

### ❌ Região ICMS Saída sobrescreveu a Natureza configurada
Esperado por padrão. Para impedir, marque **`Manter (CFOP, CST ICMS, CSOSN, Base ICMS e Aliq. ICMS)`** na Natureza. Para CBS/IBS, marcar também o segundo `Manter`.

### ❌ Não acho o campo "Natureza de Operação Reversa" na tela
É um campo legado, presente no código da tela mas **fora da área visível**. Pode ignorar.

---

## 🔗 Telas relacionadas

- **Cadastro de NCM** (`21`) — outra fonte de valores fiscais
- **Região ICMS Saída** (`93`) — mapeia contextos para escolher Natureza
- **Região ICMS ST Saída** (`94`) — análogo para Substituição Tributária (em fila)
- **Cadastro de CFOP** — fonte das pesquisas de CFOP
- **Tabela de Classificação Tributária** — autocomplete do Código Classificação
- **Importar XML** (`204`) — consumidor do CFOP Reverso
- **Tipos de Movimento** (`37`) — define Natureza padrão por movimento

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Configuradores fiscais e equipe de suporte
