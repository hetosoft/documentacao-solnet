# 📚 Documentação Sol.NET ERP

Portal central da documentação do **Sol.NET**, o ERP da Hetosoft. Use o menu lateral para navegar por todos os módulos a qualquer momento — abaixo está um resumo de cada um para você encontrar o ponto de partida certo.

---

## 🗂️ Módulos

### 💰 [Financeiro](Financeiro/)
DRE, portadores e Reforma Tributária.
- [Documentação DRE](Financeiro/Documentacao DRE.md)
- [Portadores e meios de pagamento](Financeiro/Documentacao Portadores.md)
- [Reforma Tributária no Sol.NET](Financeiro/Documentacao Reforma Tributaria.md) ⭐

### 📦 [Movimentação](Movimentacao/)
Operações comerciais, tipos de movimento e precificação.
- [Documentação Movimentação](Movimentacao/Documentacao Movimentacao.md)
- [Guia Rápido](Movimentacao/Guia Rapido.md) · [FAQ](Movimentacao/FAQ.md)
- [Preço de Venda — Guia do Usuário](Movimentacao/Preco de Venda - Guia do Usuario.md)

### 👥 [RH — Lançamentos](RH/)
Controle interno de despesas com pessoal para integração com o DRE.
- [Folha de Pagamento](RH/Documentacao Folha de Pagamento.md)
- [Processo Mensal](RH/Processo Mensal.md)
- [Guia Rápido](RH/Guia Rapido.md) · [FAQ](RH/FAQ.md)

### 🌱 [Agronômico](Agronomico/) ⭐ NOVO
Receituário Agronômico em conformidade com o MAPA.
- [Documentação Receituário](Agronomico/Documentacao Receituario Agronomico.md)
- [Guia Rápido](Agronomico/Guia Rapido.md) · [FAQ](Agronomico/FAQ.md)

<<<<<<< Updated upstream
---

### 📦 **[Módulo Movimentação](Movimentacao/)**
Sistema completo de controle de operações comerciais:

#### **📋 [Índice Completo](Movimentacao/)**
Portal de navegação para toda documentação de movimentação

#### **📖 [Documentação Completa](Movimentacao/documentacao/)**
- Visão geral e arquitetura do sistema
- Configuração de tipos de movimento
- Fluxo de trabalho detalhado
- Exemplos práticos e melhores práticas

#### **🚀 [Guia Rápido](Movimentacao/guia-rapido/)**
- Atalhos de teclado essenciais
- Checklist para novos movimentos
- Soluções rápidas para problemas comuns
- Configurações básicas

#### **❓ [FAQ - Perguntas Frequentes](Movimentacao/faq/)**
- Configuração e tipos de movimento
- Controle financeiro e de estoque
- Documentos fiscais e workflows
- Cenários específicos por segmento

#### **💰 [Precificação - Tabela de Preços](Movimentacao/preco-de-venda-guia/)**
Funcionalidades avançadas de precificação

#### **💲 [Preço de Venda - Guia do Usuário](Movimentacao/TabelaPreco/)**
Manual completo para gestão de preços de venda

---

### 👥 **[Módulo RH - Lançamentos de Recursos Humanos](RH/)**
Controle interno de despesas com pessoal para integração com DRE:

#### **📋 [Índice Completo](RH/)**
Portal de navegação para toda documentação de RH

#### **💼 [Documentação de Lançamentos de Folha](RH/Documentacao Folha de Pagamento.md)**
- Visão geral: o que o módulo faz e não faz
- Cadastro detalhado de funcionários (Pessoa RH)
- Fluxo de trabalho: contabilidade → lançamento → DRE
- Configuração de contas contábeis
- Vinculação obrigatória a funcionários
- Exemplos práticos de lançamentos

#### **📅 [Processo Mensal de Lançamento](RH/Processo Mensal.md)**
- Formulário de Lançamento RH detalhado
- Processo passo a passo mês a mês
- Como registrar valores de cada funcionário
- Conferência e validação
- Relatórios e dicas de produtividade

#### **🚀 [Guia Rápido](RH/Guia Rapido.md)**
- Checklist mensal de lançamentos
- Tipos de lançamento (salários, encargos, provisões)
- Fluxo rápido de registro de valores
- Problemas comuns e soluções

#### **❓ [FAQ - Perguntas Frequentes](RH/FAQ.md)**
- Sobre o módulo e suas limitações
- Vinculação obrigatória a funcionários
- Como fazer lançamentos individuais
- Integração com DRE
- Diferença entre módulo RH e sistema de folha completo

---

### 🌱 **[Módulo Agronômico - Receituário Agronômico](Agronomico/)** ⭐ NOVO
Emissão de receituário agronômico em conformidade com o MAPA:

#### **📋 [Índice Completo](Agronomico/)**
Portal de navegação para toda documentação do Módulo Agronômico

#### **📖 [Documentação Receituário Agronômico](Agronomico/Documentacao Receituario Agronomico.md)**
- Cadastros de apoio (culturas, diagnósticos, formulados, configuração de bula, embalagens)
- Cadastros administrativos (profissionais, ART/TRT, locais de aplicação)
- Emissão integrada à Movimentação (gatilho automático em movimentos fiscais) e emissão avulsa
- Validações automáticas (bula digital, saldo e validade de ART, vínculo cliente↔local, empresa↔ART)
- Cancelamento com estorno automático de saldo de ART
- Impressão via ReportBuilder no modelo legal

#### **🚀 [Guia Rápido](Agronomico/Guia Rapido.md)**
- Checklist de configuração inicial
- Fluxo diário com o gatilho automático na Movimentação
- Pesquisa de telas (F1) e códigos `ID_FORMULARIO`
- Soluções para os erros mais comuns

#### **❓ [FAQ - Perguntas Frequentes](Agronomico/FAQ.md)**
- Quem pode assinar (CREA × CFTA)
- Saldo/validade de ART
- Bloqueios por bula incompatível ou dose fora do permitido
- Cancelamento e estorno
- Conformidade legal e relação com órgãos estaduais

---

### 🛒 **[Self Checkout](SelfCheckout/)**
Aplicação de autoatendimento que faz parte do ecossistema Sol.NET:

#### **📋 [Índice Completo](SelfCheckout/)**
Portal de navegação para toda documentação do Self Checkout

#### **📖 [Documentação de Instalação](SelfCheckout/Documentacao Instalacao.md)**
- Pré-requisitos de hardware e software
- Instalação das DLLs Skia para renderização gráfica
- Instalação das fontes Poppins
- Configuração da balança Toledo Prix R7 (Baud Rate 2400)
- Configuração inicial do servidor
- Configurações padrão no Cadastro de Empresas (Sol.NET)
- Configuração de dispositivos no Self Checkout
- Testes e verificação completa
- Solução de problemas comuns
- Checklist final de instalação

#### **🚀 [Guia Rápido](SelfCheckout/Guia Rapido.md)**
- Checklist resumido de instalação
- Passos essenciais de configuração
- Comandos e atalhos principais
- Soluções rápidas para problemas comuns
- Scripts de automação

#### **❓ [FAQ - Perguntas Frequentes](SelfCheckout/FAQ.md)**
- Instalação e configuração
- Problemas com DLLs e fontes
- Integração com balança Toledo
- Operação do Self Checkout
- Integração com Sol.NET
- Manutenção e atualizações
=======
### 🛒 [Self Checkout](SelfCheckout/)
Aplicação de autoatendimento integrada ao Sol.NET.
- [Documentação de Instalação](SelfCheckout/Documentacao Instalacao.md)
- [Guia Rápido](SelfCheckout/Guia Rapido.md) · [FAQ](SelfCheckout/FAQ.md)
>>>>>>> Stashed changes

---

## 🎯 Por Onde Começar

- **👤 Novo usuário** — comece pelo módulo que vai usar e leia, na ordem: Documentação → Guia Rápido → FAQ.
- **🔧 Administrador / configurador** — vá direto às seções de **configuração** dentro de cada Documentação e use os FAQs para cenários específicos.
- **⚡ Usuário experiente** — os **Guias Rápidos** funcionam como referência de bolso para o dia a dia.

<<<<<<< Updated upstream
### **🔧 Administrador/Configurador?**
1. **Documentação completa**: Foque nas seções de configuração avançada
2. **Tipos e regras**: Configure tipos de movimento e regras de negócio  
3. **Integrações**: Configure portadores financeiros e integrações
4. **Cenários específicos**: Consulte FAQs para situações complexas

### **⚡ Usuário Experiente?**
1. **Guias rápidos**: Use como referência para atalhos e operações
2. **FAQs específicos**: Consulte para situações não habituais
3. **Novidades**: Acompanhe atualizações e novas funcionalidades
4. **Contribua**: Envie feedback para melhorias na documentação

---

## 🧭 Navegação Rápida

### **Por Área de Interesse**

#### **💳 Gestão Financeira**
- [Documentação DRE](Financeiro/Documentacao DRE.md)
- [Configuração de Portadores](Financeiro/Documentacao Portadores.md)
- [Controle Financeiro em Movimentações](Movimentacao/faq/#-controle-financeiro)
- [Processo de Quitação](Movimentacao/guia-rapido/#-atalhos-essenciais)

#### **🏛️ Reforma Tributária - Sol.NET** ⭐ DESTAQUE
- [Guia Completo - Uso no Sol.NET](Financeiro/Documentacao Reforma Tributaria.md)
- [Guia Rápido - Workflows Práticos](Financeiro/Guia Rapido Reforma Tributaria.md)
- [FAQ - Dúvidas Sol.NET](Financeiro/FAQ Reforma Tributaria.md)
- [Cadastro NCM e Classificações](Financeiro/Documentacao Reforma Tributaria.md#-cadastro-de-ncm---centro-de-controle)
- [Cálculos em Movimentação](Financeiro/Documentacao Reforma Tributaria.md#-movimentação---cálculo-de-tributos)

#### **👥 Gestão de Pessoal**
- [Folha de Pagamento Completa](RH/Documentacao Folha de Pagamento.md)
- [Guia Rápido RH](RH/Guia Rapido.md)
- [Integração RH com DRE](Financeiro/Documentacao DRE.md#-recursos-humanos-rh)
- [FAQ RH](RH/FAQ.md)

#### **🌱 Receituário Agronômico**
- [Documentação Completa](Agronomico/Documentacao Receituario Agronomico.md)
- [Guia Rápido](Agronomico/Guia Rapido.md)
- [FAQ](Agronomico/FAQ.md)
- [Configuração de Bula Digital](Agronomico/Documentacao Receituario Agronomico.md#-configuração-de-bula-bula-digital)
- [Gestão de ART/TRT](Agronomico/Documentacao Receituario Agronomico.md#-cadastro-de-arttrt)

#### **📊 Operações Comerciais**  
- [Fluxo de Trabalho Completo](Movimentacao/documentacao/#-fluxo-de-trabalho---passo-a-passo)
- [Tipos de Movimento](Movimentacao/documentacao/#-cadastro-de-tipos-de-movimento---centro-de-controle)
- [Exemplos Práticos](Movimentacao/documentacao/#-exemplos-pr%C3%A1ticos)

#### **⚙️ Configuração e Administração**
- [Cadastro de Tipos](Movimentacao/#-administradorconfigurador)
- [Configurações Avançadas](Financeiro/documentacao-portadores/#-configura%C3%A7%C3%A3o-avan%C3%A7ada)
- [Cenários Específicos](Movimentacao/faq/#-cen%C3%A1rios-espec%C3%ADficos)

#### **🆘 Suporte e Problemas**
- [Solução de Problemas](Movimentacao/documentacao/#-solu%C3%A7%C3%A3o-de-problemas-comuns)  
- [FAQ Completo](Movimentacao/faq/)
- [Problemas Comuns](Movimentacao/guia-rapido/#-problemas-comuns---solu%C3%A7%C3%B5es-r%C3%A1pidas)
=======
> 🔎 Toda tela do Sol.NET é aberta pela **pesquisa universal (F1)**, digitando o nome ou o código (`ID_FORMULARIO`) da tela.
>>>>>>> Stashed changes

---

## 🗺️ Mapa do Sistema

![](/Assets/SolNET%20Mindmap.svg)

---

**📅 Última atualização**: Abril de 2026  
**📦 Versão**: 2.1  
**🎯 Público-alvo**: Usuários finais, administradores e configuradores Sol.NET
