# 📄 Cadastro de Contas Correntes - Sol.NET

## 🎯 Visão Geral

O **Cadastro de Contas Correntes** mantém a lista das contas bancárias movimentadas pela empresa. Cada conta corrente pertence a uma **agência** (que por sua vez é de um **banco**), tem um **número de conta** com seu eventual **dígito verificador** e, opcionalmente, um **titular**, uma **data de abertura** e um **tipo de conta** (individual, conjunta, jurídica ou geral).

É o cadastro que fecha a tríade base do financeiro (**Banco → Agência → Conta Corrente**) e é referenciado por **Portadores** (boletos, cobrança, integrações bancárias) e por toda movimentação que envolve crédito ou débito bancário.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Contas Correntes |
| **Código (`F1`)** | `11` |

Abra a pesquisa universal (atalho `F1`) e digite **`11`** ou parte do nome **`Contas Correntes`**.

---

## 🧭 Estrutura da tela

A tela segue o padrão dos cadastros do Sol.NET, com duas áreas:

1. **Tab `Visualizar`** — grid de busca com as colunas `Descrição`, `Numero`, `Banco` e `Agência`. Quando a conta tem dígito verificador, ele aparece concatenado ao número no formato `1234-5`. Duplo clique numa linha leva direto à edição.
2. **Tab `Cadastrar`** — formulário com os campos abaixo.

---

## 📝 Campos

| Label | Obrigatório | Observação |
|-------|:---:|------------|
| **Descrição** | ✅ | Identificação amigável da conta, até 256 caracteres. Convertida para caixa alta. Exige ao menos uma letra. Use um nome que diferencie contas do mesmo banco (ex.: `BRADESCO — CC PRINCIPAL`, `BRADESCO — CC PAGAMENTOS`). |
| **Agência** | ✅ | Combo populado a partir do **Cadastro de Agências** (tela `10`). Ao selecionar uma agência, o campo **Banco** é preenchido automaticamente. |
| **Banco** | — | Somente leitura. Preenchido automaticamente quando você seleciona a **Agência**, mostrando o banco daquela agência. Existe para conferência visual; não é digitado. |
| **Número C/C** | ✅ | Número da conta corrente, até 20 caracteres (apenas números). É o número que aparece em boletos, arquivos CNAB e extratos bancários. |
| **Dígito** | ◻️ | Dígito verificador da conta (até 5 caracteres no banco de dados). Algumas contas têm, outras não. Quando preenchido, é exibido junto com o número no formato `1234-5`. |
| **Abertura** | ◻️ | Data de abertura da conta. Pode ficar em branco. |
| **Tipo de Conta** | ◻️ | Lista fixa com quatro opções: **INDIVIDUAL**, **CONJUNTA**, **JURIDICA**, **GERAL**. |
| **Titular** | ◻️ | Nome do titular da conta, até 80 caracteres. Aceita apenas letras (sem números). Convertido para caixa alta. |
| **Código OFX** | ◻️ | Código identificador da conta usado no arquivo OFX (formato padrão para importação de extratos bancários eletrônicos). Preencha quando você costuma importar o extrato da conta via OFX e o banco usa um código próprio para identificá-la no arquivo. |
| **Permitir Remessa de Cheque** | ◻️ | Marque quando esta conta pode ser usada na operação de remessa de cheques. |

> ℹ️ **Tamanho do `Código OFX`** — a tela aceita até 20 caracteres, mas o banco de dados comporta até 50. Para uso normal a limitação de 20 é mais do que suficiente, já que o código costuma ser curto.

---

## ✅ Regras de validação automática (ao salvar)

Antes de gravar, o sistema verifica:

1. **Campos obrigatórios preenchidos** — `Descrição`, `Agência` e `Número C/C` não podem ficar em branco.
2. **Descrição com letra** — a `Descrição` precisa ter ao menos uma letra.

> ℹ️ **Não há validação de duplicidade na tela.** É possível cadastrar duas contas correntes com a mesma descrição ou com o mesmo número — o sistema não bloqueia. Em ambientes com várias contas, fica por conta do operador manter as descrições distintas para não confundir.

Se alguma validação falhar, o salvamento é abortado e o sistema posiciona o cursor no campo problemático.

---

## 🚫 Exclusão

Não há validação específica feita pela tela na hora de excluir. Como a conta corrente é referenciada por **Portadores** e por todas as movimentações financeiras (pagamentos, recebimentos, baixas), a tentativa de excluir uma conta em uso é bloqueada pelas regras do banco de dados — o sistema mostra uma mensagem indicando que existem registros vinculados.

Para contas correntes que não devem mais ser usadas, a prática recomendada é manter o cadastro (preservando o histórico) e parar de movimentar — eventualmente o cadastro pode ser inativado pela opção de inativo do próprio registro.

---

## 💡 Exemplos práticos

### Cadastrar uma conta corrente

1. Pré-requisito: o **Banco** (tela `9`) e a **Agência** (tela `10`) já devem estar cadastrados. Se a agência ainda não existe, cadastre-a primeiro.
2. Pesquisa `F1` → digite `11` → abre o `Cadastro de Contas Correntes`.
3. Clique em **Novo**.
4. **Descrição**: `BRADESCO — CC PRINCIPAL`
5. **Agência**: selecione `BRADESCO — AG. CENTRO` na lista. O campo **Banco** é preenchido sozinho com `BRADESCO`.
6. **Número C/C**: `123456`
7. **Dígito**: `7` (se houver)
8. **Abertura**: (opcional) data em que a conta foi aberta
9. **Tipo de Conta**: escolha conforme o caso (ex.: `JURIDICA` para CNPJ da empresa)
10. **Titular**: nome do titular conforme aparece no contrato bancário (ex.: `EMPRESA EXEMPLO LTDA`)
11. **Código OFX**: preencha se for importar extratos OFX desta conta e o banco usar um código próprio (consulte o suporte do banco)
12. **Permitir Remessa de Cheque**: marque se esta conta for usada em remessa de cheques
13. Salve.

A conta aparecerá no grid de busca como `BRADESCO — CC PRINCIPAL | 123456-7 | BRADESCO | BRADESCO — AG. CENTRO`.

### Inativar uma conta antiga

Quando a conta sai de operação (encerrada pelo banco) mas o histórico de movimentações precisa ser preservado:

1. Localize a conta na aba **Visualizar**.
2. Abra para edição.
3. Marque a opção de inativar o cadastro.
4. Salve.

A conta deixa de aparecer em listas usadas para novos lançamentos, mas o histórico continua consultável.

---

## ❓ FAQ / Problemas comuns

**Por que o campo `Banco` não permite digitar?**
Porque ele é preenchido automaticamente pela **Agência** escolhida (cada agência pertence a um banco). Para mudar o banco, troque a agência.

**A agência que eu quero não aparece na lista de `Agência`.**
Cadastre a agência antes em `Cadastro de Agências` (tela `10`). Se ela já existe e mesmo assim não aparece, confira se não está inativada.

**Posso cadastrar duas contas correntes com o mesmo número?**
Sim — a tela não bloqueia duplicidade. Mas é desaconselhado: causa confusão na operação. Diferencie pela `Descrição` e mantenha a regra de que cada conta real do banco corresponde a um único cadastro.

**O `Tipo de Conta` afeta alguma regra?**
É um classificador para consulta e relatórios. As quatro opções fixas (`INDIVIDUAL`, `CONJUNTA`, `JURIDICA`, `GERAL`) refletem categorias bancárias usuais — escolha a que corresponde à conta no banco.

**Quando preencher `Código OFX`?**
Apenas se você costuma **importar extratos OFX** desta conta no Sol.NET e o banco usa um código próprio para identificá-la no arquivo OFX (alguns bancos usam o próprio número da conta, outros usam um identificador específico). Em caso de dúvida, faça uma importação de teste — se o sistema não reconhecer a conta, preencha o código indicado pelo banco no arquivo.

**O que é "Permitir Remessa de Cheque"?**
Habilita a conta para uso na operação de remessa de cheques. Se você não usa esse fluxo, deixe desmarcado — o cadastro funciona normalmente para todas as outras operações.

**Tentei excluir e o sistema bloqueou.**
Há portador, movimentação ou lançamento vinculado. Mantenha o cadastro (inative se necessário) — o histórico antigo continua consultável.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Relação |
|------|:---:|---------|
| [Bancos](documentacao_bancos.md) | `9` | Pai da hierarquia (banco → agência → conta) |
| [Agências](documentacao_agencias.md) | `10` | Conta corrente é da agência cadastrada aqui |
| [Portadores](documentacao_portadores.md) | `12` | Portador de boleto / cobrança usa a conta corrente |

---

## ⚠️ Limites desta documentação

Esta documentação foi construída a partir da inspeção direta do comportamento da tela no Sol.NET. **Não cobre**:

- **Regras automáticas que rodam dentro do banco de dados** ao salvar/alterar/excluir o registro — podem ajustar ou complementar o que está descrito aqui.
- **Importação de extratos OFX** — esta documentação descreve apenas o campo `Código OFX`; a operação de importação propriamente dita é tratada em outra tela.
- **Operação de remessa de cheques** — esta documentação descreve apenas o flag `Permitir Remessa de Cheque`; o fluxo da remessa é tratado em outra tela.
- **Variações por release** — versões mais novas do Sol.NET podem ter campos adicionais.

Para informações fora desse escopo, consulte o suporte Hetosoft.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 5.0 (refeito do zero descartando a documentação anterior)
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo Financeiro
