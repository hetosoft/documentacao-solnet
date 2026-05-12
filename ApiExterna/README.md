---
title: "Índice: Documentação Módulo API Externa - Sol.NET ERP"
permalink: /ApiExterna/
---
# 📡 Índice: Documentação Módulo API Externa - Sol.NET ERP

## 🎯 Sobre o módulo

A **API Externa** é uma modalidade de integração do Sol.NET que permite a parceiros consultarem dados do ERP (produtos, estoque, pessoas, movimentos, condições de pagamento, tabelas de preço, fretes, empresas) por meio de um serviço REST. Em uma fase seguinte, a API também aceitará envio de dados, como pedidos de venda e orçamentos.

Cada parceiro recebe uma **credencial** — composta por um `Client ID` e uma `Secret Key` — gerada pela equipe de suporte da Hetosoft no Sol.NET. Essa credencial é o que dá acesso à API e define quais contextos (Produtos, Estoque, Pessoas, etc.) e operações (consulta, inclusão futura) o parceiro pode usar, com controle adicional de IP autorizado, expiração e limite de requisições por minuto.

> 📡 **Arquitetura distribuída** — o serviço da API é instalado e mantido no ambiente de cada cliente do Sol.NET. **Não existe URL única da Hetosoft**: a URL final é definida pelo time técnico responsável pela instalação. O suporte gera a credencial pela tela do Sol.NET, mas a URL deve ser obtida com quem hospeda o serviço.

Todo acesso a telas é pela **pesquisa universal** — atalho **`F1`** — digitando o **código** ou parte do **nome** da tela.

---

## 🧭 Telas e documentos do módulo

| Tela | Código (`F1`) | Documento |
|------|:---:|------|
| [Cadastro de Acessos WebAPI Externa](documentacao_api_externa.md) | `150` | 🟢 disponível |

### Material de apoio

- 📘 [Documentação completa da API Externa](documentacao_api_externa.md) — visão geral, campos do cadastro, permissões, segurança, fluxo passo a passo
- ⚡ [Guia Rápido](guia_rapido.md) — checklist para gerar uma credencial durante o atendimento
- ❓ [FAQ / Problemas comuns](faq.md) — perguntas frequentes do suporte sobre a API Externa

---

## 📚 Documentação relacionada

- **[Movimentação — Documentação](../Movimentacao/documentacao_movimentacao.md)** — contexto sobre os dados de movimentos que a API consulta
- **[Financeiro — Cond. de Pagamento](../Financeiro/documentacao_condicoes_pagamento.md)** — contexto sobre as condições de pagamento consultadas pela API

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 1.0
**🎯 Público-alvo**: Equipe de suporte Hetosoft
