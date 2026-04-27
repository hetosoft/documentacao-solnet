---
title: "Guia Rápido: Produção - Sol.NET"
permalink: /Movimentacao/Producao/guia_rapido/
---
# 📄 Guia Rápido — Produção - Sol.NET

> Guia direto ao ponto para configurar e operar o módulo de Produção. Para detalhes conceituais, ver a [Documentação Completa](documentacao_producao.md).

## 🎯 Visão Geral

Duas telas, ambas abertas pela **pesquisa universal (F1)**:

| Tela | Código (F1) | Para que serve |
|------|-------------|----------------|
| **Fórmulas de Produtos** | `143` | Cadastrar a "receita" do produto (ingredientes, embalagens, perdas). |
| **Produção de Produtos** | `144` | Executar uma produção e gerar os movimentos de estoque. |

---

## 🚦 Setup inicial (uma vez por empresa)

Antes de cadastrar a primeira fórmula:

1. **Crie 3 tipos de movimento** em `Cadastro de Tipos de Movimento` (pesquisa F1):
   - `Produção - Entrada` (entra estoque, sem financeiro / sem nota).
   - `Produção - Saída` (baixa estoque, sem financeiro / sem nota).
   - `Produção - Perda` (baixa estoque a título de perda).
2. **Confira** o `Local de Estoque` e `Situação de Estoque` que serão usados.
3. **Garanta o cadastro** do produto acabado e de todos os insumos com **custo unitário > 0**.
4. **Conceda permissões** dos módulos `FORMULA PRODUCAO PRODUTO` (tela `143`) e `PRODUCAO PRODUTOS` (tela `144`) aos usuários responsáveis.

---

## 🧪 Cadastrar uma Fórmula

Tela: **Fórmulas de Produtos** — código `143` (pesquisa F1).

1. Abra a tela e acione `Novo` (botão da própria tela).
2. Preencha o cabeçalho:
   - **Descrição**, **Produto Acabado**, **Total Produzido** + **Unidade de Produção**.
   - **Fator de Conversão** (quantos itens por unidade de produção).
3. Adicione os **itens** na grade `Ingredientes`:
   - Produto, quantidade, unidade.
   - **Tipo de Item**: `Composição`, `Embalagem` ou `Perda`.
4. Salve.

> 💡 Atalho útil: a partir do **Cadastro de Produtos**, com o produto selecionado, clique com o botão direito na grade de busca → **Cadastro Fórmula Produção** abre a fórmula já filtrando pelo produto.

---

## 🏭 Executar uma Produção

Tela: **Produção de Produtos** — código `144` (pesquisa F1).

### Passo a passo

1. **Novo** → preencha o cabeçalho:
   - Loja/Empresa, Local de Estoque, Situação de Estoque.
   - **Os três tipos de movimento** (Entrada, Saída e Perda).
   - **Fórmula** — ao escolher, os ingredientes são copiados.
2. Ajuste **Quantidade Real** se a produção rendeu diferente do previsto pela fórmula.
3. Verifique a aba `Ingredientes`:
   - Se necessário, ajuste a `Qtd. Real` consumida de cada item.
   - Confirme que **todos os itens** têm `Custo Unitário > 0` e `Total Custo > 0`.
4. Salve a produção.
5. Acione `Iniciar Produção` (botão da tela). Status passa para `EM PRODUÇÃO` e a hora de início é registrada.
6. Quando concluir, acione `Finalizar Produção`. O sistema gera os 3 movimentos automaticamente.

### Onde os movimentos aparecem?

- Na própria tela de Produção, **aba `Movimento`**: Entrada, Saída e Perda lado a lado.
- Na tela de **Movimentação** regular (pesquisa F1), localizáveis pelo `COD_VINCULO_INICIO` apontando para o ID do movimento de Saída.

---

## ✅ Checklist — Antes de iniciar

- [ ] Tipos de movimento de Entrada, Saída e Perda **selecionados**.
- [ ] Loja/Empresa **selecionada**.
- [ ] Local de Estoque e Situação de Estoque **selecionados**.
- [ ] Fórmula **selecionada** e ingredientes copiados.
- [ ] Produção **salva** (sem isso, não é possível mudar status).

## ✅ Checklist — Antes de finalizar

- [ ] Status atual = `EM PRODUÇÃO`.
- [ ] `Quantidade Real` informada.
- [ ] `Quantidade de Itens Produzidos` > 0.
- [ ] Todos os ingredientes com `Custo Unitário > 0` e `Total Custo > 0`.
- [ ] Se a fórmula tem itens do tipo `Perda` → tipo de movimento de Perda **preenchido**.

---

## ❌ Cancelar uma Produção

| Status atual | Como cancelar |
|--------------|---------------|
| `EM ESPERA` | Acione `Cancelar Produção` direto. |
| `EM PRODUÇÃO` | Acione `Cancelar Produção` direto. |
| `FINALIZADO` | **Primeiro** cancele os 3 movimentos vinculados na tela de **Movimentação** (Entrada, Saída e Perda). **Só então** volte na Produção e acione `Cancelar Produção`. |
| `CANCELADO` | Não é possível — crie uma nova produção. |

> ⚠️ Tentar cancelar uma produção `Finalizada` antes de cancelar os movimentos resulta em: *"Não é possível alterar status de produção com movimentos associados e não cancelados"*.

---

## 🛠️ Erros frequentes — solução rápida

| Erro | Solução |
|------|---------|
| *"Salve o cadastro antes de alterar seu status…"* | Salve a produção antes de iniciar ou finalizar. |
| *"Todos os ingredientes devem ter suas informações de custo preenchidas."* | Vá no `Cadastro de Produtos` do insumo → aba `Custos` e atualize o custo, ou edite o item da produção. |
| *"Para criar movimentos é necessário selecionar uma empresa."* | Selecione a Loja/Empresa no cabeçalho. |
| *"Erro ao criar o movimento de …, selecione um tipo de movimento"* | Verifique se os 3 tipos (Entrada, Saída, Perda) estão preenchidos. |
| *"Já existe um movimento associado à essa produção"* | A produção já foi finalizada antes. Veja na aba `Movimento`. |
| *"Não é possível alterar produção em status FINALIZADO"* | Não dá para voltar para `Em Produção`. Para corrigir, cancele a produção (após cancelar os 3 movimentos) e crie uma nova. |

---

## 🔗 Próximos passos

- [Documentação completa](documentacao_producao.md) — referência detalhada (modelo de dados, vínculos entre movimentos, cálculo de custo).
- [FAQ — Produção](faq.md) — dúvidas comuns.
- [Atualização Automática de Custo](../atualizacao_de_custo_automatica.md) — entender como a entrada do produto acabado afeta o custo médio.

---

**Última atualização**: Abril de 2026
**Versão**: 1.0
**Público-alvo**: Operadores e supervisores responsáveis pela produção
