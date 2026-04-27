---
title: "Cashback PDV - Sol.NET"
permalink: /Movimentacao/cashback_pdv/
---
# 📄 Cashback PDV - Sol.NET

## 🎯 Visão Geral

O **Cashback PDV** permite que vendas finalizadas no PDV gerem crédito de cashback para o cliente, calculado automaticamente a partir de regras configuráveis por empresa, portador e forma de pagamento. O cashback acumula como saldo da pessoa beneficiária e pode ser utilizado em vendas futuras.

A geração ocorre **em background**, executada pelo **Monitor de Integração** após a finalização do movimento — o operador do PDV não precisa de nenhuma ação adicional para creditar o cashback.

### Características Principais

- ✅ **Geração automática** após a finalização da venda no PDV
- ✅ **Regras flexíveis** por empresa, portador e forma de pagamento
- ✅ **Limite e validade** configuráveis por regra
- ✅ **Pessoa Beneficiária**: o cashback pode ser creditado para uma pessoa diferente da que comprou
- ✅ **Filtro por pessoa**: opção de só gerar cashback quando a pessoa estiver marcada como elegível
- ✅ **Agrupamento opcional**: consolidar todo o cashback do cliente em um único título a receber
- ✅ **Estorno e devolução tratados**: regras específicas evitam saldo inconsistente

---

## 🧰 Pré-requisitos

Antes de o sistema gerar cashback para uma venda, é necessário que **todos** os itens abaixo estejam atendidos:

1. **Tipo de movimento marcado como `É PDV`** com a opção `Gerar Cashback PDV` ativada (ver [Configuração no Tipo de Movimento](#-configuração-no-tipo-de-movimento)).
2. **Pelo menos uma regra de cashback** cadastrada e válida para a combinação `Empresa × Portador × Forma de Pagamento` da venda (ver [Cadastro de Regras de Cashback](#-cadastro-de-regras-de-cashback)).
3. **Data de emissão do movimento** maior ou igual à data informada em `Contas/Mov. a partir de` na regra (campo obrigatório).
4. Se a regra estiver com `Validar tag pessoa` marcada, a pessoa do movimento precisa ter `Utilizar Cashback` ativado em seu cadastro.
5. **Monitor de Integração** em execução (é ele quem processa os movimentos pendentes).

> ⚠️ **Importante (upgrade):** Movimentos do PDV anteriores ao release que introduziu o Cashback PDV são marcados como “já processados” na atualização do banco e **não geram cashback retroativo**. Apenas vendas novas, finalizadas com o tipo de movimento configurado para gerar cashback, entram no fluxo.

---

## ⚙️ Configuração

A configuração envolve três telas, todas acessíveis pela **pesquisa universal (F1)** — abra pela pesquisa e digite parte do nome da tela.

### 🛒 Configuração no Tipo de Movimento

Tela: **Cadastro de Tipos de Movimento** (abra pela pesquisa F1 e digite parte do nome).

Na aba `Itens` → grupo `Outros`, marque:

- **`Gerar Cashback PDV`** → habilita a geração automática de cashback nas vendas finalizadas com este tipo.

#### Restrições validadas pelo sistema

- O tipo precisa estar marcado como **`É PDV`**. Caso contrário, ao salvar, o sistema exibe a mensagem:
  > *Não permitido `Gerar Cashback PDV`, Obrigatório ser `É PDV`!*
- A opção é **mutuamente exclusiva** com `Gerar Pontos` / `Usar Pontos` no mesmo grupo `Outros`. Caso ambos estejam ativos, o sistema bloqueia com a mensagem:
  > *Não permitido os Dois Ativado! `Gerar Cashback PDV` e `Tipo Pontos`*

> 💡 Crie tipos de movimento dedicados (por exemplo, `Venda PDV — Com Cashback`) para deixar claro quais operações geram crédito.

---

### 🏷️ Cadastro de Regras de Cashback

Tela: **Cadastro de Regras de Cashback** (abra pela pesquisa F1 e digite parte do nome).

#### Campos da regra (cabeçalho)

| Campo | Descrição |
|-------|-----------|
| **Descrição** | Identificação da regra. |
| **Empresa(s)** | Empresas em que a regra se aplica (seleção múltipla). |
| **Contas/Mov. a partir de** | Data inicial de validade da regra. **Campo obrigatório**. Aplica-se a contas/movimentos com data de emissão maior ou igual a esta data. |
| **Percentual** | Percentual de cashback (ex.: `5,00%`). |
| **Limite** | Valor máximo de cashback que pode ser gerado por movimento (em moeda). Use `0,00` para desabilitar o limite. |
| **Validade** | Quantidade de dias que o cliente terá para usar o cashback gerado. Use `0` para validade indeterminada. |
| **Gerar Cashback para Contas Vencidas** | Permite gerar cashback mesmo quando a conta foi paga após o vencimento. O botão `?` ao lado da data inicial detalha esse comportamento. |
| **Gerar Cashback com base no Movimento** | Quando marcado, o cashback é gerado já na finalização do movimento, sem aguardar a quitação financeira. |
| **Validar tag pessoa** | Quando marcado, a regra **só** se aplica se a pessoa do movimento estiver com `Utilizar Cashback` ativo no cadastro. Use para limitar cashback a um grupo específico de clientes. |

#### Detalhes da regra — Portador e Forma de Pagamento

Cada regra precisa de pelo menos um detalhe combinando **Portador** e (opcionalmente) **Forma de Pagamento**:

- **Portador**: o portador (carteira/banco) usado na venda.
- **Forma de Pagamento**: o sistema aceita regras vinculadas apenas ao portador, sem exigir forma de pagamento específica. Informe a forma quando quiser percentuais distintos por modalidade (ex.: crédito × débito).

> 💡 Para variar o percentual conforme a forma de pagamento, crie **uma regra para cada combinação** que precisa de tratamento próprio.

---

### 👤 Cadastro de Pessoas — Aba `Cashback`

Tela: **Cadastro de Pessoas** (abra pela pesquisa F1 e digite parte do nome). Após selecionar a pessoa, abra a aba **`Cashback`**.

| Campo / Botão | Descrição |
|---------------|-----------|
| **Utilizar Cashback** | Marca a pessoa como elegível ao cashback quando alguma regra estiver com `Validar tag pessoa` ativo. Sem isso, regras com `Validar tag pessoa` ignoram esta pessoa. |
| **Pessoa Beneficiária** | Outra pessoa cadastrada que **receberá** o cashback gerado pelas compras desta. Útil em B2B para creditar o representante, ou em famílias/grupos onde o saldo deve ficar centralizado. Se vazio, o cashback é creditado na própria pessoa do movimento. |
| **Mostrar Extrato Cashback** | Botão que abre o **Extrato Cashback** já filtrado pela pessoa selecionada (detalhes em *Consulta de Extrato* mais adiante). |

---

### 🛠️ Configuração geral (sistema)

Tela: **Configuração** (abra pela pesquisa F1 e digite parte do nome). Aba **`Crédito`**.

- **Agrupar Cashback** *(checkbox)* — Hint: *“Gerar novo cashback na mesma contasPR aberta.”*
  - **Marcado**: cada nova venda **soma** o cashback no mesmo título a receber em aberto da pessoa beneficiária. O cliente passa a ter um único saldo consolidado.
  - **Desmarcado**: cada venda gera um título a receber separado para o cashback. Permite controle granular por venda.

> 💡 É uma configuração **do sistema** (não por tipo de movimento). Combine com o campo `Não exibir cashback no processo de Quitação` (também na aba `Crédito`) caso queira ocultar esses títulos das telas de quitação.

---

## 🔄 Operação no Dia a Dia

### 1. Venda no PDV

O operador finaliza a venda normalmente. Não há nenhum botão extra no PDV: o sistema apenas marca o movimento como **pendente** de processamento de cashback.

### 2. Processamento automático

O **Monitor de Integração** verifica periodicamente os movimentos PDV finalizados que estão pendentes e, para cada um:

1. Consulta as regras de cashback válidas para a empresa, portador e forma de pagamento da venda.
2. Calcula o valor do cashback (`percentual × valor base`), respeitando o `Limite` da regra.
3. Cria o título a receber correspondente em `CONTAS_PR` para a **pessoa beneficiária** (ou para a própria pessoa do movimento, se a beneficiária não estiver definida).
4. Registra a operação no **Extrato Cashback** com data/hora, percentual aplicado, valor e referência ao movimento.
5. Atualiza o movimento marcando o status do cashback como **GERADO**.

> 💡 Se o tipo de movimento gera cashback mas **nenhuma regra** se aplicou (por exemplo, portador sem regra cadastrada), o movimento é marcado como **NÃO APLICÁVEL** e não volta ao processamento.

### 3. Consulta de Extrato

A tela **Extrato Cashback** é aberta pelo botão **`Mostrar Extrato Cashback`** disponível na aba `Cashback` do Cadastro de Pessoas. Não é uma tela de pesquisa F1 independente — ela já abre filtrada pela pessoa selecionada.

A consulta exibe, por linha:
- **Data de Emissão** do movimento original
- **Empresa**
- **Pessoa Movimento** (quem comprou)
- **Beneficiário** (quem recebeu o cashback)
- **Valor** (positivo no crédito; negativo no estorno)
- **Percentual** aplicado
- **Total Nota** que originou o cashback

No rodapé, o campo **Total** mostra o **saldo atual de cashback** da pessoa, calculado como soma de todos os créditos menos os estornos.

> Dica: o filtro `Empresa(s)` no topo permite isolar o saldo por loja quando o grupo opera várias filiais.

---

## 🔁 Estorno e Devolução

O sistema impõe regras específicas para preservar a integridade do saldo de cashback.

### Estorno de movimento já processado

Se o operador tentar **estornar** um movimento cujo cashback já foi gerado (status `GERADO`), o sistema **converte o estorno em cancelamento** e exibe uma confirmação com tempo de espera de 5 segundos:

> *Este movimento possui cashback processado e só pode ser CANCELADO.*  
> *O estorno será realizado seguido do cancelamento automático.*  
> *Deseja prosseguir com o CANCELAMENTO?*

Ao confirmar:
1. O movimento é estornado e cancelado.
2. O cashback é revertido automaticamente — gera registro **negativo** no Extrato.
3. O título em `CONTAS_PR` é atualizado para refletir a redução do saldo.

### Devolução com nota referenciada

- **Devolução referenciando 1 nota**: permitida normalmente; o cashback é revertido proporcionalmente ao valor devolvido.
- **Devolução referenciando múltiplas notas**, quando ao menos uma delas tem cashback **processado**: bloqueada pelo sistema:

> *Não Permitido!*  
> *A devolução não pode referenciar múltiplos documentos quando um ou mais movimentos possuem cashback processado.*  
> *Remova as referências adicionais e mantenha apenas uma nota referenciada.*

A mesma validação também impede **adicionar** uma segunda nota referenciada quando alguma das notas envolvidas tem cashback processado.

> 💡 Se houver necessidade de devolver várias notas com cashback de uma só vez, faça **uma devolução por nota**.

---

## 📊 Status de Processamento do Cashback

Cada movimento PDV recebe um status de cashback que aparece na grade de pesquisa de movimentos:

| Status | Significado |
|--------|-------------|
| **NÃO PROCESSADO** | Movimento aguardando o Monitor de Integração processar. |
| **GERADO** | Cashback calculado e creditado com sucesso. |
| **ESTORNADO** | Cashback foi revertido (estorno/cancelamento do movimento). |
| **NÃO APLICÁVEL** | O tipo de movimento gera cashback, mas nenhuma regra válida se aplicou (ex.: portador sem regra). Não retorna ao processamento. |
| **NÃO ESTORNADO** | A devolução referenciou um movimento com cashback gerado, mas não havia saldo disponível para estorno (ex.: o cliente já consumiu o crédito). O movimento original permanece sinalizado para acompanhamento. |

> 💡 Status “NÃO PROCESSADO” por mais de alguns minutos costuma indicar que o Monitor de Integração não está rodando. Verifique o serviço.

---

## 💡 Exemplos Práticos

### Exemplo 1 — Cashback fixo de 5% no cartão de crédito

**Configuração**:
- Tipo de movimento `Venda PDV — Cartão` com `É PDV` e `Gerar Cashback PDV` marcados.
- Regra `Cashback Crédito 5%`:
  - Percentual: `5,00%`, Limite: `0,00`, Validade: `30` dias.
  - `Contas/Mov. a partir de`: data atual.
  - Detalhes: Portador `Cartão de Crédito`.

**Resultado**:
- Venda de R$ 200,00 → R$ 10,00 creditados na pessoa do movimento, válidos por 30 dias.

### Exemplo 2 — Cashback diferenciado por forma de pagamento

**Configuração**:
- Mesmo tipo de movimento.
- Regra A: Portador `Cartão de Crédito` + Forma `Crédito à Vista`, percentual `5%`.
- Regra B: Portador `Cartão de Crédito` + Forma `Crédito Parcelado`, percentual `2%`.

**Resultado**:
- Mesma venda paga à vista gera mais cashback que parcelada.

### Exemplo 3 — Cashback restrito a clientes VIP

**Configuração**:
- Regra `Cashback VIP 10%` com `Validar tag pessoa` marcado.
- No Cadastro de Pessoas, marque `Utilizar Cashback` apenas para os clientes VIP.

**Resultado**:
- Vendas para clientes sem `Utilizar Cashback` ativo são marcadas como `NÃO APLICÁVEL`.
- Vendas para clientes VIP geram 10% normalmente.

### Exemplo 4 — Cashback consolidado para representante (B2B)

**Configuração**:
- No Cadastro de Pessoas dos clientes finais, preencha **Pessoa Beneficiária** com a pessoa do **representante**.
- (Opcional) Ative **Agrupar Cashback** na Configuração para consolidar tudo num único título a receber por representante.

**Resultado**:
- Vendas dos clientes finais creditam cashback diretamente na conta do representante.

### Exemplo 5 — Cancelamento depois do cashback

**Cenário**:
- Venda de R$ 1.000 gerou R$ 50 de cashback (5%).
- Cliente pede cancelamento.

**Fluxo**:
1. No Cadastro de Movimentação, ao acionar o estorno, o sistema avisa que o movimento será **cancelado**.
2. Após confirmar, o cashback é revertido: -R$ 50,00 no Extrato e título em CONTAS_PR ajustado.
3. Se nesse meio-tempo o cliente já tinha usado parte do crédito, o movimento original recebe status **NÃO ESTORNADO** e a equipe financeira deve avaliar manualmente.

---

## ❓ FAQ / Problemas Comuns

### Por que minha venda PDV não gerou cashback?
Verifique, em ordem:
1. O tipo de movimento tem `É PDV` **e** `Gerar Cashback PDV` marcados?
2. Existe regra cadastrada para a combinação `Empresa × Portador × Forma de Pagamento` da venda?
3. A data de emissão é igual ou posterior a `Contas/Mov. a partir de` da regra?
4. A regra exige `Validar tag pessoa` e a pessoa não tem `Utilizar Cashback` ativo?
5. O Monitor de Integração está rodando? Status pendente por muito tempo costuma indicar serviço parado.

### O cashback é gerado já no PDV ou depois?
O processamento é assíncrono — feito pelo Monitor de Integração logo após a finalização. O operador do PDV não precisa esperar.

### Para onde vai o cashback se a pessoa tem `Pessoa Beneficiária` configurada?
Para a **Pessoa Beneficiária**. Se o campo estiver em branco, o cashback é creditado para a própria pessoa do movimento.

### O que muda quando ligo `Agrupar Cashback`?
Cada nova venda passa a **somar** o crédito num único título a receber em aberto, em vez de criar um título por venda. Use quando quiser que o cliente tenha um saldo consolidado, mais simples de gerenciar.

### Posso alterar uma regra existente?
Pode. As alterações **valem para movimentos novos**; o cashback já gerado em vendas anteriores **não é recalculado** — ele preserva o percentual e o valor originais.

### Como o cliente usa o cashback?
O cashback é representado por um título a receber em `CONTAS_PR` em nome da pessoa beneficiária. Ele pode ser abatido em vendas futuras pela tela de **Operações de Pessoa** ou pelo fluxo de quitação configurado.

### Movimentos antigos do PDV vão gerar cashback retroativo?
**Não.** Na atualização que introduziu o Cashback PDV, todos os movimentos PDV anteriores são marcados como já processados — apenas vendas novas entram no fluxo.

### Posso cancelar uma venda PDV depois que o cashback já foi gerado?
Sim — mas o sistema converte o estorno em **cancelamento** automaticamente e reverte o cashback. Se o cliente já tiver consumido parte do saldo, o movimento fica com status `NÃO ESTORNADO` para acompanhamento manual.

### Não consigo fazer uma devolução referenciando várias notas. O que faço?
Quando alguma das notas referenciadas tem cashback processado, o sistema bloqueia o agrupamento. Faça **uma devolução por nota** referenciada.

### Onde vejo o saldo de cashback de um cliente?
No Cadastro de Pessoas, aba `Cashback`, clique em **`Mostrar Extrato Cashback`**. O rodapé exibe o saldo total e a grade lista todas as movimentações.

---

**Última atualização**: Abril de 2026  
**Versão**: 1.0  
**Público-alvo**: Operadores e supervisores de PDV, administradores Sol.NET
