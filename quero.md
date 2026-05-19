---
title: "Quero… — Índice por tarefa"
permalink: /quero/
---

# 📄 Quero… — Índice por tarefa

## 🎯 Visão Geral

Índice **orientado à pergunta do usuário**, não à tela. Se você sabe **o que quer fazer** mas não tem certeza por onde começar, este é o atalho.

Cada entrada mostra a pergunta em primeira pessoa, a resposta curta e onde ir.

> 💡 Para entender o vocabulário usado nas respostas, abra o [Glossário](glossario.md). Para o modelo mental do sistema, comece pela [Visão geral](visao_geral_sol_net.md).

---

## 📦 Movimentação — estoque, vendas, compras

### Quero saber quanto tenho de um produto

→ Abra [Saldo Estoque](Movimentacao/documentacao_saldo_estoque.md) (`78`). Filtre por produto e/ou Local. Mostra todas as camadas (Físico, Disponível, Reservado etc.).

### Quero entender por que o saldo de um produto está errado

→ Abra [Histórico de Produtos](Movimentacao/documentacao_historico_de_produtos.md) (`206`). Lista cada movimento que tocou o saldo desse produto, em ordem. Combine com a [Trilha de auditoria de ajuste](Movimentacao/Trilhas/trilha_ajuste_estoque_auditoria.md) se a divergência for de ajuste manual.

### Quero lançar uma nota de entrada (compra com NF-e do fornecedor)

→ Siga a [Trilha de entrada de NF-e](Movimentacao/Trilhas/trilha_entrada_nfe.md) — passa por [Manifestação](Fiscal/documentacao_manifestacao_destinatario.md) → [Importar XML](Movimentacao/documentacao_importar_xml.md) → [Conferência](Movimentacao/documentacao_conferencia_xml.md) → [Movimentos de Compras](Movimentacao/Movimentos/movimentos_de_compras.md) (`201`).

### Quero faturar uma venda do começo ao fim

→ Siga a [Trilha de venda completa](Movimentacao/Trilhas/trilha_venda_completa.md) — pedido/orçamento → [Movimentos de Vendas](Movimentacao/Movimentos/movimentos_de_vendas.md) (`202`) → emissão fiscal → [Quitação](Financeiro/documentacao_quitacao.md).

### Quero fazer devolução de uma venda

→ Siga a [Trilha de devolução de venda](Movimentacao/Trilhas/trilha_devolucao_venda.md) — abre em [Outros Movimentos](Movimentacao/Movimentos/outros_movimentos.md) (`203`) com Tipo `Devolução de Venda` e Movimento Referenciado para a venda original.

### Quero estornar (cancelar) um movimento já finalizado

→ Na tela do Movimento (`201`/`202`/`203`), localize o registro e use `F11` ou o botão `Estornar`. Reverte estoque, financeiro e fiscal (se a SEFAZ permitir). Detalhes na [referência de Movimentos](Movimentacao/Movimentos/documentacao_movimentos.md) (seção `Estornar`).

### Quero ajustar saldo de um produto

→ Abra [Ajuste de Estoque](Movimentacao/documentacao_ajuste_de_estoque.md) (`79`). Para um ajuste rastreável com auditoria posterior, siga a [Trilha de ajuste com auditoria](Movimentacao/Trilhas/trilha_ajuste_estoque_auditoria.md).

### Quero ajustar o preço de venda de um produto

→ Abra [Tabela de Preço](Movimentacao/documentacao_tabela_de_preco.md) (`27`). Veja qual Tabela está vinculada ao Tipo de Movimento que você usa (na tela `Tipos de Movimento`, código `37`) e ajuste lá.

### Quero ver os totais de vendas (por dia, vendedor, portador, condição)

→ Abra [Histórico de Movimentações](Movimentacao/documentacao_historico_de_movimentacoes.md) (`205`) e filtre pelo período. As sub-abas agregam por data, mês, pessoa, tipo, portador, condição de pagamento, vendedor, operador e tabela de preço; a aba `Comissão` calcula comissão sobre vendas e devoluções.

### Quero entender uma mensagem de erro que apareceu

→ Veja o [Índice unificado de mensagens](Movimentacao/indice_mensagens.md). Lista mensagem por mensagem com causa provável e onde resolver.

### Quero saber por que meu Movimento gerou (ou não gerou) financeiro

→ Olhe o `Tipo de Movimento` que está sendo usado, em `37`. A flag `Gerar Lançamento Financeiro` (e configurações relacionadas) decide. Conceito mais amplo na [Visão geral — 3 dimensões](visao_geral_sol_net.md#-as-3-dimens%C3%B5es-de-qualquer-opera%C3%A7%C3%A3o).

### Quero saber por que meu Movimento não baixou o estoque

→ Olhe a `Transação de Estoque` amarrada ao Tipo do Movimento, em `33`. Confira as colunas `Físico` e `Disponível`. Local de Estoque no Cabeçalho também influencia — o saldo é por Local.

### Quero produzir um item a partir de uma fórmula

→ Abra [Produção de Produtos](Movimentacao/Producao/documentacao_producao_de_produtos.md) (`144`). A fórmula em si é cadastrada em [Fórmula de Produtos](Movimentacao/Producao/documentacao_formulas_de_produtos.md) (`143`).

### Quero configurar/ajustar cashback do PDV

→ Abra [Regras Cashback](Movimentacao/documentacao_regras_cashback.md) (`124`).

---

## 💰 Financeiro

### Quero quitar um título a pagar ou a receber

→ Abra [Quitação](Financeiro/documentacao_quitacao.md) (`303`) para quitação em lote ou pelo movimento de origem, ou abra o título em [Pagar e Receber](Financeiro/documentacao_pagar_e_receber.md) (`301`) e quite individualmente.

### Quero ver os títulos abertos de um cliente ou fornecedor

→ Abra [Pagar e Receber](Financeiro/documentacao_pagar_e_receber.md) (`301`) e filtre pela Pessoa.

### Quero operar o caixa do dia (abertura, lançamentos, fechamento)

→ Abra [Caixa Geral — operação](Financeiro/documentacao_caixa_geral_op.md) (`302`).

---

## 🏛️ Fiscal

### Quero manifestar (Ciência / Confirmação / Desconhecimento) uma NF-e que entrou

→ Abra [Manifestação do Destinatário](Fiscal/documentacao_manifestacao_destinatario.md) (`401`). É a primeira etapa antes de qualquer lançamento de entrada.

### Quero entender como Reforma Tributária (CBS/IBS) afeta minha operação

→ Leia [Reforma Tributária — Documentação](Fiscal/documentacao_reforma_tributaria.md) e o [Guia Rápido](Fiscal/guia_rapido_reforma_tributaria.md).

### Quero acertar a regra de ICMS para um estado/contexto

→ [Região ICMS Saída](Fiscal/documentacao_regiao_icms.md) (`93`) para ICMS regular; [Região ICMS ST Saída](Fiscal/documentacao_regiao_icms_st_saida.md) (`94`) para Substituição Tributária.

### Quero cadastrar uma nova Natureza de Operação (CFOP)

→ Abra [Natureza de Operação](Fiscal/documentacao_natureza_operacao.md) (`36`).

---

## 🏷️ Produtos

### Quero cadastrar um produto novo

→ Abra [Cadastro de Produtos](Produtos/documentacao_produtos.md) (`32`). Para a visão por checklist, use o [Guia Rápido](Produtos/guia_rapido.md).

### Quero saber por que o sistema diz que o código/descrição do produto já existe

→ Veja a [FAQ de Produtos](Produtos/faq.md) — seção sobre validação de código/descrição duplicada.

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Todos os usuários do Sol.NET
