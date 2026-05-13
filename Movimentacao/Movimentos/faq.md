# ❓ FAQ — Movimentos - Sol.NET

Este FAQ concentra as **mensagens de validação** que aparecem ao lançar, finalizar, emitir fiscal, quitar e estornar movimentos, além das **perguntas mais frequentes** sobre comportamento do formulário. Para a referência completa, veja a [documentação](documentacao_movimentos.md). Para o panorama da seção, veja a [Visão Geral](README.md).

As validações abaixo se aplicam às três telas (`201` Compras, `202` Vendas, `203` Outros), porque todas usam o mesmo formulário. As mensagens aparecem em popup e o foco vai para o campo que causou o problema.

---

## 🛡️ Validações ao salvar / finalizar — guia de troubleshooting

### Cabeçalho — Tipo, Pessoa, Empresa

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Defina um Tipo de Movimento!"* | Tentou gravar sem selecionar um Tipo. | Cabeçalho → preencher `Tipo de Movimento`. |
| *"Empresa Não Permitida Para esse Tipo Movimento!"* | A Empresa selecionada não está autorizada no Tipo escolhido. | Trocar Empresa ou ajustar o Tipo em [Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) (`37`) → aba `Outras Operações → Empresa`. |
| *"Pessoa do Movimento Diferente da Pessoa da Chamada!"* | Vinculou uma `Chamada` cuja pessoa é diferente da pessoa do movimento. | Trocar a Chamada ou ajustar a pessoa. |

### Fiscal — CFOP, Chave de Acesso, Cidade

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"CFOP não é de entrada!"* | Tela `201` (Compras) com CFOP fora da faixa `1xxx/2xxx/3xxx`. | Ajustar a Natureza de Operação na Tipo de Movimento ou no Cabeçalho. |
| *"CFOP não é de saída!"* | Tela `202` (Vendas) com CFOP fora da faixa `5xxx/6xxx/7xxx`. | Idem. |
| *"CFOP não é dentro do estado!"* | Operação interna do estado (NFC-e típica) com CFOP interestadual/exterior. | Trocar Natureza de Operação. |
| *"CFOP não é dentro do estado! (NFC-e)"* | NFC-e exige CFOP `5xxx` (dentro do estado). | Ajustar Natureza de Operação. |
| *"CFOP não é fora do estado!"* | Inverso — esperava-se CFOP interestadual. | Idem. |
| *"CFOP não é Exterior(Internacional)!"* | Operação de importação/exportação com CFOP interno. | Usar CFOP `3xxx` ou `7xxx`. |
| *"Chave de Acesso Incorreta!"* | Chave de Acesso da NF referenciada está inválida (formato ou dígito verificador). | Recopiar a Chave do XML/DANFE original. |
| *"Chave de Acesso já Criada Edição Parcial!"* | Tentou editar campos travados em movimento já com NF-e autorizada. | Usar `Correção Manual` em modo de pesquisa, ou cancelar/estornar antes. |
| *"Cidade de Prestação sem Configuração de Tributação!"* | NFS-e sem configuração de tributação para a cidade do prestador. | Cadastro de Cidade (módulo Fiscal). |

### Itens

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Movimento sem item!"* | Tentou gravar/finalizar sem nenhum produto. | Sub-aba `Itens` → adicionar ao menos uma linha. |
| *"Empresa Não Permitida Para esse Tipo Movimento!"* (no item) | Produto não está autorizado para a Empresa/Tipo selecionados. | Cadastro do Produto / Tipo de Movimento. |
| *"Deletar Produto Linkado Só Individualmente!"* | Tentou apagar em lote produtos com vínculo (ex.: bundle, fórmula). | Apagar um a um. |
| *"Atualização de custo bloqueada para este tipo de movimento."* | Tentou recalcular custo num Tipo que não permite (ex.: Venda). | Operação só é válida em Tipos de Compra/Outros configurados. |
| *"Erro ao Atualizar Custo!"* / *"Erro ao Recalcular Preços!"* | Falha de cálculo (provavelmente saldo inconsistente, custo zerado, divisão por zero). | Conferir o produto em `Saldo Estoque` (`78`) e o histórico em `Histórico de Produtos` (`206`). |
| *"Alteraram o 'Custo' Antes de Voçê, Consulte a Nota de Novo!"* / *"Alteraram o 'Preço' Antes de Voçê, Consulte a Nota de Novo!"* | Outro usuário alterou custo/preço enquanto você editava o mesmo movimento. | Recarregar (consultar de novo) e refazer a alteração. |

### Caixa, Quitação e Portador

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Caixa Aberto. Fechamento Nº: ( ... )"* / *"Caixa Aberto. Turno Nº: ( ... )"* | Caixa do usuário/empresa está aberto e bloqueia a operação que você tentou (ou exige que esteja aberto e não está). | Abrir/fechar o Caixa em `Caixa Geral - operação` (módulo Financeiro). |
| *"Apenas Portador já impresso, podem ser limpo!"* | Tentou limpar portador de título não impresso. | Imprimir antes ou usar outro título. |
| *"Apenas títulos com status 'ABERTOS, CANCELADOS' podem ser limpo o portador!"* | Tentou limpar portador de título quitado/parcial. | Estornar a quitação antes (se aplicável). |
| *"Entrada inválida!"* / *"Entrada menor que o permitido"* / *"Entrada igual ou maior que o valor!"* | Valor de entrada na quitação fora dos limites configurados. | Ajustar o valor de entrada. |

### Devolução e Vínculos

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Não Permitido, Obrigatório Referenciar Nota! (Devolução)"* | Tipo `DEVOLUÇÃO` exige `Movimento Referenciado` e ele está vazio. | Cabeçalho → `Referenciar Nota`. |
| *"Não Permitido, Obrigatório Referenciar Nota da Mesma Empresa! (Devolução)"* | A NF referenciada pertence a outra empresa do grupo. | Selecionar uma NF da mesma empresa. |
| *"Chamada Obrigatório!"* | Tipo exige amarra com Chamada e ela está vazia. | Cabeçalho → vincular Chamada. |
| *"OS Obrigatório!"* / *"Empresa da 'OS' Diferente da 'OS-Requisição'!"* / *"Não Permitido, OS não Está em Aberto!"* | Validações de Ordem de Serviço vinculada — OS exigida, com mesma empresa e em aberto. | Aba `OS / Req.` — selecionar a OS correta. |

### Tipo de Movimento divergente em operações disparadas

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Tipo de Movimento diferente do tipo escolhido em Ajuste de Estoque!"* | Você lançou um movimento direto em `203` que conflita com um ajuste em andamento de outro Tipo. | Conferir o `Tipo` selecionado contra o configurado em [Ajuste de Estoque](../documentacao_ajuste_de_estoque.md) (`79`). |

### Erros genéricos

| Mensagem | Quando aparece |
|----------|----------------|
| *"Erro ao Agrupar Movimento!"* | Falha ao agrupar dois ou mais movimentos. Conferir compatibilidade dos movimentos (Tipos diferentes, status diferentes). |
| *"Erro ao Cadastrar o Cliente!"* | Cadastro automático de cliente (geralmente em integrações ou importações) falhou. Cadastrar manualmente em `Pessoas`. |
| *"Erro ao Calcular!"* | Falha de cálculo de totais (preço × quantidade × desconto × impostos). Conferir valores numéricos. |
| *"Erro ao Cancelar Financeiro!"* | Falha ao cancelar contas PR no estorno. Conferir se há quitação que precisa ser estornada primeiro. |
| *"Erro ao gerar parcelas!"* / *"Erro ao gerar parcelas com valor negativo!"* | Falha ao gerar parcelas a partir da Condição de Pagamento. Conferir valor total e condição. |
| *"Erro ao Excluir Crédito!"* | Falha ao excluir crédito de pessoa. Conferir se o crédito já foi usado em outro movimento. |
| *"Erro ao Gravar no Banco de Dados os Itens!"* | Falha de gravação no banco. Costuma indicar problema de conexão ou integridade. Reabrir o movimento e tentar de novo; se persistir, abrir chamado para o suporte. |

### Modo de operação

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Correção Manual permitido apenas em modo de Pesquisa"* | Tentou `Correção Manual` com o movimento já aberto em edição. | Fechar a edição, voltar à lista, selecionar o registro e acionar `Correção Manual` a partir dali. |
| *"Essa função só pode ser utilizada em modo de Busca!"* | Operação só faz sentido sobre uma lista de resultados, não sobre um movimento aberto. | Voltar à sub-aba de Consulta. |
| *"Escolha pelo menos Um(1) Movimento!"* | Operação em lote sem nada selecionado. | Selecionar ao menos uma linha. |

---

## ❓ Perguntas frequentes

### Por que três telas para o mesmo formulário?

Cada uma das telas (`201`, `202`, `203`) **filtra** os Tipos de Movimento disponíveis pelo `Comportamento` configurado em [Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) (`37`): Entrada → `201`; Saída → `202`; Outros → `203`. O formulário em si é o mesmo, e o detalhe da operação (sub-abas visíveis, campos exigidos, fluxos disparados) sai do Tipo escolhido, não da tela.

### O combo `Tipo de Movimento` não mostra o Tipo que preciso.

Verifique nesta ordem:
1. O Tipo está **Inativo**? → ative em `37`.
2. O Tipo tem `Comportamento` compatível com a tela aberta? → `201` exige Entrada, `202` exige Saída, `203` exige Outros.
3. O usuário tem permissão no **grupo de acesso** que inclui esse Tipo? → o controle é em telas de permissão fora deste cadastro; solicite ao administrador.

### O movimento foi gravado mas o saldo do produto não baixou.

A `Transação de Estoque` amarrada ao Tipo não está configurada para subtrair as camadas certas (`Físico`, `Disponível`). Abra [Transações de Estoque](../documentacao_transacoes_de_estoque.md) (`33`), localize a Transação amarrada ao Tipo do movimento e confira os marcadores. Verifique também o `Local de Estoque` informado no Cabeçalho — o saldo é por Local, e às vezes o que parece "não baixou" é "baixou no Local errado".

### Onde vejo o histórico completo de alterações deste movimento?

Em [Histórico de Movimentações](../documentacao_historico_de_movimentacoes.md) (`205`) — toda gravação, edição, finalização, mudança de Tipo, quitação, transmissão fiscal e estorno fica registrada com data, hora e usuário.

### Como repor um movimento estornado?

O estorno **não apaga** o movimento — ele apenas reverte o efeito (estoque, financeiro, fiscal). Para refazer, abra um **novo** movimento com os mesmos dados, ou (em casos específicos) acione `Mudar Tipo` (`F7`) sobre o estornado para mudar para um Tipo equivalente novo. Em hipótese alguma o estorno deve ser tratado como exclusão definitiva.

### O sistema bloqueia a edição porque a NF-e já foi autorizada — o que fazer?

Depende do que você precisa alterar:
- **Campos não-fiscais** (observação, vendedor adicional) → usar `Correção Manual` em modo de pesquisa.
- **Campos fiscais** (CFOP, alíquotas, produtos, valores) → emitir uma **Carta de Correção Eletrônica** (CC-e) quando aplicável (correções permitidas pela SEFAZ), **ou** cancelar a NF-e (dentro do prazo SEFAZ — geralmente 24h), estornar o movimento e refazer.

### A finalização está bloqueada porque o Caixa está aberto / fechado.

A mensagem é literal: o sistema diz se o Caixa precisa estar aberto e está fechado, ou se está aberto e precisa estar fechado. Abra ou feche o Caixa em `Caixa Geral - operação` (módulo Financeiro) conforme o que a mensagem indica.

### Quero ver só os movimentos de um cliente / período / Tipo específicos.

A sub-aba de Consulta (`Movimentos`) tem filtros por período de emissão, Pessoa, Tipo, status, Empresa, Local. Para filtros mais específicos ou repetidos, use **Pesquisa Salva** (sub-aba) para salvar a combinação e reusar.

### O movimento gerou parcelas com valores estranhos.

Conferir nesta ordem:
1. `Condição de Pagamento` no Cabeçalho — o número e os intervalos das parcelas saem dela.
2. `Descontos/Outras Despesas` — acréscimo/desconto no total redistribui as parcelas.
3. Edição manual na sub-aba `Financeiro → Parcelas` — alguém pode ter ajustado manualmente após a geração automática.

### O que significa o status `VINCULADO`?

Aparece quando o movimento foi origem de uma **Mudança Duplicar** (`F7` com o Tipo de destino configurado como `Duplicar` em `Tipos de Movimento → aba Mudar`) e o novo movimento gerado está ativo. O original fica **congelado** nesse status — não aceita novas operações até que o subsequente (o "duplicado") seja cancelado, momento em que volta a aceitar ações. A pilha de movimentos relacionados fica visível na sub-aba `Vínculos`. Veja [Mudar (F7)](documentacao_movimentos.md#mudar-bot%C3%A3o-mudar--f7) para o conceito completo.

---

## 🔗 Links

- [Visão Geral](README.md) — papel dos Movimentos no Sol.NET e mapa rápido.
- [Documentação](documentacao_movimentos.md) — referência completa do formulário (sub-abas, fluxos, atalhos).
- [Movimentos de Compras](movimentos_de_compras.md) · [Movimentos de Vendas](movimentos_de_vendas.md) · [Outros Movimentos](outros_movimentos.md).

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Usuários operacionais / Equipe de Suporte / Consultores de Implantação Sol.NET
