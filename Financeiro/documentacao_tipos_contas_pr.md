# 📄 Cadastro de Tipos de Contas PR - Sol.NET

## 🎯 Visão Geral

O **Tipo de Conta PR** é a classificação **gerencial** dos títulos a pagar e a receber — uma camada própria do financeiro, separada do [Plano de Contas](documentacao_plano_de_contas.md) (que é contábil) e dos [Centros de Custos](documentacao_centros_de_custos.md) (que é organizacional).

É um cadastro em **árvore** (sintética / analítica), igual à estrutura do Plano de Contas e Centros de Custos:

- **Sintética** — funciona como **agrupamento ou consolidado**. Não recebe lançamento.
- **Analítica** — é a **conta-folha** que efetivamente classifica os títulos.

O código é composto automaticamente:

```
Tipo de Conta = Sintética [+ "." + Complemento (se Analítica)]
```

Cada Tipo de Conta PR analítico carrega **atributos de Natureza, Fixo/Variável e Classificação** (Despesa/Receita/Investimento/Outros) — os mesmos do Plano de Contas — e pode opcionalmente apontar para um **Plano de Contas** e **Centro de Custo** padrão (aba `Contabilidade RH`), além de parâmetros de RH (Dia, Operação, Nível, Próximo Mês).

O Tipo de Conta PR é referenciado por:

- **[Pagar e Receber](documentacao_pagar_e_receber.md)** (tela `301`) — cada título carrega um `Tipo de Conta PR` (campo `Tipo de Conta`)
- **[Plano de Contas](documentacao_plano_de_contas.md)** (tela `14`) — quando o plano tem aba Holerite preenchida, aponta para um Tipo de Conta PR
- **[Formas de Pagamento](documentacao_formas_pagamento.md)** (tela `7`) — restrição de inativação por uso em tipos de documento

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Tipos de Contas PR |
| **Código (`F1`)** | `82` |

Abra a pesquisa universal (atalho `F1`) e digite **`82`** ou parte do nome **`Tipos de Contas PR`**.

---

## 🧭 Estrutura da tela

A tela segue o padrão dos cadastros do Sol.NET:

1. **Tab `Visualizar`** — grid de busca com filtros próprios (`Fixo/Variável`, `Natureza`, `Classificação`, busca por `Código ou Descrição Contábil`, marcador `Contabilidade RH`). Linhas de **contas sintéticas** aparecem em **cinza** no grid.
2. **Tab `Cadastrar`** — formulário organizado em sub-abas:
   - **`Principal`** — identificação, tipo (sintética/analítica), hierarquia e atributos da analítica
   - **`Contabilidade RH`** — vínculo com plano de contas, centro de custo e parametrização de RH (uso opcional)
   - **`Hetosoft`** — opções internas da Hetosoft (visível **apenas** quando o operador está logado como usuário Hetosoft)

---

## 📝 Campos da aba `Principal`

### Identificação e hierarquia

| Label | Obrigatório | Observação |
|-------|:---:|------------|
| **Descrição** | ✅ | Nome amigável (até 80 caracteres). |
| **Contabilidade RH** | ◻️ | Marcador na busca para filtrar tipos que participam de contabilidade RH. |
| **Contábil** | ◻️ | Filtro na busca por código/descrição contábil. |
| **Tipo de Conta** (radio) | ✅ | `Sintética (Agrupamento ou Consolidado)` ou `Analítica (Pode receber lançamentos)`. |
| **Conta Sintética** | ✅* | Código da conta-pai. Use pesquisa ou tecla de localização. |
| **Descrição** (do superior) | — | Preenchida automaticamente a partir da `Conta Sintética` escolhida. |
| **Conta Analítica** | ✅* | Complemento (até 3 caracteres) que entra após o `.` no código. Só vale para Analítica. |
| **Tipo de Conta** (código final) | — | Código final, montado automaticamente: `Sintética` ou `Sintética.Complemento`. |

### Bloco `Analítica` (visível apenas quando `Tipo de Conta = Analítica`)

| Label | Obrigatório (se Analítica) | Opções |
|-------|:---:|--------|
| **Natureza** | ✅ | `Crédito` (0) ou `Débito` (1) |
| **Fixo/Variável** | ✅ | `Fixo` (0) ou `Variável` (1) |
| **Classificação** | ✅ | `Despesa` (0), `Receita` (1), `Investimento` (2), `Outros` (3) |

---

## 📝 Campos da aba `Contabilidade RH`

Use apenas se este tipo de conta participa de **contabilidade RH** (folha de pagamento). Quando o **Cód. Referência** ou a **Descrição Contábil** estão preenchidos, todos os demais campos desta aba ficam **obrigatórios**.

| Label | Observação |
|-------|------------|
| **Cód. Referência Ex: /10/202/** | Lista de códigos separados e cercados por `/`. O sistema completa com `/` no início e no fim automaticamente. |
| **Descrição Contábil** | Descrição contábil. |
| **Plano de Contas** | Vínculo com [Plano de Contas](documentacao_plano_de_contas.md) (tela `14`) — busca por pesquisa. |
| **Centro de Custo** | Vínculo com [Centros de Custos](documentacao_centros_de_custos.md) (tela `15`) — busca por pesquisa. |
| **Dia** | Dia de referência do lançamento. |
| **Operação** | `+ CRÉDITO` (0) ou `- DÉBITO` (1). |
| **Nível** | Nível hierárquico no RH: `Nível 1`, `Nível 2` ou `Nível 3`. |
| **Próximo Mês** | Marcar quando o lançamento deve cair no próximo mês. |
| **OBS** | Observação livre. |
| **Registro** | Tipo de registro de folha: `Normal`, `Férias` ou `Décimo Terceiro`. |

---

## 📝 Aba `Hetosoft` (uso interno Hetosoft)

A aba aparece **apenas** quando o operador está logado como usuário Hetosoft. Em uso normal de cliente ela fica oculta.

Campos:

- **Movimento** — referência a um movimento padrão para clonagem (busca por pesquisa).
- **SAC - Sistema** — vincula este tipo de conta a um sistema Hetosoft: `Sol.NET`, `Sol Server`, `Sol.NET Delivery`, `Sol.NET Integração`.
- **SAC - Financeiro** — flag `Não Validar Financeiro` (uso interno).

Para clientes essas opções não têm efeito. **Se você é cliente, ignore esta aba.**

---

## ✅ Regras de validação automática (ao salvar)

A função de validação aplica:

1. **Quando `Cód. Referência` OU `Descrição Contábil` preenchidos**, todos os campos da aba `Contabilidade RH` ficam obrigatórios: `Descrição Contábil`, `Plano de Contas`, `Centro de Custo`, `Dia`, `Operação`, `Nível`.
2. **Campos obrigatórios preenchidos** — `Descrição`, `Tipo de Conta` etc.
3. **Descrição única** — mensagem: *"Descrição (VALOR) Já Existe!"*.
4. **Código único** — mensagem: *"Tipo de Conta (VALOR) Já Existe!"*.
5. **Se `Conta Analítica` (complemento) preenchido, tipo precisa ser Analítica** — *"Esse tipo de conta só pode ser Analítica!"* (o sistema ajusta o tipo).
6. **Se `Conta Analítica` em branco, tipo precisa ser Sintética** — *"Esse tipo de conta só pode ser Sintética!"* (o sistema ajusta o tipo).
7. **Confirmação ao clonar** — se você está clonando, o sistema confirma antes de salvar.

### Edição restrita de hierarquia

Quando você abre **para alteração** um tipo **sintético** que já tem analíticas filhas (códigos começando com `<tipo>.`), os campos `Conta Sintética` e `Conta Analítica` ficam **bloqueados para edição** — evita quebrar a árvore.

---

## 🚫 Exclusão

Não há validação específica feita pela tela na hora de excluir. Como o tipo é referenciado por **títulos a pagar e receber**, pelo **Plano de Contas** (no vínculo de Holerite) e por **Formas de Pagamento** (na restrição de inativação), a tentativa de excluir um tipo em uso é bloqueada pelas regras do banco de dados.

Para tipos que não devem mais ser usados, a prática recomendada é **inativar** o cadastro.

---

## 🧰 Recursos extras

- **Visualizar Hierarquia** (menu de contexto): recarrega o grid filtrado pela árvore do tipo selecionado.
- **Clonar Registro** (menu de contexto): cria uma cópia do tipo selecionado para você ajustar.
- **Novo Registro** (menu de contexto / `F6` em modo pesquisa): abre uma janela secundária para inserir um novo tipo sem sair da pesquisa.

---

## 💡 Exemplos práticos

### Estrutura típica

Exemplo de árvore que separa as principais categorias gerenciais de uma empresa comercial:

```
1   RECEITAS                       (Sintética)
  1.001 VENDA À VISTA              (Analítica — Crédito, Variável, Receita)
  1.002 VENDA A PRAZO              (Analítica)
2   DESPESAS OPERACIONAIS          (Sintética)
  2.001 ALUGUEL                    (Analítica — Débito, Fixo, Despesa)
  2.002 ENERGIA                    (Analítica — Débito, Variável, Despesa)
  2.003 SALÁRIOS                   (Analítica — Débito, Fixo, Despesa)
3   IMPOSTOS                       (Sintética)
  3.001 ICMS                       (Analítica)
  3.002 ISS                        (Analítica)
4   INVESTIMENTOS                  (Sintética)
  4.001 EQUIPAMENTOS               (Analítica — Débito, Variável, Investimento)
```

### Criar uma sintética nova

1. Pesquisa `F1` → digite `82` → **Novo**.
2. **Descrição**: `DESPESAS OPERACIONAIS`
3. **Tipo de Conta**: `Sintética (Agrupamento ou Consolidado)`.
4. **Conta Sintética**: `2`.
5. **Conta Analítica**: (deixe vazio).
6. Salve.

### Criar uma analítica sob uma sintética

1. **Novo**.
2. **Descrição**: `ALUGUEL`
3. **Tipo de Conta**: `Analítica (Pode receber lançamentos)`.
4. **Conta Sintética**: selecione `2` (`DESPESAS OPERACIONAIS`) pela pesquisa.
5. **Conta Analítica**: `001`.
6. O campo **Tipo de Conta** mostra `2.001` automaticamente.
7. Bloco **Analítica** (agora visível):
   - **Natureza**: `Débito`
   - **Fixo/Variável**: `Fixo`
   - **Classificação**: `Despesa`
8. (Opcional) Aba `Contabilidade RH` → preencha apenas se este tipo participa de folha de pagamento.
9. Salve.

### Inativar um tipo antigo

1. Localize na aba **Visualizar**.
2. Abra para edição.
3. Marque a opção de inativar.
4. Salve.

---

## ❓ FAQ / Problemas comuns

**Qual a diferença entre Tipo de Conta PR, Plano de Contas e Centro de Custo?**
São **três dimensões independentes** que classificam um título financeiro:
- **Plano de Contas** — classificação **contábil** (Receita de Vendas, Despesa com Salários, etc.)
- **Centro de Custo** — classificação **organizacional** (onde aconteceu: Loja A, Departamento X)
- **Tipo de Conta PR** — classificação **gerencial dos títulos a pagar/receber** (Aluguel, Energia, Salários, etc.)

Cada lançamento financeiro pode carregar os três simultaneamente para permitir análises cruzadas.

**Mudei para Sintética mas o sistema reverteu para Analítica.**
A regra de consistência: se `Conta Analítica` (complemento) está preenchida, o sistema força Analítica. Limpe o complemento se quiser realmente Sintética.

**Por que não consigo editar a sintética?**
Provavelmente ela já tem analíticas filhas. O sistema bloqueia edição da hierarquia para preservar a árvore.

**No grid algumas linhas aparecem em cinza.**
São as **sintéticas**, marcadas para diferenciar visualmente das analíticas. Sintéticas não recebem lançamento.

**Tentei excluir e o sistema bloqueou.**
O tipo está em uso por títulos (Pagar e Receber), Plano de Contas (vínculo Holerite) ou Forma de Pagamento. Mantenha o cadastro e inative.

**Quando preencher a aba `Contabilidade RH`?**
Apenas se sua empresa usa a contabilidade de RH integrada e este tipo participa do fluxo de folha. Preencher `Cód. Referência` ou `Descrição Contábil` ativa toda a aba como obrigatória — **não preencha "por garantia"** se você não usa esse fluxo, porque vai impedir o salvamento.

**A aba `Hetosoft` aparece para mim, mas não consigo entender os campos.**
Essa aba só é visível em ambiente de teste/suporte Hetosoft. Se você é cliente final, ignore — não vai aparecer no seu ambiente de produção.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Relação |
|------|:---:|---------|
| [Pagar e Receber](documentacao_pagar_e_receber.md) | `301` | Cada título carrega um Tipo de Conta PR |
| [Plano de Contas](documentacao_plano_de_contas.md) | `14` | Plano pode apontar Tipo de Conta PR padrão na aba Holerite |
| [Centros de Custos](documentacao_centros_de_custos.md) | `15` | Apontado pelo Tipo de Conta na aba Contabilidade RH |
| [Formas de Pagamento](documentacao_formas_pagamento.md) | `7` | Vínculo restringe inativação |

---

## ⚠️ Limites desta documentação

Esta documentação foi construída a partir da inspeção direta do comportamento da tela no Sol.NET. **Não cobre**:

- **Regras automáticas que rodam dentro do banco de dados** ao salvar/alterar/excluir o registro.
- **Comportamento detalhado em relatórios** — a doc trata apenas do cadastro; relatórios que agregam por Tipo de Conta PR têm suas próprias regras.
- **Aba `Hetosoft`** — uso interno; não detalhado.
- **Variações por release** — versões mais novas do Sol.NET podem ter campos adicionais.

Para informações fora desse escopo, consulte o suporte Hetosoft.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 5.0 (refeito do zero descartando a documentação anterior)
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo Financeiro
