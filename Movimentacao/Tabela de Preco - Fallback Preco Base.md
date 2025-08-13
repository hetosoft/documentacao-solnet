---
title: "Configuracação de Tabela de Preço"
permalink: /Movimentacao/TabelaPreco/
---
# 💰 Precificação: Uso do Preço da Base de Cálculo - Sol.NET

## 🎯 Visão Geral

**Data da Implementação**: 08 de Agosto de 2025  
**Aplicações**: Sol.NET (Cadastro de Tabela de Preço e cálculo de venda)  
**Público-alvo**: Usuários e administradores do módulo de precificação

### 📋 Resumo da Funcionalidade
Foi adicionada uma opção na **Tabela de Preço** para, quando a tabela não for elegível para o cliente/produto na venda, utilizar automaticamente o preço definido na **Base de Cálculo** da própria tabela (ex.: Preço 1…8 ou custos) como preço da venda, sem aplicar percentuais da tabela. Também foi revisado o fallback para usar o **Preço de Venda 1** quando o preço base calculado estiver zerado, conforme configuração.

### ✨ Principais Novidades:
- Novo campo/flag: “Buscar Preço Base Cálculo se Tabela de Preço inelegível”.
- Ajuste no fallback: “Buscar Preço Venda1 preço base Zerado(0)”.
- Atualização de banco: inclusão do campo BUSCAR_PRECO_BASE_CALC em TABELA_PRECO e definição automática para tabelas com base de cálculo por preços 1,2,3,4,5,6,7(15),8(16).
- Ajustes visuais na tela de Cadastro de Tabela de Preço (melhor aproveitamento de espaço e pequenos aprimoramentos de usabilidade).

---

## 🔄 O que mudou

### 💾 1) Banco de Dados
- Nova coluna em TABELA_PRECO: BUSCAR_PRECO_BASE_CALC (SmallInt)
- Migração aplica: BUSCAR_PRECO_BASE_CALC = 1 onde BASE_CALCULO IN (1,2,3,4,5,6,15,16)
  - Impacto: por padrão, tabelas que têm base de cálculo em Preços (1 a 8) já vêm habilitadas para usar o preço base quando a tabela não for elegível.

Observação: a atualização é aplicada automaticamente pelo processo de atualização do sistema. Não requer ação manual.

### 2) Tela “Cadastro de Tabela de Preço”
Na aba de valores (grupo “Extra”) foram ajustadas/renomeadas as opções:
- Buscar Preço Venda1 preço base Zerado(0)
  - Campo: BUSCAR_PRECO1
  - Quando marcado, se o preço base calculado ficar 0, o sistema usa o Preço de Venda 1 do produto como fallback.

- Buscar Preço Base Cálculo se Tabela de Preço inelegível (NOVO)
  - Campo: BUSCAR_PRECO_BASE_CALC
  - Quando marcado, se a tabela não puder ser aplicada na venda (por regra de cliente, produto, status, região etc.), o sistema utilizará o preço definido pela Base de Cálculo da própria tabela para a venda, sem aplicar percentuais.

Outros ajustes: ampliação do tamanho da janela e lista de grids, pequenos aprimoramentos de usabilidade (sem mudança de comportamento de negócio).

### 🧮 3) Lógica de Cálculo de Preço na Venda
Comportamento quando a Tabela de Preço NÃO é elegível:
1. Se “Buscar Preço Base Cálculo…” estiver marcado: usa-se o preço conforme a Base de Cálculo da tabela.
   - Base de Cálculo suportada:
     - 1..6, 15, 16: Preços 1..8 do cadastro de produto.
     - 7..14: bases de custo (CUSTO_INICIAL, CUSTO_UNITARIO, CUSTO_MEDIO, CUSTO_VENDA, ULTIMO_PRECO_COMPRA, CUSTO_MEDIO_UNITARIO), com leitura complementar por empresa quando aplicável.
2. Se o preço obtido for 0 e “Buscar Preço Venda1 preço base Zerado(0)” estiver marcado: utilizar Preço de Venda 1.

Resultado: evita-se erro de precificação quando não há regra aplicável para o cliente/produto, mantendo uma referência de preço coerente com a política da tabela.

---

## ⚙️ Como Configurar
1) Acesse: Cadastros > Tabela de Preço.
2) Selecione a tabela desejada e abra a aba de Valores > grupo “Extra”.
3) Opções:
   - Marque “Buscar Preço Base Cálculo se Tabela de Preço inelegível” para habilitar o uso do preço da Base de Cálculo quando a tabela não for aplicável.
   - (Opcional) Marque “Buscar Preço Venda1 preço base Zerado(0)” para que, se o preço base resultar 0, o sistema utilize o Preço de Venda 1 do produto.
4) Confira a “Base de Cálculo” da tabela (ex.: Preço 1, Preço 2, Custos…). Ela definirá qual preço será usado no cenário de inelegibilidade.
5) Grave as alterações.

Recomendação: valide as configurações em um produto de teste realizando uma simulação de venda para um cliente inelegível à tabela.

---

## 💡 Exemplos Práticos
- Exemplo A (Preço):
  - Tabela com Base de Cálculo = Preço 2 (Preço de venda 2) e “Buscar Preço Base Cálculo…” marcado.
  - Cliente/produto não atendem às regras da tabela.
  - Resultado: o sistema usa o Preço 2 do produto na venda (sem aplicar percentuais da tabela).

- Exemplo B (Custo):
  - Tabela com Base de Cálculo = Custo Médio Unitário.
  - “Buscar Preço Base Cálculo…” marcado.
  - Resultado: usa o custo médio unitário como preço base da venda se a tabela estiver inelegível.

- Exemplo C (Fallback Venda 1):
  - “Buscar Preço Base Cálculo…” marcado, porém o preço base calculado é 0.
  - “Buscar Preço Venda1 preço base Zerado(0)” também marcado.
  - Resultado: usa o Preço de Venda 1 do produto.

---

## ⚠️ Impactos e Compatibilidade
- Compatível com Firebird e SQL Server (campo novo criado via DDL padrão do sistema).
- Sem alterações em integrações externas.
- Comportamento antigo é preservado quando o novo flag não estiver marcado.
- Para tabelas com base em preços (1..8), o novo flag já vem habilitado por padrão após a atualização; revise conforme sua política comercial.

---

## ✅ Checklist Pós-Atualização
- [ ] Verificar se a migração criou BUSCAR_PRECO_BASE_CALC em TABELA_PRECO.
- [ ] Revisar as Tabelas de Preço mais usadas e confirmar se as opções no grupo “Extra” estão conforme a estratégia desejada.
- [ ] Realizar uma venda de teste com cliente/produto inelegíveis para validar o preço aplicado.

---

## ❓ Perguntas Frequentes (FAQ)
1) O sistema sempre usará a Base de Cálculo quando a tabela não for elegível?
   - Somente se a opção “Buscar Preço Base Cálculo…” estiver marcada na Tabela de Preço.

2) E se a Base de Cálculo resultar preço 0?
   - Se “Buscar Preço Venda1 preço base Zerado(0)” estiver marcado, o Preço de Venda 1 será usado como fallback.

3) Preciso rodar script manual de banco?
   - Não. A atualização do sistema aplica a alteração automaticamente.

4) Há impacto em promoções ou condições de pagamento?
   - Apenas quando a tabela é inelegível: nesse caso, usa-se o preço da base sem aplicar percentuais da tabela. Promoções específicas seguem suas próprias regras de elegibilidade.

---

## 🔧 Notas Técnicas (Para Administradores)
- Campo novo: TABELA_PRECO.BUSCAR_PRECO_BASE_CALC (SmallInt)
- Lógica: inclusão de função de mapeamento da Base de Cálculo para preço/custo na precificação da venda; fallback condicionado ao BUSCAR_PRECO1.
- Migração identificada via GUIDs internos do processo de atualização; disponível no histórico do processo “ExecutarStatements”.

Em caso de dúvidas, consulte o suporte Hetosoft informando “PR 6914 — Precificação (Base de Cálculo em tabela inelegível)”.

---

**📅 Última atualização**: Agosto de 2025
**🏷️ Versão**: PR 6914
**👥 Público-alvo**: Usuários e administradores do módulo de precificação Sol.NET
