# 📄 Importar XML NF-e - Sol.NET

## 🎯 Visão Geral

A tela **Importar XML NF-e** é o ponto onde o Sol.NET **lê o arquivo `.xml` de uma NF-e** (emitida por um fornecedor ou pela própria empresa) e o transforma em um movimento de entrada — ou registra a saída correspondente, no caso de NF-e própria.

A tela faz três coisas principais:

1. **Carregar o XML** e extrair automaticamente cabeçalho, fornecedor, itens, tributos e duplicatas.
2. **Vincular cada item do XML a um produto do cadastro** — manualmente, com duplo clique, ou automaticamente pelo código do fornecedor.
3. **Lançar a NF-e na Movimentação** como uma entrada concreta (com seus três modos: normal, parcial ou própria), gerando estoque, financeiro e demais reflexos.

A tela também mantém o **histórico de todos os XMLs já carregados**, com filtros por loja, fornecedor, período, situação e conferência — funcionando como um diário de entradas a partir de NF-e.

### Para que serve

- ✅ Lançar a entrada de mercadoria de fornecedor a partir do XML, sem digitar nota manualmente
- ✅ Vincular produtos do XML ao cadastro de produtos (com criação rápida de produtos novos)
- ✅ Comparar o que o fornecedor enviou no XML com o que foi conferido fisicamente
- ✅ Imprimir o **DANFE** a partir do XML
- ✅ Lançar **parcialmente** uma NF-e quando apenas parte da mercadoria foi recebida
- ✅ Registrar a saída de uma NF-e **emitida pela própria empresa** que precisa virar movimento

### Situações comuns no dia a dia

- Mensagem `Chave de Acesso já Cadastrada` → a mesma NF-e já foi carregada antes; é preciso localizar o registro existente no grid em vez de carregar de novo.
- Mensagem `( ... ) NÃO É SUA EMPRESA` → o CNPJ do destinatário no XML não bate com nenhuma loja cadastrada; conferir se a NF-e foi emitida para o CNPJ correto.
- Item da nota fica sem vínculo no grid → ainda não há código de fornecedor cadastrado para esse produto; duplo clique no item resolve, vinculando ou cadastrando o produto.
- NF-e foi lançada mas o financeiro não apareceu → o XML pode não ter trazido as parcelas (NF-e à vista), ou as parcelas precisam ser conferidas na aba `Financeiro` antes do lançamento.

---

## 🚪 Como acessar

A tela é aberta pela pesquisa universal:

1. Pressione **F1** em qualquer ponto do Sol.NET.
2. Digite **`204`** (código da tela) ou parte do nome **Importar XML**.
3. Confirme para abrir a tela `Importar XML NF-e`.

A tela também é aberta **automaticamente a partir da Manifestação do Destinatário** quando o usuário escolhe lançar a entrada de uma NF-e baixada da SEFAZ — nesse caminho, a chave de acesso já vem preenchida.

---

## 🔍 Consulta de XMLs já importados

Ao abrir a tela, a primeira coisa que o usuário vê é o grid com os XMLs já carregados no Sol.NET. Os filtros ficam acima do grid, distribuídos em duas guias de pesquisa.

### Filtros principais (1ª guia)

| Filtro | O que faz |
|--------|-----------|
| `Descrição da Loja` | Limita o resultado a uma loja específica. Por padrão traz todas as lojas que o usuário tem acesso. |
| `Status` | `Edição` (importado mas ainda não lançado), `Finalizado` (pronto para lançar), `Importado` (já gerou movimento). |
| `Status Conferência` | `Não Conferido`, `Em Andamento`, `Finalizada Sem Divergência`, `Finalizada Com Divergência`. Veja o documento [Conferência de XML](documentacao_conferencia_xml.md). |
| `Campo a pesquisar` | Define o campo: `Razão/Fantasia`, `Pessoas`, `Série`, `Nº Documento`, `Chave de Acesso`, `Total`, `UF`. |
| `Condição` | Operador da busca: `Contém`, `Inicia Com`, `=`, `>`, `<`, `>=`, `<=`, `<>`, `Entre`, `Lista`, `Fora da Lista`. |
| `Data` | Critério temporal: `Emissão` (do XML) ou `Cadastro` (quando entrou no Sol.NET). |
| `Inicial` / `Final` | Intervalo de datas. |

### Filtros adicionais (2ª guia)

| Filtro | O que faz |
|--------|-----------|
| `Financeiro` | `Não Lançados` (XMLs sem duplicatas geradas) ou `Lançados`. |
| `Operações` | `Internas` (entradas) ou `Externas` (saídas / emissão própria). |

### O que o grid mostra

Cada linha representa um XML carregado e traz, entre outras colunas: `Status`, `Descrição da Loja`, `Sigla Loja`, `Data Emissão`, `Série`, `Nº Doc.`, `Total Nota`, `Qt. Produtos`, `Conf.` (status de conferência), `Razão Social`, `Fantasia`, `Pessoa`, `Cidade`, `Chave de Acesso`, `Emissão` (Própria / Terceiro), `Comportamento` (Entrada / Saída), os valores fiscais (ICMS ST, IPI, Frete, Seguro, FCP, etc.), `Status Conferência`, `Financeiro` (`LANÇADO` / `NÃO LANÇADO`) e `Usuário Conferência`.

> 💡 As cores do `Status Conferência` no grid mudam conforme o andamento — uma coluna que vira amarela ou vermelha indica divergência ou conferência em andamento. Veja [Conferência de XML](documentacao_conferencia_xml.md).

---

## 📥 Importar um novo XML

### O caminho recomendado: a partir da Manifestação do Destinatário

A forma **padrão** de lançar a entrada de uma NF-e no Sol.NET é **não abrir a tela `Importar XML` diretamente**. O fluxo correto começa na [Manifestação do Destinatário](documentacao_manifestacao_destinatario.md) (tela `401`):

1. Pressione **F1** → `401` para abrir a `Manifestação do Destinatário`.
2. Localize a NF-e no grid (filtros por loja, período, fornecedor, chave de acesso etc.).
3. Com a linha selecionada, clique no botão **`NF-e`** (entre os botões `Zerar NSU` e `Confirmar`).
4. O Sol.NET abre a tela `Importar XML NF-e` **já em modo de inclusão**, carrega o XML armazenado no banco (baixado pelo `Sol.NET_MonitorNFCe`) e preenche todas as abas automaticamente.
5. Confira, vincule itens pendentes (se houver) e use `Lançar NF-e` para gerar o movimento.

Esse caminho é o recomendado porque garante que o XML usado é o oficial da SEFAZ (vinculado à manifestação) e dispensa qualquer manipulação de arquivo `.xml` no disco.

### Caminho alternativo: carregar um `.xml` de arquivo

Há casos em que o XML não veio pela SEFAZ — fornecedor enviou por e-mail, pendrive, recebimento em outra loja, etc. Para esses casos:

1. Abra a tela `Importar XML NF-e` (F1 → `204`).
2. Clique em `Novo` para entrar em modo de inclusão.
3. Na sub-aba **`XML`**, grupo **`Arquivo`**, use o botão à direita do campo `Caminho` para escolher o `.xml` no computador (o botão à esquerda limpa o caminho).
4. O Sol.NET lê o arquivo e preenche cabeçalho, fornecedor, itens, financeiro e tributos.

> 💡 **O campo `Chave de Acesso` (grupo `Manifesto`) não é editável para iniciar uma importação.** Esse campo apenas **exibe** a chave de acesso de um XML já carregado (seja vindo da Manifestação, seja extraído do arquivo selecionado). Não digite a chave manualmente esperando que o sistema baixe o XML — não há essa ação.

### O que o Sol.NET faz ao ler o XML

Em uma única passada, o sistema extrai e preenche:

- **Cabeçalho** — natureza da operação, tipo de pagamento, série, número, data de emissão, protocolo, chave de acesso, informações adicionais.
- **Empresa destinatária** — busca pelo CNPJ do destinatário no XML. Se bate com alguma loja, preenche `Descrição da Loja` e `Sigla`. Se **não bate**, mostra `( ... ) NÃO É SUA EMPRESA!` e o lançamento fica bloqueado (a menos que a empresa tenha autorizado importar terceiros).
- **Fornecedor / Emitente** — razão social, fantasia, CNPJ/CPF, IE, telefone, endereço completo, UF, CEP. Se já existe no cadastro de pessoas, vincula automaticamente; se não existe, o usuário pode cadastrá-lo pelo campo `Fornecedor`.
- **Comportamento** — `Entrada` ou `Saída`, lido do XML (`Ide.tpNF`).
- **Emissão** — `PROPRIA` quando o CNPJ do emitente também é uma loja cadastrada; `TERCEIRO` caso contrário.
- **Itens** — todos os produtos do XML, com código do fornecedor, EAN, descrição, unidade, quantidade, valor unitário, descontos, totais, e os tributos (ICMS, ICMS ST, IPI, FCP, COFINS, PIS).
- **Financeiro** — duplicatas / parcelas (número, vencimento, valor) lidas das tags de cobrança.
- **Totais** — descontos, acréscimos, frete, seguro, bases de cálculo, ICMS desonerado, FCP.

### Erros de carregamento comuns

| Mensagem | O que significa | Como resolver |
|----------|-----------------|---------------|
| `Arquivo XML Inválido!` | O arquivo selecionado não é um XML de NF-e válido (corrompido, esquema errado, arquivo trocado). | Selecionar o arquivo correto; pedir ao fornecedor um novo XML se necessário. |
| `Chave de Acesso já Cadastrada!` | Já existe um registro no Sol.NET com essa chave. | Use os filtros para localizar o registro existente em vez de carregar novamente. |
| `( fornecedor ) NÃO É SUA EMPRESA!` | O CNPJ do destinatário no XML não bate com nenhuma loja. | Verificar se a NF-e foi emitida para o CNPJ correto. Se a empresa permite importar para terceiros, habilitar o campo `Descrição da Loja` para escolher manualmente. |
| `Pessoa não cadastrada!` ao vincular item | O fornecedor do XML ainda não está no cadastro de pessoas. | Cadastrar o fornecedor primeiro (botão à direita do campo `Fornecedor`). |

---

## 🧭 Sub-abas do formulário

Depois de carregado, o XML pode ser conferido e editado nas seguintes abas:

### Aba `XML`
Mostra a estrutura crua do arquivo (memo `XML`) e os grupos `Manifesto` / `Arquivo`. Útil para verificar o conteúdo bruto quando algo no parser parece divergir do que está na nota.

### Aba `Cabeçalho`
Reúne os campos do cabeçalho da NF-e, agrupados em três blocos:

- **Identificação** — `Descrição da Loja`, `Sigla`, `Status`, `Natureza da Operação`, `Tipo Pagamento`, `CNPJ`, `Nº Documento`, `Data Emissão`, `Série`, `Emissão` (Própria / Terceiro), `Comportamento` (Entrada / Saída).
- **Dados do Fornecedor** — `Razão Social`, `Fantasia`, `IE`, `CNPJ/CPF`, `Telefone`, `Endereço`, `Nº`, `Bairro`, `Cidade`, `Cód. Cidade`, `UF`, `CEP`, `Complementos`, `Fornecedor` (vínculo com cadastro de pessoas), `Informações Adicionais`.
- **Autorização** — `Protocolo` e `Chave de Acesso` (somente leitura, extraídos do XML).

### Aba `Itens`
A aba mais usada. Aqui o usuário **confere e vincula** cada produto do XML ao cadastro de produtos. Veja a próxima seção.

Dentro de `Itens` há ainda duas sub-abas:

- **`Totais`** — totalizadores fiscais e financeiros (Desc. Produtos, Acrésc. Produtos, Frete, Seguro, Base ICMS, Valor ICMS, Base ICMS ST, Valor ICMS ST, Base IPI, Valor IPI, Cred ICMS SN).
- **`Tributação`** — bases e valores de PIS, COFINS, FCP (Valor Total FCP, Vl. FCP Ret. ST, Vl. FCP Ret Ant. ST) e ICMS Desonerado.

### Aba `Financeiro`
Lista as **parcelas / duplicatas** trazidas do XML, com `Número`, `Vencimento` e `Valor`. Esse grid alimenta a geração de contas a pagar no momento do lançamento da NF-e.

### Aba `Conferência`
**Visível apenas quando a empresa tem o tipo de conferência XML habilitado** no `Cadastro de Empresas`. Mostra o resultado da contagem física da mercadoria, feita pelo app **Sol.NET Administrativo** — é uma visão de leitura, não há marcação nesta tela. Veja o documento dedicado: [Conferência de XML](documentacao_conferencia_xml.md).

---

## 🛒 Vinculando itens do XML ao cadastro de produtos

Esta é a parte que mais consome tempo no dia a dia. Cada linha da aba `Itens` representa um produto no XML do fornecedor — e cada uma precisa "casar" com um produto do cadastro **antes** da NF-e poder ser lançada como movimento.

### Como o Sol.NET tenta vincular automaticamente

Ao **selecionar o fornecedor** (ou quando o XML é carregado e o fornecedor já existe no cadastro), o sistema:

1. Pega o **código do fornecedor** (`Cód. Forn.`) de cada item do XML.
2. Procura no cadastro de produtos um produto que **já tenha esse código associado a esse fornecedor**.
3. Se encontrar, preenche automaticamente: `Código`, `Código Barra`, `Descrição` (do produto no cadastro), `Custo Inicial`, e calcula a conversão de unidade quando aplicável (`Unid.` × `Unid(P)`).

Itens vinculados aparecem com a descrição do produto cadastrado preenchida; itens não vinculados ficam com `Descrição` vazia.

### Quando o vínculo precisa ser manual

Sempre que uma das condições abaixo é verdadeira, o vínculo automático falha e o usuário tem que decidir:

- O **fornecedor é novo** ou ainda não tem produtos com código cadastrado.
- O **código do fornecedor** está em branco no XML.
- O produto **nunca foi comprado** desse fornecedor antes.

Nesses casos, a coluna `Descrição` do item aparece em branco. O usuário precisa **abrir o item e fazer a vinculação manual**:

1. **Duplo clique** sobre a linha do item (ou pressione Enter sobre ela).
2. A tela `Cadastro de Produtos` (código `32` na pesquisa F1) abre **em modo pesquisa**, já filtrada para mostrar produtos. A descrição que aparece no topo é o nome do produto **no fornecedor** (o que veio no XML), para ajudar a identificar.
3. Localize o produto correspondente no cadastro e confirme.
4. O Sol.NET grava o vínculo: a partir daí, **qualquer próxima compra desse mesmo produto com esse fornecedor é vinculada automaticamente** (pelo mesmo `Cód. Forn.`).

### Cadastrando um produto novo durante o vínculo

Se o produto **não existe** no cadastro, o usuário pode incluí-lo **a partir da mesma janela** que abriu para vincular:

1. No `Cadastro de Produtos` que abriu, vá para o modo de inclusão.
2. Os campos `Código do Fornecedor`, `EAN do Fornecedor` e `Descrição no Fornecedor` já vêm pré-preenchidos com os valores do XML — isso ajuda a manter consistência.
3. Preencha os demais campos do produto (descrição interna, unidade, NCM, CST, etc.) e salve.
4. Ao retornar à tela `Importar XML`, o item fica vinculado ao produto recém-criado.

### Regras e bloqueios no vínculo

| Situação | O que o Sol.NET faz |
|----------|---------------------|
| Produto selecionado é do tipo **Serviço** | Bloqueia com `Não Permitido, Tipo Serviço!`. Itens de NF-e de mercadoria não podem casar com produtos de serviço. |
| Produto está marcado para **desagregação** | Bloqueia com `Não Permitido, Produto configurado para desagregação!`. Esses produtos têm fluxo próprio. |
| Produto é **linkado** e a configuração proíbe | Bloqueia com `Não Permitido, Vinculo de produto linkado!`. A regra é controlada por configuração geral do sistema. |
| Produto é **linkado** e a configuração permite | Mostra um aviso `Produto Linkado Selecionado!` com código, código de barra e descrição — o usuário precisa confirmar leitura. |
| Item está com **quantidade zero** ou **valor zero** | Não bloqueia o vínculo, mas é sinalizado ao tentar lançar a NF-e. |
| **Diferença de custo** acima do percentual configurado (margem positiva ou negativa) | Avisa no momento do lançamento — o usuário pode prosseguir ou rever. |

### Coluna `Conf.` no grid de itens

Quando o item é vinculado, a coluna `Conf.` (de "conferido") mostra que o item está pronto para virar movimento. Itens sem vínculo permanecem destacados — o **lançamento da NF-e é bloqueado** enquanto houver itens não vinculados, com a mensagem `Não Existe Nenhum Item com Vinculo!`.

---

## ▶️ Lançar a NF-e na movimentação

Depois que **todos os itens estão vinculados** e o cabeçalho está correto, o usuário decide qual tipo de lançamento fazer. A faixa de botões no rodapé da tela traz três variações de "Lançar" e a impressão do DANFE.

### `Lançar NF-e` — o fluxo padrão

Para a maioria absoluta dos casos, este é o botão a usar.

- **Quando usar**: NF-e de **entrada** vinda de fornecedor (mercadoria recebida da forma como a nota descreve, parcelas a pagar como vieram no XML).
- **O que acontece**: o Sol.NET abre a tela `Movimentos de Compras` (código `201` na pesquisa F1) já preenchida com cabeçalho, itens, tributos e financeiro do XML. O usuário ajusta o que for necessário (tipo de movimento, conta de financeiro, observações) e grava — gerando estoque e contas a pagar.
- Após gravar, o XML passa para status `Importado` e ganha vínculo com o `ID_MOVIMENTO` criado.

### `Lançar Parcial`

- **Quando usar**: quando a mercadoria foi recebida só **em parte** e a empresa quer registrar a entrada **apenas dos itens efetivamente recebidos** — devoluções parciais na origem, falta de mercadoria, conferência divergente para mais ou para menos.
- **O que acontece**: o fluxo é idêntico ao `Lançar NF-e`, mas o usuário pode marcar/desmarcar itens e ajustar quantidades antes da gravação do movimento. O XML continua na tela e pode ser lançado novamente para o restante (ou referenciado em uma divergência fiscal).

### `Lançar Próprio`

- **Quando usar**: para NF-e em que **a empresa é a própria emitente** (campo `Emissão` = `PROPRIA`). Acontece, por exemplo, quando o XML de uma nota de saída/devolução emitida pela empresa volta da SEFAZ e precisa ser conciliado.
- **Bloqueio**: o botão verifica `Emissão`. Se a NF-e não for emissão própria, mostra `Não Permitido! Somente Emissão PROPRIA.` e cancela.
- **Verificações de integridade**:
  - Se já existe um movimento vinculado mas ele foi **cancelado**, o aviso `Movimentação Cancelada! Lançar NF-e Novamente.` aparece e o vínculo é desfeito automaticamente.
  - Se o movimento vinculado foi **excluído**, o aviso `Movimentação Excluida! Lançar NF-e Novamente.` aparece e o vínculo também é desfeito.
- **O que acontece**: o Sol.NET abre a tela `Movimentação` (saída) preenchida com os dados do XML. Após gravar, o XML fica como `Importado` e vinculado ao movimento de saída.

### `DANFE`

Imprime o **Documento Auxiliar da NF-e** a partir do XML armazenado. Funciona tanto a partir do grid (após selecionar uma linha) quanto da tela de cadastro (já com o XML carregado). O sistema abre o preview com opção de configurar a impressora.

---

## 🔗 Relação com a Manifestação do Destinatário

A tela [Manifestação do Destinatário](documentacao_manifestacao_destinatario.md) é a **porta de entrada padrão** dos XMLs no Sol.NET. O fluxo correto é sempre:

1. O `Sol.NET_MonitorNFCe` (aplicação à parte) baixa periodicamente os XMLs da SEFAZ e grava no banco.
2. O usuário abre a `Manifestação do Destinatário` (tela `401`), localiza a nota e a manifesta (`Confirmação`, `Ciência` etc.).
3. Com a linha selecionada, clica no botão **`NF-e`** (entre `Zerar NSU` e `Confirmar`). O Sol.NET abre a tela `Importar XML` já em inclusão, carrega o XML do banco e preenche todas as abas.
4. Depois de gravado o movimento via `Lançar NF-e`, o grid da Manifestação passa a mostrar as colunas `M-` (do movimento), permitindo conferir divergências (valor, data, número) entre o que o fornecedor emitiu e o que foi lançado.

Abrir o `Importar XML` diretamente (F1 → `204` → `Novo`) é um **caminho excepcional**, usado apenas quando o XML chegou por fora da SEFAZ (e-mail, pendrive, outra loja). O fluxo principal sempre passa pela Manifestação.

---

## 💡 Exemplos Práticos

### Exemplo 1 — Entrada normal de fornecedor recorrente (fluxo padrão via Manifestação)

**Cenário**: o fornecedor enviou a mercadoria com NF-e. O `Sol.NET_MonitorNFCe` já baixou o XML da SEFAZ. O cliente já comprou várias vezes desse fornecedor.

1. Abra a `Manifestação do Destinatário` (F1 → `401`).
2. Localize a NF-e no grid (filtros por loja, fornecedor, período ou chave de acesso).
3. Se ainda não manifestou, clique em `Confirmar(1)` (ou `Ciência(4)` quando aplicável).
4. Com a linha selecionada, clique no botão **`NF-e`** (entre `Zerar NSU` e `Confirmar`).
5. A tela `Importar XML NF-e` abre em inclusão, com todas as abas preenchidas a partir do XML armazenado.
6. Aba `Itens`: **todos os itens devem aparecer vinculados** (descrição preenchida) porque o vínculo foi gravado em compras anteriores. Confira valores e quantidade.
7. Aba `Financeiro`: confira as parcelas que vieram do XML.
8. Clique em `Lançar NF-e`. A tela `Movimentos de Compras` abre com tudo preenchido.
9. Ajuste o `Tipo de Movimento` se necessário e grave.
10. O XML passa para status `Importado` e o vínculo aparece nas colunas `M-` da Manifestação.

### Exemplo 2 — Primeira compra de um fornecedor novo

**Cenário**: fornecedor novo, ainda não cadastrado no Sol.NET, com itens nunca comprados. O XML já foi baixado pela Manifestação.

1. Manifeste a nota e abra pelo botão `NF-e` como no Exemplo 1.
2. Mensagem `( razão social ) NÃO É SUA EMPRESA!` **não** aparece — o destinatário (você) está correto.
3. A aba `Cabeçalho` mostra o fornecedor com `Fornecedor` em branco. Clique no botão **`Cadastrar fornecedor`** à direita do campo (ícone de adicionar) — o cadastro de pessoas abre com CNPJ, razão, endereço já preenchidos do XML. Salve.
4. Volte para a aba `Itens`. Todos os itens estão sem descrição (sem vínculo).
5. Duplo clique no primeiro item — abre o `Cadastro de Produtos` em pesquisa. Se o produto já existe no seu cadastro com outro código, localize-o e confirme — o sistema grava o vínculo para esse fornecedor.
6. Se o produto **não existe**, vá para inclusão dentro do `Cadastro de Produtos`. Os campos `Cód. Fornecedor`, `EAN Fornecedor` e `Descrição Fornecedor` já vêm preenchidos do XML — complete o restante (NCM, CST, unidade, preço de venda) e salve.
7. Repita para os demais itens. A partir da segunda compra, esse fornecedor vai entrar como no Exemplo 1.

### Exemplo 3 — Tentativa de duplicidade

**Cenário**: o usuário tenta lançar uma NF-e que já foi importada antes (por exemplo, abriu o `Importar XML` direto com `Novo` e selecionou um `.xml` cujo registro já existe).

1. Após o carregamento, o Sol.NET detecta a chave já cadastrada e mostra `Chave de Acesso já Cadastrada!`.
2. A tela limpa o campo e abre o registro existente na aba de busca para que o usuário confirme.
3. Se o registro anterior já virou movimento (`Status = Importado`), nada precisa ser feito — a nota já está lançada.
4. Se o registro anterior está em `Edição`, abra-o pelo grid e termine o lançamento por lá.

### Exemplo 4 — Recebimento parcial

**Cenário**: a NF-e tem 10 itens, mas só 7 chegaram fisicamente.

1. Abra a nota pelo fluxo da Manifestação (Exemplo 1, passos 1–5).
2. Vincule todos os 10 itens ao cadastro.
3. Na aba `Itens`, marque (na coluna `Sel.`) apenas os 7 itens que chegaram.
4. Ajuste a quantidade dos 7 itens se houver divergência de unidade.
5. Clique em `Lançar Parcial`. A tela de movimento abre só com os itens marcados.
6. Grave. O Sol.NET registra o movimento parcial e mantém o XML para complementação futura (ou para uma operação de divergência).

---

## ❓ FAQ / Problemas Comuns

A lista completa está em [FAQ — Importar XML](faq_importar_xml.md). Os mais frequentes:

- **"O XML do fornecedor não está sendo aceito"** → quase sempre arquivo corrompido ou XML de NFC-e (consumidor) em vez de NF-e. Peça novo arquivo.
- **"Aparece *NÃO É SUA EMPRESA*"** → CNPJ do destinatário no XML difere do CNPJ das lojas cadastradas. Conferir loja correta ou autorização para importar terceiro.
- **"Não estou conseguindo vincular um item específico"** → o produto pode estar como **Serviço** ou marcado para **desagregação**; nesses casos o vínculo é bloqueado por regra.
- **"Importei mas o financeiro não veio"** → o XML pode não ter trazido a tag de cobrança (NF-e à vista, por exemplo), ou as parcelas foram canceladas na conferência. Verifique a aba `Financeiro`.

---

**Última atualização**: Maio de 2026  
**Versão**: 1.0  
**Público-alvo**: Usuários e administradores do Sol.NET ERP
