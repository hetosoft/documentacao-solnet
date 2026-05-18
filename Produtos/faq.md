# 📄 FAQ — Cadastro de Produtos - Sol.NET

## 🎯 Visão Geral

Perguntas e respostas mais comuns sobre a tela `Produtos` (código `32`). Documento principal: [documentacao_produtos.md](documentacao_produtos.md).

---

## 🔢 Código, descrição e duplicidade

### ❓ Tentei salvar e o sistema sugeriu um código diferente. Por quê?

Você usou um código já existente. O Sol.NET oferece o **próximo código sequencial disponível** e atualiza o gerador interno (`PRODUTO_CODIGO_GERADOR`) para o próximo cadastro. Aceite só se a duplicidade era acidental — caso contrário, cancele e veja qual produto está usando o código.

### ❓ Como posso ter dois produtos com a mesma descrição?

Use **fabricantes diferentes**. A regra de unicidade é por combinação `Descrição + Marca/Fabricante`. Sem o fabricante (campo em branco), o sistema trata como `"NENHUM"` — então **duas descrições idênticas sem fabricante também batem** na regra.

### ❓ A mensagem "Já Existe essa DESCRIÇÃO Associada a MARCA/FABRICANTE" travou meu cadastro. O que faço?

Existem três alternativas:

1. Alterar a descrição (a forma mais limpa).
2. Preencher um **Fabricante** que diferencie o cadastro.
3. Se o caso real exige a duplicidade, o suporte Hetosoft pode habilitar a exceção `Aceitar descrição igual` — esse acesso é restrito ao suporte.

### ❓ Posso usar acentos e caracteres especiais na descrição?

Sim. A descrição aceita acentos e caracteres usuais. Evite somente `;` e `"` — alguns campos legados não toleram bem em exportações fiscais.

---

## 💵 Preços, custos e moedas

### ❓ Por que o sistema bloqueia ao salvar pedindo "Preechar Moeda N"?

Cada coluna de preço (1 a 8) tem sua própria moeda. Se você informou **Preço de Venda 3 > 0**, a **Moeda 3** precisa estar preenchida. Vá à aba `Preços` e confira a moeda na coluna apontada na mensagem.

### ❓ Não pretendo usar as 8 colunas de preço. Posso deixar as outras em branco?

Sim. Só preencha as colunas que a empresa de fato utiliza. As demais ficam com valor zero e moeda em branco — sem prejuízo.

### ❓ A Margem de Lucro Real ficou diferente da Margem de Lucro que digitei. O que aconteceu?

Pode ser:

- **Margem mínima** ou **máxima** configurada limitou o resultado.
- Regra de **arredondamento** na Tabela de Preço alterou o preço final, mudando a margem efetiva.
- **Comissão** ou **lucro líquido** entrou no cálculo.

A `Margem de Lucro` é a desejada; a `Margem de Lucro Real` é a efetivamente aplicada.

### ❓ Onde vejo o histórico de alterações de preço?

Na aba **Informações → Datas**. Cada uma das 8 colunas mostra a última data e o usuário que alterou. Para conferir o valor anterior, olhe o campo `Preço Anterior` na própria aba `Preços`.

### ❓ O custo médio aumentou de uma hora para outra. O que mexeu nele?

O **Custo Médio** é recalculado pelas entradas de estoque (compras, devoluções de venda, ajustes, transferências). Em geral, uma nota recente com valor diferente do custo médio anterior causa a variação. Consulte o [Histórico de Produtos](../Movimentacao/documentacao_historico_de_produtos.md) para identificar o movimento.

---

## 🏛️ Tributação

### ❓ O NCM mudou para um produto. Preciso atualizar todos os movimentos antigos?

Não — movimentos já lançados preservam o NCM usado na época. Atualize o cadastro do produto e os **novos** movimentos passam a usar o NCM atual. Marque também a `Data de Auditoria NCM` (aba `Informações → Tributos`) para deixar registrado quando o NCM foi conferido.

### ❓ Onde configuro CBS e IBS (Reforma Tributária)?

Na aba **Tributação**, no bloco **CBS/IBS**. Para entender o cronograma e o cálculo, leia [Reforma Tributária](../Fiscal/documentacao_reforma_tributaria.md).

### ❓ Esse produto não tem NCM ainda. Posso cadastrar mesmo assim?

Pode, mas ele não vai ser emissível em documentos fiscais até o NCM ser preenchido. Para mercadorias destinadas a consumo interno (uso e consumo), ainda assim recomenda-se preencher.

### ❓ O que é "ICMS Crédito Outorgado — Saída"?

É o NCM (e parâmetros) usados quando a UF concede crédito outorgado para a saída desse produto. Só preencha se a empresa de fato opera nesse regime na UF.

---

## 🔧 Casos especiais (balança, medicamento, agro, e-commerce)

### ❓ Cadastro de balança não está aparecendo na sub-aba Balança. Por quê?

Verifique:

1. A **Unidade** do produto é compatível com balança (geralmente `KG` ou unidade similar).
2. O **Setor da Balança** está preenchido.
3. As **Informações Nutricionais** mínimas estão preenchidas — algumas balanças e impressoras de etiqueta exigem os campos do painel completo.

### ❓ Vendo medicamento. Tenho que preencher PMC sempre?

Sim, para itens regulados pela ANVISA. O **PMC** (Preço Máximo ao Consumidor) é a referência regulatória; sua falta bloqueia operações específicas de farmácia.

### ❓ Em defensivo agrícola, o Registro MAPA é obrigatório?

Sim para emissão de [Receituário Agronômico](../Agronomico/documentacao_receituario_agronomico.md). Sem registro, o sistema não autoriza a emissão.

### ❓ Marquei o produto como e-commerce mas ele não aparece no site. O que conferir?

Sequência de checagens:

1. **Inativo** está desmarcado?
2. **Inativo para Venda** está desmarcado?
3. Em **Outros → Produto por Empresa**, a empresa do e-commerce está vinculada e ativa?
4. **Estoque Mínimo para E-commerce** está respeitado pelo saldo atual?
5. Há **erro de integração** registrado na aba `Informações → Geral`?

### ❓ "TP_DESATIVAR_ECOMMERCE" e "Inativo" são a mesma coisa?

Não. `Inativo` retira o produto de tudo. A flag de desativar e-commerce só impede a exibição no canal de comércio eletrônico, preservando uso interno e venda em loja física.

---

## 📦 Estoque, grade e linkado

### ❓ Vendi um produto e o saldo ficou negativo. Por quê?

A flag **Não Validar Estoque** está marcada no cadastro do produto. Quando desligada, o Sol.NET bloqueia vendas sem saldo no Local de Estoque. Verifique também as regras do `Tipo de Movimento` usado (consulte [Tipos de Movimento](../Movimentacao/TiposDeMovimento/documentacao_tipos_de_movimento.md)).

### ❓ Qual a diferença entre "Produto Linkado" e "Produto Grade"?

- **Grade** — o mesmo produto em variações (ex.: tamanho × cor). Saldo controlado por variação.
- **Linkado** — produto associado a outro com fator de conversão (ex.: caixa de 12 unidades vinculada à unidade). Saldo controlado no produto-pai; o filho consome o saldo via Conversão.

### ❓ Cadastrei a caixa e a unidade. Como movimentação da caixa afeta o saldo da unidade?

Com **Produto Linkado** + **Conversão**. No cadastro da caixa, aponte o produto-unidade em `Produto Linkado` e informe o fator (`12`) em `Conversão`. Uma venda da caixa retira 12 unidades do estoque do produto-unidade.

### ❓ Como funciona o Preço Progressivo?

Aba `Outros → Preço Progressivo`. Cadastre faixas de quantidade com preços. Ao vender, o Sol.NET aplica o preço da faixa correspondente. Útil em atacado e em distribuição.

---

## 🔒 Inativação, exclusão e auditoria

### ❓ Posso excluir um produto?

Em geral, **não** quando ele tem movimentações associadas — a exclusão quebraria a integridade dos lançamentos históricos. Use **Inativo** para retirar do uso. A função `Unificar Dados Produtos` (tela `815`) permite mesclar cadastros duplicados; também é a forma de "remover" um cadastro indesejado mantendo o histórico.

### ❓ Inativei o produto e ele ainda aparece em algumas telas. É bug?

Não. `Inativo` esconde o produto de novas operações, mas mantém:

- Saldos antigos.
- Movimentos lançados.
- Vínculos como insumo de fórmulas e referências em outros cadastros.

Para sumir completamente, considere usar a **Unificação de Produtos** levando o histórico para outro cadastro.

### ❓ Quem alterou o cadastro pela última vez?

Aba `Informações → Geral`: campos `Alterado em` e `Usuário`. Para alteração de preço por coluna, veja `Informações → Datas`.

---

## 🔗 Documentos relacionados

- [Documentação completa do Cadastro de Produtos](documentacao_produtos.md)
- [Guia Rápido — Cadastro de Produtos](guia_rapido.md)
- [NCM](../Fiscal/documentacao_ncm.md), [Reforma Tributária](../Fiscal/documentacao_reforma_tributaria.md)
- [Histórico de Produtos](../Movimentacao/documentacao_historico_de_produtos.md)
- [Fórmulas de Produtos](../Movimentacao/Producao/documentacao_formulas_de_produtos.md), [Produção de Produtos](../Movimentacao/Producao/documentacao_producao_de_produtos.md)

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Equipe de suporte Hetosoft e usuários do Sol.NET
