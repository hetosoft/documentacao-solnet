---
title: "Índice: Trilhas operacionais — Sol.NET"
permalink: /Movimentacao/Trilhas/
---

# 🛤️ Trilhas operacionais — Sol.NET

## 🎯 Visão Geral

As **trilhas** são guias narrativos que atravessam **várias telas em sequência** para cobrir uma demanda real do dia a dia — uma entrada de NF-e completa, uma venda do começo ao fim, uma devolução, um ajuste com auditoria. Cada trilha mostra o caminho que liga as telas, o que esperar em cada etapa e onde os erros costumam aparecer.

> 💡 **Quando usar uma trilha vs. uma documentação de tela.** A documentação de cada tela responde "como esta tela funciona". A trilha responde "como cumpro esta demanda do começo ao fim". Use a trilha quando estiver executando uma tarefa real; volte para a documentação da tela quando precisar de detalhes específicos de um campo ou validação.

---

## 📄 Trilhas publicadas

| Trilha | Demanda que resolve | Telas envolvidas |
|---|---|---|
| [Entrada de NF-e completa](trilha_entrada_nfe.md) | Recebi uma NF-e do fornecedor — preciso manifestar, conferir, lançar e gerar o financeiro. | Manifestação (`401`) → Importar XML (`204`) → Conferência → Movimentos de Compras (`201`) |
| [Venda completa](trilha_venda_completa.md) | Quero vender, emitir documento fiscal e quitar — do orçamento ou venda direta até a baixa do título. | Movimentos de Vendas (`202`) → emissão fiscal → Quitação (`303`) |
| [Devolução de venda](trilha_devolucao_venda.md) | Cliente devolveu mercadoria — preciso registrar a volta no estoque, emitir fiscal de devolução e gerar crédito. | Movimentos de Vendas (`202`, consulta da venda original) → Outros Movimentos (`203`) |
| [Ajuste de estoque com auditoria](trilha_ajuste_estoque_auditoria.md) | Preciso corrigir saldo de produtos e conseguir auditar o ajuste depois. | Ajuste de Estoque (`79`) → Outros Movimentos (`203`) → Histórico de Produtos (`206`) / Transações de Estoque (`33`) |

---

## 📌 Como ler uma trilha

Cada trilha segue a mesma estrutura:

1. **Diagrama de fluxo** — mapa visual das telas pela ordem.
2. **Passos** — cada passo nomeia a tela, código F1 e o que fazer.
3. **O que esperar como resultado** — em estoque, financeiro e fiscal.
4. **Quando dá errado** — mensagens comuns e link para o [índice unificado de mensagens](../indice_mensagens.md).
5. **Para aprofundar** — links para a documentação completa das telas envolvidas.

---

## 🗺️ Outras formas de entrar

| Quer | Vá para |
|---|---|
| Entender o modelo mental antes de qualquer operação | [Visão geral do Sol.NET](../../visao_geral_sol_net.md) |
| Definir o vocabulário (Movimento, Tipo, Transação, Faturar, Quitar…) | [Glossário](../../glossario.md) |
| Resolver uma dúvida específica por tarefa ("Quero…") | [Índice por tarefa](../../quero.md) |
| Ler a referência completa do trio Movimentos `201/202/203` | [Movimentos — referência](../Movimentos/documentacao_movimentos.md) |
| Configurar como um Tipo de Movimento se comporta | [Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) |

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Usuários operacionais / Retaguarda / Suporte
