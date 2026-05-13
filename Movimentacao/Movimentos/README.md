---
title: "Índice: Movimentos — Movimentação Sol.NET"
permalink: /Movimentacao/Movimentos/
---

# 📚 Movimentos — Sol.NET

**Movimentos** é o coração operacional do módulo Movimentação: a tela onde toda transação de estoque com documento (compra recebida, venda emitida, transferência, devolução, ajuste, produção) é lançada, consultada, editada, finalizada, quitada e auditada. O Sol.NET expõe o mesmo formulário sob **três códigos** distintos na pesquisa universal, um por categoria:

- [Movimentos de Compras](movimentos_de_compras.md) — código `201` — entrada com documento fiscal de compra (notas de fornecedor, devoluções para fornecedor, importações).
- [Movimentos de Vendas](movimentos_de_vendas.md) — código `202` — Tipos acessados por **vendedores** (venda balcão, orçamento, pedido de venda, OS faturada). Vendas em frente de caixa acontecem na aplicação **PDV**, à parte, documentada em outra seção.
- [Outros Movimentos](outros_movimentos.md) — código `203` — Tipos operados pela **retaguarda**: **transferências entre filiais**, **devoluções de venda**, ajustes, perdas, produção, brindes, consumo interno.

Cada movimento amarra **um** [Tipo de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) (cadastro `37`) e dele herda todas as regras: efeito no estoque (via `Transações de Estoque` — `33`), efeito no financeiro, fiscal (modelo, série, CFOPs), Funcionários exigidos, Tabela de Preço aplicada, Local de Estoque padrão, Portador, Condição de Pagamento padrão, regras de mobile/devolução/cashback.

---

## 📄 Documentos desta seção

- [Movimentos — referência completa](documentacao_movimentos.md) — comportamento comum às três telas: mapa do formulário, sub-abas, fluxos principais (Lançar, Editar, Finalizar, Mudar, Quitar, Imprimir, Emitir NF-e, Estornar), atalhos validados, validações automáticas, exemplos práticos, telas relacionadas.
- [Movimentos de Compras](movimentos_de_compras.md) — particularidades da tela `201` (CFOPs de entrada, atualização de custo, importação de XML, devolução para fornecedor).
- [Movimentos de Vendas](movimentos_de_vendas.md) — particularidades da tela `202` (CFOPs de saída, ciclo Orçamento → Pedido → Venda, consulta de vendas vindas do PDV).
- [Outros Movimentos](outros_movimentos.md) — particularidades da tela `203` (transferências, ajustes, perdas, produção, brindes).
- [FAQ](faq.md) — perguntas frequentes e mensagens de validação ao salvar, finalizar e emitir fiscal.

---

## 🧭 Mapa rápido do formulário

O formulário se divide em duas grandes áreas:

| Área | O que tem |
|------|-----------|
| **Consulta** | Lista de movimentos lançados, com sub-abas: `Movimentos` (geral + Produtos / Pagamentos / Observações / Protocolo Fiscal / Entrega PDV), `Contas PR` (Registros / Renegociação / Detalhes / Cheque / Cartão / Crédito Pessoa Usado/Gerado), `OS / Req.`, `Agrupar`, `Vínculos`, `Parcial` (Movimento Parcial + Quitação Parcial), `Chamada`, `Crédito - Gerado`, `Pesquisa PDV`, `Pesquisa Salva`, `Comportamentos`. |
| **Lançamento** | Cabeçalho, Itens (com Totais / Tributação / ICMS/ST/IPI Livre / Pontos / Estoque do Produto / IVA), Campos Complementares, Descontos/Outras Despesas, Precificação (Custos / Preços / Buscador de Preço), Chamada, Cadastro/Fechamento, **Financeiro** (Contas / Parcelas / Rateio / Imagens / Forma de Pagamento), Entrega, Entrega PDV (para movimentos vindos do PDV), MDF-e, Itens Cancelados, Vencimento (controle de lote/validade dos produtos), Outras Operações. |

Quais sub-abas aparecem em cada movimento depende inteiramente do `Tipo de Movimento` selecionado no Cabeçalho.

---

## ⌨️ Atalhos validados (resumo)

| Tecla | Ação |
|-------|------|
| `F1` | Pesquisa universal de telas. |
| `F6` | Finalizar. |
| `F7` | Mudar (conversão automática entre Tipos). |
| `F8` | Quitar. |
| `F9` | Imprimir. |
| `F10` | Emitir NF-e / NFC-e / NFS-e. |
| `F11` | Estornar. |

Funcionam **fora** do modo de pesquisa. Mais detalhes na [referência completa](documentacao_movimentos.md#%EF%B8%8F-atalhos-validados).

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Usuários operacionais / Equipe de Suporte / Consultores de Implantação Sol.NET
