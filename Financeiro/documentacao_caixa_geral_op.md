# 📄 Caixa Geral - Sol.NET

## 🎯 Visão Geral

A tela **Caixa Geral** (`código 302`) é a operação do dia a dia financeiro: é onde **entradas e saídas** são lançadas em cada caixa cadastrado em **[Cadastro de Caixa Geral](documentacao_caixa_geral.md)** (tela `13`), onde acontecem as operações de **compensação** (cheque, boleto, etc.), **transferências entre caixas**, **conciliação bancária**, **conciliação de cartões**, **conferência de caixa**, **renegociação de cheques** e **importação de extratos OFX**.

> ⚠️ **Não confunda com o Cadastro:** a tela **Cadastro de Caixa Geral** (código `13`) define **os caixas existentes** (PDV, banco, cartões, etc.). Esta tela (código `302`) é a **operação** — os lançamentos efetivos.

Por ser uma tela ampla, ela é aberta em **modos** diferentes conforme a origem (uso normal, fechamento de caixa, importação OFX, zerar caixas).

> ℹ️ **Esta documentação cobre os fluxos principais.** A tela tem dezenas de validações cruzadas, flags por tipo de operação, integrações (TEF, retorno de boletos, conciliação online) e regras por tipo de caixa. Casos fora do comum devem ser confirmados com o suporte.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Caixa Geral |
| **Código (`F1`)** | `302` |

Abra a pesquisa universal (atalho `F1`) e digite **`302`** ou parte do nome **`Caixa Geral`**.

A tela também é aberta automaticamente por outras telas em modos especiais (fechamento, OFX, zerar caixas).

---

## 🧭 Estrutura da tela (visão rápida)

### Tab `Visualizar` (consulta de movimentos)

A tab de consulta é organizada em várias áreas:

- **Filtros do topo** — Tipo de Operação (`Transferência`, `Estorno`, `Normal`, `Cancelados`), Empresa, Caixa, Data inicial/final, Status, Campo pesquisado + condição, etc.
- **Páginas de visualização** (sub-PageControl):
  - **Caixa** — lançamentos do caixa selecionado (entradas/saídas/transferências)
  - **Contas** — sub-páginas Registros e Renegociação
  - **Pagamentos** — sub-páginas Detalhes, Cheque, Cartão, Crédito Pessoa Usado, Crédito Pessoa Gerado
  - **Movimentos** — vínculo com vendas/compras
  - **Vínculos** — sub-páginas Transferência, Origem/Destino
  - **Cheque Renegociado** — histórico de cheques renegociados
  - **Histórico do Cheque** — rastreabilidade
  - **Resumo Caixas** — totais por caixa
  - **Transferência** — visualização de transferências
  - **Totais** — totalizadores gerais

Filtros e padrões (descrição da loja, datas, tipo de operação) podem ser **salvos como padrão do usuário** pelos menus de contexto — "Salvar Padrão" — para a tela reabrir já configurada.

### Tab `Cadastrar` (lançamento e edição de um movimento)

Quando você clica em **Novo** ou **Alterar**, a tela mostra o painel com sub-abas:

| Sub-aba | Para quê serve |
|---------|----------------|
| **Dados Cadastrais** | Cabeçalho do lançamento — caixa, pessoa, valor, data, tipo de operação, histórico, plano de contas, centro de custo |
| **Cheque** | Dados específicos quando o lançamento é em cheque (banco, agência, conta, nº cheque, vencimento, emitente, prorrogação, remessa gerada) |
| **Cartão** | Dados específicos quando é em cartão (operadora, parcelas, taxa, TEF, transação) |
| **Rateio** | Rateio contábil do valor em múltiplas linhas (plano de contas + centro de custo + empresa + valor/percentual) |
| **Transferência** | Quando o lançamento é uma transferência (sub-abas Cheque, Cartão, Contas Vinculados) |
| **Imagens** | Anexar fotos/documentos ao lançamento |

### Tab `Operações`

Concentra as operações em lote / conciliação:

| Sub-aba | Para quê serve |
|---------|----------------|
| **Conferência de Caixa** | Confere o saldo do caixa contra os lançamentos |
| **Conciliação Cartões** | Importa arquivo da operadora de cartão e concilia automaticamente |
| **Conciliação Bancária** | Processa arquivo de retorno bancário e concilia automaticamente |

---

## 🔧 Fluxos principais

### 🔹 Lançar movimento no caixa

1. Pesquisa `F1` → `302` → escolha o caixa em `Caixa` (filtro do topo).
2. Clique em **Novo**.
3. **Aba `Dados Cadastrais`**:
   - **Tipo de Operação** — `Entrada`, `Saída`, `Transferência` ou outros (varia por caixa)
   - **Empresa**
   - **Caixa** — o caixa onde o movimento entra/sai
   - **Pessoa** (se aplicável) — cliente ou fornecedor
   - **Data**
   - **Valor**
   - **Histórico** — descrição do lançamento
   - **Plano de Contas** + **Centro de Custo** — classificação contábil
   - **Compensado** — marca se o valor já foi compensado (default depende do tipo)
4. Se o lançamento é em **cheque** → preencha a aba `Cheque` (banco, agência, conta, nº cheque, vencimento, emitente).
5. Se em **cartão** → preencha a aba `Cartão` (operadora, parcelas, taxa).
6. (Opcional) Aba `Rateio` → quebre o valor em múltiplas linhas.
7. (Opcional) Aba `Imagens` → anexe comprovantes.
8. **Gravar**.

### 🔹 Compensar / Descompensar

Operações em lote sobre lançamentos selecionados na consulta:

- **Compensar (F6)** — botão na barra inferior. Marca os lançamentos selecionados como compensados (cheque pago, boleto liquidado, etc.).
- **Descomp.(F7)** — botão na barra inferior. Reverte a compensação dos lançamentos selecionados.

Passos:

1. Tab `Visualizar` → filtre os lançamentos.
2. Marque na coluna de seleção (`Sel.`) os movimentos desejados.
3. Pressione `F6` (Compensar) ou `F7` (Descompensar).

> ℹ️ O sistema valida o status do lançamento e o tipo do caixa antes — alguns tipos não permitem compensar/descompensar diretamente.

### 🔹 Transferir entre caixas

Operação para mover valor de um caixa para outro (ex.: do PDV para o caixa banco).

1. Tab `Visualizar` → marque os movimentos a transferir.
2. No menu de contexto (botão direito) escolha:
   - **Transferência de Totais - Selecionados** — transfere o valor total
   - **Transferência de Totais - Selecionados (Empresas)** — transfere consolidando por empresa
   - **Transferência Individuais - Selecionados** — uma transferência por movimento
3. Confirme o caixa de destino e a data.
4. O sistema cria dois lançamentos (saída no caixa origem + entrada no destino) com vinculação entre eles.

Para cheques há opções específicas:

- **Transferência de Cheque - Saída** — transferir cheque
- **Transferência de Cheque - Saída (Selecionados)** — em lote

### 🔹 Renegociar cheque

Quando um cheque é devolvido ou precisa ter prazo renegociado:

1. Tab `Visualizar` → encontre o cheque (use o filtro de tipo cheque).
2. No menu de contexto: **Renegociar Cheque**.
3. Confirme os dados da renegociação.
4. O cheque original passa a aparecer na aba **Cheque Renegociado**; o novo título fica vinculado.

Para reverter: menu de contexto → **Cancelar Renegociação do Cheque**.

Para investigar: **Ver vínculos da Renegociação** mostra a árvore renegociado→original.

### 🔹 Conferência de Caixa

Aba `Operações → Conferência de Caixa`:

1. Selecione o caixa e o período.
2. Clique em **Buscar Conferência** — o sistema carrega o saldo esperado vs o lançado.
3. Identifique divergências (lançamentos faltando, valores incorretos).
4. Ajuste pelos lançamentos individuais (volte para a tab `Visualizar`).

### 🔹 Conciliação de Cartões

Aba `Operações → Conciliação Cartões`:

1. Clique em **Importar Conciliação Cartão** — selecione o arquivo enviado pela operadora.
2. O sistema carrega as linhas (cada uma é uma transação reportada pela operadora).
3. Clique em **Buscar Conciliação Cartão** — o sistema cruza com os lançamentos de cartão do caixa por NSU, número de autorização, data e valor.
4. Para cada linha o status pode ser:
   - **Conciliado OK/Ajustado** — bateu
   - **Conciliado Divergente** — bateu mas com diferença (valor, data, etc.)
   - **Não Conciliado** — não encontrou correspondência
5. Marque os lançamentos a confirmar (botão **Seleção Aut.** seleciona os "OK" automaticamente).
6. **Gravar** — confirma as conciliações.
7. **Confirmar Divergentes** — aceita os divergentes manualmente.
8. **Desfazer** — reverte a conciliação.

### 🔹 Conciliação Bancária (Boletos)

Aba `Operações → Conciliação Bancária`:

1. Clique em **Buscar Boleto Retorno** — abre arquivo CNAB de retorno do banco.
2. **Executar Processar Boleto Retorno** — processa as ocorrências, batendo cada boleto retornado contra os títulos do sistema.
3. O sistema marca:
   - **Conciliado** — boleto pago, bate com título
   - **Conciliado Divergente** — pago, mas com diferença (valor, juros, etc.)
   - **Previsão** — agendado/programado
4. Use **Seleção Aut.**, **Desfazer Sel.**, **Gravar**, **Gravar com Divergência** conforme o caso.
5. Para movimentos "Previsão", o menu de contexto tem **Colocar na Previsão** / **Remover da Previsão**.

### 🔹 Rateio contábil

Aba `Rateio` (dentro do Cadastrar): mesma lógica do Rateio em [Pagar e Receber](documentacao_pagar_e_receber.md) — uma ou mais linhas com `Plano de Contas + Centro de Custo + Empresa + Valor/Percentual + Histórico + Data`. O **Total** precisa fechar com o valor do lançamento e o **percentual** precisa fechar em 100%.

### 🔹 Anexar imagens

Aba `Imagens` (dentro do Cadastrar): mesma operação de Pagar e Receber — origem PC, Banco de Dados ou Câmera, com opção de marcar uma como Padrão e flag PDF/Inativo.

### 🔹 Localizar / filtrar — recursos extras

- **Salvar Pesquisa** — guarda os filtros atuais com um nome.
- **Localizar Pesquisa** — abre lista de pesquisas salvas para carregar.
- **Salvar Padrão** (menus de contexto) — guarda o tipo de operação, a loja e as datas como padrão da próxima abertura.
- **Ver vínculos** — em movimentos com vínculo (transferência, renegociação, origem/destino), mostra a árvore completa.

### 🔹 Atalhos contextuais (menu direito)

Em vários grids o menu de contexto oferece atalhos rápidos:

- **Ir para Pessoa** — abre o cadastro da pessoa do lançamento
- **Ir para Movimentação** — abre a venda/compra que originou
- **Ir para ContasPR** — abre o título em **Pagar e Receber** (tela `301`)
- **Ir para Caixa Geral** — abre o lançamento de caixa correspondente
- **Copiar / Buscar Nº Autorização / NSU / Vl. Orig/Bruto** — pega o dado para colar/pesquisar em outro contexto
- **Cadastrar → Caixa Geral / Contas PR** — cria registro novo a partir do contexto

---

## ✅ Validações comuns ao salvar

A validação ao gravar tem dezenas de regras. Os pontos mais comuns:

1. **Detalhes não podem estar em edição** (rateio, imagem) — feche antes de gravar.
2. **Campos obrigatórios preenchidos** (Caixa, Valor, Data, Tipo de Operação).
3. **Validação de cartão** quando aplicável — campos do cartão precisam estar consistentes.
4. **Validação de cheque** quando aplicável — banco/agência/conta válidos.
5. **Rateio fecha em 100%** quando há lançamento de rateio.
6. **Permissão por empresa por usuário** — o usuário precisa ter permissão de criar/editar lançamento naquela empresa.
7. **Permissão por caixa por usuário** — o usuário precisa ter permissão de operar aquele caixa (configurado em **Cadastro de Usuários**).
8. **Pendência impede fechamento** — se for fechamento de caixa, lançamentos pendentes (não compensados, em divergência) podem bloquear.

Quando uma validação falha, o sistema mostra a mensagem específica e posiciona o cursor/aba no campo problemático.

---

## 🔐 Modos de abertura

A tela tem comportamentos diferentes conforme **quem a abriu**:

| Modo | O que faz |
|------|-----------|
| **Normal** | Abertura padrão pela pesquisa `F1 → 302` |
| **Fechamento Caixa** | Abertura específica para fechamento de caixa (do turno/período) |
| **Cadastrar pelo OFX** | Abertura via importação automática de extrato OFX |
| **Zerar Caixas** | Abertura para zerar valores de caixas (operação especial) |

O modo é definido pela tela que abre a `Caixa Geral` e ajusta validações, botões disponíveis e permissões.

---

## 💡 Exemplos práticos

### Lançar entrada manual no caixa do PDV

1. Pesquisa `F1` → `302` → **Caixa**: selecione `PDV LOJA SEDE — CAIXA 01`.
2. **Novo**.
3. **Tipo de Operação**: `Entrada`.
4. **Valor**: `R$ 50,00`.
5. **Histórico**: `RECEBIMENTO AVULSO — CLIENTE X`.
6. **Plano de Contas** + **Centro de Custo**: classifique.
7. **Gravar**.

### Transferir total do PDV para o caixa banco

1. Tab `Visualizar` → filtre por **Caixa** = `PDV LOJA SEDE — CAIXA 01`, **Data** de hoje, **Status** = não compensados.
2. Marque todos os movimentos da coluna `Sel.`.
3. Menu de contexto → **Transferência de Totais - Selecionados**.
4. Escolha o caixa de destino (ex.: `BANCO BRADESCO — CC 1234-5`) e confirme a data.
5. O sistema cria saída no PDV e entrada no caixa banco, vinculadas.

### Compensar cheques recebidos

1. Tab `Visualizar` → na sub-aba `Pagamentos → Cheque`, filtre por cheques **não compensados** com vencimento até hoje.
2. Marque na coluna `Sel.` os cheques que foram compensados pelo banco.
3. `F6` (Compensar).

### Conciliar cartões a partir do arquivo da operadora

1. Tab `Operações → Conciliação Cartões`.
2. **Importar Conciliação Cartão** → selecione o arquivo `.txt`/`.csv` da operadora.
3. **Buscar Conciliação Cartão** → o sistema cruza com as vendas em cartão.
4. **Seleção Aut.** → marca todos os "Conciliado OK".
5. **Gravar** → confirma.
6. Para os "Conciliado Divergente", revise valor por valor e use **Confirmar Divergentes** ou ajuste antes.

### Conciliar boletos recebidos pelo banco

1. Tab `Operações → Conciliação Bancária`.
2. **Buscar Boleto Retorno** → selecione o arquivo CNAB de retorno.
3. **Executar Processar Boleto Retorno**.
4. Revise as ocorrências:
   - **Conciliado** → bate, deixa marcado.
   - **Conciliado Divergente** → revise (juros/multa/desconto).
   - **Não Conciliado** → investigue.
5. **Gravar**.

### Renegociar cheque devolvido

1. Tab `Visualizar` → encontre o cheque devolvido.
2. Marque na coluna `Sel.`.
3. Menu de contexto → **Renegociar Cheque**.
4. Confirme os dados.
5. O cheque original aparece na aba `Cheque Renegociado`.

---

## ❓ FAQ / Problemas comuns

**Lancei um movimento e não aparece na consulta.**
Provavelmente está com filtro de **Caixa** errado ou **Data** fora do período. Confira os filtros do topo.

**Tentei compensar um cheque mas o botão não funciona.**
Verifique se há ao menos um movimento marcado na coluna `Sel.` e se o status atual permite a operação. Cheques já compensados não podem ser compensados de novo.

**Importei a conciliação de cartão mas muitos ficaram "Não Conciliado".**
As linhas que não bateram podem ser por: NSU/autorização diferente do registrado, valor diferente, data diferente, ou cartão lançado em outro caixa. Investigue caso a caso.

**O retorno de boleto marcou divergência mas o valor está certo.**
Pode ser por juros/multa/desconto cobrado/aplicado. Revise o detalhe e use **Gravar com Divergência** se for aceitável.

**Modo "Fechamento Caixa" — o que é?**
Modo especial aberto a partir da operação de fechamento. Pode bloquear o fechamento se houver pendências (lançamentos não compensados, divergências de conciliação). Resolva as pendências antes de tentar fechar.

**Modo "Cadastrar pelo OFX" — preciso configurar algo antes?**
Sim. A conta corrente do caixa precisa ter o `Código OFX` preenchido em **[Contas Correntes](documentacao_contas_correntes.md)** (tela `11`). Sem isso, o sistema não consegue casar as linhas do arquivo OFX com a conta correta.

**Não consigo lançar movimento no caixa de outro usuário.**
A operação por caixa é controlada por permissão por usuário. Solicite ao administrador a permissão de uso do caixa no **Cadastro de Usuários**.

**Posso transferir entre caixas de empresas diferentes?**
Use **Transferência de Totais - Selecionados (Empresas)** para consolidar por empresa. A transferência normal pode bloquear quando as empresas são diferentes (depende da configuração).

**O menu de contexto tem "Edição Parcial" — o que faz?**
Permite alterar apenas alguns campos do lançamento sem ter que reabrir tudo. Útil para corrigir histórico, plano de contas, centro de custo etc.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Relação |
|------|:---:|---------|
| [Cadastro de Caixa Geral](documentacao_caixa_geral.md) | `13` | Define os caixas operados aqui |
| [Pagar e Receber](documentacao_pagar_e_receber.md) | `301` | Títulos são quitados gerando lançamento no caixa |
| Quitação | `303` | Tela específica de quitação que alimenta o caixa |
| [Portadores](documentacao_portadores.md) | `12` | Configuração de cobrança / boletos / conciliação |
| [Formas de Pagamento](documentacao_formas_pagamento.md) | `7` | Usada em conciliação de cartões |
| [Contas Correntes](documentacao_contas_correntes.md) | `11` | Conta vinculada ao caixa (importação OFX) |
| [Plano de Contas](documentacao_plano_de_contas.md) | `14` | Classificação contábil dos lançamentos e rateio |
| [Centros de Custos](documentacao_centros_de_custos.md) | `15` | Centro de custo dos lançamentos |
| Histórico de Caixa Geral | `208` | Histórico/relatório dos lançamentos |
| Histórico de Lançamento Rateio | `212` | Histórico do rateio contábil |

---

## ⚠️ Limites desta documentação

Esta documentação foi construída a partir da inspeção direta do comportamento da tela no Sol.NET. Por se tratar de uma tela operacional muito grande, com integrações externas (TEF, retorno online de boletos, OFX, conciliação de cartões), **a doc cobre os fluxos principais e as regras mais comuns**, mas não esgota:

- **Variantes específicas de cada operadora de cartão e cada banco** na conciliação.
- **Integrações TEF / HetoBank / OFX** — o comportamento depende do provedor e do convênio.
- **Operações em lote complexas** (zerar caixa, fechamento em massa, transferência consolidada).
- **Regras automáticas que rodam dentro do banco de dados** ao salvar/alterar/excluir um registro.
- **Variações por release** — esta tela evolui frequentemente.

Para casos fora do comum, em especial integrações específicas (operadoras, bancos, OFX), consulte o suporte Hetosoft.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 5.0 (refeito do zero descartando a documentação anterior)
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo Financeiro
