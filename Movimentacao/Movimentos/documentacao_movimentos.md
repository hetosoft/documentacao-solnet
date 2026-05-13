# 📄 Movimentos - Sol.NET

## 🎯 Visão Geral

**Movimento** é o documento operacional que registra toda transação relevante no Sol.NET — uma compra recebida, uma venda emitida, uma transferência entre filiais, uma devolução, uma produção, um ajuste de inventário. Cada movimento amarra **um** [Tipo de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) (cadastro `37`) e, por meio dele, herda todas as regras que determinam o efeito do lançamento: como o estoque é afetado (via [Transações de Estoque](../documentacao_transacoes_de_estoque.md) — cadastro `33`), qual financeiro gerar, qual fiscal emitir, em qual Local operar, qual Tabela de Preço aplicar, quais Funcionários exigir.

O Sol.NET expõe o mesmo formulário operacional sob **três códigos** distintos na pesquisa universal — um para cada grande categoria de movimento. Esta página descreve o **comportamento comum** das três telas. As particularidades de cada modo estão nos perfis específicos:

- [Movimentos de Compras](movimentos_de_compras.md) — código `201`.
- [Movimentos de Vendas](movimentos_de_vendas.md) — código `202`.
- [Outros Movimentos](outros_movimentos.md) — código `203`.

> 💡 **Por que 3 telas para o "mesmo" formulário?** Cada código filtra, no momento da abertura, quais **Tipos de Movimento** estão disponíveis para seleção: `201` lista apenas Tipos com Comportamento `Entrada`; `202`, Tipos de `Saída`; `203`, Tipos `Outros` (transferências, perdas, ajustes, produção, devoluções neutras). O comportamento real do movimento — quais sub-abas aparecem, quais campos exigir, quais validações disparar — é decidido pelo Tipo selecionado, não pelo código de entrada.

---

## 🔑 Como acessar

| Tela | Código (`F1`) | O que abre |
|------|---------------|------------|
| Movimentos de Compras | `201` | Formulário filtrado para Tipos de **Entrada**. |
| Movimentos de Vendas | `202` | Formulário filtrado para Tipos de **Saída**. |
| Outros Movimentos | `203` | Formulário filtrado para Tipos de Comportamento `Outros`. |

Abra a pesquisa universal (atalho `F1`) e digite o código ou parte do nome da tela.

---

## 🧭 Mapa do formulário

O formulário se divide em **duas grandes áreas**: a área de **Consulta** (lista de movimentos já lançados, com filtros) e a área de **Lançamento** (cabeçalho, itens, financeiro, totalizações, fiscal). Cada área agrupa várias sub-abas independentes — todas opcionais no sentido de que aparecem conforme o `Tipo de Movimento` configurar a tela.

### 🔍 Consulta — sub-abas

| Sub-aba | Para quê serve |
|---------|----------------|
| **Movimentos** | Lista principal de movimentos lançados. Filtros por Tipo, período, Pessoa, status, Empresa, Local. Sub-painéis: **Produtos** (itens do movimento selecionado), **Pagamentos**, **Observações**, **Protocolo Fiscal**, **Entrega PDV** (dados de entrega quando o movimento veio do PDV). |
| **Contas PR** | Títulos do contas a Pagar/Receber gerados por este movimento. Sub-abas: **Registros**, **Renegociação**, **Detalhes**, **Cheque** (com Histórico do Cheque), **Cartão**, **Crédito Pessoa - Usado**, **Crédito Pessoa - Gerado**. |
| **OS / Req.** | Vínculos com Ordem de Serviço e OS-Requisição. |
| **Agrupar** | Movimentos que foram agrupados — ver quais movimentos-origem compõem o movimento atual e vice-versa. |
| **Vínculos** | Outras amarras explícitas com outros movimentos (referência fiscal, devolução, vínculo manual). |
| **Parcial** | Sub-abas **Movimento Parcial** e **Quitação Parcial** — partes do movimento liberadas/quitadas em etapas. |
| **Chamada** | Histórico de chamadas (atendimento) ligadas ao movimento. |
| **Crédito - Gerado** | Créditos de pessoa gerados pelo movimento (devoluções, p.ex.). |
| **Pesquisa PDV** | Filtros adicionais para **consultar** movimentos que se originaram no PDV (a aplicação de frente de caixa, documentada à parte). Esta tela apenas visualiza/edita o registro lançado por lá — não é onde se opera o PDV. |
| **Pesquisa Salva** | Filtros pré-configurados pelo usuário (salvar uma consulta para reusar). |
| **Comportamentos** | Configurações de visualização da própria tela (colunas, ordenação padrão). |

### 📝 Lançamento — sub-abas

| Sub-aba | O que recebe |
|---------|--------------|
| **Cabeçalho** | Identificação do movimento: Tipo, Série, Número do Documento, Empresa, Pessoa, Datas (Emissão, E/S, Opcionais), Condição de Pagamento, Portador, Funcionários, Natureza de Operação, Modelo, Local de Estoque (origem e destino), Tabela de Preço. |
| **Itens** | Produtos do movimento. Sub-abas: **Totais**, **Tributação**, **ICMS/ST/IPI Livre**, **Pontos**, **Estoque do Produto**, **IVA** (impostos consolidados). |
| **Campos Complementares** | Campos extras configurados em `Tipos de Movimento → Campos Livres`. |
| **Descontos/Outras Despesas** | Acréscimos, descontos, fretes, despesas que afetam o total do movimento. |
| **Precificação** | Aba auxiliar para revisão de preços antes de gravar. Sub-abas: **Custos**, **Preços**, **Buscador de Preço**. |
| **Chamada** | Dados da chamada/atendimento vinculada ao movimento (quando o Tipo trabalha com Chamada). |
| **Cadastro/Fechamento** | Dados de cadastro/fechamento associados (ex.: fechamento de comanda, abertura de OS). |
| **Financeiro** | Contas a Pagar/Receber geradas pelo movimento. Sub-abas: **Contas** (títulos lançados), **Parcelas** (geração manual ou via Condição de Pagamento), **Rateio**, **Imagens** (anexos), **Forma de Pagamento**. |
| **Entrega** | Dados de entrega — endereço, transportadora, prazos. |
| **Entrega PDV** | Dados de entrega para vendas que **se originaram no PDV** — quando a retaguarda precisa completar ou ajustar essas informações. |
| **MDF-e** | Quando o movimento envolve transporte próprio: sub-abas **Rodoviário**, **Locais**, **Percurso/Condutor**, **Reboque**. |
| **Itens Cancelados** | Itens removidos do movimento, mantidos para auditoria. |
| **Vencimento** | **Controle de lote e data de validade dos produtos** do movimento — não tem relação com vencimento de parcelas (parcelas ficam em `Financeiro`). |
| **Outras Operações** | Sub-abas auxiliares: **Informações** (Adicionais e Outras Info., como Município Origem/Destino para transporte). |

> 💡 **Quais sub-abas aparecem.** Cada Tipo de Movimento decide quais sub-abas ficam visíveis. Um Tipo `VENDA BALCÃO` mostra Cabeçalho + Itens + Descontos/Outras Despesas + Financeiro. Um Tipo `TRANSFERÊNCIA ENTRE LOJAS` mostra Cabeçalho + Itens (sem Financeiro, porque não gera contas). Um Tipo `DEVOLUÇÃO DE VENDA` mostra também a aba `Crédito - Gerado` (na área de Consulta). Tipos que controlam produtos com lote/validade ativam a aba **Vencimento**; Tipos com transporte próprio ativam **MDF-e**.

> ℹ️ **PDV é uma aplicação separada.** Tipos de Movimento com a flag `PDV` marcada (configurada em [Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md)) **não aparecem** no combo `Tipo` em `Movimentos de Vendas` (`202`) — eles são exclusivos da aplicação `PDV` (frente de caixa), que será documentada à parte. Esta tela apenas **consulta** e, em alguns casos, **edita** registros que vieram do PDV (sub-abas `Pesquisa PDV` e `Entrega PDV`).

---

## 🔧 Fluxos principais

### Lançar um movimento novo

1. Abra a tela (`201`, `202` ou `203` conforme a categoria).
2. Clique em **Novo** (ou pressione o botão equivalente).
3. Na sub-aba **Cabeçalho**:
   - Selecione o `Tipo de Movimento` — a partir deste momento o formulário se reconfigura (campos visíveis, obrigatoriedades, sub-abas).
   - Preencha `Pessoa` (cliente, fornecedor, funcionário — conforme o Tipo).
   - Ajuste `Série`, `Número do Documento`, `Datas`, `Local de Estoque`, `Tabela de Preço`, `Condição de Pagamento`, `Portador`, `Funcionários` (conforme exigências).
4. Vá para a sub-aba **Itens** e adicione cada produto: código/nome, Quantidade, Preço (do produto ou da tabela), Desconto/Acréscimo.
5. Em **Descontos/Outras Despesas**, se necessário, ajuste totais (frete, despesas, descontos no total).
6. Em **Financeiro → Parcelas**, confira/edite as parcelas geradas a partir da Condição de Pagamento (válido para Tipos que geram financeiro).
7. Pressione **Gravar** (ou `F6` para gravar e **finalizar** em um passo — ver atalhos abaixo).

### Editar um movimento já lançado

1. Localize o movimento na lista da sub-aba **Movimentos** (filtros por período, Pessoa, Tipo, status).
2. Duplo-clique no registro (ou use o botão **Alterar** / `F7`).
3. O formulário entra em modo de edição. Campos congelados pela situação do movimento (já finalizado, transmitido, quitado, com NF-e autorizada) ficam bloqueados — o que pode ser alterado depende da configuração do `Tipo de Movimento` e do estado atual.
4. Faça os ajustes e **Grave** novamente.

> ℹ️ **Correção Manual.** Quando o movimento já está em estado que normalmente bloqueia edição, alguns campos podem ainda ser ajustados pelo recurso *Correção Manual* — ele só pode ser acionado em **modo de pesquisa** (selecionando o registro na lista). Tentar acionar em modo de edição direta é bloqueado: *"Correção Manual permitido apenas em modo de Pesquisa"*.

### Finalizar (botão **Finalizar** / `F6`)

A finalização é o passo que **consolida** o movimento — gera o financeiro definitivo, baixa estoque conforme a Transação amarrada, emite o documento fiscal (se aplicável). Antes da finalização, validações cruzadas são executadas (caixa aberto, série fiscal disponível, campos obrigatórios, totalizações consistentes).

### Mudar (botão **Mudar** / `F7`)

Converte um movimento de um Tipo para outro **conforme regras configuradas** em `Cadastro de Tipos de Movimento → aba Mudar` — típico no ciclo `ORÇAMENTO → PEDIDO → VENDA`. A mudança copia os itens e o cabeçalho, ajustando o Tipo e re-aplicando regras fiscais/financeiras.

### Quitar (botão **Quitar** / `F8`)

Liquida os títulos do contas PR ligados ao movimento. Pode ser pelo total, por título individual ou por agrupamento. Variantes implementadas: `Quitar Multiplo`, `Quitar Contas PR`, `Quitar/Imprimir Só Portador`.

### Imprimir (botão **Imprimir** / `F9`)

Aciona o modelo de impressão vinculado ao Tipo (`Cadastro de Tipos de Movimento → aba Relatórios`). Pode imprimir DANFE, comprovante, espelho, ordem de serviço — conforme o que estiver configurado.

### Emitir NF-e / NFC-e / NFS-e (botão **NF-e** / `F10`)

Aciona a transmissão fiscal do documento eletrônico. O sistema gera o XML, assina, envia à SEFAZ/Prefeitura, recebe protocolo e atualiza o movimento com a Chave de Acesso. Status fiscais (`Autorizada`, `Rejeitada`, `Cancelada`, `Denegada`) ficam visíveis na sub-aba `Movimentos → Protocolo Fiscal`.

### Estornar (botão **Estornar** / `F11`)

Reverte completamente o efeito do movimento — devolve saldo ao estoque, cancela financeiro, cancela documento fiscal (quando permitido pela SEFAZ). A reversão é registrada e gera trilha de auditoria visível em `Histórico de Movimentações` (código `205`).

---

## ⌨️ Atalhos validados

| Tecla | Ação |
|-------|------|
| `F1` | Abre a pesquisa universal de telas. |
| `F6` | **Finalizar** o movimento atual. |
| `F7` | **Mudar** o Tipo de Movimento (conversão automática). |
| `F8` | **Quitar** os títulos vinculados. |
| `F9` | **Imprimir** o movimento. |
| `F10` | Emitir **NF-e / NFC-e / NFS-e**. |
| `F11` | **Estornar** o movimento. |
| `Esc` | Volta à sub-aba anterior dentro do Lançamento, ou fecha a pesquisa quando aberta como popup. |
| `+` (numérico) | Quando configuração `UsarComanda` está ativa, abre a tela de **Comanda** a partir da consulta. |

> ⚠️ Os atalhos `F6`–`F11` só funcionam **fora** do modo de pesquisa. Dentro da lista de busca, eles ficam inativos.

---

## ✅ Validações automáticas ao salvar e operar

O formulário executa **centenas** de verificações distintas ao salvar, finalizar, mudar, quitar e estornar. As mensagens são exibidas em popup e o foco vai para o componente que causou. As mais frequentes estão organizadas por categoria no [FAQ](faq.md). Categorias cobertas:

- **Cabeçalho** — Tipo de Movimento obrigatório, Pessoa obrigatória, Empresa permitida para o Tipo, Local de Estoque, Tabela de Preço, Funcionários (obrigatórios conforme configuração do Tipo).
- **Itens** — pelo menos um item (*"Movimento sem item!"*), produtos com Tipo Movimento compatível (*"Empresa Não Permitida Para esse Tipo Movimento!"*), preço/custo dentro de faixas, quantidades positivas (ou negativas conforme o Tipo).
- **Fiscal** — CFOP coerente com Comportamento (*"CFOP não é de entrada!"* / *"CFOP não é de saída!"*); estado/internacional (*"CFOP não é dentro do estado!"*, *"CFOP não é Exterior(Internacional)!"*); Chave de Acesso válida; Modelo × Série compatíveis.
- **Caixa** — ao finalizar, verifica se o **Caixa** está aberto para o usuário/empresa (*"Caixa Aberto. Fechamento Nº: ( ... )"*).
- **Financeiro** — parcelas com valor positivo, total das parcelas = total do movimento, Portador válido para a Condição de Pagamento.
- **Pagamento SPED** — Tipos de pagamento SPED válidos para o documento eletrônico.
- **Devolução** — quando o movimento é devolução, exige Movimento Referenciado (*"Não Permitido, Obrigatório Referenciar Nota! (Devolução)"*); a referência precisa ser da **mesma empresa** (*"Não Permitido, Obrigatório Referenciar Nota da Mesma Empresa! (Devolução)"*).
- **Concorrência** — se outro usuário alterou Custo/Preço da Nota enquanto você editava: *"Alteraram o 'Custo' Antes de Voçê, Consulte a Nota de Novo!"* / *"Alteraram o 'Preço' Antes de Voçê, Consulte a Nota de Novo!"*.

> 💡 Veja o [FAQ](faq.md) para a lista detalhada com **onde resolver cada mensagem**.

---

## 💡 Exemplos práticos

### Exemplo 1 — Lançar uma venda balcão (`202`)

1. Pesquisa `F1` → `202` → **Novo**.
2. **Cabeçalho**: `Tipo` = `VENDA BALCÃO`, `Pessoa` = cliente, `Local de Estoque` = `01 - Matriz`, `Condição de Pagamento` = `À VISTA`, `Portador` = `Caixa`.
3. **Itens**: adicione cada produto. O preço vem da Tabela amarrada ao Tipo; ajuste desconto/quantidade conforme combinado.
4. **Descontos/Outras Despesas**: se for o caso, lance frete ou desconto no total.
5. **Financeiro → Parcelas**: parcela única confirmada automaticamente.
6. Pressione `F6` (Finalizar) → o sistema gera financeiro, baixa estoque e imprime cupom (se o Tipo tiver Relatório configurado).

### Exemplo 2 — Lançar entrada de NF de compra (`201`)

1. Pesquisa `F1` → `201` → **Novo**.
2. **Cabeçalho**: `Tipo` = `COMPRA À VISTA` (ou `A PRAZO`), `Pessoa` = fornecedor, `Série` e `Número do Documento` = os da NF recebida, `Data de Emissão` = data da NF, `Data E/S` = data do recebimento físico.
3. **Itens**: lance cada produto com `Custo` da nota. Se o Tipo tem `Atualizar Custo Automático` marcado em `Tipos de Movimento → Itens → Quantidade`, esse custo será propagado para o cadastro do produto ao gravar.
4. **Financeiro → Parcelas**: confira parcelas conforme acordado com o fornecedor.
5. `F6` (Finalizar) → estoque entra, financeiro a pagar é gerado, conta a pagar fica no `Contas PR`.

### Exemplo 3 — Transferência entre lojas (`203`)

1. Pesquisa `F1` → `203` → **Novo**.
2. **Cabeçalho**: `Tipo` = `TRANSFERÊNCIA ENTRE EMPRESAS` (configurado em `37` com Comportamento `Outros`, destino Empresa), `Local Origem` = local da loja A, `Local Destino` / `Empresa Destino` = local da loja B.
3. **Itens**: produtos a transferir, com quantidades.
4. `F6` (Finalizar) → o Sol.NET baixa do Local Origem e entra no Local Destino. Não há financeiro porque o Tipo está configurado sem `Gerar Lançamento`.

### Exemplo 4 — Devolução de venda gerando crédito ao cliente

1. Pesquisa `F1` → `201` (ou `203`, conforme o Tipo `DEVOLUÇÃO DE VENDA` esteja cadastrado) → **Novo**.
2. **Cabeçalho**: `Tipo` = `DEVOLUÇÃO DE VENDA`. **Referenciar Nota**: aponte para a venda original (o Tipo exige; sem isso a validação bloqueia).
3. **Itens**: lance os produtos devolvidos.
4. `F6` → estoque volta, fiscal de entrada é emitido, e (se o Tipo tem `Devolução Crédito` marcado em `37`) um **Crédito de Pessoa** é gerado para o cliente. O crédito aparece na sub-aba **Crédito - Gerado** desse movimento e na ficha da pessoa.

### Exemplo 5 — Emitir NF-e de uma venda já finalizada

1. Localize a venda em `202`, na sub-aba **Movimentos**.
2. Selecione o registro e pressione `F10` (NF-e) — ou clique em `Emitir NF-e`.
3. O sistema gera o XML, assina, envia à SEFAZ. O protocolo retorna na sub-aba `Movimentos → Protocolo Fiscal`.
4. Se o status for `Rejeitada`, leia a mensagem da SEFAZ no Protocolo Fiscal e corrija conforme o erro (CFOP, NCM, alíquotas, IE do destinatário etc.) — depois `F10` de novo.

---

## ❓ FAQ rápido

**Movimento foi gravado mas o saldo do produto não baixou.**
A `Transação de Estoque` amarrada ao Tipo não está configurada para subtrair as camadas certas. Confira em `Transações de Estoque` (`33`) → confirme as colunas `Físico` e `Disponível`. Confira também o `Local de Estoque` informado no Cabeçalho — o saldo é por Local.

**O combo `Tipo de Movimento` não mostra o Tipo que preciso.**
O Tipo está inativo, ou está com Comportamento incompatível com a tela aberta (Entrada → `201`, Saída → `202`, Outros → `203`), ou o usuário não tem permissão no grupo de acesso desse Tipo.

**Onde vejo o histórico completo das alterações deste movimento?**
Em [Histórico de Movimentações](../documentacao_historico_de_movimentacoes.md) (código `205`) — todas as operações (gravação, edição, finalização, mudança, quitação, estorno, transmissão fiscal) ficam registradas com data, hora e usuário.

**Lancei na tela errada (compra na `202` em vez de `201`).**
Não há como lançar na tela errada, na verdade — o filtro de Tipos por Comportamento impede. Se a sensação é que o Tipo deveria estar disponível em outra tela, é a **configuração do Tipo** em `37` que está com Comportamento divergente. Ajuste lá.

Mais perguntas e a referência completa de mensagens de erro em [FAQ](faq.md).

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Como se relaciona |
|------|---------------|--------------------|
| [Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) | `37` | Cada movimento herda **todas** suas regras do Tipo selecionado. Tela mais importante a entender em conjunto. |
| [Transações de Estoque](../documentacao_transacoes_de_estoque.md) | `33` | O Tipo aponta para a Transação que decide o efeito de cada camada de saldo (Físico, Disponível, Reservado etc.). |
| [Locais de Estoque](../documentacao_locais_de_estoque.md) | `28` | Identifica em qual armazém/loja o saldo afetado vive. Cabeçalho exige Local quando o Tipo movimenta estoque. |
| [Tabela de Preço](../documentacao_tabela_de_preco.md) | `27` | Origem do `Preço` aplicado a cada item no Cabeçalho/Itens. |
| [Saldo Estoque](../documentacao_saldo_estoque.md) | `78` | Visão consolidada do efeito dos movimentos nos saldos por Local/Situação. |
| [Histórico de Movimentações](../documentacao_historico_de_movimentacoes.md) | `205` | Trilha de auditoria do que aconteceu com cada movimento. |
| [Histórico de Produtos](../documentacao_historico_de_produtos.md) | `206` | Filtra por produto — vê quais movimentos afetaram cada item. |
| [Ajuste de Estoque](../documentacao_ajuste_de_estoque.md) | `79` | Tela auxiliar que **dispara** movimentos visíveis em `203`. |
| `Pedido de Compra` | `64` | Tela que **dispara** movimentos em `201` ao ser convertido em entrada. |
| [Produção de Produtos](../Producao/documentacao_producao_de_produtos.md) | `144` | **Dispara** movimentos visíveis em `203` (saída dos ingredientes, entrada do acabado, perda). |
| [Regras Cashback](../documentacao_regras_cashback.md) | `124` | Cashback é configurado por Tipo de Movimento e usado predominantemente pelo PDV (aplicação à parte). Movimentos vindos do PDV chegam aqui com o cashback já aplicado/gerado, visível nas sub-abas `Crédito Pessoa - Usado` / `Crédito Pessoa - Gerado`. |

---

## ⚠️ Limites desta documentação

- O formulário tem mais de **80 mil linhas de código** e **354 colunas** na tabela principal (`MOVIMENTOS`), além de 16 tabelas filhas (itens, parcelas, impostos, observações, comandas, referenciados etc.). Esta página é um **mapa de navegação** — não cobre cada campo individualmente.
- A documentação cobre o **comportamento comum** das três telas (`201/202/203`). Para particularidades de cada modo, veja os perfis individuais.
- Telas de **Conferência** (`209/210/211/220`) compartilham boa parte do código deste formulário mas operam em modo de leitura/conferência — serão documentadas em separado.
- Detalhes profundos de **fiscal** (DANFE, regras de cada tipo de NF-e/NFC-e/NFS-e, contingência, manifesto, MDF-e) ficam na documentação do **módulo Fiscal**.
- Regras de **comissão**, **promoção**, **cashback** e **agrupamento** são acionadas a partir das configurações do Tipo e tratadas em telas/documentações dedicadas.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Usuários operacionais (caixa, frente de loja, retaguarda) / Suporte
