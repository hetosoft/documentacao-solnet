# 📄 Cadastro de Condições de Pagamento - Sol.NET

## 🎯 Visão Geral

A **Condição de Pagamento** define **como** um valor é dividido no tempo: à vista, com entrada, parcelas iguais, parcelas manuais, com ou sem juros, com ou sem acréscimo/desconto. Cada condição é classificada por **Tipo** (Venda, Compra, Outros, Todos, ou combinações) e carrega:

- **Detalhes de Parcelas** — rateio percentual em cada parcela e intervalo de dias entre elas (soma das parcelas precisa ser **100%**).
- **Acréscimo/Desconto por Parcela Manual** — quando o cálculo varia conforme o número de parcelas escolhido pelo operador.
- **Formas de Pagamento permitidas** — lista de formas que podem ser usadas com esta condição (se nenhuma marcada, todas valem).
- **Validações e Permissões** — autorização de supervisor, valor mínimo de parcela, restrições de portador, etc.
- **Mobile/PDV** — comportamento no PDV (padrão, convênio) e mobile.

É um cadastro central do financeiro, junto com **Formas de Pagamento** (tela `7`). As condições aparecem em vendas, compras e demais lançamentos onde for preciso parcelar.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Condições de Pagamento |
| **Código (`F1`)** | `8` |

Abra a pesquisa universal (atalho `F1`) e digite **`8`** ou parte do nome **`Condições de Pagamento`**.

---

## 🧭 Estrutura da tela

A tela segue o padrão dos cadastros do Sol.NET, com duas áreas:

1. **Tab `Visualizar`** — grid de busca. As colunas `Tipo` e `Status (A Prazo)` aparecem decodificadas (texto, não número).
2. **Tab `Cadastrar`** — formulário com painel de identificação (`Descrição`, `Tipo`, `Juros/Multa`, `Acréscimo/Desconto`, status, flags) + sub-PageControl `pagDetalhes` com várias abas.

### Sub-abas do `Cadastrar` → `pagDetalhes`

| Sub-aba | Para quê serve |
|---------|----------------|
| **Parcelas** | Grid principal — rateio percentual de cada parcela e dias entre elas. Total **precisa fechar em 100%**. |
| **Parcelas Manual** | Configurações usadas quando o operador escolhe o número de parcelas na hora do lançamento. Define máximo de parcelas, vencimento fixo, regra da primeira parcela, primeira parcela em N dias. |
| **Acréscimo/Desconto(%) por Parcelas Manual** | Grid de acréscimo (ou desconto) específico por número de parcelas — todos positivos ou todos negativos. |
| **Formas de Pagamento** | Grid para marcar quais formas podem ser usadas com esta condição. Se **nenhuma** for marcada, **todas** as formas valem. |
| **Validação/Permissões** | Permissões e validações: pedir autorização supervisor, valor mínimo de parcela, desabilitar aplicação de desconto, não validar entrada mínima, aceitar acréscimo/desconto de pessoa, e restrições de portador. |
| **Mobile/PDV** | Comportamento no PDV (permitido, tipo Convênio: `Padrão` ou `Padrão Com Entrada`) e Mobile. |

---

## 📝 Campos principais (identificação)

| Label | Para quê serve |
|-------|----------------|
| **Descrição** | Nome amigável (obrigatório, único). |
| **Tipo** | Para que tipo de operação esta condição vale: `VENDA`, `COMPRA`, `OUTROS`, `TODOS`, `VENDA/OUTROS` ou `COMPRA/OUTROS`. |
| **Juros de Mora (%)** | Percentual aplicado em atraso. |
| **Multa de Mora (%)** | Percentual de multa em atraso. |
| **Para Hoje** | Marcador auto-calculado: condição equivale a "à vista" (1 parcela com `Dias entre Parc. = 0`). |
| **Com Entrada** | Marcador auto-calculado: tem entrada (mais de 1 parcela com primeira em `Dias = 0`). |
| **Parcela Manual** | Marcador auto-calculado: `Máximo Parcelas Manual > 0`. |
| **Acréscimo/Desconto (%)** | Percentual padrão aplicado ao total. Use negativo para desconto, positivo para acréscimo. |
| **Aplicar Acré/Desc** | Onde aplicar o acréscimo/desconto: `Sobre Movimento` ou `Sobre Valor do Item`. **Obrigatório quando há acréscimo/desconto.** |
| **Status** | Classificação: `A Vista` ou `A Prazo`. |
| **Form. Pagamento** | Marcador (auto-calculado a partir da aba `Formas de Pagamento`): indica que a condição **restringe** quais formas valem. |
| **Combinação Portador** | Permite combinar portadores. |
| **Acré/Desc Só no Financeiro** | Quando marcado, o acréscimo/desconto não impacta o movimento, só o financeiro. |
| **Juntar Parcelas (Atenção)** | Junta parcelas iguais. |
| **Acréscimo sobre entrada** | Aplica acréscimo também sobre a entrada. |
| **Parcela Gerencial** | Marca parcela como gerencial. |
| **Desconto (%)** | Desconto adicional configurado. |

### Aba `Parcelas Manual`

| Label | Para quê serve |
|-------|----------------|
| **Máximo Parcelas Manual** | Quantidade máxima de parcelas que o operador pode escolher. |
| **Primeira parcela para (Dias)** | Quantidade de dias para a primeira parcela. |
| **Vencimento com dia Fixo (se 30 dias)** | Mantém o dia fixo do mês quando o intervalo é 30 dias. |
| **Parcelas - Quantidade Padrão Um (1)** | Padrão começar com 1 parcela. |
| **Entrar Com Quantidade Parcela Vazio** | Começa com quantidade em branco. |

### Aba `Acréscimo/Desconto(%) por Parcelas Manual`

Grid com colunas:

- **Nº Parcela** — número da parcela
- **Acréscimo/Desconto (%)** — percentual a aplicar quando o operador escolhe esse número de parcelas

Botões: **Inserir**, **Atualizar**, **Deletar**, **Cancelar**.

### Aba `Formas de Pagamento`

Grid com checkbox por linha. Cada linha é uma forma de pagamento — marque a coluna de seleção para incluí-la nesta condição.

> ℹ️ Se **nenhuma** forma estiver marcada, a condição aceita **todas** as formas. Se pelo menos uma estiver marcada, a condição passa a **restringir** o uso (apenas as marcadas valem). O sistema seta o flag `Form. Pagamento` automaticamente para refletir isso.

### Aba `Validação/Permissões`

- **Portador** (combo): `(em branco)` / `Não Aceitar Portador (Boleto, Convênio, Carnê, Nota Promissória)` / `Não Aceitar Portador (Geral)` — restringe que tipos de portador podem ser usados com esta condição.
- **Sempre Pedir Autorização para Supervisor** — pede autorização sempre que essa condição for usada.
- **Mínimo Valor Parcela** — valor mínimo permitido por parcela.
- **Desabilitar Aplicação de Desconto (Zerar)** — desliga aplicação de desconto.
- **Não validar valor mínimo de Entrada** — pula a validação de entrada mínima.
- **Aceitar Acréscimo/Desconto de Pessoa** — usa o percentual configurado na pessoa (cliente/fornecedor).

### Aba `Mobile/PDV`

- **PDV** — permite uso desta condição no PDV.
- **Convênio** (combo): `(em branco)` / `Padrão` / `Padrão Com Entrada` — define o convênio padrão do PDV. **Apenas uma condição** por valor pode ter este flag — ao marcar `Padrão` em uma, o sistema desmarca em todas as outras automaticamente.
- **Mobile** — permite uso no mobile.

---

## ✅ Regras de validação automática (ao salvar)

A função `Validar` da tela aplica as seguintes regras de forma rígida; o salvamento é abortado caso alguma falhe:

1. **Detalhes não podem estar em edição** — feche a edição em curso nas abas de detalhes antes de salvar.
2. **Campos obrigatórios preenchidos** — Descrição, Tipo etc.
3. **`Parcelas` não pode estar vazio** — *"Gere os dados da condição de pagamento!"*.
4. **Rateio = 100%** — a soma dos percentuais das parcelas precisa dar exatamente `100`. Mensagem: *"Total rateio incorreto. Valor têm que ser igual a 100%!"*.
5. **Manual com 1 parcela exige `Dias entre Parc. > 0`** — *"Rateio incorreto. Dias entre Parcelas têm que ser maior 0"*.
6. **Manual com mais de 2 registros é bloqueado** — *"Rateio incorreto. Máximo permitido de registro 2 quando Máximo Parcelas Manual maior 0"*.
7. **`Parcelas - Quantidade Padrão Um(1)` e `Entrar Com Quantidade Parcela Vazio` mutuamente exclusivos** — não marque as duas.
8. **`Vencimento Fixo` ajustado automaticamente** — em condições "Para Hoje", "Parcela Manual" com `Máximo Parcelas = 1`, ou "Com Entrada" com menos de 3 parcelas no plano principal, o sistema desmarca e informa: *"Não é necessário Vencimento Fixo para Pagamento 'Para Hoje' ou Com apenas Uma Parcela!"*.
9. **Descrição única** — mensagem: *"Descrição (VALOR) Já Existe!"*.
10. **`Aplicar Acré/Desc` obrigatório quando há `Acréscimo/Desconto (%)`** — *"Aplicar Acré/Desc Obrigatorio! Se Acréscimo/Desconto(%) for diferente zero(0)"*.
11. **Acréscimo/Desconto Manual: tudo positivo ou tudo negativo** — não misture acréscimos e descontos no mesmo cadastro. Mensagem: *"Não Permitido! Existe Acréscimos e Descontos em Parcelas Manuais. Utilize somente um deles!"*.
12. **`Aplicar Acré/Desc` incompatível com `Acré/Desc Só no Financeiro`** — quando `Aplicar Acré/Desc` está marcado, `Acré/Desc Só no Financeiro` não pode estar.
13. **`Acréscimo sobre entrada`** — não permitido aplicar acréscimo sobre item quando a condição não aplica acréscimo sobre entrada.
14. **Inativar bloqueado para Padrão Convênio PDV** — *"Não permitido inativar condição de pagamento do tipo Padrão Convênio PDV!"*.
15. **Inativar bloqueado se usada como `Mudar Para Condição` em alguma Forma de Pagamento** — *"Não permitido inativar. A Condição de Pagamento é usada em configuração de Forma de Pagamento!"*.
16. **Quando a condição é usada como `Mudar Para Condição` em Forma de Pagamento, aquela forma precisa estar marcada na aba `Formas de Pagamento`** — caso contrário: *"Condição de Pagamento usada em configuração de Forma de Pagamento! Obrigatório selecionar a forma de pagamento ... Ou não usar configuração de forma de pagamento."*.
17. **Confirmação ao clonar** — se você está clonando, o sistema confirma antes de salvar.

---

## 🚫 Regras de exclusão

A exclusão é bloqueada quando a condição está em uso:

| Situação | Mensagem |
|----------|----------|
| Existe **movimento** com esta condição | *"Não permitido, Existe Movimento(s) com esta Condição de Pagamento!"* |

Quando a exclusão é autorizada, o sistema apaga em transação as tabelas auxiliares (`CP_DETALHE`, `CP_DETALHE_PARC`) junto com a condição.

Em qualquer caso de bloqueio, a condição deve ser **inativada** (com as ressalvas das validações 14 e 15 acima) em vez de excluída.

---

## 💡 Exemplos práticos

### Condição "À Vista" (Para Hoje)

1. Pesquisa `F1` → digite `8` → **Novo**.
2. **Descrição**: `À VISTA`
3. **Tipo**: `TODOS`
4. **Status**: `A Vista`
5. Na aba **Parcelas** → **Inserir**:
   - **Nº**: `1`
   - **Percentual**: `100`
   - **Dias entre Parc.**: `0`
   - **Atualizar**.
6. **Total rateado** deve mostrar `100`.
7. Salve.

O sistema marca **Para Hoje** automaticamente.

### Condição "30/60/90 dias" (3 parcelas iguais)

1. **Descrição**: `30/60/90 DIAS`
2. **Tipo**: `VENDA`
3. **Status**: `A Prazo`
4. Na aba **Parcelas**, insira três linhas:
   - `Nº 1` / `Percentual 33.33` / `Dias 30`
   - `Nº 2` / `Percentual 33.33` / `Dias 30`
   - `Nº 3` / `Percentual 33.34` / `Dias 30`
5. Confira que o **Total rateado** dá `100`.
6. Salve.

### Condição "Entrada + 2x" (com entrada)

1. **Descrição**: `ENTRADA + 2X`
2. **Tipo**: `VENDA`
3. **Status**: `A Prazo`
4. Na aba **Parcelas**:
   - `Nº 1` / `Percentual 33.33` / `Dias 0` ← entrada
   - `Nº 2` / `Percentual 33.33` / `Dias 30`
   - `Nº 3` / `Percentual 33.34` / `Dias 30`
5. **Total rateado** = `100`.
6. Salve. O sistema marca **Com Entrada** automaticamente.

### Condição "Manual" (operador escolhe nº de parcelas)

1. **Descrição**: `ATÉ 12X SEM ENTRADA`
2. **Tipo**: `VENDA`
3. **Status**: `A Prazo`
4. Na aba **Parcelas Manual** → **Máximo Parcelas Manual**: `12`. **Primeira parcela para (Dias)**: `30`.
5. Na aba **Parcelas**, insira **uma única linha**:
   - `Nº 1` / `Percentual 100` / `Dias entre Parc. 30`
6. (Opcional) Na aba **Acréscimo/Desconto(%) por Parcelas Manual**, configure acréscimos por número de parcelas (ex.: `Nº 4` → `+2%`, `Nº 6` → `+3%`, etc.). Lembre: **só positivos** ou **só negativos**.
7. (Opcional) Na aba **Formas de Pagamento**, marque apenas as formas permitidas (ex.: `CARTAO DE CREDITO`). Se deixar nenhuma marcada, todas valem.
8. Salve. O sistema marca **Parcela Manual** automaticamente.

---

## ❓ FAQ / Problemas comuns

**O sistema reclama "Total rateio incorreto. Valor têm que ser igual a 100%!".**
A soma dos percentuais das linhas na aba **Parcelas** precisa dar **exatamente 100**. Ajuste a última parcela com a sobra de centavos (ex.: `33.34` no lugar de `33.33`) para fechar.

**O que diferencia uma condição "Manual" das demais?**
A condição manual tem **Máximo Parcelas Manual > 0** e usa o número escolhido pelo operador na hora do lançamento. As demais (`Para Hoje`, `Com Entrada`) têm o número de parcelas fixo no cadastro.

**Por que misturar acréscimo e desconto na aba `Acréscimo/Desconto por Parcelas Manual` é bloqueado?**
Por consistência de regra: uma condição é "de juros" (acréscimo) **ou** "de desconto" — não as duas coisas. Para situações híbridas, crie duas condições separadas.

**Marquei algumas formas na aba `Formas de Pagamento` e outras ficaram excluídas. É isso mesmo?**
Sim. Marcou uma → restringiu. Quer voltar a aceitar todas? Desmarque todas as linhas — o flag `Form. Pagamento` é auto-ajustado pelo sistema.

**Configurei `Convênio = Padrão` aqui e perdi essa marcação em outra condição.**
Esperado: apenas **uma** condição pode ser `Padrão` (e apenas uma `Padrão Com Entrada`). Ao marcar em uma, o sistema **desmarca automaticamente em todas as outras** para garantir a unicidade.

**Tentei inativar e o sistema disse "usada em configuração de Forma de Pagamento".**
Alguma forma de pagamento aponta esta condição no campo `Mudar para Condição de Pagamento` (tela `7`, sub-aba PDV). Abra essa forma e remova o vínculo, ou ajuste o cadastro lá antes.

**Tentei excluir e o sistema bloqueou por movimentação.**
Há movimento (venda, compra, etc.) usando esta condição. Mantenha o cadastro e use a inativação (com as ressalvas das validações 14 e 15 acima).

**Por que algumas combinações desmarcam `Vencimento Fixo` sozinhas?**
A regra de vencimento fixo só faz sentido para condições parceladas com intervalo de 30 dias e mais de uma parcela. Em "Para Hoje" ou "1 parcela manual", o sistema desmarca e avisa.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Relação |
|------|:---:|---------|
| [Formas de Pagamento](documentacao_formas_pagamento.md) | `7` | Cada condição aceita um conjunto de formas; e formas podem forçar mudar para uma condição específica |
| [Portadores](documentacao_portadores.md) | `12` | Aba `Validação/Permissões` restringe quais portadores aceitam a condição |

---

## ⚠️ Limites desta documentação

Esta documentação foi construída a partir da inspeção direta do comportamento da tela no Sol.NET. **Não cobre**:

- **Regras automáticas que rodam dentro do banco de dados** ao salvar/alterar/excluir o registro — podem ajustar ou complementar o que está descrito aqui.
- **Cálculo detalhado de juros, multa e acréscimo/desconto na hora do lançamento** — esta documentação descreve apenas os campos do cadastro; o cálculo efetivo ocorre nas telas de venda, compra, pagamento e quitação.
- **Comportamento detalhado do `Convênio Padrão` no PDV** — o efeito desse flag é tratado na operação do PDV.
- **Variações por release** — versões mais novas do Sol.NET podem ter campos adicionais.

Para informações fora desse escopo, consulte o suporte Hetosoft.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 5.0 (refeito do zero descartando a documentação anterior)
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo Financeiro
