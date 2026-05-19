# 📄 Grupos de Produtos - Sol.NET

## 🎯 Visão Geral

**Grupos de Produtos** é o segundo nível da hierarquia oficial de classificação de produtos no Sol.NET — sempre **filho de uma Família**. A árvore completa é Família → Grupo → Subgrupo, e cada produto pode ser vinculado aos três níveis na aba `Principal` do `Cadastro de Produtos`.

Como a Família já carrega regras de margem, comissão, desconto e integração e-commerce/mobile, o Grupo serve para **refinar** essas regras dentro da linha. Por exemplo: dentro da Família `FEMININO`, o Grupo `LANCAMENTOS` pode ter margem maior e desconto menor que o Grupo `LIQUIDACAO`. O produto vinculado ao Grupo herda as regras do Grupo, e o Grupo herda da Família — mas ao salvar o produto, os percentuais ficam gravados no próprio produto.

### Principais características

- ✅ **Segundo nível** da hierarquia Família → Grupo → Subgrupo.
- ✅ **Sempre vinculado a uma Família** (campo obrigatório).
- ✅ **Refina** a política de margem, comissão e desconto da Família.
- ✅ **Controles separados de Mobile e e-Commerce** — pode habilitar/desabilitar o envio para integrações no nível do Grupo, sem precisar mexer na Família inteira.
- ✅ **Foto do Grupo** vinculável para uso em catálogos visuais.

> 🔎 **Diferença em relação à Família**: o Grupo **não tem** a regra de arredondamento de preços (exclusiva das Famílias). Em compensação, tem dois toggles extras de "Desativar Envio" (e-Commerce e Mobile), o que permite desligar a integração de um Grupo específico sem afetar os outros da mesma Família.

---

## 🚪 Como acessar

Abra a pesquisa universal (atalho `F1`) e digite **`25`** (ou parte do nome `Grupos de Produtos`).

---

## 📝 Campos do cadastro

### Identificação

- **Descrição** — nome do Grupo, obrigatório, gravado em maiúsculas. Aparece nos combos, filtros e relatórios.
- **Família de Produto** — combo obrigatório. Vincula o Grupo a uma Família cadastrada previamente em `Famílias de Produtos` (código `24`).
- **Descrição e-Commerce** — descrição alternativa enviada para o site e para o app de força de venda.
- **Foto** — imagem opcional do Grupo, usada em catálogos e integrações.

### Política de margem para o preço do produto

Define a faixa de margem usada quando o `Cadastro de Produtos` calcula o preço a partir da margem desejada:

- **Alterar Preço Produto → Mínimo** — margem mínima admitida (%).
- **Alterar Preço Produto → Máximo** — margem máxima admitida (%).

### Política de margem na movimentação

Mesma ideia, para alterações de preço **durante a venda**:

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

### Integração (terceiros) — e-commerce

- **Enviar Para o Site** — quando marcado, os produtos do Grupo entram na rotina de integração com o e-commerce.
- **Desativar Envio p/ Site** — bloqueia o envio dos produtos do Grupo para o e-commerce, mesmo que a Família esteja com envio habilitado. Funciona como "exceção" da Família.

> ⚠️ **Os dois toggles não podem ser marcados ao mesmo tempo**. Ao salvar com ambos marcados, o sistema avisa `Não Permitido, "Enviar Para o Site" e "Desativar Envio p/ Site" Marcados Simultaneamente!`.

### Mobile (e-Commerce / Força de Venda)

- **Enviar** — quando marcado, os produtos do Grupo são enviados para o app de força de venda e/ou e-commerce mobile.
- **Desabilitar Envio** — bloqueia o envio dos produtos do Grupo para o mobile, mesmo que a Família esteja com envio habilitado.
- **Ordenar** — número inteiro que define a ordem de exibição do Grupo nas integrações mobile. Grupos com `Ordenar` menor aparecem primeiro.

> ⚠️ A mesma regra dos toggles vale para Mobile: `Enviar` e `Desabilitar Envio` **não podem** estar marcados simultaneamente.

---

## ⚙️ Regras de validação

- **Descrição obrigatória** — não é possível salvar sem preencher.
- **Família obrigatória** — todo Grupo precisa estar vinculado a uma Família.
- **Descrição única por Família** — dois Grupos da **mesma** Família não podem ter a mesma descrição. Famílias diferentes podem ter Grupos com nomes iguais. Se a regra for violada, o sistema avisa `(DESCRICAO) e (FAMILIA) Já Existe!`.
- **Descrição e-Commerce única por Família** — segue a mesma regra de unicidade combinada com a Família.
- **Toggles de envio mutuamente exclusivos** — não é permitido marcar `Enviar Para o Site` e `Desativar Envio p/ Site` ao mesmo tempo. Idem para os toggles de Mobile.

---

## 🔗 Relação com Famílias, Sub Grupos e Produtos

- **Famílias** (código `24`) — o Grupo é sempre filho de uma Família. A Família precisa estar cadastrada antes.
- **Sub Grupos** (código `26`) — são filhos do Grupo. Ao criar um Sub Grupo, é obrigatório informar o Grupo a que ele pertence.
- **Produtos** (código `32`) — podem ser vinculados ao Grupo na aba `Principal`. O vínculo é opcional — um produto pode ter Família sem Grupo, ou os três níveis. Quando o Grupo é informado no produto, a Família dele é preenchida automaticamente.

**Não é possível excluir** um Grupo que tenha Sub Grupos vinculados ou que tenha produtos diretamente vinculados a ele. Antes de remover:

1. Reclassifique os produtos para outro Grupo no `Cadastro de Produtos`.
2. Reclassifique ou exclua os Sub Grupos que pertencem a esse Grupo no `Cadastro de Sub Grupo de Produtos`.

---

## 💡 Exemplos Práticos

### Cenário 1 — Loja de roupas refinando margem por Grupo

Dentro da Família `FEMININO`, a loja cria três Grupos:

- `LANCAMENTOS` — margem mínima `80%`, desconto máximo `5%`. Coleção nova, sem promoção.
- `COLECAO ANTERIOR` — margem mínima `50%`, desconto máximo `20%`. Mercadoria do estoque que precisa girar.
- `LIQUIDACAO` — margem mínima `15%`, desconto máximo `50%`. Mercadoria final de estação.

Cada produto, ao ser cadastrado, herda do Grupo a faixa de margem e desconto. O caixa do PDV trava descontos acima do limite definido pelo Grupo.

### Cenário 2 — Bloqueio de Grupo específico no e-commerce

A Família `MEDICAMENTOS` está habilitada para envio ao site (a maioria dos produtos é vendida online). Mas o Grupo `CONTROLADOS` precisa ficar fora da loja virtual por exigência regulatória. Solução: na tela `Grupos de Produtos`, abra o Grupo `CONTROLADOS` e marque `Desativar Envio p/ Site` (sem marcar `Enviar`). Essa configuração bloqueia o envio só desse Grupo, sem mexer na Família.

### Cenário 3 — Ordenação no app mobile

A força de venda usa o app para apresentar a linha de produtos por categoria. Os Grupos `PROMOCOES` e `LANCAMENTOS` recebem `Ordenar = 1` e `Ordenar = 2` para aparecerem no topo da lista. Os demais Grupos (`PADRAO`, `KITS`, etc.) recebem números maiores, ficando no final.

---

## ❓ FAQ / Problemas Comuns

### ❓ Por que preciso escolher a Família antes de criar o Grupo?

Porque o Grupo herda contexto da Família — regras, classificações e integrações. Sem Família, o Sol.NET não saberia onde o Grupo se encaixa na hierarquia, e os relatórios gerenciais não conseguiriam consolidar por linha.

### ❓ Tentei salvar e apareceu "Não Permitido, Enviar e Desativar Envio Marcados Simultaneamente". O que faço?

Você marcou as duas opções de envio (para o site ou para mobile) ao mesmo tempo. Desmarque uma delas — só uma faz sentido por vez: ou o Grupo é enviado (`Enviar`), ou está bloqueado (`Desativar Envio`), ou nenhuma das duas está marcada (comportamento padrão herdado da Família).

### ❓ Mudei a margem do Grupo. Os produtos já cadastrados foram alterados?

Não. O Grupo guarda os percentuais como **sugestão** para novos cadastros e recálculos manuais. Os produtos já existentes mantêm as próprias margens gravadas na aba `Preços` do `Cadastro de Produtos`. Para forçar atualização em massa, é necessário usar a ferramenta de atualização de preços a partir do Grupo (consulte o suporte).

### ❓ Dois Grupos com a mesma descrição em Famílias diferentes — isso é permitido?

Sim. A regra de unicidade da descrição é **por Família**. Você pode ter:

- Família `MASCULINO`, Grupo `CAMISETAS`
- Família `FEMININO`, Grupo `CAMISETAS`

Os dois coexistem normalmente. O que não é permitido é repetir `CAMISETAS` duas vezes dentro da **mesma** Família.

### ❓ Posso mudar a Família de um Grupo depois de criado?

Sim, abrindo o Grupo e alterando o campo `Família de Produto`. Mas atenção: os produtos vinculados a esse Grupo passam automaticamente a pertencer à nova Família, o que pode afetar relatórios consolidados, comissão e curva ABC. Em operações grandes, prefira criar o Grupo novo na Família correta e reclassificar os produtos um a um.

### ❓ Posso excluir um Grupo?

Só se ele não tiver nenhum Sub Grupo nem nenhum produto vinculado. O sistema bloqueia a exclusão quando há dependentes. Antes de remover, reclassifique tudo que aponta para o Grupo.

### ❓ A descrição aceita acento?

Não. O campo grava em maiúsculas e sem acentos — `ELETRÔNICOS` será salvo como `ELETRONICOS`.

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Equipe de suporte Hetosoft e usuários do Sol.NET
