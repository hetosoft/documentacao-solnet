---
title: "Índice: Documentação Módulo Fiscal Sol.NET"
permalink: /Fiscal/
---
# 🏛️ Índice: Documentação Módulo Fiscal Sol.NET

Documentação dos temas tributários do Sol.NET — **Reforma Tributária Brasileira (EC 132/2023)** e operações fiscais do dia a dia, como a **Manifestação do Destinatário** de NF-e e CT-e.

> Para DRE e Portadores, consulte o **[Módulo Financeiro](../Financeiro/README.md)**.

---

## 📋 Documentos Disponíveis

### 🏛️ Reforma Tributária

#### 📖 [Documentação Reforma Tributária](documentacao_reforma_tributaria.md)
Como o Sol.NET está preparado para a reforma e como operar no dia a dia:
- Cronograma de implementação (2026-2033) e fases de transição
- Cadastro de NCM, alíquotas CBS / IBS e regimes especiais
- Cálculo automático na Movimentação e controle de créditos
- Não cumulatividade plena — fluxo de aproveitamento
- Impactos por tipo de empresa (comércio, indústria, serviços)
- Exemplos práticos passo a passo

#### ⚡ [Guia Rápido — Reforma Tributária](guia_rapido_reforma_tributaria.md)
Referência de bolso para uso diário:
- Checklist de preparação na empresa
- Workflows comuns (entrada, saída, transferência)
- Tabela de alíquotas estimadas
- Diagnóstico rápido de problemas

#### ❓ [FAQ — Reforma Tributária](faq_reforma_tributaria.md)
Respostas para as dúvidas mais frequentes:
- Conceitos da reforma (CBS, IBS, IS)
- Créditos tributários e não cumulatividade
- Impacto por tipo de empresa
- Cronograma e período de transição
- Operação prática no Sol.NET

---

### 📨 Manifestação do Destinatário

#### 📖 [Documentação Manifestação do Destinatário](documentacao_manifestacao_destinatario.md)
Como manifestar NF-e e CT-e emitidas contra o CNPJ da empresa:
- Os quatro tipos de manifestação (Confirmação, Ciência, Desconhecimento, Operação Não Realizada)
- Download de notas da SEFAZ, filtros e busca
- Botões da tela, manifestação em lote, controle do NSU
- Vínculo com a Movimentação interna do Sol.NET
- Exemplos práticos passo a passo

#### ⚡ [Guia Rápido — Manifestação do Destinatário](guia_rapido_manifestacao_destinatario.md)
Cartão de referência para a rotina diária do suporte:
- Checklist da rotina de manifestação
- Tabelas de códigos da `Situação da Manifestação` e `Situação da NF-e`
- Combinações úteis de filtros
- Diagnóstico rápido

#### ❓ [FAQ — Manifestação do Destinatário](faq_manifestacao_destinatario.md)
Perguntas comuns sobre conceitos, operação, NSU e vínculo com a Movimentação.

> 📥 **Importar XML NF-e** e **Conferência de XML** agora vivem em **[Movimentação](../Movimentacao/README.md#-importar-xml-nf-e)** — a partir da Manifestação, o lançamento da NF-e como entrada acontece dentro da Movimentação.

---

### 🗂️ Cadastros Fiscais

Cadastros de configuração tributária que sustentam a emissão de documentos fiscais. Cada NCM, região e natureza de operação determina **como o sistema deve tributar** cada movimento.

#### 📖 [Cadastro de NCM — Documentação](documentacao_ncm.md)
Tela `21`: regra tributária associada ao código NCM, com cobertura para os três blocos de impostos:
- ICMS, ICMS-ST e FCP — aba `Principal`
- Tributação Federal — PIS, COFINS e IPI
- Reforma Tributária — CBS e IBS na aba `IVA`
- Atualização via Tabela NCM (`121`) federal

#### ⚡ [Cadastro de NCM — Guia Rápido](guia_rapido_ncm.md)
Checklist do dia a dia: ordem de preenchimento, mapa dos grupos da aba `Principal` e da aba `IVA`, e soluções rápidas para os erros mais comuns (rejeição da SEFAZ, EX, descrição não autocompletada).

#### ❓ [Cadastro de NCM — FAQ](faq_ncm.md)
Conceito, diferenças entre `21` e Tabela NCM `121`, regras de PIS/COFINS, comportamento de Tributação Federal vs. campos da aba, Reforma Tributária e tratamento de rejeições.

#### 📖 [Região ICMS Saída — Documentação](documentacao_regiao_icms.md)
Tela `93`: mapeamento contextual que liga **contexto da operação → Natureza de Operação aplicada**:
- Cabeçalho com Tipo (PESSOA/PRODUTO), CSTs cobertos, Operação e vigência
- Configurações (sub-CRUD) com filtros de loja, estado, regime, atividade, IE e tipo de item
- Natureza de Operação como pivô; CFOP, CST, alíquotas e CBS/IBS exibidos a partir dela
- Flags `Manter CST/CSOSN`, `Manter Base/Aliq.` e `Manter Red/Aliq. IBS/CBS` para sobrescrever o NCM
- Vigência sempre aplicada; especificidade da linha decide o vencedor

#### ⚡ [Região ICMS Saída — Guia Rápido](guia_rapido_regiao_icms.md)
Checklist para cadastrar uma Região, anatomia da tela, comportamento dos curingas (`-1` / vazio), regras de coerência CFOP × Tipo × Localização e soluções para os erros recorrentes.

#### ❓ [Região ICMS Saída — FAQ](faq_regiao_icms.md)
Conceito, escolha entre múltiplas linhas, aplicação no movimento, override do NCM, validações e relação com Tipos de Movimento e Natureza de Operação.

#### 📖 [Natureza de Operação — Documentação](documentacao_natureza_operacao.md)
Tela `36`: cadastro central dos parâmetros fiscais por tipo de operação. Consolida:
- CFOP principal com autocomplete inteligente (ajusta Tipo e Localização)
- Regras de ICMS, PIS/COFINS, CBS/IBS (Reforma Tributária) e CSOSN
- CFOP Reverso para importação de XML (mapeia o CFOP de saída do fornecedor)
- CFOPs alternativos para Material de Uso/Consumo e Ativo Imobilizado
- Flags `Manter` para fazer a Natureza prevalecer sobre a Região ICMS
- Flags `Não Gerar Crédito` (ICMS e PIS/COFINS) com efeito direto no SPED

#### ⚡ [Natureza de Operação — Guia Rápido](guia_rapido_natureza_operacao.md)
Checklists separados para Naturezas de Saída e de Entrada, anatomia das abas (Importar XML, Informações, Extras, Pis/Confis), tabela de coerência CFOP × Tipo × Localização e soluções para erros recorrentes.

#### ❓ [Natureza de Operação — FAQ](faq_natureza_operacao.md)
Conceito, autocomplete do CFOP, regras fiscais, flags Manter, Importar XML, Reforma Tributária e como a Natureza chega ao item do movimento.

#### 📖 [Região ICMS ST Saída — Documentação](documentacao_regiao_icms_st_saida.md)
Tela `94`: regras de cálculo do ICMS por Substituição Tributária. Trabalha com:
- Percentuais diretos de **B.C. ICMS ST**, **MVA** e **alíquota ICMS-ST** por contexto
- Vínculo por **Produto** ou por **Pessoa**, com bloqueio de exclusão quando há produtos vinculados
- Flag `Usar MVA NCM` para puxar a margem direto do NCM do item
- Modo de cálculo `Industria MT` para o regime de indústrias de Mato Grosso

#### ⚡ [Região ICMS ST Saída — Guia Rápido](guia_rapido_regiao_icms_st_saida.md)
Checklist para cadastrar uma Região ICMS-ST, anatomia da tela, formato das listas de lojas/estados, operações do detalhe e erros mais comuns.

#### ❓ [Região ICMS ST Saída — FAQ](faq_regiao_icms_st_saida.md)
Diferença para a `93`, escolha entre Tipo `PRODUTO` × `PESSOA`, papel do `Usar MVA NCM`, quando usar `Industria MT` e como destravar a exclusão quando há produtos vinculados.

---

## 🎯 Por Onde Começar

- **👤 Primeira leitura** — abra a [Documentação da Reforma Tributária](documentacao_reforma_tributaria.md) para entender o cronograma fiscal e depois passe pela [Documentação da Manifestação](documentacao_manifestacao_destinatario.md) para o fluxo de NF-e e CT-e da SEFAZ. O lançamento subsequente em entrada está em [Movimentação — Importar XML](../Movimentacao/documentacao_importar_xml.md).
- **🔧 Configurador** — foque nas seções de cadastro de NCM e regras tributárias na [Documentação da Reforma Tributária](documentacao_reforma_tributaria.md), e use o [FAQ](faq_reforma_tributaria.md) para casos específicos.
- **⚡ Operacional / Suporte** — o guia rápido da [Manifestação do Destinatário](guia_rapido_manifestacao_destinatario.md) cobre a rotina diária no atendimento; para a etapa de lançamento, consulte o [Guia Rápido — Importar XML](../Movimentacao/guia_rapido_importar_xml.md) em Movimentação.

---

## 🔗 Módulos Relacionados

- **[Financeiro](../Financeiro/README.md)** — DRE e Portadores; lançamentos contábeis dos tributos.
- **[Movimentação](../Movimentacao/README.md)** — onde a reforma é aplicada na emissão de documentos fiscais; também é onde as NF-e manifestadas são lançadas como entrada.

---

**📅 Última atualização**: Maio de 2026  
**📦 Versão**: 1.7  
**🎯 Público-alvo**: Usuários, contadores, configuradores e equipe de suporte Sol.NET
