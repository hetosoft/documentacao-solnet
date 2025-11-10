---
title: "Guia Rápido: Módulo RH - Folha de Pagamento - Sol.NET"
permalink: /RH/guia-rapido/
---
# 🚀 Guia Rápido: Módulo RH - Folha de Pagamento

## ⚡ Atalhos Essenciais

| Tecla | Função | Contexto |
|-------|--------|----------|
| **F2** | Consulta rápida | Buscar funcionário por nome/matrícula |
| **F4** | Novo registro | Criar novo funcionário/evento/cargo |
| **F5** | Salvar | Salvar alterações em cadastros |
| **F6** | Lançar evento | Adicionar evento na folha |
| **F8** | Imprimir | Imprimir relatórios/holerites |
| **F9** | Processar | Iniciar processamento da folha |
| **F10** | Gerar holerite | Emitir holerite individual |
| **Ctrl+F** | Buscar | Localizar texto em relatórios |
| **Ctrl+P** | Imprimir | Impressão rápida |
| **Esc** | Cancelar | Cancelar operação atual |

---

## 📋 Checklist Rápido - Folha Mensal

### **Semana 1 (Dias 1-7)**
```
[ ] Conferir cadastros atualizados
[ ] Verificar admissões e demissões do mês anterior
[ ] Atualizar dependentes (IRRF/Salário Família)
[ ] Registrar afastamentos (INSS, licenças)
[ ] Lançar comissões e gratificações fixas
```

### **Semana 2 (Dias 8-15)**
```
[ ] Importar ponto eletrônico
[ ] Conferir horas extras e faltas
[ ] Lançar eventos variáveis (bonificações, prêmios)
[ ] Verificar benefícios (VT, VR, plano de saúde)
[ ] Validar empréstimos e pensões alimentícias
```

### **Semana 3 (Dias 16-23)**
```
[ ] Processar folha de pagamento (F9)
[ ] Conferir totais: INSS, IRRF, FGTS
[ ] Validar líquido a pagar
[ ] Gerar holerites (F10)
[ ] Revisar valores discrepantes
[ ] Aprovar folha
```

### **Semana 4 (Dias 24-30)**
```
[ ] Gerar lançamentos contábeis
[ ] Processar provisões (13º e férias)
[ ] Gerar eventos eSocial (S-1200, S-1210)
[ ] Gerar SEFIP (FGTS)
[ ] Criar títulos a pagar (Financeiro)
[ ] Distribuir holerites
[ ] Fazer backup da folha
```

### **Início do Mês Seguinte**
```
[ ] Dia 5: Pagar salários
[ ] Dia 7: Enviar SEFIP e recolher FGTS
[ ] Dia 15: Fechar eSocial (S-1299)
[ ] Dia 20: Pagar INSS (GPS)
[ ] Último dia útil 2º decêndio: Pagar IRRF
```

---

## ⏱️ Prazos Críticos

### **Mensal**
- 📅 **Dia 5**: Pagamento de salários
- 📅 **Dia 7**: SEFIP e FGTS
- 📅 **Dia 15**: Fechamento eSocial periódico
- 📅 **Dia 20**: GPS (INSS)
- 📅 **Último dia útil 2º decêndio**: DARF (IRRF)

### **Anual**
- 📅 **28/Fev**: Informe de Rendimentos
- 📅 **Último dia útil Fev**: DIRF
- �� **22/Mar**: RAIS
- 📅 **30/Nov**: 1ª parcela 13º
- 📅 **20/Dez**: 2ª parcela 13º

---

## 🧮 Calculadora Rápida

### **INSS 2024**
```
Até R$ 1.320,00        → 7,5%
R$ 1.320,01 - R$ 2.571,29 → 9%
R$ 2.571,30 - R$ 3.856,94 → 12%
R$ 3.856,95 - R$ 7.507,49 → 14%
Teto máximo: R$ 908,85
```

### **IRRF 2024**
```
Até R$ 2.112,00        → Isento
R$ 2.112,01 - R$ 2.826,65 → 7,5%  (deduzir R$ 158,40)
R$ 2.826,66 - R$ 3.751,05 → 15%   (deduzir R$ 370,40)
R$ 3.751,06 - R$ 4.664,68 → 22,5% (deduzir R$ 651,73)
Acima de R$ 4.664,68   → 27,5% (deduzir R$ 884,96)

Deduções:
- R$ 189,59 por dependente
- INSS descontado
- Pensão alimentícia
```

### **FGTS**
```
FGTS = Salário Bruto × 8%
```

### **Horas Extras**
```
Hora Normal = Salário ÷ 220
Hora Extra 50% = Hora Normal × 1,5
Hora Extra 100% = Hora Normal × 2
DSR = (Horas Extras ÷ Dias Úteis) × Domingos
```

---

## 🔄 Fluxos Rápidos

### **Admitir Funcionário**
```
1. F4 (Novo Funcionário)
2. Preencher Dados Pessoais (CPF, RG, endereço)
3. Aba Trabalhista (cargo, salário, admissão)
4. Aba Contábil (centro custo, conta salário)
5. Aba Benefícios (VT, VR, plano saúde)
6. F5 (Salvar)
7. RH > eSocial > S-2200 (Admissão)
```

### **Processar Folha**
```
1. Conferir cadastros atualizados
2. Importar ponto (RH > Importar > Ponto)
3. Lançar eventos variáveis (F6)
4. F9 (Processar Folha)
5. Conferir totais e exceções
6. Gerar holerites (F10)
7. Aprovar folha
```

### **Processar Férias**
```
1. RH > Férias > Programação
2. Selecionar funcionário
3. Informar período aquisitivo
4. Definir data início e quantidade dias
5. Calcular férias
6. Conferir valor (salário + 1/3)
7. Gerar recibo de férias
8. Baixar provisão
```

### **Processar Rescisão**
```
1. RH > Rescisão > Nova
2. Selecionar funcionário
3. Informar data demissão e tipo
4. Sistema calcula verbas:
   - Saldo salário
   - Aviso prévio
   - 13º proporcional
   - Férias vencidas + proporcionais
   - FGTS + multa 40%
5. Conferir cálculos
6. Gerar TRCT
7. eSocial > S-2299 (Desligamento)
8. FGTS > S-5001 (Liberação)
```

---

## ��️ Configurações Rápidas

### **Criar Novo Evento (Rubrica)**
```
Menu: RH > Cadastros > Eventos > F4

Campos essenciais:
- Código: Número único (ex: 150)
- Descrição: Nome do evento
- Tipo: Vencimento ou Desconto
- Incidências: Marcar INSS, FGTS, IRRF
- Conta Contábil: Vincular
- Código eSocial: Informar rubrica

F5 para salvar
```

### **Configurar Integração Contábil**
```
Menu: RH > Configurações > Integração

Definir:
- Conta Salários (6.2.01)
- Conta Encargos (6.2.02)
- Conta Provisão 13º (6.2.03)
- Conta Provisão Férias (6.2.04)
- Conta Salários a Pagar (2.1.2.01)
- Conta INSS a Recolher (2.1.2.02)
- Conta FGTS a Recolher (2.1.2.03)

Ativar: "Gerar Lançamentos Automáticos"
```

### **Ativar eSocial**
```
Menu: RH > Configurações > eSocial

1. Escolher ambiente: Produção
2. Importar Certificado Digital (A1 ou A3)
3. Configurar dados empregador
4. Enviar eventos de tabela:
   - S-1000 (Empregador)
   - S-1005 (Estabelecimento)
   - S-1010 (Rubricas)
   - S-1020 (Lotações)
5. Ativar envio automático
```

---

## ⚠️ Problemas Comuns - Soluções Rápidas

### **Funcionário não aparece na folha**
```
Verificar:
✓ Status = Ativo
✓ Data admissão < período folha
✓ Sem afastamento sem remuneração
✓ Não demitido no período
✓ Filtros da tela (departamento/centro custo)
```

### **INSS diferente do esperado**
```
✓ Sol.NET usa tabela progressiva (correto)
✓ Não é cálculo simples (salário × alíquota)
✓ Use Calculadora INSS do sistema
✓ Menu: RH > Ferramentas > Calc INSS
```

### **Erro ao gerar eSocial**
```
Erros comuns:
1. CPF inválido → Corrigir cadastro
2. Data incompatível → Verificar admissão
3. Rubrica não existe → Cadastrar S-1010
4. Certificado vencido → Renovar

Solução: Corrigir e reenviar ou retificar
```

### **SEFIP não abre arquivo**
```
✓ Atualizar SEFIP (site Caixa)
✓ Verificar todos tem PIS válido
✓ Conferir competência correta
✓ Regerar marcando "Validar dados"
```

### **Diferença no líquido a pagar**
```
1. Imprimir holerite detalhado
2. Conferir evento por evento
3. Verificar descontos extras (empréstimos)
4. Conferir arredondamentos
5. Comparar com mês anterior
```

---

## 📊 Relatórios Principais

### **Emitir Holerite**
```
Menu: RH > Relatórios > Holerite
Opções:
- Individual (F10 no cadastro)
- Por departamento
- Todos os funcionários
- PDF ou impressão direta
```

### **Folha de Pagamento Analítica**
```
Menu: RH > Relatórios > Folha Analítica
Detalhamento completo:
- Todos os eventos por funcionário
- Totalização por evento
- Provisões do mês
- Base cálculo INSS/FGTS/IRRF
```

### **Relatório de Encargos**
```
Menu: RH > Relatórios > Encargos
Exibe:
- Total INSS Empresa
- Total FGTS
- Total IRRF
- Provisões (13º e Férias)
- Custo total folha
```

### **Custo por Centro**
```
Menu: RH > Relatórios > Custo Centro
Análise gerencial:
- Custo por departamento
- Comparativo mensal
- Gráficos de evolução
- Export para Excel
```

---

## 💡 Dicas Produtivas

### **Atalhos Personalizados**
```
Configure seus próprios atalhos:
Menu > Ferramentas > Personalizar Atalhos

Sugestões:
- F11: Relatório Folha Analítica
- F12: Suporte/Ajuda
- Ctrl+H: Histórico do funcionário
```

### **Templates de Eventos**
```
Crie templates para eventos recorrentes:
1. Processar folha com eventos
2. Menu: RH > Templates > Salvar Template
3. Nomear (ex: "Comissões Vendas")
4. Próximo mês: Carregar Template
```

### **Filtros Salvos**
```
Salve filtros frequentes:
- Departamento Administrativo
- Comissionados
- Hora Extra > 20h
- Afastados

Menu: Filtros > Salvar Filtro
```

### **Alertas Configuráveis**
```
Configure alertas automáticos:
Menu: RH > Configurações > Alertas

Exemplos:
- Hora extra acima de X horas
- Salário abaixo do piso
- INSS acima do teto
- IRRF negativo
```

---

## 🔍 Consultas Rápidas

### **Histórico do Funcionário**
```
F2 > Digite matrícula/nome
Clique em "Histórico"
Visualize:
- Todas as folhas
- Alterações salariais
- Férias tiradas
- Afastamentos
- Eventos lançados
```

### **Situação eSocial**
```
Menu: RH > eSocial > Consultar Situação
Informe CPF ou matrícula
Retorna:
- Eventos enviados
- Status (processado/rejeitado)
- Erros se houver
- Recibos de entrega
```

### **Posição de Provisões**
```
Menu: RH > Relatórios > Provisões
Visualize:
- Provisão 13º acumulada
- Provisão Férias acumulada
- Previsão de pagamento
- Valor por funcionário
```

---

## 📱 Acesso Mobile

### **Portal do Funcionário**
```
URL: solnet.com.br/portal
Acesso: CPF + senha

Funcionário pode:
- Visualizar holerites
- Baixar informe rendimentos
- Consultar saldo férias
- Atualizar dados pessoais
- Solicitar declarações
```

---

## �� Suporte Rápido

### **Ajuda Contextual**
```
Tecla F1 em qualquer tela
Exibe ajuda específica da funcionalidade
```

### **Chat Online**
```
Ícone de chat no canto inferior direito
Atendimento em horário comercial
```

### **Central de Ajuda**
```
Menu: Ajuda > Central de Ajuda
Base de conhecimento completa
Vídeos tutoriais
FAQ atualizado
```

### **Contatos Emergenciais**
```
Durante fechamento (dia 20-5):
- Suporte estendido até 20h
- E-mail: suporte.urgente@solnet.com.br
- WhatsApp: (xx) xxxxx-xxxx
```

---

## 🎯 Metas de Eficiência

### **Tempo Ideal por Processo**
```
Admissão: 15 minutos
Alteração cadastral: 5 minutos
Lançamento eventos mês: 2 horas
Processamento folha (100 func): 30 minutos
Conferência pós-processamento: 1 hora
Geração eSocial: 15 minutos
Geração SEFIP: 10 minutos
```

### **Redução de Erros**
```
Meta: < 1% de reprocessamentos
Técnicas:
- Usar checklists
- Conferência em dupla
- Alertas automáticos ativos
- Validação antes de finalizar
```

---

**📅 Última atualização**: Janeiro de 2025  
**📦 Versão**: 1.0  
**🎯 Público-alvo**: Usuários operacionais do módulo RH

*Este guia rápido serve como referência ágil para operações diárias. Para informações detalhadas, consulte a [Documentação Completa](Documentacao Folha de Pagamento.md).*
