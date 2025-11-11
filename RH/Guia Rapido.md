---
title: "Guia Rápido: Lançamentos de RH - Sol.NET"
permalink: /RH/guia-rapido/
---
# 🚀 Guia Rápido: Lançamentos de RH

## 📋 Checklist Mensal

### **Receber Informações da Contabilidade**
```
[ ] Solicitar resumo da folha de pagamento do mês
[ ] Conferir valores totais por categoria
[ ] Verificar separação por departamento
[ ] Confirmar competência (mês/ano)
```

### **Lançar no Sol.NET**
```
[ ] Acessar Menu RH → Lançamentos de Folha
[ ] Lançar Salários por departamento
[ ] Lançar Encargos Sociais
[ ] Lançar Benefícios (se houver)
[ ] Lançar Provisões (13º e Férias)
[ ] Salvar lançamentos
```

### **Conferir**
```
[ ] Gerar DRE do período
[ ] Verificar se valores aparecem nas contas corretas
[ ] Conferir totalização por centro de custo
[ ] Validar com resumo da contabilidade
```

---

## 💰 Tipos de Lançamento

### **Salários**
```
Conta Débito: 6.2.01 - Salários
Conta Crédito: 2.1.2.01 - Salários a Pagar
Valor: Conforme informado pela contabilidade
```

### **Encargos Sociais (INSS + FGTS)**
```
Conta Débito: 6.2.02 - Encargos Sociais
Conta Crédito: 2.1.2.02 - Encargos a Recolher
Valor: Conforme informado pela contabilidade
```

### **Benefícios (VT/VR/Plano Saúde)**
```
Conta Débito: 6.2.03 - Benefícios
Conta Crédito: 2.1.2.04 - Benefícios a Pagar
Valor: Conforme informado pela contabilidade
```

### **Provisão 13º Salário**
```
Conta Débito: 6.2.04 - Provisão 13º
Conta Crédito: 2.1.3.01 - Provisão 13º a Pagar
Valor: 1/12 do custo anual (conforme contabilidade)
```

### **Provisão Férias**
```
Conta Débito: 6.2.05 - Provisão Férias
Conta Crédito: 2.1.3.02 - Provisão Férias a Pagar
Valor: 1/12 do custo anual + 1/3 (conforme contabilidade)
```

---

## 🔄 Fluxo Rápido de Lançamento

### **Passo 1: Preparar**
- Tenha em mãos o resumo da contabilidade
- Identifique valores por categoria
- Separe por departamento se aplicável

### **Passo 2: Lançar**
1. Menu: **RH → Lançamentos de Folha**
2. **Novo Lançamento**
3. Preencher:
   - Data: Último dia do mês de competência
   - Histórico: "Folha de Pagamento - MM/AAAA"
   - Centro de Custo: Departamento
   - Conta Débito: Conta de despesa
   - Conta Crédito: Conta de passivo
   - Valor: Conforme contabilidade
4. **Salvar**

### **Passo 3: Conferir**
1. Menu: **Financeiro → DRE**
2. Selecionar período
3. Verificar valores nas contas
4. Comparar total com resumo da contabilidade

---

## 📊 Exemplo Prático

### Resumo da Contabilidade (Março/2024):
```
Salários Brutos:        R$ 40.000,00
Encargos (INSS + FGTS): R$ 11.200,00
Benefícios (VT/VR):     R$  3.000,00
Provisão 13º:           R$  3.333,33
Provisão Férias:        R$  4.444,44
──────────────────────────────────
Total:                  R$ 61.977,77
```

### Lançamentos no Sol.NET:

**Lançamento 1:**
```
Data: 31/03/2024
Histórico: Folha de Pagamento - Março/2024
D - 6.2.01 Salários → R$ 40.000,00
C - 2.1.2.01 Salários a Pagar → R$ 40.000,00
```

**Lançamento 2:**
```
Data: 31/03/2024
Histórico: Encargos sobre Folha - Março/2024
D - 6.2.02 Encargos Sociais → R$ 11.200,00
C - 2.1.2.02 Encargos a Recolher → R$ 11.200,00
```

**Lançamento 3:**
```
Data: 31/03/2024
Histórico: Benefícios - Março/2024
D - 6.2.03 Benefícios → R$ 3.000,00
C - 2.1.2.04 Benefícios a Pagar → R$ 3.000,00
```

**Lançamento 4:**
```
Data: 31/03/2024
Histórico: Provisão 13º - Março/2024
D - 6.2.04 Provisão 13º → R$ 3.333,33
C - 2.1.3.01 Provisão 13º a Pagar → R$ 3.333,33
```

**Lançamento 5:**
```
Data: 31/03/2024
Histórico: Provisão Férias - Março/2024
D - 6.2.05 Provisão Férias → R$ 4.444,44
C - 2.1.3.02 Provisão Férias a Pagar → R$ 4.444,44
```

**Total lançado:** R$ 61.977,77 ✓

---

## ⚠️ Problemas Comuns

### **Valores não aparecem no DRE**
**Causa:** Conta contábil errada ou período diferente  
**Solução:** Verifique a conta e a competência do lançamento

### **Total diferente da contabilidade**
**Causa:** Faltou lançar alguma categoria  
**Solução:** Compare item por item com o resumo fornecido

### **Lançamento duplicado**
**Causa:** Salvou o mesmo lançamento duas vezes  
**Solução:** Exclua um dos lançamentos duplicados

### **Centro de custo errado**
**Causa:** Selecionou departamento incorreto  
**Solução:** Edite o lançamento e corrija o centro de custo

---

## 💡 Dicas Produtivas

### **Padronize Históricos**
Use sempre o mesmo padrão:
- "Folha de Pagamento - MM/AAAA"
- "Encargos sobre Folha - MM/AAAA"
- "Provisão 13º - MM/AAAA"

### **Lance na Mesma Data**
Use sempre o último dia do mês de competência:
- Facilita filtros e consultas
- Organiza melhor o DRE

### **Separe por Departamento**
Se a empresa tem vários departamentos:
- Solicite valores separados da contabilidade
- Lance com centro de custo diferente
- Permite análise gerencial por área

### **Provisione Mensalmente**
Não esqueça de provisionar 13º e férias todo mês:
- Distribui o custo ao longo do ano
- DRE mais realista
- Evita "surpresas" no mês de pagamento

---

## 📞 Dúvidas Frequentes

**Preciso cadastrar todos os funcionários?**  
→ Não obrigatório. Cadastre apenas se quiser controle interno de nomes.

**O sistema calcula os valores?**  
→ Não. Lance os valores informados pela contabilidade.

**Como emito holerites?**  
→ O Sol.NET não emite holerites. Use o sistema da contabilidade.

**O sistema envia dados para o governo?**  
→ Não. Sol.NET não tem integração com órgãos externos.

**Posso lançar valores estimados?**  
→ Sim, se a contabilidade atrasar. Ajuste depois com valores reais.

---

**📅 Última atualização**: Janeiro de 2025  
**🎯 Público-alvo**: Usuários do módulo RH Sol.NET

*Para informações detalhadas, consulte a [Documentação Completa](Documentacao Folha de Pagamento.md).*
