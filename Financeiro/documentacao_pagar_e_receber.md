# 📄 Pagar e Receber - Sol.NET

## 🎯 Visão Geral

A tela **Pagar e Receber** é o centro operacional do Financeiro: é onde **títulos a pagar** (contas com fornecedores, prestadores, etc.) e **títulos a receber** (faturas de clientes, vendas a prazo, etc.) são **lançados**, **consultados**, **quitados**, **estornados**, **renegociados** e **acompanhados** — incluindo emissão e retorno de **boletos**, anexação de **imagens** (notas, comprovantes), **rateio contábil** por plano de contas / centro de custo / empresa, e **vinculação** com a venda/compra que originou o título.

Por ser uma tela operacional ampla, ela é aberta em **modos** diferentes conforme a origem (consulta normal, acerto manual, estorno de movimento, quitar individual a partir do movimento, importação OFX, etc.). A maior parte do uso é o **modo normal**: pesquisa de títulos, lançamento de novos, quitação e estorno.

> ℹ️ **Esta documentação cobre os fluxos principais.** A tela tem dezenas de validações cruzadas, flags de comportamento e integrações (TEF, HetoBank, boletos online, RH, OFX, conciliação). Casos fora do comum — especialmente integrações específicas — devem ser confirmados com o suporte.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Pagar e Receber |
| **Código (`F1`)** | `301` |

Abra a pesquisa universal (atalho `F1`) e digite **`301`** ou parte do nome **`Pagar e Receber`**.

A tela **também é aberta automaticamente** por outras telas em modos especiais — por exemplo, ao clicar em "Localizar ContasPR" / "Estornar" / "Quitar" no histórico de movimentos, ou ao usar funções específicas de RH e cheque.

---

## 🧭 Estrutura da tela (visão rápida)

### Tab `Visualizar` (consulta de títulos)

A tab `Visualizar` é a tela de busca/consulta — onde você filtra e localiza os títulos para depois agir sobre eles (quitar, estornar, cancelar, emitir boleto, etc.).

Filtros principais:

- **Tipo** (entrada/saída) — Receber, Pagar ou ambos
- **Empresa**
- **Campo Pesquisado** + **Condição** + texto livre — pesquisa por descrição, número de documento, pessoa, etc.
- **Data** + **Data Inicial** / **Data Final** — período de emissão / vencimento / quitação (escolhido em `Data`)
- **Status** — Em Aberto, Quitado, Vencido, Cancelado, Renegociado etc.
- **Portador** — filtra por portador específico
- **Usuário Cadastrou** — filtra pelo usuário que criou o título

O grid de resultados mostra os títulos. Acima dele, um sumário com totais por categoria (Quitados, Vencidos, A Vencer, Cancelados/Renegociados) e os totais agregados (Total Geral, Total em Aberto, Total Quitado).

Pesquisas frequentes podem ser **salvas** (`Salvar Pesquisa`) e **localizadas** depois (`Pesquisar`).

### Tab `Cadastrar` (lançamento e edição de um título)

Quando você clica em **Novo** ou **Alterar** (ou dá duplo clique em uma linha), a tela mostra o painel de cadastro com **várias sub-abas**:

| Sub-aba | Para quê serve |
|---------|----------------|
| **Dados Cadastrais** | Cabeçalho do título — pessoa, valor, datas, tipo, portador, condição, plano de contas, centro de custo, observações, dados RH |
| **Lançamento** | Geração das parcelas (manual ou por condição de pagamento) — define como o valor será dividido no tempo |
| **Rateio** | Rateio do valor do título em múltiplas linhas (plano de contas + centro de custo + empresa + valor/percentual) |
| **Boleto** | Emissão e gestão de boletos do título (valor, vencimento, multa/juros/desconto/abatimento, status: gerado/remessa/ativo/baixado) |
| **Imagem** | Anexar fotos/documentos ao título (nota fiscal, comprovante, etc.) |
| **Vínculos** | Outros títulos vinculados a este (ex.: parcelas do mesmo movimento) |
| **Original** / **Renegociada** / **Contas Orig** | Histórico de renegociação — quando este título é fruto de renegociação ou já foi renegociado |
| **Datas e Valores** | Datas de quitação/renegociação/cancelamento/estorno + valores baixados (parcela, desconto, multa/juros, acréscimo) |
| **Pagamentos** | Visualização do histórico de pagamentos, cheques, cartões, créditos gerados/usados (para títulos já com baixa) |
| **Movimento** | Vínculo com a venda/compra que originou o título |
| **Portador** | Configurações específicas do portador no título (impresso, usuário, caixa) |

> ℹ️ Algumas abas só aparecem ou só são editáveis dependendo do **estado** do título (em aberto / quitado / cancelado / renegociado) e do **tipo de operação** sendo feita.

---

## 🔧 Fluxos principais

### 🔹 Lançar um título (novo)

1. Pesquisa `F1` → digite `301` → abre a tela.
2. Clique em **Novo**.
3. **Aba `Dados Cadastrais`**:
   - **Tipo (Pagar/Receber)** — escolha o tipo do título
   - **Empresa** — empresa proprietária do título
   - **Pessoa** — fornecedor/cliente (busca por pesquisa)
   - **Data Emissão**
   - **Data Vencimento** — precisa ser ≥ data de emissão
   - **Valor da Parcela** — valor total (será distribuído nas parcelas se houver)
   - **Número do Documento** — para Contas a Pagar com pessoa, **o sistema valida que esse número não está duplicado para a mesma pessoa** (regra `varNumeroDocCPRValida` ativa por padrão)
   - **Tipo de Documento** — link com [Tipos de Documentos]
   - **Portador** — link com [Portadores](documentacao_portadores.md) — quem cobra/recebe
   - **Plano de Contas** + **Centro de Custo** + **Tipo de Conta PR** — classificação contábil
   - **% Desconto / Multa / Juros Mora** — opcionais
   - **Observação**
   - (Se a pessoa é funcionário) **MES/ANO** + **Nível RH** — vincula o título ao Lançamento de RH; obrigatório quando a pessoa for funcionário e tipo for "Pagar"
4. **Aba `Lançamento`** — escolha o modo:
   - **Manual**: informe `Quantidade de Parcelas`, `Dias entre Parcelas`, `Tipo de Intervalo`, `Tipo de Operação` e clique em **Gerar Registros**. Limite máximo é 999 parcelas (recomendado até 100).
   - **Condição de Pagamento**: escolha uma `Condição de Pagamento` cadastrada (tela `8`), opcional `Valor Entrada` e `Quantidade de Parcelas`, e clique em **Gerar Parcelas**.
   - O **Total Parcelado** precisa fechar com o **Valor** do título — o sistema mostra a `Diferença`.
5. (Opcional) **Aba `Rateio`** — quebre o valor em várias linhas de plano/centro/empresa (ver "Rateio contábil" abaixo).
6. (Opcional) **Aba `Boleto`** — gere boleto se for um título a receber via boleto (ver "Emitir boleto" abaixo).
7. (Opcional) **Aba `Imagem`** — anexe documentos (nota, comprovante, contrato).
8. Clique em **Gravar**.

> ℹ️ **Permissões por empresa**: o sistema verifica se o usuário tem permissão para inserir título daquela empresa naquele tipo (Pagar/Receber) através das permissões cadastradas em **Cadastro de Usuários × Formulário × Empresa**. Sem permissão, o lançamento é bloqueado.

### 🔹 Localizar / filtrar títulos

1. Na tab `Visualizar`, ajuste os filtros do topo:
   - **Tipo** (Receber/Pagar)
   - **Empresa**
   - Selecione o **Campo Pesquisado** (Descrição, Documento, Pessoa, etc.) + **Condição** (igual/contém/começa) + digite o termo
   - **Período** — escolha em `Data` (Emissão/Vencimento/Quitação/Cadastro) e ajuste `Data Inicial`/`Data Final`. O atalho `GenModificarDatas` permite mover rapidamente para mês anterior/atual/próximo
   - **Status** — restrinja a Em Aberto, Quitado, etc.
   - **Portador**, **Usuário** — refine
2. Aperte **Enter** (no filtro) ou clique no botão de buscar — o grid recarrega.
3. O **sumário** acima do grid mostra automaticamente os totais por categoria.

#### Pesquisas salvas

- **Salvar Pesquisa**: guarda os filtros atuais com um nome.
- **Pesquisar** (botão): abre a lista de pesquisas salvas para carregar uma.
- **Excluir Pesquisa**: remove uma pesquisa salva.

> ℹ️ **Permissão de mudar datas**: dependendo da configuração, alguns usuários ficam com `Data Inicial` e `Data Final` travadas no dia (sem poder mudar). O parâmetro é configurado em **Cadastro de Usuários** (`conConfig_PermissaoMudaDataConsultaCPR`).

### 🔹 Quitar (baixar) títulos

A quitação dá baixa em um ou mais títulos selecionados. O atalho de teclado é **F6** (botão `Quitar(F6)`).

1. Na tab `Visualizar`, encontre os títulos a quitar.
2. **Marque** a coluna `Sel.` (OPCAO) dos títulos desejados — pode marcar vários.
3. Clique em **Quitar** (ou pressione `F6`).
4. O sistema valida (regras abaixo) e, se passar, abre a tela de **Quitação** (tela `303`) com os títulos selecionados.

**Regras impeditivas comuns**:

- **Status diferente de "Em Aberto"** — só títulos em aberto podem ser quitados. Mensagem: *"Apenas títulos com status 'EM ABERTO' podem ser quitados!"*.
- **Mistura de tipos** — não pode misturar `Receber` e `Pagar` na mesma quitação. Mensagem: *"Não é permitido quitar Pagar e Receber juntos!"*.
- **Mistura de tipos de crédito** — Pré-Créditos e títulos normais têm regras separadas.
- **Empresas diferentes** — quando `varAgruparContasQuitacao` está ligado, todos os títulos selecionados precisam ser da **mesma empresa**.
- **Permissão por empresa** — o usuário precisa ter permissão de quitar para cada empresa envolvida.

**Requitar** (refazer quitação): a tela tem um modo `ModoRequitar` para refazer uma quitação que está em estado especial (consulte o suporte se precisar usar).

### 🔹 Estornar

Estornar = desfazer a quitação de um título já quitado.

1. Tab `Visualizar` → encontre o título quitado.
2. Marque a coluna `Sel.`.
3. Clique em **Estornar**.
4. O sistema reverte a quitação, retornando o título para "Em Aberto" (apaga os registros em `CONTROLE_FINANCEIRO` e remove valores baixados).

> ℹ️ Estorno **não** afeta o cadastro do título original — apenas remove a quitação. O título volta a ter status "Em Aberto" e pode ser quitado novamente.

### 🔹 Cancelar título

Cancelar = anular um título em aberto (não emite estorno — apenas marca como cancelado).

1. Tab `Visualizar` → marque o(s) título(s) na coluna `Sel.`.
2. Clique em **Excluir** (cancelamento).
3. O sistema valida (regras abaixo) e, se passar, cancela e registra a data em `Cancelamento`.

**Regras impeditivas**:

- **Sem títulos marcados** — *"Selecione os títulos para serem cancelados!"*.
- **Status diferente de "Em Aberto"** — *"Apenas títulos com status 'EM ABERTO' podem ser cancelados!"*.
- **Título oriundo de renegociação** — *"Títulos que foram 'oriundos de uma renegociação' — Você pode fazer o 'Cancelamento da Renegociação' — Deseja Cancelar individualmente?"*.
- **Vinculado com RH fechado** — *"Não Permitido Cancelar, Conta Vinculada com Lançamento RH Fechado!"*.
- **Tem boleto de remessa ativo** — não permitido cancelar enquanto há boleto em remessa que ainda não foi baixado.
- **Sem permissão por empresa** — bloqueio individual por empresa.

### 🔹 Renegociar títulos

Renegociar = criar um (ou vários) título(s) novo(s) substituindo títulos antigos, podendo ajustar valores com multa/juros/desconto.

1. Tab `Visualizar` → marque os títulos originais.
2. Clique em **Renegociar** (no menu de funções ou no botão equivalente).
3. O painel `Renegociação` mostra:
   - **Nº Parcelas Reneg** — quantidade de novas parcelas
   - **Valor Parcelas Reneg** — valor unitário
   - **Multa / Juros / Desconto Reneg** — ajustes
   - **Total Renegociado** — valor final
4. Preencha e confirme.
5. O sistema:
   - Marca os títulos originais como **renegociados** (status muda)
   - Cria os novos títulos com referência aos originais
   - Mantém o histórico nas abas `Original` (vê os títulos que deram origem) e `Renegociada` (vê os títulos novos)

### 🔹 Rateio contábil

A aba `Rateio` permite quebrar o valor do título em várias linhas — cada uma com **Plano de Contas + Centro de Custo + Empresa + Valor + Percentual + Histórico + Data**.

1. Aba `Rateio` → clique em **Inserir** (botão `btnLrNovo`).
2. Preencha a linha:
   - **Empresa** (combo)
   - **Plano de Contas** (busca por pesquisa) — link com tela `14`
   - **Centro de Custo** (busca por pesquisa) — link com tela `15`
   - **Valor** ou **Percentual** (o sistema calcula o outro)
   - **Data** + **Histórico** (descrição livre)
3. **Atualizar** para salvar a linha.
4. Repita.
5. O painel inferior mostra: **Valor Total** (do título), **Valor Rateado** (soma das linhas), **Diferença** (deve ficar zero), **Percentual Total** (deve fechar em 100%).

A validação não deixa salvar se o rateio não bater com o valor total.

### 🔹 Emitir boleto

A aba `Boleto` gera/gerencia os boletos do título (apenas para títulos a Receber com portador do tipo Boleto).

1. Aba `Boleto` → clique em **Inserir** (botão `btnNovoBoleto`).
2. Só permite criar um novo boleto se **não há boleto ativo** anteriormente (mensagem: *"Já existe boleto ativo!"*).
3. Preencha:
   - **Vencimento Boleto** — default = data do vencimento do título ou hoje (se vencimento já passou)
   - **Valor Boleto** — default = valor da parcela
   - **Multa / Juros / Desconto / Abatimento** (valor)
   - **Datas** de Multa/Juros, Desconto, Abatimento, Protesto
   - **Portador Boleto** — default = portador do título
   - **Observação**
4. **Atualizar** para salvar.

Status do boleto:
- **Gerado** — boleto foi gerado pelo sistema
- **Remessa** — arquivo de remessa CNAB enviado ao banco
- **Ativo** — boleto válido (apenas um ativo por vez)
- **Rejeitado** — banco rejeitou
- **Baixado** — boleto pago/baixado

**Excluir boleto**: só permite excluir se `Gerado = 0` — boletos já gerados não podem ser apagados.

#### Buscar retorno

O Sol.NET processa arquivos de retorno bancário (CNAB) e online:

- **Buscar Boleto Retorno** — abre arquivo de retorno
- **Buscar Retorno Web** — consulta online
- **Executar Processar Boleto Retorno** — processa retornos online em lote (a partir do portador selecionado em `Portador Boleto Retorno`)

Para cada registro:
- Se encontrou o título correspondente (por Nosso Número + Portador) → marca como baixado/compensado
- Se não encontrou → registra em "Erro" (mostra dados do boleto para investigação)

> ℹ️ Detalhes de **configuração de cada banco** (layout CNAB, código de transmissão, credenciais online) ficam em **Portadores** (tela `12`).

### 🔹 Anexar imagens / documentos

A aba `Imagem` permite anexar fotos/scans ao título — nota fiscal, comprovante de pagamento, contrato, etc.

1. Aba `Imagem` → **Inserir** (botão `btnNovoImg`).
2. Origem da imagem:
   - **PC** — selecionar arquivo do computador
   - **Banco de Dados** — carregar imagem armazenada
   - **Câmera** — capturar foto direto da webcam/câmera
3. Confirme a inserção.
4. **Atualizar** para salvar.
5. Você pode marcar uma imagem como **Padrão** (aparece como principal nas visualizações).

### 🔹 Vincular ao movimento

A aba `Movimento` mostra a venda/compra que originou o título (quando o título veio de uma operação fiscal). É só leitura — o vínculo é criado automaticamente no momento em que a venda/compra gera os títulos.

### 🔹 Cadastrar pelo OFX

Quando a tela é aberta no modo `9` (Cadastrar pelo OFX), o fluxo é otimizado para importação automática a partir de extrato bancário OFX. O modo é acionado por outra tela (não diretamente da pesquisa `F1`).

---

## ✅ Resumo das principais validações ao salvar

A função `Validar` da tela tem dezenas de regras. Os pontos mais comuns:

1. **Detalhes não podem estar em edição** (boleto, imagem, rateio) — feche antes de gravar.
2. **Campos obrigatórios preenchidos** (Pessoa, Valor, Datas, Portador, etc.).
3. **Número de Documento único por pessoa** (A Pagar) — o sistema mostra todos os dados do documento existente em caso de duplicidade.
4. **RH obrigatório se pessoa é funcionário** (e tipo = Pagar).
5. **Empresa do título = empresa do funcionário** (RH).
6. **Lançamentos RH não retroagem antes do último fechado** (busca em `LANCAMENTO_RH`).
7. **Permissão por nível RH** (Nível 2 e 3 exigem permissões específicas).
8. **Data Vencimento ≥ Data Emissão**.
9. **Total das parcelas fecha com o valor do título** (Diferença = 0).
10. **Permissões por empresa por usuário** — para inserir/editar/quitar/cancelar.
11. **Rateio fecha em 100%** quando há lançamento de rateio.
12. **Boleto ativo bloqueia novo boleto** — só um ativo por vez.

Quando uma validação falha, o sistema mostra a mensagem específica e posiciona o cursor/aba no campo problemático.

---

## 🔐 Modos de comportamento (`TipoComportamento`)

A tela tem comportamentos diferentes conforme **quem a abriu**:

| Modo | O que faz |
|------|-----------|
| `0` | **Normal** — abertura padrão pela pesquisa `F1 → 301` |
| `1` | **Acerto Manual** — abertura para acerto manual de títulos (form é renomeado `FrmContasPR_Pag`) |
| `3` | **Estornar a partir do Movimento** — abertura via "Estornar" no histórico de movimento |
| `4` | **Renegociar Cheque** — abertura para renegociar cheque (form é renomeado `FrmContasPR_Cheque`) |
| `5` | **Limpar Portador** — operação rápida de remover portador |
| `6` | **Limpar Portador Selecionados** — operação em lote |
| `7` | **Quitar Individual a partir do Movimento** — abertura via "Quitar" no histórico de movimento |
| `8` | **Atualizar Boleto** — não entra em permissão de editar/salvar |
| `9` | **Cadastrar pelo OFX** — abertura via importação OFX (form é renomeado `FrmContasPR_OFX`) |

O modo é definido pela tela que abre a `Pagar e Receber` e ajusta validações, botões disponíveis e permissões.

---

## 💡 Exemplos práticos

### Lançar uma conta a pagar simples

1. Pesquisa `F1` → `301` → **Novo**.
2. **Tipo**: `Pagar`
3. **Empresa**: escolha
4. **Pessoa**: selecione o fornecedor
5. **Data Emissão**: hoje
6. **Data Vencimento**: 30 dias
7. **Valor**: `R$ 1.000,00`
8. **Número Documento**: `NF 1234`
9. **Tipo de Documento**: `NOTA FISCAL`
10. **Portador**: `CAIXA — DINHEIRO`
11. **Plano de Contas**: `2.001 FORNECEDORES`
12. **Centro de Custo**: `1.001 ADMINISTRATIVO`
13. Aba `Lançamento` → modo **Manual** → `Quantidade de Parcelas: 1`, `Dias entre Parcelas: 0` → **Gerar Registros**.
14. **Gravar**.

### Lançar conta a receber parcelada

1. **Novo** → **Tipo**: `Receber`.
2. **Pessoa**: selecione o cliente.
3. **Valor**: `R$ 900,00`.
4. Aba `Lançamento` → modo **Condição de Pagamento** → escolha `30/60/90 DIAS` → **Gerar Parcelas**. O sistema gera três parcelas de `R$ 300,00` com 30 dias entre elas.
5. (Opcional) Aba `Boleto` → **Inserir** para gerar boleto da primeira parcela.
6. **Gravar**.

### Quitar várias contas de uma vez

1. Tab `Visualizar` → filtre por **Status: Em Aberto** e ajuste o **Período**.
2. Marque na coluna `Sel.` os títulos.
3. **F6** (ou clique em `Quitar`).
4. Na tela de Quitação (tela `303`), informe forma de pagamento, valor, eventuais descontos/multas e confirme.

### Renegociar um título em atraso

1. Tab `Visualizar` → encontre o título vencido.
2. Marque na coluna `Sel.`.
3. **Renegociar** (no menu de funções).
4. No painel `Renegociação` informe:
   - `Nº Parcelas Reneg`: `3`
   - `Multa Reneg`: `R$ 50,00`
   - `Juros Reneg`: `R$ 30,00`
   - `Desconto Reneg`: `0`
5. Confirme. O título original muda para "Renegociado" e três novos títulos são criados com referência ao original (visíveis nas abas `Original`/`Renegociada`).

### Anexar comprovante de pagamento ao título

1. Abra o título em **Alterar**.
2. Aba `Imagem` → **Inserir**.
3. Clique no botão de origem (PC / Banco de Dados / Câmera) e selecione/capture a imagem.
4. **Atualizar** para salvar.
5. **Gravar** o título.

---

## ❓ FAQ / Problemas comuns

**O sistema diz "Nº do Documento Já Existe para Essa Pessoa" — o que faço?**
Significa que já existe um título a pagar para essa pessoa com esse mesmo número de documento. Confira em **Localizar** — provavelmente é o mesmo documento sendo lançado duas vezes. Se for outro documento, ajuste o número (ex.: incluindo a série).

**Não consigo cancelar o título — sistema diz "Conta Vinculada com Lançamento RH Fechado".**
O título está vinculado a um lançamento de RH que já foi fechado. Reabra o lançamento de RH primeiro (se tiver permissão), depois cancele o título.

**Tentei excluir um boleto e o sistema bloqueou.**
Boletos com `Gerado = 1` não podem ser excluídos (o boleto já foi gerado, possivelmente entregue ao banco/cliente). Use a baixa/cancelamento normal pelo retorno bancário ou pela tela de boletos.

**Não consigo quitar Receber e Pagar juntos.**
É regra — a quitação processa um lado de cada vez. Faça duas quitações separadas.

**Lancei a quantidade de parcelas mas o Total não fecha com o Valor.**
Ajuste o valor das parcelas ou a quantidade até que o **Total Parcelado** seja igual ao **Valor** (o sistema mostra a `Diferença`). Para parcelas iguais, deixe a última absorver os centavos de arredondamento.

**O botão Quitar(F6) está desabilitado.**
Você precisa estar no modo **leitura** (sem edição em andamento) e ter pelo menos um título marcado na coluna `Sel.`. Se há edição em andamento, **Gravar** ou **Desfazer** primeiro.

**Modo "Acerto Manual" — o que é?**
Modo especial aberto por outras telas (ex.: caixa, conferência) para ajustar manualmente o histórico de um título. Tem regras próprias e é geralmente usado pela equipe de suporte.

**O título sumiu da lista depois que quitei.**
Você provavelmente está filtrando por **Status: Em Aberto**. Mude o filtro para **Quitado** ou para o status correspondente.

**Importação OFX não encontrou um título.**
O OFX usa o `Código OFX` da conta corrente (cadastrado em **Contas Correntes**, tela `11`) para casar. Confirme que o código está preenchido e bate com o que o banco envia.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Relação |
|------|:---:|---------|
| Quitação | `303` | Tela aberta a partir de `Quitar(F6)` |
| Histórico de ContasPR | `207` | Histórico/relatório dos títulos |
| [Portadores](documentacao_portadores.md) | `12` | Define como o título é cobrado/recebido (incl. boletos) |
| [Formas de Pagamento](documentacao_formas_pagamento.md) | `7` | Usada na quitação |
| [Cond. de Pagamento](documentacao_condicoes_pagamento.md) | `8` | Modo de gerar parcelas |
| [Plano de Contas](documentacao_plano_de_contas.md) | `14` | Classificação contábil do título e do rateio |
| [Centros de Custos](documentacao_centros_de_custos.md) | `15` | Centro de custo do título e do rateio |
| [Caixa Geral](documentacao_caixa_geral.md) | `13` | Caixa usado na quitação |
| Tipos de Documentos | — | Cadastro de tipos (Nota Fiscal, Duplicata, etc.) |
| Tipos de Contas PR | `82` | Classificação do título |

---

## ⚠️ Limites desta documentação

Esta documentação foi construída a partir da inspeção direta do comportamento da tela no Sol.NET. Por se tratar de uma tela operacional muito grande, com integrações externas (TEF, HetoBank, retorno online de boletos, OFX, RH), **a doc cobre os fluxos principais e as regras mais comuns**, mas não esgota:

- **Variantes específicas de cada banco** para emissão e retorno de boletos.
- **Integrações TEF / HetoBank / OFX** — o comportamento depende do convênio e do provedor.
- **Regras de RH** — a parte de Lançamento RH (MES/ANO, Nível, validações de fechamento) é coberta também pela tela do módulo RH.
- **Operações em lote complexas** (renegociação coletiva, cancelamento em massa, processamento de retorno em volume).
- **Regras automáticas que rodam dentro do banco de dados** ao salvar/alterar/excluir um registro.
- **Variações por release** — esta tela evolui frequentemente.

Para casos fora do comum, em especial integrações específicas, consulte o suporte Hetosoft.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 5.0 (refeito do zero descartando a documentação anterior)
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo Financeiro
