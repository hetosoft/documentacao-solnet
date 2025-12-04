---
title: "Guia Rápido - Reforma Tributária Sol.NET"
permalink: /Financeiro/guia-rapido-reforma-tributaria/
---
# ⚡ Guia Rápido: Reforma Tributária - Sol.NET

## 🎯 Resumo para Usuários Sol.NET

### **O que muda no sistema?**
```
📊 Tributos: 5 → 2
   PIS + COFINS + IPI  →  CBS (Federal)
   ICMS + ISS          →  IBS (Estadual/Municipal)

📋 Cadastros: NCM obrigatório com classificação tributária

🧮 Cálculo: Automático CBS/IBS em Movimentação

💰 Crédito: Aproveitamento automático (crédito pleno)
```

### **Cronograma:**
- **2026**: Teste no Sol.NET (0,9% CBS + 0,1% IBS)
- **2027**: CBS substitui PIS/COFINS automaticamente
- **2029-2032**: Sistema calcula tributos antigos + novos
- **2033**: Só CBS + IBS

---

## ⚡ Workflows Rápidos Sol.NET

### **1. Configurar NCM (Fazer UMA VEZ)**

```
Menu → Cadastros → Fiscal → NCM (Ctrl+Alt+N)

Novo (F4):
1. Código NCM: [8 dígitos]
2. Descrição: [auto-preenche]
3. Classificação: Padrão / Reduzida / Zero
4. CBS%: [auto-preenche conforme classificação]
5. IBS%: [auto-preenche conforme classificação]
6. Salvar (F5)

✅ Vincular produtos:
   Cadastros → Produtos → Aba Fiscal → Campo NCM
```

---

### **2. Lançar Compra (Gera Crédito)**

```
Menu → Movimentação → Nova (F4)

Cabeçalho:
├─ Tipo: Compra
├─ Fornecedor: [F2]
├─ Data: [hoje]
└─ Continuar → Items (F9)

Item:
├─ Produto: [F2 buscar]
├─ Quantidade: [informar]
├─ Valor Unit: [informar]
└─ Sistema calcula CBS/IBS automaticamente

Finalizar (F6)
📊 Créditos registrados automaticamente
```

---

### **3. Lançar Venda (Usa Crédito)**

```
Menu → Movimentação → Nova (F4)

Cabeçalho:
├─ Tipo: Venda
├─ Cliente: [F2]
├─ UF Destino: [importante para IBS]
└─ Continuar → Items (F9)

Item:
├─ Produto: [F2]
├─ Quantidade: [informar]
├─ Valor Unit: [informar]
└─ Sistema:
    1. Calcula CBS/IBS
    2. Busca créditos automaticamente
    3. Mostra tributo líquido

Finalizar (F6) → Gerar NFe (F10)
📊 Créditos aproveitados automaticamente
```

---

### **4. Consultar Créditos Acumulados**

```
Menu → Fiscal → Controle de Créditos

Visualizar:
├─ Saldo CBS disponível
├─ Saldo IBS disponível
├─ Origem dos créditos (por NF)
└─ Compensações realizadas

Filtrar: Período / Tipo / Situação
Exportar: PDF / Excel
```

---

### **5. Apurar Período (Mensal)**

```
Menu → Fiscal → Apuração CBS/IBS

Competência: [mês/ano]

Sistema gera:
├─ Total Débitos (vendas)
├─ Total Créditos (compras)
├─ Saldo a Recolher
└─ Guias de pagamento

Gerar Guias (F10)
Imprimir / Enviar banco
```

---

## 📊 Tabela Rápida - Alíquotas Sol.NET

| Classificação | CBS | IBS | Total | Produtos |
|---------------|-----|-----|-------|----------|
| **Padrão** | 8,5% | 17,5% | 26% | Maioria |
| **Reduzida** | 5,4% | 10,5% | 15,9% | Cesta básica, saúde |
| **Zero** | 0% | 0% | 0% | Livros, exportação |

> 💡 Sistema usa classificação do NCM para aplicar alíquota correta

---

## 🧮 Cálculo no Sol.NET (Automático)

### **O que o sistema faz:**

**Entrada (Compra):**
```
Produto: R$ 100
Sistema calcula:
├─ CBS (8,5%): R$ 8,50 → CRÉDITO
├─ IBS (17,5%): R$ 17,50 → CRÉDITO
└─ Total crédito: R$ 26,00 (registrado)
```

**Saída (Venda):**
```
Produto: R$ 150
Sistema calcula:
├─ CBS (8,5%): R$ 12,75 → DÉBITO
├─ IBS (17,5%): R$ 26,25 → DÉBITO
├─ Total débito: R$ 39,00
│
Sistema compensa:
├─ Débito: R$ 39,00
├─ Crédito: R$ 26,00 (da compra)
└─ A recolher: R$ 13,00 (só sobre margem!)
```

**💡 Você não faz nada**: Sistema gerencia tudo automaticamente!

---

## ⌨️ Atalhos Sol.NET - Reforma Tributária

| Atalho | Função | Onde usar |
|--------|--------|-----------|
| **Ctrl+Alt+N** | Cadastro NCM | Cadastros → Fiscal |
| **F2** | Buscar produto/cliente | Em qualquer campo |
| **F4** | Novo registro | Movimentação, Cadastros |
| **F5** | Salvar | Qualquer tela de edição |
| **F6** | Finalizar movimento | Cabeçalho movimentação |
| **F9** | Editar items | Na movimentação |
| **F10** | Gerar NFe | Após finalizar movimento |
| **F12** | Consulta rápida | Vários contextos |

---

## 🎯 Classificações Tributárias - Produtos Comuns

### **Alíquota Reduzida (15,9% total):**
✅ Arroz, feijão, farinha, leite, pão, açúcar, sal  
✅ Medicamentos essenciais (lista Anvisa)  
✅ Fraldas, absorventes  
✅ Produtos agropecuários in natura  
✅ Serviços de saúde e educação  

### **Alíquota Zero (0%):**
✅ Transporte público coletivo  
✅ Livros, jornais, periódicos  
✅ Frutas e verduras in natura  
✅ Ovos  
✅ Exportações (todas)  

### **Alíquota Padrão (26%):**
✅ Demais produtos e serviços  
✅ Bebidas alcoólicas  
✅ Cosméticos e perfumaria  
✅ Eletrônicos  
✅ Vestuário  

---

## 🚨 Validações Importantes

### **Antes de Finalizar Movimento:**

**✅ Verificar:**
- [ ] Todos os items têm NCM configurado
- [ ] Alíquotas CBS/IBS estão corretas
- [ ] UF Destino preenchida (para IBS)
- [ ] Cliente/Fornecedor com dados completos

**❌ Sistema bloqueia se:**
- Item sem NCM (após 2027)
- Alíquota inválida para o NCM
- Dados obrigatórios faltando
- CST incompatível com operação

---

## 💡 Dicas Práticas

### **📌 Configuração Inicial:**
1. **Priorize cesta básica**: Configure primeiro produtos com alíquota reduzida (maior impacto)
2. **Use relatório**: `Fiscal → Validação NCM` lista produtos pendentes
3. **Copie NCM similar**: Use produto já configurado como modelo

### **📌 Operação Diária:**
1. **Deixe automático**: Não altere cálculos sem necessidade
2. **Monitore créditos**: Consulte semanalmente saldo disponível
3. **Documente ajustes**: Se alterar manualmente, anote o motivo

### **📌 Controle Mensal:**
1. **Apure dia 25**: Dá tempo de corrigir problemas
2. **Confira notas**: Todas as compras geraram crédito?
3. **Exporte relatório**: Envie para contador antes do fechamento

---

## 🔴 Problemas Comuns - Soluções Rápidas

### **❌ "Item sem NCM configurado"**
**Solução:**
```
1. Cadastros → Produtos → Buscar produto
2. Aba Fiscal → Campo NCM
3. Selecionar NCM (F2)
4. Salvar (F5)
```

---

### **❌ "Alíquota diferente da esperada"**
**Solução:**
```
1. Verificar classificação do NCM
2. Cadastros → Fiscal → NCM → Editar
3. Conferir campo "Classificação Tributária"
4. Ajustar se necessário
5. Salvar e refazer movimento
```

---

### **❌ "Créditos não aproveitados"**
**Solução:**
```
1. Fiscal → Controle de Créditos
2. Verificar se compras estão registradas
3. Conferir notas de entrada finalizadas
4. Se ok, reprocessar movimento:
   - Editar venda → Salvar novamente
5. Se persistir: Suporte Sol.NET
```

---

### **❌ "NFe rejeitada - tributos"**
**Solução:**
```
1. Conferir alíquotas CBS/IBS no item
2. Verificar CST configurado
3. Validar UF Destino no cabeçalho
4. Refazer NFe (F10)
5. Erro persiste: Ver log detalhado (F12)
```

---

## 📅 Checklist Mensal - Rotina Fiscal

### **🗓️ Até dia 5:**
- [ ] Lançar todas as compras do mês anterior
- [ ] Conferir se geraram créditos corretamente
- [ ] Validar notas fiscais de entrada

### **🗓️ Até dia 15:**
- [ ] Lançar todas as vendas do mês anterior
- [ ] Verificar aproveitamento de créditos
- [ ] Conferir documentos fiscais de saída

### **🗓️ Até dia 20:**
- [ ] Acessar `Fiscal → Apuração CBS/IBS`
- [ ] Gerar relatório do período
- [ ] Conferir saldos a recolher
- [ ] Gerar guias de pagamento

### **🗓️ Até dia 25:**
- [ ] Pagar guias CBS (Receita Federal)
- [ ] Pagar guias IBS (Comitê Gestor)
- [ ] Arquivar comprovantes

### **🗓️ Até dia 30:**
- [ ] Exportar relatórios para contabilidade
- [ ] Backup de dados fiscais
- [ ] Revisar pendências para próximo mês

---

## 🆘 Suporte Rápido

### **Chat no Sistema:**
```
Ícone de chat no sistema Sol.NET
Atendimento: Seg-Sex 8h-18h
Resposta média: 5 minutos
```

### **E-mail Fiscal:**
```
📧 suporte.fiscal@solnet.com.br
Anexar: Print do erro + Código do movimento
Resposta: Até 24h
```

### **Telefone Urgente:**
```
📞 Consulte portal do cliente
Ramal: Suporte Fiscal (opção 2)
Horário: Comercial
```

### **Documentação Completa:**
```
📚 Menu Sol.NET → Ajuda → Reforma Tributária
Ou acesse: docs.solnet.com.br/reforma
```

---

## 🎓 Treinamentos Disponíveis

### **Webinars Mensais:**
- 🗓️ Toda 3ª terça-feira do mês
- ⏰ 14h - 15h30
- 📋 Inscrição: Portal do cliente
- 💻 Online (Teams)

### **Vídeos Tutoriais:**
- ▶️ Configurar NCM (5min)
- ▶️ Lançar compra com crédito (8min)
- ▶️ Lançar venda usando crédito (10min)
- ▶️ Apurar período mensal (12min)
- ▶️ Resolver problemas comuns (15min)

### **Certificação:**
- 🏆 Curso completo: 4h (EAD)
- 🏆 Certificado Sol.NET
- 🏆 Gratuito para clientes

---

## 🔗 Links Úteis

### **Documentação Relacionada:**
- 📖 [Guia Completo Reforma](Documentacao Reforma Tributaria.md)
- ❓ [FAQ Detalhado](FAQ Reforma Tributaria.md)
- 📊 [Módulo Financeiro](README.md)
- 📦 [Movimentação](../Movimentacao/README.md)

### **Recursos Externos:**
- 🏛️ [Reforma Tributária (Gov)](https://reformatributaria.gov.br)
- 🏛️ [Comitê Gestor IBS](https://ibs.gov.br)
- 📚 [NCM - Tabela Completa](https://www.gov.br/receitafederal/ncm)

---

**📅 Última atualização**: Dezembro de 2024  
**📦 Versão**: 2.0 (Workflows Sol.NET)  
**🎯 Público-alvo**: Usuários operacionais Sol.NET  
**⏱️ Tempo de leitura**: ~15 minutos

---

> **⚡ Lembre-se**: Este é um guia rápido. Para informações detalhadas, consulte a [Documentação Completa](Documentacao Reforma Tributaria.md).

> **🚀 Sol.NET gerencia tudo automaticamente!** Você só precisa: configurar NCM uma vez, lançar movimentos normalmente, e consultar relatórios. O sistema cuida de cálculos, créditos e apuração.
