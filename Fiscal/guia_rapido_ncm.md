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
3. ☐ Digitar o código NCM (formato `NN.NN.NN.NN`).
4. ☐ Conferir se **Descrição**, **Tipo** e **CNI** foram preenchidos automaticamente (vêm da Tabela NCM `121`).
5. ☐ Preencher **EX** se o produto exigir desdobramento por finalidade.
6. ☐ Selecionar a **Tributação Federal** apropriada (perfil pré-cadastrado de PIS/COFINS/IPI).
7. ☐ Selecionar a **Região Tributária ICMS ST**, quando aplicável.
8. ☐ Preencher o grupo **ICMS Normal — Saída** (Base, Alíquota, CST de Entrada e Saída, CSOSN se for Simples).
9. ☐ Conferir **Fundo Combate Pobreza** e **Crédito Outorgado** quando o estado exigir.
10. ☐ Conferir a aba **IVA** (CST, Classificação, Alíquotas CBS e IBS) para empresas já operando sob a Reforma.
11. ☐ Salvar.

---

## 🧮 Aba `Principal` — o que mora em cada grupo

| Grupo | O que preencher |
|---|---|
| **ICMS Normal — Saída** | Base/Alíquota Interno e Externo, CST Saída e Entrada, CSOSN, MVA, Modalidade BC, Redução BC, Código de Desoneração |
| **Fundo Combate Pobreza** | FCP Aliq., MVA FCP, FCP Aliq. Externa |
| **ICMS Crédito Outorgado — Saída** | Crédito Interno, Crédito Externo, Código do Crédito |
| **Tributação Federal** | PIS/COFINS (Entrada / Saída / Entrada Dev.) e IPI — **só vale se o combo do cabeçalho estiver vazio** |
| **SEFAZ REJEITOU** | NCM Inválido + texto do retorno da NF-e/NFC-e |

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
- Conferir se preencheu a **EX** quando o NCM exige desdobramento
- Conferir se o código está na Tabela NCM `121`
- Marcar **NCM Inválido** no grupo SEFAZ REJEITOU e colar o retorno para registro

### ❌ Descrição NCM não preencheu automaticamente
- A Tabela NCM `121` provavelmente está desatualizada — abrir chamado para a Hetosoft revisar
- Como contorno: preencher manualmente o campo e salvar

### ❌ Alíquota CBS configurada mas a NF-e não aplica
- Verificar se está usando o **CST CBS/IBS correto** (campo `CST` da aba IVA, não o CST da aba Principal)
- Verificar se a operação cai dentro do cronograma da Reforma já em vigor

### ❌ PIS/COFINS vindo errado mesmo com os campos da aba `Principal` preenchidos
- O combo **Tributação Federal** do cabeçalho **prevalece** sobre os campos da aba — se estiver preenchido, é ele quem manda

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
