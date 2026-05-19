# 📄 Índice unificado de mensagens - Sol.NET

## 🎯 Visão Geral

Índice consolidado das **mensagens de validação** que aparecem nas telas operacionais de Movimentação e nas telas relacionadas (Importar XML, Tipos de Movimento, Manifestação Fiscal). Use esta página quando uma mensagem aparecer e você não souber por onde começar a resolver.

> 💡 **Esta página é índice, não fonte primária.** A coluna `Detalhes` aponta para a FAQ ou documentação onde a mensagem é explicada em profundidade. Quando uma mensagem nova for adicionada a uma FAQ específica, adicione também uma linha aqui — só assim o índice continua útil.

**Cobertura desta primeira rodada:** mensagens das telas `201/202/203` (Movimentos), `37` (Tipos de Movimento), `204` (Importar XML) e mensagens relacionadas à Manifestação do Destinatário (`401`). Mensagens dos demais módulos (RH, Self Checkout, iFood, API Externa) entrarão em rodadas posteriores.

---

## 📑 Como ler a tabela

- **Mensagem** — texto exato (ou parte significativa) que aparece em popup ou no protocolo.
- **Onde aparece** — tela e momento (gravar, finalizar, vincular item etc.).
- **Causa provável** — o motivo mais comum.
- **Detalhes** — link para a FAQ/documentação onde o problema é explicado e resolvido.

---

## 🧾 Movimentos (`201/202/203`) — Cabeçalho, Tipo, Pessoa

| Mensagem | Onde aparece | Causa provável | Detalhes |
|---|---|---|---|
| `Defina um Tipo de Movimento!` | Movimentos — ao gravar | Cabeçalho sem Tipo selecionado. | [FAQ — Movimentos](Movimentos/faq.md#cabe%C3%A7alho--tipo-pessoa-empresa) |
| `Empresa Não Permitida Para esse Tipo Movimento!` | Movimentos — ao gravar | Empresa não autorizada no Tipo. | [FAQ — Movimentos](Movimentos/faq.md#cabe%C3%A7alho--tipo-pessoa-empresa) |
| `Pessoa do Movimento Diferente da Pessoa da Chamada!` | Movimentos — ao gravar | Chamada vinculada é de outra pessoa. | [FAQ — Movimentos](Movimentos/faq.md#cabe%C3%A7alho--tipo-pessoa-empresa) |
| `Chamada Obrigatório!` | Movimentos — ao finalizar | Tipo exige Chamada amarrada. | [FAQ — Movimentos](Movimentos/faq.md#devolu%C3%A7%C3%A3o-e-v%C3%ADnculos) |
| `OS Obrigatório!` / `Empresa da 'OS' Diferente da 'OS-Requisição'!` / `Não Permitido, OS não Está em Aberto!` | Movimentos — ao finalizar | Validações de Ordem de Serviço vinculada. | [FAQ — Movimentos](Movimentos/faq.md#devolu%C3%A7%C3%A3o-e-v%C3%ADnculos) |

---

## 📦 Movimentos — Itens

| Mensagem | Onde aparece | Causa provável | Detalhes |
|---|---|---|---|
| `Movimento sem item!` | Movimentos — ao gravar/finalizar | Sub-aba `Itens` vazia. | [FAQ — Movimentos](Movimentos/faq.md#itens) |
| `Deletar Produto Linkado Só Individualmente!` | Movimentos — ao excluir itens em lote | Item com vínculo (bundle, fórmula). | [FAQ — Movimentos](Movimentos/faq.md#itens) |
| `Atualização de custo bloqueada para este tipo de movimento.` | Movimentos — ao recalcular custo | Tipo de venda (não permite atualizar custo). | [FAQ — Movimentos](Movimentos/faq.md#itens) |
| `Erro ao Atualizar Custo!` / `Erro ao Recalcular Preços!` | Movimentos — ao recalcular | Saldo inconsistente, custo zero, divisão por zero. | [FAQ — Movimentos](Movimentos/faq.md#itens) |
| `Alteraram o 'Custo' Antes de Voçê, Consulte a Nota de Novo!` / `Alteraram o 'Preço' …` | Movimentos — ao gravar edição | Outro usuário alterou no mesmo movimento. | [FAQ — Movimentos](Movimentos/faq.md#itens) |

---

## 🏛️ Movimentos — Fiscal (CFOP, Chave de Acesso)

| Mensagem | Onde aparece | Causa provável | Detalhes |
|---|---|---|---|
| `CFOP não é de entrada!` | `201` — ao finalizar | CFOP fora da faixa `1xxx/2xxx/3xxx`. | [FAQ — Movimentos](Movimentos/faq.md#fiscal--cfop-chave-de-acesso-cidade) |
| `CFOP não é de saída!` | `202` — ao finalizar | CFOP fora da faixa `5xxx/6xxx/7xxx`. | [FAQ — Movimentos](Movimentos/faq.md#fiscal--cfop-chave-de-acesso-cidade) |
| `CFOP não é dentro do estado!` / `CFOP não é dentro do estado! (NFC-e)` | Movimentos — ao finalizar | NFC-e ou operação interna com CFOP interestadual. | [FAQ — Movimentos](Movimentos/faq.md#fiscal--cfop-chave-de-acesso-cidade) |
| `CFOP não é fora do estado!` | Movimentos — ao finalizar | Esperava interestadual; informou interno. | [FAQ — Movimentos](Movimentos/faq.md#fiscal--cfop-chave-de-acesso-cidade) |
| `CFOP não é Exterior(Internacional)!` | Movimentos — ao finalizar | Importação/exportação com CFOP interno. | [FAQ — Movimentos](Movimentos/faq.md#fiscal--cfop-chave-de-acesso-cidade) |
| `Chave de Acesso Incorreta!` | Movimentos — ao referenciar nota | Chave inválida (formato ou dígito verificador). | [FAQ — Movimentos](Movimentos/faq.md#fiscal--cfop-chave-de-acesso-cidade) |
| `Chave de Acesso já Criada Edição Parcial!` | Movimentos — ao editar | Tentou editar campo travado em movimento com NF-e autorizada. | [FAQ — Movimentos](Movimentos/faq.md#fiscal--cfop-chave-de-acesso-cidade) |
| `Cidade de Prestação sem Configuração de Tributação!` | Movimentos — ao finalizar NFS-e | Cidade do prestador sem configuração de tributação. | [FAQ — Movimentos](Movimentos/faq.md#fiscal--cfop-chave-de-acesso-cidade) |

---

## 💰 Movimentos — Caixa, Portador, Quitação

| Mensagem | Onde aparece | Causa provável | Detalhes |
|---|---|---|---|
| `Caixa Aberto. Fechamento Nº: ( … )` / `Caixa Aberto. Turno Nº: ( … )` | Movimentos — ao finalizar | Caixa precisa estar aberto/fechado e está no estado oposto. | [FAQ — Movimentos](Movimentos/faq.md#caixa-quita%C3%A7%C3%A3o-e-portador) |
| `Apenas Portador já impresso, podem ser limpo!` | Movimentos — ao limpar portador | Tentou limpar portador de título não impresso. | [FAQ — Movimentos](Movimentos/faq.md#caixa-quita%C3%A7%C3%A3o-e-portador) |
| `Apenas títulos com status 'ABERTOS, CANCELADOS' podem ser limpo o portador!` | Movimentos — ao limpar portador | Título quitado/parcial. | [FAQ — Movimentos](Movimentos/faq.md#caixa-quita%C3%A7%C3%A3o-e-portador) |
| `Entrada inválida!` / `Entrada menor que o permitido` / `Entrada igual ou maior que o valor!` | Movimentos — ao quitar | Valor de entrada fora dos limites. | [FAQ — Movimentos](Movimentos/faq.md#caixa-quita%C3%A7%C3%A3o-e-portador) |

---

## 🔄 Movimentos — Devolução

| Mensagem | Onde aparece | Causa provável | Detalhes |
|---|---|---|---|
| `Não Permitido, Obrigatório Referenciar Nota! (Devolução)` | Movimentos — ao finalizar devolução | Tipo Devolução sem `Movimento Referenciado`. | [FAQ — Movimentos](Movimentos/faq.md#devolu%C3%A7%C3%A3o-e-v%C3%ADnculos) · [Trilha de devolução](Trilhas/trilha_devolucao_venda.md) |
| `Não Permitido, Obrigatório Referenciar Nota da Mesma Empresa! (Devolução)` | Movimentos — ao finalizar devolução | Referência aponta para nota de outra empresa. | [FAQ — Movimentos](Movimentos/faq.md#devolu%C3%A7%C3%A3o-e-v%C3%ADnculos) · [Trilha de devolução](Trilhas/trilha_devolucao_venda.md) |

---

## 🛠️ Movimentos — Operação e auxiliares

| Mensagem | Onde aparece | Causa provável | Detalhes |
|---|---|---|---|
| `Correção Manual permitido apenas em modo de Pesquisa` | Movimentos | Tentou Correção Manual com movimento aberto em edição. | [FAQ — Movimentos](Movimentos/faq.md#modo-de-opera%C3%A7%C3%A3o) |
| `Essa função só pode ser utilizada em modo de Busca!` | Movimentos | Operação só vale sobre a lista, não sobre um movimento aberto. | [FAQ — Movimentos](Movimentos/faq.md#modo-de-opera%C3%A7%C3%A3o) |
| `Escolha pelo menos Um(1) Movimento!` | Movimentos — operação em lote | Nada selecionado. | [FAQ — Movimentos](Movimentos/faq.md#modo-de-opera%C3%A7%C3%A3o) |
| `Tipo de Movimento diferente do tipo escolhido em Ajuste de Estoque!` | `203` — ao lançar | Lançamento direto conflita com ajuste em andamento. | [FAQ — Movimentos](Movimentos/faq.md#tipo-de-movimento-divergente-em-opera%C3%A7%C3%B5es-disparadas) |

### Erros genéricos (gravação, integridade, cálculo)

| Mensagem | Detalhes |
|---|---|
| `Erro ao Agrupar Movimento!` | [FAQ — Movimentos](Movimentos/faq.md#erros-gen%C3%A9ricos) |
| `Erro ao Cadastrar o Cliente!` | [FAQ — Movimentos](Movimentos/faq.md#erros-gen%C3%A9ricos) |
| `Erro ao Calcular!` | [FAQ — Movimentos](Movimentos/faq.md#erros-gen%C3%A9ricos) |
| `Erro ao Cancelar Financeiro!` | [FAQ — Movimentos](Movimentos/faq.md#erros-gen%C3%A9ricos) |
| `Erro ao gerar parcelas!` / `Erro ao gerar parcelas com valor negativo!` | [FAQ — Movimentos](Movimentos/faq.md#erros-gen%C3%A9ricos) |
| `Erro ao Excluir Crédito!` | [FAQ — Movimentos](Movimentos/faq.md#erros-gen%C3%A9ricos) |
| `Erro ao Gravar no Banco de Dados os Itens!` | [FAQ — Movimentos](Movimentos/faq.md#erros-gen%C3%A9ricos) |

---

## 📥 Importar XML (`204`)

### Carregamento

| Mensagem | Causa provável | Detalhes |
|---|---|---|
| `Arquivo XML Inválido!` | Arquivo corrompido, modelo errado (NFC-e/CT-e/NFS-e/MDF-e), salvo como texto, alterado manualmente. | [FAQ — Importar XML](faq_importar_xml.md#-por-que-aparece-arquivo-xml-inv%C3%A1lido) |
| `Chave de Acesso já Cadastrada!` | XML já carregado (por outro usuário, pela Manifestação ou em segundo plano). | [FAQ — Importar XML](faq_importar_xml.md#-aparece-chave-de-acesso-j%C3%A1-cadastrada-mas-eu-n%C3%A3o-importei-essa-nota-por-qu%C3%AA) |
| `( razão social ) NÃO É SUA EMPRESA!` | CNPJ do destinatário no XML não bate com nenhuma loja cadastrada. | [FAQ — Importar XML](faq_importar_xml.md#--raz%C3%A3o-social--n%C3%83o-%C3%89-sua-empresa--o-que-isso-significa) |
| `Pessoa não cadastrada!` ao vincular item | Fornecedor do XML não está no cadastro de pessoas. | [Documentação Importar XML](documentacao_importar_xml.md#erros-de-carregamento-comuns) |

### Vínculo de itens

| Mensagem | Causa provável | Detalhes |
|---|---|---|
| `Não Existe Nenhum Item com Vinculo!` | Lançamento bloqueado enquanto houver item sem vínculo. | [Documentação Importar XML](documentacao_importar_xml.md#coluna-conf-no-grid-de-itens) |
| `Não Permitido, Tipo Serviço!` | Item vinculado a produto cadastrado como Serviço. | [FAQ — Importar XML](faq_importar_xml.md#-n%C3%A3o-permitido-tipo-servi%C3%A7o-ao-vincular-item--o-que-fazer) |
| `Não Permitido, Produto configurado para desagregação!` | Produto marcado para desagregação tem fluxo próprio. | [FAQ — Importar XML](faq_importar_xml.md#-n%C3%A3o-permitido-produto-configurado-para-desagrega%C3%A7%C3%A3o--por-que-aparece) |
| `Não Permitido, Vinculo de produto linkado!` | Configuração geral proíbe vincular produtos linkados. | [Documentação Importar XML](documentacao_importar_xml.md#regras-e-bloqueios-no-v%C3%ADnculo) |
| `Produto Linkado Selecionado!` | Aviso (não bloqueio) — vinculou produto linkado em configuração que permite. | [Documentação Importar XML](documentacao_importar_xml.md#regras-e-bloqueios-no-v%C3%ADnculo) |

### Lançamento

| Mensagem | Causa provável | Detalhes |
|---|---|---|
| `Não Permitido! Somente Emissão PROPRIA.` | Usou `Lançar Próprio` em NF-e de terceiros. | [FAQ — Importar XML](faq_importar_xml.md#-tentei-lan%C3%A7ar-pr%C3%B3prio-e-apareceu-somente-emiss%C3%A3o-propria-o-que-fazer) |
| `Movimentação Cancelada! Lançar NF-e Novamente.` | Movimento vinculado foi cancelado; vínculo é desfeito automaticamente. | [Documentação Importar XML](documentacao_importar_xml.md#lan%C3%A7ar-pr%C3%B3prio) |
| `Movimentação Excluida! Lançar NF-e Novamente.` | Movimento vinculado foi excluído. | [FAQ — Importar XML](faq_importar_xml.md#-lancei-o-xml-mas-vi-que-o-movimento-foi-exclu%C3%ADdo-depois-o-v%C3%ADnculo-ainda-existe) |
| `Diferença de Custo de X%` | Aviso (não bloqueio) — custo do XML difere do cadastrado acima do percentual configurado. | [FAQ — Importar XML](faq_importar_xml.md#-aparece-diferen%C3%A7a-de-custo-de-x-no-lan%C3%A7amento-devo-cancelar) |

---

## ⚙️ Tipos de Movimento (`37`) — validações ao salvar

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Tipos de Movimento` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nesta tela.

### Identificação e Conta

| Mensagem | Causa | Detalhes |
|---|---|---|
| `Esse tipo de conta só pode ser Analítica!` | Tipo Sintética com Complemento preenchido. | [FAQ — Tipos](TiposDeMovimento/faq.md#identifica%C3%A7%C3%A3o-e-conta-aba-dados-cadastrais) |
| `Esse tipo de conta só pode ser Sintética!` | Tipo Analítica sem Complemento. | [FAQ — Tipos](TiposDeMovimento/faq.md#identifica%C3%A7%C3%A3o-e-conta-aba-dados-cadastrais) |

### Fiscal

| Mensagem | Causa | Detalhes |
|---|---|---|
| `Tipo Emissão Terceiro não permitido… ( … )!` | Tipo Emissão Terceiro com sequência incompatível. | [FAQ — Tipos](TiposDeMovimento/faq.md#fiscal-aba-cabe%C3%A7alho--fiscal) |
| `Não Permitido, CFOP em Natureza de Op. Não é de entrada!` / `Não é de Saída!` | Comportamento × CFOP da Natureza incompatíveis. | [FAQ — Tipos](TiposDeMovimento/faq.md#fiscal-aba-cabe%C3%A7alho--fiscal) |
| `Selecione ao menos uma série!` / `Selecione ao menos uma série padrão!` / `série padrão tem que está selecionada!` | Configuração de série fiscal incompleta. | [FAQ — Tipos](TiposDeMovimento/faq.md#fiscal-aba-cabe%C3%A7alho--fiscal) |
| `Tipos de Séries (Fiscal/Não Fiscal) devem ser iguais Ao Tipo do Modelo de Documento!` | Série fiscal × Modelo não fiscal (ou vice-versa). | [FAQ — Tipos](TiposDeMovimento/faq.md#fiscal-aba-cabe%C3%A7alho--fiscal) |
| `Série RPS e Série Lote é Obrigatório para NFS-e!` | Modelo NFS-e exige as duas séries adicionais. | [FAQ — Tipos](TiposDeMovimento/faq.md#fiscal-aba-cabe%C3%A7alho--fiscal) |
| `Obrigatório marcar a Tag Consumo em Outras Operações para o Modelo de Documento selecionado.` | Cupom Fiscal exige flag `Consumo`. | [FAQ — Tipos](TiposDeMovimento/faq.md#fiscal-aba-cabe%C3%A7alho--fiscal) |

### Estoque, Tabela de Preço, Custo

| Mensagem | Causa | Detalhes |
|---|---|---|
| `Não Permitido, Obrigatório Local de Estoque!` / `Obrigatório Transação de Estoque!` | Tipo que movimenta estoque sem Local/Transação padrão. | [FAQ — Tipos](TiposDeMovimento/faq.md#estoque-aba-itens--estoque) |
| `Não Permitido, '…' Sem Transação de Estoque!` | `Estatística de Estoque` ou `Baixar Quantidade na Promoção` sem Transação. | [FAQ — Tipos](TiposDeMovimento/faq.md#estoque-aba-itens--estoque) |
| `Selecione 'Vender Sem Estoque'!` | Tipo com Transação sem definir Sim/Não. | [FAQ — Tipos](TiposDeMovimento/faq.md#estoque-aba-itens--estoque) |
| `Não permitido, Selecione uma forma de buscar o preço! Selecione uma Tabela de Preço!` | Nenhuma Tabela com `OPCAO = 1` marcada. | [FAQ — Tipos](TiposDeMovimento/faq.md#tabela-de-pre%C3%A7o-aba-itens--tabela-de-pre%C3%A7o) |
| `Não permitido, selecione uma Tabela de Preço Padrão!` | Tabelas marcadas, nenhuma é Padrão. | [FAQ — Tipos](TiposDeMovimento/faq.md#tabela-de-pre%C3%A7o-aba-itens--tabela-de-pre%C3%A7o) |
| `Não permitido, '…Atualizar Custo Automático', Somente para Compras/Outros!` | Flag em Tipo de Vendas. | [FAQ — Tipos](TiposDeMovimento/faq.md#quantidade-e-custo-aba-itens--quantidade) |

### Devolução / Crédito / Origem-Destino

| Mensagem | Causa | Detalhes |
|---|---|---|
| `Não permitido, '…Devolução…' Em uma devolução!` / `…Não é devolução!` | Flags de devolução inconsistentes. | [FAQ — Tipos](TiposDeMovimento/faq.md#devolu%C3%A7%C3%A3o-e-cr%C3%A9dito-aba-outras-opera%C3%A7%C3%B5es--sistema) |
| `Não permitido, Sem '…Devolução Crédito…'!` / `'…Devolução Crédito…' se não gerar Crédito!` | Combinação flags de devolução × crédito incoerente. | [FAQ — Tipos](TiposDeMovimento/faq.md#devolu%C3%A7%C3%A3o-e-cr%C3%A9dito-aba-outras-opera%C3%A7%C3%B5es--sistema) |
| `Não permitido, 'Quitar Crédito Automaticamente' se não gerar Crédito!` / `se não for Tipo de Mov. 'PDV'!` | `Quitar Crédito Automaticamente` exige PDV + gerar crédito. | [FAQ — Tipos](TiposDeMovimento/faq.md#devolu%C3%A7%C3%A3o-e-cr%C3%A9dito-aba-outras-opera%C3%A7%C3%B5es--sistema) |
| `Não permitido, 'Empresa' Destino do Movimento do Tipo Pessoa!` | Tipo Destino Empresa em configuração que espera Pessoa. | [FAQ — Tipos](TiposDeMovimento/faq.md#origem--destino-aba-cabe%C3%A7alho--origemdestino) |
| `Não permitido, Preencher 'Empresa'!` / `Não Preenchido 'Empresa'!` | Incoerência entre `Tipo Empresa Destino` e empresa selecionada. | [FAQ — Tipos](TiposDeMovimento/faq.md#origem--destino-aba-cabe%C3%A7alho--origemdestino) |
| `Não Permitido Credito pessoa para Tipo de Movimento com Destino à Empresas!` | Crédito pessoa ✕ destino Empresa. | [FAQ — Tipos](TiposDeMovimento/faq.md#origem--destino-aba-cabe%C3%A7alho--origemdestino) |

### PDV / Funcionários / Memorizar / OS

| Mensagem | Causa | Detalhes |
|---|---|---|
| `Não permitido, Não Consultar em Lancamento para Tipo de Mov. 'PDV'!` | Tipo PDV não pode ter `Não Consultar`. | [FAQ — Tipos](TiposDeMovimento/faq.md#pdv-e-comportamento-aba-outras-opera%C3%A7%C3%B5es--sistema) |
| `Não Permitido, '…Memorizar Vendedor…' com a opção '…Vínculo com Usuário…'!` | Memorizar Vendedor ✕ Vínculo Usuário. | [FAQ — Tipos](TiposDeMovimento/faq.md#pdv-e-comportamento-aba-outras-opera%C3%A7%C3%B5es--sistema) |
| `Não Permitido, '…Memorizar Vendedor…' com a opção 'Funcionário Padrão'!` | Memorizar Vendedor ✕ Funcionário Padrão. | [FAQ — Tipos](TiposDeMovimento/faq.md#pdv-e-comportamento-aba-outras-opera%C3%A7%C3%B5es--sistema) |
| `Não Permitido, '…Permitir Tipo Mov…' com a opção '…Devolução Crédito…'!` | Incompatibilidade. | [FAQ — Tipos](TiposDeMovimento/faq.md#pdv-e-comportamento-aba-outras-opera%C3%A7%C3%B5es--sistema) |
| `Não Permitido, '…Permitir Financeiro Aberto…' com a opção '…Devolução Crédito…'!` | Incompatibilidade. | [FAQ — Tipos](TiposDeMovimento/faq.md#pdv-e-comportamento-aba-outras-opera%C3%A7%C3%B5es--sistema) |
| `Não Permitido, '…Movimento Parcial…' com a opção 'Venda Parcial'!` | Incompatibilidade. | [FAQ — Tipos](TiposDeMovimento/faq.md#pdv-e-comportamento-aba-outras-opera%C3%A7%C3%B5es--sistema) |
| `Não Permitido!, A Opção 'SEPARAR ITENS DO MOVIMENTO (Global)' Esta Ativada em Configuração Geral.` | Configuração global da empresa bloqueia. | [FAQ — Tipos](TiposDeMovimento/faq.md#pdv-e-comportamento-aba-outras-opera%C3%A7%C3%B5es--sistema) |
| `Não Permitido!, A Opção 'Promoção com Atualização em Grupo (MAIOR= ou A CADA)' Esta Ativada em Configuração Geral.` | Configuração global. | [FAQ — Tipos](TiposDeMovimento/faq.md#pdv-e-comportamento-aba-outras-opera%C3%A7%C3%B5es--sistema) |
| `Não permitido! '…OS…' e '…OS Requisição…' ao mesmo tempo.` | Tipo não pode ser OS e OS Requisição simultaneamente. | [FAQ — Tipos](TiposDeMovimento/faq.md#os--os-requisi%C3%A7%C3%A3o-aba-outras-opera%C3%A7%C3%B5es--sistema) |

### Financeiro / Funcionário

| Mensagem | Causa | Detalhes |
|---|---|---|
| `Plano de Contas e Centro de Custo Obrigatório para Tipo de Movimento com Financeiro!` | `Gerar Lançamento` ativo sem Plano/Centro padrão. | [FAQ — Tipos](TiposDeMovimento/faq.md#financeiro-aba-financeiro--financeiro-1) |
| `Não permitido, 'Não Estornar Financeiro', Somente para Compras/Outros!` | Flag em Tipo de Saída (só vale para Entrada/Outros). | [FAQ — Tipos](TiposDeMovimento/faq.md#financeiro-aba-financeiro--financeiro-1) |
| `…Só permitido para Funcionário!` | Configuração só faz sentido com funcionário. | [FAQ — Tipos](TiposDeMovimento/faq.md#funcion%C3%A1rio-e-outros) |
| `Obrigatório Editar 'Chave Protocolo'!` | Configuração de protocolo exige edição manual. | [FAQ — Tipos](TiposDeMovimento/faq.md#funcion%C3%A1rio-e-outros) |

---

## 📨 Ajuste de Estoque (`79`) e telas auxiliares

| Mensagem | Onde aparece | Causa | Detalhes |
|---|---|---|---|
| `Ajuste de Estoque sem Produtos!` | `79` — ao criar ajustes | Grid vazia. | [Ajuste de Estoque](documentacao_ajuste_de_estoque.md#valida%C3%A7%C3%B5es-autom%C3%A1ticas) |
| `Não Permitido! Só Status Aberto.` | `79` — ao editar | Tentou editar ajuste já processado. | [Ajuste de Estoque](documentacao_ajuste_de_estoque.md#valida%C3%A7%C3%B5es-autom%C3%A1ticas) · [Trilha de ajuste](Trilhas/trilha_ajuste_estoque_auditoria.md) |
| `Produto Configurado para 'Não Movimentar Estoque'!` | `79` — ao adicionar produto | Produto marcado para não movimentar no cadastro. | [Ajuste de Estoque](documentacao_ajuste_de_estoque.md#valida%C3%A7%C3%B5es-autom%C3%A1ticas) |
| `Não Permitido, Quantidade Máxima Excedida (999.999,99)!` | `79` — contagem | Valor acima do limite. | [Ajuste de Estoque](documentacao_ajuste_de_estoque.md#valida%C3%A7%C3%B5es-autom%C3%A1ticas) |
| `Só com Status 'ABERTO'` | `79` — ao excluir | Ajuste processado é imutável. | [Ajuste de Estoque](documentacao_ajuste_de_estoque.md#ao-excluir-um-ajuste) |
| `Não permitido, Existe Movimento(s) Vinculado!` | `79` — ao excluir | Há movimentos gerados a partir do ajuste. | [Ajuste de Estoque](documentacao_ajuste_de_estoque.md#ao-excluir-um-ajuste) |

---

## 🏛️ Manifestação do Destinatário (`401`) e NF-e SEFAZ

Mensagens vindas da SEFAZ (rejeições) aparecem no protocolo da NF-e (sub-aba `Protocolo Fiscal` em Movimentos) ou no log da Manifestação. Causas mais frequentes em ambiente real:

| Tipo de rejeição | Causa típica | Onde resolver |
|---|---|---|
| Chave de Acesso inválida | Chave malformada ou já cancelada/inutilizada na SEFAZ. | Conferir DANFE/XML; pedir reemissão. |
| Inscrição Estadual do destinatário inválida | IE do cadastro de Pessoa errada ou desabilitada. | Atualizar IE no `Cadastro de Pessoas`. |
| CFOP inconsistente com a operação | CFOP no movimento não combina com sentido da operação (entrada/saída/interno/interestadual). | Ajustar [Natureza de Operação](../Fiscal/documentacao_natureza_operacao.md) ou Tipo de Movimento. |
| NCM inválido / Tributação inconsistente | Produto sem NCM, ou NCM/CST/CSOSN não bate com cadastro fiscal. | [Cadastro de NCM](../Fiscal/documentacao_ncm.md) e cadastro do Produto. |
| Documento referenciado obrigatório (devolução) | Falta NF original referenciada na devolução. | Referenciar a NF original no Cabeçalho. Ver [Trilha de devolução](Trilhas/trilha_devolucao_venda.md). |

Para o cenário e a interface da Manifestação, ver a [documentação dedicada](../Fiscal/documentacao_manifestacao_destinatario.md) e o [FAQ da Manifestação](../Fiscal/faq_manifestacao_destinatario.md).

---

## 🔗 Páginas-fonte

- [FAQ — Movimentos (`201/202/203`)](Movimentos/faq.md)
- [FAQ — Tipos de Movimento (`37`)](TiposDeMovimento/faq.md)
- [FAQ — Importar XML (`204`)](faq_importar_xml.md)
- [FAQ — Manifestação do Destinatário (`401`)](../Fiscal/faq_manifestacao_destinatario.md)
- [Documentação — Ajuste de Estoque (`79`)](documentacao_ajuste_de_estoque.md)

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Operação / Retaguarda / Suporte
