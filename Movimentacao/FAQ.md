---
title: "FAQ - Movimentação"
permalink: /Movimentacao/faq/
---
# ❓ FAQ: Sistema de Movimentação Sol.NET

## 🔧 Configuração e Tipos de Movimento

### **Q: Como criar um tipo de movimento que só gera documento fiscal, sem afetar estoque nem financeiro?**
**R:** Configure o tipo com:
- Transação de Estoque: "Sem Movimentação"
- Lançamento Financeiro: "Sem Lançamento"
- Documento Fiscal: "NF-e Emissão Própria"

**Uso:** Remessas para demonstração, empréstimos, etc.

---

### **Q: Por que algumas vendas baixam estoque e outras não?**
**R:** O comportamento depende da **configuração do Tipo de Movimento**, não da natureza da operação. Cada tipo pode ter configuração diferente:
- Tipo "Venda Normal": baixa estoque
- Tipo "Orçamento": não baixa estoque
- Tipo "Venda Futura": pode não baixar estoque até confirmação

---

### **Q: Como configurar vendas com entrega programada?**
**R:** Crie dois tipos complementares:
1. **"Venda com Entrega Futura"**:
   - Gera financeiro (Contas a Receber)
   - NÃO baixa estoque
   - Emite documento fiscal
2. **"Entrega de Mercadoria"**:
   - Baixa estoque
   - NÃO gera financeiro (já foi gerado)
   - Pode emitir documento de remessa

---

### **Q: É possível ter comportamentos diferentes para o mesmo cliente?**
**R:** Sim! O comportamento é definido pelo **Tipo de Movimento escolhido**:
- Cliente XYZ com tipo "Venda à Vista" → Vai para caixa
- Cliente XYZ com tipo "Venda a Prazo" → Gera título
- Cliente XYZ com tipo "Orçamento" → Não gera impactos

---

## 💰 Controle Financeiro

### **Q: Por que não foram gerados títulos no Contas a Receber?**
**R:** Verifique se o Tipo de Movimento está configurado com:
- Lançamento Financeiro: "Contas a Receber" (para vendas)
- Condição de Pagamento definida
- Portador selecionado
- Cliente com dados financeiros completos

---

### **Q: Como configurar venda à vista sem gerar títulos?**
**R:** Use Lançamento Financeiro: "Caixa Direto"
- O valor vai direto para o caixa/fluxo de caixa
- Não passa pelo Contas a Receber
- Ideal para vendas à vista, cartão, PIX

---

### **Q: Posso ter vendas que geram financeiro mas não baixam estoque?**
**R:** Sim! Configure:
- Transação Estoque: "Sem Movimentação"
- Lançamento Financeiro: "Contas a Receber"
- **Uso:** Vendas de produtos sob encomenda, serviços com material do cliente

---

### **Q: Como funciona o F8 (Quitar Movimento)?**
**R:** F8 baixa automaticamente os títulos gerados pelo movimento:
- Localiza títulos vinculados ao movimento
- Permite informar data e forma de pagamento
- Atualiza status para "Quitado"
- Movimenta caixa/banco conforme configurado

---

## 📦 Controle de Estoque

### **Q: Movimento finalizado não baixou estoque. Por quê?**
**R:** Possíveis causas:
1. Tipo configurado com "Sem Movimentação de Estoque"
2. Produto sem controle de estoque ativo
3. Local de estoque não informado
4. Erro na finalização (verificar status)

---

### **Q: Como permitir estoque negativo em casos específicos?**
**R:** Na configuração do Tipo de Movimento:
- Desabilitar "Validar Estoque Negativo"
- **Uso:** Produtos sob encomenda, vendas especiais

---

### **Q: Posso transferir produtos entre filiais?**
**R:** Sim! Crie tipos específicos:
1. **"Transferência - Saída"**: Baixa estoque da origem
2. **"Transferência - Entrada"**: Aumenta estoque do destino
3. Vincule os movimentos através de transformação (F7)

---

### **Q: Como fazer ajustes de estoque?**
**R:** Use tipos específicos:
- **"Entrada por Ajuste"**: Para aumentar estoque
- **"Saída por Ajuste"**: Para diminuir estoque
- Configure sem impacto financeiro
- Documente o motivo do ajuste

---

## 🧾 Documentos Fiscais

### **Q: Movimento finalizado mas documento fiscal não foi emitido. Por quê?**
**R:** Verifique:
1. Tipo configurado para "Emissão Própria"
2. Certificado digital válido e instalado
3. Conexão com internet (SEFAZ)
4. Série e numeração configuradas
5. Produto com NCM cadastrado

---

### **Q: Posso emitir NFC-e para algumas vendas e Cupom Fiscal para outras?**
**R:** Sim! Configure tipos diferentes:
- Tipo "Venda NFC-e": Modelo "NFC-e"
- Tipo "Venda Cupom": Modelo "Cupom Fiscal"
- Use o tipo adequado para cada situação

---

### **Q: Como configurar remessa sem venda?**
**R:** Configure tipo com:
- Transação Estoque: "Transferência" ou "Sem Movimentação"
- Lançamento Financeiro: "Sem Lançamento"
- Documento Fiscal: "NF-e Remessa"
- **CFOP** adequado para remessa

---

## 🔄 Workflows e Transformações

### **Q: Como converter orçamento aprovado em venda?**
**R:** Use F7 (Transformar Movimento):
1. Abra o orçamento
2. Pressione F7
3. Selecione tipo de destino (ex: "Venda")
4. Confirme a transformação
5. Finalize o novo movimento (F6)

---

### **Q: Posso transformar qualquer tipo de movimento?**
**R:** Depende da configuração. No cadastro do tipo origem, configure:
- Quais tipos são permitidos como destino
- Se permite transformação múltipla
- Se bloqueia o movimento origem

---

### **Q: Como funciona a transformação parcial?**
**R:** Durante a transformação (F7):
- Selecione apenas os itens desejados
- O movimento origem mantém itens não transformados
- Útil para entregas parciais, vendas fracionadas

---

## 🚨 Problemas e Soluções

### **Q: Erro "Movimento não pode ser finalizado"**
**R:** Causes mais comuns:
1. Campos obrigatórios não preenchidos
2. Produtos sem NCM (documentos fiscais)
3. Estoque insuficiente (se validação ativa)
4. Cliente sem dados completos
5. Condição de pagamento não definida

**Solução:** Revisar todas as abas e completar informações necessárias.

---

### **Q: Movimento "perdido" ou com status incorreto**
**R:** Possíveis situações:
- **Status "Aberto"**: Movimento em edição, não processado
- **Status "Finalizado"**: Processado corretamente
- **Status "Cancelado"**: Anulado, impactos revertidos
- **Status "Vinculado"**: Transformado em outro movimento

---

### **Q: Como cancelar movimento já finalizado?**
**R:** Depende dos impactos gerados:
1. **Sem títulos em aberto**: Pode cancelar direto
2. **Com títulos em aberto**: Cancelar títulos primeiro
3. **Documento fiscal emitido**: Cancelar/inutilizar documento
4. **Estoque movimentado**: Sistema reverte automaticamente

---

### **Q: Duplicação de numeração fiscal**
**R:** Soluções:
1. Verificar configuração de séries
2. Conferir numeração automática/manual
3. Validar controle de empresas/filiais
4. Reinicializar contador se necessário

---

## 🎯 Cenários Específicos

### **Q: Como trabalhar com consignação?**
**R:** Use sequência de tipos:
1. **"Remessa Consignação"**: Transfere produtos
2. **"Venda Consignação"**: Confirma vendas
3. **"Retorno Consignação"**: Reverte não vendidos

---

### **Q: Como configurar vendas com desconto promocional automático?**
**R:** Configure no tipo de movimento:
- Regras de desconto por quantidade/valor
- Tabelas de preço promocionais
- Condições de pagamento especiais

---

### **Q: Movimento para devolução de vendas**
**R:** Configure tipo específico:
- Transação Estoque: "Entrada de Estoque"
- Lançamento Financeiro: "Contas a Pagar" (ou estorno)
- Documento Fiscal: "NF-e Devolução"
- Vincule ao movimento original

---

### **Q: Como usar diferentes comportamentos por filial?**
**R:** Configure:
- Tipos específicos por empresa/filial
- Controle de acesso por usuário/empresa
- Parâmetros diferentes por local
- Numeração fiscal independente

---

## 📊 Controle e Monitoramento

### **Q: Como identificar movimentos com problemas?**
**R:** Use relatórios de controle:
- Movimentos não finalizados (status "Aberto")
- Documentos fiscais rejeitados
- Títulos não gerados
- Divergências de estoque

---

### **Q: Como rastrear alterações em movimentos?**
**R:** O sistema mantém:
- Histórico completo de alterações
- Usuário responsável por cada ação
- Data/hora de cada modificação
- Log de erros e correções

---

### **Q: Relatórios para análise de vendas**
**R:** Disponíveis:
- Vendas por período/vendedor
- Produtos mais vendidos
- Margem de lucro por movimento
- Performance por tipo de movimento

---

## 🚀 Dicas de Produtividade

### **Q: Como acelerar o cadastro de movimentos recorrentes?**
**R:** Estratégias:
1. Configure tipos específicos com padrões
2. Use templates de itens/serviços
3. Configure clientes com dados completos
4. Utilize transformações (F7) sempre que possível

---

### **Q: Como treinar equipe para usar eficientemente?**
**R:** Foque em:
1. **Atalhos principais**: F4, F5, F6, F7, F8
2. **Tipos mais usados**: Configure bem os mais recorrentes
3. **Validações**: Sempre conferir antes do F6
4. **Padrões**: Crie rotinas consistentes

---

### **Q: Como evitar erros operacionais?**
**R:** Boas práticas:
1. Configure validações nos tipos
2. Use nomenclaturas claras
3. Treine operadores adequadamente
4. Monitore relatórios de inconsistências
5. Realize conciliações periódicas

---

*FAQ atualizada em: Dezembro de 2024*  
*Próxima atualização: Março de 2025*