---
title: "Guia Rápido - Reforma Tributária"
permalink: /Financeiro/guia-rapido-reforma-tributaria/
---
# ⚡ Guia Rápido: Reforma Tributária - Sol.NET

## 🎯 Resumo Executivo

### **O que muda?**
```
5 TRIBUTOS        →        2 TRIBUTOS
PIS + COFINS + IPI  →  CBS (Federal)
ICMS + ISS          →  IBS (Estadual/Municipal)
```

### **Quando?**
- **2026**: Teste (0,9% CBS + 0,1% IBS)
- **2027**: CBS substitui PIS/COFINS
- **2029-2032**: Transição gradual ICMS/ISS → IBS
- **2033**: Só CBS + IBS

### **Principal benefício:**
✅ **CRÉDITO PLENO** - Desconto total de tributos pagos nas compras

---

## ⏱️ Checklist de Preparação

### **🔧 Preparação Sistemas (2025-2026)**
- [ ] Atualizar cadastro de produtos com NCM/NBS corretos
- [ ] Revisar plano de contas para novos tributos
- [ ] Testar cálculos com alíquotas estimadas
- [ ] Validar integrações fiscais (NFe, NFSe)
- [ ] Configurar CBS e IBS no Sol.NET (quando disponível)
- [ ] Ativar CBS/IBS de teste no sistema
- [ ] Gerar documentos fiscais no novo padrão
- [ ] Validar cálculos e relatórios
- [ ] Treinar usuários finais
- [ ] Reportar dúvidas ao suporte Sol.NET

### **🔄 Transição (2027-2032)**
- [ ] Migrar para CBS em 2027 (substituir PIS/COFINS)
- [ ] Acompanhar redução gradual ICMS/ISS
- [ ] Controlar créditos no período duplo
- [ ] Ajustar precificação conforme necessário
- [ ] Monitorar legislação complementar

---

## 📊 Tabela Rápida de Alíquotas (Estimadas)

| Categoria | CBS | IBS | Total | Exemplos |
|-----------|-----|-----|-------|----------|
| **Padrão** | 8,5%-9,5% | 17,5%-18,5% | ~26,5%-27,5% | Maioria produtos/serviços |
| **Reduzida (60%)** | ~5,1% | ~10,5% | ~15,6%-16,8% | Cesta básica, saúde, educação |
| **Zero** | 0% | 0% | 0% | Transporte público, livros |
| **Exportação** | 0% | 0% | 0% | Todos exportados |

> ⚠️ **Atenção**: Valores estimados. Alíquotas exatas serão definidas por lei complementar.

---

## 🧮 Cálculo Simplificado

### **Como calcular tributos na reforma:**

**Passo 1: Valor da operação**
```
Venda = R$ 1.000,00
```

**Passo 2: Aplicar alíquotas**
```
CBS (8,5%) = R$ 85,00
IBS (17,5%) = R$ 175,00
Total tributos = R$ 260,00
```

**Passo 3: Deduzir créditos** (NOVIDADE!)
```
Compras com tributos: R$ 600,00
CBS pago na compra (8,5%) = R$ 51,00
IBS pago na compra (17,5%) = R$ 105,00
Total créditos = R$ 156,00
```

**Passo 4: Tributo líquido**
```
Tributo a pagar = R$ 260,00 - R$ 156,00 = R$ 104,00
Carga efetiva = 10,4% sobre a venda
(Tributo apenas sobre valor agregado de R$ 400!)
```

### **⚡ Fórmula Rápida:**
```
Tributo Líquido = (Valor Venda - Valor Compra) × (CBS% + IBS%)
```

---

## 🏪 Exemplos por Segmento

### **Comércio Varejista**
```
💡 Principal impacto: Crédito pleno em mercadorias

Antes (2024):
├─ Compra: R$ 70 + R$ 15 tributos (crédito limitado ~R$ 8)
├─ Venda: R$ 100 + R$ 21 tributos
└─ Custo tributário: ~R$ 13

Depois (2033):
├─ Compra: R$ 70 + R$ 18 tributos (CRÉDITO PLENO R$ 18)
├─ Venda: R$ 100 + R$ 26 tributos
└─ Custo tributário: R$ 8 (só sobre margem de R$ 30)

✅ Benefício: ~R$ 5 por operação
```

### **Indústria**
```
💡 Principal impacto: Crédito total insumos + fim IPI

Antes (2024):
├─ Matéria-prima: R$ 100 + tributos R$ 26 (crédito parcial)
├─ Produto final: R$ 300 + tributos R$ 78
└─ Custo: ~R$ 60

Depois (2033):
├─ Matéria-prima: R$ 100 + tributos R$ 26 (CRÉDITO R$ 26)
├─ Produto final: R$ 300 + tributos R$ 78
└─ Custo: R$ 52 (só sobre valor agregado)

✅ Benefício: ~R$ 8 + simplificação operacional
```

### **Prestação de Serviços**
```
💡 Principal impacto: Crédito sobre insumos (antes negado)

Antes (2024):
├─ Serviço: R$ 500
├─ ISS+PIS+COFINS: R$ 28
└─ Sem crédito de materiais/equipamentos

Depois (2033):
├─ Serviço: R$ 500
├─ CBS+IBS: R$ 39 (alíquota padrão)
├─ Créditos: ~R$ 8 (materiais, equipamentos)
└─ Líquido: R$ 31

⚠️ Leve aumento, mas com benefício de créditos
```

---

## 🚀 Atalhos e Dicas Sol.NET

### **⌨️ Atalhos Úteis**

| Função | Atalho | Quando usar |
|--------|--------|-------------|
| Simulador impacto | **F11** | Testar cenários reforma |
| Config. tributos | **Ctrl+T** | Ajustar CBS/IBS |
| Consulta NCM | **F2** | Validar classificação |
| Relatório créditos | **F9** | Acompanhar aproveitamento |
| Análise comparativa | **Shift+F11** | Antes × Depois reforma |

> 💡 **Nota**: Atalhos disponíveis em versões futuras do Sol.NET

### **📍 Menu Rápido**
```
Financeiro
  └─ Reforma Tributária
      ├─ Simulador de Impacto
      ├─ Configuração CBS/IBS
      ├─ Relatório de Créditos
      ├─ Análise Comparativa
      └─ Guia de Transição
```

---

## 🎯 Produtos com Alíquotas Especiais

### **Alíquota Reduzida (60% da padrão)**
✅ Arroz, feijão, farinha, leite, pão, açúcar (cesta básica)  
✅ Medicamentos essenciais (lista Anvisa)  
✅ Dispositivos médicos e acessibilidade  
✅ Serviços de saúde e educação  
✅ Produtos agropecuários selecionados  

### **Alíquota Zero**
✅ Transporte público coletivo  
✅ Livros, jornais, periódicos  
✅ Produtos hortifrutigranjeiros in natura  
✅ Ovos, leite natural  
✅ Medicamentos doenças graves (via Anvisa)  

### **Isenções**
✅ Exportações (todas)  
✅ Programa habitacional popular  
✅ Produtos de reciclagem/economia circular  

---

## ❓ Dúvidas Rápidas

**Q: Vou pagar mais impostos?**  
**R:** Não necessariamente. Depende do setor e aproveitamento de créditos. Use o simulador Sol.NET.

**Q: Simples Nacional acaba?**  
**R:** NÃO. Continua com CBS e IBS incluídos na guia única.

**Q: Quando preciso mudar meu sistema?**  
**R:** Sol.NET fará atualizações automáticas. Você só precisa validar cadastros de produtos (NCM/NBS).

**Q: Benefícios fiscais que tenho hoje continuam?**  
**R:** Gradualmente reduzidos até 2032. Extintos em 2033 (salvo exceções da reforma).

**Q: Como aproveitar créditos?**  
**R:** Automático no Sol.NET. Basta ter documentos fiscais corretos das compras.

---

## 🔴 Erros Comuns a Evitar

### ❌ **Não classificar produtos corretamente**
**Impacto**: Alíquota errada aplicada  
**Solução**: Revisar NCM/NBS de todos os produtos AGORA

### ❌ **Ignorar créditos disponíveis**
**Impacto**: Pagar mais tributos que o necessário  
**Solução**: Validar todas as notas de compra e aproveitamento

### ❌ **Não ajustar preços**
**Impacto**: Margem de lucro reduzida ou preços não competitivos  
**Solução**: Usar simulador Sol.NET para recalcular precificação

### ❌ **Achar que pode deixar "para depois"**
**Impacto**: Correria e erros na hora da implementação  
**Solução**: Preparar desde já, mesmo com transição só em 2026

### ❌ **Confiar em alíquotas estimadas para decisões finais**
**Impacto**: Planejamento impreciso  
**Solução**: Aguardar publicação oficial e ajustar quando confirmado

---

## 📞 Suporte Rápido

### **🆘 Em caso de dúvidas:**

**Chat Sol.NET**: Suporte online no sistema  
**E-mail**: reforma.tributaria@solnet.com.br  
**Telefone**: 0800-xxx-xxxx (ramal 2)  
**Documentação completa**: [Reforma Tributária - Guia Completo](Documentacao Reforma Tributaria.md)

### **📚 Materiais complementares:**
- [FAQ Detalhado](Documentacao Reforma Tributaria.md#-faq---perguntas-frequentes)
- [Exemplos Práticos](Documentacao Reforma Tributaria.md#-exemplos-práticos)
- [Cronograma Completo](Documentacao Reforma Tributaria.md#-cronograma-de-implementação)

---

## 📅 Marcos Importantes

| Data | Evento | Ação necessária |
|------|--------|-----------------|
| **2024-2025** | Preparação | Mapear produtos e simular |
| **2026** | Teste | Validar sistema e treinar |
| **Jan/2027** | CBS entra | Substituir PIS/COFINS |
| **Jan/2029** | IBS inicia | Começar transição ICMS/ISS |
| **Jan/2033** | Regime pleno | Operar só CBS+IBS |

---

## 💡 Dica de Ouro

> **A grande vantagem da reforma é o CRÉDITO PLENO!**  
> Quanto mais você compra para produzir/revender, mais crédito acumula.  
> Isso reduz drasticamente a carga tributária sobre sua margem.  
> 
> **Foque em**: Documentação perfeita de compras + Aproveitamento máximo de créditos

---

## 🎓 Próximos Passos

### **1. Entenda o básico** ✅
Você já está aqui! Continue com:

### **2. Leia a documentação completa** 📖
[Documentação Reforma Tributária](Documentacao Reforma Tributaria.md)

### **3. Simule seu cenário** 🧮
Use ferramentas Sol.NET quando disponíveis

### **4. Capacite sua equipe** 👥
Webinars e treinamentos Sol.NET

### **5. Acompanhe atualizações** 📡
Legislação em constante evolução

---

**📅 Última atualização**: Dezembro de 2024  
**📦 Versão**: 1.0 (Guia Rápido)  
**🎯 Público-alvo**: Usuários práticos Sol.NET  
**⏱️ Tempo de leitura**: ~10 minutos

---

> **🚀 Lembre-se**: A reforma tributária é uma **oportunidade** de simplificação e potencial economia. Com planejamento adequado e o Sol.NET ao seu lado, sua empresa estará pronta para aproveitar os benefícios!
