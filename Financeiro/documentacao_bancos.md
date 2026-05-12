# 📄 Cadastro de Bancos - Sol.NET

## 🎯 Visão Geral

O **Cadastro de Bancos** mantém a lista de instituições financeiras reconhecidas pelo Sol.NET. Cada banco é identificado pelo seu **código oficial** (o número de 3 dígitos atribuído pelo Banco Central / FEBRABAN — ex.: `001` Banco do Brasil, `237` Bradesco, `341` Itaú, `104` Caixa) e pela sua **descrição**.

É um cadastro base, pequeno e estável: serve de referência para todos os demais cadastros do financeiro que precisam apontar para um banco — em especial **Agências** (que pertencem a um banco) e **Contas Correntes** (que apontam para agência + banco). Por consequência, é também o ponto de partida para **Portadores** que emitem boletos, arquivos de remessa (CNAB) e integrações on-line, já que esses portadores são vinculados a contas correntes de bancos cadastrados aqui.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Bancos |
| **Código (`F1`)** | `9` |

Abra a pesquisa universal (atalho `F1`) e digite **`9`** ou parte do nome **`Bancos`**.

---

## 🧭 Estrutura da tela

A tela segue o padrão dos cadastros do Sol.NET, com duas áreas:

1. **Tab `Visualizar`** — grid de busca com as colunas `Descrição` e `Código`. Duplo clique numa linha leva direto à edição.
2. **Tab `Cadastrar`** — formulário enxuto, com apenas três campos.

---

## 📝 Campos

| Label | Obrigatório | Observação |
|-------|:---:|------------|
| **Descrição** | ✅ | Nome do banco, até 80 caracteres. Convertido para caixa alta automaticamente. Exige ao menos uma letra (não aceita só números/símbolos). |
| **Código (Fonte Banco Central)** | ✅ | Código oficial do banco, com 3 dígitos numéricos. Completa com zero à esquerda automaticamente. Aceita apenas números. Dica visível no campo: *"Ex: Bradesco - 237"*. |
| **Pessoa/Vinculo** | ◻️ | Opcional. Vincula o banco a uma pessoa do cadastro (geralmente a própria pessoa jurídica do banco). A pesquisa aberta neste campo já vem filtrada por pessoas marcadas como **Fornecedor**. Use o botão **(–)** para limpar a referência. |

> 💡 O **Código** é o mesmo número usado pelo mercado financeiro: `001` BB, `033` Santander, `104` Caixa, `237` Bradesco, `341` Itaú, `260` Nu Pagamentos, etc. Use sempre o código oficial — ele é o que aparece em boletos, arquivos CNAB e integrações bancárias e precisa bater com o que o convênio/banco espera.

---

## ✅ Regras de validação automática (ao salvar)

Antes de gravar, o sistema verifica:

1. **Campos obrigatórios preenchidos** — `Descrição` e `Código` não podem ficar em branco.
2. **Descrição com letra** — a `Descrição` precisa ter ao menos uma letra (não é aceito um nome só com números ou símbolos).
3. **Descrição única** — não é permitido cadastrar dois bancos com a mesma `Descrição`. Se houver duplicidade, o sistema bloqueia o salvamento e informa o registro existente.

Se alguma validação falhar, o salvamento é abortado e o sistema posiciona o cursor no campo problemático.

---

## 🚫 Exclusão

Não há validação específica feita pela tela na hora de excluir. Como o banco é referenciado por outros cadastros (em especial **Agências** e, por consequência, **Contas Correntes** e **Portadores**), a tentativa de excluir um banco que esteja em uso é bloqueada pelas regras do banco de dados — o sistema mostra uma mensagem indicando que existem registros vinculados.

A prática recomendada para bancos antigos que não devem mais ser usados é manter o cadastro e simplesmente **deixar de criar novas agências e contas correntes** vinculadas a ele.

---

## 💡 Exemplos práticos

### Cadastrar o Banco Bradesco

1. Pesquisa `F1` → digite `9` → abre o `Cadastro de Bancos`.
2. Clique em **Novo**.
3. **Descrição**: `BRADESCO`
4. **Código (Fonte Banco Central)**: `237`
5. (Opcional) Em **Pessoa/Vinculo**, abra a pesquisa e vincule a pessoa jurídica `BANCO BRADESCO S.A.` se ela já existir no cadastro de pessoas (como fornecedor).
6. Salve.

### Vincular o banco a uma pessoa do cadastro

Use **Pessoa/Vinculo** quando a empresa mantém o **banco** também como **fornecedor** no Sol.NET — por exemplo, quando entram títulos a pagar para o banco (anuidade de cartão, tarifas, débitos de empréstimo). Assim, ao consultar histórico, o banco aparece tanto no cadastro de Bancos quanto na sua pessoa correspondente.

Esse vínculo é **opcional** — operações de cobrança, conta corrente e portador funcionam normalmente sem ele.

---

## ❓ FAQ / Problemas comuns

**O sistema não deixa salvar dois bancos com o mesmo nome.**
Correto — `Descrição` precisa ser única. Se você está tentando cadastrar uma variação (ex.: `BRADESCO` e `BRADESCO PJ`), diferencie pela descrição.

**Posso usar qualquer número de 3 dígitos no `Código`?**
Tecnicamente sim, mas use sempre o **código oficial** do banco junto ao Banco Central / FEBRABAN. Esse número aparece em boletos, é exigido em arquivos CNAB e é o que valida a integração com APIs bancárias. Usar um código inventado vai funcionar no cadastro, mas pode falhar mais adiante na emissão de cobrança.

**Onde encontro a lista oficial de códigos?**
No site da FEBRABAN, do Banco Central, ou no rodapé de qualquer boleto/extrato bancário emitido pelo banco em questão.

**Preciso preencher `Pessoa/Vinculo`?**
Não. É opcional. Só vale a pena preencher se a sua empresa também movimenta esse banco como um **fornecedor** (lança títulos a pagar para o próprio banco). Caso contrário, deixe em branco.

**Excluí um banco e o sistema bloqueou.**
Provavelmente há agência, conta corrente ou portador vinculado. Se o banco realmente saiu de operação, basta deixar de criar novos vínculos — os históricos antigos continuam consultáveis.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Relação |
|------|:---:|---------|
| Agências | `10` | Cada agência pertence a um banco cadastrado aqui |
| Contas Correntes | `11` | Conta corrente é da agência → do banco |
| [Portadores](documentacao_portadores.md) | `12` | Portador de boleto / CNAB referencia conta corrente do banco |

---

## ⚠️ Limites desta documentação

Esta documentação foi construída a partir da inspeção direta do comportamento da tela no Sol.NET. **Não cobre**:

- **Regras automáticas que rodam dentro do banco de dados** ao salvar/alterar/excluir o registro — podem ajustar ou complementar o que está descrito aqui.
- **A lista oficial dos códigos de banco** — essa informação é mantida pela FEBRABAN / Banco Central e não pelo Sol.NET.
- **Variações por release** — versões mais novas do Sol.NET podem ter campos adicionais.

Para informações fora desse escopo, consulte o suporte Hetosoft.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 5.0 (refeito do zero descartando a documentação anterior)
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo Financeiro
