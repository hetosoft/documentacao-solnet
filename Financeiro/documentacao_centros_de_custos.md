# 📄 Cadastro de Centros de Custos - Sol.NET

## 🎯 Visão Geral

O **Centro de Custo** é a unidade de **rateio** das despesas e receitas da empresa: por departamento, projeto, filial, frota, obra, etc. É um cadastro em **árvore** (sintética / analítica) com a mesma lógica do [Plano de Contas](documentacao_plano_de_contas.md), e os dois andam juntos — geralmente cada lançamento financeiro carrega *plano de conta* + *centro de custo* para permitir leitura cruzada (o que aconteceu × onde aconteceu).

- **Sintética** — funciona como **agrupamento ou consolidado**. Não recebe lançamento — apenas soma as analíticas que estão sob ela.
- **Analítica** — é a **conta-folha**: é nela que efetivamente entram os lançamentos. Para ser analítica, ela aponta para uma sintética como `Conta Sintética` (superior) e tem um `Complemento` próprio.

O código é composto automaticamente:

```
Centro de Custo = Sintética [+ "." + Complemento (se Analítica)]
```

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Centros de Custos |
| **Código (`F1`)** | `15` |

Abra a pesquisa universal (atalho `F1`) e digite **`15`** ou parte do nome **`Centros de Custos`**.

---

> 🔎 **Na lista de busca** — as linhas de **contas sintéticas** aparecem em **cinza**, para diferenciá-las das analíticas. Os filtros próprios da lista são `Fixo/Variável`, `Natureza` e `Classificação`.

## 📝 Campos

### Identificação e hierarquia

| Label | Obrigatório | Observação |
|-------|:---:|------------|
| **Descrição** | ✅ | Nome amigável do centro, até 80 caracteres. |
| **Tipo de Conta** | ✅ | `Sintética (Agrupamento ou Consolidado)` ou `Analítica (Pode receber lançamentos)`. |
| **Conta Sintética** | ✅* | Código da conta-pai. Use o botão de pesquisa ou pressione tecla de localização para selecionar. |
| **Descrição** (do superior) | — | Mostrada ao lado, preenchida automaticamente a partir da `Conta Sintética` escolhida. Não digite. |
| **Conta Analítica** | ✅* | Complemento (até 3 caracteres) que entra após o `.` no código. Só vale para Analítica. |
| **Centro de Custo** | — | Código final, montado automaticamente: `Sintética` ou `Sintética.Complemento`. Não digite. |

*Observação:* o sistema deduz o tipo conforme o complemento: complemento preenchido → Analítica; vazio → Sintética. As regras de validação ajustam o tipo se houver inconsistência.

### Bloco `Analítica` (visível apenas quando `Tipo de Conta = Analítica`)

| Label | Obrigatório (se Analítica) | Opções |
|-------|:---:|--------|
| **Natureza** | ✅ | `Crédito` (0) ou `Débito` (1) |
| **Fixo/Variável** | ✅ | `Fixo` (0) ou `Variável` (1) |
| **Classificação** | ✅ | `Despesa` (0), `Receita` (1), `Investimento` (2), `Outros` (3) |

### Bloco `Extra`

| Label | Observação |
|-------|------------|
| **Conta Relatório** | Código auxiliar de relatório (texto livre). |
| **Superior** | Vínculo adicional a outro centro de custo (busca por pesquisa). |

---

## ✅ Regras de validação automática (ao salvar)

A função `Validar` da tela aplica as seguintes regras de forma rígida; o salvamento é abortado caso alguma falhe:

1. **Campos obrigatórios preenchidos** — `Descrição`, `Tipo de Conta` etc.
2. **Descrição única** — mensagem: *"Descrição (VALOR) Já Existe!"*.
3. **Centro de Custo único** — mensagem: *"Centro de Custo (VALOR) Já Existe!"*.
4. **Se `Conta Analítica` (complemento) preenchido, tipo precisa ser Analítica** — *"Esse tipo de conta só pode ser Analítica!"* (o sistema ajusta o tipo).
5. **Se `Conta Analítica` em branco, tipo precisa ser Sintética** — *"Esse tipo de conta só pode ser Sintética!"* (o sistema ajusta o tipo).
6. **Confirmação ao clonar** — se você está clonando, o sistema confirma antes de salvar.

### Edição restrita de hierarquia

Quando você abre **para alteração** um centro **sintético** que já tem analíticas filhas (códigos começando com `<centro>.`), os campos `Conta Sintética` e `Conta Analítica` ficam **bloqueados para edição** — evita quebrar a árvore.

Para mudar a estrutura, primeiro mova/exclua as analíticas filhas.

---

## 🚫 Regras de exclusão

A exclusão é bloqueada quando o centro de custo está em uso:

| Situação | Mensagem |
|----------|----------|
| Existe **Tipo de Movimento** vinculado a este centro | *"Não permitido, Existe Tipos de Movimento com este Centro de Custo!"* |
| Existe **lançamento de Contas PR (rateio)** com este centro | *"Não permitido, Existe Contas PR com este Centro de Custo!"* |

Em qualquer um desses casos, o centro deve ser **inativado** em vez de excluído.

---

## 🧰 Recursos extras

- **Visualizar Hierarquia** (menu de contexto): recarrega o grid filtrado pela árvore do centro selecionado (toda a sub-árvore sob a sintética).
- **Clonar Registro** (menu de contexto): cria uma cópia do centro selecionado para você ajustar.
- **Novo Registro** (menu de contexto / `F6` em modo pesquisa): abre uma janela secundária para inserir um novo centro sem sair da pesquisa.

---

## 💡 Exemplos práticos

### Estrutura típica

A estrutura é livre — depende da forma como a empresa organiza seus rateios. Exemplos comuns:

**Por departamento**:
```
1   ADMINISTRAÇÃO              (Sintética)
  1.001 RH                     (Analítica — Débito, Fixo, Despesa)
  1.002 CONTABILIDADE          (Analítica)
2   COMERCIAL                  (Sintética)
  2.001 LOJA SEDE              (Analítica)
  2.002 LOJA FILIAL            (Analítica)
3   PRODUÇÃO                   (Sintética)
```

**Por projeto/obra**:
```
1   OBRAS                      (Sintética)
  1.001 OBRA RUA A             (Analítica)
  1.002 OBRA RUA B             (Analítica)
```

### Criar uma sintética nova

1. Pesquisa `F1` → digite `15` → **Novo**.
2. **Descrição**: `ADMINISTRAÇÃO`
3. **Tipo de Conta**: `Sintética (Agrupamento ou Consolidado)`.
4. **Conta Sintética**: `1`.
5. **Conta Analítica**: (deixe vazio).
6. Salve.

### Criar uma analítica sob uma sintética

1. **Novo**.
2. **Descrição**: `RH`
3. **Tipo de Conta**: `Analítica (Pode receber lançamentos)`.
4. **Conta Sintética**: selecione `1` (`ADMINISTRAÇÃO`) pela pesquisa.
5. **Conta Analítica**: `001`.
6. O campo **Centro de Custo** mostra `1.001` automaticamente.
7. Bloco **Analítica** (agora visível):
   - **Natureza**: `Débito`
   - **Fixo/Variável**: `Fixo`
   - **Classificação**: `Despesa`
8. Salve.

### Inativar um centro antigo

1. Localize o centro na lista.
2. Abra para edição.
3. Marque a opção de inativar.
4. Salve.

---

## ❓ FAQ / Problemas comuns

**Mudei para Sintética mas o sistema reverteu para Analítica.**
A regra de consistência: se `Conta Analítica` (complemento) está preenchida, o sistema força Analítica. Limpe o complemento se quiser realmente Sintética.

**Por que não consigo editar a sintética?**
Provavelmente ela já tem analíticas filhas. O sistema bloqueia edição da hierarquia para preservar a árvore.

**No grid algumas linhas aparecem em cinza.**
São as **sintéticas**, marcadas para diferenciar visualmente das analíticas. Sintéticas não recebem lançamento.

**Tentei excluir e o sistema bloqueou.**
O centro está em uso por `Tipos de Movimento` ou por lançamento de `Contas PR`. Mantenha o cadastro e inative.

**Posso ter o mesmo centro de custo apontando para mais de um plano de contas?**
Sim — centro e plano são dimensões independentes. Cada lançamento carrega os dois separadamente. O Plano de Contas responde "o que" (natureza contábil); o Centro de Custo responde "onde" (departamento, projeto, filial).

**Qual a diferença entre Centro de Custo e Plano de Contas?**
Plano de Contas é a classificação **contábil** (Despesa de salários, Receita de vendas, etc.). Centro de Custo é a classificação **organizacional** (RH, Comercial, Loja A, etc.). O mesmo lançamento usa os dois ao mesmo tempo.

**Quando deixar de usar Centro de Custo?**
Algumas empresas, principalmente as menores, não usam centros de custo de maneira detalhada. Nesse caso, cadastre pelo menos uma analítica genérica (`GERAL`) para usar nos lançamentos.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Relação |
|------|:---:|---------|
| [Plano de Contas](documentacao_plano_de_contas.md) | `14` | Andam juntos em todo lançamento financeiro |
| [Formas de Pagamento](documentacao_formas_pagamento.md) | `7` | Aponta centro padrão na aba Controle De Cartão |
| [Portadores](documentacao_portadores.md) | `12` | Aponta centro padrão na aba Cob. Bancária |

---

## ⚠️ Limites desta documentação

Esta documentação foi construída a partir da inspeção direta do comportamento da tela no Sol.NET. **Não cobre**:

- **Regras automáticas que rodam dentro do banco de dados** ao salvar/alterar/excluir o registro — podem ajustar ou complementar o que está descrito aqui.
- **Comportamento detalhado em relatórios** — esta documentação trata apenas do cadastro; os relatórios que agregam por centro têm suas próprias regras.
- **Variações por release** — versões mais novas do Sol.NET podem ter campos adicionais.

Para informações fora desse escopo, consulte o suporte Hetosoft.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 5.0 (refeito do zero descartando a documentação anterior)
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo Financeiro
