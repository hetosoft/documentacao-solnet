# 📄 Cadastro de Caixa Geral - Sol.NET

## 🎯 Visão Geral

O **Caixa Geral** é o "container" lógico onde entra e sai dinheiro no Sol.NET: caixa físico do PDV, caixa de loja, caixa banco (representando uma conta corrente bancária), caixa de cartões etc. Cada caixa pode estar:

- **Associado a uma Conta Corrente** — quando representa uma conta bancária e participa de conciliação;
- **Vinculado a uma Empresa específica** — para multi-empresa;
- **Classificado por tipo de uso** — Caixa PDV, Caixa Resumo, Conciliação Bancária, Conciliação de Cartões, etc.;
- **Agrupado** em até cinco grupos (`Grupo 1` a `Grupo 5`) para relatórios consolidados;
- **Com regra de fechamento** — por `Período` ou por `Turno`.

O Caixa Geral é referenciado por:

- **Formas de Pagamento** (tela `7`) — cada regra de Controle de Cartão aponta para um Caixa Geral;
- **Portadores** (tela `12`) — cada portador é associado a um caixa;
- **Operações de Caixa Geral** (tela `302`) — onde os lançamentos efetivamente acontecem;
- **Quitação** (tela `303`) — onde o caixa é selecionado para quitação de títulos;
- **Cadastro de Usuários** — para definir permissões de quem pode operar cada caixa.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Caixa Geral |
| **Código (`F1`)** | `13` |

Abra a pesquisa universal (atalho `F1`) e digite **`13`** ou parte do nome **`Caixa Geral`**.

---

## 🧭 Estrutura da tela

A tela tem duas áreas principais:

1. **Tab `Visualizar`** — grid de busca. A coluna **Permite Fechamento** aparece decodificada (`PERÍODO` ou `TURNO`). Em **modo pesquisa** (quando o caixa é selecionado por outra tela), só aparecem os caixas que o **usuário logado** tem permissão de uso.
2. **Tab `Cadastrar`** — formulário com duas sub-abas:
   - **`Principal`** — identificação, conta associada, empresa, tipos e fechamento.
   - **`Usuário`** — grid de leitura mostrando quais usuários têm acesso a este caixa e que permissões cada um tem (Selecionar, Padrão, Consultar, Quitar, Transferir, Cheque). **A vinculação é feita no Cadastro de Usuários**, não aqui.

---

## 📝 Campos da aba `Principal`

### Identificação

| Label | Obrigatório | Observação |
|-------|:---:|------------|
| **Descrição** | ✅ | Nome do caixa (até 80 caracteres). |
| **Conta Corrente** | ◻️ | Conta corrente bancária associada (link com **Contas Correntes**, tela `11`). Preencha quando o caixa representa um banco/conta. Use o botão **(–)** para limpar a referência. |
| **Permite Fechamento** | ◻️ | Define a regra de fechamento: `Período` ou `Turno`. Em branco = sem fechamento configurado. |
| **Descrição da Loja** | ◻️* | Empresa proprietária do caixa. Fica obrigatório quando `Empresa de Quitação = do Caixa` está marcado (ver validação 2). |
| **Caixas Agrupados** | ◻️ | Agrupa este caixa em um dos cinco grupos (`Grupo 1` a `Grupo 5`) para relatórios consolidados. |
| **Conciliação Bancária Tipos de Previsão (Ex: /APLIC.INVEST/APLICACAO FACIL/)** | ◻️ | Lista de tipos de previsão para conciliação bancária, separados e cercados por `/`. O sistema completa com `/` no início e no fim automaticamente. |

### Grupo `Fechar./Turno Atual`

Estes campos guardam o **último fechamento/turno** registrado. Geralmente são atualizados automaticamente pelas operações de fechamento — só edite manualmente quando precisar ajustar um histórico.

| Label | Observação |
|-------|------------|
| **Data** | Data do último fechamento/turno. |
| **Hora** | Hora do último fechamento/turno. |
| **Fechar./Turno** | Código do último fechamento/turno. |

### Grupo `Tipos` (checkboxes)

Cada flag liga um comportamento específico em outra parte do sistema. Marque conforme o tipo de operação que este caixa representa:

| Label | Para quê serve |
|-------|----------------|
| **Caixas PDVS** | Este caixa é usado pelo PDV. |
| **Não Visível em Quitação** | Esconde este caixa nas listas de quitação. |
| **Mobile** | Caixa usado por operação mobile. |
| **Caixas Resumo** | Caixa de "resumo" (agregação de outros caixas). |
| **Entrada Sangria PDVS** | Caixa de destino para a sangria do PDV. |
| **É Banco** | Marca este caixa como representando uma conta bancária. Geralmente combinado com `Conta Corrente` preenchida. |
| **Conciliação Bancária** | Habilita a operação de conciliação bancária neste caixa. |
| **Editar Compensado** | Permite editar lançamentos já compensados. |
| **Empresa de Quitação = do Caixa** | A empresa da quitação é forçada para a empresa deste caixa. **Exige** que `Descrição da Loja` esteja preenchida. |
| **Fechamento Cego (Servidor)** | Operação de fechamento cego (sem ver os valores anteriores) feita no servidor. |
| **Aba Conferência de Caixa** | Habilita a aba de conferência de caixa. |
| **Conciliação Cartões** | Habilita a operação de conciliação de cartões neste caixa. |

---

## 📝 Aba `Usuário` (grid de permissões)

Grid de leitura mostrando os **usuários** que têm acesso a este caixa e que ações cada um pode executar. As colunas:

| Coluna | Significado |
|--------|-------------|
| **Código** | Código do usuário |
| **Login** | Login do usuário |
| **Sel.** | Usuário tem acesso a este caixa |
| **Padrão** | Este é o caixa padrão do usuário (apenas um por usuário) |
| **Consultar** | Pode consultar |
| **Quitar** | Pode quitar |
| **Transferir** | Pode transferir |
| **Cheque** | Pode operar cheques |

> ℹ️ **As permissões são definidas no Cadastro de Usuários**, não nesta tela. Aqui o grid existe apenas para visualizar a configuração atual.

---

## ✅ Regras de validação automática (ao salvar)

A função `Validar` da tela aplica as seguintes regras de forma rígida; o salvamento é abortado caso alguma falhe:

1. **Campos obrigatórios preenchidos** — em especial `Descrição`.
2. **`Empresa de Quitação = do Caixa` exige `Descrição da Loja`** — se você marcar o checkbox `Empresa de Quitação = do Caixa`, o campo `Descrição da Loja` precisa ter uma empresa selecionada. Mensagem: *"Obrigatório Selecionar Empresa! 'Empresa de Quitação = do Caixa'"*.
3. **Descrição única** — mensagem: *"Descrição (VALOR) Já Existe!"*.

Se alguma validação falhar, o salvamento é abortado e o sistema posiciona o cursor no campo problemático.

---

## 🚫 Exclusão

Não há validação específica feita pela tela na hora de excluir. Como o caixa é referenciado por **Portadores**, **Formas de Pagamento** (aba `Controle De Cartão`), **lançamentos no Caixa Geral** e demais movimentações, a tentativa de excluir um caixa em uso é bloqueada pelas regras do banco de dados.

Para caixas que não devem mais ser usados, a prática recomendada é **inativar** o cadastro (preservando o histórico).

---

## 🔐 Comportamento em modo pesquisa

Quando este cadastro é aberto **como pesquisa** por outra tela (ex.: tela de quitação pedindo para escolher um caixa), o sistema mostra apenas os caixas que o **usuário logado** tem permissão de uso (configurado no Cadastro de Usuários). Em modo de manutenção normal (abrir pela pesquisa `F1` → `13`), todos os caixas aparecem para edição/criação.

---

## 💡 Exemplos práticos

### Caixa do PDV principal

1. Pesquisa `F1` → digite `13` → **Novo**.
2. **Descrição**: `PDV LOJA SEDE — CAIXA 01`
3. **Permite Fechamento**: `Turno`
4. **Descrição da Loja**: `LOJA SEDE` (selecione a empresa)
5. Marque **Caixas PDVS**.
6. (Opcional) Marque **Empresa de Quitação = do Caixa** se quiser forçar que toda quitação feita neste caixa seja da empresa selecionada.
7. Salve.

### Caixa "Banco" para conciliação

1. **Novo**.
2. **Descrição**: `BANCO BRADESCO — CC 1234-5`
3. **Conta Corrente**: selecione a conta corrente correspondente.
4. **Permite Fechamento**: `Período`
5. Marque **É Banco** e **Conciliação Bancária**.
6. (Opcional) Preencha **Conciliação Bancária Tipos de Previsão** com os códigos de previsão usados nas aplicações financeiras (ex.: `/APLIC.INVEST/CDB/`).
7. Salve.

Esse caixa entra na operação de conciliação bancária (cruzando o extrato bancário com os lançamentos do sistema).

### Caixa de cartões (conciliação)

1. **Novo**.
2. **Descrição**: `CARTÕES — VISA`
3. Marque **Conciliação Cartões**.
4. Marque **Editar Compensado** se a equipe precisa ajustar lançamentos já compensados.
5. Salve.

Use este caixa nas regras de Controle de Cartão de **Formas de Pagamento** (tela `7`, sub-aba `Controle De Cartão`, campo `Caixa`).

### Inativar um caixa antigo

1. Localize na aba **Visualizar**.
2. Abra para edição.
3. Marque a opção de inativar o cadastro.
4. Salve.

---

## ❓ FAQ / Problemas comuns

**O caixa que cadastrei não aparece quando outro usuário tenta usá-lo.**
Provavelmente esse usuário não tem permissão de uso no caixa. Vá ao **Cadastro de Usuários**, abra o usuário e marque o caixa na aba/lista de Caixas Permitidos. O modo pesquisa só mostra os caixas autorizados ao usuário logado.

**Marquei "Empresa de Quitação = do Caixa" mas o sistema não deixa salvar.**
Você precisa também selecionar uma empresa em **Descrição da Loja** — sem isso, o sistema não tem como "forçar" a empresa na quitação.

**Posso usar o mesmo caixa em várias lojas?**
Pode. Se você quiser que ele valha em todas as lojas, deixe **Descrição da Loja** em branco e **não** marque `Empresa de Quitação = do Caixa`. Para restringir a uma empresa, selecione e marque.

**Para que serve `Caixas Agrupados`?**
Para agrupar caixas em até cinco grupos (`Grupo 1` a `Grupo 5`) em relatórios consolidados. Por exemplo, todos os caixas físicos das lojas em `Grupo 1`, todos os caixas banco em `Grupo 2`, e assim por diante.

**Posso editar manualmente `Data`, `Hora` e `Fechar./Turno` do último fechamento?**
Pode, mas evite. Esses campos são atualizados automaticamente pela operação de fechamento e edição manual pode causar inconsistência com os movimentos. Só ajuste para corrigir um histórico — e idealmente com acompanhamento do suporte.

**Tentei excluir e o sistema bloqueou.**
O caixa está referenciado por portadores, formas de pagamento, lançamentos ou movimentações. Mantenha o cadastro e inative.

**O que é "Fechamento Cego (Servidor)"?**
O operador faz o fechamento sem ver os valores prévios — o cálculo é feito pelo servidor. Útil para impedir conferência prévia (controle interno mais rígido).

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Relação |
|------|:---:|---------|
| [Contas Correntes](documentacao_contas_correntes.md) | `11` | Conta associada (campo `Conta Corrente`) |
| [Formas de Pagamento](documentacao_formas_pagamento.md) | `7` | Forma de pagamento aponta caixa na aba `Controle De Cartão` |
| [Portadores](documentacao_portadores.md) | `12` | Portador é associado a um caixa |
| Cadastro de Usuários | — | Define permissões por caixa (aba `Usuário` desta tela é só leitura) |

---

## ⚠️ Limites desta documentação

Esta documentação foi construída a partir da inspeção direta do comportamento da tela no Sol.NET. **Não cobre**:

- **Regras automáticas que rodam dentro do banco de dados** ao salvar/alterar/excluir o registro — podem ajustar ou complementar o que está descrito aqui.
- **Operações de Caixa Geral propriamente ditas** (lançamentos, fechamento, transferência) — esta documentação descreve apenas o cadastro; a operação é tratada na tela `302`.
- **Conciliação Bancária** e **Conciliação de Cartões** — esta doc descreve apenas os flags que habilitam; o fluxo de conciliação propriamente dito ocorre em outras telas.
- **Permissões por caixa por usuário** — gerenciadas no Cadastro de Usuários.
- **Variações por release** — versões mais novas do Sol.NET podem ter campos adicionais.

Para informações fora desse escopo, consulte o suporte Hetosoft.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 5.0 (refeito do zero descartando a documentação anterior)
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo Financeiro
