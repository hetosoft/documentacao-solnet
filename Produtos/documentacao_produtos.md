# 📄 Cadastro de Produtos - Sol.NET

## 🎯 Visão Geral

**Produtos** é o cadastro mais central do Sol.NET. Tudo que envolve estoque, movimentação, fiscal, PDV, e-commerce, balança, agronômico ou medicamento começa aqui. Cada registro de produto consolida, no mesmo formulário, informações de **identificação**, **classificação comercial**, **preços e custos por coluna (até oito)**, **tributação completa** (NCM, CEST, ICMS, ICMS-ST, IPI, CBS/IBS da Reforma Tributária), **estoque**, **histórico** e configurações específicas de **balança**, **medicamento**, **formulado agronômico** e **e-commerce/mobile**.

A tela é dimensionada para cobrir cenários muito diferentes — desde uma mercadoria simples de revenda até um defensivo agrícola com registro MAPA, passando por medicamentos com PMC e cód. ANVISA. Por causa disso, ela tem **dez abas principais** no formulário de lançamento, várias delas com **sub-abas** ativadas conforme o tipo de operação da empresa.

### Principais características

- ✅ **Até 8 colunas de preço de venda** com margens, comissões, moedas e promoções independentes por coluna.
- ✅ **Tributação completa**, incluindo blocos preparados para a **Reforma Tributária (CBS/IBS)**.
- ✅ **Vínculos hierárquicos** com Família, Grupo, Subgrupo, Departamento, Fabricante e Fornecedor.
- ✅ **Sub-cadastros especializados**: balança (informações nutricionais), medicamento (ANVISA), formulado agronômico (MAPA), grade (variantes), linkado (produto associado), preço progressivo, produto por empresa.
- ✅ **Auditoria de NCM e descrição** com flags de verificação periódica.
- ✅ **Validações fortes** contra cadastros duplicados e inconsistências entre unidade × quantidade tributária e moeda × preço.

---

## 🚪 Como acessar

Abra a pesquisa universal (atalho `F1`) e digite **`32`** (ou parte do nome `Produtos`). Todos os usuários com permissão de cadastro têm acesso pela mesma pesquisa.

> 💡 **Por que esse cadastro é tão grande?** Como o Sol.NET atende clientes de varejo, atacado, distribuição, farmácia, agropecuária e indústria, todos os campos específicos desses ramos convivem na mesma tela. Em uma empresa comum, a maioria das abas e sub-abas fica vazia — só preencha o que faz sentido para o tipo de produto que você cadastra.

---

## 🧭 Sub-abas do formulário

A área de lançamento (parte de cadastro e edição) traz **dez abas**. A ordem reflete a sequência natural de preenchimento, mas você pode preencher fora de ordem se preferir.

| Aba | O que recebe |
|---|---|
| **Principal** | Identificação, classificação, status, unidade, foto, grade e linkado. |
| **Preços** | Preços de venda 1–8, margens, comissões, moedas, promoções, markup. |
| **Preço Auxiliar** | Dois preços auxiliares (com descrição livre) — usados em integrações ou contextos paralelos. |
| **Custos** | Custo médio, custo unitário, custo de venda, custo inicial, último e penúltimo custo. |
| **Campos Complementares** | Descrição complementar fiscal, observação, aplicação, descrição completa e linhas extras. |
| **Tributação** | NCM, CEST, regiões ICMS, ICMS Crédito Outorgado, CBS/IBS, vigências, ANP, regime especial. |
| **Outros** | Conjunto de sub-abas especializadas (similares, sugestão, balança, estoque mínimo, localização, preço progressivo, por empresa, medicamento, fórmulas, formulado agro). |
| **Movimentação** | Unidade tributária, quantidades, conversões entre produtos linkados, peso. |
| **Informações** | Sub-abas somente leitura: Geral (datas, usuário), Tributos (auditoria), Datas (alterações de preço). |
| **Estoque** | Saldos e custo médio do estoque consolidado. |

Cada aba é detalhada nas próximas seções.

---

## 📋 Aba Principal

A primeira aba reúne tudo que identifica o produto, classifica comercialmente e controla a disponibilidade.

### Identificação

- **Código** — código interno do produto. Pode ser digitado ou gerado automaticamente. Quando ocorre duplicidade no momento de salvar, o sistema oferece o próximo código sequencial disponível (ver [Validações](#validações-principais)).
- **Descrição** — nome do produto. Limite 120 caracteres. A combinação `Descrição + Marca/Fabricante` precisa ser única (ver validações).
- **Descrição Reduzida** — versão curta usada em cupons, etiquetas e telas estreitas.
- **Descrição Completa** — texto livre adicional para e-commerce e relatórios.
- **Código de Barras** — código GTIN/EAN. Pode haver múltiplos códigos por produto (gerenciados em sub-cadastro à parte do `Produtos`).
- **Código do Fabricante** e **Código do Fornecedor** — códigos externos quando o produto é identificado também por terceiros.

### Tipo de Item — Atividade

Combo obrigatório com a classificação SPED do item:

| Valor SPED exibido | O que significa |
|---|---|
| `00 – Mercadoria para Revenda` | Item comprado para ser revendido. |
| `01 – Matéria-Prima` | Insumo de produção. |
| `02 – Embalagem` | Embalagem. |
| `03 – Produto em Processo` | Item em fabricação. |
| `04 – Produto Acabado` | Produto pronto para venda. |
| `05 – Subproduto` | Subproduto da industrialização. |
| `06 – Produto Intermediário` | Intermediário de produção. |
| `07 – Material de Uso e Consumo` | Item de uso/consumo interno. |
| `08 – Ativo Imobilizado` | Bem do ativo. |
| `09 – Serviços` | Serviço prestado. |
| `10 – Outros insumos` | Demais insumos. |
| `99 – Outras` | Demais classificações. |

> ⚠️ **Atenção:** o valor exibido na tela (`00`, `01`, …, `99`) é o **código SPED** apresentado ao usuário. Internamente, o sistema grava esses códigos com numeração própria e **não** com o número que aparece. Para a operação isso não muda nada — basta escolher a descrição correta — mas em relatórios ou exportações que mostrem o valor bruto da coluna pode haver diferença em relação ao `99` mostrado na tela.

### Status e disponibilidade

- **Inativo** — quando marcado, oculta o produto da maioria das pesquisas e bloqueia novos lançamentos.
- **Inativo para Venda** — disponível para compra/movimentação interna, mas não pode ser vendido.
- **Inativo para Compra** — vendável, mas não permite entrada (ex.: produto descontinuado pelo fornecedor).
- **Desabilitar Desconto / Comissão / Arredondamento** — flags que removem comportamentos automáticos para este produto.
- **Permissão de Venda / Permissão Maioridade** — restringem a quem pode vender (ex.: itens controlados, bebidas alcoólicas).

### Classificação comercial

Todos os campos abaixo são lookups para cadastros próprios (abra pela pesquisa F1):

- **Família** (tela `24`) — primeiro nível.
- **Grupo** (tela `25`) — segundo nível.
- **Subgrupo** (tela `26`) — terceiro nível.
- **Departamento** (tela `104`) — visão por departamento da loja, independente da hierarquia Família/Grupo/Subgrupo.
- **Fabricante** e **Fornecedor** (pesquisas de Pessoas).
- **Atualização em Grupo** (tela `45`) — agrupador para mudanças em lote.

### Unidade e tributária

- **Unidade** — unidade de medida principal (UN, KG, M, etc.).
- **Unidade Tributária** + **Quantidade Tributária** — usadas quando o produto é movimentado/tributado em unidade diferente da unidade principal. Os dois campos andam juntos:
  - Se preencher Quantidade Tributária, **é obrigatório** preencher Unidade Tributária (e vice-versa).
  - Quando Unidade = Unidade Tributária, a Quantidade Tributária precisa ser **1**.

### Foto e imagens

A coluna esquerda da aba mantém um carrossel de imagens do produto. Use os botões laterais para adicionar/trocar a imagem principal. As demais imagens são gerenciadas em diálogo próprio aberto pelo botão das miniaturas.

### Grade e Linkado

- **Grade** — vincula o produto a uma estrutura de variantes (ex.: tamanho × cor). O cadastro de `Grade` é à parte, e cada filho da grade pode ter seu próprio código e preço.
- **Linkado** — associa o produto a outro (produto-pai). Útil em conversões (ex.: caixa que se desmembra em unidades). Quando há produto linkado, o campo **Conversão** torna-se obrigatório.

---

## 💵 Aba Preços

A área de preços é, depois da Principal, a aba mais usada. Tudo aqui replica em oito colunas (`Preço 1` a `Preço 8`), permitindo políticas diferentes para canais distintos (atacado/varejo, e-commerce, vendedor externo, etc.).

### Custos no contexto de preço

- **Custo Unitário** — base de cálculo do preço.
- **Margem de Custo (%)** — acréscimo aplicado sobre o custo unitário.
- **Custo de Venda** — valor de custo levado para o cálculo do preço.

### Composição do preço — por coluna (1 a 8)

| Campo | O que faz |
|---|---|
| **Margem de Lucro %** | Margem desejada sobre o custo de venda. |
| **Margem de Lucro Real %** | Margem efetivamente aplicada (pode divergir da desejada quando há arredondamento ou margem mínima). |
| **Margem Bruta %** | Margem antes de impostos e despesas. |
| **Lucro Líquido** | Resultado líquido para a coluna. |
| **Comissão %** | Comissão calculada sobre essa coluna. |
| **Markup %** | Multiplicador sobre o custo. |
| **Preço de Venda** | Valor final praticado. |
| **Preço Anterior** | Histórico do preço imediatamente anterior. |
| **Preço Voltar** | Valor para usar com a função de reverter preço. |
| **Promoção** | Preço promocional para a coluna. |
| **Moeda** | Moeda do preço (ver validação abaixo). |
| **Data da última alteração** + **Usuário** | Registrados automaticamente. |

### Margens limite e arredondamento

- **Margem Mínima** e **Margem Máxima** — limites de segurança. O Sol.NET avisa quando a margem real cai fora da faixa.
- **% Desconto de Venda** — desconto-padrão sugerido em vendas.
- **Desabilitar Arredondamento** — quando marcado, o sistema não aplica regras de arredondamento configuradas em Tabela de Preço.

### Moeda por preço — validação

Cada coluna tem sua própria moeda. O sistema impede que você grave um preço maior que zero **sem** moeda associada — se preencher `Preço de Venda 1 = 12,90` deixando a Moeda 1 em branco, ao salvar o cursor é levado para a aba `Preços`, focado na Moeda da coluna, com a mensagem `Não permitido! Preechar Moeda <N>`.

> 💡 **Lucro Líquido x Margem.** Margem e markup são calculadores; o Lucro Líquido é o resultado financeiro real estimado depois de impostos e despesas configurados em Tabela de Preço. Use-o para conferir se o preço composto faz sentido.

---

## 💼 Aba Preço Auxiliar

Aba reduzida para registrar **dois preços alternativos** ao conjunto principal:

- **Preço Auxiliar 1** — descrição livre + valor.
- **Preço Auxiliar 2** — descrição livre + valor.

Esses preços não entram automaticamente nos cálculos de venda — são consultados sob demanda por integrações, relatórios ou regras específicas (ex.: preço de fábrica, preço sugerido, preço de tabela externa).

---

## 💲 Aba Custos

Concentra todos os campos relacionados ao **custo** do produto, em formato histórico.

### Custo médio

- **Custo Médio** — valor por unidade, calculado pelo Sol.NET conforme as entradas registradas. Não é editado manualmente em condições normais.
- **Custo Médio Unitário** — variação por unidade quando o produto tem fator de conversão.
- **Custo Médio do Estoque** (`CUSTO_MEDIO_EST`) — saldo total em valor da posição atual do estoque por custo médio.
- **Custo Médio com ICMS / com PIS/COFINS** — custo médio considerando os tributos creditados.

### Penúltimo e último custo

Cada um desses blocos guarda o custo de aquisição imediatamente anterior, com data:

- **Último Preço de Compra** — referência mais recente, vinda de movimentos de compra.
- **Penúltimo Custo** — registro anterior ao último (útil para conferência de tendência).

### Histórico de alterações de preço

A coluna lateral guarda **data + usuário** de cada alteração nas oito colunas de preço (`Data Alteração 1` … `Data Alteração 8`). Esses campos são preenchidos automaticamente quando o preço da coluna é alterado e salvo.

---

## ➕ Aba Campos Complementares

Reúne descrições e textos auxiliares que aparecem em documentos fiscais, ordens de serviço e relatórios.

- **Descrição Complementar (Fiscal)** — texto que entra junto da descrição do item nos documentos fiscais (NF-e, NFC-e, CT-e). Limite mais largo que a descrição principal.
- **Observação** — anotação interna não publicada.
- **Aplicação** — onde o produto é aplicado (especialmente útil em autopeças e produtos industriais).
- **Descrição Completa** — texto longo para portais de e-commerce.
- **Linha Extra 1 / Linha Extra 2** — duas linhas livres adicionais.
- **SPED – Código Anterior** / **SPED – Descrição Anterior** / **Data Alteração SPED** — preservam o código/descrição usados antes de uma mudança, para preservar a continuidade em arquivos SPED.

> 💡 **Quando preencher Descrição Complementar Fiscal?** Sempre que o fisco exigir informação complementar no item — por exemplo, características técnicas obrigatórias em medicamentos, número de lote em produtos sujeitos a rastreabilidade, ou anotações de natureza tributária.

---

## 🏛️ Aba Tributação

A aba mais densa do cadastro. Concentra **toda** a base tributária do produto. Mudanças aqui se refletem em todos os movimentos posteriores e nos arquivos fiscais.

### Cabeçalho fiscal

- **NCM** — Nomenclatura Comum do Mercosul. Lookup para o cadastro de [NCM](../Fiscal/documentacao_ncm.md). É a chave para as alíquotas federais (IPI, PIS/COFINS) e para a referência da Reforma Tributária.
- **CEST** — quando aplicável.
- **Origem** — origem da mercadoria (nacional, importada, etc.).
- **Tributação Estadual** — vinculação ao cadastro de Tributação Estadual.

### Regiões ICMS

- **Região ICMS Saída** — vincula o produto a uma Região ICMS Saída ([documentação](../Fiscal/documentacao_regiao_icms.md)), que define a alíquota efetiva por UF de destino.
- **Região ICMS-ST Saída** — equivalente para ICMS-ST ([documentação](../Fiscal/documentacao_regiao_icms_st_saida.md)).

### De Olho no Imposto

Grupo com **Vigência Inicial** e demais marcações para o programa "De Olho no Imposto" (impostos discriminados no cupom). Vincula a data a partir da qual o produto passa a discriminar a carga tributária no documento fiscal.

### ICMS Normal — Saída

Bloco usado quando a operação exige reduções, basis específicas ou regimes próprios na saída. Campos típicos:

- **NCM Base** — NCM usado especificamente para o cálculo da base.
- Alíquotas auxiliares, percentuais de redução e flags do regime.

### ICMS Crédito Outorgado — Saída

Combo com o cadastro de NCM para fins de **crédito outorgado** quando a UF do estabelecimento concede o benefício.

### CBS/IBS — Reforma Tributária

Bloco preparado para a Reforma Tributária (EC 132/2023):

- **Alíquota CBS** — Contribuição sobre Bens e Serviços (tributo federal).
- **Alíquota IBS** — Imposto sobre Bens e Serviços (tributo subnacional).
- **Regime especial** — quando aplicável.

> Para a visão geral da Reforma Tributária no Sol.NET, leia [documentacao_reforma_tributaria.md](../Fiscal/documentacao_reforma_tributaria.md).

### Outros campos da aba

- **AMP / Combustível** — flags específicas para combustíveis.
- **Tabela ANP** — quando o produto está sujeito ao controle ANP.
- **Imendes – Regime Especial** — regime tributário especial para vínculo com o sistema Imendes.
- **Código de Natureza da Receita** — campo informativo usado em relatórios.
- **Data de Auditoria NCM** + **Não Auditar Tributação** — controle interno para revisões periódicas dos NCMs cadastrados.

---

## 🔧 Aba Outros — sub-abas especializadas

A aba `Outros` agrupa todas as funcionalidades opcionais. Cada sub-aba pode ficar completamente vazia se a empresa não usar a feature correspondente.

### Atualização em Grupo

Grid com todos os campos de Atualização em Grupo já aplicados ao produto, vindos da tela `Atualização em Grupo` (`45`). Útil para auditar quais alterações em lote tocaram este produto.

### Produtos Similar

Lista de produtos **semelhantes** que podem substituir o item em rupturas. Cada linha é um vínculo simples (id do produto similar + observação). Usado no PDV e em buscadores para sugerir alternativas.

### Produtos Sugestão

Lista de produtos sugeridos em **venda casada** (ex.: ao vender um item, sugerir acessórios). Vincula um ou mais produtos com observação livre.

### Balança

Bloco completo para produtos pesáveis (balança no PDV ou balança no recebimento). Inclui:

- **Setor da Balança** + **Receita** + **Quantidade** + **Validade**.
- **Informações Nutricionais** completas, com porção, parte inteira/decimal, medida caseira:
  - Valor Energético, Carboidratos, Proteína, Gordura Total / Saturada / Trans, Fibra, Sódio.
  - Açúcares Totais e Açúcares Adicionados.
  - Lactose e Galactose (com flag de impressão).
- **Selos de alto teor** — Alto Açúcar, Alta Gordura, Alto Sódio.
- **% sobre Valor Diário** para cada nutriente.
- **Quantidade Automática por Porção** e **Quantidade por Embalagem** — para cálculo automático.

### Estoque Mínimo

Define **estoque mínimo** e parâmetros relacionados, usados no cálculo de sugestão de compra e em alertas do dashboard.

### Localização

Endereçamento físico do produto no depósito: prateleira, corredor, posição. Geralmente integrado com o leitor de coletor.

### Preço Progressivo

Permite definir preços diferentes conforme a **quantidade vendida** (ex.: 1–9 un. → R$ 10,00; 10–49 un. → R$ 9,00; 50+ → R$ 8,00). Cada faixa é uma linha do grid.

### Produto por Empresa

Quando a base atende **mais de uma empresa** (multiempresa), esta sub-aba permite configurar dados específicos por empresa — estoque mínimo, preços, status (`Inativo` por empresa), local padrão. Sem registros aqui, o produto vale para todas as empresas com os dados das demais abas.

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Empresas` (não nesta aba — mas no cadastro de Empresas referenciado) requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de mexer em Empresas.

### Medicamento

Bloco específico para farmácias:

- **PMC** (Preço Máximo ao Consumidor).
- **Código ANVISA**.
- **Motivo de Isenção** — quando o produto é isento de algum tributo controlado.
- **Tipo de Medicamento Veterinário** — quando se aplica.

### Fórmulas

Vínculo com [Fórmulas de Produtos](../Movimentacao/Producao/documentacao_formulas_de_produtos.md) (tela `143`). Lista as fórmulas em que este produto entra como insumo **e** as fórmulas que produzem este produto.

### Formulado Agro.

Bloco para defensivos agrícolas:

- **Registro MAPA** (com botão de busca/validação).
- **Formulado** (ingrediente ativo, classe).
- **Embalagem** (lookup) e **Tipo de Embalagem** — definem unidade comercial regulada.

> 💡 **Quando preencher os blocos especializados?** Os blocos de Balança, Medicamento e Formulado Agro só fazem sentido quando o ramo da empresa exige. Em uma loja de autopeças, por exemplo, esses três ficam vazios — não tem impacto algum em vendas e movimentações regulares.

---

## 🔄 Aba Movimentação

Aba editável que reúne os parâmetros usados nas movimentações do produto:

- **Unidade Tributária** e **Quantidade Tributária** — confirmados aqui também (espelham os campos da aba Principal).
- **Peso Bruto** e **Peso Líquido** — usados em frete, balança, NF-e.
- **Altura / Largura / Comprimento** — dimensões para frete e prateleira.
- **Conversão de Estoque** — quando o produto é linkado, define a relação numérica entre pai e filho.
- **Produto de Estoque** — para casos em que o saldo de estoque é mantido em outro produto (ex.: kit que consome saldo do produto-base).
- **Não Validar Estoque** — quando marcado, permite vendas mesmo sem saldo. Use com cautela — desligar o controle de estoque para um item afeta todos os relatórios de ruptura.
- **Tipo de Frete** — comportamento padrão de frete.

---

## ℹ️ Aba Informações

Aba **somente leitura**, dividida em três sub-abas. Útil para suporte e auditoria.

### Geral

- **Cadastrado em** — data e hora de criação do registro.
- **Alterado em** — última alteração geral.
- **Usuário** — quem cadastrou e quem alterou por último.
- **Status de descrição** e **Data de Verificação da Descrição** — flags da rotina de revisão de descrição.
- **Status de imagem** e **Data de Verificação da Imagem** — flags análogas para imagens.
- **Erro de Integração** — quando o produto sincroniza com sistemas externos e o último envio falhou.

### Tributos

Linha do tempo de auditoria tributária:

- **Data de Auditoria NCM** — última vez que o NCM foi conferido.
- **Não Auditar Tributação** — exclui o produto das rotinas automáticas de auditoria fiscal.

### Datas

Para cada uma das **oito colunas de preço**, exibe **Data + Usuário** da última alteração de:

- Preço de venda.
- Custo unitário.
- Preço anterior.

Essas datas alimentam relatórios de alteração de preço e o histórico exibido no PDV.

---

## 📦 Aba Estoque

Visão consolidada do estoque do produto:

- **Saldo atual** por Local de Estoque (vinculado ao cadastro de [Locais de Estoque](../Movimentacao/documentacao_locais_de_estoque.md)).
- **Custo médio do estoque** (`Custo Médio Estoque` × `Custo Médio Valor`).
- **Indicadores de ponto de equilíbrio** por coluna de preço.
- **Estoque mínimo para e-commerce** quando configurado.

Para a análise detalhada de movimentação por produto, consulte [Histórico de Produtos](../Movimentacao/documentacao_historico_de_produtos.md).

---

## ⚠️ Validações principais

Todas as validações abaixo rodam **ao salvar** o cadastro. Quando alguma falha, o foco vai para o campo (e aba) correspondente e o sistema exibe a mensagem indicada.

### Código duplicado

- Mensagem: **`<Label> (VALOR) Já Existe!`**.
- Comportamento: o sistema oferece **gerar o próximo código sequencial** disponível e gravar o gerador `PRODUTO_CODIGO_GERADOR` para o próximo cadastro. Aceite só se a duplicidade for, de fato, acidental.

### Descrição duplicada por Fabricante

- Regra: a combinação **`Descrição + Marca/Fabricante`** precisa ser única (Fabricante em branco também é considerado).
- Mensagem: **`Já Existe essa "DESCRIÇÃO" Associada a "MARCA/FABRICANTE"`** com o nome do fabricante (ou `"NENHUM"` quando não preenchido).
- Quando ignorar a regra: o sistema permite que o suporte habilite "Aceitar descrição igual" em situações específicas — esse acesso é restrito ao suporte.

### Unidade Tributária × Quantidade Tributária

- Se você preenche **Quantidade Tributária**, **Unidade Tributária** vira obrigatória: mensagem **`Obrigatório preecher os dois campos!`** com o foco na Unidade Tributária na aba `Movimentação`.
- Se Unidade = Unidade Tributária, **Quantidade Tributária precisa ser 1**: mensagem **`Não Permitido, Unidade e Unidade Tributária Iguais! Com "<Quantidade Tributária>" Diferente de (1)Um.`**. O sistema corrige automaticamente para 1.

### Moeda × Preço

- Regra: cada **Preço de Venda > 0** exige a **Moeda** correspondente preenchida (1 a 8 são independentes).
- Mensagem: **`Não permitido! Preechar Moeda <N>`** — o foco vai para o combo da moeda na aba `Preços`.

### Produto Linkado × Conversão

- Quando há Produto Linkado, **Conversão** torna-se obrigatória: mensagem **`Obrigatório preecher o campo "<rótulo>"!`**.

### Produto Diversos

- Existem três flags `Produto Diversos` (geral, pedido, CT-e). Se uma flag está marcada no registro, **não é possível** desmarcá-la depois sem permissão equivalente: o sistema bloqueia com **`Não permitido! Desmarcar "<nome>"`**.

---

## 💡 Exemplos práticos

### Cadastrar uma mercadoria de revenda simples

1. Abra a pesquisa universal (`F1`), digite `32` e abra `Produtos`. Clique em `Novo`.
2. Na aba **Principal**, preencha:
   - **Código**: digite ou deixe o sistema gerar.
   - **Descrição**: nome comercial.
   - **Tipo de Item**: `00 – Mercadoria para Revenda`.
   - **Família / Grupo / Subgrupo**: classifique no cadastro hierárquico.
   - **Fabricante**: opcional; se preenchido, lembre-se que `Descrição + Fabricante` precisa ser único.
   - **Unidade**: ex. `UN`.
3. Na aba **Preços**, informe **Custo Unitário 1**, **Margem de Lucro 1** e **Moeda 1**. O Preço de Venda 1 será calculado.
4. Na aba **Tributação**, vincule **NCM** e, se aplicável, **CEST** e **Região ICMS Saída**.
5. Confirme a gravação. Se houver duplicidade de código ou descrição, ajuste conforme a mensagem.

### Cadastrar um produto pesável com balança

1. Faça o cadastro básico como acima.
2. Na aba **Principal**, defina **Unidade = KG**.
3. Na aba **Outros**, sub-aba **Balança**:
   - **Setor**, **Receita**, **Validade**.
   - Preencha o painel **Informações Nutricionais**: porção, parte inteira/decimal, valor energético, carboidratos, proteína, gordura total/saturada/trans, fibra, sódio, açúcares totais e adicionados.
   - Se necessário, marque os selos **Alto Açúcar / Alta Gordura / Alto Sódio**.
4. Salve. O produto está pronto para ser enviado à balança e impresso na etiqueta de gôndola.

### Cadastrar um medicamento

1. Cadastro básico como em "Mercadoria de revenda".
2. Na aba **Outros**, sub-aba **Medicamento**:
   - **PMC** — Preço Máximo ao Consumidor (obrigatório por regulação).
   - **Código ANVISA**.
   - **Motivo de Isenção** quando aplicável.
3. Marque `TP_MEDICAMENTO` (campo `Medicamento`) no cadastro. Em alguns layouts esse flag aparece direto na aba Principal.
4. Salve.

### Cadastrar um defensivo agrícola (formulado)

1. Cadastro básico, com **Tipo de Item = 00 ou conforme política**.
2. Na aba **Outros**, sub-aba **Formulado Agro.**:
   - **Registro MAPA** (use o botão para validar o registro).
   - **Formulado** (ingrediente ativo).
   - **Embalagem** e **Tipo de Embalagem**.
3. Em **Tributação**, confirme NCM apropriado para defensivo.
4. Salve. O produto fica disponível também para uso em [Receituário Agronômico](../Agronomico/documentacao_receituario_agronomico.md).

### Atualizar o preço de venda de um item já cadastrado

1. Abra `Produtos` (`32`) e localize o item.
2. Vá direto para a aba **Preços**.
3. Altere o **Preço de Venda 1** (ou a coluna desejada). O Sol.NET registra automaticamente o **Preço Anterior** e a data/usuário da alteração.
4. Confira na aba **Informações → Datas** o histórico após salvar.

### Inativar um produto

- **Saída completa do catálogo** — marque **Inativo** na aba Principal.
- **Permitir só consumo interno, sem venda** — marque **Inativo para Venda**.
- **Item descontinuado pelo fornecedor** — marque **Inativo para Compra** (continua vendável até esgotar o saldo).

---

## ❓ FAQ / Problemas comuns

Veja a versão estendida em [faq.md](faq.md).

### ❓ O sistema sugeriu um código diferente do que digitei. Por quê?

Você tentou gravar com um código já usado. O Sol.NET oferece o próximo código sequencial livre e atualiza o gerador `PRODUTO_CODIGO_GERADOR` para que o próximo cadastro continue a partir daí. Se o código antigo era o realmente desejado, cancele e investigue qual produto já o usa.

### ❓ Estou tentando salvar mas o foco fica indo para a aba Preços com mensagem de moeda. Como resolver?

Algum **Preço de Venda > 0** está sem **Moeda** correspondente preenchida. Vá à aba `Preços` e confirme a moeda em cada coluna onde o preço foi informado. Mesmo `Preço 2` precisa de `Moeda 2`.

### ❓ Posso usar a mesma descrição em produtos de fabricantes diferentes?

Sim. A regra de unicidade é por combinação `Descrição + Marca/Fabricante`. Dois produtos com descrição "Camiseta Básica" + fabricantes diferentes coexistem normalmente.

### ❓ Onde vejo o histórico de movimentações deste produto?

No módulo [Movimentação → Histórico de Produtos](../Movimentacao/documentacao_historico_de_produtos.md). Esta tela cobre apenas o **cadastro**.

### ❓ A aba "Produto por Empresa" está vazia — está errado?

Não. Quando a aba está vazia, o produto vale para todas as empresas com os dados informados nas demais abas. Você só preenche ali quando precisa **diferenciar** o produto entre empresas (estoque mínimo, preço, status diferente, local diferente).

### ❓ Tenho um produto que é uma "caixa com 12 unidades". Como cadastro?

Cadastre os dois produtos (a unidade e a caixa) e use **Produto Linkado** + **Conversão** no produto-caixa apontando para o produto-unidade com fator `12`. Movimentações da caixa rebatem no saldo da unidade.

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Equipe de suporte Hetosoft e usuários do Sol.NET
