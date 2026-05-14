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

---

### 📥 Importar XML NF-e

#### 📖 [Documentação Importar XML](documentacao_importar_xml.md)
Como carregar o XML de uma NF-e e transformá-lo em movimento de entrada (ou saída, no caso de emissão própria):
- Tela `Importar XML NF-e` (código `204`) — consulta e filtros de XMLs carregados
- Carregamento via arquivo `.xml` e via Manifestação do Destinatário
- Sub-abas `XML`, `Cabeçalho`, `Itens`, `Financeiro`, `Conferência`
- Vínculo de itens do XML com o cadastro de produtos (manual, automático e cadastro durante o vínculo)
- Lançamento na movimentação: `Lançar NF-e`, `Lançar Parcial`, `Lançar Próprio` e `DANFE`
- Relação com a Manifestação do Destinatário

#### ⚡ [Guia Rápido — Importar XML](guia_rapido_importar_xml.md)
Cartão de referência para o suporte:
- Checklist da rotina padrão de importação
- Os três botões de lançamento e quando usar cada um
- Tabelas de status, conferência e financeiro
- Mensagens de erro mais comuns e como resolver
- Combinações úteis de filtros

#### ❓ [FAQ — Importar XML](faq_importar_xml.md)
Perguntas comuns sobre carregamento, vínculo de itens, lançamento e relação com Manifestação.

#### 🔬 [Conferência de XML](documentacao_conferencia_xml.md)
Fluxo dedicado da conferência física da mercadoria:
- Habilitação por loja no `Cadastro de Empresas`
- Estados da conferência (`Não Conferido`, `Em Andamento`, `Sem Divergência`, `Com Divergência`)
- Aba `Conferência` dentro do `Importar XML` e o que o conferente faz
- Reabertura de conferências finalizadas (permissão especial)
- Como a conferência interage com `Lançar NF-e` / `Lançar Parcial`

---

## 🎯 Por Onde Começar

- **👤 Primeira leitura** — abra a [Documentação da Reforma Tributária](documentacao_reforma_tributaria.md) para entender o cronograma fiscal, depois passe pela [Documentação da Manifestação](documentacao_manifestacao_destinatario.md) e pela [Documentação Importar XML](documentacao_importar_xml.md) para a rotina diária de entrada de notas.
- **🔧 Configurador** — foque nas seções de cadastro de NCM e regras tributárias na [Documentação da Reforma Tributária](documentacao_reforma_tributaria.md), e use o [FAQ](faq_reforma_tributaria.md) para casos específicos.
- **⚡ Operacional / Suporte** — os guias rápidos da [Manifestação do Destinatário](guia_rapido_manifestacao_destinatario.md) e do [Importar XML](guia_rapido_importar_xml.md) cobrem a rotina mais comum no atendimento.

---

## 🔗 Módulos Relacionados

- **[Financeiro](../Financeiro/README.md)** — DRE e Portadores; lançamentos contábeis dos tributos.
- **[Movimentação](../Movimentacao/README.md)** — onde a reforma é aplicada na emissão de documentos fiscais; também é onde as NF-e manifestadas são lançadas como entrada.

---

**📅 Última atualização**: Maio de 2026  
**📦 Versão**: 1.2  
**🎯 Público-alvo**: Usuários, contadores, configuradores e equipe de suporte Sol.NET
