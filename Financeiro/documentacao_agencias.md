# 📄 Cadastro de Agências - Sol.NET

## 🎯 Visão Geral

O **Cadastro de Agências** mantém a lista de agências bancárias usadas pela empresa. Cada agência **pertence a um banco** (cadastrado em **Bancos**) e é identificada pelo seu **número** (geralmente quatro dígitos) e, opcionalmente, pelo **dígito verificador**.

É o passo intermediário entre **Bancos** e **Contas Correntes**: uma conta corrente é sempre criada em uma agência específica, que por sua vez é de um banco. Não há como cadastrar uma conta corrente sem primeiro existir a agência onde ela está.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Agências |
| **Código (`F1`)** | `10` |

Abra a pesquisa universal (atalho `F1`) e digite **`10`** ou parte do nome **`Agências`**.

---

## 🧭 Estrutura da tela

A tela segue o padrão dos cadastros do Sol.NET, com duas áreas:

1. **Tab `Visualizar`** — grid de busca com as colunas `Descrição`, `Número Agência` e `Banco`. Quando a agência tem dígito verificador, ele é exibido junto com o número no formato `1234-5`. Duplo clique numa linha leva direto à edição.
2. **Tab `Cadastrar`** — formulário enxuto, com quatro campos.

---

## 📝 Campos

| Label | Obrigatório | Observação |
|-------|:---:|------------|
| **Descrição** | ✅ | Identificação da agência, até 80 caracteres. Convertido para caixa alta. Exige ao menos uma letra. Use um nome amigável que diferencie agências do mesmo banco (ex.: `BRADESCO — AG. CENTRO`, `BRADESCO — AG. SHOPPING`). |
| **Número Agência** | ✅ | Número oficial da agência (até 10 caracteres, apenas números). É esse número que aparece em boletos, arquivos CNAB e extratos. |
| **Dígito** | ◻️ | Dígito verificador da agência (até 20 caracteres). Algumas agências têm, outras não. Quando preenchido, é exibido junto com o número no formato `1234-5`. |
| **Banco** | ✅ | Banco ao qual esta agência pertence — lista preenchida a partir do **Cadastro de Bancos** (tela `9`). Se o banco ainda não existe, cadastre-o primeiro. |

---

## ✅ Regras de validação automática (ao salvar)

Antes de gravar, o sistema verifica:

1. **Campos obrigatórios preenchidos** — `Descrição`, `Número Agência` e `Banco` não podem ficar em branco.
2. **Descrição com letra** — a `Descrição` precisa ter ao menos uma letra.
3. **Número Agência único** — não é permitido cadastrar duas agências com o mesmo `Número Agência`. Se houver duplicidade, o sistema bloqueia o salvamento e informa o registro existente.

> ℹ️ A validação de duplicidade considera o **número da agência** isoladamente, sem combinar com o banco. Em ambientes com mais de um banco, prefira diferenciar pela **descrição** (incluindo o nome do banco) — assim, o usuário sempre identifica visualmente qual é qual mesmo que duas instituições usem o mesmo número.

Se alguma validação falhar, o salvamento é abortado e o sistema posiciona o cursor no campo problemático.

---

## 🚫 Exclusão

Não há validação específica feita pela tela na hora de excluir. Como a agência é referenciada por **Contas Correntes**, a tentativa de excluir uma agência que esteja em uso é bloqueada pelas regras do banco de dados — o sistema mostra uma mensagem indicando que existem registros vinculados.

Para agências que não devem mais ser usadas, a prática recomendada é manter o cadastro (preservando o histórico de contas correntes e movimentações que apontam para ela) e simplesmente **deixar de criar novas contas correntes** nela.

---

## 💡 Exemplos práticos

### Cadastrar uma agência do Bradesco

1. Pesquisa `F1` → digite `10` → abre o `Cadastro de Agências`.
2. Clique em **Novo**.
3. **Descrição**: `BRADESCO — AG. CENTRO`
4. **Número Agência**: `1234`
5. **Dígito**: `5` (se a agência usa dígito; deixe em branco se não)
6. **Banco**: selecione `BRADESCO` na lista.
7. Salve.

A agência aparecerá no grid de busca como `BRADESCO — AG. CENTRO | 1234-5 | BRADESCO`.

### Mesmo número em bancos diferentes

Se dois bancos têm uma agência com o mesmo número (ex.: agência `0001` no BB e agência `0001` no Itaú), a validação de duplicidade vai impedir cadastrar as duas. Nesse caso, ajuste o **Número Agência** para incluir uma diferença mínima permitida pelo banco (raramente acontece com números reais) ou converse com o suporte para entender se a configuração precisa de tratamento especial.

---

## ❓ FAQ / Problemas comuns

**Posso cadastrar a mesma agência (mesmo número) para dois bancos diferentes?**
Não — o sistema valida o número da agência sem combinar com o banco. Use descrições distintas e ajuste para diferenciar quando necessário.

**O dígito é obrigatório?**
Não. Algumas agências têm dígito verificador (o número que aparece após o hífen, como em `1234-5`), outras não. Quando o convênio do banco exige, preencha; caso contrário, deixe em branco.

**Por que a agência aparece como `1234-5` no grid mas eu cadastrei só o número?**
O grid concatena `Número Agência` + `-` + `Dígito` na exibição quando há dígito. Os dois campos continuam sendo gravados separados no cadastro.

**O banco não aparece na lista do campo `Banco`.**
Cadastre o banco antes em `Cadastro de Bancos` (tela `9`). A lista do campo `Banco` é populada a partir desse cadastro.

**Tentei excluir uma agência e o sistema bloqueou.**
Provavelmente existe uma conta corrente vinculada. Se a agência saiu de operação, mantenha o cadastro e apenas deixe de criar novas contas nela.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Relação |
|------|:---:|---------|
| [Bancos](documentacao_bancos.md) | `9` | Cada agência pertence a um banco cadastrado aqui |
| Contas Correntes | `11` | A conta corrente é da agência cadastrada aqui |
| [Portadores](documentacao_portadores.md) | `12` | Portador de boleto / CNAB usa conta corrente da agência |

---

## ⚠️ Limites desta documentação

Esta documentação foi construída a partir da inspeção direta do comportamento da tela no Sol.NET. **Não cobre**:

- **Regras automáticas que rodam dentro do banco de dados** ao salvar/alterar/excluir o registro — podem ajustar ou complementar o que está descrito aqui.
- **Lista oficial de agências** — esta informação é mantida pelo próprio banco, não pelo Sol.NET.
- **Variações por release** — versões mais novas do Sol.NET podem ter campos adicionais.

Para informações fora desse escopo, consulte o suporte Hetosoft.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 5.0 (refeito do zero descartando a documentação anterior)
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo Financeiro
