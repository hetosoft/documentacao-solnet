---
title: "Índice: Documentação Movimentação Sol.NET"
permalink: /Movimentacao/
---

# 📚 Documentação do Módulo Movimentação — Sol.NET

> 🚧 **Em reescrita.** O conteúdo anterior deste módulo foi descartado e está sendo refeito do zero, no mesmo padrão usado em [Financeiro](../Financeiro/) — uma página por tela, ancorada no código-fonte e em consultas ao banco. Novos documentos são listados aqui à medida que forem publicados. Dúvidas pontuais sobre telas ainda não cobertas podem ser respondidas pelo suporte Hetosoft.

---

## 📄 Documentos publicados

### Operação — onde os movimentos acontecem

- **[Movimentos](Movimentos/)** — trio operacional `Movimentos de Compras` (`201`), `Movimentos de Vendas` (`202`), `Outros Movimentos` (`203`). Subpasta com referência completa, perfil por tela e FAQ.

### 📥 Importar XML NF-e

Lançamento de entrada (e registro de saída de NF-e própria) a partir do XML recebido pela SEFAZ ou por arquivo. O fluxo padrão começa pela [Manifestação do Destinatário](../Fiscal/documentacao_manifestacao_destinatario.md) (módulo Fiscal); a importação e o lançamento na movimentação acontecem aqui.

- [Documentação Importar XML](documentacao_importar_xml.md) — `204`. Tela completa, sub-abas (`XML`, `Cabeçalho`, `Itens`, `Financeiro`, `Conferência`), vínculo de itens com produtos e os botões `Lançar NF-e`, `Lançar Parcial`, `Lançar Próprio`, `DANFE`.
- [Guia Rápido — Importar XML](guia_rapido_importar_xml.md) — checklist da rotina, mensagens de erro mais comuns e quando usar cada botão de lançamento.
- [FAQ — Importar XML](faq_importar_xml.md) — carregamento, vínculo de itens, lançamento e relação com a Manifestação.
- [Conferência de XML](documentacao_conferencia_xml.md) — habilitação por loja no `Cadastro de Empresas`, estados da conferência, aba `Conferência` dentro do `Importar XML` e interação com `Lançar NF-e` / `Lançar Parcial`.

### Configuração — o que define o comportamento da operação

- **[Tipos de Movimento](TiposDeMovimento/)** — `37`. Configura todas as regras herdadas pelos movimentos.
- [Transações de Estoque](documentacao_transacoes_de_estoque.md) — `33`. Define o efeito em cada camada de saldo.
- [Locais de Estoque](documentacao_locais_de_estoque.md) — `28`.
- [Tabela de Preço](documentacao_tabela_de_preco.md) — `27`.
- [Regras Cashback](documentacao_regras_cashback.md) — `124`.

### Consulta — saldos e histórico

- [Saldo Estoque](documentacao_saldo_estoque.md) — `78`.
- [Histórico de Movimentações](documentacao_historico_de_movimentacoes.md) — `205`.
- [Histórico de Produtos](documentacao_historico_de_produtos.md) — `206`.

### Operações auxiliares — disparam movimentos visíveis no trio `201/202/203`

- [Ajuste de Estoque](documentacao_ajuste_de_estoque.md) — `79`.
- **[Produção](Producao/)** — `Fórmulas de Produtos` (`143`) + `Produção de Produtos` (`144`).

---

> 💡 As telas `Pedido de Compra` (`64`), `Cadastro de Produtos` (`32`), Conferências (`209/210/211/220`) e os guias temáticos cross-tela (Atualização de Custo, Cashback no PDV, Preço de Venda, Tabela de Preço — Fallback) ainda estão em fila de reescrita.
