---
title: "Guia Rápido: Movimentação Sol.NET"
permalink: /Movimentacao/guia-rapido/
---
# 🚀 Guia Rápido: Movimentação Sol.NET

## ⌨️ Atalhos Essenciais

| Tecla | Ação | Quando Usar |
|-------|------|-------------|
| **F4** | Novo Movimento | Iniciar qualquer movimento |
| **F5** | Salvar Alterações | Salvar edição em andamento |
| **F6** | Finalizar | Processar movimento completo |
| **F7** | Transformar | Converter em outro tipo |
| **F8** | Quitar | Baixar títulos financeiros |

## 📋 Checklist: Novo Movimento

### ✅ Antes de Começar
- [ ] Definir o tipo de movimento correto
- [ ] Verificar empresa de origem
- [ ] Confirmar cliente/fornecedor
- [ ] Validar data de emissão

### ✅ Durante a Operação
- [ ] Adicionar todos os itens necessários
- [ ] Conferir preços e quantidades
- [ ] Aplicar descontos (se houver)
- [ ] Definir condição de pagamento
- [ ] Revisar totais

### ✅ Antes de Finalizar (F6)
- [ ] Conferir todos os dados
- [ ] Validar estoque (se aplicável)
- [ ] Verificar informações fiscais
- [ ] Confirmar forma de pagamento

## 💡 Exemplos Rápidos por Tipo

### 🛒 **Venda Tradicional**
```
F4 → Tipo: "Venda" → Cliente → Itens → F6
Resultado: ↓ Estoque + ↑ Contas Receber + 🧾 NFC-e
```

### 📄 **Orçamento**
```
F4 → Tipo: "Orçamento" → Cliente → Itens → F6
Resultado: 📊 Apenas registro (sem impactos)
```

### 💰 **Venda à Vista**
```
F4 → Tipo: "Venda à Vista" → Cliente → Itens → F6
Resultado: ↓ Estoque + 💰 Caixa + 🧾 NFC-e
```

### 🔄 **Transformar Orçamento em Venda**
```
Abrir Orçamento → F7 → Tipo: "Venda" → F6
Resultado: Novo movimento com impactos
```

## 🚨 Problemas Comuns - Soluções Rápidas

### ❌ "Não é possível finalizar o movimento"
**Causa**: Campo obrigatório em branco  
**Solução**: Verificar abas e preencher dados necessários

### ❌ "Estoque insuficiente"
**Causa**: Validação de estoque ativa  
**Solução**: Ajustar estoque ou desabilitar validação no tipo

### ❌ "Erro na emissão fiscal"
**Causa**: Certificado ou configuração  
**Solução**: Verificar certificado digital e conexão

### ❌ "Títulos não gerados"
**Causa**: Configuração financeira do tipo  
**Solução**: Revisar tipo de lançamento no cadastro do tipo

## 🎛️ Configuração Rápida: Tipo de Movimento

### Para **VENDA COM ESTOQUE E FINANCEIRO**:
- ✅ Transação Estoque: "Saída de Estoque"
- ✅ Lançamento Financeiro: "Contas a Receber"
- ✅ Documento Fiscal: "NFC-e Emissão Própria"

### Para **ORÇAMENTO** (sem impactos):
- ❌ Transação Estoque: "Sem Movimentação"
- ❌ Lançamento Financeiro: "Sem Lançamento"
- ❌ Documento Fiscal: "Não Fiscal"

### Para **VENDA À VISTA**:
- ✅ Transação Estoque: "Saída de Estoque"  
- ✅ Lançamento Financeiro: "Caixa Direto"
- ✅ Documento Fiscal: "NFC-e Emissão Própria"

## 🔍 Verificação Rápida de Impactos

### Após Finalizar, Verificar:
1. **Estoque**: Consultar saldo do produto
2. **Financeiro**: Verificar títulos gerados
3. **Fiscal**: Confirmar emissão do documento
4. **Status**: Movimento deve estar "Finalizado"

## 📞 Dica de Produtividade

> **Personalize os Tipos**: Crie tipos específicos para situações recorrentes (ex: "Venda Loja", "Venda Delivery", "Venda Atacado") com configurações pré-definidas para agilizar a operação.

## 🎯 Meta: Operação Eficiente

1. **Conheça os Atalhos**: Pratique F4, F5, F6, F7, F8
2. **Use o Tipo Certo**: Cada situação tem seu tipo ideal
3. **Valide Antes de F6**: Evita retrabalho
4. **Monitor os Resultados**: Confira impactos após finalizar

---
*Guia atualizado em: Dezembro de 2024*