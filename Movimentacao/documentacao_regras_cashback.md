# 📄 Cadastro de Regras Cashback - Sol.NET

## 🎯 Visão Geral

A **Regra de Cashback** define **quando** e **quanto** crédito o Sol.NET devolve ao cliente em forma de cashback. Cada regra cadastrada nesta tela responde a três perguntas: **em qual loja** vale, **quais combinações de Portador + Forma de Pagamento** disparam o cashback, e **qual percentual** sobre o valor pago é creditado — com um teto opcional por operação (Valor Limite) e um prazo de validade do crédito.

O cashback gerado vira um saldo da pessoa, que pode ser usado para quitar contas a receber ou abater pagamentos em movimentos futuros, conforme a regra estiver configurada. A geração pode ser disparada na **emissão do movimento** (venda) ou na **quitação da conta** correspondente, e a regra controla o que acontece quando a conta foi paga **vencida** — com ou sem dias de carência.

> ℹ️ **Onde o cashback aparece para o cliente.** A regra apenas **gera** o crédito. O extrato e o uso do saldo aparecem em outras telas (`Pagar e Receber` — código `301`, e no fluxo de quitação do PDV). Esta tela é exclusivamente de configuração das regras.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro Regras Cashback |
| **Código (`F1`)** | `124` |

Abra a pesquisa universal (atalho `F1`) e digite **`124`** ou parte do nome **`Regras Cashback`**.

---

## 📝 Campos do cabeçalho

| Campo | Para quê serve |
|-------|----------------|
| **Descrição** | Nome livre da regra (até 120 caracteres). Use nomes que descrevam o público ou o cartão: `CASHBACK CARTÃO LOJA`, `PROMO PIX 5%`, `VIP 10% LIMITE 50`. |
| **%** | Percentual aplicado sobre o valor pago — `5` significa 5 % de cashback. |
| **Valor Limite** | Valor máximo de cashback gerado por operação. Use `0` para não limitar. Em uma compra de R$ 1.000 com 5 % e limite de R$ 30, o cashback gerado é R$ 30 (não R$ 50). |
| **Validade em Dias** | Quantos dias o crédito gerado fica disponível para uso antes de expirar. `0` significa sem expiração explícita (vale enquanto o saldo existir). |
| **Loja** | **Multi-seleção.** Marque uma ou mais empresas onde a regra vale. Cada loja gera uma combinação única — duas regras ativas não podem repetir Portador + Forma de Pagamento na **mesma** loja. |
| **Contas/Mov. a partir de** | Data inicial de validade. O cashback só é gerado para movimentos / contas emitidos a partir desta data. |
| **Gerar Cashback para Contas Vencidas** | Controla o comportamento quando a conta é paga **depois** do vencimento. Detalhes no quadro abaixo. |
| **Gerar Cashback com base no Movimento** | Quando marcado, o cálculo do cashback usa o **valor do movimento** (venda). Desmarcado, usa o valor efetivamente **pago/quitado** em cada parcela. |
| **Validar tag pessoa** | Quando marcado, a regra **só** se aplica a clientes cuja Pessoa esteja marcada com determinada tag/categoria (a tag é configurada no Cadastro de Pessoas). |
| **Inativo** | Marca a regra como inativa — ela continua existindo no banco mas deixa de ser aplicada nos novos movimentos. |

### Quadro: Comportamento de `Gerar Cashback para Contas Vencidas`

| Cenário | Caixa **desmarcada** (usa carência) | Caixa **marcada** (ignora vencimento) |
|---------|------------------------------------|--------------------------------------|
| Conta paga antes do vencimento | ✅ Gera cashback | ✅ Gera cashback |
| Conta paga após vencimento, **sem** dias de carência | ❌ Não gera | ✅ Gera mesmo assim |
| Conta paga após vencimento, **dentro** da carência (ex.: 2 dias) | ✅ Gera (a carência cobre) | ✅ Gera |

Os dias de carência são configurados separadamente (Forma de Pagamento / regra do negócio). O botão de ajuda ao lado do campo na tela mostra esta mesma tabela.

---

## 🔧 Painel `Detalhe Cashback` (combinações Portador × Forma de Pagamento)

O painel inferior do formulário lista as **combinações** que disparam a regra. Cada linha é um par **Portador + Forma de Pagamento** — se a venda é paga **com essa combinação** numa das lojas marcadas, o cashback é gerado.

| Botão | O que faz |
|-------|-----------|
| **Inserir** | Inicia uma nova combinação. Exige que pelo menos uma `Loja` esteja marcada antes. |
| **Adicionar / Atualizar** | Salva a combinação corrente. O botão muda de `Adicionar` (durante a inclusão) para `Atualizar` (durante a edição). |
| **Deletar** | Remove a combinação selecionada da grade. |
| **Cancelar** | Cancela a inclusão / alteração em andamento. |

### Regras das combinações

- A combinação **Portador + Forma de Pagamento** é **única dentro da regra** — duplicar é bloqueado com a mensagem *"Essa combinação já foi inserida"*.
- **Não pode existir a mesma combinação em outra Regra de Cashback ativa para a mesma Loja**. Se houver, o sistema mostra exatamente qual regra, qual loja e qual combinação conflita, e a gravação é recusada.
- O combo `Portador` lista apenas portadores **ativos** com tipo de entrada/saída compatível com cashback (entrada e ambos).
- O combo `Forma de Pagamento` lista apenas formas **ativas**.

---

## ✅ Validações automáticas ao salvar

| Quando você grava | O sistema verifica |
|-------------------|--------------------|
| Sempre | `Descrição` é obrigatória e **única** — duplicar a descrição é bloqueado pelo sistema. |
| Sempre | Os campos do detalhe atualmente em edição precisam estar gravados (não pode haver um `Inserir` aberto sem confirmar). |
| Sempre | As combinações `Portador + Forma de Pagamento` não podem colidir com outra regra ativa **na mesma loja** (ver quadro acima). |
| Ao inserir um detalhe | Pelo menos uma `Loja` precisa estar marcada antes de clicar em `Inserir`. |
| Ao adicionar um detalhe | O combo `Portador` é obrigatório. |
| Em clonagem | Pede confirmação antes de clonar o registro. |

---

## 🚫 Exclusão

A exclusão remove em cascata todos os detalhes da regra (combinações Portador × Forma) e os vínculos com as lojas. Não há bloqueio explícito — mesmo que a regra já tenha gerado extratos de cashback (em `EXTRATO_CASHBACK`), a exclusão é permitida.

> ⚠️ **Boa prática.** Se a regra já gerou cashback para clientes, **prefira marcar como Inativo** em vez de excluir. Excluir uma regra ativa que tem extrato em uso pode dificultar auditoria futura sobre como aquele crédito foi gerado.

---

## 📋 Clonar regra

A tela oferece a função **Clonar Registro** no menu de contexto da grade de busca — clique-direito sobre a regra desejada e escolha `Clonar Registro`. Útil para criar variações: clone a regra base, ajuste o percentual ou a Forma de Pagamento, e grave com nova Descrição.

O sistema confirma antes de clonar e a cópia abre já em modo de edição para você ajustar antes de gravar.

---

## 💡 Exemplos práticos

### Exemplo 1 — Cashback de 5 % em vendas pagas com cartão de crédito

1. Pesquisa `F1` → `124` → abre `Cadastro Regras Cashback`.
2. Clique em **Novo**.
3. Preencha o cabeçalho:
   - `Descrição`: `CASHBACK CARTÃO 5%`.
   - `%`: `5`.
   - `Valor Limite`: `0` (sem teto).
   - `Validade em Dias`: `90`.
   - `Loja`: marque a(s) loja(s) onde a regra vale.
   - `Contas/Mov. a partir de`: hoje.
   - `Gerar Cashback com base no Movimento`: marcado.
   - `Gerar Cashback para Contas Vencidas`: desmarcado.
4. No painel inferior:
   - Clique **Inserir**.
   - `Portador`: o portador do cartão (ex.: `CIELO CRÉDITO`).
   - `Forma de Pagamento`: `CARTÃO DE CRÉDITO`.
   - Clique **Adicionar**.
5. Repita o passo 4 para cada combinação de Portador × Forma desejada (ex.: outros portadores de cartão).
6. **Gravar**.

### Exemplo 2 — Cashback exclusivo para clientes VIP (com tag)

1. Garanta que a tag VIP esteja cadastrada e aplicada às Pessoas elegíveis no `Cadastro de Pessoas`.
2. Pesquisa `F1` → `124` → **Novo**.
3. Cabeçalho:
   - `Descrição`: `CASHBACK VIP 10%`.
   - `%`: `10`.
   - `Valor Limite`: `100,00`.
   - `Validade em Dias`: `180`.
   - `Loja`: todas as lojas.
   - **Validar tag pessoa**: marcado.
4. Adicione as combinações Portador × Forma desejadas.
5. **Gravar**.

Vendas para clientes sem a tag VIP **não** geram cashback, mesmo que a combinação Portador + Forma bata.

### Exemplo 3 — Clonar uma regra para criar uma versão promocional

1. Na grade de busca, localize a regra base (ex.: `CASHBACK CARTÃO 5%`).
2. Clique-direito sobre a linha → `Clonar Registro` → confirme.
3. A cópia abre em modo de inclusão.
4. Ajuste:
   - `Descrição`: `PROMO BLACK FRIDAY 8%`.
   - `%`: `8`.
   - `Contas/Mov. a partir de`: data de início da promoção.
   - `Validade em Dias`: ajuste se necessário.
5. **Gravar**.

A regra antiga permanece ativa em paralelo — durante a promoção, a regra com maior percentual prevalece (a configuração de prioridade fica fora desta tela).

---

## ❓ FAQ / Problemas comuns

**Cadastrei a regra mas o cliente não recebeu cashback. Por quê?**
Confira nesta ordem: (1) `Inativo` está desmarcado? (2) A `Loja` da venda está marcada na regra? (3) A combinação `Portador + Forma de Pagamento` usada no pagamento corresponde **exatamente** a uma linha do painel inferior? (4) A `Contas/Mov. a partir de` é anterior à data da venda? (5) Se `Validar tag pessoa` está marcado, o cliente tem a tag correta? (6) Se a conta foi paga vencida, `Gerar Cashback para Contas Vencidas` está adequado para o cenário?

**O sistema bloqueou minha gravação dizendo que a combinação já existe em outra regra.**
Isso é proteção contra **duas regras concorrentes** na mesma loja com a mesma combinação. Resolva uma das três formas: (1) inativando a regra antiga; (2) removendo a combinação conflitante da regra antiga; (3) tirando a loja conflitante da nova regra.

**A descrição que quero usar já está cadastrada e eu não acho onde.**
A duplicidade é checada em **todas** as regras, ativas e inativas. Use o campo de busca no topo da tela com `INICIA COM` para localizar regras com descrições parecidas, inclusive as inativadas.

**Qual a diferença entre `Gerar Cashback com base no Movimento` marcado e desmarcado?**
Marcado: o cashback é calculado sobre o **valor total do movimento (venda)** na hora da emissão. Desmarcado: é calculado a cada **quitação** das parcelas — útil para vendas parceladas, onde cada parcela paga gera sua fatia de cashback.

**Excluí uma regra mas o extrato dela continua aparecendo no cliente.**
Sim — o extrato (`EXTRATO_CASHBACK`) é independente da regra que o gerou. Quando você exclui uma regra, o extrato gerado por ela continua valendo para os clientes que receberam aquele saldo. Por isso a recomendação é **inativar** em vez de excluir, sempre que houver extrato gerado.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Como se relaciona |
|------|---------------|--------------------|
| `Formas de Pagamento` | `7` | Fornece o combo `Forma de Pagamento` do painel de detalhes. |
| `Portadores` | `12` | Fornece o combo `Portador` — apenas portadores ativos com tipo compatível com cashback aparecem. |
| `Cadastro de Pessoas` | `1` | Onde a tag/categoria do cliente é definida, usada quando `Validar tag pessoa` está marcado. |
| `Movimentos` | `53` | Origem das vendas que disparam a geração do cashback. |
| `Pagar e Receber` | `301` | Onde o cashback gerado pode ser usado para quitar contas e onde aparece o extrato. |

---

## ⚠️ Limites desta documentação

- Não detalha como o **PDV** (Self Checkout ou frente de loja) consome o cashback no momento da venda — esse fluxo será coberto em um guia cross-tela específico.
- A priorização entre **regras concorrentes** (qual prevalece quando duas combinações batem) não é configurada nesta tela; depende do conjunto ativo no momento da venda.
- O **extrato** do cashback (saldo disponível, créditos vencidos, uso histórico) é consultado fora desta tela.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de Suporte / Administradores Sol.NET
