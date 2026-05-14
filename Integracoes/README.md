---
title: "Índice: Integrações Sol.NET"
permalink: /Integracoes/
---
# 🔌 Índice: Integrações Sol.NET

Aqui ficam os documentos das **integrações** entre o Sol.NET e plataformas externas — sistemas de pedidos, marketplaces, gateways e demais canais que se conectam ao ERP para trocar pedidos, produtos, preços ou status.

Cada integração tem sua própria pasta com os documentos no padrão do portal: **Documentação**, **Guia Rápido** e **FAQ**.

---

## 📋 Integrações Disponíveis

### 🍔 **[iFood — Pedidos](iFood/README.md)**
Captura automática de pedidos do iFood, separação no balcão e geração do movimento de venda no Sol.NET.

- Configuração na aba `iFood` do `Cadastro de Empresas` (código `1`)
- Captura em background pelo `Sol.NET Monitor de Integração`
- Operação no `Monitor de Pedidos iFood` (código `151`): Aceitar → Iniciar Preparação → Pronto p/ Retirada → Finalizar Separação
- Recusa com motivo vindo da API do iFood
- Ajuste de quantidade e exclusão de item por ruptura, com sincronização para o iFood
- Vínculo manual de produto quando o código externo do iFood não bate com o `Cadastro de Produtos`
- Tratamento de cancelamento e disputa originados do próprio iFood

---

## 🎯 Por onde começar

### **🆕 Preparando uma empresa para receber pedidos iFood**
1. Confirme com a Hetosoft que a licença **SAC iFood** está ativa para a empresa
2. Configure a aba `iFood` em `Cadastro de Empresas` (código `1`) — veja a [Documentação de Pedidos iFood](iFood/documentacao_pedidos_ifood.md)
3. Garanta que o `Sol.NET Monitor de Integração` esteja em execução no servidor
4. Treine o atendente no `Monitor de Pedidos iFood` (código `151`) usando o [Guia Rápido](iFood/guia_rapido.md)

### **⚡ Operando o fluxo do dia a dia**
1. Use o [Guia Rápido — Pedidos iFood](iFood/guia_rapido.md) como cartão de referência
2. Consulte o [FAQ — Pedidos iFood](iFood/faq.md) quando algo travar

---

**📅 Última atualização**: Maio de 2026  
**📦 Versão**: 1.0  
**🎯 Público-alvo**: Usuários do Sol.NET e atendentes de balcão
