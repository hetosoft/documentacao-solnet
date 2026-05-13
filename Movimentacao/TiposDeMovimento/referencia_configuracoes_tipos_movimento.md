# 📄 Tipos de Movimento — Referência de Configurações (Checkboxes e Combos) - Sol.NET

## 🎯 Visão Geral

Esta página complementa a [Documentação principal](documentacao_tipos_de_movimento.md) com uma **referência campo-a-campo** dos controles do formulário `Cadastro de Tipos de Movimento` (código `37`). O escopo aqui é restrito aos campos **de marcação** (checkboxes) e **de escolha** (combos) — os demais controles (caixas de texto, grids, lookups de tabelas relacionadas, painéis com botões) estão na [Documentação principal](documentacao_tipos_de_movimento.md) e no [FAQ](faq.md).

Cada item descreve o que muda no comportamento do Sol.NET quando a opção é marcada (checkbox) ou ao escolher cada valor do combo. Flags com impacto fiscal, financeiro ou de estoque ganham um bloco `> ⚠️ Atenção` logo abaixo, com a regra prática a respeitar.

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Tipos de Movimento` exigem permissão de acesso de suporte. Toda mudança aqui se propaga para movimentos futuros lançados em `201/202/203` (e na aplicação PDV) — alinhe sempre com a equipe Hetosoft antes de tocar nas opções.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Tipos de Movimento |
| **Código (`F1`)** | `37` |

Abra a pesquisa universal (`F1`) e digite **`37`** ou parte do nome **`Tipos de Movimento`**. A consulta dos registros existentes acontece na lista do alto da tela; abrir um registro leva ao formulário com as abas descritas a seguir.

---

## 📑 Como ler esta referência

- **Cada seção corresponde a uma aba** do formulário, na ordem em que aparece na tela.
- **Checkboxes** entram em lista compacta: `- **Caption visível** — efeito quando marcado`.
- **Combos** entram como item de lista com sub-itens por opção: cada opção é apresentada como `` `Valor` — efeito ``.
- **Marcas críticas** (impacto fiscal/financeiro/estoque/PDV) ganham um blockquote `> ⚠️ **Atenção.**` logo após o item.
- Combos que carregam **opções dinâmicas** (Tabelas de Preço, Portadores, Empresas, Locais de Estoque etc.) descrevem apenas **o que o combo seleciona**, sem listar opções — porque elas vêm de cadastros vinculados.
- O alvo é o **uso operacional** do campo. Para validações cruzadas (mensagens "Obrigatório…", "Não permitido…"), use o [FAQ](faq.md).

---

## 🗂️ Aba `Dados Cadastrais`

Primeira aba ao abrir um Tipo. Concentra a identificação, a hierarquia operacional e os flags de comportamento mais abrangentes.

### Checkboxes

- **PDV** — torna este Tipo de Movimento **exclusivo da aplicação PDV** (frente de caixa). Não muda o comportamento interno do Tipo; apenas o restringe.
  > ⚠️ **Atenção.** Tipos com `PDV` marcado **deixam de aparecer** no combo `Tipo` das telas `Movimentos de Compras` (`201`), `Movimentos de Vendas` (`202`) e `Outros Movimentos` (`203`) da retaguarda. Eles só são selecionáveis dentro da aplicação PDV (mesmo Sol.NET compilado em modo PDV — outra aplicação do ponto de vista do usuário).

- **Devolução** — classifica este Tipo como movimento de devolução, habilitando os controles de crédito/cashback da aba `Campos Complementares` e expondo o Tipo nos fluxos de devolução do PDV.
  > ⚠️ **Atenção.** Devolução de venda é operada pela retaguarda em `Outros Movimentos` (`203`), não em `Movimentos de Vendas` (`202`). Marque `Devolução` em Tipos usados para retornos — não em vendas comuns.

- **Permitir Agrupar** — autoriza a função `Agrupar Movimentos` a recolher vários movimentos deste Tipo em uma única nota fiscal (ex.: 10 pedidos viram 1 NF-e).

- **Receber Agrupamento** — autoriza este Tipo a ser o **destino** de um agrupamento (o Tipo no qual a nota agrupada será gerada).

- **Pedido de Compra** — habilita este Tipo a aparecer na tela `Pedido de Compra` (código `64`), permitindo que ele seja usado como Tipo do pedido.

- **Estatística: Vendas/Compras (Movimento)** — inclui movimentos deste Tipo nos relatórios estatísticos de Vendas/Compras a nível de **cabeçalho** (totais por dia, por pessoa, por vendedor).

- **Estatística: Vendas/Compras (Estoque)** — inclui os itens deste Tipo nos relatórios estatísticos a nível de **estoque** (giro de produto, curva ABC).

- **Não consultar em lançamento** — esconde este Tipo do combo `Tipo` ao lançar um novo movimento manualmente. O Tipo continua disponível para ser referenciado por **fluxos pré-determinados** (ex.: alvo de um `Mudar` configurado em outro Tipo), mas o usuário não consegue escolhê-lo direto na criação de um movimento.
  > ⚠️ **Atenção.** Use em Tipos intermediários de um fluxo automatizado (ex.: `PEDIDO_INTERNO` que só nasce via Mudar a partir de `ORÇAMENTO`). Evita que o operador crie movimentos órfãos desse Tipo sem passar pelo fluxo correto.

- **Marcar Importado** — ao usar a função `Importar Itens` no movimento, marca cada item importado com o ID do movimento de origem (rastreabilidade — permite saber depois de qual movimento aquele item foi trazido).

- **Usar Notas Referenciadas** — habilita a aba `Notas Referenciadas` no movimento, onde se cita chave de NF-e de origem (caso comum em devolução/complemento).

- **Referenciar Mov. Próprio** — controla **qual** movimento é gravado como referência ao importar itens de outro movimento:
  - **Desmarcada** — o sistema verifica se o movimento que está sendo importado **já referencia** outro movimento e usa essa referência (cadeia indireta). É o caso da rotina cupom → pedido de devolução → NF-e Devolução: a NF-e Devolução importa itens do `Pedido de Devolução` e, com a flag **desmarcada**, herda como referência o cupom fiscal que o pedido já apontava (a NF-e fiscal acaba apontando o documento fiscal original — comportamento desejado).
  - **Marcada** — o sistema referencia diretamente o movimento que está sendo importado (no exemplo acima, a NF-e Devolução referenciaria o próprio `Pedido de Devolução`, não o cupom).

  > 💡 **Fluxo típico desmarcado.** Cliente faz devolução, atendente cria rápido um `Pedido de Devolução` apontando o cupom fiscal (operação repetida várias vezes ao dia). Ao fim do dia, o operador seleciona todos os pedidos para gerar a NF-e de Devolução. Como o documento fiscal final precisa apontar o cupom (não o pedido intermediário), o Tipo `NF-e Devolução` mantém esta flag **desmarcada**.

### Combos

- **Tipo Geral** — classifica este Tipo dentro da hierarquia geral usada por relatórios e fluxos automatizados. Opções:
  - `Vendas/Compras` — operação fiscal/financeira padrão.
  - `Devolução` — operação de retorno (use junto com o checkbox `Devolução`).
  - `Transferência` — movimentação entre empresas/filiais.
  - `Ajuste Estoque` — ajuste sem efeito fiscal.
  - `Perdas` — baixa de estoque por perda.

> ⚠️ **Atenção.** A classificação operativa também depende do **operador** do Tipo (combo `Tipo Movimento` no painel principal — `Vendas`/`Compras`/`Outros`) e do **Comportamento** (`Entrada`/`Saída`/`Outros`). A combinação dos três define em qual das telas `201/202/203` o Tipo aparece — devolução de venda e transferência entre filiais sempre caem em `203` (`Outros Movimentos`), mesmo que envolvam venda.

---

## 🗂️ Aba `Tipo Mov. por Empresa`

Permite refinar configurações deste Tipo **por empresa/filial** quando o Sol.NET está em modo multi-empresa.

### Checkboxes

- **Individual** — sinaliza que este Tipo terá configurações **individualizadas** por empresa (cada loja pode ter regras próprias). Sem essa marca, todas as empresas compartilham a mesma configuração.

### Combos

- **Descrição da Loja** — escolhe a empresa/loja cujas configurações estão sendo editadas. As opções vêm do cadastro de Empresas.

---

## 🗂️ Aba `Cabeçalho` — Características

Controla o que aparece e o que pode ser editado no **cabeçalho** do movimento (numeração, série, modo de edição).

### Checkboxes

- **Não permitir consumidor** — bloqueia salvar o movimento se a pessoa for o **Consumidor Padrão**. Use em Tipos que exigem cliente identificado (ex.: vendas para empresas).
  > ⚠️ **Atenção.** Bloqueio é validado ao salvar — mensagem do tipo "Não permite consumidor padrão" aparece e impede gravação.

- **Não permitir sem CPF** — bloqueia salvar com pessoa **sem CPF/CNPJ**. Combina com a regra acima para forçar identificação completa.

### Combos

- **Numeração** — define a edição do campo `Número do Documento` no movimento:
  - `Mostra` (0) — número visível, não editável (gerado pelo sistema).
  - `Edita` (1) — número visível e editável manualmente.

- **Tipo de Sequência** — origem do número do documento:
  - `Automático` (0) — gerado pelo Sol.NET a partir da tabela interna de sequências.
  - `Manual` (1) — preenchido pelo usuário.

- **Série** — controla a edição do campo `Série`:
  - `Mostra` (0) — visível, não editável (vem do padrão do Tipo).
  - `Edita` (1) — editável manualmente no movimento.

- **Editar após salvar** — define o que **fica bloqueado para edição** após o movimento ser salvo:
  - `Padrão` (0) — nada é bloqueado.
  - `Não Editar - Tudo` (1) — bloqueia toda edição do movimento.
  - `Não Editar - Produtos` (2) — bloqueia só os itens.
  - `Não Editar - Pessoas` (3) — bloqueia só os campos de pessoa/vendedor.
  - `Não Editar - Produtos + Pessoas` (4) — bloqueia itens e pessoas.
  > ⚠️ **Atenção.** Esse trava é por Tipo. Em fluxos de Pedido → Venda, deixe `Pedido` em `Padrão` (precisa editar até finalizar) e `Venda` em `Não Editar - Tudo` ou `Não Editar - Produtos` (não deve permitir alteração após emissão fiscal).

---

## 🗂️ Aba `Cabeçalho` — Origem/Destino

Define a origem e o destino do movimento (Empresa × Empresa, Empresa × Pessoa) e os padrões aplicados.

### Checkboxes

- **Solicitar Descrição do consumidor** — exibe um diálogo pedindo a descrição (nome) do consumidor ao lançar o movimento, mesmo quando a pessoa é o Consumidor Padrão. Útil em NFC-e que precisa do nome no XML.

### Combos

- **Empresa/Filial — Padrão** (origem) — escolhe a empresa **origem** do movimento. As opções vêm do cadastro de Empresas.

- **Empresa/Filial — Padrão** (destino) — escolhe a empresa **destino** do movimento. Opções idênticas; usada em transferências entre filiais.

- **Empresa X Empresa** — regra de validação entre origem e destino quando ambos são empresas:
  - `Destino Igual Origem` (0) — destino tem que ser a mesma empresa da origem (operações internas).
  - `Destino Diferente Origem` (1) — destino tem que ser empresa diferente (transferências).
  > ⚠️ **Atenção.** Marcar errado trava a gravação do movimento — "Destino Igual Origem" / "Destino Diferente Origem" são mensagens de validação ao salvar.

---

## 🗂️ Aba `Cabeçalho` — Datas

Configura as **quatro datas** que o movimento pode carregar — Emissão, Entrada/Saída (E/S) e duas datas opcionais — e a origem do valor padrão de cada uma.

### Combos de visibilidade (aplicam-se a cada data)

Cada uma das datas tem um combo `Mostra` / `Edita` / `Invisível`:

- **Emissão** — controla o campo `DT_EMISSAO`.
- **Entrada e Saída** — controla o campo `DT_ES`.
- **Opcional 1** — primeira data opcional (label customizável pelo Tipo, ex.: "Vencimento").
- **Opcional 2** — segunda data opcional.

Para cada combo:
- `Mostra` (0) — visível, não editável.
- `Edita` (1) — visível e editável.
- `Invisível` (2) — não aparece no formulário.

### Combos de valor inicial (origem da data padrão)

- **Padrão (Entrada e Saída)** — origem inicial de `DT_ES`:
  - `Emissão` (1) — copia da data de emissão.
  - `Sistema` (2) — usa a data atual do sistema.

- **Padrão (Opcional 1)** / **Padrão (Opcional 2)** — origem inicial das datas opcionais:
  - `Nenhum` (0) — começa em branco.
  - `Emissão` (1) — copia da emissão.
  - `Sistema` (2) — usa data atual.

---

## 🗂️ Aba `Cabeçalho` — Funcionários

Configura os três slots de funcionário/vendedor que o movimento pode carregar e como o sistema preenche/exige cada um.

### Checkboxes

- **Funcionário vínculo usuário** — preenche automaticamente o `Funcionário 1` com o vendedor vinculado ao usuário logado, sobrepondo o valor padrão do Tipo.
  > ⚠️ **Atenção.** Conflita com `Memorizar o vendedor` e com um `Funcionário Padrão` preenchido no Tipo — habilitar mais de um produz a validação "Funcionário inválido…" ao salvar. Veja [FAQ](faq.md) para detalhe.

- **Pedir pessoa ao salvar se for obrigatório** — exibe um diálogo perguntando o vendedor/funcionário ao gravar, caso o slot esteja vazio e seja obrigatório.

- **Memorizar o vendedor** — lembra o último vendedor escolhido na tela e reutiliza no próximo movimento do mesmo Tipo. Útil em PDV para evitar redigitar o vendedor a cada venda.

### Combos

- **Tipo Pessoa** (slots 1, 2 e 3) — filtra quais tipos de pessoa podem preencher cada slot:
  - `Todos` (-1) — qualquer pessoa.
  - `Cliente` (0).
  - `Fornecedor` (1).
  - `Fabricante` (2).
  - `Funcionário` (3).
  - `Transportadora` (4).
  - `Contador` (5).

> ⚠️ **Atenção.** Em Tipos de Compras, o slot 1 costuma exigir `Fornecedor`; em Tipos de Vendas, `Funcionário` (vendedor) ou `Cliente`. Misturar produz mensagens "Pessoa inválida para este Tipo de Movimento".

---

## 🗂️ Aba `Cabeçalho` — Fiscal

Concentra todas as regras fiscais — manter alíquotas após edição, região ICMS, ICMS ST manual, finalidade NF-e, CST da última compra, DIFAL.

### Checkboxes

- **Manter (Tudo)** — preserva manualmente os valores fiscais já digitados no movimento, mesmo quando o sistema recalcularia automaticamente (ao trocar de Tipo, ao adicionar item, etc.).
  > ⚠️ **Atenção.** Quando marcado, **desativa** o recálculo automático de impostos. Use apenas em Tipos cujo movimento sempre é digitado manualmente pelo contador (operações atípicas, NFs de ajuste).

- **Manter (IBS/CBS)** — versão restrita do anterior, aplicada **apenas** aos tributos `IBS`/`CBS` da Reforma Tributária. Mantém o que o usuário digitou de IBS/CBS mesmo quando o cálculo automático rodaria.

- **Executar Região** — aplica a regra de Região ICMS configurada para o Tipo (sintetiza CST/CFOP por destino).

- **Não executar Região na Venda** — exceção: em operações de venda, **ignora** a Região (cálculo manual).

- **ICMS/ICMS ST Manual (Desativar Cálculo Automático)** — desliga o cálculo automático de ICMS e ICMS ST. Os valores precisam vir digitados ou vir da NF-e de origem (compras).
  > ⚠️ **Atenção.** Mantém o digitado mesmo após edição. Use em Tipos `COMPRA À VISTA` quando o XML de entrada já traz ICMS calculado pelo fornecedor.

- **Liberar Cálculo ICMS/ICMS ST/IPI Livre** — permite o usuário **preencher os impostos pelo totalizador** do movimento; o sistema rateia automaticamente o valor digitado entre os itens. Útil em notas onde o contador prefere ajustar o total fechado em vez de item a item.

- **Limitar Crédito de Entrada pelo Crédito Outorgado** — em regimes que concedem Crédito Outorgado (substituição parcial do ICMS), aplica o teto desse regime no crédito de ICMS de entrada — impedindo apropriação maior que a permitida.

- **(X) NF-e Vincular Documento de Arrecadação (DAR/GNRE)** — vincula no XML da NF-e o documento de arrecadação (DAR ou GNRE) referente à operação. Específico de operações que envolvem recolhimento prévio do imposto (ICMS antecipado, DIFAL recolhido na origem etc.).

- **Pegar CST ICMS da Ultima Compra** — em movimentos de **devolução**, busca o CST ICMS do produto na **última NF-e de compra** e usa esse CST na devolução (mantém coerência de classificação fiscal entre a entrada original e o retorno).

- **Pedir CPF ao Enviar NF se Consumidor Padrão** — bloqueia o envio da NF-e (ao finalizar) se a pessoa for o Consumidor Padrão sem CPF, exibindo diálogo para o operador informar o CPF.

- **ICMS Normal completo da Nota** — destaca o ICMS Normal no rodapé da NF (campo totalizador), em vez de apenas item-a-item.

- **Destacar ICMS ST Retido Anteriormente** — destaca no XML/DANFE o ICMS ST que já foi retido na cadeia anterior (compras de produtos com ST já paga pelo fornecedor).

- **Agrupar - Informações Adicionais por Vendedor** — quando agrupa movimentos em uma só NF, agrupa também o texto de Informações Adicionais por vendedor, em vez de concatenar tudo.

### Combos

- **Estado** — escopo geográfico do Tipo:
  - `Dentro` (0) — operações dentro do mesmo estado da empresa.
  - `Fora` (1) — operações interestaduais.
  - `Exterior` (2) — operações com exterior.

- **Operação Região ICMS** — escolhe qual conjunto de Regiões ICMS o Tipo aplica:
  - vazio — usa a Região ICMS Padrão.
  - `Venda` (0) — usa Região configurada para Venda.
  - `Devolução` (1) — usa Região configurada para Devolução.
  - `Transferência` (2) — usa Região configurada para Transferência.
  - `Compra` (3) — usa Região configurada para Compra.
  - `Regra 5` (4) a `Regra 10` (10) — slots de regra customizada, mapeáveis à necessidade da empresa.

- **Modelo de Documento Padrão** — modelo fiscal emitido (NF-e, NFC-e, NFS-e, CT-e, Cupom Fiscal). As opções vêm do cadastro de Modelos de Documento Fiscal.

- **Situação** — status fiscal padrão do documento (Autorizado, Cancelado, Inutilizado etc.). Configura o estado inicial em que o movimento entra na base.

- **Finalidade da NF-e Padrão** — campo `finNFe` do XML:
  - `Normal` (0) — emissão normal.
  - `Complementar` (1) — complemento de NF-e anterior.
  - `Ajuste` (2) — ajuste tributário.
  - `Devolução` (3) — devolução/retorno.

- **ICMS ST - Cálculo Automático Compra** — método de cálculo automático de ICMS ST com base no MVA do NCM do produto (aplica-se a operações de compra):
  - `(Todos Itens) Calcular de Estimativa Simplificada (Obsoleto)` (2) — método legado, **não usar em novas configurações**.
  - `(CST 060) Substituir ST do Item pelo MVA Produto` (3) — substitui o ICMS ST do item pelo valor calculado via MVA do NCM (vigência CST 060).
  - `(CST 060) Calcular ST do Item pelo MVA Produto ZERO` (4) — calcula com MVA, mas zera o resultado no item (registro fiscal sem impacto no total).

- **DIFAL - ICMS Interestadual** — comportamento do DIFAL em operações interestaduais:
  - `Não` (1) — não destaca DIFAL.
  - `Destacar somente Aliq. e Base` (2) — destaca alíquota e base sem calcular partilha.

---

## 🗂️ Aba `Cabeçalho` — Detalhes PDV

Configurações específicas da experiência PDV (frente de caixa).

### Checkboxes

- **Usar Troco** — habilita a tela de cálculo de troco no PDV ao finalizar a venda em dinheiro.
- **Usar Entrega** — habilita o fluxo de entrega no PDV (registra endereço de entrega).
- **Usar Taxa (Frete)** — habilita a digitação de taxa de frete no PDV.

---

## 🗂️ Aba `Cabeçalho` — Mobile

Configurações para movimentos lançados pelo aplicativo Mobile (coletor, força de vendas).

### Checkboxes

- **É e-Commerce** — marca o Tipo como vinculado a operações de e-Commerce (integração com loja virtual).
- **Não exibir botão de exclusão** — esconde o botão de excluir movimento no Mobile (impede que o vendedor delete movimentos em campo).

### Combos

- **Usuário** — usuário do cadastro de Usuários e-Commerce associado a este Tipo (usado pela integração de e-Commerce para identificar quem opera o movimento). As opções vêm carregadas em runtime do cadastro de usuários — escolha o usuário correspondente.

---

## 🗂️ Aba `Itens` — Principal

Maior aba do formulário em número de flags. Controla o que o movimento aceita **por linha de produto/serviço** — campos visíveis, regras de preço, conferência, rastreio, descontos.

### Checkboxes

- **Limpar Valores ao Importar Itens** — ao trazer itens de outro movimento referenciado, zera os valores monetários e recalcula pela tabela do Tipo atual.

- **Colocar Valor Item se Valor Zero (0)** — se o preço do item vier zerado, força o sistema a buscar o preço da Tabela de Preço (em vez de aceitar zero).

- **Permitir Salvar Movimento Sem Item** — autoriza salvar um movimento sem nenhuma linha. Útil para Tipos de adiantamento financeiro sem contrapartida em produto.
  > ⚠️ **Atenção.** Tipos que geram NF-e **não** podem ser salvos sem item — a SEFAZ rejeita. Marque essa flag só em Tipos não-fiscais.

- **Permitir Mov./Item com Valor Zero (0)** — autoriza linhas com valor zero. Necessário para bonificações, brindes e amostras grátis.
  > ⚠️ **Atenção.** Em vendas fiscais, item zerado pode disparar alerta de auditoria. Configure no Tipo correto (`BONIFICAÇÃO`, `AMOSTRA`) — não no `VENDA BALCÃO` padrão.

- **Diminuir Desconto no Valor Unitário** — quando o usuário aplica desconto na linha, o sistema **reduz o preço unitário** correspondentemente em vez de manter o desconto como campo separado.

- **Utilizar Desagregação** — habilita a desagregação de itens (produto composto se quebra em componentes ao lançar).

- **Gerar Cashback PDV** — itens deste Tipo geram pontos de cashback dentro da aplicação PDV.

- **Salvar apenas Financeiro ao lançar** — ao importar XML de NF-e de compra, salva **apenas** os financeiros gerados (contas a pagar), sem trazer os itens para o estoque. Usado em integrações onde estoque é controlado em outro sistema.

- **Inserir rastro automaticamente** — gera registro de rastreabilidade (lote/série) automaticamente para os itens, sem pedir ao usuário.

- **Usar Conferência de itens** — habilita o fluxo de conferência (bipar produtos antes de finalizar) nos movimentos deste Tipo.

- **Validar Controle de Vencimento** — exige que itens com controle de vencimento tenham data de validade preenchida.

- **Criar conferência de pedido** — ao finalizar o movimento, cria registro de conferência (útil para separação em logística).

- **Usar Conferência externa** — sincroniza conferência com sistema externo (coletor de dados de terceiro).

- **Calcular em Compras/Outros** — calcula automaticamente Tabela de Preço também em movimentos de **Compras** e **Outros** (não só em Vendas).

- **Recalcular Automaticamente** — força o recálculo de preços de tabela a cada alteração da linha (pessoa, quantidade, condição de pagamento).

- **Somente se Alterar a Pessoa** — restringe o recálculo automático: só recalcula quando a pessoa do movimento muda.

### Combos

- **Tipo de Item** — tipos de linha permitidos no movimento:
  - `Somente Produto` (0) — só linhas de produto.
  - `Somente Serviço` (1) — só linhas de serviço.
  - `Ambos` (2) — produtos e serviços misturados.
  > ⚠️ **Atenção.** O valor configurado precisa casar com o `Modelo de Documento` na aba Fiscal. NF-e (modelo 55) só aceita produto; NFS-e só aceita serviço; nota mista é caso excepcional.

- **Editar (Produto)** — visibilidade do campo `Preço do Produto`:
  - `Mostra` (0) — visível, não editável.
  - `Edita` (1) — editável.
  - `Invisível` (2) — escondido.

- **Editar (Serviço)** — idem para preço de serviço.

- **Desconto (Produto)** / **Desconto (Serviço)** — modo de desconto aceito por linha:
  - `Não` (0) — não permite desconto.
  - `Ambos` (1) — aceita valor e percentual.
  - `Valor` (2) — só valor absoluto.
  - `Percentual` (3) — só percentual.

- **Acréscimos (Produto)** / **Acréscimos (Serviço)** — idem para acréscimos.

- **Pesquisar só por:** — restringe a pesquisa de produto na linha a um **único** campo (acelera PDV de alta rotatividade):
  - `Código Interno` (0) — pesquisa só pelo código interno do Sol.NET.
  - `Código de Barras` (1) — só por código de barras (EAN/UPC).
  - `Código do Fabricante` (2).
  - `Código do Fornecedor` (3).
  - `Código do Produto` (4) — código primário do cadastro.

- **Tipo de Pontos** — comportamento de pontuação (fidelidade):
  - `Gerar Pontos` (1) — itens deste Tipo geram pontos.
  - `Usar Pontos` (2) — itens consomem pontos acumulados.

- **Duplicar e Clonar Movimento** — comportamento dos impostos ao clonar/duplicar:
  - `Limpar Imposto e Transferir para o Item` (1) — zera impostos no cabeçalho e força recálculo por item.
  - `Limpar Imposto no Item` (2) — zera os impostos da linha (recálculo total).
  > ⚠️ **Atenção.** Essa regra entra em ação no fluxo "Mudar" (`F7`) quando configurado como `DUPLICAR` (ver aba Finalizar). Em produção, prefira `Limpar Imposto no Item` quando o Tipo origem e destino têm tributação diferente.

- **Obrigatório** — força regra especial por linha:
  - `Medicamento` (1) — exige preencher campos regulatórios de medicamento (SNGPC).


---

## 🗂️ Aba `Itens` — Tabela de Preço

Vincula as Tabelas de Preço aceitas pelo Tipo. O grid e os botões ficam fora do escopo desta página (vide [Documentação principal](documentacao_tipos_de_movimento.md)).

### Combos

- **Tabela de Preço** — escolhe a Tabela de Preço padrão (vem do cadastro `Tabela de Preço`, código `27`).

- **Descrição** — refinamento da Tabela por empresa quando o Sol.NET está em modo multi-empresa.

---

## 🗂️ Aba `Itens` — Estoque

Define qual Transação de Estoque, Local padrão e comportamento de saldo o movimento aplica.

### Checkboxes

- **Baixar Quantidade de Promoção** — em promoções com **limite de quantidade** (ex.: "promocional para os primeiros 50 itens vendidos"), ao baixar o estoque do item por este Tipo, decrementa o contador `n` da promoção. Sem essa flag, o estoque baixa mas o contador da promoção não anda — risco de a promoção continuar valendo após exceder o limite configurado.
  > ⚠️ **Atenção.** Exige `Transação de Estoque` preenchida (validação ao salvar). Marque em Tipos de venda que devem efetivamente consumir o saldo da promoção.

### Combos

- **Transação** — Transação de Estoque que define o efeito de cada linha no saldo (vem do cadastro `Transações de Estoque`, código `33`).
  > ⚠️ **Atenção.** Tipos que movimentam estoque **exigem** Transação preenchida. A validação "Obrigatório Transação de Estoque!" trava o registro sem isso.

- **Local de Estoque — Padrão** (origem) — Local de Estoque default das linhas (vem do cadastro `Locais de Estoque`, código `28`).

- **Baixar Estoque Sem Saldo** — comportamento quando a linha pediria mais do que o saldo disponível:
  - `Sim` (0) — permite baixa, saldo fica negativo.
  - `Bloquear` (1) — impede gravar.
  - `Com Liberação` (2) — pede liberação por usuário com permissão.
  > ⚠️ **Atenção.** Em vendas fiscais, `Sim` (saldo negativo) é fonte comum de inconsistência inventário × SPED. Use `Bloquear` ou `Com Liberação` em Tipos críticos.

- **Local de Estoque — Destino** — Local destino em movimentos de transferência.

- **Descrição** (multi-empresa) — empresa para a qual a configuração de local aplica.

- **Local Estoque** (multi-empresa) — Local específico da empresa escolhida acima.

---

## 🗂️ Aba `Itens` — Quantidade

Conversão de unidades, separação por linha e comissão.

### Checkboxes

- **Mostrar campos (Conversão)** — exibe na linha os campos auxiliares de conversão de unidade (Quantidade Caixa, Quantidade Unidade).

- **Mostrar campo (Vl. Unitário Caixa)** — exibe o campo de preço por caixa em paralelo ao preço unitário.

- **SEPARAR ITENS DO MOVIMENTO (Individual)** — não agrupa linhas idênticas; cada inserção gera uma linha separada (mesmo que o produto seja o mesmo).
  > ⚠️ **Atenção.** Importante em movimentos de produção e em rastreabilidade onde cada unidade carrega lote/série distinto. Em vendas comuns, deixe desmarcado (o sistema agrupa linhas iguais por padrão).

- **Usar retirada em Movimento Item** — habilita o campo "Quantidade Retirada" na linha (parcial: parte do item fica retido, parte sai).

- **Quantidade de Retirada Iniciar com Zero (0,000)** — quando o anterior está marcado, força o campo a começar zerado em vez de copiar a quantidade total.

- **Gerar Comissão** — itens deste Tipo geram comissão para o vendedor segundo as regras do cadastro de Cargo/Comissão.
  > ⚠️ **Atenção.** Devoluções precisam **desmarcar** essa flag (ou usar Tipo dedicado para devolução) — senão a comissão da venda original é paga e a devolução não estorna.

---

## 🗂️ Aba `Valores` — Produto

Modo de aplicação de descontos, acréscimos, seguro, frete e dos quatro campos genéricos de valor.

### Combos

- **Desconto** / **Acréscimos** / **Seguro** — modo de aplicação no cabeçalho (rateado nas linhas):
  - `Não` (0) — campo desabilitado.
  - `Ambos` (1) — valor ou percentual.
  - `Valor` (2) — só valor absoluto.
  - `Percentual` (3) — só percentual.

- **Tipo de Valor (1 a 4)** — modo dos quatro campos genéricos de valor configuráveis pelo Tipo:
  - `Ambos` (0) — aceita valor e percentual.
  - `Valor` (1) — só valor.
  - `Percentual` (2) — só percentual.

- **Aplicar sobre (1 a 4)** — escopo do cálculo de cada um dos quatro campos:
  - `Ambos` (0) — produtos e serviços.
  - `Produtos` (1) — só produtos.
  - `Serviços` (2) — só serviços.

- **Tipo de Frete** — escolhe a regra de frete padrão (vem de um cadastro auxiliar).

- **Operação (Frete)** — como o frete é calculado:
  - `Percentual da Venda` (0).
  - `Preço Quilo` (1).
  - `Fixo` (2).
  - `Valor venda menor que` (3) — frete só aplica quando a venda fica abaixo de um valor configurável.

---

## 🗂️ Aba `Valores` — Serviços

Idêntica à aba `Valores Produto` na lógica, com flags específicas de serviço.

### Checkboxes

- **Frete Serviço fora do Movimento** — frete de serviço lançado em movimento à parte, não embutido nas linhas.

- **Permitir Movimentos Em Aberto** — autoriza Tipos de precificação a deixar movimentos "em aberto" (sem fechar) — comum em fluxos de contrato/recorrência.

- **Bloquear atualização de custo** — desativa qualquer atualização automática de custo de produto/serviço pelos movimentos deste Tipo.
  > ⚠️ **Atenção.** Use em Tipos de movimentação interna que não devem mexer no custo médio (ajuste de estoque, transferência sem efeito de custo).

### Combos

- **Desconto** / **Acréscimos** — idênticos aos da aba Produto.

- **Atualizar Custo do Produto ao Finalizar (Movimentos de Entrada)** — método de atualização do custo:
  - `Normal - Fecha ao Salvar` (1) — calcula custo médio padrão e fecha a tela ao salvar.
  - `Sem Fechar a Tela ao Salvar` (2) — atualiza custo mas mantém o movimento aberto para conferência.
  - Outras opções menos usadas — confirme com o contador antes de escolher.
  > ⚠️ **Atenção.** Funciona **apenas em Tipos de Compras/Outros** (entradas). Em Vendas, este combo é ignorado — não atualiza custo de venda no Sol.NET.

---

## 🗂️ Aba `Financeiro`

Define se o Tipo gera conta a pagar/receber e quais datas/regras se aplicam.

### Checkboxes

- **Previsão** — o financeiro gerado nasce com status `Previsão` em vez de `Em Aberto`. Útil para Tipos de previsão (orçamento → pedido → venda) onde a conta só vira realidade após confirmação.

- **Fazer Parcelas Manual** — habilita o "Gerador de Parcelas Manual" no movimento (cria parcelas linha a linha em vez de pela Condição de Pagamento).

- **Estornar Mov. c/ Financeiro Executado** — ao estornar/excluir um movimento, **permite** o estorno mesmo quando o financeiro já está executado (quitado/baixado).
  > ⚠️ **Atenção.** Esta opção **só é permitida em Tipos de Compras/Outros**. Em Tipos de Venda, marcar dispara validação "Não Estornar Financeiro só é permitido em Tipos de Compras/Outros" e impede salvar.

- **Mostrar Rentabilidade nas notificações** — exibe lucro/rentabilidade do movimento nos toasts/alertas pós-finalização.

- **Aplicar Pessoa Rateio** — quando a pessoa do movimento tem uma **configuração de Pessoa Rateio** cadastrada no próprio cadastro de Pessoas, o sistema usa essa regra ao gerar o rateio das contas. Desmarcado, ignora essa configuração e aplica o rateio padrão do Tipo.

### Combos

- **Vencimento a Partir** — qual data do movimento é usada como `Vencimento` da conta:
  - `Emissão` (0).
  - `E/S` (1) — Entrada/Saída.
  - `Opcional 1` (2).
  - `Opcional 2` (3).
  - `Sistema` (4) — data atual no momento da geração.

- **Data de Emissão (financeiro)** — qual data do movimento é usada como `Emissão` da conta. Mesmas opções acima.

---

## 🗂️ Aba `Financeiro` — Contas PR

Padrões do título financeiro gerado (Condição, Portador, Tipo de Documento).

### Checkboxes

- **Não agrupar no Financeiro Axe** — desabilita o agrupamento automático no fluxo `Pagar/Receber` (cada movimento gera contas separadas).

- **Não agrupar no Contas a Receber/Quitação** — desabilita o agrupamento na tela de Quitação (parcelas de movimentos diferentes não se misturam).

### Combos

- **Condição** — Condição de Pagamento padrão (vem do cadastro `Condições de Pagamento`, código `8`).

- **Portador - Padrão** — Portador padrão (vem do cadastro `Portadores`, código `12`).

- **Tipo de Documento Padrão** — Tipo de Documento padrão (vem do cadastro `Tipos de Contas PR`, código `82`).

---

## 🗂️ Aba `Financeiro` — Portador

### Combos

- **Portador** — Portador específico que o Tipo aceita (filtra os do cadastro de Portadores).
- **Descrição** (multi-empresa) — empresa associada ao portador acima.

---

## 🗂️ Aba `Finalizar`

Define o que acontece quando o usuário finaliza o movimento (imprime, envia DF-e, abre quitação, muda para outro Tipo).

### Checkboxes

- **Imprimir se recebido** — imprime o documento apenas se o recebimento (quitação) já estiver registrado.

- **DANFE se recebido** — envia/imprime DANFE apenas após recebimento confirmado.

- **Imprimir ao finalizar** — chama o componente de impressão automaticamente assim que o movimento é finalizado.

- **DANFE ao finalizar** — chama o componente DF-e automaticamente após a finalização (sem esperar pagamento).

- **Pagamento ao Finalizar** — abre a tela de quitação automaticamente após salvar.

- **Clicar em OK Automaticamente** — confirma o diálogo de "Mudar" sem perguntar (quando há mudança configurada).

- **Manter Financeiro (Atenção)** — ao mudar (`F7`) para outro Tipo, preserva o financeiro já gerado em vez de regerá-lo.
  > ⚠️ **Atenção.** Mantém o financeiro como está. Se o Tipo destino tem regras de financeiro diferentes, podem surgir contas inconsistentes — alinhe com suporte antes de marcar.

- **Manter Estoque (Atenção)** — idem para movimentações de estoque.
  > ⚠️ **Atenção.** Bloqueia o estorno da Transação de Estoque original e a aplicação da nova. Use só quando origem e destino têm Transação compatível.

- **Manter Tudo 1 de 2 (Atenção)** / **Manter Tudo 2 de 2 (Atenção)** — bloqueia recriação de **tudo** ao mudar de Tipo (financeiro + estoque + fiscal + agrupamento). São duas flags porque a regra "tudo" cobre dois grupos de tabelas; em produção, marque ambas ou nenhuma.
  > ⚠️ **Atenção.** Funciona como "freeze" do movimento na transição. Combina geralmente com `Pedido → Venda` em fluxos onde só o Tipo muda mas as condições já estavam acertadas.

- **Manter Data Vencimento (Atenção)** — ao mudar, preserva a data de vencimento das contas geradas.

- **Manter Local de Estoque** — ao mudar, preserva o Local de Estoque original.

- **Finalizar automaticamente** — finaliza o movimento assim que é salvo (sem clicar em Finalizar).
  > ⚠️ **Atenção.** Em Tipos fiscais, isso aciona NF-e imediatamente após salvar. Use só quando há certeza de que o lançamento já está revisado — não há rollback após finalização fiscal.

### Combos

- **Operação (Inverter Empresa)** — comportamento da empresa origem/destino ao mudar:
  - `Inverter Empresas (Dest - Origem)` (0) — troca origem e destino no novo movimento.
  - `Manter Empresa Origem Tipo Mov.` (1 ou 2) — mantém origem.

- **Ao mudar** — modo de mudança via `F7`:
  - `TRANSFORMA EM` (0) — **o mesmo movimento muda de Tipo** (o registro continua existindo; agora ele simplesmente é do Tipo destino). Não gera segundo registro.
  - `DUPLICAR` (1) — gera **novo** movimento com o Tipo destino; o original fica em status `VINCULADO`, preservado para histórico.
  > ⚠️ **Atenção.** `DUPLICAR` é o modo padrão do ciclo `ORÇAMENTO → PEDIDO → VENDA` — permite manter o histórico do orçamento mesmo após virar venda. `TRANSFORMA EM` é não-destrutivo (o movimento permanece, só muda de Tipo), mas perde a noção de "etapa anterior" porque só sobra um registro. Veja [Documentação principal](documentacao_tipos_de_movimento.md) para o detalhe.

- **Tipo Movimento** (faturar 1 e 2) — em qual operador o Tipo destino aparece para escolha do usuário:
  - `VENDA` (0).
  - `COMPRA` (1).
  - `OUTROS` (2).

- **Comportamento** (ao mudar) — o que acontece com o movimento destino:
  - `Salvar` (0) — só salva, fica em edição.
  - `Finalizar automático` (1) — finaliza direto.
  - `Ficar em modo Edição` (2) — abre o destino em edição para o usuário ajustar.

---

## 🗂️ Aba `Relatórios`

### Combos

- **Opções** — comportamento de impressão no finalizar:
  - `ESCOLHER RELATÓRIO` (0) — diálogo pedindo qual relatório imprimir.
  - `IMPRIMIR SEQUENCIAL` (1) — imprime na sequência configurada sem perguntar.

---

## 🗂️ Aba `Promocional`

Configurações de campanhas promocionais vinculadas ao Tipo.

### Checkboxes

- **Validar Cupom Promocional** — exige cupom promocional válido (não expirado, não usado) para finalizar movimentos deste Tipo.

### Combos

- **Opção** — quando imprimir o cupom:
  - `Imprimir ao finalizar` (1) — imprime junto com o documento principal.
  - `Após finalizar` (2) — pergunta após finalização.

---

## 🗂️ Aba `Campos Complementares`

Flags variadas: crédito de devolução, notificações, chamadas, financeiro aberto.

### Checkboxes

- **Consumo (Energia, Água e Gás / Transporte / Comunicação)** — marca o Tipo como movimento de medição de consumo (faturas de utilidades — energia, água, gás, transporte, comunicação).

- **Permitir Financeiro Aberto** — permite que o movimento tenha financeiro em aberto sem bloquear novos lançamentos.

- **Amarrar Pessoa** — em devoluções com referência a outro movimento, exige que a pessoa do movimento original seja **a mesma** da devolução.
  > ⚠️ **Atenção.** Travamento útil para impedir devolução em conta errada (cliente A devolvendo nota de cliente B). Habilite em todos os Tipos de devolução.

- **Notificar Créditos** — exibe notificação ao operador quando a pessoa tem crédito disponível (de devolução anterior) aplicável.

- **(PDV) Quitar Créditos Automaticamente** — no PDV, abate automaticamente o crédito disponível da pessoa na próxima compra.

- **Funcionário - Chamadas** — habilita o módulo de Chamadas vinculado ao Tipo (atendimento sob demanda, OS por chamada).

- **Criar Chamada de Prazo** — gera automaticamente uma chamada de acompanhamento (prazo) ao finalizar o movimento.

### Combos

- **Tipo Devolução** — comportamento do crédito de devolução:
  - `GERAR CREDITO` (0) — gera crédito a favor da pessoa.
  - `USAR CREDITO` (1) — abate crédito existente.
  - `USAR CASHBACK` (2) — abate cashback acumulado.
  - `USAR AMBOS` (3) — abate crédito + cashback.
  > ⚠️ **Atenção.** Combina com `Devolução` (aba Dados Cadastrais). Em PDV é comum `USAR AMBOS` para abater na próxima compra. Em retaguarda, costuma-se `GERAR CREDITO` (cliente pega o crédito para uso futuro).

- **Tipo Gerar Crédito** — escopo do crédito gerado:
  - `PRODUTOS` (0) — gera crédito por produto (qualquer item dispara).
  - `ITENS NO MOVIMENTO` (1) — só os itens efetivamente referenciados no movimento.

- **Permitir Tipo Movimento** — quais Tipos de Movimento podem ser **referenciados** quando o movimento é uma devolução:
  - `VENDA` (0).
  - `VENDA/OUTROS` (1).
  - `VENDA/COMPRA/OUTROS` (2) — todos.
  - `COMPRA` (3).
  - `COMPRA/OUTROS` (4).
  - Variações até `(7)` para combinações raras.

- **Status Chamada** — status padrão da chamada criada (vem do cadastro de Chamadas).

- **Tipo Atendimento** — tipo de atendimento padrão (vem do cadastro de Tipos de Atendimento).

---

## 🗂️ Aba `Outras Operações`

Flags de comportamento especial — OS, K235, produção, contas vencidas.

### Checkboxes

- **É OS** — marca o Tipo como Ordem de Serviço (habilita campos de OS no formulário do movimento).

- **É OS Requisição** — variante: OS de requisição (entrada de pedido de serviço, antes da execução). De acordo com o hint do `OS (Sem Serviços)`, `É OS` proíbe inserir serviços e `É OS Requisição` permite — escolha um, não os dois.

- **OS (Sem Serviços)** — OS que **não** carrega serviços (só produtos consumidos). Útil em manutenção corretiva.

- **Consumo de Insumos (Bloco K235 SPED Fiscal)** — itens consumidos são reportados no Bloco K235 (Insumos Consumidos) do SPED Fiscal.
  > ⚠️ **Atenção.** Marque em Tipos de produção/ordem de serviço industrial. Em vendas comuns, deixe desmarcado (movimento não vira K235).

- **Produção** — classifica o Tipo como movimento de produção. Habilita campos específicos (ficha técnica, perdas, produto acabado) e integra com a tela `Produção de Produtos` (código `144`).
  > ⚠️ **Atenção.** Tipos de produção têm dois lados: entrada do acabado e saída dos ingredientes — ambos precisam ter `Produção` marcado para o fluxo automático da tela `144` funcionar.

- **Detalhar Contas Vencidas** — ao lançar movimento para uma pessoa com pendências, exibe a lista detalhada de contas em aberto e vencidas dela (lembrete de inadimplência), permitindo ao operador conferir antes de seguir.

---

## 🗂️ Aba `Empresa/Produto`

Permite financeiro separado quando o Tipo opera com produtos e serviços ao mesmo tempo.

### Checkboxes

- **Ativar Financeiro Separado** — em notas mistas (produto + serviço), **diminui** do financeiro principal o valor de impostos referente à parte de serviço e **gera um título adicional** correspondente a essa diferença. Resultado: dois títulos no contas a receber/pagar — o "principal" com valor já reduzido, e o "extra" do recolhimento do imposto de serviço.

### Combos

- **Tipo de Documento Padrão** (variantes 2 e 3) — Tipos de Documento alternativos usados quando o `Financeiro Separado` está ativo (um para produtos, outro para serviços/crédito).

---

## 🗂️ Aba `Serviços`

### Checkboxes

- **Calcular Vl. ISS Retido Antecipadamente** — calcula o ISS retido **na geração do título**, em vez de só na quitação. Usado em prefeituras que exigem retenção antecipada.

### Combos

- **Descrição** (multi-empresa) — empresa associada à configuração de serviços.

---

## 🗂️ Aba `Série`

### Combos

- **Descrição** (multi-empresa) — escolhe a empresa cuja Série padrão está sendo editada (vem do cadastro de Séries Fiscais).

---

## 🗂️ Aba `Sistema`

### Checkboxes

- **Produto Agrotóxico** — marca o Tipo como vinculado ao módulo Agronômico, habilitando a integração com `Receituário Agronômico` (código `142`) e regras de rastreabilidade de agrotóxico.

---

## ⚠️ Limites desta documentação

- **Cobre apenas** os controles do tipo *checkbox* e *combo* do formulário. Caixas de texto, grids, lookups vinculados a outros cadastros, sub-painéis com botões e abas de relatório ficam descritos na [Documentação principal](documentacao_tipos_de_movimento.md).
- **Controles ocultos** (escondidos por padrão na tela, como o antigo `Código retornado`) foram **omitidos** porque o usuário não os enxerga em uso comum. Se algum controle aparecer em instalação customizada e você precisar do significado, consulte o suporte.
- Valores codificados (números entre parênteses como `(0)`, `(1)`...) foram conferidos no formulário e na tabela `CONFIG_TIPOS_MOVIMENTO` em maio de 2026. Releases posteriores podem alterar opções ou renomear flags — releia o `.dfm`/`Config_Tipos_Movimento.cs` ou consulte o suporte antes de assumir significado em versões antigas/novas.
- Para mensagens de validação ao salvar ("Obrigatório…", "Não permitido…", "Tipo Emissão Terceiro…"), o [FAQ](faq.md) lista cada uma com a aba/sub-aba onde resolver.
- Combos cujas **opções vêm de outro cadastro** (Tabelas de Preço, Portadores, Empresas, Locais, Tipos de Documento, Usuários e-Commerce etc.) não têm valores listados aqui — as opções variam por instalação. Use o cadastro vinculado para entender o que cada opção representa.

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Equipe de Suporte / Consultores de Implantação Sol.NET
