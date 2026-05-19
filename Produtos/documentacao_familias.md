# 📄 Famílias de Produtos - Sol.NET

## 🎯 Visão Geral

**Famílias de Produtos** é o primeiro nível da hierarquia oficial de classificação de produtos no Sol.NET. Cada produto pode pertencer a uma `Família`, que se subdivide em `Grupos` e, por sua vez, em `Sub Grupos`. Essa árvore organiza o cadastro em três níveis e é a base dos relatórios gerenciais, da curva de margem, da política de comissão e desconto por linha, e das integrações de e-commerce e mobile.

Diferente de um cadastro puramente descritivo, a Família carrega **regras de negócio** que são herdadas pelo produto no momento da precificação:

- **Margens** mínima e máxima — usadas quando o preço do produto é calculado a partir da margem desejada.
- **Comissão** à vista e a prazo — sugestão de comissão para a venda.
- **Desconto** à vista e a prazo — máximo de desconto admitido para a linha.
- **Regra de arredondamento** dos preços calculados via margem.
- **Sinalizadores de e-commerce e mobile** — controlam se a linha inteira é enviada para integrações de site e força de venda.

### Principais características

- ✅ **Raiz da hierarquia** Família → Grupo → Subgrupo.
- ✅ **Regras herdadas** pelo produto quando o preço é calculado pela margem desejada.
- ✅ **Política de comissão e desconto** centralizada por linha.
- ✅ **Regra de arredondamento** automática (exclusiva das Famílias — Grupos e Subgrupos não têm).
- ✅ **Integração e-commerce/mobile** controlada no nível da Família.
- ✅ **Foto da Família** vinculável para uso em catálogos e e-commerce.

---

## 🚪 Como acessar

Abra a pesquisa universal (atalho `F1`) e digite **`24`** (ou parte do nome `Famílias de Produtos`).

---

## 📝 Campos do cadastro

### Identificação

- **Descrição** — nome da Família, obrigatório, gravado em maiúsculas. É o que aparece em todos os combos, filtros e relatórios.
- **Descrição e-Commerce** — descrição alternativa para integrações de site e mobile. Útil quando o nome interno da Família é abreviado ou técnico, e o e-commerce precisa de algo mais descritivo para o consumidor.
- **Foto** — imagem opcional da Família, usada em catálogos visuais e integrações de e-commerce.

### Política de margem para o preço do produto

Define a faixa de margem usada quando o `Cadastro de Produtos` calcula o preço a partir da margem desejada (em vez de digitar o preço direto):

- **Alterar Preço Produto → Mínimo** — margem mínima admitida (%).
- **Alterar Preço Produto → Máximo** — margem máxima admitida (%).

### Política de margem na movimentação

Mesma ideia, mas para alterações de preço **durante a venda** (descontos ou acréscimos lançados em movimento):

- **Alterar Preço Venda (Mov.) → Mínimo** — margem mínima admitida no movimento (%).
- **Alterar Preço Venda (Mov.) → Máximo** — margem máxima admitida no movimento (%).

### Comissão

Percentuais sugeridos para o cálculo de comissão do vendedor:

- **Comissão → A Vista** — comissão para venda à vista (%).
- **Comissão → A Prazo** — comissão para venda a prazo (%).

### Desconto

Percentuais máximos de desconto aceitos na venda da linha:

- **Desconto → A Vista** — desconto máximo à vista (%).
- **Desconto → A Prazo** — desconto máximo a prazo (%).

### Arredondamento

Regra aplicada automaticamente quando o preço do produto é calculado a partir da margem desejada (a Família é o **único** dos cadastros hierárquicos que tem essa configuração — Grupos e Subgrupos não a possuem).

- **Preços** — combo com cinco opções:
  - *Não arredondar* (em branco)
  - *Decimais — Ex.: 1,02/1,00 - 1,03/1,05 - 1,06/1,10* — arredonda para múltiplos de centavos com corte fixo.
  - *Decimais — Ex.: 1,02/0,99 - 1,03/1,05 - 1,06/1,09* — arredonda para centavos terminando em 9.
  - *Centavos — Ex.: 10,20/10,00 - 10,30/10,50 - 10,60/11,00* — arredonda para múltiplos de R$ 0,50.
  - *Centavos — Ex.: 10,20/9,99 - 10,30/10,49 - 10,60/10,99* — arredonda para preços terminando em ,99 ou ,49.
- **Preços (3,4) Acima** — valor de corte a partir do qual o arredondamento de centavos (opções 3 ou 4) começa a valer. Útil para diferenciar regra de produtos baratos versus caros.

> 💡 **Como funciona na prática:** no `Cadastro de Produtos` (código `32`), aba `Preços`, quando o usuário informa **Margem desejada (%)** em vez de digitar o preço, o sistema multiplica o custo pela margem e aplica a regra de arredondamento da Família para gerar o preço final. Sem regra de arredondamento definida, o preço calculado é gravado exatamente como vier do cálculo.

### Integração (terceiros) — e-commerce

- **Enviar Para o Site** — quando marcado, os produtos da Família entram na rotina de integração com a loja virtual / e-commerce. Quando desmarcado, a Família inteira fica fora da sincronização.

### Mobile (e-Commerce / Força de Venda)

- **Enviar** — quando marcado, os produtos da Família são enviados para o app de força de venda e/ou e-commerce mobile.
- **Ordenar** — número inteiro que define a ordem de exibição da Família nas integrações mobile. Famílias com `Ordenar` menor aparecem primeiro.

---

## ⚙️ Regras de validação

- **Descrição obrigatória** — não é possível salvar sem preencher.
- **Descrição única** — duas Famílias não podem ter a mesma descrição (comparação sem distinção de maiúsculas/minúsculas). Se tentar, o sistema avisa `(VALOR) Já Existe!`.
- **Descrição e-Commerce única** — segue a mesma regra: duas Famílias não podem ter a mesma `Descrição e-Commerce`.

---

## 🔗 Relação com Produtos, Grupos e Subgrupos

A Família é o ponto de partida da hierarquia:

- **Grupos** (código `25`) são sempre filhos de uma Família. Ao criar um Grupo, é obrigatório informar a Família a que ele pertence.
- **Sub Grupos** (código `26`) são filhos de um Grupo (e, por consequência, da Família do Grupo).
- **Produtos** (código `32`) podem ser vinculados à Família, ao Grupo e ao Subgrupo na aba `Principal`. Cada nível é independente — um produto pode ter só Família, ou Família + Grupo, ou os três níveis.

**Não é possível excluir** uma Família que tenha Grupos vinculados, ou que tenha produtos diretamente vinculados a ela. Antes de remover:

1. Reclassifique os produtos para outra Família no `Cadastro de Produtos`.
2. Reclassifique ou exclua os Grupos que pertencem a essa Família no `Cadastro de Grupos`.

---

## 💡 Exemplos Práticos

### Cenário 1 — Loja de roupas com política única por linha

A loja organiza as Famílias por linha de produto: `MASCULINO`, `FEMININO`, `INFANTIL`. Cada Família define:

- Margem mínima `30%` e máxima `120%` — limites de margem aplicados quando o gerente calcula preço sugerido a partir do custo.
- Comissão à vista `5%` e a prazo `3%` — política única para os vendedores em todos os produtos da linha.
- Desconto à vista máximo `10%` — barreira contra desconto excessivo no caixa.
- Arredondamento `Centavos — terminando em 9` — todos os preços calculados são forçados para `R$ X,99`.

Quando o cadastro de um novo produto da linha `MASCULINO` informa custo `R$ 50,00` e margem `100%`, o sistema calcula `R$ 100,00`, aplica a regra `,99` e grava `R$ 99,99`.

### Cenário 2 — Distribuidora com integração e-commerce parcial

A distribuidora cadastra Famílias para todas as linhas que comercializa, mas só uma parte vai para o site. Famílias como `DEFENSIVOS AGRICOLAS` ficam com `Enviar Para o Site` **desmarcado** (venda restrita a B2B no presencial), enquanto `SEMENTES` e `FERRAMENTAS` ficam **marcadas**. A integração lê apenas as Famílias habilitadas.

### Cenário 3 — Família "técnica" com descrição amigável para o site

A Família interna se chama `MAT ELET BAIXA TENSAO` para padronizar relatórios fiscais. Na `Descrição e-Commerce`, o usuário coloca `MATERIAL ELETRICO RESIDENCIAL`. O ERP segue usando o nome técnico nos relatórios internos, mas a loja virtual exibe a versão amigável para o consumidor final.

---

## ❓ FAQ / Problemas Comuns

### ❓ Para que serve `Descrição e-Commerce` se já existe `Descrição`?

A `Descrição` é usada em todos os lugares internos do Sol.NET — combos, relatórios, listas de pesquisa. A `Descrição e-Commerce` é o nome enviado para a loja virtual e o app de força de venda. Quando você quer que o consumidor final veja um nome diferente do nome técnico interno, preencha as duas com textos diferentes.

### ❓ A regra de arredondamento é aplicada sempre?

Não. Ela só roda quando o preço do produto é calculado pelo sistema a partir da margem desejada (no `Cadastro de Produtos`, aba `Preços`, ao informar a margem em vez de digitar o preço direto). Se você digitar o preço diretamente, o valor é gravado como informado, sem arredondamento.

### ❓ Tentei marcar "Enviar Para o Site" e "Desativar Envio p/ Site" ao mesmo tempo e o sistema bloqueou.

Essa opção de "Desativar Envio" existe nos cadastros de **Grupos** (`25`) e **Sub Grupos** (`26`), não em Famílias. Em Famílias só há a opção `Enviar Para o Site`. Confira em qual tela você está.

### ❓ Mudei a comissão da Família. Os produtos já cadastrados foram atualizados?

A Família guarda o **percentual sugerido**. Como cada produto carrega seus próprios percentuais de comissão na aba `Preços`, a alteração da Família **não muda retroativamente** o que já está nos produtos. A nova regra é aplicada apenas a novos cadastros e a recálculos manuais a partir do produto.

### ❓ Posso excluir uma Família?

Só se ela não tiver nenhum Grupo nem nenhum produto vinculado. O sistema bloqueia a exclusão quando há dependentes. Para limpar, primeiro reclassifique tudo que aponta para a Família e depois exclua.

### ❓ Qual a ordem ideal de cadastro?

1. Cadastre primeiro as **Famílias** (define a estrutura da linha).
2. Depois os **Grupos** (vinculados à Família).
3. Depois os **Sub Grupos** (vinculados ao Grupo).
4. Por último, os **Produtos** (vinculados aos três níveis).

Você pode pular níveis se a empresa não precisa de todos — Grupo e Subgrupo são opcionais no `Cadastro de Produtos`.

### ❓ A descrição aceita acento?

Não. O campo grava em maiúsculas e sem acentos — `ELETRÔNICOS` será salvo como `ELETRONICOS`. Isso uniformiza a busca textual e os filtros.

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Equipe de suporte Hetosoft e usuários do Sol.NET
