---
title: "FAQ: Módulo RH - Folha de Pagamento - Sol.NET"
permalink: /RH/faq/
---
# ❓ FAQ - Perguntas Frequentes: Módulo RH - Folha de Pagamento

## 📑 Índice

- [🔧 Configuração e Cadastros](#-configuração-e-cadastros)
- [💰 Cálculos e Processamento](#-cálculos-e-processamento)
- [🔗 Integrações](#-integrações)
- [📄 eSocial e Obrigações](#-esocial-e-obrigações)
- [🛠️ Problemas Técnicos](#️-problemas-técnicos)
- [📊 Relatórios](#-relatórios)
- [🎯 Cenários Específicos](#-cenários-específicos)
- [💡 Dicas de Produtividade](#-dicas-de-produtividade)

---

## 🔧 Configuração e Cadastros

### **P: Como faço o primeiro cadastro de funcionário no sistema?**
**R:** 
1. Menu RH > Cadastros > Funcionários
2. Pressione F4 (Novo)
3. Preencha obrigatoriamente:
   - **Aba Dados Pessoais**: Nome, CPF, RG, data nascimento
   - **Aba Trabalhista**: Matrícula, data admissão, cargo, salário
   - **Aba Contábil**: Centro de custo, conta salário, conta encargos
4. Opcionalmente preencha:
   - **Aba Benefícios**: Vale transporte, vale refeição, plano saúde
   - **Aba Documentos**: CTPS, PIS, título eleitor
   - **Aba Dependentes**: Para IRRF e salário família
5. Pressione F5 para salvar
6. Gere o evento S-2200 (Admissão) no eSocial

### **P: Qual a diferença entre cargo e função?**
**R:**
- **Cargo**: Posição formal na empresa (ex: "Analista Financeiro")
  - Cadastrado em: RH > Cadastros > Cargos
  - Tem CBO, faixa salarial, requisitos
  - Usado para eSocial e relatórios oficiais
  
- **Função**: Atividade específica desempenhada
  - Pode ser diferente do cargo
  - Usado para controles internos
  - Exemplo: Cargo "Assistente" exercendo função "Recepcionista"

### **P: Como configurar o rateio de um funcionário em múltiplos centros de custo?**
**R:**
1. Abra o cadastro do funcionário
2. Vá para Aba "Rateio"
3. Clique em "Adicionar Rateio"
4. Informe:
   - Centro de Custo: Departamento
   - Percentual: % a ser alocado
   - Conta Contábil: Conta de despesa específica
5. Adicione quantos rateios necessários (total deve ser 100%)
6. Exemplo prático:
   ```
   Centro Custo 001 - Administrativo: 60%
   Centro Custo 002 - Vendas: 40%
   ```
7. O sistema dividirá salário e encargos automaticamente

### **P: Como criar um novo evento (rubrica) na folha?**
**R:**
Menu RH > Cadastros > Eventos > F4

Preencha:
- **Código**: Número único (ex: 150 para "Comissão Vendas")
- **Descrição**: Nome que aparecerá no holerite
- **Tipo**: 
  - Vencimento (aumenta o valor a receber)
  - Desconto (diminui o valor a receber)
- **Incidências**: Marque se incide sobre:
  - INSS (maioria dos vencimentos)
  - FGTS (maioria dos vencimentos)
  - IRRF (vencimentos menos descontos permitidos)
  - 13º Salário
  - Férias
- **Conta Contábil**: Vincule a conta do plano de contas
- **Código eSocial**: Informe a rubrica correspondente na tabela S-1010

**Exemplo - Comissão sobre Vendas:**
```
Código: 150
Descrição: Comissão sobre Vendas
Tipo: Vencimento
Incidências: INSS ✓ | FGTS ✓ | IRRF ✓
Conta: 6.1.01.005 - Comissões Vendas
eSocial: 1409 - Comissões
```

### **P: Onde configuro as contas contábeis para integração com o DRE?**
**R:**
Há 3 locais (em ordem de prioridade):

1. **Por Funcionário** (mais específico):
   - Cadastro do Funcionário > Aba Contábil
   - Permite contas diferentes por pessoa

2. **Por Departamento**:
   - Cadastros > Departamentos > Aba Contábil
   - Todos do departamento usam essas contas

3. **Configuração Global** (padrão):
   - RH > Configurações > Integração Contábil
   - Usado quando não há configuração específica

**Contas essenciais:**
```
Débito (Despesas):
- Conta Salários
- Conta Encargos
- Conta Provisão 13º
- Conta Provisão Férias

Crédito (Passivos):
- Salários a Pagar
- INSS a Recolher
- FGTS a Recolher
- IRRF a Recolher
```

### **P: Como atualizar em lote vários funcionários (ex: reajuste salarial)?**
**R:**
Menu RH > Processos > Atualização em Lote

Opções:
1. **Reajuste Salarial**:
   - Selecione funcionários (por cargo, depto, ou todos)
   - Escolha tipo: Percentual ou Valor Fixo
   - Informe o percentual (ex: 5%)
   - Data vigência do reajuste
   - Sistema atualiza e gera histórico

2. **Alteração de Benefícios**:
   - Selecione grupo de funcionários
   - Altere valor VT, VR, ou plano saúde
   - Aplique em lote

3. **Mudança de Departamento**:
   - Útil em reorganizações
   - Selecione funcionários
   - Informe novo departamento/centro custo

**IMPORTANTE**: Sempre faça backup antes de atualizações em lote!

---

## 💰 Cálculos e Processamento

### **P: Como o sistema calcula as horas extras?**
**R:**
O cálculo depende do tipo de hora extra:

**1. Hora Extra 50% (dias úteis):**
```
Valor Hora Normal = Salário ÷ 220 horas
Valor Hora Extra 50% = Valor Hora Normal × 1,5

Exemplo (Salário R$ 3.000,00):
Hora Normal = R$ 3.000 ÷ 220 = R$ 13,64
10 horas extras 50% = R$ 13,64 × 1,5 × 10 = R$ 204,60
```

**2. Hora Extra 100% (domingos e feriados):**
```
Valor Hora Extra 100% = Valor Hora Normal × 2

4 horas em domingo = R$ 13,64 × 2 × 4 = R$ 109,12
```

**3. DSR sobre Horas Extras:**
```
DSR = (Total HE ÷ Dias Úteis) × Domingos/Feriados

Mês com 22 dias úteis e 5 domingos:
DSR = (R$ 204,60 ÷ 22) × 5 = R$ 46,50
```

**Configuração:**
Menu RH > Configurações > Parâmetros Folha
- Considerar DSR sobre HE: Sim
- Base de cálculo: 220 horas (padrão CLT)

### **P: Por que o INSS calculado é diferente do que eu esperava?**
**R:**
Desde 2020, o Brasil usa **tabela progressiva** para INSS (não é mais alíquota fixa!).

**Como funciona:**
Cada faixa do salário tem uma alíquota diferente, similar ao IRRF.

**Exemplo (Salário R$ 5.000,00):**
```
Faixa 1: R$ 1.320,00 × 7,5% = R$ 99,00
Faixa 2: (R$ 2.571,29 - R$ 1.320,00) × 9% = R$ 112,62
Faixa 3: (R$ 3.856,94 - R$ 2.571,29) × 12% = R$ 154,28
Faixa 4: (R$ 5.000,00 - R$ 3.856,94) × 14% = R$ 160,03
────────────────────────────────────────────
TOTAL INSS: R$ 525,93 (10,52% efetivo)
```

**NÃO É**: R$ 5.000,00 × 14% = R$ 700,00 ❌

**Para conferir:**
Menu RH > Ferramentas > Calculadora INSS
Digite o salário bruto e veja o cálculo detalhado

### **P: Como funciona o cálculo do IRRF?**
**R:**
O IRRF também usa tabela progressiva, mas com deduções:

**Passo 1 - Base de Cálculo:**
```
Salário Bruto
(-) INSS descontado
(-) Dependentes (R$ 189,59 cada)
(-) Pensão alimentícia (se judicial)
(=) Base de Cálculo IRRF
```

**Passo 2 - Aplicar Alíquota:**
```
Aplica alíquota conforme faixa
Subtrai parcela a deduzir
```

**Exemplo (Salário R$ 5.000, 2 dependentes):**
```
Base: R$ 5.000,00 - R$ 525,93 (INSS) - R$ 379,18 (2 dep) = R$ 4.094,89
Alíquota: 22,5% (faixa R$ 3.751,06 a R$ 4.664,68)
Cálculo: R$ 4.094,89 × 22,5% = R$ 921,35
Dedução: R$ 921,35 - R$ 651,73 = R$ 269,62
IRRF: R$ 269,62
```

### **P: Como o sistema calcula as provisões de 13º e férias?**
**R:**
**Provisão de 13º Salário:**
```
Provisão Mensal = (Salário Base + Médias de HE/Comissões) ÷ 12

Exemplo:
Salário: R$ 4.000,00
Média HE (últimos 12 meses): R$ 500,00
Base: R$ 4.500,00
Provisão/mês: R$ 4.500,00 ÷ 12 = R$ 375,00

Encargos (FGTS 8%): R$ 375,00 × 8% = R$ 30,00
```

**Provisão de Férias:**
```
Provisão Mensal = (Salário + Médias + 1/3 Constitucional) ÷ 12

Exemplo:
Salário: R$ 4.000,00
Média HE: R$ 500,00
Subtotal: R$ 4.500,00
Adicional 1/3: R$ 1.500,00
Total: R$ 6.000,00
Provisão/mês: R$ 6.000,00 ÷ 12 = R$ 500,00

Encargos (FGTS 8%): R$ 500,00 × 8% = R$ 40,00
```

**Configuração:**
Menu RH > Configurações > Provisões
- Provisionar 13º: Ativado
- Provisionar Férias: Ativado
- Considerar médias: Últimos 12 meses

### **P: Como processar férias de um funcionário?**
**R:**
Menu RH > Férias > Programação de Férias

**Passo a passo:**
1. Selecione o funcionário
2. Sistema mostra períodos aquisitivos disponíveis
3. Escolha o período (ex: 01/01/2023 a 31/12/2023)
4. Informe:
   - Data início: Quando começam as férias
   - Dias: 30 (integral) ou menos (fracionado)
   - Abono pecuniário: Se vender 10 dias
5. Sistema calcula:
   ```
   Valor Férias: R$ 4.000,00 (salário)
   Adicional 1/3: R$ 1.333,33
   Total Bruto: R$ 5.333,33
   
   Descontos:
   INSS: R$ 491,45
   IRRF: R$ 280,00 (se aplicável)
   
   Líquido: R$ 4.561,88
   ```
6. Gerar recibo de férias
7. Baixar da provisão
8. Pagar até 2 dias antes do início

**Lançamento Contábil:**
```
D - 2.1.3.02 - Provisão Férias (baixa)
C - 2.1.2.01 - Férias a Pagar (líquido)
C - 2.1.2.02 - INSS a Recolher
C - 2.1.2.04 - IRRF a Recolher
```

### **P: Como calcular uma rescisão de contrato?**
**R:**
Menu RH > Rescisão > Nova Rescisão

O sistema calcula automaticamente todas as verbas conforme tipo de desligamento:

**Demissão sem justa causa:**
- ✅ Saldo de salário (dias trabalhados)
- ✅ Aviso prévio (trabalhado ou indenizado)
- ✅ 13º proporcional
- ✅ Férias vencidas + 1/3
- ✅ Férias proporcionais + 1/3
- ✅ Saque FGTS + multa 40%

**Pedido de demissão:**
- ✅ Saldo de salário
- ✅ 13º proporcional
- ✅ Férias vencidas + 1/3
- ✅ Férias proporcionais + 1/3
- ❌ Aviso prévio indenizado
- ❌ Multa FGTS 40%

**Demissão por justa causa:**
- ✅ Saldo de salário
- ❌ Aviso prévio
- ❌ 13º proporcional
- ✅ Férias vencidas + 1/3 (se houver)
- ❌ Férias proporcionais
- ❌ Saque FGTS
- ❌ Multa FGTS

**IMPORTANTE:**
- Pagar até 10 dias da notificação
- Gerar TRCT (Termo de Rescisão)
- Enviar S-2299 (Desligamento) ao eSocial
- Enviar S-5001 (FGTS) para liberação saque

---

## 🔗 Integrações

### **P: Como a folha de pagamento integra com o DRE?**
**R:**
Após processar a folha:

1. **Gerar Lançamentos Contábeis:**
   Menu RH > Processos > Gerar Lançamentos Contábeis
   
2. **O sistema faz:**
   - Identifica centro de custo de cada funcionário
   - Agrupa por conta contábil configurada
   - Gera lançamentos de débito (despesas) e crédito (passivos)
   - Atualiza saldos no Plano de Contas
   
3. **Lançamentos típicos:**
   ```
   D - 6.2.01 - Salários Administrativo
   D - 6.2.02 - Encargos Sociais
   D - 6.2.03 - Provisão 13º Salário
   D - 6.2.04 - Provisão Férias
   C - 2.1.2.01 - Salários a Pagar
   C - 2.1.2.02 - INSS a Recolher
   C - 2.1.2.03 - FGTS a Recolher
   C - 2.1.3.01 - Provisão 13º a Pagar
   C - 2.1.3.02 - Provisão Férias a Pagar
   ```

4. **Reflete no DRE:**
   - Despesas com pessoal aparecem no agrupamento correto
   - Por centro de custo (se configurado)
   - Permite análise de custo por departamento

**Para conferir:**
Menu Financeiro > DRE > Gerar DRE
Veja as despesas com pessoal no período

### **P: Como gerar os títulos a pagar da folha no Financeiro?**
**R:**
Menu RH > Processos > Gerar Financeiro

O sistema cria automaticamente:

1. **Salários Líquidos:**
   - Valor: Total líquido da folha
   - Vencimento: Dia 5 do mês seguinte
   - Tipo: Salários
   - Portador: Conforme configurado (TED, conta corrente)

2. **INSS Patronal + Descontado:**
   - Valor: INSS empresa + INSS funcionários
   - Vencimento: Dia 20 do mês seguinte
   - Código barras: GPS automático

3. **FGTS:**
   - Valor: 8% sobre folha
   - Vencimento: Dia 7 do mês seguinte
   - Referência: Competência (MM/AAAA)

4. **IRRF:**
   - Valor: Total retido dos funcionários
   - Vencimento: Último dia útil 2º decêndio
   - Código: DARF 0561

**Configuração:**
RH > Configurações > Integração Financeira
- Ativar: "Gerar Títulos Automaticamente"
- Definir portadores padrão
- Configurar históricos

### **P: É possível importar dados do ponto eletrônico?**
**R:**
Sim! Menu RH > Importação > Ponto Eletrônico

**Formatos suportados:**
- AFD (Arquivo Fonte de Dados - padrão MTE)
- ACJEF (Arquivo Controle de Jornada Eletrônica de Funcionários)
- TXT personalizado (configure layout)
- Excel/CSV (via assistente de importação)

**Processo:**
1. Export arquivo do relógio de ponto
2. RH > Importação > Ponto Eletrônico
3. Selecione arquivo
4. Escolha competência (mês/ano)
5. Sistema processa e calcula:
   - Horas normais trabalhadas
   - Horas extras 50% e 100%
   - Faltas e atrasos
   - Adicional noturno
   - DSR sobre horas extras
6. Confira relatório de importação
7. Aprove ou ajuste manualmente

**Integração contínua:**
Configure importação automática diária:
RH > Configurações > Ponto Eletrônico > Importação Automática

### **P: Como funciona a integração com o eSocial?**
**R:**
O Sol.NET gera automaticamente os eventos do eSocial:

**Eventos de Tabela (uma vez):**
- S-1000: Dados do Empregador
- S-1005: Estabelecimentos
- S-1010: Rubricas (eventos da folha)
- S-1020: Lotações (departamentos)

**Eventos Não Periódicos (conforme ocorrência):**
- S-2200: Admissão (ao cadastrar funcionário)
- S-2206: Alteração Contratual (mudança salário/cargo)
- S-2230: Afastamento Temporário
- S-2299: Desligamento (rescisão)

**Eventos Periódicos (mensais):**
- S-1200: Remuneração (gerado ao processar folha)
- S-1210: Pagamentos Diversos
- S-1299: Fechamento Mensal

**Fluxo automático:**
1. Processar folha (F9)
2. Sistema gera S-1200 automaticamente
3. Validar eventos (RH > eSocial > Validar)
4. Enviar ao eSocial (manual ou automático)
5. Receber retorno e protocolo
6. Fechar competência com S-1299

**Configuração:**
RH > Configurações > eSocial
- Certificado Digital (A1 ou A3)
- Ambiente: Produção
- Envio automático: Ativado (recomendado)

---

## 📄 eSocial e Obrigações

### **P: Quais eventos do eSocial o Sol.NET gera automaticamente?**
**R:**
**Gerados Automaticamente:**
- ✅ S-1200 (Remuneração) - ao processar folha
- ✅ S-1210 (Pagamentos Diversos) - se houver
- ✅ S-2200 (Admissão) - ao cadastrar com data
- ✅ S-2299 (Desligamento) - ao processar rescisão
- ✅ S-2300 (Trabalhador Sem Vínculo) - se configurado

**Gerados Manualmente:**
- 📝 S-1000 (Empregador) - configuração inicial
- 📝 S-1005 (Estabelecimentos) - cadastro de filiais
- 📝 S-1010 (Rubricas) - ao cadastrar eventos
- 📝 S-1020 (Lotações) - ao cadastrar departamentos
- 📝 S-2206 (Alteração Contratual) - mudanças cadastrais
- 📝 S-2230 (Afastamento) - licenças, férias
- 📝 S-1299 (Fechamento) - fim do mês

**Para enviar manualmente:**
Menu RH > eSocial > Eventos Pendentes
Selecione eventos > Enviar

### **P: Como corrigir um erro no eSocial já enviado?**
**R:**
**Tipo 1 - Evento Rejeitado (não processou):**
1. Consulte o erro no extrato do eSocial
2. RH > eSocial > Eventos com Erro
3. Corrija os dados no cadastro
4. Reenvie o mesmo evento
5. Não precisa retificar

**Tipo 2 - Evento Processado mas com Erro:**
1. RH > eSocial > Retificação de Eventos
2. Localize o evento original (informar recibo)
3. Sistema carrega dados enviados
4. Corrija as informações
5. Envie evento retificador
6. Sistema usa mesmo número de recibo original

**Erros Comuns e Soluções:**

| Erro | Causa | Solução |
|------|-------|---------|
| CPF Inválido | CPF errado ou inativo | Corrigir no cadastro e reenviar |
| Data Incompatível | Admissão após evento | Ajustar datas e retificar |
| Rubrica não cadastrada | Falta S-1010 | Cadastrar rubrica na tabela |
| CAEPF obrigatório | Falta no S-1000 | Incluir no cadastro empregador |

**IMPORTANTE:** 
- Eventos de tabela (S-1000, S-1010, etc.) devem ser enviados ANTES dos eventos de folha
- Mantenha sempre o Serpro/Gov.br atualizados

### **P: Como gerar e enviar a SEFIP?**
**R:**
Menu RH > Obrigações > SEFIP

**Processo completo:**

1. **Processar Folha:**
   - Folha do mês deve estar fechada e conferida

2. **Gerar Arquivo SEFIP:**
   - Selecione competência (MM/AAAA)
   - Escolha tipo:
     - Mensal (normal)
     - 13º Salário
     - Rescisão
   - Gere arquivo .sfi

3. **Validar no Sistema:**
   - Sol.NET faz validação prévia
   - Confira:
     - Todos funcionários têm PIS
     - Valores de FGTS corretos
     - Código GPS correto
     - Dados da empresa completos

4. **Importar no Aplicativo SEFIP:**
   - Baixe SEFIP atualizado (site Caixa)
   - Arquivo > Importar > Arquivo de Transmissão
   - Selecione o .sfi gerado

5. **Validar no SEFIP:**
   - SEFIP faz validações adicionais
   - Corrija erros se houver
   - Gere RE (Relação de Empregados)
   - Confira totalizadores

6. **Transmitir:**
   - Conectividade Social ICP
   - Certificado Digital necessário
   - Guarde número do protocolo

7. **Gerar GRF:**
   - Após transmissão
   - Guia para pagamento FGTS
   - Vencimento: Dia 7

**Prazo:** Até dia 7 do mês seguinte

**Arquivo gerado contém:**
- Remuneração de cada trabalhador
- Base de cálculo FGTS (8%)
- Informações de movimentação
- Afastamentos e licenças

### **P: Como emitir o Informe de Rendimentos para funcionários?**
**R:**
Menu RH > Relatórios > Informe de Rendimentos

**Processo:**

1. **Selecionar Ano-Calendário:**
   - Ano anterior (ex: 2024 para IR 2025)

2. **Escolher Tipo:**
   - Modelo Simplificado (padrão RFB)
   - Modelo Completo (com detalhamento mensal)
   - Modelo Empresa (personalizado com logo)

3. **Selecionar Funcionários:**
   - Todos ativos e demitidos no ano
   - Por departamento
   - Individual (matrícula/CPF)

4. **Informações Incluídas:**
   - Rendimentos tributáveis (salários, HE, férias, 13º)
   - Contribuição Previdenciária Oficial (INSS)
   - Imposto de Renda Retido (IRRF)
   - Rendimentos isentos (se houver)
   - 13º salário separadamente
   - Dependentes declarados

5. **Gerar e Distribuir:**
   - PDF individual por funcionário
   - E-mail automático (se configurado)
   - Impressão em lote
   - Portal do colaborador (acesso online)

**Prazo:** Até 28 de fevereiro

**Validação:**
- Confronte valores com DIRF
- Confira CPF e nome completo
- Valide dependentes informados

**DICA:** Configure envio automático por e-mail:
RH > Configurações > E-mail > Informe Rendimentos Automático

### **P: O que fazer se a RAIS/eSocial Social der erro de envio?**
**R:**
**Para eSocial Social:**

Consulte o tipo de erro:
- Menu RH > eSocial > Consultar Retornos
- Identifique o código do erro

**Erros Comuns:**

**Erro 1:** "Empregador não encontrado"
- Causa: S-1000 não enviado ou incorreto
- Solução: Enviar/corrigir S-1000 primeiro

**Erro 2:** "Trabalhador já possui vínculo ativo"
- Causa: Tentativa de admitir funcionário já ativo
- Solução: Verificar se não foi enviado duplicado

**Erro 3:** "Incompatibilidade de data"
- Causa: Data de evento anterior à admissão
- Solução: Ajustar datas no cadastro

**Erro 4:** "Rubrica não cadastrada"
- Causa: Evento da folha sem correspondente no S-1010
- Solução: Enviar S-1010 com a rubrica primeiro

**Para RAIS:**

RAIS foi substituída pelo eSocial, mas para anos anteriores:

1. **Validar Cadastros:**
   - Todos têm PIS válido
   - Datas de admissão/demissão corretas
   - Nacionalidade informada

2. **Regerar Arquivo:**
   - RH > Obrigações > RAIS
   - Marcar "Validar antes de gerar"
   - Corrigir inconsistências

3. **Transmitir:**
   - Portal RAIS Online (Gov.br)
   - Upload do arquivo
   - Conferir recibo

**Suporte Oficial:**
- eSocial: esocial.gov.br
- RAIS: rais.gov.br

---

## 🛠️ Problemas Técnicos

### **P: Funcionário não aparece na folha do mês atual**
**R:**
Verifique em ordem:

1. **Status do Cadastro:**
   - Abra o cadastro (F2 + matrícula)
   - Status deve ser "Ativo"
   - Se "Demitido" ou "Afastado", não processa

2. **Data de Admissão:**
   - Deve ser anterior ou igual ao período da folha
   - Ex: Admitido em 15/01, processa a partir de Janeiro

3. **Afastamento:**
   - Menu RH > Afastamentos
   - Verifique se há afastamento sem vencimento ativo

4. **Filtros da Tela:**
   - Na tela de processamento
   - Verifique filtros de departamento/centro custo
   - Marque "Todos" ou o específico do funcionário

5. **Data de Demissão:**
   - Se demitido antes do período, não aparece
   - Ex: Demitido 20/01, não aparece em Fevereiro

**Se ainda não aparecer:**
- RH > Ferramentas > Reconstruir Índices
- Processar novamente

### **P: Valor líquido diferente entre holerite e título a pagar**
**R:**
**Causas possíveis:**

1. **Arredondamentos:**
   - Sistema arredonda para 2 decimais
   - Diferença de centavos é normal

2. **Descontos Posteriores:**
   - Verifique se adicionou descontos após gerar financeiro
   - Solução: Regerar financeiro

3. **Adiantamentos:**
   - Adiantamento quinzenal foi lançado separadamente
   - Líquido do holerite = Bruto - Descontos - Adiantamento
   - Título a pagar = Só o saldo

4. **Múltiplos Títulos:**
   - Sistema pode gerar títulos separados:
     - Salário principal
     - Férias
     - Rescisão
   - Some todos os títulos

**Para conferir:**
```sql
Holerite:
Total Vencimentos: R$ 5.500,00
Total Descontos: R$ 1.100,00
Líquido: R$ 4.400,00

Financeiro:
Título Salário: R$ 3.400,00
Título Adiantamento (já pago): R$ 1.000,00
Total: R$ 4.400,00 ✓
```

**Solução:**
- Exclua títulos gerados
- Regere financeiro: RH > Processos > Gerar Financeiro
- Confira novamente

### **P: Provisão de férias não está sendo lançada automaticamente**
**R:**
**Checklist de configuração:**

1. **Ativar Provisões:**
   - Menu RH > Configurações > Provisões
   - "Provisionar Férias Mensalmente" = ✓ Ativado

2. **Contas Contábeis:**
   - RH > Configurações > Integração Contábil
   - "Conta Provisão Férias" = Informada (ex: 6.2.04)
   - "Conta Provisão Férias a Pagar" = Informada (ex: 2.1.3.02)
   - "Conta FGTS sobre Férias" = Informada

3. **Funcionários com Cadastro Completo:**
   - Cada funcionário deve ter:
     - Centro de custo definido
     - Conta contábil de salário
     - Data de admissão válida

4. **Processar Provisões:**
   - Após processar folha mensal
   - Menu RH > Processos > Processar Provisões
   - Selecione competência
   - Execute

5. **Conferir Lançamento:**
   - Menu Financeiro > DRE
   - Procure conta 6.2.04 - Provisão Férias
   - Deve ter valor = (Total Folha + 1/3) ÷ 12

**Executar manualmente (se necessário):**
```
RH > Processos > Provisões > Recalcular Provisões
Selecione período (ex: últimos 12 meses)
Execute
```

### **P: Sistema está lento ao processar a folha**
**R:**
**Otimizações:**

1. **Processamento por Lotes:**
   - Em vez de processar 500 funcionários de uma vez
   - Processe por departamento:
     - Administrativo (100)
     - Vendas (150)
     - Produção (200)
     - Etc.

2. **Desativar Validações Durante Processamento:**
   - RH > Configurações > Performance
   - Desmarcar "Validar limites durante processamento"
   - Validar após processar

3. **Limpar Histórico Antigo:**
   - Menu RH > Manutenção > Arquivar Folhas Antigas
   - Mova folhas com mais de 5 anos para arquivo
   - Mantém performance

4. **Rebuild de Índices:**
   - RH > Ferramentas > Manutenção Banco
   - Reconstruir Índices
   - Executar fora do horário comercial

5. **Atualizar Estatísticas:**
   - Menu RH > Ferramentas > Atualizar Estatísticas
   - Melhora plano de execução das consultas

6. **Hardware:**
   - Verifique:
     - Memória RAM disponível (mínimo 8GB)
     - Espaço em disco (SSD recomendado)
     - Antivírus não bloqueando banco de dados

**Suporte Técnico:**
Se persistir: suporte.tecnico@solnet.com.br
Informe:
- Número de funcionários
- Tempo de processamento
- Configuração do servidor

---

## 📊 Relatórios

### **P: Como emitir holerite de um funcionário específico?**
**R:**
**Método 1 - Direto do Cadastro:**
1. F2 (Consulta rápida)
2. Digite nome ou matrícula
3. F10 (Gerar Holerite)
4. Selecione competência
5. Escolha formato (PDF, impressão, e-mail)

**Método 2 - Por Relatório:**
1. Menu RH > Relatórios > Holerite
2. Filtros:
   - Competência: MM/AAAA
   - Funcionário: Específico
3. Gerar

**Método 3 - Portal do Funcionário:**
- Funcionário acessa: solnet.com.br/portal
- Login: CPF + senha
- Menu "Meus Holerites"
- Seleciona competência
- Download PDF

**Formatos disponíveis:**
- PDF (padrão)
- Excel (para análise)
- E-mail direto ao funcionário
- Impressão térmica (para ponto)

### **P: Como gerar relatório de custo por departamento?**
**R:**
Menu RH > Relatórios > Custo por Centro

**Configurações:**
1. **Período:**
   - Mês específico
   - Intervalo (ex: Jan a Dez)
   - Ano completo

2. **Filtros:**
   - Todos os departamentos
   - Específico(s)
   - Por tipo (direto/indireto)

3. **Detalhamento:**
   - Resumido: Só totais
   - Analítico: Com detalhes por funcionário
   - Gráfico: Visualização comparativa

4. **Informações Incluídas:**
   - Salários
   - Encargos (INSS, FGTS)
   - Benefícios (VT, VR, plano)
   - Provisões (13º, férias)
   - Horas extras
   - **Total Geral por Departamento**

5. **Análises Possíveis:**
   - Percentual sobre receita
   - Custo médio por funcionário
   - Evolução mensal
   - Comparativo orçado x realizado

**Export:**
- Excel (com gráficos)
- PDF (para apresentação)
- CSV (para BI)

**Exemplo de saída:**
```
Departamento Administrativo:
Salários: R$ 50.000,00
Encargos: R$ 14.000,00
Benefícios: R$ 8.000,00
Provisões: R$ 10.000,00
TOTAL: R$ 82.000,00 (28% da receita)
```

### **P: Como consultar histórico salarial de um funcionário?**
**R:**
Menu RH > Consultas > Histórico Salarial

1. **Selecionar Funcionário:**
   - F2 para busca rápida
   - Ou informar matrícula

2. **Período:**
   - Desde admissão
   - Últimos 12 meses
   - Personalizado

3. **Informações Exibidas:**
   - Data do reajuste
   - Salário anterior
   - Salário novo
   - Percentual de aumento
   - Motivo (dissídio, mérito, promoção)
   - Usuário que alterou

4. **Gráfico de Evolução:**
   - Visualização temporal
   - Comparativo com inflação
   - Média do departamento

**Exemplo:**
```
João da Silva - Matrícula 001

Data       | Salário  | Reajuste | Motivo
-----------|----------|----------|------------------
01/01/2022 | R$ 3.000 | -        | Admissão
01/05/2022 | R$ 3.180 | 6%       | Dissídio
01/01/2023 | R$ 3.500 | 10%      | Promoção Analista
01/05/2023 | R$ 3.717 | 6,2%     | Dissídio
01/01/2024 | R$ 4.000 | 7,6%     | Mérito
```

---

## 🎯 Cenários Específicos

### **P: Como processar folha complementar (ex: comissões atrasadas)?**
**R:**
Menu RH > Processos > Folha Complementar

**Quando usar:**
- Comissões calculadas após fechamento
- Bonificações decididas depois
- Correções de valores
- Horas extras não lançadas

**Processo:**
1. **Criar Folha Complementar:**
   - Selecione competência da folha original
   - Marque "Folha Complementar"
   - Informe descrição (ex: "Comissões Janeiro")

2. **Lançar Eventos:**
   - Apenas os eventos complementares
   - Sistema mantém eventos da folha original

3. **Processar:**
   - Calcula INSS, IRRF, FGTS sobre complemento
   - Considera limite de teto (INSS) já usado
   
4. **Gerar Holerite Complementar:**
   - Emite holerite separado
   - Ou holerite consolidado (original + complementar)

5. **Integração:**
   - Lançamentos contábeis complementares
   - Títulos a pagar adicionais
   - eSocial: S-1200 retificador

**Exemplo:**
```
Folha Original (processada dia 25):
Salário: R$ 3.000,00
INSS: R$ 360,00
Líquido: R$ 2.640,00

Folha Complementar (dia 30 - comissões):
Comissão: R$ 1.500,00
INSS: R$ 172,00 (considerando já descontado)
IRRF: R$ 85,00 (recalculado sobre total)
Líquido Adicional: R$ 1.243,00

Pagamento:
Dia 5: R$ 2.640,00 (salário)
Dia 10: R$ 1.243,00 (complemento)
```

### **P: Como fazer acerto de contas (diferenças de meses anteriores)?**
**R:**
Menu RH > Processos > Acertos

**Tipos de acerto:**

1. **Diferenças Salariais:**
   - Dissídio retroativo
   - Correção de salário lançado errado

2. **Horas Extras Não Pagas:**
   - Banco de horas vencido
   - HE não lançadas

3. **Descontos Indevidos:**
   - Devolução de valores
   - Correção de faltas lançadas erradas

**Processo:**

1. **Identificar Diferença:**
   - Calcule: Valor Correto - Valor Pago = Diferença

2. **Criar Evento de Acerto:**
   - RH > Cadastros > Eventos
   - Código: 900-999 (eventos de acerto)
   - Descrição: "Acerto Salário - Ref. MM/AAAA"

3. **Lançar na Folha Atual:**
   - Processe normalmente a folha do mês
   - Adicione evento de acerto
   - Sistema calcula encargos sobre acerto

4. **Encargos e Impostos:**
   - INSS: Recolher sobre acerto
   - IRRF: Aplicar tabela progressiva
   - FGTS: 8% sobre diferença
   - **ATENÇÃO:** Encargos incidem no mês do pagamento, não do competência original

5. **Contabilização:**
   - Lançar na competência atual
   - Histórico: "Acerto ref. MM/AAAA"

**Exemplo - Dissídio Retroativo:**
```
Dissídio Maio/2024: 10% retroativo a Janeiro

Funcionário com salário R$ 3.000,00:
Janeiro a Abril (4 meses): R$ 3.000 × 10% × 4 = R$ 1.200

Lançamento em Maio:
Evento: Acerto Dissídio Jan-Abr
Valor: R$ 1.200,00
INSS: Calcular sobre R$ 1.200 (mês maio)
IRRF: Somar com salário maio e recalcular
FGTS: R$ 1.200 × 8% = R$ 96,00

Pagar em Maio junto com folha normal
```

**Observação Fiscal:**
Para diferenças grandes, consulte contador sobre:
- Tributação de acertos
- Possibilidade de parcelamento
- Impacto no eSocial

### **P: Como processar férias coletivas?**
**R:**
Menu RH > Férias > Férias Coletivas

**Planejamento:**

1. **Definir Parâmetros:**
   - Período: Datas início e fim
   - Departamentos: Todos ou específicos
   - Dias: Quantidade (mínimo 10 dias por período)
   - Parcelas: Máximo 2 períodos por ano

2. **Comunicações Obrigatórias:**
   - Sindicato: 15 dias antes
   - MTE: 15 dias antes
   - Funcionários: Com antecedência razoável

**Processamento no Sistema:**

1. **Cadastrar Férias Coletivas:**
   - RH > Férias > Férias Coletivas > Novo
   - Informe:
     - Descrição: "Férias Coletivas Final de Ano 2024"
     - Data início: 23/12/2024
     - Data fim: 05/01/2025
     - Dias: 14 dias (10 úteis)
     - Departamentos: Todos

2. **Selecionar Funcionários:**
   - Sistema lista todos do(s) departamento(s)
   - Marque os que tirarão férias
   - Desmarque gestores/essenciais (se aplicável)

3. **Calcular Férias:**
   - Sistema calcula para cada funcionário:
     - Verifica período aquisitivo disponível
     - Calcula valor (salário + 1/3)
     - Desconta INSS e IRRF
     - Baixa da provisão

4. **Gerar Recibos:**
   - Em lote para todos
   - PDF individual para assinatura
   - Envio por e-mail automático

5. **Comunicar MTE:**
   - RH > Férias Coletivas > Comunicação MTE
   - Gerar documento oficial
   - Enviar via eSocial (evento futuro)

6. **Pagamento:**
   - Até 2 dias antes do início
   - Gerar título no financeiro
   - Processar pagamento

**eSocial:**
- Enviar S-1280 (Comunicação Férias Coletivas)
- Informar no S-1200 individual de cada funcionário

**Exemplo:**
```
Empresa: 100 funcionários
Período: 23/12/2024 a 05/01/2025 (14 dias)

Cálculo por funcionário:
Salário: R$ 4.000,00
14 dias férias: R$ 4.000,00 × (14/30) = R$ 1.867,00
Adicional 1/3: R$ 1.867,00 ÷ 3 = R$ 622,00
Total Bruto: R$ 2.489,00

INSS: R$ 269,00
IRRF: R$ 120,00
Líquido: R$ 2.100,00

Multiplicar por 100 funcionários
Pagamento total: R$ 210.000,00
```

### **P: Como processar 13º salário?**
**R:**
**Calendário:**
- **1ª Parcela**: Até 30/novembro (50% sem descontos)
- **2ª Parcela**: Até 20/dezembro (saldo com descontos)

**Processamento 1ª Parcela:**

Menu RH > 13º Salário > 1ª Parcela

1. **Calcular:**
   - Base: Salário de dezembro ÷ 2
   - Proporção: Meses trabalhados ÷ 12
   - Sem descontos (INSS, IRRF)

2. **Exemplo:**
   ```
   Funcionário admitido em março (10 meses):
   Salário: R$ 4.000,00
   Média HE: R$ 500,00
   Base: (R$ 4.000 + R$ 500) × 10 ÷ 12 = R$ 3.750
   1ª Parcela: R$ 3.750 ÷ 2 = R$ 1.875,00
   Líquido: R$ 1.875,00 (sem descontos)
   ```

3. **Gerar Títulos:**
   - RH > 13º Salário > Gerar Financeiro
   - Vencimento: 30/novembro

4. **Baixar Provisão (50%):**
   - Sistema baixa metade da provisão acumulada

**Processamento 2ª Parcela:**

Menu RH > 13º Salário > 2ª Parcela

1. **Calcular:**
   - Total 13º: Salário dezembro × meses ÷ 12
   - Saldo: Total - 1ª Parcela
   - Aplicar descontos:
     - INSS sobre valor total (não só 2ª parcela)
     - IRRF sobre valor total
   
2. **Exemplo:**
   ```
   Total 13º: R$ 3.750,00
   1ª Parcela já paga: R$ 1.875,00
   Saldo bruto: R$ 1.875,00
   
   Descontos (sobre total R$ 3.750):
   INSS: R$ 412,00
   IRRF: R$ 95,00
   
   2ª Parcela líquida:
   R$ 1.875,00 - R$ 412,00 - R$ 95,00 = R$ 1.368,00
   ```

3. **Gerar Títulos:**
   - Vencimento: 20/dezembro
   - Inclui INSS e FGTS a recolher

4. **Baixar Provisão Restante:**
   - Sistema baixa 50% restante + encargos

**eSocial:**
- Informar no S-1200 de dezembro
- Código específico para 13º salário
- S-1210 se 13º complementar

**Rescisão com 13º Proporcional:**
- Calcular meses trabalhados no ano
- Incluir 13º proporcional nas verbas rescisórias
- Descontar 1ª parcela se já paga

---

## 💡 Dicas de Produtividade

### **P: Posso processar a folha por departamento ao invés de todos juntos?**
**R:**
Sim! É até recomendado para empresas grandes.

**Vantagens:**
- ✅ Mais rápido (processa menos funcionários por vez)
- ✅ Facilita conferência (foca em um grupo)
- ✅ Permite correções sem reprocessar tudo
- ✅ Diferentes responsáveis por área

**Como fazer:**

1. **Processamento Departamental:**
   ```
   Menu RH > Processar Folha
   Filtros:
   - Departamento: Administrativo
   - F9 (Processar)
   
   Depois:
   - Departamento: Vendas
   - F9 (Processar)
   
   E assim por diante...
   ```

2. **Consolidação:**
   - Sistema mantém tudo na mesma competência
   - Relatórios consolidam automaticamente
   - Integração contábil agrupa tudo

3. **Vantagem Adicional:**
   - Gestor de cada área pode conferir seu departamento
   - Delegar responsabilidades
   - Reduzir gargalos

**Cuidado:**
- Não feche a competência até processar todos
- Conferir totalizadores finais
- eSocial: Enviar S-1299 só depois de todos

### **P: Como criar templates de eventos para agilizar lançamentos?**
**R:**
Menu RH > Templates > Criar Template

**Casos de uso:**

**1. Comissões de Vendas:**
```
Template: "Comissões Equipe Vendas"

Eventos:
- 150 - Comissão Vendas: Variável
- 151 - Prêmio Meta: R$ 500,00 (fixo)
- 020 - DSR sobre Comissão: Calculado

Funcionários:
- João (001)
- Maria (002)
- Carlos (003)
[...]

Próximo mês:
- Carregar template
- Ajustar valores variáveis
- Processar
```

**2. Gratificações Fixas:**
```
Template: "Gratificações Mensais Gerência"

Evento: 120 - Gratificação Gerência
Funcionários: Todos com cargo "Gerente"
Valor: R$ 2.000,00

Aplicar todo mês automaticamente
```

**3. Descontos Recorrentes:**
```
Template: "Descontos Consignados"

Empréstimos, planos, pensões
Carrega valores de tabela externa
Aplica em lote
```

**Criar Template:**
1. Processar folha normal com eventos
2. Antes de finalizar: Salvar como Template
3. Nomear e descrever
4. Próximo mês: Carregar Template
5. Ajustar valores se necessário
6. Processar

**Economia de tempo:**
- Lançamento manual: 2h
- Com template: 15min

### **P: É possível automatizar o envio de holerites por e-mail?**
**R:**
Sim! Configure uma vez e sistema envia automaticamente.

**Configuração:**

1. **Ativar Recurso:**
   ```
   Menu RH > Configurações > E-mail
   
   Marcar:
   ✓ Enviar holerites automaticamente após processamento
   ✓ Enviar informe de rendimentos automaticamente
   ```

2. **Configurar E-mails Funcionários:**
   - Cada funcionário deve ter e-mail no cadastro
   - Aba "Contatos" > E-mail
   - Validar endereço (clique em "Testar")

3. **Personalizar Mensagem:**
   ```
   Assunto: Holerite {MES}/{ANO} - {NOME_FUNCIONARIO}
   
   Corpo:
   Olá {NOME},
   
   Segue em anexo seu holerite referente a {MES}/{ANO}.
   
   Atenciosamente,
   Departamento Pessoal
   ```

4. **Servidor SMTP:**
   - Configurar servidor de e-mail
   - Gmail, Outlook, servidor próprio
   - Porta, SSL, autenticação

5. **Automatização:**
   - Após processar folha (F9)
   - Após aprovar
   - Sistema envia automaticamente para todos

**Vantagens:**
- Economia de papel
- Acesso imediato do funcionário
- Comprovante de envio
- Portal colaborador dispensável

**Segurança:**
- E-mail criptografado (TLS)
- PDF pode ter senha (CPF do funcionário)
- Log de envios auditável

**Alternativa - Portal do Colaborador:**
- Funcionário acessa via web
- Consulta todos os holerites
- Baixa quando precisar
- Mais seguro que e-mail

### **P: Como configurar alertas para valores fora do padrão?**
**R:**
Menu RH > Configurações > Alertas

**Tipos de alerta:**

**1. Horas Extras Excessivas:**
```
Condição: Horas Extras > 40h no mês
Ação: Alerta vermelho na tela + e-mail gestor
Motivo: Possível erro ou necessidade contratar
```

**2. Salário Abaixo do Piso:**
```
Condição: Salário < Piso da Categoria
Ação: Bloquear processamento
Motivo: Ilegalidade
```

**3. INSS Acima do Teto:**
```
Condição: INSS > R$ 908,85
Ação: Alerta laranja + ajuste automático
Motivo: Limite legal
```

**4. IRRF Negativo:**
```
Condição: IRRF calculado < 0
Ação: Alerta + zerar valor
Motivo: Impossível IRRF negativo
```

**5. Variação Salarial Grande:**
```
Condição: Salário mês atual > 150% mês anterior
Ação: Alerta + solicitar confirmação
Motivo: Possível erro digitação
```

**6. Funcionário Sem Eventos:**
```
Condição: Funcionário ativo sem eventos no mês
Ação: Alerta amarelo
Motivo: Verificar afastamento ou esquecimento
```

**Configurar:**
1. RH > Configurações > Alertas
2. Escolher tipo de alerta
3. Definir condição (valor, percentual)
4. Escolher ação:
   - Alerta visual
   - E-mail
   - Bloquear processamento
   - Ajuste automático
5. Salvar

**No Processamento:**
- Sistema valida regras
- Exibe alertas em tela
- Permite correção antes de continuar
- Log de alertas para auditoria

**Exemplo prático:**
```
Processando 150 funcionários:

⚠️ ALERTAS ENCONTRADOS:

🔴 Urgente (2):
- João Silva: 55h extras (limite 40h)
- Maria Santos: Salário R$ 1.100 (piso R$ 1.320)

🟡 Atenção (3):
- Carlos Pereira: Sem eventos lançados este mês
- Ana Costa: Aumento 80% vs mês anterior
- Pedro Lima: 15 faltas (média 2 faltas/mês)

Deseja continuar processamento? [Sim] [Corrigir]
```

---

**📅 Última atualização**: Janeiro de 2025  
**📦 Versão**: 1.0  
**🎯 Público-alvo**: Usuários e administradores do módulo RH  

*Para dúvidas não cobertas neste FAQ, consulte a [Documentação Completa](Documentacao Folha de Pagamento.md) ou entre em contato com o suporte técnico.*
