---
title: "Glossário do Sol.NET"
permalink: /glossario/
---

# 📖 Glossário — Sol.NET

## 🎯 Visão Geral

Glossário central do Sol.NET ERP. Reúne os termos que aparecem todo dia na operação — documentos fiscais, conceitos de tributação, vocabulário de movimentação, estoque e financeiro. Cada termo tem definição curta e, quando faz sentido, lista as telas onde ele é usado.

> 💡 **Como usar.** A maioria das páginas do portal aponta para este glossário na primeira vez que mencionam um termo. Cada termo aqui tem uma âncora estável — você pode linkar direto, ex.: `glossario.md#nf-e`.

---

## 🔤 Índice alfabético

[CBS](#cbs) · [Cashback](#cashback) · [Centro de Custo](#centro-de-custo) · [CFOP](#cfop) · [Chave de Acesso](#chave-de-acesso) · [Conferência](#conferencia) · [CSOSN](#csosn) · [CST](#cst) · [CT-e](#ct-e) · [DANFE](#danfe) · [Estornar](#estornar) · [Faturar](#faturar) · [Finalizar](#finalizar) · [IBS](#ibs) · [ICMS](#icms) · [ICMS-ST](#icms-st) · [Local de Estoque](#local-de-estoque) · [Manifesto](#manifesto-do-destinatario) · [MDF-e](#mdf-e) · [Movimento](#movimento) · [Mudar](#mudar) · [NCM](#ncm) · [NF-e](#nf-e) · [NF-e de terceiros](#nf-e-de-terceiros) · [NF-e própria](#nf-e-propria) · [NSU](#nsu) · [Plano de Contas](#plano-de-contas) · [Quitar](#quitar) · [Reforma Tributária](#reforma-tributaria) · [Saldo](#saldo) · [Saldo PEPS](#saldo-peps) · [Tabela de Preço](#tabela-de-preco) · [Tipo de Movimento](#tipo-de-movimento) · [Transação de Estoque](#transacao-de-estoque)

---

## 📨 Documentos fiscais e SEFAZ

### NF-e

**Nota Fiscal Eletrônica** — documento fiscal eletrônico que registra a circulação de mercadorias entre empresas (B2B) ou para consumidor final. Autorizada pela SEFAZ do estado de origem, identificada por uma [Chave de Acesso](#chave-de-acesso) de 44 dígitos. Substitui a antiga nota fiscal modelo 1/1-A em papel.

**Onde aparece:** [Importar XML](Movimentacao/documentacao_importar_xml.md) (`204`) · [Movimentos de Compras](Movimentacao/Movimentos/movimentos_de_compras.md) (`201`) · [Movimentos de Vendas](Movimentacao/Movimentos/movimentos_de_vendas.md) (`202`) · [Manifestação do Destinatário](Fiscal/documentacao_manifestacao_destinatario.md) (`401`)

### NF-e própria {#nf-e-propria}

NF-e em que **a empresa do Sol.NET é o emissor** — toda venda B2B que sai da empresa é uma NF-e própria. O XML é gerado pelo próprio Sol.NET, assinado e transmitido à SEFAZ.

**Onde aparece:** [Movimentos de Vendas](Movimentacao/Movimentos/movimentos_de_vendas.md) (`202`) · [Importar XML](Movimentacao/documentacao_importar_xml.md) (`204`) (botão `Lançar Próprio` registra a saída no Sol.NET a partir de uma NF-e que a empresa emitiu por fora)

### NF-e de terceiros

NF-e em que **outra empresa é o emissor** e a empresa do Sol.NET é o destinatário — toda compra recebida é uma NF-e de terceiros. Chega via SEFAZ (a partir da [Manifestação](#manifesto-do-destinatario)) ou por importação manual do XML.

**Onde aparece:** [Manifestação do Destinatário](Fiscal/documentacao_manifestacao_destinatario.md) (`401`) · [Importar XML](Movimentacao/documentacao_importar_xml.md) (`204`) · [Movimentos de Compras](Movimentacao/Movimentos/movimentos_de_compras.md) (`201`)

### CT-e

**Conhecimento de Transporte Eletrônico** — documento fiscal eletrônico que registra a prestação de serviço de transporte (frete de carga). Análogo à NF-e, mas para serviço de transporte: emitido pela transportadora, recebido pelo embarcador ou destinatário. Também passa por manifestação na [Manifestação do Destinatário](Fiscal/documentacao_manifestacao_destinatario.md).

**Onde aparece:** [Manifestação do Destinatário](Fiscal/documentacao_manifestacao_destinatario.md) (`401`)

### MDF-e

**Manifesto Eletrônico de Documentos Fiscais** — documento que **agrupa** uma ou mais NF-e/CT-e em um mesmo transporte (uma carga, uma viagem, um veículo). Quem opera transporte próprio precisa emitir MDF-e para cada percurso, declarando o que está sendo levado, por onde e por quem.

**Onde aparece:** sub-aba `MDF-e` dentro de [Movimentos](Movimentacao/Movimentos/documentacao_movimentos.md), quando o Tipo de Movimento envolve transporte próprio.

### DANFE

**Documento Auxiliar da NF-e** — versão impressa (PDF) da NF-e, usada para acompanhar a mercadoria no transporte e para o destinatário conferir. Não é o documento fiscal em si (esse é o XML autorizado), apenas a representação visual.

**Onde aparece:** botão `DANFE` em [Importar XML](Movimentacao/documentacao_importar_xml.md) (`204`) e nos [Movimentos](Movimentacao/Movimentos/documentacao_movimentos.md) (`201/202/203`) após autorização da NF-e.

### Chave de Acesso

Sequência única de **44 dígitos** que identifica cada NF-e/NFC-e/CT-e/MDF-e autorizada pela SEFAZ. Funciona como o número de série do documento fiscal: dois documentos nunca têm a mesma chave. É o que o Sol.NET usa para amarrar uma NF-e recebida à compra correspondente.

**Onde aparece:** grupo `Manifesto` em [Importar XML](Movimentacao/documentacao_importar_xml.md) (`204`) (display apenas — não é digitada) · [Manifestação do Destinatário](Fiscal/documentacao_manifestacao_destinatario.md) (`401`).

### NSU

**Número Sequencial Único** — número que a SEFAZ atribui a cada evento (NF-e, CT-e, manifestação, cancelamento etc.) que envolve a empresa. O Sol.NET usa o NSU para saber até qual ponto já consultou a SEFAZ — assim, da próxima vez, busca só o que é novo. Cada empresa tem seu próprio sequencial.

**Onde aparece:** [Manifestação do Destinatário](Fiscal/documentacao_manifestacao_destinatario.md) (`401`) — botões `Zerar NSU` e demais controles do ciclo de consulta SEFAZ.

### Manifestação do Destinatário {#manifesto-do-destinatario}

Obrigação fiscal: para cada NF-e em que sua empresa é o destinatário, a SEFAZ exige que você se manifeste com **um dos quatro eventos** dentro do prazo legal:

- **Ciência da Operação** — registra que tomou conhecimento da NF-e. Não compromete.
- **Confirmação da Operação** — confirma que recebeu a mercadoria/serviço descrito na NF-e.
- **Desconhecimento da Operação** — declara que não reconhece a NF-e (não comprou, não recebeu).
- **Operação Não Realizada** — declara que a operação não foi concluída (devolução, recusa).

A manifestação fecha a obrigação fiscal antes de qualquer lançamento no Sol.NET. Só depois disso o XML é processado pelo `Sol.NET MonitorNFCe` (ciclo automático, ~59 min) e fica disponível para lançamento na [Importar XML](Movimentacao/documentacao_importar_xml.md).

**Onde aparece:** [Manifestação do Destinatário](Fiscal/documentacao_manifestacao_destinatario.md) (`401`).

---

## 🏛️ Tributação

### CFOP

**Código Fiscal de Operações e Prestações** — código de 4 dígitos definido pelo CONFAZ que classifica a natureza da operação fiscal (venda dentro do estado, venda interestadual, devolução, transferência, importação etc.). O primeiro dígito indica a abrangência geográfica (`1.xxx` = dentro do estado, `2.xxx` = interestadual, `3.xxx` = exterior, `5/6/7.xxx` = saída correspondente). Toda nota fiscal exige CFOP por item.

**Onde aparece:** [Natureza de Operação](Fiscal/documentacao_natureza_operacao.md) (`36`) — é onde o CFOP é cadastrado e amarrado à operação.

### CST

**Código de Situação Tributária** — código que indica o tratamento tributário do produto na operação (tributado, isento, substituição tributária, suspenso, diferido etc.). Existe um CST para cada imposto (ICMS, PIS, COFINS, IPI). Empresas do regime normal usam CST de ICMS; empresas do Simples Nacional usam [CSOSN](#csosn).

**Onde aparece:** [NCM](Fiscal/documentacao_ncm.md) (`21`) · [Natureza de Operação](Fiscal/documentacao_natureza_operacao.md) (`36`).

### CSOSN

**Código de Situação da Operação no Simples Nacional** — equivalente do [CST](#cst) de ICMS para empresas optantes pelo Simples Nacional. Usado quando a empresa emissora é do Simples (informa crédito de ICMS, ou ausência dele, para o destinatário).

**Onde aparece:** [NCM](Fiscal/documentacao_ncm.md) (`21`).

### NCM

**Nomenclatura Comum do Mercosul** — código de 8 dígitos que classifica produtos para fins fiscais (federal e estadual). É a chave que governa qual alíquota de IPI, PIS, COFINS, ICMS, ICMS-ST e (no novo regime) [CBS](#cbs)/[IBS](#ibs) se aplica ao produto. No Sol.NET, o cadastro de NCM concentra as regras tributárias que serão aplicadas a todos os produtos vinculados àquele código.

**Onde aparece:** [Cadastro de NCM](Fiscal/documentacao_ncm.md) (`21`) · [Cadastro de Produtos](Produtos/documentacao_produtos.md) (`32`) (campo `NCM`).

### ICMS

**Imposto sobre Circulação de Mercadorias e Serviços** — imposto estadual incidente sobre a maior parte das operações de venda, transferência e prestação de serviço de transporte/comunicação. Alíquotas variam por estado e por tipo de operação (interna, interestadual). No Sol.NET, as regras de ICMS por contexto vivem na [Região ICMS Saída](Fiscal/documentacao_regiao_icms.md) e por NCM no [Cadastro de NCM](Fiscal/documentacao_ncm.md).

**Onde aparece:** [Região ICMS Saída](Fiscal/documentacao_regiao_icms.md) (`93`) · [NCM](Fiscal/documentacao_ncm.md) (`21`) · [Natureza de Operação](Fiscal/documentacao_natureza_operacao.md) (`36`).

### ICMS-ST

**Substituição Tributária do ICMS** — regime em que **um único elo da cadeia** (geralmente a indústria ou o importador) recolhe o ICMS de **todas as operações futuras** daquele produto, até o consumidor final. Para os demais elos (atacadistas, varejistas), o ICMS-ST entra como custo. Exige cálculo específico envolvendo Base de Cálculo, MVA (Margem de Valor Agregado) e alíquota interna do estado de destino.

**Onde aparece:** [Região ICMS ST Saída](Fiscal/documentacao_regiao_icms_st_saida.md) (`94`) · [NCM](Fiscal/documentacao_ncm.md) (`21`).

### CBS

**Contribuição sobre Bens e Serviços** — tributo federal criado pela [Reforma Tributária](#reforma-tributaria) que substitui PIS, COFINS e parte do IPI. Apuração não-cumulativa, alíquota uniforme nacional. Em transição gradual até 2033.

**Onde aparece:** [Reforma Tributária](Fiscal/documentacao_reforma_tributaria.md) · [NCM](Fiscal/documentacao_ncm.md) (`21`) (campos de tributação CBS).

### IBS

**Imposto sobre Bens e Serviços** — tributo de competência compartilhada entre Estados e Municípios, criado pela [Reforma Tributária](#reforma-tributaria) para substituir ICMS e ISS. Alíquota composta pela soma de uma parte estadual e uma municipal, definida no destino da operação.

**Onde aparece:** [Reforma Tributária](Fiscal/documentacao_reforma_tributaria.md) · [NCM](Fiscal/documentacao_ncm.md) (`21`) (campos de tributação IBS).

### Reforma Tributária {#reforma-tributaria}

Mudança no sistema tributário brasileiro (EC 132/2023) que substitui **PIS + COFINS + IPI** por **[CBS](#cbs)** e **ICMS + ISS** por **[IBS](#ibs)**, com transição gradual entre 2026 e 2033. Cria também o **Imposto Seletivo (IS)** para produtos específicos. A documentação dedicada cobre cronograma, parametrização e impacto nas telas do Sol.NET.

**Onde aparece:** [Reforma Tributária — documentação completa](Fiscal/documentacao_reforma_tributaria.md).

---

## 📦 Movimentação

### Movimento

**Documento operacional** que registra toda transação relevante: compra recebida, venda emitida, transferência entre filiais, devolução, produção, ajuste de inventário. É a unidade central da operação no Sol.NET. Cada movimento amarra **um** [Tipo de Movimento](#tipo-de-movimento) e herda dele todas as regras (efeito no estoque, financeiro gerado, fiscal emitido).

O mesmo formulário operacional é exposto sob três códigos na pesquisa F1, conforme o `Comportamento` do Tipo: `201` (Entrada/Compras), `202` (Saída/Vendas), `203` (Outros).

**Onde aparece:** [Movimentos — referência completa](Movimentacao/Movimentos/documentacao_movimentos.md) · [Movimentos de Compras](Movimentacao/Movimentos/movimentos_de_compras.md) (`201`) · [Movimentos de Vendas](Movimentacao/Movimentos/movimentos_de_vendas.md) (`202`) · [Outros Movimentos](Movimentacao/Movimentos/outros_movimentos.md) (`203`).

### Tipo de Movimento

**Cadastro de configuração** que define o comportamento do [Movimento](#movimento): qual [Transação de Estoque](#transacao-de-estoque) aplicar, qual fiscal emitir, se gera financeiro (e qual), qual Tabela de Preço usar por padrão, quais campos do cabeçalho são obrigatórios, quais sub-abas ficam visíveis, quais validações disparar. É a tela mais importante para entender qualquer movimento — o movimento em si só registra valores; o Tipo decide o que esses valores significam para o sistema.

**Onde aparece:** [Tipos de Movimento](Movimentacao/TiposDeMovimento/documentacao_tipos_de_movimento.md) (`37`).

### Transação de Estoque {#transacao-de-estoque}

**Cadastro** que define o efeito de um movimento em cada **camada de saldo** (Físico, Disponível, Reservado, Negociado etc.). Uma Transação pode somar no Físico e Disponível (entrada de compra), subtrair de ambos (venda balcão), subtrair só do Disponível e somar no Reservado (reserva), e assim por diante. Cada [Tipo de Movimento](#tipo-de-movimento) aponta para uma Transação — é o que decide se um movimento entra, sai, transfere ou apenas reserva mercadoria.

**Onde aparece:** [Transações de Estoque](Movimentacao/documentacao_transacoes_de_estoque.md) (`33`).

### Conferência {#conferencia}

Etapa intermediária — entre o recebimento da NF-e e o lançamento do movimento — em que um conferente confirma fisicamente, item a item, se a mercadoria recebida confere com a NF-e em quantidade e identificação. Acontece dentro da [Importar XML](Movimentacao/documentacao_importar_xml.md) (`204`), na sub-aba `Conferência`, e é habilitada por loja no `Cadastro de Empresas`. A conferência é registrada pelo app **Sol.NET Administrativo** (a aba `Conferência` da tela `204` apenas **exibe** o resultado).

**Onde aparece:** [Conferência de XML](Movimentacao/documentacao_conferencia_xml.md) · sub-aba `Conferência` em [Importar XML](Movimentacao/documentacao_importar_xml.md) (`204`).

### Cashback

Crédito que o cliente recebe sobre o valor da compra, para usar em compras futuras. No Sol.NET, é configurado por [Tipo de Movimento](#tipo-de-movimento) e por regras (percentual, validade, valor mínimo) na tela `Regras Cashback`. Predominantemente usado pelo PDV (frente de caixa); na retaguarda, o cashback aparece nas sub-abas `Crédito Pessoa — Gerado` e `Crédito Pessoa — Usado` do movimento.

**Onde aparece:** [Regras Cashback](Movimentacao/documentacao_regras_cashback.md) (`124`).

---

## 🗃️ Estoque e produtos

### Local de Estoque

**Armazém, loja ou depósito físico** onde o saldo da mercadoria vive. Cada movimento que afeta estoque exige um Local de origem (saída) e/ou destino (entrada). O [Saldo](#saldo) é sempre **por produto × Local**: o mesmo produto pode ter 50 unidades em uma loja e 0 em outra.

**Onde aparece:** [Locais de Estoque](Movimentacao/documentacao_locais_de_estoque.md) (`28`).

### Saldo

Quantidade do produto disponível em cada **camada** dentro de cada [Local de Estoque](#local-de-estoque). As camadas mais comuns são **Físico** (o que está no armazém), **Disponível** (o que pode ser vendido — Físico − reservas) e **Negociado** (vendido mas ainda não entregue). Cada [Transação de Estoque](#transacao-de-estoque) define em quais camadas o movimento soma ou subtrai.

**Onde aparece:** [Saldo Estoque](Movimentacao/documentacao_saldo_estoque.md) (`78`) · [Histórico de Produtos](Movimentacao/documentacao_historico_de_produtos.md) (`206`).

### Saldo PEPS

**Primeiro que Entra, Primeiro que Sai** — método de avaliação de estoque em que a saída consome primeiro a camada mais antiga. Influencia o **custo médio** registrado, porque cada entrada com custo diferente vira uma camada FIFO, e a saída custeia a camada mais antiga. Usado pelo Sol.NET quando o produto é configurado para controle PEPS.

**Onde aparece:** [Saldo Estoque](Movimentacao/documentacao_saldo_estoque.md) (`78`).

### Tabela de Preço {#tabela-de-preco}

**Cadastro** que define o preço de venda de cada produto **por contexto** (loja, condição de pagamento, faixa de cliente, período promocional). Cada [Tipo de Movimento](#tipo-de-movimento) aponta para uma Tabela padrão; o movimento pode usar a Tabela do Tipo ou outra escolhida no cabeçalho.

**Onde aparece:** [Tabela de Preço](Movimentacao/documentacao_tabela_de_preco.md) (`27`).

---

## ⚙️ Verbos da operação

### Faturar

Termo genérico para **emitir nota fiscal de venda** — converter um orçamento/pedido em uma NF-e/NFC-e autorizada pela SEFAZ. No Sol.NET, faturar normalmente passa por [Mudar](#mudar) o movimento para um Tipo que emite documento fiscal (ou por finalizar uma venda direta no `202`), seguido da emissão fiscal.

**Onde aparece:** [Movimentos de Vendas](Movimentacao/Movimentos/movimentos_de_vendas.md) (`202`) · [Movimentos — referência](Movimentacao/Movimentos/documentacao_movimentos.md).

### Finalizar

Operação que **consolida** um movimento: gera o financeiro definitivo, baixa o estoque conforme a Transação amarrada e (se aplicável) emite o documento fiscal. Antes de finalizar, o sistema dispara dezenas de validações cruzadas (caixa aberto, série fiscal disponível, campos obrigatórios, totalizações consistentes).

**Onde aparece:** [Movimentos — referência](Movimentacao/Movimentos/documentacao_movimentos.md) — operação central de qualquer movimento.

### Mudar

Operação que **converte um movimento de um Tipo para outro** conforme regras configuradas em `Tipos de Movimento → aba Mudar`. Típico no ciclo `ORÇAMENTO → PEDIDO → VENDA`. O Tipo de destino decide o comportamento da mudança em **um de dois modos**:

- **Transformar** — o mesmo movimento muda de Tipo. O identificador interno é preservado.
- **Duplicar** — um novo movimento é criado; o original muda de status para `VINCULADO` e fica congelado, formando uma pilha auditável.

A escolha entre Transformar e Duplicar é decidida pelo cadastro do Tipo de destino, não pelo operador.

**Onde aparece:** [Movimentos — referência](Movimentacao/Movimentos/documentacao_movimentos.md) (seção `Mudar`).

### Quitar

Operação que **liquida os títulos do contas a Pagar/Receber** ligados a um movimento. Pode ser por total, por título individual ou por agrupamento. As variantes incluem `Quitar Múltiplo`, `Quitar Contas PR` e `Quitar/Imprimir Só Portador`.

**Onde aparece:** [Movimentos — referência](Movimentacao/Movimentos/documentacao_movimentos.md) · [Quitação](Financeiro/documentacao_quitacao.md) (`303`) · [Pagar e Receber](Financeiro/documentacao_pagar_e_receber.md) (`301`).

### Estornar

Operação que **reverte completamente o efeito de um movimento** — devolve saldo ao estoque, cancela financeiro e cancela documento fiscal (quando permitido pela SEFAZ). O movimento estornado aparece nos relatórios de movimentação como estornado/cancelado.

**Onde aparece:** [Movimentos — referência](Movimentacao/Movimentos/documentacao_movimentos.md) (seção `Estornar`).

---

## 💰 Financeiro

### Centro de Custo

Unidade de **rateio gerencial** das despesas e receitas — departamento, projeto, frota, loja. Cada lançamento financeiro pode ser rateado entre um ou mais centros de custo para fins de análise de resultado por área.

**Onde aparece:** [Centros de Custos](Financeiro/documentacao_centros_de_custos.md).

### Plano de Contas

Estrutura hierárquica que classifica as **contas contábeis e gerenciais** da empresa (receitas, despesas, ativos, passivos). Toda movimentação financeira lançada no Sol.NET aponta para uma conta do Plano — é o que permite gerar DRE, balanço e relatórios gerenciais por conta.

**Onde aparece:** [Plano de Contas](Financeiro/documentacao_plano_de_contas.md).

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Todos os usuários do Sol.NET
