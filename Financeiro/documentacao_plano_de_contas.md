# 📄 Cadastro de Plano de Contas - Sol.NET

## 🎯 Visão Geral

O **Plano de Contas** é a estrutura hierárquica que classifica todo lançamento financeiro e contábil da empresa. É um cadastro em **árvore**, com dois tipos de conta:

- **Sintética** — funciona como **agrupamento ou consolidado**. Não recebe lançamento — apenas soma as analíticas que estão sob ela.
- **Analítica** — é a **conta-folha**: é nela que efetivamente entram os lançamentos. Para ser analítica, a conta precisa apontar para uma sintética como `Conta Sintética` (superior) e ter um `Complemento` próprio.

A montagem do código segue o padrão:

```
Conta = Sintética [+ "." + Complemento (se Analítica)]
```

Ou seja, uma sintética `4` ("Contas de resultado") pode ter analíticas `4.001`, `4.002`, etc. — o código é composto automaticamente pelo sistema a partir dos campos `Conta Sintética` + `Conta Analítica` (complemento).

O Plano de Contas é referenciado por:

- **Configuração de Tipos de Movimento** (telas de fiscal/movimentação) — define que plano cada movimento alimenta;
- **Contas a Pagar/Receber** — cada título carrega um plano de conta;
- **Portadores, Formas de Pagamento, Caixa Geral** — apontam para plano padrão;
- **DRE / Relatórios contábeis** — agregam por sintética.

A tela também tem uma área específica para parametrização de **Holerite pelo Excel** (RH).

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Plano de Contas |
| **Código (`F1`)** | `14` |

Abra a pesquisa universal (atalho `F1`) e digite **`14`** ou parte do nome **`Plano de Contas`**.

---

> 🔎 **Na lista de busca** — filtros próprios são `Fixo/Variável`, `Natureza`, `Classificação` e busca por `Código ou Descrição Contábil`. Linhas de **contas sintéticas** aparecem em **cinza** no grid (para diferenciar das analíticas).

## 🧭 Sub-abas do formulário

- **`Principal`** — identificação, tipo (sintética/analítica), hierarquia (conta superior + complemento), agrupamento e atributos da analítica (natureza, fixo/variável, classificação).
- **`Holerite pelo Excel`** — parametrização de RH/folha (uso opcional; só preencha se a conta participa do fluxo de folha de pagamento via Excel).
- **`Holerite`** — opções de visualização e busca contábil.

---

## 📝 Campos da aba `Principal`

### Identificação e hierarquia

| Label | Obrigatório | Observação |
|-------|:---:|------------|
| **Descrição** | ✅ | Nome amigável da conta, até 80 caracteres. |
| **Tipo de Conta** | ✅ | `Sintética (Agrupamento ou Consolidado)` ou `Analítica (Pode receber lançamentos)`. |
| **Conta Sintética** | ✅* | Código da conta-pai. Use o botão de pesquisa ou pressione tecla de localização para selecionar de uma lista. |
| **Descrição Sintética** | — | Preenchida automaticamente a partir da `Conta Sintética` escolhida. Não digite aqui. |
| **Conta Analítica** | ✅* | Complemento (até 3 caracteres) que entra após o `.` no código da analítica. Só vale para tipo Analítica. |
| **Conta** | — | Código final, montado automaticamente: `Sintética` (se for sintética) ou `Sintética.Complemento` (se for analítica). Não digite aqui. |

*Observação:* o sistema deduz o tipo automaticamente conforme o complemento: complemento preenchido → analítica; vazio → sintética. As regras de validação ajustam o tipo se houver inconsistência.

### Agrupamento

| Label | Para quê serve |
|-------|----------------|
| **Grupo de Contas** | Classificação contábil clássica da conta. Opções: `Contas de ativo`, `Contas de passivo`, `Patrimônio líquido`, `Contas de resultado`, `Contas de compensação`, `Outras`. |
| **Data Inclusão/Alteração** | Data informativa. |

### Bloco `Analítica` (visível apenas quando `Tipo de Conta = Analítica`)

Estes campos só aparecem e ficam obrigatórios quando a conta é analítica:

| Label | Obrigatório (se Analítica) | Opções |
|-------|:---:|--------|
| **Natureza** | ✅ | `Crédito` (0) ou `Débito` (1) |
| **Fixo/Variável** | ✅ | `Fixo` (0) ou `Variável` (1) |
| **Classificação** | ✅ | `Despesa` (0), `Receita` (1), `Investimento` (2), `Outros` (3) |

### Bloco `Extra`

| Label | Observação |
|-------|------------|
| **Cod. Relatório** | Código auxiliar de relatório (texto livre). |
| **Superior** | Vinculação adicional a outra conta (busca via pesquisa). |

---

## 📝 Campos da aba `Holerite pelo Excel`

Use apenas se a conta deve participar do fluxo de **importação de Holerite pelo Excel** do módulo RH. Quando o **Cód. Referência** é preenchido, todos os demais campos desta aba ficam **obrigatórios** e a conta precisa ser **Analítica**.

| Label | Observação |
|-------|------------|
| **Cód. Referência Ex: /10/202/** | Lista de códigos do Excel separados e cercados por `/`. O sistema completa com `/` no início e no fim automaticamente. |
| **Descrição Contábil** | Descrição usada no Holerite. |
| **Tipo de Conta** | Link com `Tipos de Contas PR` (tela `82`). |
| **Centro de Custo** | Link com `Centros de Custos` (tela `15`). |
| **Dia** | Dia de referência do lançamento. |
| **Operação** | `+ CRÉDITO` (0) ou `- DÉBITO` (1). |
| **Nível** | Nível hierárquico no Holerite: `Nível 1`, `Nível 2` ou `Nível 3`. |
| **Próximo Mês** | Marcar quando o lançamento deve cair no próximo mês. |
| **OBS** | Observação livre. |
| **Registro** | Tipo de registro de folha: `Normal`, `Férias` ou `Décimo Terceiro`. |

---

## 📝 Campos da aba `Holerite`

| Label | Observação |
|-------|------------|
| **Código ou Descrição Contábil** | Filtro de busca por código contábil ou descrição contábil — usado em conjunto com a pesquisa principal. |
| **Mostrar Todos** | Quando marcado, expande a listagem para incluir todas as contas (ignora o filtro do Holerite). |

---

## ✅ Regras de validação automática (ao salvar)

A função `Validar` da tela aplica as seguintes regras de forma rígida; o salvamento é abortado caso alguma falhe:

1. **Quando `Cód. Referência` preenchido — conta precisa ser Analítica** — *"Não Permitido! Holerite pelo Excel com conta Sintética!"*. Além disso, `Descrição Contábil`, `Centro de Custo`, `Dia`, `Operação`, `Nível` e `Registro` ficam obrigatórios.
2. **Campos obrigatórios preenchidos** — `Descrição`, `Tipo de Conta` etc.
3. **Descrição única** — mensagem: *"Descrição (VALOR) Já Existe!"*.
4. **Código único** — mensagem: *"Conta (VALOR) Já Existe!"*.
5. **Se `Conta Analítica` (complemento) preenchido, tipo precisa ser Analítica** — *"Esse tipo de conta só pode ser Analítica!"* (o sistema ajusta o tipo).
6. **Se `Conta Analítica` em branco, tipo precisa ser Sintética** — *"Esse tipo de conta só pode ser Sintética!"* (o sistema ajusta o tipo).
7. **Confirmação ao clonar** — se você está clonando, o sistema confirma antes de salvar.

### Edição restrita de hierarquia

Quando você abre **para alteração** uma conta **sintética** que já tem analíticas filhas (códigos começando com `<conta>.`), os campos `Conta Sintética` e `Conta Analítica` ficam **bloqueados para edição**. Isso evita quebrar a árvore quando outras contas dependem desta.

Para realmente mudar a estrutura, primeiro mova/exclua as analíticas filhas — depois edite a sintética.

---

## 🚫 Regras de exclusão

A exclusão é bloqueada quando o plano de conta está em uso. A tela verifica duas tabelas antes de excluir:

| Situação | Mensagem |
|----------|----------|
| Existe **Tipo de Movimento** vinculado a este plano | *"Não permitido, Existe Tipos de Movimento com este Plano de Conta!"* |
| Existe **lançamento de Contas PR (rateio)** com este plano | *"Não permitido, Existe Contas PR com este Plano de Conta!"* |

Em qualquer um desses casos, o plano deve ser **inativado** em vez de excluído, preservando o histórico.

---

## 🧰 Recursos extras

### Visualizar Hierarquia

No menu de contexto do grid (clique com botão direito), opção **Visualizar Hierarquia** — recarrega o grid filtrado pela árvore daquela conta (toda a sub-árvore sob a sintética selecionada).

### Clonar Registro

No menu de contexto, opção **Clonar Registro** — cria uma cópia da conta selecionada para você ajustar o que mudar.

### Salvar / Ajustes do Grid

No menu de contexto: **Salvar** persiste a largura atual das colunas. **Ajustes** permite escolher quais colunas mostrar no grid.

---

## 💡 Exemplos práticos

### Estrutura típica (convenção contábil)

A estrutura segue a tradição contábil brasileira (não é regra do sistema, é convenção):

```
1   Contas de ativo                  (Sintética)
  1.001 Caixa                        (Analítica — Crédito, Variável, Despesa, no exemplo)
  1.002 Bancos                       (Analítica)
2   Contas de passivo                (Sintética)
  2.001 Fornecedores                 (Analítica)
3   Patrimônio líquido               (Sintética)
4   Contas de resultado              (Sintética)
  4.001 Receita de Vendas            (Analítica — Crédito, Variável, Receita)
  4.002 Despesa com Salários         (Analítica — Débito, Fixo, Despesa)
```

### Criar uma conta sintética nova

1. Pesquisa `F1` → digite `14` → **Novo**.
2. **Descrição**: `CONTAS DE RESULTADO`
3. **Tipo de Conta**: `Sintética (Agrupamento ou Consolidado)`.
4. **Conta Sintética**: `4` (digite ou use a pesquisa — para sintéticas de nível superior, é só o número raiz).
5. **Conta Analítica**: (deixe vazio — sintética não tem complemento).
6. **Grupo de Contas**: `Contas de resultado`.
7. Salve.

### Criar uma conta analítica nova sob uma sintética

1. **Novo**.
2. **Descrição**: `RECEITA DE VENDAS`
3. **Tipo de Conta**: `Analítica (Pode receber lançamentos)`.
4. **Conta Sintética**: selecione `4` (`CONTAS DE RESULTADO`) pela pesquisa.
5. **Conta Analítica**: `001` (complemento — 1 a 3 dígitos).
6. O campo **Conta** mostra `4.001` automaticamente.
7. Bloco **Analítica** (agora visível):
   - **Natureza**: `Crédito`
   - **Fixo/Variável**: `Variável`
   - **Classificação**: `Receita`
8. **Grupo de Contas**: `Contas de resultado`.
9. Salve.

### Inativar uma conta antiga

1. Localize a conta na lista.
2. Abra para edição.
3. Marque a opção de inativar.
4. Salve.

Inativar é o caminho recomendado para contas com histórico (já que a exclusão é bloqueada por dependências).

---

## ❓ FAQ / Problemas comuns

**Mudei o tipo para Sintética mas o sistema reverteu para Analítica.**
A regra de consistência: se `Conta Analítica` (complemento) está preenchida, o sistema força o tipo para Analítica. Limpe o complemento se quiser mesmo Sintética.

**Por que não consigo editar a conta sintética?**
Provavelmente ela já tem analíticas filhas. Para preservar a árvore, o sistema bloqueia edição dos campos de hierarquia (Conta Sintética e Complemento) quando existem outras contas que apontam para essa.

**Tentei excluir e o sistema bloqueou.**
A conta está em uso por `Tipos de Movimento` ou por `Contas a Pagar/Receber` (lançamento de rateio). Mantenha o cadastro e inative.

**No grid algumas linhas aparecem em cinza — o que significa?**
São as **contas sintéticas**, marcadas em cinza para diferenciar visualmente das analíticas. Sintéticas não recebem lançamento.

**Quando preencher a aba `Holerite pelo Excel`?**
Apenas se sua empresa importa o holerite pelo Excel no Sol.NET e essa conta participa do fluxo. Preencher o `Cód. Referência` ativa todos os outros campos como obrigatórios — não preencha "por garantia" se você não usa esse fluxo, porque vai te impedir de salvar.

**Por que os marcadores `Natureza`, `Fixo/Variável` e `Classificação` só aparecem para Analítica?**
Sintéticas são apenas agrupadores — não fazem sentido carregar esses atributos. As analíticas, sim, precisam dessas marcações para alimentar relatórios e o DRE corretamente.

**Posso usar um código fora da convenção (`1`, `2`, `3`, `4`)?**
Pode. O sistema aceita qualquer estrutura de código numérico. A convenção `1` = Ativo, `2` = Passivo, etc. é histórica e ajuda na leitura, mas não é uma regra do sistema.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Relação |
|------|:---:|---------|
| Centros de Custos | `15` | Apontado pelo plano (aba Holerite pelo Excel) e usado junto com plano em lançamentos |
| Tipos de Contas PR | `82` | Apontado pelo plano (aba Holerite pelo Excel) |
| [Formas de Pagamento](documentacao_formas_pagamento.md) | `7` | Aponta plano padrão (aba Controle De Cartão) |
| [Portadores](documentacao_portadores.md) | `12` | Aponta plano padrão (aba Cob. Bancária) |
| Configuração DRE | `131` | Configura agrupamento DRE por plano |

---

## ⚠️ Limites desta documentação

Esta documentação foi construída a partir da inspeção direta do comportamento da tela no Sol.NET. **Não cobre**:

- **Regras automáticas que rodam dentro do banco de dados** ao salvar/alterar/excluir o registro — podem ajustar ou complementar o que está descrito aqui.
- **Importação de Holerite pelo Excel** propriamente dita — esta documentação descreve apenas a configuração feita por conta; o fluxo de importação é tratado em outra tela.
- **Cálculo do DRE** — esta documentação trata apenas do cadastro do plano; a montagem do DRE é feita em `Configuração DRE` (tela `131`).
- **Variações por release** — versões mais novas do Sol.NET podem ter campos adicionais.

Para informações fora desse escopo, consulte o suporte Hetosoft.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 5.0 (refeito do zero descartando a documentação anterior)
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo Financeiro
