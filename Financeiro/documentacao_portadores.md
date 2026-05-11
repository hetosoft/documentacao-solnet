---
title: "Documentação Técnica: Módulo Portadores - Sol.NET ERP"
permalink: /Financeiro/documentacao-portadores/
---
# 📄 Documentação Técnica: Módulo Portadores - Sol.NET ERP

## 🎯 Visão Geral

O **Módulo Portadores** é um componente essencial do sistema Sol.NET ERP, responsável pelo gerenciamento de instrumentos de pagamento e cobrança. Este módulo centraliza as configurações de diferentes tipos de documentos financeiros, permitindo controle detalhado sobre boletos bancários, carnês, notas promissórias, convênios, cheques e integrações bancárias.

### Principais Características:

- ✅ **Múltiplos tipos de documento**: Boleto, Carnê, Nota Promissória, Convênio, Cheque, Hetobank
- ✅ **Configuração bancária completa**: Suporte a 25+ bancos brasileiros
- ✅ **Controle por empresa**: Portadores específicos por loja/filial
- ✅ **Remessa eletrônica**: Formatos C240/C400 para automação bancária
- ✅ **Validações automáticas**: Regras de negócio integradas
- ✅ **Integração PIX**: Suporte completo ao sistema de pagamentos instantâneos
- ✅ **Comissões configuráveis**: Percentuais diferenciados por tipo de pagamento

---

## 🏗️ Estrutura do Módulo

### Organização da Interface

O módulo é organizado através do **Cadastro de Portadores** (código `[A CONFIRMAR]` na pesquisa F1), que centraliza todas as configurações e funcionalidades relacionadas ao gerenciamento de instrumentos de pagamento. A interface possui duas visualizações principais:

- **Visualização de Consulta**: Lista todos os portadores cadastrados com informações resumidas
- **Visualização de Cadastro**: Permite criação e edição detalhada de portadores através de abas especializadas

### Integração com Outros Módulos

O módulo Portadores integra-se diretamente com:
- **Contas a Receber/Pagar**: Controle de títulos e cobranças
- **Vendas/PDV**: Seleção de formas de pagamento
- **Financeiro**: Conciliação bancária e fluxo de caixa
- **Relatórios**: Geração de documentos e demonstrativos

## 📊 Estrutura da Interface: Abas e Funcionalidades

### Aba Principal - Informações Gerais

**Campos obrigatórios:**
- **Descrição**: Nome identificador do portador
- **Código**: Código único alfanumérico (até 30 caracteres)
- **Tipo Documento**: Define o comportamento do portador

**Campos opcionais:**
- **Descrição da Loja**: Empresa associada ao portador
- **Conta Corrente Associada**: Vinculação com contas bancárias
- **Caixa**: Caixa de destino para pagamentos
- **Forma de Pagamento**: Forma de pagamento padrão
- **Tipo Ent/Saída**: Controla se é usado em entradas, saídas ou ambos

**Configurações especiais:**
- **Mínimo Valor Parcela**: Define o valor mínimo para cada parcela
- **Sempre Pedir Autorização para Supervisor**: Exige aprovação gerencial
- **Somente Condições Pagamento Portador**: Restringe condições de pagamento
- **Parcela com Vencimento <= Hoje Mudar Portador Para**: Define portador alternativo para parcelas vencidas
- **Remover Juros e Multa da Condição de Pagamento**: Remove encargos automáticos

### 1. Aba Boleto - Configurações Bancárias

#### Seção: Dados Bancários Principais
O sistema oferece suporte a mais de 25 instituições bancárias brasileiras, incluindo Banco do Brasil, Santander, Caixa Econômica Federal, Bradesco, Itaú, HSBC, Banrisul, entre outros.

**Campos principais:**
- **Banco cobrança**: Seleção do banco emissor dos boletos
- **Layout**: Formato de impressão (Padrão, Carnê, Fatura, Entrega, Térmica, PIX)  
- **Remessa**: Tipo de arquivo para remessa bancária (C240/C400)
- **Beneficiário**: Código identificador do beneficiário no banco
- **Convênio**: Número do convênio bancário estabelecido
- **Variação**: Variação específica da carteira quando aplicável

#### Seção: Mensagens e Documentos
- **Mensagem para local do pagamento**: Texto instrucional customizável
- **Espécie Doc.**: Código do tipo de documento conforme banco
- **Espécie Moeda**: Símbolo da moeda utilizada
- **Carteira**: Tipo específico de carteira bancária
- **Aceite**: Define se o título possui aceite (Sim/Não)

#### Seção: Percentuais Financeiros
Configuração de encargos e descontos aplicáveis:
- **Valor Mora/Juros %**: Percentual mensal de juros por atraso
- **Valor Desconto %**: Percentual de desconto para pagamento antecipado
- **Valor Abatimento %**: Percentual de abatimento sobre o valor
- **Valor Multa %**: Percentual de multa por atraso

#### Seção: Prazos de Aplicação
Configuração de períodos para aplicação de regras:
- **Dias Multa/Juros**: Prazo após vencimento para aplicar encargos
- **Dias Desconto**: Prazo antes do vencimento para desconto
- **Dias Abatimento**: Período para aplicar abatimento
- **Dias Protesto**: Prazo para envio a protesto
- **Dias Baixa/Devolução**: Prazo para baixa automática do título

#### Seção: Controle de Numeração
**Última Sequencia ID** - Controle automático de numeração:
- **Nosso Número (Banco)**: Controle sequencial do banco
- **Arquivo Remessa (Banco)**: Numeração dos arquivos de remessa

#### Seção: Configurações Especiais
- **Taxa de Atualização**: Taxa para correção monetária
- **Tipo Protesto**: Modalidade de protesto a ser utilizada
- **Descrição da Loja - Remessa**: Identificação da empresa na remessa
- **Beneficiário (Zeros Esquerda)**: Formatação com zeros à esquerda
- **Característica Boleto**: Características especiais do documento
- **Salvar PDF no Banco de Dados**: Armazenamento digital dos boletos

#### Seção: Opções Avançadas
- **Ajustar Valor Recebido pela Taxa de Cobrança**: Aplica ajuste por taxa
- **Colocar Referência Boleto Anterior**: Inclui referência de boletos anteriores
- **Colocar Descrição Tipo de Contas**: Adiciona descrição do tipo de conta
- **Obs E-Mail**: Observações específicas para envio por e-mail
- **Pasta Padrão Abrir Arquivos (Retorno)**: Diretório para arquivos de retorno
- **Obs Boleto**: Observações gerais do boleto
- **Pasta Padrão Salvar Arquivos (Remessa)**: Diretório para arquivos de remessa
- **Baixa de Quitação Remessa e Avisos**: Configurações de baixa automática
- **Código Transmissão Remessa**: Código específico para transmissão
- **Ajustar Valor Quitação pelo Desc. e Abat.**: Ajuste automático por descontos

#### Seção: Instruções Bancárias
- **Instrução 1**: Primeira linha de instrução bancária
- **Instrução 2**: Segunda linha de instrução bancária
- **Adicionar Num. Doc. em Obs**: Inclui número do documento nas observações
- **Aceitar Recebimento Parcial**: Permite pagamentos parciais

#### Seção: Integração Digital (WebService)
- **WebService**: Habilitação da integração online
- **ClientID**: Identificador do cliente na integração
- **ClientSecret**: Chave secreta para autenticação
- **KeyUser**: Chave do usuário
- **Enviar ao Imprimir**: Transmissão automática na impressão

#### Seção: PIX - Pagamentos Instantâneos
- **Incluir PIX**: Habilita funcionalidade PIX
- **Tipo chave PIX**: Tipo da chave (CPF/CNPJ, E-mail, Telefone, Aleatória)
- **Chave PIX**: Valor da chave configurada
- **Consulta automática**: Verificação automática de pagamentos PIX

#### Seção: Contabilização
- **Plano de Contas**: Conta contábil para lançamentos
- **Centro de Custo**: Centro de custo associado
- **Tipo de Conta**: Classificação do tipo de conta
- **Não gerar registro de Tarifa Bancária**: Suprime lançamento de tarifas

### 2. Aba Carnê - Configurações de Carnê

**Funcionalidades:**
- **Relatório**: Seleção do layout específico para impressão de carnês
- Acesso direto ao catálogo de relatórios do sistema
- Configuração especializada para impressão em lote de carnês
- Personalização de layouts conforme necessidades da empresa

### 3. Aba Nota Promissória - Configurações de Promissórias

**Funcionalidades:**
- **Relatório**: Layout dedicado para notas promissórias
- Integração com sistema de impressão customizado
- Suporte a modelos padronizados e personalizados
- Conformidade com requisitos legais para promissórias

### 4. Aba Convênio - Gestão de Convênios

**Seção: Relatórios Especializados**
- **Relatório - Movimentação**: Relatório detalhado de movimentação de convênio
- **Relatório - Contas PR**: Relatório específico para contas a receber de convênio

**Características especiais:**
- Suporte a múltiplos relatórios para análises comparativas
- Flexibilidade na apresentação de dados conforme tipo de convênio
- Integração com sistema de faturamento especializado

### 5. Aba Empresas - **Portador por Empresa**

#### Interface de Controle
Esta seção permite definir quais empresas/lojas podem utilizar o portador específico.

**Grade de Empresas** - Lista todas as empresas cadastradas no sistema:
- **Descrição da Loja**: Nome completo da empresa/filial
- **Seleção**: Checkbox para ativar/desativar o portador para a empresa

**Menu de Ações Rápidas**:
- **"Selecionar Todos"**: Marca todas as empresas de uma vez
- **"Desmarcar Todos"**: Desmarca todas as seleções
- **Seleção Individual**: Controle empresa por empresa

**Regras de Negócio:**
- Um portador pode ser restrito a empresas específicas
- Empresas não selecionadas não visualizam o portador
- Controle granular por loja/filial
- Configuração flexível para redes de lojas

### 6. Aba Hetobank - Integração Digital

**Funcionalidades:**
- **Forma Pagamento Hetobank**: Vinculação com formas de pagamento específicas
- Integração direta com plataforma bancária digital
- Processamento automatizado de pagamentos eletrônicos
- Suporte a transações em tempo real

### 7. Aba Outros - Configurações Complementares

#### Seção: Comissões
Configuração de percentuais de comissão diferenciados:
- **A Vista %**: Percentual de comissão para vendas à vista
- **A Prazo %**: Percentual de comissão para vendas parceladas

#### Seção: Configurações Especiais
- **Boleto em Homologação**: Para testes em ambiente bancário
- **Mobile**: Habilitação para dispositivos móveis

---

## ⚙️ Tipos de Documento Suportados

### 1. BOLETO (Tipo: 0)
**Características:**
- ✅ Configuração bancária completa
- ✅ Remessa eletrônica (C240/C400)
- ✅ Nosso número automático
- ✅ Suporte PIX integrado
- ✅ Validações específicas de banco

**Regras de negócio:**
- Obrigatório definir banco de cobrança
- Necessário informar tipo de protesto
- Controle de numeração sequencial
- Integração com arquivos de retorno

### 2. CARNÊ (Tipo: 1)
**Características:**
- ✅ Layout específico para impressão
- ✅ Múltiplas parcelas em uma página
- ✅ Controle de vencimentos automático
- ✅ Integração com relatórios personalizados

### 3. NOTA PROMISSÓRIA (Tipo: 2)
**Características:**
- ✅ Modelo juridicamente válido
- ✅ Campos customizáveis
- ✅ Impressão em formulário específico
- ✅ Controle de vencimentos

### 4. CONVÊNIO (Tipo: 3)
**Características:**
- ✅ Relatórios especializados
- ✅ Controle de movimentação
- ✅ Integração com contas a receber
- ✅ Regra especial de mudança de portador

**Regras especiais:**
- Para portadores tipo CONVÊNIO, é obrigatório definir um "**Parcela com Vencimento <= Hoje Mudar Portador Para**"
- Esta configuração permite troca automática do portador quando parcelas vencem
- Funcionalidade essencial para controle de inadimplência em convênios

### 5. CHEQUE (Tipo: -2)
**Características:**
- ✅ Controle de permissões específicas
- ✅ Validação no processo de venda
- ✅ Integração com sistema de aprovação
- ✅ Histórico de devoluções

### 6. HETOBANK (Tipo: 4)
**Características:**
- ✅ Pagamentos digitais
- ✅ Integração API bancária
- ✅ PIX automático
- ✅ Conciliação eletrônica

---

---

## 🔧 Regras de Negócio e Validações

### 1. Validações de Campos Obrigatórios

**Validação de Descrição Única**
Não pode haver mais de um portador com a mesma descrição no sistema

**Validação de Código Único**  
Não pode haver mais de um portador com o mesmo código no sistema

### 2. Validações Específicas por Tipo

#### Boleto (Tipo: 0)
**Validação Tipo de Protesto Obrigatório**
Quando o tipo do documento for Boleto, é obrigatório informar o tipo de protesto

**Validação Dias Protesto Compatível**
Os dias de protesto só são permitidos para tipos específicos de documentos

**Validação Empresa Obrigatória**
Deve ser informada uma empresa através da **Descrição da Loja** ou **Descrição da Loja - Remessa**

#### Convênio (Tipo: 3)
**Validação Portador de Mudança Obrigatório**
Para portadores tipo CONVÊNIO é obrigatório definir o campo **Parcela com Vencimento <= Hoje Mudar Portador Para**

### 3. Validações de Relacionamento

**Validação de Exclusividade de Configuração de Empresa**
- A **Descrição da Loja** e **Descrição da Loja - Remessa** são mutuamente exclusivas
- **Descrição da Loja** individual e seleção múltipla na aba **Portador por Empresa** são mutuamente exclusivas

### 4. Validações de Configuração

**Validação Remoção de Juros/Multa**
A opção **Remover Juros e Multa da Condição de Pagamento** não é permitida para portadores tipo BOLETO

**Validação Conflito entre Prazos**
Quando definido **Dias Protesto**, não é possível definir **Dias Baixa/Devolução**

### 5. Validações na Exclusão

**Verificação de Uso em Outros Módulos**
Antes de excluir um portador, o sistema verifica automaticamente seu uso em:
- Cadastro de pessoas (clientes e fornecedores)
- Módulo de contas a receber e contas a pagar
- Histórico de movimentos financeiros

O sistema impedirá a exclusão caso existam vínculos ativos com o portador.

---

## 💾 Estrutura de Dados

### Organização das Informações do Portador

O sistema organiza as informações de cada portador em categorias bem definidas:

**Identificação Básica:**
- **Descrição**: Nome identificador único do portador
- **Código**: Código alfanumérico único para referência
- **Tipo**: Categoria do documento (Boleto, Carnê, Nota Promissória, etc.)

**Configurações Gerais:**
- **Descrição da Loja**: Empresa responsável pelo portador
- **Conta Corrente Associada**: Vinculação bancária
- **Caixa**: Destino dos pagamentos
- **Forma de Pagamento**: Forma padrão associada
- **Tipo Ent/Saída**: Controle de uso (entrada, saída ou ambos)

**Configurações Bancárias (para Boletos):**
- **Banco cobrança**: Instituição bancária emissora
- **Layout**: Modelo de impressão
- **Remessa**: Tipo de arquivo bancário (C240/C400)
- **Beneficiário**, **Convênio**, **Variação**: Identificadores bancários
- **Carteira**, **Espécie Doc.**, **Espécie Moeda**: Especificações do documento
- **Aceite**: Configuração de aceite do título

**Percentuais e Prazos Financeiros:**
- **Valor Mora/Juros %**: Encargos por atraso
- **Valor Desconto %**: Desconto para pagamento antecipado  
- **Valor Abatimento %** e **Valor Multa %**: Ajustes financeiros
- **Dias Multa/Juros**, **Dias Desconto**, **Dias Protesto**: Prazos de aplicação

**Configurações PIX:**
- **Incluir PIX**: Ativação de pagamento instantâneo
- **Tipo chave PIX**: Modalidade da chave (CPF/CNPJ, E-mail, Telefone, Aleatória)
- **Chave PIX**: Valor da chave configurada

**Relatórios e Layouts:**
- **Relatório** (Carnê): Modelo de impressão para carnês
- **Relatório** (Nota Promissória): Layout para promissórias
- **Relatório - Movimentação** e **Relatório - Contas PR**: Relatórios de convênio

**Comissões e Controles:**
- **A Vista %** e **A Prazo %**: Percentuais de comissão
- **Mínimo Valor Parcela**: Valor mínimo permitido
- **Sempre Pedir Autorização para Supervisor**: Controle de permissões

**Integração Hetobank:**
- **Forma Pagamento Hetobank**: Vinculação com pagamentos digitais

### Controle de Acesso por Empresa

O sistema permite associar portadores a empresas específicas através da funcionalidade **Portador por Empresa**, onde:
- Cada empresa pode ser selecionada individualmente
- Empresas não selecionadas não visualizam o portador
- Controle granular para redes de lojas ou filiais

### Controle de Numeração Sequencial

O sistema mantém controle automático de:
- **Nosso Número (Banco)**: Numeração sequencial para cada banco
- **Arquivo Remessa (Banco)**: Controle de arquivos enviados
- Sincronização automática com retornos bancários

---

## 🎨 Padrões de Uso e Boas Práticas

### 1. Configuração de Boleto Padrão

**Exemplo: Boleto Bancário Padrão**
- Exemplo: Configuração Banco do Brasil
- Descrição: 'BOLETO BANCO DO BRASIL'
- Tipo: Boleto
- Banco Cobrança: 'Banco do Brasil'
- Layout: 'Padrao'
- REMESSA: 'c400'
- Beneficiario: '12345678'
- Convenio: '987654321'
- Carteira: '17'
- Tipo Protesto: 3 - Nao Protestar
- Espécie Moeda: "$"
- Aceite: Não


### 2. Configuração de Carnê

**Exemplo: Carnê mensal**
- Descrição: "CARNÊ MENSAL LOJA"
- Código: "CARNE01"
- Tipo: Carnê
- Layout: Carnê
- Relatório: Vincular modelo customizado

### 3. Configuração PIX

**Exemplo: Portador com PIX**
- Descrição: "BOLETO COM PIX"
- Tipo: Boleto
- Layout: Padrão PIX
- Incluir PIX: Habilitado
- Tipo chave PIX: CNPJ
- Chave PIX: CNPJ da empresa

### 4. Configuração por Empresa

**Método 1: Empresa específica**
- Selecionar uma única empresa no campo **Descrição da Loja**

**Método 2: Múltiplas empresas**
- Utilizar a aba **Portador por Empresa** para seleção granular

**Método 3: Empresa para remessa**
- Usar **Descrição da Loja - Remessa** para empresa específica de envio

### 5. Validação de Configuração

**Verificações essenciais:**
- **Descrição**: Campo obrigatório e único
- **Código**: Campo obrigatório e único
- **Para boletos**: Banco cobrança obrigatório
- **Empresas**: Pelo menos uma forma de associação deve ser configurada

---

## 🔍 Cenários de Uso Comuns

### 1. Boleto Bancário Completo

**Objetivo**: Configurar boleto com remessa eletrônica

**Configuração:**
1. Tipo Documento: BOLETO
2. **Banco cobrança**: Selecionar banco
3. Dados bancários: **Beneficiário**, **Convênio**, **Carteira**
4. Percentuais: **Valor Mora/Juros %**, **Valor Multa %**, **Valor Desconto %**
5. Prazos: **Dias Protesto**, **Dias Baixa/Devolução**
6. PIX: Configurar **Chave PIX** se necessário

**Resultado**: Boletos com código de barras, PIX e remessa automática

### 2. Carnê para Vendas Parceladas

**Objetivo**: Imprimir carnês personalizados

**Configuração:**
1. Tipo Documento: CARNÊ
2. Layout: Carnê
3. **Relatório**: Selecionar modelo específico
4. Empresa: Definir loja emissora

**Resultado**: Carnê impresso com todas as parcelas

### 3. Convênio Empresarial

**Objetivo**: Gestão de convênios com empresas

**Configuração:**
1. Tipo Documento: CONVÊNIO
2. Portador Mudança: Definir portador para parcelas vencidas
3. Relatórios: Movimentação e contas a receber
4. Empresas: Múltiplas lojas se necessário

**Resultado**: Controle completo de convênios

### 4. Cheques com Controle

**Objetivo**: Aceitar cheques com validação

**Configuração:**
1. Tipo Documento: CHEQUE
2. Permissões: Sempre pedir autorização
3. Valor mínimo: Definir limite se necessário
4. Integração: Serasa/SPC para validação

**Resultado**: Controle rigoroso de cheques

### 5. Hetobank Digital

**Objetivo**: Pagamentos digitais integrados

**Configuração:**
1. Tipo Documento: HETOBANK
2. Forma Pagamento: Vincular forma específica
3. API: Configurar credenciais
4. PIX: Ativar se disponível

**Resultado**: Pagamentos automatizados

---

## 🛠️ Manutenção e Troubleshooting

### Problemas Comuns e Soluções

#### 1. Erro "Nosso Número Duplicado"

**Sintomas**: Rejeição na remessa bancária por numeração duplicada
**Causa**: Perda de sincronismo na numeração sequencial do **Nosso Número (Banco)**
**Solução**:
- Verificar o último nosso número utilizado no módulo de contas a receber
- Ajustar o controle sequencial através das configurações do portador
- Contatar o suporte técnico para restaurar a numeração correta

#### 2. PIX Não Aparece no Boleto

**Sintomas**: QR Code PIX ausente na impressão do boleto
**Causa**: Configuração incompleta na aba **Boleto**
**Solução**:
1. Verificar se **Incluir PIX** está habilitado
2. Confirmar se o **Layout** está configurado como "Padrão PIX"
3. Validar se a **Chave PIX** foi preenchida corretamente
4. Testar se o **Tipo chave PIX** está configurado adequadamente

#### 3. Remessa Não Gerada

**Sintomas**: Arquivo de remessa vazio ou não criado
**Causa**: Configurações de empresa ou filtros incorretos
**Solução**:
- Verificar se existe configuração em **Descrição da Loja** ou **Descrição da Loja - Remessa**
- Confirmar se a empresa atual está selecionada na aba **Portador por Empresa**
- Validar se o portador está ativo para a empresa que está tentando gerar a remessa

#### 4. Validação de Parcela Mínima

**Sintomas**: Erro ao gerar título com valor abaixo do esperado
**Causa**: Campo **Mínimo Valor Parcela** configurado no portador
**Solução**:
- Verificar o valor definido em **Mínimo Valor Parcela**
- Ajustar o valor da parcela para atender ao mínimo exigido
- Ou ajustar a configuração do portador se o limite estiver inadequado

### Logs e Auditoria

O sistema mantém automaticamente um log detalhado de todas as alterações realizadas nos portadores, incluindo:
- Data e hora de cada modificação
- Usuário responsável pela alteração
- Tipo de operação realizada (criação, edição, exclusão)
- Histórico de valores alterados

**Acesso aos Logs:**
- Abra a pesquisa universal (F1), digite **Auditoria** (código `[A CONFIRMAR]`) e abra a tela de logs.
- Filtrar por "Portadores" para ver apenas mudanças em portadores
- Consultar histórico específico por portador

### Backup e Restore

**Informações Incluídas no Backup:**
- Configurações completas do portador
- Vínculos com empresas, contas correntes e caixas
- Histórico de numeração sequencial
- Configurações de relatórios associados

**Procedimento de Backup:**
1. Acessar as configurações do sistema
2. Selecionar "Backup de Configurações"
3. Incluir dados dos portadores na exportação
4. Armazenar arquivo de backup em local seguro

**Procedimento de Restore:**
1. Verificar compatibilidade da versão
2. Fazer backup preventivo antes da restauração
3. Executar importação através das configurações do sistema
4. Validar integridade dos dados restaurados

---

## 📋 Checklist de Configuração

### Antes de Usar o Portador

- [ ] **Dados básicos completos**: Descrição, código e tipo
- [ ] **Empresa configurada**: Individual, múltipla ou remessa
- [ ] **Conta corrente vinculada** (se aplicável)
- [ ] **Validar unicidade**: Código não duplicado

### Para Boletos Bancários

- [ ] **Banco selecionado** e configurado
- [ ] **Dados bancários**: Beneficiário, convênio, carteira
- [ ] **Layout apropriado**: Padrão ou PIX
- [ ] **Remessa configurada**: C240 ou C400
- [ ] **Numeração inicializada**: Nosso número e arquivo remessa
- [ ] **Percentuais definidos**: Juros, multa, desconto
- [ ] **Prazos configurados**: Protesto, baixa, desconto
- [ ] **PIX configurado** (se necessário)

### Para Outros Documentos

- [ ] **Relatórios selecionados**: Carnê, nota promissória, convênio
- [ ] **Permissões definidas**: Autorização, valor mínimo
- [ ] **Comissões configuradas**: À vista e a prazo
- [ ] **Regras especiais**: Portador mudança (convênio)

### Testes Recomendados

- [ ] **Gerar documento teste**: Verificar layout e dados
- [ ] **Remessa bancária**: Testar arquivo de remessa
- [ ] **PIX**: Validar QR Code e chave
- [ ] **Integração**: Testar com sistema bancário
- [ ] **Relatórios**: Imprimir documentos finais

---

## 🔗 Integração com Outros Módulos

### 1. Módulo Contas a Receber/Pagar
- Vinculação automática de títulos ao portador
- Controle de vencimentos e juros
- Geração de remessa e processamento de retorno

### 2. Módulo PDV/Vendas
- Seleção de portador na venda
- Validação de permissões
- Controle de valor mínimo por parcela

### 3. Módulo Financeiro
- Conciliação bancária automática  
- Controle de fluxo de caixa
- Relatórios gerenciais

### 4. Módulo Fiscal
- Integração com nota fiscal
- Controle de impostos sobre serviços financeiros
- Auditoria fiscal

---

## 📞 Suporte

Para dúvidas técnicas ou problemas específicos:

1. **Consulte os logs**: abra a pesquisa universal (F1) e digite **Auditoria** (código `[A CONFIRMAR]`); filtre por "Portadores".
2. **Verifique configurações**: Duplo-clique no portador para editar
3. **Teste isolado**: Use ambiente de homologação quando disponível  
4. **Documente casos**: Contribua com novos cenários de uso

---

**Última atualização**: 07 de agosto de 2025  
**Versão**: 1.0  
**Responsável**: Equipe Sol.NET  
**Criado por**: Copilot Assistant

*Esta documentação fornece um guia completo para configuração e uso do módulo Portadores, essencial para o controle financeiro e bancário no Sol.NET ERP.*