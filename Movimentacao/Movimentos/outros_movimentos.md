# 📄 Outros Movimentos - Sol.NET

## 🎯 Visão Geral

`Outros Movimentos` concentra os Tipos de Movimento operados pela **retaguarda/almoxarifado** — fluxos que não são compra fiscal de fornecedor (`201`) nem venda de vendedor (`202`): **transferências entre filiais/locais**, **devoluções de venda**, ajustes de inventário, perdas, consumo interno, brindes, amostras grátis, entradas/saídas disparadas por `Pedido de Compra` ou `Produção`, doações.

> 💡 É comum a devolução de venda parecer que "deveria estar em Vendas" — afinal, é uma venda voltando. A regra do Sol.NET segue o **operador**, não o sentido fiscal: devolução de venda é operada pela retaguarda (conferindo o que voltou, ajustando estoque, gerando crédito), por isso fica aqui.

A tela compartilha o mesmo formulário operacional usado em `Movimentos de Compras` (`201`) e `Movimentos de Vendas` (`202`), mas **filtra os Tipos de Movimento disponíveis** para aqueles configurados em [Cadastro de Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) (`37`) como movimentos de retaguarda (tipicamente Comportamento `Outros`; devolução de venda configurada como Entrada também recai aqui quando o Tipo é operacional, não de vendedor).

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Outros Movimentos |
| **Código (`F1`)** | `203` |

Abra a pesquisa universal (`F1`) e digite `203` ou parte do nome **Outros Movimentos**.

---

## 🧭 Particularidades do modo Outros

A categoria `Outros` é a mais **heterogênea** das três — cada Tipo aqui costuma ter sua configuração própria em `37`, porque o que essas operações têm em comum é só **não serem nem compra nem venda direta**. Cenários típicos:

- **Transferências entre lojas/locais** — Comportamento `Outros` com `Tipo Empresa Destino` definido em `Cabeçalho → Origem/Destino` da configuração do Tipo. Estoque sai do `Local Origem` e entra no `Local Destino`, com ou sem documento fiscal próprio (NF de transferência) conforme a regra.
- **Ajuste de Estoque** — o cadastro auxiliar `Ajuste de Estoque` (`79`) **dispara** movimentos visíveis aqui em `203`. O Tipo amarrado define se o ajuste é de entrada (positivo) ou saída (negativa). Veja [Ajuste de Estoque](../documentacao_ajuste_de_estoque.md).
- **Produção de Produtos** — `Produção de Produtos` (`144`) também **dispara** movimentos em `203`: saída dos ingredientes, entrada do acabado, perda. Veja [Produção](../Producao/documentacao_producao_de_produtos.md).
- **Pedido de Compra** convertido — `Pedido de Compra` (`64`) pode ser configurado para gerar movimento aqui em vez de em `201`, dependendo do desenho do cliente.
- **Brindes, amostras, doações, consumo interno** — Tipos `Outros` que tipicamente saem do estoque sem financeiro, ou com financeiro de despesa.
- **Devolução de Venda** — quando o cliente devolve mercadoria já vendida, o Tipo `DEVOLUÇÃO DE VENDA` (configurado em `37` com `Devolução = Sim`, geralmente com `Devolução Crédito` para gerar crédito ao cliente) **fica aqui** em `203`, não em `202`. Exige `Referenciar Nota` apontando para a venda original. Estoque volta, fiscal de entrada é emitido, e (se configurado) um Crédito de Pessoa é gerado.

  Em lojas de balcão com NFC-e, é comum a devolução acontecer em **duas etapas**: o atendente cria um `Pedido de Devolução` rapidamente apontando o cupom fiscal de venda (operação repetida várias vezes ao longo do dia); no fim do dia, todos os pedidos viram uma `NF-e Devolução` consolidada. Para que a NF-e final referencie o **cupom fiscal de origem** — e não o pedido intermediário — o Tipo `NF-e Devolução` precisa estar configurado com o flag **`Referenciar Mov. Próprio` desmarcado**, fazendo o sistema herdar a referência cadastrada no pedido. Detalhes do flag em [Referenciar Mov. Próprio](../TiposDeMovimento/referencia_configuracoes_tipos_movimento.md#%EF%B8%8F-aba-dados-cadastrais).
- **Devolução neutra** — quando a devolução não se enquadra como compra (sem refazer estoque do fornecedor) nem como venda direta, pode ser cadastrada como `Outros` com regras dedicadas.

> 💡 **CFOPs aceitos**: o validador do CFOP em `Outros` é mais flexível — não há restrição absoluta de faixa como em Entrada/Saída. Cada Tipo definirá em `Cabeçalho → Fiscal` quais CFOPs aceita.

> ⚠️ **Atualizar Custo Automático**: válido em `Outros` (assim como em Compras). É comum em ajustes de inventário positivos e em entradas de produção (o produto acabado precisa de custo).

---

## 💡 Exemplos práticos

### Transferência entre lojas

1. Pesquisa `F1` → `203` → **Novo**.
2. `Tipo` = `TRANSFERÊNCIA ENTRE EMPRESAS` (configurado em `37` com Comportamento `Outros`, `Tipo Empresa Destino` definido).
3. **Cabeçalho**: `Local Origem` = local da loja A; `Empresa Destino` + `Local Destino` = loja B.
4. **Itens**: produtos e quantidades.
5. `F6` (Finalizar) → estoque sai do Local Origem e entra no Local Destino. Se o Tipo tem fiscal configurado, NF de transferência é emitida.

### Lançar perda de estoque (quebra/avaria)

1. Pesquisa `F1` → `203` → **Novo**.
2. `Tipo` = `PERDA DE ESTOQUE`.
3. **Itens**: produtos perdidos com quantidades.
4. `F6` → estoque baixa, lançamento no Histórico fica disponível para auditoria.

> 💡 Em vez de ir direto na `203`, prefira disparar a perda pelo cadastro auxiliar [Ajuste de Estoque](../documentacao_ajuste_de_estoque.md) (`79`) — ele cria o movimento aqui automaticamente, mas a inserção fica registrada na tela específica.

### Entrada de produto acabado vindo da Produção

1. Use o cadastro [Produção de Produtos](../Producao/documentacao_producao_de_produtos.md) (`144`) — ele dispara os movimentos em `203`.
2. Para consultar/auditar: pesquisa `F1` → `203` → filtrar por Tipo (`PRODUÇÃO - ENTRADA ACABADO`, `PRODUÇÃO - SAÍDA INGREDIENTE`, `PRODUÇÃO - PERDA`).

### Devolução de cupom fiscal via pedido intermediário

Cenário típico em loja de balcão com volume alto de devoluções: a NF-e de Devolução é emitida **uma vez no fim do dia**, consolidando todos os retornos do dia. A divisão em duas etapas (pedido intermediário + NF-e final) acelera o atendimento e mantém a referência fiscal no documento certo.

**Configuração-chave dos Tipos** (em `37`):

- Tipo `PEDIDO DE DEVOLUÇÃO` — Comportamento `Outros`, sem efeito fiscal definitivo (não emite NF-e), `Itens → Estoque` com Transação que **não** afeta saldo (o estoque volta só na etapa fiscal), `Cabeçalho → Características` com `Não consultar em lançamento` **desmarcado** (atendente precisa selecioná-lo manualmente), `Finalizar/Mudar → Mudar` apontando para `NF-e Devolução`.
- Tipo `NF-e Devolução` — Comportamento `Entrada` (volta para a empresa), `Cabeçalho → Fiscal` com Modelo `NF-e` e CFOPs de devolução (`1202`/`2202`/`1410`/`2410` conforme a operação), `Dados Cadastrais` com **`Referenciar Mov. Próprio` desmarcado** (essencial — faz a NF-e herdar a referência do cupom que o pedido apontou), `Itens → Estoque` com Transação que **soma** Físico/Disponível, `Cabeçalho → Características` com `Não consultar em lançamento` **marcado** (só nasce via Mudar a partir do Pedido — atendente não cria manualmente).

**Operação no dia a dia**:

1. **Cliente chega para devolver.** Atendente: pesquisa `F1` → `203` → **Novo** → `Tipo` = `PEDIDO DE DEVOLUÇÃO`.
2. **Em `Notas Referenciadas`**: aponta o cupom fiscal de origem (chave NFC-e + número). Itens são importados do cupom.
3. **Confere quantidades/valores devolvidos** e finaliza o pedido. Cliente sai com comprovante; sem NF-e fiscal ainda.
4. **Etapas repetidas** ao longo do dia para cada cliente que aparece.
5. **Fim do dia / fechamento**: operador localiza todos os `PEDIDO DE DEVOLUÇÃO` do dia (filtro por Tipo + período).
6. **Aplica `F7 Mudar` em cada pedido** → vira `NF-e Devolução`. Como o Tipo destino tem `Referenciar Mov. Próprio` **desmarcado**, a NF-e herda como referência o **cupom fiscal** que o pedido apontava (não o próprio pedido). A SEFAZ recebe uma NF-e Devolução referenciando o documento fiscal original.
7. **Estoque volta** (Transação do `NF-e Devolução` soma) e, se configurado, **Crédito de Pessoa é gerado** para uso futuro.

> 💡 **Por que duas etapas em vez de gerar NF-e direto?** Reduz fricção no atendimento (atendente não espera retorno da SEFAZ a cada devolução) e consolida o fiscal num momento controlado, fora do pico de fluxo da loja.

---

## 🔗 Documentação completa

O detalhamento do formulário — sub-abas, fluxos, atalhos, validações, exemplos comuns, FAQ — está em [Movimentos](documentacao_movimentos.md). Esta página descreve apenas o que diferencia o modo `Outros`.

Outras referências úteis:

- [Tipos de Movimento](../TiposDeMovimento/documentacao_tipos_de_movimento.md) (`37`) — onde os Tipos `Outros` são configurados.
- [Ajuste de Estoque](../documentacao_ajuste_de_estoque.md) (`79`) — telas auxiliares que disparam movimentos aqui.
- [Produção de Produtos](../Producao/documentacao_producao_de_produtos.md) (`144`) — idem.
- [Histórico de Movimentações](../documentacao_historico_de_movimentacoes.md) (`205`) — análise e totais dos movimentos lançados aqui.

---

**Última atualização**: Maio de 2026
**Versão**: 5.1
**Público-alvo**: Retaguarda de estoque / Logística / Suporte
