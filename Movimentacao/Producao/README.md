---
title: "Índice: Produção — Movimentação Sol.NET"
permalink: /Movimentacao/Producao/
---

# 📚 Documentação de Produção — Sol.NET

A produção interna do Sol.NET permite **cadastrar fórmulas** (receitas) e **executá-las**, disparando a criação automática dos movimentos de estoque correspondentes — saída dos insumos, entrada do produto acabado e (quando há) perda. Os movimentos disparados aparecem nas telas operacionais `Movimentos de Compras` (código `201`), `Movimentos de Vendas` (código `202`) ou `Outros Movimentos` (código `203`), conforme o Tipo de Movimento configurado para cada um. Esta seção concentra os dois cadastros centrais do fluxo.

## 📄 Documentos disponíveis

- [Cadastro de Fórmula de Produtos](documentacao_formulas_de_produtos.md) — tela `143`. Define a receita: produto acabado, ingredientes, perdas, proporção (Fator × Total).
- [Cadastro de Produção de Produtos](documentacao_producao_de_produtos.md) — tela `144`. Executa uma fórmula, registra início/fim e gera os três movimentos automáticos na finalização.

## 🔗 Veja também (fora da subpasta)

- [Cadastro de Tipos de Movimento](../TiposDeMovimento/) — define os tipos usados para entrada do acabado, saída dos insumos e perda.
- [Transações de Estoque](../documentacao_transacoes_de_estoque.md) — define o efeito de cada movimento nas camadas de saldo (Físico, Disponível etc.).
- [Saldo Estoque](../documentacao_saldo_estoque.md) — onde o efeito da produção é visível.

---

**Última atualização**: Maio de 2026
