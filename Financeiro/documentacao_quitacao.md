# 📄 Quitação - Sol.NET

## 🎯 Visão Geral

A tela **Quitação** (`código 303`) é a tela onde a **baixa de títulos** efetivamente acontece. É aberta a partir do **[Pagar e Receber](documentacao_pagar_e_receber.md)** (tela `301`) quando você seleciona títulos e clica em **Quitar(F6)**, ou diretamente pelo `F1 → 303`. Aqui você:

- Vê os **títulos selecionados** e o total a quitar
- Informa **uma ou mais formas de pagamento** (dinheiro, cheque, cartão, PIX, crédito da pessoa, etc.)
- Aplica **descontos, multas, juros e acréscimos** específicos da quitação
- Faz a **conferência** entre o total dos títulos e o total recebido (com indicadores de **Falta**, **Troco** e **Acerto**)
- Pode **usar crédito da pessoa** disponível (em vez de receber novo valor)
- Pode **gerar crédito** quando o cliente paga mais do que deve
- Confirma com **OK** (consolida em conjunto) ou **OK (Individual)** (uma quitação por título)

A tela também tem visualizações auxiliares — **Cheques** recebidos, **Contas Abertas** da pessoa, **CPF/CNPJ na Nota** (para emissão fiscal), e **Título Manual de Acerto**.

> ℹ️ **Esta documentação cobre os fluxos principais.** A tela é grande, com integrações específicas (TEF, HetoBank/PIX, cheque eletrônico). Casos fora do comum devem ser confirmados com o suporte.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Quitação |
| **Código (`F1`)** | `303` |

A forma usual de chegar aqui é:

1. Pela tela **Pagar e Receber** (`301`) — marque os títulos e clique em **Quitar(F6)**.
2. Direto pela pesquisa universal — `F1` → `303` (uso menos comum).

---

## 🧭 Estrutura da tela

A tela é organizada em **áreas verticais** (não em sub-abas como Pagar e Receber):

| Área | Para quê serve |
|------|----------------|
| **Cabeçalho** | Pessoa (cliente/fornecedor), tipo `Pagar/Receber`, identificação |
| **Forma de Pagamentos** | Painel central onde você insere/edita/exclui formas de pagamento usadas na quitação. Tem sub-abas: `Cadastro`, `Cheque (Buscar F8)`, `Cartão de Crédito/Débito`. |
| **Totais** | Indicadores de `Total Parcelas`, `Total Recebido`, `Falta`, `Troco`, `Acerto` — atualizados ao vivo |
| **Crédito de Pessoa** | Sub-abas para `Usar Crédito` (consumir crédito da pessoa) e `Gerar Crédito` (criar crédito novo) |
| **Cheques** | Visualização de cheques recebidos da pessoa (próprios e de terceiros) |
| **Contas Abertas** | Outras contas em aberto da pessoa (para eventualmente incluir na quitação) |
| **CPF/CNPJ na Nota** | Informação fiscal para emissão de comprovante |
| **Título Manual de Acerto** | Cria um título adicional ad-hoc para acerto na hora da quitação |
| **Botões finais** | `OK` (consolidado), `OK (Individual)`, `Gerar Crédito`, `ESC - Cancelar` |

---

## 🔧 Fluxos principais

### 🔹 Quitar título(s) com uma única forma de pagamento

1. Em **Pagar e Receber**, marque o(s) título(s) e clique em **Quitar(F6)**.
2. A tela `Quitação` abre com os títulos carregados e o `Total Parcelas` mostrando a soma.
3. No painel **Forma de Pagamentos** → **Inserir**:
   - **Forma de Pagamento**: escolha (ex.: `DINHEIRO`, `PIX`, `CARTAO`, `CHEQUE`)
   - **Valor**: por padrão preenche com a falta
   - (Específico por forma) Cheque: dados na sub-aba `Cheque`. Cartão: dados na sub-aba `Cartão`.
   - **Atualizar** para confirmar a linha.
4. Confira que **Falta = 0** (`Total Recebido = Total Parcelas`).
5. Clique em **OK** para confirmar a quitação.

### 🔹 Quitar com várias formas de pagamento

Use quando o cliente paga parte em dinheiro, parte em cartão, parte em cheque, etc.

1. Repita o **Inserir** no painel **Forma de Pagamentos** uma vez para cada forma.
2. Ajuste o **Valor** de cada uma — a soma das formas precisa fechar com o `Total Parcelas`.
3. Quando o `Total Recebido` igualar o `Total Parcelas` (Falta = 0), clique em **OK**.

> ℹ️ Se sobrar valor, o sistema mostra como **Troco** e oferece opções (gerar crédito, devolver em dinheiro, etc.) conforme a configuração da forma de pagamento.

### 🔹 Receber valor maior que o título (Troco / Crédito)

Quando o cliente paga mais que o devido (ex.: paga uma duplicata de R$ 95 com uma cédula de R$ 100):

1. Insira a forma de pagamento com o valor maior (R$ 100).
2. O indicador **Troco** acende mostrando R$ 5,00.
3. Conforme a configuração da forma de pagamento (ver [Formas de Pagamento](documentacao_formas_pagamento.md), sub-aba `Troco`):
   - **Troco Só Visual** — só mostra o troco como informação; o operador devolve o dinheiro à parte.
   - **Troco Em Registro** — registra o troco como movimento (Dinheiro ou Crédito Pessoa).
4. Clique em **OK** para confirmar.

Para **gerar crédito** ativamente para a pessoa: clique em **Gerar Crédito** (botão lateral) — o valor sobrante vira crédito armazenado em nome da pessoa, utilizável em quitações futuras.

### 🔹 Usar crédito da pessoa como forma de pagamento

Quando a pessoa tem crédito acumulado (de quitações anteriores ou geração manual):

1. Na seção **Crédito de Pessoa → Usar Crédito**, os créditos disponíveis aparecem listados.
2. Selecione/marque os créditos a usar.
3. O valor dos créditos é abatido do `Total Parcelas` automaticamente.
4. Complete o restante com outras formas de pagamento (se houver `Falta` > 0).
5. **OK** para confirmar.

### 🔹 Pagamento Posterior (F9)

Em alguns casos a quitação **registra a forma** sem efetivar o recebimento imediato — o valor cai depois (ex.: cheque ainda não compensado, cartão ainda não processado pela operadora).

1. Insira a forma de pagamento normalmente.
2. Marque a opção **Pagamento Posterior (F9)** (na sub-aba `Cadastro` do painel de formas).
3. **Atualizar** e **OK**.

O sistema registra a quitação mas mantém o status como "a compensar" — quando o pagamento for efetivamente recebido, é confirmado pela tela de [Caixa Geral](documentacao_caixa_geral_op.md) (`302`).

### 🔹 Buscar cheque já cadastrado (F8)

Quando o cliente paga com um cheque que já está no sistema (de outro cliente, por exemplo — troca de cheques):

1. Na sub-aba `Cheque` do painel de formas, pressione **F8** (ou clique no botão de buscar).
2. Localize o cheque na pesquisa.
3. O sistema preenche os dados do cheque automaticamente.

### 🔹 Quitar individual vs OK consolidado

- **OK (consolidado, botão principal)** — quita **todos os títulos selecionados** com as formas informadas (a quitação é única, vinculada ao conjunto).
- **OK (Individual)** — quita os títulos **um a um**, criando uma quitação separada para cada. Útil quando você precisa de comprovantes separados ou rastreabilidade por título.

### 🔹 Cancelar a quitação

Clique em **ESC - Cancelar** (botão lateral) ou pressione `ESC`. Os dados informados são descartados e os títulos voltam ao estado "Em Aberto" sem mudança.

### 🔹 Título Manual de Acerto

Permite criar um título extra (acerto) na hora da quitação, sem precisar abrir o Pagar e Receber separado:

1. Aba/seção **Título Manual de Acerto** → **Inserir**.
2. Preencha **Tipo de Operação**, valor, plano de contas, centro de custo, etc.
3. O título entra na quitação atual.
4. Útil para ajustes pontuais (taxa adicional, juros não calculados, desconto extraordinário).

### 🔹 Informar CPF/CNPJ na nota

A seção **CPF/CNPJ na Nota** permite informar o documento do tomador para o comprovante fiscal — geralmente quando o pagador é diferente do titular do título (ex.: pessoa jurídica que paga pelo funcionário).

---

## ✅ Validações comuns ao confirmar

A validação ao confirmar a quitação tem várias regras:

1. **Campos obrigatórios** — Forma de pagamento sem campos vazios.
2. **Validação da forma de pagamento** — cada forma tem regras próprias (cartão exige operadora, cheque exige banco/agência/conta/número, etc.).
3. **Validação de cheque** — banco e agência cadastrados, número não duplicado, vencimento válido.
4. **Validação de promoção/bins** — se a forma de pagamento tem promoção atrelada (BIN do cartão), o sistema checa.
5. **Validação de troco** — se há troco registrado, a forma de troco precisa estar configurada na forma de pagamento.
6. **Validação ao finalizar** — `Total Recebido` precisa fechar com `Total Parcelas + Acerto` (a `Falta` precisa ser zero ou compatível com a configuração).
7. **Data da quitação não pode ser anterior à data de emissão** do título — bloqueio padrão.
8. **Permissão por empresa por usuário** — para quitar títulos da empresa em questão.

Quando uma validação falha, o sistema mostra a mensagem específica e posiciona o cursor/área no campo problemático.

---

## 🔐 Modos de abertura

| Modo | O que faz |
|------|-----------|
| **Normal** | Abertura usual — vem do `Quitar(F6)` em Pagar e Receber, ou direto pela pesquisa `F1 → 303` |
| **Ler Arquivo Retorno** | Abertura específica para processar pagamentos vindos de arquivo (retorno bancário), com pessoa pré-selecionada |

O modo é definido pela tela que abre a Quitação.

---

## 💡 Exemplos práticos

### Quitar uma duplicata com dinheiro

1. **Pagar e Receber** → marque a duplicata → **Quitar(F6)**.
2. Na Quitação: painel `Forma de Pagamentos` → **Inserir**.
3. **Forma**: `DINHEIRO`. **Valor**: já vem preenchido com o valor da duplicata.
4. **Atualizar**.
5. **OK**.

### Quitar com 50% dinheiro + 50% cartão de crédito

1. **Quitar(F6)** com o título selecionado.
2. **Inserir** → `DINHEIRO` → ajustar **Valor** para 50%. **Atualizar**.
3. **Inserir** → `CARTAO DE CREDITO - VISA` → preencher dados do cartão (operadora, parcelas) → ajustar **Valor** para 50%. **Atualizar**.
4. Conferir `Falta = 0`.
5. **OK**.

### Cliente paga 95 com cédula de 100 (troco)

1. **Quitar(F6)** com a duplicata de R$ 95.
2. **Inserir** → `DINHEIRO` → **Valor**: `100`. **Atualizar**.
3. `Troco` mostra `5,00`.
4. **OK** — o sistema processa o troco conforme a configuração da forma (visual ou registro).

### Usar crédito acumulado da pessoa

1. **Quitar(F6)** com duplicata de R$ 200.
2. Na seção **Crédito de Pessoa → Usar Crédito** aparece um crédito de R$ 80.
3. Marque o crédito.
4. `Falta` cai para R$ 120.
5. **Inserir** → `DINHEIRO` → R$ 120 → **Atualizar**.
6. **OK**.

### Cliente paga R$ 50 a mais e quer guardar como crédito

1. **Quitar(F6)** com duplicata de R$ 100.
2. **Inserir** → `DINHEIRO` → **Valor**: `150`. **Atualizar**.
3. Clique em **Gerar Crédito** — os R$ 50 sobrantes viram crédito em nome do cliente.
4. **OK**.

### Quitar vários títulos individualmente (com comprovantes separados)

1. **Pagar e Receber** → marque 3 títulos → **Quitar(F6)**.
2. Configure as formas de pagamento conjuntamente.
3. Clique em **OK (Individual)** — em vez de uma quitação consolidada, o sistema cria três quitações separadas, uma por título.

---

## ❓ FAQ / Problemas comuns

**Clico em OK e o sistema diz que falta valor.**
O `Total Recebido` (soma das formas de pagamento) precisa fechar com o `Total Parcelas`. Se aparece `Falta`, insira mais uma forma de pagamento ou ajuste o valor das existentes.

**Sobrou valor — Troco aparece — o que faço?**
Três caminhos:
- Devolver em dinheiro ao cliente — basta clicar em **OK** se a forma de pagamento tem troco "Só Visual".
- Gerar crédito para o cliente — clique em **Gerar Crédito**.
- Não receber o valor sobrante — ajuste o valor da forma de pagamento para igualar exatamente o devido.

**O cheque informado já existe.**
O sistema valida que o número do cheque (banco + agência + conta + número) não está duplicado. Confira se o cheque já não foi lançado em outra operação. Pode ser que esteja apenas com status diferente — investigue antes de re-cadastrar.

**Não consigo usar uma forma de pagamento na quitação.**
Pode ser por:
- A condição de pagamento do título **restringe** quais formas são aceitas (configuração em [Cond. de Pagamento](documentacao_condicoes_pagamento.md), aba `Formas de Pagamento`).
- A forma de pagamento está inativa.
- O usuário não tem permissão de uso (raro).

**A data da quitação não pode ser anterior à emissão do título.**
Correto — regra padrão. Se você precisa de uma exceção (caso atípico), consulte o suporte Hetosoft.

**Quero quitar um título e gerar comprovante fiscal para outro CPF/CNPJ.**
Use a seção `CPF/CNPJ na Nota` para informar o documento do tomador antes de clicar em OK.

**O cliente quer pagar parte agora e parte depois (no cartão).**
Insira a forma de cartão e marque **Pagamento Posterior (F9)** na sub-aba `Cadastro` do painel. O sistema registra a quitação parcial; a parcela "futura" é processada quando efetivamente cair (geralmente via conciliação de cartões na tela `302`).

**"OK (Individual)" vs "OK" — quando usar cada?**
**OK** é o padrão — uma quitação só, vinculada a todos os títulos selecionados.
**OK (Individual)** é para quando cada título precisa do seu próprio comprovante, ou para rastreabilidade por título no histórico.

**Cancelei sem querer e perdi tudo.**
Use **ESC** com cuidado — não tem desfazer. Refaça a operação a partir do Pagar e Receber.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Relação |
|------|:---:|---------|
| [Pagar e Receber](documentacao_pagar_e_receber.md) | `301` | Origem da quitação (botão Quitar(F6)) |
| [Caixa Geral](documentacao_caixa_geral_op.md) | `302` | Onde o lançamento da quitação efetivamente fica registrado |
| [Formas de Pagamento](documentacao_formas_pagamento.md) | `7` | Define as formas selecionáveis aqui (e suas regras de troco, cartão, TEF, etc.) |
| [Cond. de Pagamento](documentacao_condicoes_pagamento.md) | `8` | Pode restringir quais formas são aceitas na quitação de um título |
| [Cadastro de Caixa Geral](documentacao_caixa_geral.md) | `13` | Caixa de destino do recebimento |
| [Portadores](documentacao_portadores.md) | `12` | Portador define como o título é cobrado/recebido |

---

## ⚠️ Limites desta documentação

Esta documentação foi construída a partir da inspeção direta do comportamento da tela no Sol.NET. Por se tratar de uma tela operacional com várias integrações externas (TEF, HetoBank/PIX, cheque eletrônico), **a doc cobre os fluxos principais e as regras mais comuns**, mas não esgota:

- **Variantes específicas de cada operadora de cartão / TEF** — comportamento depende do convênio.
- **Integração HetoBank / PIX** — depende dos parâmetros do convênio.
- **Promoções e BINs de cartão** — regras de validação dependem da configuração de promoção.
- **Regras automáticas que rodam dentro do banco de dados** ao confirmar a quitação.
- **Variações por release** — esta tela evolui frequentemente.

Para casos fora do comum, em especial integrações específicas, consulte o suporte Hetosoft.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 5.0 (refeito do zero descartando a documentação anterior)
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo Financeiro
