# ⚡ Guia Rápido — Cadastro de NCM

## 🎯 Para que serve

Cartão de referência para quem está incluindo ou editando NCMs no Sol.NET. Para a explicação completa, consulte a [Documentação do Cadastro de NCM](documentacao_ncm.md).

---

## 🚪 Como abrir

| Tela | Código | Para que serve |
|---|---|---|
| **Cadastro de NCM** | `21` | Lista local da empresa, com toda a parametrização tributária |
| **Cadastro Tabela NCM** | `121` | Base federal — fonte de consulta e autocompletar |

Abra pela pesquisa universal (`F1`), digitando o nome ou o código.

---

## 📋 Checklist — cadastrar um NCM novo

1. ☐ Abrir `Cadastro de NCM` (código `21`).
2. ☐ Incluir um novo registro.
3. ☐ No campo **NCM**, dar duplo clique para abrir a Tabela NCM federal e selecionar o código.
4. ☐ Conferir o que veio automaticamente: **Descrição**, **EX** e **Tipo** (vêm da Tabela NCM `121`).
5. ☐ Conferir os campos da aba `Principal` pré-preenchidos a partir da Tabela NCM Tributos + parâmetros da empresa (CST Entrada/Saída, CSOSN, Base e Alíq. interno/externo).
6. ☐ Preencher **CNI** manualmente se o produto tiver tributação zerada/monofásica/suspensão.
7. ☐ Selecionar a **Tributação Federal** apropriada — o sistema **copia** os campos de PIS/COFINS/IPI a partir do perfil; ajustar manualmente se necessário.
8. ☐ Selecionar a **Região Tributária ICMS ST**, quando aplicável.
9. ☐ Conferir o MVA quando o produto tem ST (CST Entrada = `060`).
10. ☐ Conferir **Fundo Combate Pobreza** e **Crédito Outorgado** quando o estado exigir.
11. ☐ Na aba **IVA**, usar duplo clique no **Código Classificação** para puxar CST CBS/IBS e reduções automaticamente.
12. ☐ Salvar.

---

## 🧮 Aba `Principal` — o que mora em cada grupo

| Grupo | O que preencher |
|---|---|
| **ICMS Normal — Saída** | Base/Alíquota Interno e Externo, CST Saída e Entrada, CSOSN, MVA, Modalidade BC, Código de Desoneração. **Redução BC** é calculada automaticamente como `100 − Base ICMS Interno`. |
| **Fundo Combate Pobreza** | FCP Aliq., MVA FCP, FCP Aliq. Externa |
| **ICMS Crédito Outorgado — Saída** | Crédito Interno, Crédito Externo, Código do Crédito |
| **Tributação Federal** | PIS/COFINS (Entrada / Saída / Entrada Dev.) e IPI. O combo do cabeçalho **copia** os valores do perfil para esses campos; eles podem ser ajustados manualmente depois. |
| **SEFAZ REJEITOU** | Bloco preenchido **automaticamente pelo sistema** quando a SEFAZ rejeita uma emissão; o flag `NCM Inválido` é desmarcado automaticamente ao alterar o código do NCM. |

---

## 🆕 Aba `IVA` — Reforma Tributária

`IVA` = Imposto sobre Valor Agregado (CBS + IBS).

| Campo | O que preencher |
|---|---|
| **CST** | Código de Situação Tributária CBS/IBS |
| **Código Classificação** | `cClassTrib` que vai na NF-e |
| **Alíquota CBS** / **Redução Aliq. CBS** | Alíquota cheia e redução para CBS |
| **Alíquota IBS UF** / **Redução Aliq. IBS UF** | Parte estadual do IBS |
| **Alíquota IBS Mun.** / **Redução Aliq. IBS Mun.** | Parte municipal do IBS |

> 💡 Os campos da aba `IVA` só passam a valer conforme o cronograma da Reforma — até a virada, a aba `Principal` continua sendo o que de fato é usado.

---

## 🔥 Problemas comuns — soluções rápidas

### ❌ "NCM inválido" no retorno da SEFAZ
- O sistema marca o flag **NCM Inválido** e grava o motivo no campo **Retorno da NF-e/NFC-e** automaticamente
- Ler o motivo apontado pela SEFAZ no campo de retorno
- Conferir se preencheu a **EX** quando o NCM exige desdobramento
- Conferir se o código está na Tabela NCM `121`
- Ao alterar o `CODIGO` do NCM e salvar, o flag é desmarcado automaticamente

### ❌ Descrição NCM não preencheu automaticamente
- A Tabela NCM `121` provavelmente está desatualizada — abrir chamado para a Hetosoft revisar
- Como contorno: preencher manualmente o campo e salvar

### ❌ Alíquota CBS configurada mas a NF-e não aplica
- Verificar se está usando o **CST CBS/IBS correto** (campo `CST` da aba IVA, não o CST da aba Principal)
- Verificar se a operação cai dentro do cronograma da Reforma já em vigor

### ❌ PIS/COFINS zerou depois de mexer no combo `Tributação Federal`
- Selecionar uma `Tributação Federal` **copia** os valores do perfil para os campos da aba; **limpar** o combo **zera** os campos. Se você quer valores específicos, mantenha o combo selecionado e ajuste os campos manualmente, ou deixe o combo vazio e preencha tudo na mão.

### ❌ Erro "Configure os Parâmetros dos Impostos em Empresa!"
- Aparece quando o autocomplete da Tabela NCM tenta puxar CSOSN/Alíquotas e a tela `Empresas` (código `1`) está sem `CSOSN_EXCEL`, `ICMS_ALIQ_I` ou `ICMS_ALIQ_E` preenchidos
- Requer acesso de suporte para corrigir; abra um chamado com a Hetosoft

### ❌ "Obrigatório Ter Aliq. Interno e Aliq. Externo" ao salvar
- Aparece quando o CST Saída está em `000` mas alguma das alíquotas está zerada — `000` exige alíquota cheia

### ❌ "Obrigatório Ter MVA" ao salvar
- Aparece quando o CST Entrada está em `060` (ICMS-ST) e o MVA está zerado

---

## 🔗 Telas relacionadas

- **Região ICMS Saída** (`93`) — regras de ICMS por região
- **Região ICMS ST Saída** (`94`) — regras de ICMS-ST por região
- **Natureza de Operação** (`36`) — classificação fiscal do movimento
- **Cadastro de Produtos** (`32`) — vincula cada produto a um NCM

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Configuradores fiscais e equipe de suporte
