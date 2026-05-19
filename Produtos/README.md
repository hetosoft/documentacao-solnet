---
title: "Índice: Documentação Módulo Produtos Sol.NET"
permalink: /Produtos/
---
# 🏷️ Índice: Documentação Módulo Produtos Sol.NET

Documentação da entidade **Produtos** no Sol.NET — o cadastro mais central do sistema, base para tudo que envolve estoque, movimentações, fiscal, PDV, mobile e e-commerce.

> Para o **histórico de movimentações** de cada produto, consulte o módulo [Movimentação](../Movimentacao/documentacao_historico_de_produtos.md). Para **fórmulas e produção**, [Movimentação → Produção](../Movimentacao/Producao/).

---

## 📋 Documentos disponíveis

### 🏷️ Cadastro de Produtos

#### 📖 [Documentação do Cadastro de Produtos](documentacao_produtos.md)
Referência completa da tela `Produtos` (código `32`):
- Identificação, classificação e status
- Preços (até 8 colunas), promoções e moedas por preço
- Custos, margens, lucro líquido e markup
- Tributação (NCM, CEST, ICMS, ICMS-ST, CBS/IBS da Reforma Tributária)
- Sub-abas especializadas: Balança, Medicamento, Formulado Agro, Estoque Mínimo, Localização, Preço Progressivo, Produto por Empresa
- Validações principais (código, descrição, unidade tributária, moeda × preço)

#### ⚡ [Guia Rápido — Cadastro de Produtos](guia_rapido.md)
Checklist da rotina de cadastro: o que preencher na ordem, em qual aba, e o que confirmar antes de salvar.

#### ❓ [FAQ — Cadastro de Produtos](faq.md)
Perguntas comuns sobre código duplicado, inativação, preços, tributação, balança, medicamento, agronômico e integrações.

---

### 🧩 Cadastros auxiliares

Telas de classificação que orbitam o `Cadastro de Produtos`. Cada uma documentada individualmente:

#### 🌳 [Famílias de Produtos](documentacao_familias.md)
Primeiro nível da hierarquia (código `24`). Centraliza margem, comissão, desconto, regra de arredondamento de preços e integrações e-commerce/mobile da linha.

#### 📦 [Grupos de Produtos](documentacao_grupos.md)
Segundo nível (código `25`), filho de uma Família. Refina margem e política comercial e adiciona toggles para desativar envio de e-commerce/mobile do Grupo.

#### 🔖 [Sub Grupo de Produtos](documentacao_sub_grupos.md)
Terceiro nível (código `26`), filho de um Grupo. Permite subdividir a categoria com regras próprias de margem, comissão e integração.

#### 🏬 [Departamento de Produtos](documentacao_departamento.md)
Classificação livre (código `104`) paralela à hierarquia. Geralmente usada para setor físico da loja (açougue, padaria, hortifrúti) ou área de negócio.

#### 📋 [Lista de Produtos](documentacao_lista_produtos.md)
Rótulo livre (código `80`) para classificação interna. Também é o vínculo usado pelo Self-Checkout para identificar itens pesáveis.

---

## 🔗 Outras telas relacionadas

Todas abertas pela pesquisa universal (atalho `F1`).

| Tela | Código | O que faz |
|---|---|---|
| Unificar Dados Produtos | `815` | Mescla cadastros duplicados. |
| Histórico de Produtos | — | Movimentações de cada produto (módulo [Movimentação](../Movimentacao/documentacao_historico_de_produtos.md)). |
| Fórmulas de Produtos | `143` | Composição para produção (módulo [Movimentação](../Movimentacao/Producao/)). |
| Produção de Produtos | `144` | Execução da fabricação (módulo [Movimentação](../Movimentacao/Producao/)). |
| NCM | — | Cadastro fiscal vinculado ao produto (módulo [Fiscal](../Fiscal/documentacao_ncm.md)). |
| Região ICMS Saída | — | Tributação ICMS (módulo [Fiscal](../Fiscal/documentacao_regiao_icms.md)). |
| Região ICMS-ST Saída | — | Tributação ICMS-ST (módulo [Fiscal](../Fiscal/documentacao_regiao_icms_st_saida.md)). |

> A tela `Unificar Dados Produtos` (código `815`) ainda não tem documentação dedicada — será coberta em revisão futura.

---

**Última atualização**: Maio de 2026
**Público-alvo**: Equipe de suporte Hetosoft e usuários do Sol.NET
