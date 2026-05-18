# 📄 Guia Rápido — Cadastro de Produtos - Sol.NET

## 🎯 Visão Geral

Checklist objetivo para cadastrar um produto novo ou ajustar um existente na tela `Produtos` (código `32`). A referência completa de cada aba está em [documentacao_produtos.md](documentacao_produtos.md).

---

## 🚪 Como acessar

1. Pressione `F1` para abrir a pesquisa universal.
2. Digite `32` ou parte de `Produtos`.
3. Abra a tela. Para criar um novo registro, clique em `Novo`. Para editar, localize na lista e abra.

---

## ✅ Checklist: cadastro completo do zero

### 1️⃣ Aba `Principal`

- [ ] **Código** — digite ou deixe gerar automaticamente.
- [ ] **Descrição** — nome comercial (máx. 120 caracteres).
- [ ] **Descrição Reduzida** — versão curta para cupom/etiqueta.
- [ ] **Tipo de Item** — selecione o SPED (`00 – Mercadoria para Revenda` é o padrão).
- [ ] **Família**, **Grupo**, **Subgrupo**, **Departamento** — classifique no cadastro hierárquico.
- [ ] **Fabricante** e **Fornecedor** — opcionais; lembre que `Descrição + Fabricante` precisa ser único.
- [ ] **Unidade** (ex.: `UN`, `KG`, `L`).
- [ ] **Unidade Tributária** + **Quantidade Tributária** — só preencha se forem diferentes da unidade principal (ambos juntos ou nenhum).
- [ ] **Status** — deixe `Inativo` desmarcado para um produto ativo.
- [ ] **Foto** — se houver, insira pelo carrossel à esquerda.

### 2️⃣ Aba `Preços`

Faça pelo menos a **Coluna 1**. As demais (até 8) só se a empresa usa políticas de preço diferenciadas.

- [ ] **Custo Unitário 1**.
- [ ] **Margem de Lucro 1 (%)**.
- [ ] **Moeda 1** ← *obrigatório quando o Preço de Venda 1 > 0*.
- [ ] **Preço de Venda 1** (resultado ou ajuste manual).
- [ ] **Comissão %**, **Markup %**, **Margem Mínima/Máxima** — se a empresa usa.

### 3️⃣ Aba `Tributação`

- [ ] **NCM** — obrigatório para emissão fiscal.
- [ ] **CEST** — quando o NCM exige.
- [ ] **Origem** — nacional, importada, etc.
- [ ] **Região ICMS Saída** — para definir alíquotas por UF.
- [ ] **Região ICMS-ST Saída** — quando aplicável.
- [ ] **CBS / IBS** — preencher conforme calendário da Reforma Tributária.

### 4️⃣ Aba `Outros` — só se aplicável

- [ ] **Balança** — produtos pesáveis, com informações nutricionais e selos de alto teor.
- [ ] **Medicamento** — PMC, código ANVISA, motivo de isenção.
- [ ] **Formulado Agro.** — registro MAPA, formulado, embalagem.
- [ ] **Estoque Mínimo** — quando o item entra no cálculo de sugestão de compra.
- [ ] **Localização** — prateleira/corredor (geralmente alimentado pelo coletor).
- [ ] **Preço Progressivo** — preços por faixa de quantidade.
- [ ] **Produto por Empresa** — diferenças por empresa (só em multiempresa).

### 5️⃣ Aba `Movimentação`

- [ ] **Peso Bruto / Peso Líquido**, **Altura / Largura / Comprimento** — para frete e balança.
- [ ] **Conversão** — quando há Produto Linkado.
- [ ] **Não Validar Estoque** — só marque se conscientemente o produto pode vender sem saldo.

### 6️⃣ Salvar

- [ ] Use o botão equivalente a Salvar/Confirmar da tela.
- [ ] Se aparecer mensagem de validação, ajuste e tente novamente. As mais comuns:
  - `<Label> (VALOR) Já Existe!` → código duplicado. Aceite a sugestão ou cancele e investigue.
  - `Já Existe essa "DESCRIÇÃO" Associada a "MARCA/FABRICANTE"` → ajuste descrição ou fabricante.
  - `Não permitido! Preechar Moeda <N>` → preencha a moeda da coluna apontada.
  - `Obrigatório preecher os dois campos!` → Unidade Tributária + Quantidade Tributária andam juntas.

---

## 🚀 Atalhos do dia a dia

| Tarefa | Caminho mais curto |
|---|---|
| Alterar preço de venda | Aba `Preços` → coluna desejada → salvar. Sistema registra `Preço Anterior` e data/usuário sozinho. |
| Inativar para venda | Aba `Principal` → marcar `Inativo para Venda`. |
| Trocar NCM com auditoria | Aba `Tributação` → atualizar NCM → marcar `Data de Auditoria NCM` (aba `Informações → Tributos`). |
| Cadastrar item idêntico de outro fabricante | Duplicar descrição mudando apenas o `Fabricante` — o sistema permite. |
| Conferir histórico de preço | Aba `Informações → Datas` (somente leitura). |
| Saber onde o item entra como insumo | Aba `Outros → Fórmulas`. |

---

## ⚠️ Lembretes importantes

- **Moeda × Preço:** cada uma das 8 colunas de preço tem sua própria moeda. Preço > 0 sem moeda = bloqueio ao salvar.
- **Descrição + Fabricante = chave única.** Use o fabricante para diferenciar produtos com nome parecido.
- **Combo `Tipo de Item`:** o `99 – Outras` que aparece na tela é exibição SPED — internamente o sistema usa numeração própria. Para a operação, basta escolher a descrição correta.
- **Aba `Informações`:** é só leitura. Para alterar qualquer coisa que apareça lá, vá à aba original (`Principal`, `Preços`, `Tributação`).
- **`Não Validar Estoque`** desliga a barreira de saldo para o produto inteiro. Use com cautela.

---

## 🔗 Documentos relacionados

- [Documentação completa do Cadastro de Produtos](documentacao_produtos.md)
- [FAQ — Cadastro de Produtos](faq.md)
- [NCM](../Fiscal/documentacao_ncm.md), [Região ICMS Saída](../Fiscal/documentacao_regiao_icms.md), [Região ICMS-ST Saída](../Fiscal/documentacao_regiao_icms_st_saida.md)
- [Histórico de Produtos](../Movimentacao/documentacao_historico_de_produtos.md), [Fórmulas de Produtos](../Movimentacao/Producao/documentacao_formulas_de_produtos.md)

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Equipe de suporte Hetosoft e usuários do Sol.NET
