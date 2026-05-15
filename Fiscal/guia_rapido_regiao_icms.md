# ⚡ Guia Rápido — Região ICMS Saída

## 🎯 Para que serve

Cartão de referência para configurar e diagnosticar regras de Região ICMS Saída. Para a explicação completa, abra a [Documentação da Região ICMS Saída](documentacao_regiao_icms.md).

A tela **não armazena alíquotas** — ela liga **contexto** (loja + estado + regime + atividade + IE + tipo de item) a uma **Natureza de Operação**, que é quem traz os valores fiscais.

---

## 🚪 Como abrir

Pela pesquisa universal (`F1`), digite `Região ICMS Saída` ou o código `93`.

---

## 📋 Checklist — cadastrar uma Região ICMS

1. ☐ Definir o **Tipo**: `PESSOA` (regra pelo destinatário) ou `PRODUTO` (regra pelo produto/NCM).
2. ☐ Preencher **Descrição** (até 80 caracteres, obrigatório).
3. ☐ Para tipo `PRODUTO`: listar **CST ICMS Prod.** no formato `/CST1/CST2/`.
4. ☐ Para tipo `PRODUTO`: escolher **Operação** (Venda, Devolução, Transferência, Compra ou Regras 5–10).
5. ☐ Definir **Data Inicial / Data Final** se a regra tem vigência limitada (vazio = sem limite).
6. ☐ Em `Configurações`, clicar **Inserir** para adicionar uma linha de detalhe.
7. ☐ Definir filtros da linha: `Nº Lojas`, `Sigla Estados`, `Regime Tributário`, `Atividade Comercial`, `Indicador IE`, `Tipo de Item`. Deixar vazio ou `-1` = qualquer.
8. ☐ Duplo clique em **Descrição CFOP** para buscar a `Natureza de Operação` e vincular.
9. ☐ Conferir os campos pré-preenchidos pela Natureza (Base ICMS, Alíq., CST, CSOSN, CBS/IBS).
10. ☐ Marcar as flags **Manter CST/CSOSN**, **Manter Base/Aliq.** e/ou **Manter Red/Aliq. IBS/CBS** conforme o que a Região deve forçar sobre o NCM.
11. ☐ Clicar **Atualizar** para salvar a linha de detalhe.
12. ☐ Repetir os passos 6–11 para cada combinação de contexto que precisa de regra própria.
13. ☐ Salvar o cadastro.

---

## 🧮 Anatomia da tela

| Bloco | O que define |
|---|---|
| **Cabeçalho** (master) | Identidade da regra: Tipo, Descrição, CST ICMS Prod., Operação, vigência. |
| **Configurações** (detalhe, sub-CRUD com Inserir/Atualizar/Deletar/Cancelar) | Linhas com filtros de contexto + Natureza de Operação vinculada + flags de override. |

### Filtros do detalhe — curingas

| Campo | Curinga |
|---|---|
| Nº Lojas | Vazio |
| Sigla Estados | Vazio |
| Regime Tributário | Vazio / `-1` |
| Atividade Comercial | Vazio / `-1` |
| Indicador IE | Vazio / `-1` |
| Tipo de Item | Vazio / `-1` |

> 💡 **Linha mais específica vence.** O sistema ordena por especificidade decrescente e usa a primeira que combina.

### Flags "Manter" — o que cada uma força

| Flag | Sobrescreve do NCM |
|---|---|
| **Manter CST/CSOSN** | CST ICMS e CSOSN |
| **Manter Base/Aliq.** | Base de Cálculo e Alíquota ICMS |
| **Manter Red/Aliq. IBS/CBS** | CST CBS/IBS, alíquotas CBS / IBS UF / IBS Mun. e reduções |

O **CFOP** da Natureza sempre sobrescreve, independente das flags (a menos que a própria Natureza tenha `TP_FIXO` marcado e mantenha tudo).

---

## 🔁 Quando a Região ICMS é aplicada

1. O **Tipo de Movimento** (`37`) controla a execução via flags `EXECUTAR_REGIAO_ICMS` / `NAO_EXECUTAR_REGIAO_ICMS`.
2. Para cada item, o sistema procura a Região:
   - Primeiro pela **Região vinculada direto no produto**.
   - Senão, pelo **CST ICMS do NCM do produto**.
3. Dentro da Região, escolhe a **linha de detalhe** mais específica pelo contexto da operação.
4. CFOP da Natureza é aplicado; flags `Manter` decidem o resto.

---

## 🔥 Problemas comuns — soluções rápidas

### ❌ "Não Permitido! Natureza de Operação Já Usada em outra Região ICMS"
- Cada Natureza só pode estar em uma Região ICMS. Use uma Natureza diferente ou clone a Natureza atual com outro CFOP equivalente.

### ❌ "Não Permitido, CST ICMS para o Tipo 'PESSOA'!"
- Regras com Tipo `PESSOA` não aceitam `CST ICMS Prod.` preenchido. Mude o Tipo para `PRODUTO` ou limpe o CST.

### ❌ "Não Permitido, OPERAÇÃO para o Tipo 'PESSOA'!"
- Mesmo motivo: o combo `Operação` só faz sentido para Tipo `PRODUTO`.

### ❌ "CFOP não é de saída!" / "CFOP não é de entrada!" / "CFOP não é dentro do estado!" / "CFOP não é Exterior!"
- A Natureza vinculada tem CFOP incompatível com o `Tipo` (Entrada/Saída) ou `Selecione` (Dentro/Fora/Exterior) marcados no detalhe. Trocar a Natureza ou ajustar o cabeçalho da Natureza.

### ❌ Região não está sendo aplicada nas vendas
- Conferir, em ordem:
  - Tipo de Movimento tem `EXECUTAR_REGIAO_ICMS` ligado ou aceita Região por padrão?
  - Produto tem Região vinculada ou o NCM do produto tem CST listado em `CST ICMS Prod.`?
  - Vigência (Data Inicial / Final) cobre a data de hoje?
  - Existe linha de detalhe que combine com loja + UF + IE + atividade + regime + tipo de item da operação?

### ❌ Alíquota da Região não está prevalecendo sobre o NCM
- Confirmar que **Manter Base/Aliq.** está marcado na linha de detalhe usada
- Se a Natureza de Operação aplicada tem `TP_FIXO` próprio marcado, ela **mantém tudo** e a Região é ignorada para esse item

---

## 🔗 Telas relacionadas

- **Cadastro de NCM** (`21`) — fonte padrão dos valores fiscais por NCM
- **Natureza de Operação** (`36`) — pivô das linhas de detalhe
- **Região ICMS ST Saída** (`94`) — análogo para Substituição Tributária
- **Tipos de Movimento** (`37`) — controla se a Região é aplicada
- **Cadastro de Produtos** (`32`) — produto pode apontar para uma Região específica

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Configuradores fiscais e equipe de suporte
