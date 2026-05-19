# 📄 Sub Grupo de Produtos - Sol.NET

## 🎯 Visão Geral

**Sub Grupo de Produtos** é o terceiro e mais detalhado nível da hierarquia oficial de classificação de produtos no Sol.NET — sempre **filho de um Grupo**, que por sua vez é filho de uma Família. A árvore completa é Família → Grupo → Sub Grupo, e cada produto pode ser vinculado aos três níveis na aba `Principal` do `Cadastro de Produtos`.

O Sub Grupo funciona da mesma maneira que o Grupo, mas em um nível ainda mais fino. Onde a Família dá o "departamento" e o Grupo dá a "categoria", o Sub Grupo permite subdividir a categoria em variações (tipo, função, material, marca interna, etc.) sem precisar criar um novo Grupo só para isso.

### Principais características

- ✅ **Terceiro nível** da hierarquia Família → Grupo → Sub Grupo.
- ✅ **Sempre vinculado a um Grupo** (campo obrigatório), que por sua vez está vinculado a uma Família.
- ✅ **Refina** ainda mais a política de margem, comissão e desconto dentro do Grupo.
- ✅ **Controles separados de Mobile e e-Commerce** — pode habilitar/desabilitar o envio para integrações no nível do Sub Grupo.
- ✅ **Foto do Sub Grupo** vinculável para uso em catálogos visuais.

> 🔎 **Diferença em relação ao Grupo**: o conjunto de campos é praticamente o mesmo, mas o Sub Grupo é filho de um Grupo (em vez de uma Família). A Família aparece como referência visual na tela (vinda do Grupo escolhido), porém só o `Grupo` é selecionável e gravado no cadastro.

---

## 🚪 Como acessar

Abra a pesquisa universal (atalho `F1`) e digite **`26`** (ou parte do nome `Sub Grupo de Produtos`).

---

## 📝 Campos do cadastro

### Identificação

- **Descrição** — nome do Sub Grupo, obrigatório, gravado em maiúsculas. Aparece nos combos, filtros e relatórios.
- **Familia de Produtos** — campo de referência exibido na tela. Aparece automaticamente conforme o Grupo escolhido — **não** é digitado nem alterado direto. Serve apenas para confirmar visualmente a hierarquia.
- **Grupo de Produto** — combo obrigatório. Vincula o Sub Grupo a um Grupo cadastrado em `Grupos de Produtos` (código `25`). Ao escolher o Grupo, a Família correspondente é mostrada no campo acima.
- **Descrição e-Commerce** — descrição alternativa enviada para o site e para o app de força de venda.
- **Foto** — imagem opcional do Sub Grupo, usada em catálogos e integrações.

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

Percentuais máximos de desconto aceitos na venda:

- **Desconto → A Vista** — desconto máximo à vista (%).
- **Desconto → A Prazo** — desconto máximo a prazo (%).

### Integração (terceiros) — e-commerce

- **Enviar Para o Site** — quando marcado, os produtos do Sub Grupo entram na rotina de integração com o e-commerce.
- **Desativar Envio p/ Site** — bloqueia o envio dos produtos do Sub Grupo para o e-commerce, mesmo que a Família ou o Grupo estejam com envio habilitado. Funciona como "exceção" do Grupo.

> ⚠️ **Os dois toggles não podem ser marcados ao mesmo tempo**. Ao salvar com ambos marcados, o sistema avisa `Não Permitido, "Enviar Para o Site" e "Desativar Envio p/ Site" Marcados Simultaneamente!`.

### Mobile (e-Commerce / Força de Venda)

- **Enviar** — quando marcado, os produtos do Sub Grupo são enviados para o app de força de venda e/ou e-commerce mobile.
- **Desabilitar Envio** — bloqueia o envio dos produtos do Sub Grupo para o mobile, mesmo que a Família ou o Grupo estejam habilitados.
- **Ordenar** — número inteiro que define a ordem de exibição do Sub Grupo nas integrações mobile. Sub Grupos com `Ordenar` menor aparecem primeiro.

> ⚠️ A mesma regra dos toggles vale para Mobile: `Enviar` e `Desabilitar Envio` **não podem** estar marcados simultaneamente.

---

## ⚙️ Regras de validação

- **Descrição obrigatória** — não é possível salvar sem preencher.
- **Grupo obrigatório** — todo Sub Grupo precisa estar vinculado a um Grupo.
- **Descrição única por Grupo** — dois Sub Grupos do **mesmo** Grupo não podem ter a mesma descrição. Grupos diferentes (até dentro da mesma Família) podem ter Sub Grupos com nomes iguais. Se a regra for violada, o sistema avisa `(DESCRICAO) e (GRUPO) Já Existe!`.
- **Descrição e-Commerce única por Grupo** — segue a mesma regra de unicidade combinada com o Grupo.
- **Toggles de envio mutuamente exclusivos** — não é permitido marcar `Enviar Para o Site` e `Desativar Envio p/ Site` ao mesmo tempo. Idem para os toggles de Mobile.

---

## 🔗 Relação com Famílias, Grupos e Produtos

- **Famílias** (código `24`) — raiz da hierarquia. O Sub Grupo herda a Família indiretamente, pelo Grupo escolhido.
- **Grupos** (código `25`) — pai direto do Sub Grupo. O Grupo precisa estar cadastrado antes.
- **Produtos** (código `32`) — podem ser vinculados ao Sub Grupo na aba `Principal`. O vínculo é opcional — um produto pode ter Família + Grupo sem Sub Grupo. Quando o Sub Grupo é informado no produto, o Grupo e a Família dele são preenchidos automaticamente, mantendo a árvore coerente.

**Não é possível excluir** um Sub Grupo que tenha produtos vinculados. Antes de remover, reclassifique os produtos para outro Sub Grupo (ou deixe-os sem Sub Grupo) no `Cadastro de Produtos`.

---

## 💡 Exemplos Práticos

### Cenário 1 — Loja de calçados subdividindo por tipo

A loja organiza:

- Família `MASCULINO`
- Grupo `CALCADOS` (dentro de `MASCULINO`)
- Sub Grupos do Grupo `CALCADOS`:
  - `SOCIAIS`
  - `ESPORTIVOS`
  - `CASUAIS`
  - `BOTAS`

Cada Sub Grupo pode ter margem e comissão próprias — por exemplo, `SOCIAIS` com margem maior por girar menos, `ESPORTIVOS` com comissão maior para incentivar venda. Os relatórios de venda permitem chegar até esse nível de detalhe.

### Cenário 2 — Sub Grupo bloqueando uma exceção

A Família `INFORMATICA` e o Grupo `ACESSORIOS` estão liberados para o e-commerce. Mas o Sub Grupo `CABOS RECONDICIONADOS` (peças usadas) não deve aparecer na loja virtual. Solução: abra o Sub Grupo em `Sub Grupo de Produtos` e marque `Desativar Envio p/ Site` (sem marcar `Enviar`). Os outros Sub Grupos do Grupo `ACESSORIOS` seguem sendo enviados normalmente.

### Cenário 3 — Reorganizando produtos quando o Grupo muda

A empresa percebe que o Sub Grupo `SUCO NATURAL` foi cadastrado dentro do Grupo errado (`BEBIDAS QUENTES` em vez de `BEBIDAS GELADAS`). Como mover o Sub Grupo direto pode afetar relatórios já consolidados:

1. Abre o Sub Grupo e troca o `Grupo de Produto`.
2. Confirma que a `Familia de Produtos` (mostrada na tela) ainda faz sentido depois da troca.
3. Os produtos vinculados ao Sub Grupo passam automaticamente a pertencer ao novo Grupo (e à Família dele, se diferente).

---

## ❓ FAQ / Problemas Comuns

### ❓ Por que o campo `Familia de Produtos` aparece preenchido sem eu digitar nada?

Ele é puxado automaticamente a partir do `Grupo de Produto` escolhido. É um campo de **referência** (não editável) que serve para você conferir a hierarquia antes de salvar. Para mudar a Família, é necessário escolher um Grupo de outra Família.

### ❓ Tentei salvar e apareceu "Não Permitido, Enviar e Desativar Envio Marcados Simultaneamente". O que faço?

Você marcou as duas opções de envio (para o site ou para mobile) ao mesmo tempo. Desmarque uma delas — só uma faz sentido por vez: ou o Sub Grupo é enviado (`Enviar`), ou está bloqueado (`Desativar Envio`), ou nenhuma das duas está marcada (herdando o comportamento do Grupo/Família).

### ❓ Dois Sub Grupos com a mesma descrição em Grupos diferentes — isso é permitido?

Sim. A regra de unicidade da descrição é **por Grupo**. Você pode ter:

- Grupo `CAMISETAS`, Sub Grupo `MANGA CURTA`
- Grupo `BLUSAS`, Sub Grupo `MANGA CURTA`

Coexistem normalmente. O que não é permitido é repetir `MANGA CURTA` duas vezes dentro do **mesmo** Grupo.

### ❓ Posso mudar o Grupo de um Sub Grupo depois de criado?

Sim, abrindo o Sub Grupo e alterando o campo `Grupo de Produto`. Os produtos vinculados passam automaticamente para o novo Grupo (e Família, se for diferente). Em operações grandes isso pode afetar relatórios já consolidados — vale validar antes.

### ❓ A regra de margem do Sub Grupo prevalece sobre a do Grupo e da Família?

Cada nível tem suas próprias regras gravadas. O `Cadastro de Produtos` usa o nível **mais específico preenchido** na hora de calcular: se o produto tem Sub Grupo, usa as regras do Sub Grupo; se não, usa as do Grupo; se não, usa as da Família. Uma vez calculados e gravados no produto, os percentuais ficam ali — mudanças posteriores no Sub Grupo não retroagem.

### ❓ Posso excluir um Sub Grupo?

Só se ele não tiver nenhum produto vinculado. O sistema bloqueia a exclusão quando há dependentes. Antes de remover, reclassifique os produtos para outro Sub Grupo (ou deixe-os sem Sub Grupo) no `Cadastro de Produtos`.

### ❓ A descrição aceita acento?

Não. O campo grava em maiúsculas e sem acentos — `INFORMÁTICA` será salvo como `INFORMATICA`.

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Equipe de suporte Hetosoft e usuários do Sol.NET
