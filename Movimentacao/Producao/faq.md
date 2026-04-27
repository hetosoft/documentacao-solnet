---
title: "FAQ: Produção - Sol.NET"
permalink: /Movimentacao/Producao/faq/
---
# 📄 FAQ — Produção - Sol.NET

> Dúvidas frequentes sobre o módulo de Produção. Para detalhes completos, ver [Documentação](documentacao_producao.md) e [Guia Rápido](guia_rapido.md).

## 🎯 Conceitos básicos

### Qual a diferença entre **Fórmula** e **Produção**?

A **Fórmula** (tela `143`) é a **receita** do produto: define quem é o produto acabado, quais insumos/embalagens entram, em que quantidade e quais perdas são esperadas. É um cadastro reutilizável — uma fórmula pode ser executada inúmeras vezes.

A **Produção** (tela `144`) é a **execução** dessa receita: representa um lote real de fabricação, com data/hora de início e fim, quantidade efetivamente produzida e os movimentos de estoque gerados ao final.

### Por que preciso de **três tipos de movimento** (Entrada, Saída e Perda)?

Porque uma produção movimenta o estoque em três direções diferentes:

- **Saída**: dá baixa nos insumos consumidos.
- **Entrada**: dá entrada no produto acabado.
- **Perda**: registra a perda prevista pela fórmula (refugo, evaporação etc.).

Ter tipos de movimento dedicados (em vez de reutilizar tipos de venda/compra) permite isolar a produção em relatórios, definir comportamento financeiro adequado (sem gerar nota nem título financeiro) e configurar permissões específicas.

### Posso cadastrar uma fórmula **sem itens do tipo Perda**?

Sim. Se a fórmula não tem perdas, o **movimento de Perda não é gerado** ao finalizar — o sistema só cria os movimentos de Entrada e Saída. Nesse caso, o tipo de movimento de Perda na produção pode ficar em branco.

### **Composição** vs **Embalagem** — qual a diferença prática?

Ambos são consumidos pelo movimento de **Saída** ao finalizar a produção. A separação serve para:

- **Relatórios**: identificar facilmente quanto foi gasto em matéria-prima vs. embalagem.
- **Análise de custo**: dimensionar a participação de cada componente.
- **Organização**: deixar a fórmula mais clara para quem revisa.

Funcionalmente, no movimento de saída, os dois entram juntos.

---

## 🏭 Operação

### Posso **alterar a fórmula** depois que ela tem produções vinculadas?

A fórmula pode ser editada, mas **as produções já criadas não são reprocessadas** — elas guardam uma cópia dos itens da fórmula no momento da criação. Alterações na fórmula só afetam **produções novas**.

### Posso **alterar quantidades** na produção depois de copiar da fórmula?

Sim — e essa é justamente a ideia. Os campos `Quantidade Real` (cabeçalho) e `Qtd. Real` (cada item dos ingredientes) existem para refletir o que **efetivamente** foi consumido/produzido, que pode ser diferente do previsto pela fórmula.

### A produção rendeu **menos** que o previsto. O que faço?

Ajuste a `Quantidade Real` no cabeçalho da produção. O sistema recalcula `Quantidade de Itens Produzidos` = `Quantidade Real` × `Fator de Conversão`, e o custo unitário do produto acabado será recalculado pela divisão `Total Custo dos Ingredientes / Quantidade de Itens Produzidos`.

### Posso **iniciar uma produção sem finalizar imediatamente**?

Sim. O ciclo é exatamente esse: `Iniciar Produção` registra `Início da Produção` e o status passa para `EM PRODUÇÃO`. A produção pode ficar nesse status pelo tempo necessário, e só vai para `FINALIZADO` (com geração dos movimentos) quando você acionar `Finalizar Produção`.

### Posso **reabrir uma produção já finalizada**?

**Não.** Uma vez que a produção está `FINALIZADO`, a única transição permitida é para `CANCELADO` — e só se os três movimentos vinculados forem cancelados antes. Para corrigir uma produção finalizada por engano, cancele-a e crie uma nova com os dados corretos.

### Posso **cancelar uma produção** que já gerou movimentos?

Sim, mas em duas etapas:

1. Vá na tela `Movimentação` (pesquisa F1) e cancele os três movimentos vinculados (Entrada, Saída e Perda).
2. Volte na tela `Produção de Produtos`, abra a produção e acione `Cancelar Produção`.

Se você tentar cancelar a produção sem antes cancelar os movimentos, o sistema bloqueia com a mensagem: *"Não é possível alterar status de produção com movimentos associados e não cancelados"*.

### Por que **não consigo recuperar** um movimento que foi gerado por uma produção?

Porque ele está **vinculado a uma produção**. O sistema bloqueia a recuperação para evitar inconsistências (movimento ativo em uma produção cancelada, por exemplo). Se precisar reativar, primeiro reverta o cancelamento na produção (não é possível) — em vez disso, crie uma nova produção/movimentos refletindo o estado correto.

---

## 💰 Custos

### Como o sistema calcula o **custo do produto acabado**?

```
Custo unitário = Total Custo dos Ingredientes / Quantidade de Itens Produzidos
```

- **Total Custo dos Ingredientes** = soma do `Total Custo` de todos os itens da produção (composição + embalagem + perda).
- **Quantidade de Itens Produzidos** = `Quantidade Real` × `Fator de Conversão`.

Esse custo unitário é o valor usado no movimento de Entrada do produto acabado, e a partir daí entra na [Atualização Automática de Custo](../atualizacao_de_custo_automatica.md) para compor o custo médio do produto.

### O custo dos insumos está **errado** no momento da finalização. Como corrigir?

Atualize o custo do insumo no `Cadastro de Produtos` (aba `Custos`) **antes** de finalizar a produção. O custo aparece na coluna `Custo Unitário` da aba `Ingredientes` da produção — se necessário, edite a linha do item para refletir o valor correto.

### **As perdas são incluídas no custo** do produto acabado?

Sim — o cálculo soma o `Total Custo` de **todos** os itens da produção (composição, embalagem **e** perda). Isso é consistente com a lógica contábil: a perda é parte do custo de produção (você comprou o insumo e ele se perdeu, esse custo precisa ser absorvido pelo produto que efetivamente foi produzido).

> 📝 Repare que o cabeçalho da produção também tem dois campos *de quantidade* — `Total Quantidade Ingredientes` (apenas itens do tipo `Composição`) e `Total Perdas` (apenas itens do tipo `Perda`). Esses campos são informativos sobre **quantidade**; o `Total Custo Ingredientes` segue uma regra diferente e soma o custo de todos os tipos.

### Posso ajustar o **custo médio** do produto acabado depois da produção?

O custo médio é recalculado automaticamente a cada movimento de entrada — incluindo o gerado pela produção. Se precisar de um ajuste manual, use a tela `Atualização de Custo` (pesquisa F1). Ver [Atualização Automática de Custo](../atualizacao_de_custo_automatica.md).

---

## 📦 Estoque

### Os insumos e o produto acabado precisam estar **no mesmo Local de Estoque**?

A produção usa o **mesmo Local de Estoque** e a **mesma Situação de Estoque** para os três movimentos. Se eles precisarem ficar em locais diferentes (ex.: matéria-prima no almoxarifado, produto acabado na expedição), faça uma **transferência** depois da produção, na própria tela de Movimentação.

### Posso produzir **com estoque negativo** dos insumos?

Depende da configuração do tipo de movimento de saída e das regras gerais de estoque do sistema. Se o tipo permite saída sem estoque, a produção é finalizada normalmente. Se não permite, a finalização falha com a mensagem padrão de saldo insuficiente. Configure conforme a política da empresa.

### A produção **reserva estoque** durante o processo?

Não há reserva automática durante o status `Em Produção`. Os insumos só são baixados de fato quando a produção é finalizada (pelo movimento de Saída).

---

## 🔗 Vínculos e auditoria

### Como localizar **todos os movimentos** gerados por uma produção?

Três caminhos:

1. **Aba `Movimento` da produção**: Entrada, Saída e Perda aparecem lado a lado.
2. **Tela `Movimentação`** (pesquisa F1): pesquise pelo `COD_VINCULO_INICIO` igual ao ID do movimento de Saída — os três aparecem.
3. **Pelo produto acabado**: o histórico de movimentos do produto traz a Entrada da produção; a partir dela, é possível navegar para os vinculados.

### Como saber, a partir de um **movimento**, se ele veio de uma produção?

Movimentos gerados por produção têm `TP_STATUS = Vinculado` (no caso da Saída) e o `COD_VINCULO_INICIO` apontando para o ID da Saída (nos três casos). Na tela de Movimentação, esses vínculos ficam visíveis e bloqueiam operações como recuperação.

### Os movimentos gerados aparecem em **relatórios fiscais**?

Depende da configuração do tipo de movimento. Por padrão, tipos usados em produção são configurados para **não emitir nota fiscal**, **não gerar duplicata/título financeiro** e ficar fora dos relatórios de venda/compra. Se aparecerem onde não deveriam, revise as flags do tipo de movimento (`Cadastro de Tipos de Movimento`).

---

## 🔐 Permissões

### Quais permissões preciso conceder?

Para cada usuário que vai operar Produção, em `Cadastro de Acessos` (pesquisa F1) habilite:

- Módulo `FORMULA PRODUCAO PRODUTO` (tela `143`) — permissões mínimas: `Pesquisar`, `Inserir`, `Alterar`.
- Módulo `PRODUCAO PRODUTOS` (tela `144`) — permissões mínimas: `Pesquisar`, `Inserir`, `Alterar`.
- `Excluir` apenas para usuários autorizados a remover registros.
- `Relatório nível 1/2/3` conforme política de acesso a relatórios.

### Quem **cadastra a fórmula** precisa ser o mesmo que **executa a produção**?

Não. É comum (e recomendado) que pessoas diferentes façam essas tarefas: o responsável técnico cadastra/atualiza a fórmula, e o operador da produção apenas executa. Conceda apenas `Pesquisar` em `FORMULA PRODUCAO PRODUTO` para os operadores que não devem alterar fórmulas.

---

## 🆘 Quando a produção **não deixa finalizar**

Se ao acionar `Finalizar Produção` o sistema retorna erro, percorra o checklist:

1. **Status atual** é `Em Produção`? (Não funciona em `Em Espera`, `Finalizado` ou `Cancelado`.)
2. **Empresa selecionada**?
3. **Os três tipos de movimento** estão preenchidos? (Se a fórmula tem itens de Perda, o tipo de Perda é obrigatório.)
4. Cada item da aba `Ingredientes` tem **Custo Unitário > 0** e **Total Custo > 0**?
5. **Quantidade de Itens Produzidos > 0**?
6. A produção **não tem ainda** movimentos vinculados?

Se todos os pontos estão OK e o erro persiste, copie a mensagem completa exibida pelo sistema e procure suporte com o número da produção e o usuário que tentou finalizar.

---

## 🔗 Documentos relacionados

- [Índice da subseção Produção](README.md)
- [Documentação completa](documentacao_producao.md)
- [Guia rápido](guia_rapido.md)
- [Documentação Movimentação (visão geral)](../documentacao_movimentacao.md)
- [Atualização Automática de Custo](../atualizacao_de_custo_automatica.md)

---

**Última atualização**: Abril de 2026
**Versão**: 1.0
**Público-alvo**: Usuários e administradores Sol.NET responsáveis por produção interna de produtos
