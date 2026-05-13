# 📄 Cadastro de Tipos de Movimento - Sol.NET

## 🎯 Visão Geral

O **Tipo de Movimento** é a configuração que define **como** cada movimento operacional (compra, venda, devolução, transferência, ajuste, produção, pedido) se comporta no Sol.NET. Ele concentra dezenas de regras — comportamento de estoque, regras fiscais, geração de financeiro, comissão, exclusividade da aplicação PDV, mobile, agrupamento, finalização — em um único registro reutilizável.

Para um panorama do papel do Tipo de Movimento no Sol.NET e o mapa das 12 abas do formulário, veja a [Visão Geral](README.md). Para troubleshooting das mensagens de bloqueio ao gravar, veja o [FAQ](faq.md).

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Tipos de Movimento` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nesta tela.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Tipos de Movimento |
| **Código (`F1`)** | `37` |

Abra a pesquisa universal (atalho `F1`) e digite **`37`** ou parte do nome **`Tipos de Movimento`**.

---

## 📝 Aba `Dados Cadastrais`

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
| **Características** | Comportamento geral do cabeçalho — Tipo Emissão (Própria × Terceiro), classificação do documento, opções padrão. Validação chave: Emissão `Terceiro` exige um `Tipo de Sequência` específico no combo — sem isso, *"Tipo Emissão Terceiro não permitido"*. |
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
| **Portador** | Painel de Portadores aceitos pelo tipo + Portador padrão. |

---

## 🎬 Aba `Finalizar`, `Mudar`, `Agrupar`

| Aba | O que configura |
|-----|-----------------|
| **Finalizar** | O que acontece quando o movimento é finalizado — botões, validações finais, geração de documentos. Inclui sub-aba `Finalizar / Mudar` que liga este Tipo a outro (ex.: `PEDIDO → VENDA` ao finalizar). |
| **Mudar** | Configura para qual Tipo este pode ser mudado (via `F7` na tela de Movimentos) e **como** essa mudança ocorre: `Transformar` (mesmo movimento muda de Tipo, sem exigir permissão de estorno) ou `Duplicar` (gera novo movimento, o anterior fica em status `VINCULADO` e forma pilha). Típico no ciclo `ORÇAMENTO → PEDIDO → VENDA`. |
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
| **Sistema** | Flags de sistema — PDV, Mobile, OS × OS Requisição, Devolução, Crédito Pessoa, Quitar Crédito Automaticamente. As validações cruzadas mais comuns aparecem no [FAQ](faq.md). |

> ℹ️ **Flag `PDV`.** Marcar `PDV` aqui **não altera** o comportamento do Tipo nas telas `Movimentos de Compras/Vendas/Outros` (`201/202/203`) — em vez disso, **torna o Tipo exclusivo da aplicação PDV** (frente de caixa), que é um sistema à parte do ponto de vista do usuário (mesmo Sol.NET compilado em modo PDV). Tipos com `PDV` marcado **não aparecem** no combo `Tipo` das telas de Movimentos da retaguarda — só são selecionáveis dentro do PDV. A aplicação PDV será documentada em outra seção.

---

## 🌿 Aba `Agrotóxico`

Configurações específicas para tipos que movimentam produtos agrotóxicos — vinculação com `Receituário Agronômico` (módulo Agronômico) e regras de rastreabilidade.

---

## 🚫 Exclusão

A exclusão de um Tipo de Movimento já em uso é bloqueada pelas integridades das tabelas filhas (Movimentos lançados com este Tipo em `201/202/203`, Tabelas de Preço vinculadas, etc.). Em produção, a recomendação é **inativar** o Tipo em vez de excluir — assim ele some dos combos de seleção em movimentos novos, mas o histórico continua referenciando o Tipo original para auditoria.

---

## 📋 Clonar Tipo de Movimento

A clonagem está disponível pelo menu de contexto do grid de busca (`Clonar Registro` — pede confirmação). Útil para criar variações: clone um Tipo `VENDA BALCÃO` para gerar `VENDA BALCÃO PROMOCIONAL` com poucas mudanças.

---

## 💡 Exemplos práticos

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Tipos de Movimento` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nesta tela.

Os exemplos abaixo descrevem o que o suporte tipicamente faz dentro deste cadastro. Tipos de Movimento mal configurados podem disparar a criação de movimentos sem financeiro, sem fiscal, com saldo de estoque incorreto, ou recusados pela SEFAZ — alinhar com a equipe Hetosoft antes de executar.

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

A partir de agora, este Tipo aparece como opção em `Movimentos de Vendas` (código `202`) para os usuários autorizados.

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

Este Tipo passa a aparecer como opção em `Movimentos de Compras` (código `201`).

### Exemplo 3 — Criar `DEVOLUÇÃO DE VENDA` que gera crédito ao cliente

1. Pesquisa `F1` → `37` → clone o Tipo `VENDA BALCÃO` (clique-direito → `Clonar Registro`).
2. Ajuste `Descrição`: `DEVOLUÇÃO DE VENDA`.
3. Aba **Cabeçalho → Fiscal**: CFOPs de **entrada** (`1xxx`/`2xxx`) — vendas que voltam.
4. Aba **Itens → Estoque**: Transação de Estoque que **soma** novamente (o produto volta).
5. Aba **Outras Operações → Sistema**:
   - `Devolução` = `Sim`.
   - `Devolução Crédito` ≥ `0` (gera crédito).
   - Se este Tipo for usado exclusivamente pela aplicação PDV (frente de caixa), marque `PDV` + `Quitar Crédito Automaticamente` — assim o crédito é abatido direto na próxima compra dentro do PDV. Para devoluções operadas pela retaguarda, deixe `PDV` desmarcado.
6. Aba **Financeiro → Financeiro 1**: `Não Estornar Financeiro` quando aplicável (válido para Tipos de Compras/Outros; bloqueado em Vendas).
7. **Gravar**.

Este Tipo passa a aparecer como opção em `Outros Movimentos` (código `203`) — devoluções de venda são operadas pela retaguarda, não por vendedores em `202`. Se a flag `PDV` for marcada, o Tipo deixa de aparecer nessas três telas e fica exclusivo da aplicação PDV.

### Exemplo 4 — Inativar um Tipo legado sem perder histórico

1. Pesquisa `F1` → `37` → localize o Tipo no grid → abra.
2. Marque `Inativo` no cabeçalho do formulário.
3. **Gravar**.

A partir desse momento, o Tipo some dos combos de seleção em movimentos novos, mas o histórico permanece intacto e a tela continua deixando consultar registros antigos.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Como se relaciona |
|------|---------------|--------------------|
| `Transações de Estoque` | `33` | O Tipo aponta para a Transação que decide o efeito em cada camada de saldo. |
| `Locais de Estoque` | `28` | Origem do Local padrão e do Local por empresa. |
| `Tabela de Preço` | `27` | O Tipo restringe quais tabelas estão disponíveis na venda. |
| `Cadastro de Produtos` | `32` | Produtos com flag `Não Movimentar Estoque` não entram em movimentos cujo Tipo movimenta estoque. |
| `Movimentos de Compras` | `201` | Tela operacional que **usa** Tipos de Movimento configurados aqui (entrada). |
| `Movimentos de Vendas` | `202` | Tela operacional que **usa** Tipos de Movimento configurados aqui (saída). |
| `Outros Movimentos` | `203` | Tela operacional que **usa** Tipos de Movimento configurados aqui (ajustes, transferências, perdas). |
| `Pedido de Compra` | `64` | Tela que dispara a criação de movimentos com Tipos configurados aqui. |
| `Produção de Produtos` | `144` | Idem — Tipos específicos para Entrada do acabado, Saída dos ingredientes e Perda. |
| `Ajuste de Estoque` | `79` | Idem — Tipos configurados para Entrada (diferença positiva) e Saída (diferença negativa). |
| `Plano de Contas` | `14` | Origem do Plano padrão no financeiro do Tipo. |
| `Centros de Custos` | `15` | Origem do Centro padrão. |
| `Portadores` | `12` | Origem dos Portadores aceitos. |
| `Condições de Pagamento` | `8` | Origem da Condição padrão. |
| `Tipos de Contas PR` | `82` | Origem do Tipo de Documento Padrão no financeiro. |
| `Histórico de Movimentações` | `205` | Onde o efeito do Tipo aparece — filtra movimentos por Tipo. |

---

## ⚠️ Limites desta documentação

- Esta é a tela **mais complexa** do módulo Movimentação. A documentação acima é um **mapa de campos** — cada combinação pode ter sub-regras que só ficam claras testando ou consultando o suporte.
- Não cobre os detalhes do **layout DANFE / DANFCe / DANFSE** vinculados a cada Tipo (assunto do módulo Fiscal).
- Não detalha as regras de **comissão** por Cargo / Vendedor — o Tipo apenas oferece os percentuais base.
- Não cobre os **grupos de acesso** (`TMOV_GRUPOS`, `TMOV_GRUPOS_ACESSOS`) que controlam quais usuários veem quais Tipos — esse controle é feito em telas de permissão fora deste cadastro.
- Não cobre o módulo **Agrotóxico** em profundidade — esse fluxo é detalhado na documentação do módulo Agronômico.
- Para a lista detalhada das mensagens de validação e onde resolver cada uma, veja o [FAQ](faq.md).

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de Suporte / Consultores de Implantação Sol.NET
