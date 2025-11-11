---
title: "Guia Rápido: Lançamentos de RH - Sol.NET"
permalink: /RH/guia-rapido/
---
# 🚀 Guia Rápido: Lançamentos de RH

## ⚠️ Regra Fundamental

**Todo lançamento de RH deve estar vinculado a um funcionário específico.**

Não é possível lançar valores totais sem associar a funcionários individuais.

---

## 📋 Checklist Mensal

### **1. Cadastrar Funcionários (se ainda não cadastrados)**
```
[ ] Verificar se todos os funcionários estão cadastrados
[ ] Completar dados faltantes (CPF, departamento, contas)
[ ] Configurar centro de custo e contas contábeis
[ ] Validar status (Ativo/Inativo)
```

### **2. Receber Informações da Contabilidade**
```
[ ] Solicitar planilha DETALHADA por funcionário
[ ] Conferir valores de cada funcionário
[ ] Validar tipos de lançamento (salários, encargos, benefícios)
[ ] Confirmar competência (mês/ano)
```

### **3. Lançar por Funcionário**
```
[ ] Acessar RH → Lançamentos de Folha
[ ] Para cada funcionário:
    [ ] Criar novo lançamento vinculado ao funcionário
    [ ] Lançar salário
    [ ] Lançar encargos
    [ ] Lançar benefícios (se houver)
    [ ] Lançar descontos
    [ ] Salvar
[ ] Repetir para TODOS os funcionários
```

### **4. Conferir**
```
[ ] Gerar DRE do período
[ ] Verificar totalização por departamento
[ ] Comparar com total geral da contabilidade
[ ] Validar alocação por centro de custo
```

---

## 🔄 Fluxo de Lançamento

### **Para Cada Funcionário:**

1. **Acessar Lançamentos:**
   - Menu: RH → Lançamentos de Folha → Novo

2. **Vincular Funcionário:**
   - **Selecionar funcionário** (campo obrigatório)
   - Competência: MM/AAAA

3. **Lançar Valores:**
   - Salário base
   - Horas extras / Comissões
   - Encargos patronais (INSS, FGTS)
   - Benefícios
   - Descontos

4. **Salvar**

5. **Próximo Funcionário:**
   - Repetir passos 1-4

---

## 📊 Exemplo Rápido

### Planilha da Contabilidade (Março/2024):

```
FUNCIONÁRIO: João Silva (Mat. 001)
─────────────────────────────────
Salário: R$ 5.000,00
INSS Patronal: R$ 1.000,00
FGTS: R$ 400,00

FUNCIONÁRIO: Maria Santos (Mat. 002)
─────────────────────────────────
Salário: R$ 3.500,00
Comissões: R$ 1.200,00
INSS Patronal: R$ 940,00
FGTS: R$ 376,00

FUNCIONÁRIO: Pedro Costa (Mat. 003)
─────────────────────────────────
Salário: R$ 4.000,00
INSS Patronal: R$ 800,00
FGTS: R$ 320,00
```

### Lançamentos no Sol.NET:

**Lançamento 1 - João Silva:**
```
Funcionário: João Silva (selecionado)
Competência: 03/2024

Salário: R$ 5.000,00
D - 6.2.01 Salários
C - 2.1.2.01 Salários a Pagar

INSS: R$ 1.000,00
D - 6.2.02 Encargos
C - 2.1.2.02 Encargos a Recolher

FGTS: R$ 400,00
D - 6.2.02 Encargos
C - 2.1.2.03 FGTS a Recolher
```

**Lançamento 2 - Maria Santos:**
```
Funcionário: Maria Santos (selecionado)
Competência: 03/2024

Salário: R$ 3.500,00
Comissões: R$ 1.200,00
INSS: R$ 940,00
FGTS: R$ 376,00
```

**Lançamento 3 - Pedro Costa:**
```
Funcionário: Pedro Costa (selecionado)
Competência: 03/2024

Salário: R$ 4.000,00
INSS: R$ 800,00
FGTS: R$ 320,00
```

**Total no DRE:** Soma automática dos 3 funcionários

---

## 💡 Tipos de Lançamento por Funcionário

| Tipo | Vinculação | Exemplo |
|------|-----------|---------|
| Salários | Obrigatória ao funcionário | João Silva: R$ 5.000 |
| Encargos | Obrigatória ao funcionário | João Silva: R$ 1.000 |
| Benefícios | Obrigatória ao funcionário | João Silva: R$ 300 |
| Provisões | Obrigatória ao funcionário | João Silva: R$ 416,67 |

---

## ⚠️ Problemas Comuns

### **Não consigo salvar o lançamento**
**Causa:** Funcionário não selecionado  
**Solução:** Selecione o funcionário antes de salvar (campo obrigatório)

### **Funcionário não aparece na lista**
**Causa:** Funcionário não cadastrado ou inativo  
**Solução:** Cadastre o funcionário ou ative-o em RH → Cadastros → Funcionários

### **Valores aparecem no departamento errado**
**Causa:** Centro de custo incorreto no cadastro do funcionário  
**Solução:** Edite o cadastro do funcionário e corrija o centro de custo

### **Total diferente da contabilidade**
**Causa:** Faltou lançar algum funcionário  
**Solução:** Compare lista de funcionários lançados com planilha da contabilidade

### **Contabilidade só fornece valores totais**
**Causa:** Falta de comunicação sobre necessidade de detalhamento  
**Solução:** Solicite planilha detalhada por funcionário - é essencial para o Sol.NET

---

## 🎯 Dicas Importantes

### **1. Cadastre TODOS os Funcionários Primeiro**
Antes de começar os lançamentos, certifique-se que todos os funcionários da folha estão cadastrados.

### **2. Configure Contas no Cadastro**
Vincule as contas contábeis no cadastro do funcionário. Isso agiliza os lançamentos.

### **3. Organize por Departamento**
Ao lançar, processe primeiro todos de um departamento, depois outro. Facilita a conferência.

### **4. Padronize Descrições**
Use sempre as mesmas descrições:
- "Salário Base"
- "INSS Patronal"
- "FGTS"
- "Comissões"

### **5. Confira Funcionário por Funcionário**
Antes de passar para o próximo, confira se todos os valores do funcionário foram lançados.

---

## 📞 Precisa de Ajuda?

**Não consigo cadastrar funcionário:**  
→ Consulte [Documentação Completa - Cadastro de Funcionários](Documentacao Folha de Pagamento.md#-cadastro-de-funcionários-pessoa-rh)

**Dúvidas sobre vinculação:**  
→ Consulte [FAQ](FAQ.md)

**Contabilidade não fornece dados por funcionário:**  
→ Explique que o Sol.NET exige vinculação individual

---

**📅 Última atualização**: Janeiro de 2025  
**🎯 Lembre-se: Cada lançamento = Um funcionário específico**

*Para informações detalhadas, consulte a [Documentação Completa](Documentacao Folha de Pagamento.md).*
