---
title: "Guia Rápido - Reforma Tributária Sol.NET"
permalink: /Fiscal/guia_rapido_reforma_tributaria/
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

- Abra a pesquisa universal (F1) e acesse a tela de Cadastro de NCM
- Crie um novo registro:
```
1. Código NCM: [8 dígitos]
2. Descrição: [auto-preenche]
3. Classificação: Padrão / Reduzida / Zero
4. CBS%: [auto-preenche conforme classificação]
5. IBS%: [auto-preenche conforme classificação]
6. Salve pelo botão equivalente
```

✅ Vincular produtos: Abra a pesquisa universal (F1), acesse Cadastro de Produtos → aba Fiscal → campo NCM

---

### **2. Lançar Compra (Gera Crédito)**

- Abra a pesquisa universal (F1) e acesse a tela de Movimentação
```
Cabeçalho:
├─ Tipo: Compra
├─ Fornecedor: [buscar pelo nome]
├─ Data: [hoje]
└─ Prossiga para lançamento de itens

Item:
├─ Produto: [buscar pelo nome]
├─ Quantidade: [informar]
├─ Valor Unit: [informar]
└─ Sistema calcula CBS/IBS automaticamente

Finalize pelo botão equivalente
📊 Créditos registrados automaticamente
```

---

### **3. Lançar Venda (Usa Crédito)**

- Abra a pesquisa universal (F1) e acesse a tela de Movimentação
```
Cabeçalho:
├─ Tipo: Venda
├─ Cliente: [buscar pelo nome]
├─ UF Destino: [importante para IBS]
└─ Prossiga para lançamento de itens

Item:
├─ Produto: [buscar pelo nome]
├─ Quantidade: [informar]
├─ Valor Unit: [informar]
└─ Sistema:
    1. Calcula CBS/IBS
    2. Busca créditos automaticamente
    3. Mostra tributo líquido

Finalize pelo botão equivalente → Use a função de Gerar NFe disponível na tela
📊 Créditos aproveitados automaticamente
```

---

### **4. Consultar Créditos Acumulados**

- Abra a pesquisa universal (F1) e acesse a tela de Controle de Créditos CBS/IBS
```
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

- Abra a pesquisa universal (F1) e acesse a tela de Apuração CBS/IBS
```
Competência: [mês/ano]

Sistema gera:
├─ Total Débitos (vendas)
├─ Total Créditos (compras)
├─ Saldo a Recolher
└─ Guias de pagamento

Use a função de Gerar Guias disponível na tela
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

## ⌨️ Acesso às Telas - Reforma Tributária

Todas as telas do Sol.NET são acessadas pela **pesquisa universal** (F1). Digite o nome ou parte do nome da tela desejada para abri-la diretamente.

**Telas mais usadas no contexto da reforma:**
- Busque "NCM" para acessar o cadastro de NCM
- Busque "Movimentação" para lançar compras e vendas
- Busque "Apuração CBS" para apurar o período mensal
- Busque "Créditos" para consultar o controle de créditos tributários
- Busque "Validação NCM" para identificar produtos sem classificação fiscal
- Busque "Impacto Reforma" para acessar o relatório comparativo

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
2. **Use relatório**: Abra a pesquisa universal (F1) e acesse a tela de Validação NCM para listar produtos pendentes
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
1. Abra a pesquisa universal (F1) e acesse Cadastro de Produtos
2. Busque o produto pelo nome
3. Aba Fiscal → Campo NCM → selecione o NCM correto
4. Salve pelo botão equivalente
```

---

### **❌ "Alíquota diferente da esperada"**
**Solução:**
```
1. Abra a pesquisa universal (F1) e acesse o Cadastro de NCM
2. Localize o NCM e edite o registro
3. Confira o campo "Classificação Tributária"
4. Ajuste se necessário e salve pelo botão equivalente
5. Refaça o movimento
```

---

### **❌ "Créditos não aproveitados"**
**Solução:**
```
1. Abra a pesquisa universal (F1) e acesse Controle de Créditos
2. Verifique se as compras estão registradas
3. Confira as notas de entrada finalizadas
4. Se estiver correto, reprocesse o movimento:
   - Abra a venda e salve novamente pelo botão equivalente
5. Se persistir: Suporte Sol.NET
```

---

### **❌ "NFe rejeitada - tributos"**
**Solução:**
```
1. Confira as alíquotas CBS/IBS no item
2. Verifique o CST configurado
3. Valide a UF Destino no cabeçalho
4. Refaça a NFe pela função de emissão disponível na tela
5. Se o erro persistir: consulte o log detalhado via suporte Sol.NET
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
- [ ] Abra a pesquisa universal (F1) e acesse a tela de Apuração CBS/IBS
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
📚 Acesse: docs.solnet.com.br/reforma
Ou consulte a documentação disponível no portal do cliente
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
- 📖 [Guia Completo Reforma](documentacao_reforma_tributaria.md)
- ❓ [FAQ Detalhado](faq_reforma_tributaria.md)
- 📊 [Módulo Financeiro](../Financeiro/README.md)
- 📦 [Movimentação](../Movimentacao/README.md)

### **Recursos Externos:**
- 🏛️ [Reforma Tributária (Gov)](https://reformatributaria.gov.br)
- 🏛️ [Comitê Gestor IBS](https://ibs.gov.br)
- 📚 [NCM - Tabela Completa](https://www.gov.br/receitafederal/ncm)

---

**📅 Última atualização**: Abril de 2026  
**📦 Versão**: 2.1 (Workflows Sol.NET)  
**🎯 Público-alvo**: Usuários operacionais Sol.NET  
**⏱️ Tempo de leitura**: ~15 minutos

---

> **⚡ Lembre-se**: Este é um guia rápido. Para informações detalhadas, consulte a [Documentação Completa](documentacao_reforma_tributaria.md).

> **🚀 Sol.NET gerencia tudo automaticamente!** Você só precisa: configurar NCM uma vez, lançar movimentos normalmente, e consultar relatórios. O sistema cuida de cálculos, créditos e apuração.
