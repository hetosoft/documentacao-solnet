# 📄 Cadastro de Transações de Estoque - Sol.NET

## 🎯 Visão Geral

Uma **Transação de Estoque** é a *receita* que diz ao Sol.NET **como cada Situação de Estoque do produto deve se comportar** quando uma operação acontece — entra, sai ou fica como está. Cada Tipo de Movimento (entrada de notas, venda, devolução, ajuste etc.) aponta para **uma** Transação de Estoque, e é a Transação que decide, na hora de gravar o movimento, se o saldo da camada **Físico** soma, subtrai ou não muda; o mesmo para **Disponível**, **Reservado**, **Pedido de Compra** e demais camadas.

A tela exibe as 10 posições de Situação de Estoque cadastradas no sistema (definidas em [`Situação de Estoque`](#-telas-relacionadas)) e pede, para cada uma, qual o efeito: `+` (Entrada), `-` (Saída) ou `Nenhum`. Combinações diferentes geram comportamentos diferentes — por exemplo, uma transação "Entrada de Notas" tipicamente soma em Físico e Disponível e deixa as demais como `Nenhum`; já uma "Reserva de Venda" pode somar em Reservado e subtrair de Disponível sem mexer no Físico.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Transações de Estoque |
| **Código (`F1`)** | `33` |

Abra a pesquisa universal (atalho `F1`) e digite **`33`** ou parte do nome **`Transações de Estoque`**.

---

## 📝 Campos

A tela tem um campo de identificação e um bloco fixo de 10 linhas — uma por posição de Situação de Estoque.

### Identificação

| Campo | Para quê serve |
|-------|----------------|
| **Descrição** | Nome livre da transação (até 80 caracteres, gravado em maiúsculas). Exemplos: `ENTRADA DE NOTAS`, `SAIDA DE NOTAS`, `RESERVA DE PEDIDO`. |

### Linhas de posição (`Selecione 1` até `Selecione 10`)

Para cada uma das 10 posições, a tela mostra:

| Coluna | O que aparece |
|--------|---------------|
| **Posição** | Número fixo da posição (`1` a `10`). |
| **Descrição da Situação** | Nome da Situação de Estoque cadastrada naquela posição (ex.: `FISICO`, `DISPONIVEL`, `RESERVADO`, `PEDIDO DE COMPRA`, `EM CONSERTO`). |
| **Selecione** | A regra desta posição. Três opções: |
|  | `+` — a operação **soma** no saldo desta camada (entrada). |
|  | `-` — a operação **subtrai** do saldo desta camada (saída). |
|  | `Nenhum` — a operação **não mexe** nesta camada. |

> ℹ️ **Quem define o nome das posições.** As descrições mostradas em cada linha (`FISICO`, `DISPONIVEL` etc.) vêm da tela `Situação de Estoque` (código `30`). Se uma posição aparece como `VAZIO 3`, `VAZIO 4` etc., significa que ela não está em uso — basta deixar como `Nenhum` para todas as transações.

---

## ✅ Validações automáticas ao salvar

| Quando você grava | O sistema verifica |
|-------------------|--------------------|
| Sempre | A `Descrição` precisa estar preenchida. |
| Sempre | As 10 linhas precisam ter uma opção marcada (`+`, `-` ou `Nenhum`). Linhas em branco impedem a gravação. |

Não há checagem de duplicidade: o sistema **permite** salvar duas transações com a mesma descrição. Use nomes claros e diferentes para evitar confusão na hora de configurar os Tipos de Movimento.

---

## 🚫 Exclusão

A exclusão é bloqueada quando a transação já está em uso:

- ❌ **Em algum Tipo de Movimento** — o sistema mostra a mensagem *"Existe Tipo de Movimento com esta Transação de Estoque!"*. Resolva trocando a transação no Tipo de Movimento que a usa antes de tentar excluir de novo.

  > ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Tipos de Movimento` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nesta tela.
- ❌ **No histórico de movimentações** — se já houve qualquer movimento que usou esta transação, a exclusão é recusada com a mensagem *"Existe Movimentação de Estoque com esta Transação de Estoque!"*. Nesse caso, a recomendação é **deixar a transação cadastrada** (ela é leve no banco) — não há campo `Inativo`, então não há como ocultá-la do cadastro de Tipos de Movimento. Quem decide quais transações o usuário vê é o cadastro dos Tipos de Movimento.

---

## 💡 Exemplos práticos

### Exemplo 1 — Entrada de Notas (compra que entra no estoque para venda)

1. Pesquisa `F1` → `33` → abre `Cadastro de Transações de Estoque`.
2. Clique em **Novo**.
3. `Descrição`: `ENTRADA DE NOTAS`.
4. Marque:
   - `Selecione 1` (FISICO): `+`
   - `Selecione 2` (DISPONIVEL): `+`
   - `Selecione 3` a `Selecione 10`: `Nenhum`
5. **Gravar**.

> Esta é a transação típica usada por Tipos de Movimento de compra/entrada que **disponibilizam** o produto para venda imediata.

### Exemplo 2 — Saída de Notas (venda ou transferência que retira do estoque)

1. Pesquisa `F1` → `33` → **Novo**.
2. `Descrição`: `SAIDA DE NOTAS`.
3. Marque:
   - `Selecione 1` (FISICO): `-`
   - `Selecione 2` (DISPONIVEL): `-`
   - Demais: `Nenhum`
4. **Gravar**.

### Exemplo 3 — Reserva de Pedido (separa o produto sem tirar do físico)

1. Pesquisa `F1` → `33` → **Novo**.
2. `Descrição`: `RESERVA DE PEDIDO`.
3. Marque:
   - `Selecione 1` (FISICO): `Nenhum`
   - `Selecione 2` (DISPONIVEL): `-`
   - `Selecione 3` (RESERVADO): `+`
   - Demais: `Nenhum`
4. **Gravar**.

> Esta transação **transfere saldo** de Disponível para Reservado — o produto continua no estoque físico, mas deixa de aparecer como "livre para vender". É a base de fluxos de pré-venda e separação.

---

## ❓ FAQ / Problemas comuns

**A tela mostra `VAZIO 3`, `VAZIO 4`… nas linhas 6 a 10. Tenho que preencher?**
Não. Posições marcadas como `VAZIO N` não têm Situação de Estoque cadastrada — deixe-as como `Nenhum`. Quem cadastra novas situações é o `Cadastro de Situação de Estoque` (código `30`), normalmente operado pelo suporte ou administrador.

**Posso editar uma Transação já usada por um Tipo de Movimento?**
Sim — a edição é permitida. Mas tenha cautela: o **histórico de movimentos já gravados não é recalculado**. A alteração só afeta movimentos **novos** que usem esse Tipo de Movimento daqui pra frente.

**Por que minha venda subtraiu do Reservado em vez de subtrair do Físico?**
O comportamento vem da Transação de Estoque associada ao Tipo de Movimento da venda. Abra o `Cadastro de Tipos de Movimento` (código `37`), localize o Tipo da venda, veja qual Transação de Estoque ele aponta, abra a Transação e confira as regras de cada posição.

**O sistema deixou eu cadastrar duas transações com a mesma descrição. É um problema?**
Funcionalmente não atrapalha, mas confunde quem vai configurar os Tipos de Movimento — o combo passa a mostrar duas opções iguais. Padronize as descrições no cadastro inicial e, se aparecerem duplicatas, renomeie uma das duas para diferenciar.

**Como saber quais Tipos de Movimento usam uma certa Transação de Estoque?**
A tela não tem essa consulta pronta. O caminho prático é abrir `Cadastro de Tipos de Movimento` (código `37`), abrir cada Tipo e verificar o campo `Transação de Estoque`. Em bases grandes, peça apoio ao suporte para uma consulta direta no banco.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Como se relaciona |
|------|---------------|--------------------|
| `Situação de Estoque` | `30` | Define quais são as 10 camadas que aparecem nesta tela (`FISICO`, `DISPONIVEL` etc.). |
| `Tipos de Movimento` | `37` | Cada Tipo de Movimento aponta para **uma** Transação de Estoque, que decide o efeito da operação em cada camada. |
| `Saldo Estoque` | `78` | Consulta o saldo resultante por Situação de Estoque — é onde o efeito desta transação aparece. |
| `Histórico de Movimentações` | `205` | Lista os movimentos que aplicaram cada Transação de Estoque. |
| `Movimentos de Compras` | `201` | Lançamento de compras — cada movimento usa um Tipo de Movimento que, por sua vez, aplica esta Transação de Estoque. |
| `Movimentos de Vendas` | `202` | Lançamento de vendas. |
| `Outros Movimentos` | `203` | Demais movimentos (transferências, ajustes via Tipo de Movimento). |

---

## ⚠️ Limites desta documentação

- Não cobre o cadastro de **Situação de Estoque** (tela `30`) — o que é cada camada e quando criar uma nova. Esse será um documento próprio.
- Não detalha a operação dos **Tipos de Movimento** (tela `37`) — apenas indica que é lá que a Transação é amarrada à operação real.
- Movimentações geradas por integrações (PDV, e-commerce, mobile) usam os mesmos Tipos de Movimento e, portanto, as mesmas Transações de Estoque — não há tratamento especial para esses canais nesta tela.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de Suporte / Administradores Sol.NET
