# 📄 Cadastro de Tipos de Movimento - Sol.NET

## 🎯 Visão Geral

O **Tipo de Movimento** é a **identidade operacional** de cada lançamento no Sol.NET. Ele responde, num único cadastro, a perguntas que todo movimento precisa carregar: *é venda ou compra?*, *sai ou entra no estoque?*, *é nota fiscal própria ou de terceiro?*, *qual CFOP, qual modelo de documento, qual série?*, *gera financeiro?*, *atualiza custo?*, *é PDV, mobile, ordem de serviço?*. Tudo o que diferencia uma venda de balcão de uma venda no PDV, ou uma compra à vista de uma compra parcelada, está aqui.

Cada movimento lançado em `Cadastro de Movimentos` (código `53`), `Pedido de Compra` (código `64`), `Produção de Produtos` (código `144`), `Ajuste de Estoque` (código `79`) ou nas variantes (`201`, `202`, `203`, `209`, `210`, `211`, `220`) aponta para **um** Tipo de Movimento — e é dele que o Sol.NET extrai todas as regras: quais Tabelas de Preço aceitar, qual `Transação de Estoque` aplicar, qual `Tipo de Documento Padrão` usar no financeiro, qual layout fiscal emitir, quais campos exigir, em qual `Local de Estoque` operar, com qual `Portador` quitar.

Por concentrar todas essas regras, é a **tela de configuração mais densa do módulo Movimentação** — com 12 abas no formulário, dezenas de sub-abas e mais de 50 validações ao salvar. Esta documentação **mapeia a tela** e os principais comportamentos; não substitui o conhecimento operacional do consultor de implantação, que tipicamente desenha os Tipos de Movimento com a empresa na fase de configuração.

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Tipos de Movimento` requerem permissão de acesso de suporte. Toda criação, edição ou inativação descrita nos exemplos e fluxos abaixo deve ser feita pela equipe de suporte Hetosoft, **não** pelo usuário final. Mudanças aqui se propagam para todos os movimentos lançados a partir do momento da alteração — não há "preview" e mudanças em produção exigem cautela e acordo prévio com o cliente.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Tipos de Movimento |
| **Código (`F1`)** | `37` |

Abra a pesquisa universal (atalho `F1`) e digite **`37`** ou parte do nome **`Tipos de Movimento`**.

---

## 🧭 Estrutura do formulário

O formulário de cadastro tem **doze abas no nível raiz**, cada uma agrupando configurações de uma dimensão diferente do Tipo de Movimento. Algumas dessas abas, por sua vez, contêm sub-abas próprias.

| Aba | Para quê serve |
|------|----------------|
| **Dados Cadastrais** | Identificação básica do tipo: descrição, código, conta contábil, comportamento (entrada × saída × ambos), tipo do movimento (Compra, Venda, Outros), tipo da operação. |
| **Cabeçalho** | Configurações do cabeçalho do movimento — Características, Origem/Destino, Datas, Funcionários, Fiscal (CFOP, Documento Fiscal, Série, Extra), Serviço, Campos Livres, Mobile. |
| **Valores** | Regras de cálculo de valor — Valores, Valores de Serviços, e a sub-aba final de fechamento. |
| **Itens** | Regras dos itens — Principal, Extras, Tabela de Preço, Tabela de Preço por Empresa, Estoque (Itens Estoque + Local Estoque por Empresa), Quantidade, Comissão, Pessoa. |
| **Financeiro** | Geração de financeiro a partir do movimento — Financeiro 1, Financeiro 2 e Portador. |
| **Finalizar** | Configurações de finalização do movimento, incluindo o sub-fluxo de mudança automática para outro tipo (Finalizar → Mudar). |
| **Mudar** | Regra de mudança de tipo (quando este tipo deve se transformar em outro durante uma etapa do fluxo). |
| **Agrupar** | Configurações de agrupamento de movimentos. |
| **Relatórios** | Vinculação a relatórios e modelos (Relatórios, DANFE, Promoção). |
| **Campos Complementares** | Campos extras específicos a este tipo — Movimento, Produtos, Serviços. |
| **Outras Operações** | Configurações operacionais variadas: bloqueios, PDV, devoluções, crédito, OS, MDF-e, e empresa-destino. Subdividida em várias sub-abas (Empresa, Sistema). |
| **Agrotóxico** | Configurações específicas de operações com produtos agrotóxicos (módulo Agronômico). |

> 💡 **Como ler a tela.** Quem está vendo um Tipo de Movimento pela primeira vez ganha tempo se for nessa ordem: **Dados Cadastrais** (saber o que é o tipo), **Cabeçalho → Características** (saber se é compra/venda, próprio/terceiro, fiscal), **Itens → Estoque** (Local + Transação), **Financeiro** (gera conta?), **Outras Operações** (PDV, mobile, devolução). Os outros painéis são afinações.

---

## 📝 Aba `Dados Cadastrais` — campos principais

Painel sempre visível na primeira aba do `Cadastrar`. Concentra a identificação e o comportamento base do Tipo.

| Campo | Para quê serve |
|-------|----------------|
| **Descrição** | Nome do Tipo de Movimento (`VENDA BALCÃO`, `COMPRA À VISTA`, `DEVOLUÇÃO VENDA`). |
| **Conta Analítica** / **Complemento** | Conta de classificação do tipo na árvore interna de tipos. O preenchimento de Complemento define se a conta é **Sintética** (sem complemento) ou **Analítica** (com complemento — gera movimento). Tentar mudar conta Analítica para Sintética e vice-versa sem ajustar o complemento é bloqueado. |
| **Tipo Movimento** | Classifica o tipo na hierarquia (Vendas / Compras / Outros). |
| **Tipo de Conta** | Sintética × Analítica — só Analítica pode lançar movimento. |
| **Comportamento** | Define o sentido fiscal/estoque: `Entrada (Compras)`, `Saída (Vendas)`, `Outros`. Quando há Natureza de Operação amarrada, o sistema valida o CFOP contra o comportamento (CFOP de entrada `1/2/3` em tipo de Entrada; CFOP de saída `5/6/7` em tipo de Saída). |

---

## 🧾 Aba `Cabeçalho` — sub-abas

A aba **Cabeçalho** agrupa o que o movimento traz **no nível de cabeçalho**, em sub-abas independentes:

| Sub-aba | O que configura |
|---------|-----------------|
| **Características** | Comportamento geral do cabeçalho — Tipo Emissão (Própria × Terceiro), classificação do documento, opções padrão. Validação chave: Emissão `Terceiro` exige um `Tipo de Sequência` específico no combo `cbxDCCarTpSequencia` — sem isso, *"Tipo Emissão Terceiro não permitido"*. |
| **Origem/Destino** | Quem é a origem do movimento (Empresa × Pessoa) e quem é o destino. A combinação **Destino = Empresa** com `cbxEmpresaEmpresa` preenchida é validada — *"Destino do Movimento do Tipo Pessoa!"* ou *"Não Preenchido… Destino Igual Origem"* são bloqueios típicos. |
| **Datas** | Datas obrigatórias ou opcionais que o movimento exige (Emissão, Saída, Faturamento, Vencimento etc.). |
| **Funcionários** | Quais funcionários (vendedor, comissionado, conferente) o movimento exige. Validação cruzada: `Memorizar Vendedor` não pode coexistir com `Vínculo com Usuário` nem com `Funcionário Padrão`. |
| **Fiscal** | Sub-sub-abas: **Natureza de Operação** (CFOPs aceitos — validados contra o comportamento), **Documento Fiscal** (Modelo do documento — NF-e, NFC-e, NFS-e, Cupom), **Fiscal Extra** (regras adicionais), **Série** (séries fiscais habilitadas + qual é a padrão). Validações fortes: `Modelo` precisa ter ao menos uma série marcada, uma série padrão, e o tipo fiscal das séries deve coincidir com o tipo do modelo de documento. |
| **Serviço** | Sub-abas Geral + Empresa — para Tipos que envolvem prestação de serviço. Quando NFS-e: `Série RPS` e `Série Lote` são obrigatórias. |
| **Campos Livres** | Campos extras que o usuário pode preencher no movimento. |
| **Mobile** | Comportamento em dispositivos móveis (coletor, força de vendas). |

---

## 💰 Aba `Valores` — sub-abas

| Sub-aba | O que configura |
|---------|-----------------|
| **Valores** | Regras de cálculo dos valores principais do movimento — totais, descontos, frete, despesas. |
| **Valores Serviços** | Equivalente para a parte de serviços do movimento. |
| **(extra)** | Configurações de fechamento de valores. |

---

## 📦 Aba `Itens` — sub-abas

A aba **Itens** é a maior em volume de regras — controla o que o movimento aceita por linha de produto:

| Sub-aba | O que configura |
|---------|-----------------|
| **Principal** | Configurações gerais da linha de item (campos visíveis, obrigatórios, calculados). |
| **Extra Item / Extra Item 2** | Configurações extras para campos específicos de item. |
| **Tabela de Preço** | Quais Tabelas de Preço o tipo aceita. **Obrigatório selecionar** ao menos uma forma de buscar o preço e marcar **uma tabela como Padrão** — *"Selecione uma Tabela de Preço!"* / *"selecione uma Tabela de Preço Padrão!"*. |
| **Tabela de Preço por Empresa** | Tabela específica por empresa quando o tipo é multi-empresa. |
| **Estoque → Itens Estoque** | `Local de Estoque` padrão e `Transação de Estoque` (obrigatórios para tipos que movimentam estoque). *"Obrigatório Local de Estoque!"* / *"Obrigatório Transação de Estoque!"*. Algumas opções (`Estatística de Estoque`, `Baixar Quantidade na Promoção`) **exigem Transação de Estoque** preenchida. |
| **Estoque → Local Estoque por Empresa** | Override de Local por empresa. |
| **Quantidade** | Regras de quantidade — `Atualizar Custo Automático`, `Vender Sem Estoque`. `Atualizar Custo Automático` é **válido só para Compras/Outros** — Vendas não atualizam custo. |
| **Comissão** | Percentuais e regras de comissão do tipo. |
| **Pessoa** | Restrições por tipo de pessoa (Cliente, Fornecedor, Funcionário etc.). |

---

## 💸 Aba `Financeiro` — sub-abas

| Sub-aba | O que configura |
|---------|-----------------|
| **Financeiro 1** | Geração de conta a receber/pagar (`Gerar Lançamento`), Tipo de Documento Padrão, Plano de Contas, Centro de Custo, Condição de Pagamento padrão. **Validações**: se `Gerar Lançamento` está em `0` ou `1`, `Tipo Documento Padrão` é obrigatório; quando há geração de financeiro, `Plano de Contas` e `Centro de Custo` são obrigatórios. `Não Estornar Financeiro` só é permitido para Compras/Outros. |
| **Financeiro 2** | Configurações adicionais (taxa de juros, abatimento, antecipação). |
| **Portador** | Painel CRUD de Portadores aceitos pelo tipo + Portador padrão. |

---

## 🎬 Aba `Finalizar`, `Mudar`, `Agrupar`

| Aba | O que configura |
|-----|-----------------|
| **Finalizar** | O que acontece quando o movimento é finalizado — botões, validações finais, geração de documentos. Inclui sub-aba `Finalizar / Mudar` que liga este Tipo a outro (ex.: `PEDIDO → VENDA` ao finalizar). |
| **Mudar** | Configura uma **mudança automática** deste tipo para outro durante o ciclo (ex.: orçamento que vira pedido que vira venda). |
| **Agrupar** | Regras de agrupamento de movimentos (juntar vários pedidos em uma única nota, por exemplo). |

---

## 🖨️ Aba `Relatórios` — sub-abas

| Sub-aba | O que configura |
|---------|-----------------|
| **Relatórios** | Modelos de relatório vinculados (impressão do movimento, comprovantes). |
| **DANFE** | Layout e regras da DANFE para tipos fiscais. |
| **Promoção** | Vinculação a modelos de etiqueta promocional. |

---

## 🔧 Aba `Outras Operações` — sub-abas

Aba "guarda-tudo" de comportamentos especiais — alvo de muitas validações cruzadas.

| Sub-aba | O que configura |
|---------|-----------------|
| **Empresa → Empresa 1 / Empresa 2 / extras** | Comportamentos por empresa-destino do movimento. |
| **Sistema** | Flags de sistema — PDV, Mobile, OS × OS Requisição, Devolução, Crédito Pessoa, Quitar Crédito Automaticamente. **Validações principais** (todas bloqueiam ao gravar): |
| | `Devolução = Sim` e `Devolução = Sim` ao mesmo tempo no mesmo tipo é inválido. |
| | `Devolução Crédito` sem `Devolução = Sim` não é permitido. |
| | `Quitar Crédito Automaticamente` só é permitido para tipos PDV **e** que geram crédito. |
| | `Não Consultar` em Lançamento não é permitido para PDV. |
| | `OS` e `OS Requisição` não podem coexistir. |
| | `Crédito Pessoa` é incompatível com Destino = Empresa. |

---

## 🌿 Aba `Agrotóxico`

Configurações específicas para tipos que movimentam produtos agrotóxicos — vinculação com `Receituário Agronômico` (módulo Agronômico) e regras de rastreabilidade.

---

## ✅ Resumo das principais validações ao salvar

A função `Validar` faz **mais de 50 verificações**. Os bloqueios mais frequentes (todos com mensagem clara apontando a aba/sub-aba):

| Bloqueio | Onde resolver |
|----------|---------------|
| `Selecione uma Tabela de Preço!` | Aba `Itens → Tabela de Preço`. |
| `Selecione uma Tabela de Preço Padrão!` | Aba `Itens → Tabela de Preço`. |
| `Obrigatório Local de Estoque!` | Aba `Itens → Estoque → Itens Estoque`. |
| `Obrigatório Transação de Estoque!` | Aba `Itens → Estoque → Itens Estoque`. |
| `Plano de Contas e Centro de Custo Obrigatório para Tipo de Movimento com Financeiro!` | Aba `Financeiro → Financeiro 1`. |
| `Conta só pode ser Analítica/Sintética` | Aba `Dados Cadastrais` — ajustar Complemento. |
| `CFOP em Natureza de Op. Não é de entrada/Saída!` | Aba `Cabeçalho → Fiscal → Natureza Operação`. CFOPs `1/2/3` para Entrada, `5/6/7` para Saída. |
| `Selecione ao menos uma série!` / `Selecione ao menos uma série padrão!` | Aba `Cabeçalho → Fiscal → Série`. |
| `Tipos de Séries devem ser iguais ao Tipo do Modelo de Documento!` | Aba `Cabeçalho → Fiscal` — alinhar fiscal/não-fiscal entre série e modelo. |
| `Série RPS e Série Lote é Obrigatório para NFS-e!` | Aba `Cabeçalho → Serviço`. |
| `Atualizar Custo Automático, Somente para Compras/Outros!` | Aba `Itens → Quantidade` — incompatível com Vendas. |
| `Não Estornar Financeiro, Somente para Compras/Outros!` | Aba `Financeiro → Financeiro 1`. |
| `Não permitido, "Devolução"…` (várias variações) | Aba `Outras Operações → Sistema`. |
| `Não Consultar em Lançamento para Tipo de Mov. "PDV"!` | Aba `Outras Operações → Sistema`. |
| `OS e OS Requisição ao mesmo tempo` | Aba `Outras Operações → Sistema`. |
| `Não Permitido Credito pessoa para Tipo de Movimento com Destino à Empresas!` | Aba `Outras Operações → Sistema` × `Cabeçalho → Origem/Destino`. |
| `SEPARAR ITENS DO MOVIMENTO (Global) Ativada em Configuração Geral` | Configuração da empresa, fora desta tela — desligar lá para gravar com a opção aqui. |
| `Promoção com Atualização em Grupo Ativada em Configuração Geral` | Configuração da empresa, fora desta tela. |

> ℹ️ **Como navegar as validações.** Ao receber uma mensagem de bloqueio, o sistema **automaticamente** abre a aba/sub-aba onde o problema está e foca o componente que causou. Basta corrigir e tentar gravar de novo.

---

## 🚫 Exclusão e Clonagem

A exclusão de um Tipo de Movimento já em uso é bloqueada pelas integridades das tabelas filhas (Movimentos lançados com este Tipo, Tabelas de Preço vinculadas, etc.). Em produção, a recomendação é **inativar** o Tipo em vez de excluir — assim ele some das telas operacionais mas o histórico continua referenciando.

A clonagem está disponível pelo menu de contexto da grade de busca (`Clonar Registro` — pede confirmação). Útil para criar variações: clone um Tipo `VENDA BALCÃO` para gerar `VENDA BALCÃO PROMOCIONAL` com poucas mudanças.

---

## 💡 Exemplos práticos

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Tipos de Movimento` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nesta tela.

Os exemplos abaixo descrevem o que o suporte tipicamente faz dentro deste cadastro. Tipos de Movimento mal configurados podem gerar movimentos sem financeiro, sem fiscal, com saldo de estoque incorreto, ou recusados pela SEFAZ — alinhar com a equipe Hetosoft antes de executar.

### Exemplo 1 — Criar um Tipo `VENDA BALCÃO`

1. Pesquisa `F1` → `37` → **Novo**.
2. Aba **Dados Cadastrais**:
   - `Descrição`: `VENDA BALCÃO`.
   - `Conta` / `Complemento`: monte a conta Analítica adequada na árvore de tipos.
   - `Comportamento`: `Saída`.
   - `Tipo Movimento`: `Vendas`.
3. Aba **Cabeçalho → Características**: marque `Própria`, defina `Tipo de Sequência` adequado.
4. Aba **Cabeçalho → Fiscal**: escolha o `Modelo de Documento` (NF-e ou NFC-e), marque CFOPs `5xxx`/`6xxx`, defina a `Série` padrão.
5. Aba **Itens → Tabela de Preço**: marque ao menos uma tabela e defina uma como **Padrão**.
6. Aba **Itens → Estoque → Itens Estoque**: defina `Local de Estoque` padrão e `Transação de Estoque` configurada para subtrair Físico e Disponível.
7. Aba **Financeiro → Financeiro 1**: defina `Plano de Contas`, `Centro de Custo`, `Tipo de Documento Padrão`, `Condição de Pagamento` padrão.
8. Aba **Financeiro → Portador**: adicione ao menos um Portador e defina o Padrão.
9. **Gravar**.

### Exemplo 2 — Criar um Tipo `COMPRA À VISTA`

1. Pesquisa `F1` → `37` → **Novo**.
2. Aba **Dados Cadastrais**:
   - `Descrição`: `COMPRA À VISTA`.
   - `Comportamento`: `Entrada`.
   - `Tipo Movimento`: `Compras`.
3. Aba **Cabeçalho → Características**: marque `Terceiro` e configure o `Tipo de Sequência` exigido.
4. Aba **Cabeçalho → Fiscal**: CFOPs `1xxx`/`2xxx`.
5. Aba **Itens → Estoque**: Local + Transação que **soma** Físico e Disponível.
6. Aba **Itens → Quantidade**: marque `Atualizar Custo Automático` (permitido em Compras).
7. Aba **Financeiro → Financeiro 1**: defina Plano/Centro/Tipo Documento — se a compra é à vista, a Condição de Pagamento padrão pode ser `À VISTA`.
8. **Gravar**.

### Exemplo 3 — Criar `DEVOLUÇÃO DE VENDA` que gera crédito ao cliente

1. Pesquisa `F1` → `37` → clone o Tipo `VENDA BALCÃO` (clique-direito → `Clonar Registro`).
2. Ajuste `Descrição`: `DEVOLUÇÃO DE VENDA`.
3. Aba **Cabeçalho → Fiscal**: CFOPs de **entrada** (`1xxx`/`2xxx`) — vendas que voltam.
4. Aba **Itens → Estoque**: Transação de Estoque que **soma** novamente (o produto volta).
5. Aba **Outras Operações → Sistema**:
   - `Devolução` = `Sim`.
   - `Devolução Crédito` ≥ `0` (gera crédito).
   - Se for PDV, marque `Quitar Crédito Automaticamente` para abater o crédito direto na próxima compra.
6. Aba **Financeiro → Financeiro 1**: `Não Estornar Financeiro` se for compra (válido), ou deixe vazio para vendas (não permitido para Vendas; o erro avisa).
7. **Gravar**.

### Exemplo 4 — Inativar um Tipo legado sem perder histórico

1. Pesquisa `F1` → `37` → localize o Tipo na grade → abra.
2. Marque `Inativo` no cabeçalho do formulário.
3. **Gravar**.

A partir desse momento, o Tipo some dos combos de seleção em movimentos novos, mas o histórico permanece intacto e a tela continua deixando consultar registros antigos.

---

## ❓ FAQ / Problemas comuns

**Criei um Tipo de Movimento e ele não aparece para seleção em `Cadastro de Movimentos` (código `53`).**
Confira: (1) `Inativo` está desmarcado? (2) o Comportamento bate com o que o usuário está tentando lançar (Entrada × Saída)? (3) o `Tipo Movimento` (Vendas/Compras/Outros) está na hierarquia esperada? (4) o usuário tem permissão de acesso ao grupo `TMOV_GRUPOS_ACESSOS` que inclui este tipo?

**O movimento foi gravado mas o saldo do produto não baixou.**
Provavelmente a `Transação de Estoque` do Tipo não está configurada para subtrair as camadas corretas (`Físico`, `Disponível`). Abra `Transações de Estoque` (código `33`), localize a Transação amarrada e confira as marcações `+`/`-`/`Nenhum` para cada situação. Veja também a aba **Itens → Estoque** deste Tipo para garantir que está apontando para a Transação correta.

**Gravei e a SEFAZ recusou o XML.**
A causa mais comum é CFOP incompatível com o comportamento do Tipo (entrada × saída) ou com a Natureza da Operação. Volte na aba **Cabeçalho → Fiscal → Natureza de Operação** e confirme que os CFOPs estão na faixa correta (1-3 para entrada, 5-7 para saída). Também confira a aba **Série** — o Modelo de Documento e a Série padrão precisam ser do mesmo tipo (fiscal/não fiscal).

**Está dando "Plano de Contas e Centro de Custo Obrigatório".**
O `Gerar Lançamento` da aba **Financeiro → Financeiro 1** está em modo que cria contas a pagar/receber, mas você não definiu o Plano e o Centro padrão. Preencha os dois ou mude o `Gerar Lançamento` para a opção que não gera financeiro.

**Tentei marcar `Atualizar Custo Automático` numa venda e foi bloqueado.**
É comportamento esperado — atualização automática de custo só faz sentido em **Compras/Outros** (entradas), porque é a entrada que define o custo. Vendas consomem o custo, não o atualizam.

**A tela tem regras que conflitam com configurações globais (mensagens "Configuração Geral").**
Algumas opções desta tela ficam bloqueadas quando a empresa tem flags globais antagônicas — por exemplo, `SEPARAR ITENS DO MOVIMENTO (Global)` ou `Promoção com Atualização em Grupo`. Nesses casos, a configuração da **empresa** precisa ser ajustada primeiro (fora desta tela), e isso também exige acesso de suporte.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Como se relaciona |
|------|---------------|--------------------|
| `Transações de Estoque` | `33` | O Tipo aponta para a Transação que decide o efeito em cada camada de saldo. |
| `Locais de Estoque` | `28` | Origem do Local padrão e do Local por empresa. |
| `Tabela de Preço` | `27` | O Tipo restringe quais tabelas estão disponíveis na venda. |
| `Cadastro de Produtos` | `32` | Produtos com flag `Não Movimentar Estoque` não entram em movimentos cujo Tipo movimenta estoque. |
| `Cadastro de Movimentos` | `53` (e variantes `201/202/203`, `209/210/211/220`) | Telas operacionais que **usam** o Tipo de Movimento configurado aqui. |
| `Pedido de Compra` | `64` | Idem, para o fluxo de pedido de compra. |
| `Produção de Produtos` | `144` | Usa Tipos específicos para Entrada do acabado, Saída dos ingredientes e Perda. |
| `Ajuste de Estoque` | `79` | Usa Tipos configurados para o ajuste — Entrada para diferença positiva, Saída para diferença negativa. |
| `Plano de Contas` | `14` | Origem do Plano padrão no financeiro do Tipo. |
| `Centros de Custos` | `15` | Origem do Centro padrão. |
| `Portadores` | `12` | Origem dos Portadores aceitos. |
| `Condições de Pagamento` | `8` | Origem da Condição padrão. |
| `Tipos de Contas PR` | `82` | Origem do Tipo de Documento Padrão no financeiro. |
| `Histórico de Movimentações` | `205` | Onde o efeito do Tipo aparece — filtra movimentos por Tipo. |

---

## ⚠️ Limites desta documentação

- Esta é a tela **mais complexa** do módulo Movimentação. A documentação acima é um **mapa de navegação** — cada combinação de campos pode ter sub-regras que só ficam claras testando ou consultando o suporte.
- Não cobre os detalhes do **layout DANFE / DANFCe / DANFSE** vinculados a cada Tipo (assunto do módulo Fiscal).
- Não detalha as regras de **comissão** por Cargo / Vendedor — o Tipo apenas oferece os percentuais base.
- Não cobre os **grupos de acesso** (`TMOV_GRUPOS`, `TMOV_GRUPOS_ACESSOS`) que controlam quais usuários veem quais Tipos — esse controle é feito em telas de permissão fora deste cadastro.
- Não cobre o módulo **Agrotóxico** em profundidade — esse fluxo é detalhado na documentação do módulo Agronômico.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de Suporte / Consultores de Implantação Sol.NET
