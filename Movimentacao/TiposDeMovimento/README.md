---
title: "Índice: Tipos de Movimento — Movimentação Sol.NET"
permalink: /Movimentacao/TiposDeMovimento/
---

# 📚 Cadastro de Tipos de Movimento — Sol.NET

O **Tipo de Movimento** é a **identidade operacional** de cada lançamento no Sol.NET. Ele responde, em um único cadastro, a perguntas que todo movimento precisa carregar: *é venda ou compra?*, *sai ou entra no estoque?*, *é nota fiscal própria ou de terceiro?*, *qual CFOP, qual modelo de documento, qual série?*, *gera financeiro?*, *atualiza custo?*, *é mobile, ordem de serviço?*, *é exclusivo da aplicação PDV?*. Tudo o que diferencia uma venda de balcão de uma devolução, ou uma compra à vista de uma compra parcelada, está aqui.

Cada movimento operacional (em `Movimentos de Compras` código `201`, `Movimentos de Vendas` código `202`, `Outros Movimentos` código `203`, e também as ações disparadas por `Pedido de Compra` código `64`, `Produção de Produtos` código `144` e `Ajuste de Estoque` código `79`) aponta para **um** Tipo de Movimento — e é dele que o Sol.NET extrai todas as regras: quais Tabelas de Preço aceitar, qual `Transação de Estoque` aplicar, qual `Tipo de Documento Padrão` usar no financeiro, qual layout fiscal emitir, quais campos exigir, em qual `Local de Estoque` operar, com qual `Portador` quitar.

Por concentrar todas essas regras, é a **tela de configuração mais densa do módulo Movimentação** — com 12 abas no formulário, dezenas de sub-abas e mais de 50 validações ao salvar.

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Tipos de Movimento` requerem permissão de acesso de suporte. Toda criação, edição ou inativação deve ser feita pela equipe de suporte Hetosoft, **não** pelo usuário final. Mudanças aqui se propagam para todos os movimentos lançados a partir do momento da alteração — não há "preview" e mudanças em produção exigem cautela e acordo prévio com o cliente.

---

## 📄 Documentos desta seção

- [Documentação](documentacao_tipos_de_movimento.md) — referência completa: como acessar, detalhe de cada uma das 12 abas e suas sub-abas, exclusão, clonagem, exemplos práticos de criação dos tipos mais comuns, telas relacionadas, limites.
- [FAQ](faq.md) — perguntas frequentes + **tabela completa de validações** (50+ mensagens reais com a aba/sub-aba onde resolver cada uma). Use como referência de troubleshooting quando uma gravação for recusada.

---

## 🧭 Mapa rápido das 12 abas do formulário

| Aba | Conteúdo |
|------|----------|
| **Dados Cadastrais** | Identificação básica: descrição, código, conta contábil, comportamento (Entrada × Saída × Outros), tipo do movimento. |
| **Cabeçalho** | Sub-abas: Características, Origem/Destino, Datas, Funcionários, **Fiscal** (Natureza Op., Documento Fiscal, Fiscal Extra, Série), Serviço, Campos Livres, Mobile. |
| **Valores** | Regras de cálculo dos valores principais e dos valores de serviços. |
| **Itens** | Sub-abas: Principal, Extras, **Tabela de Preço**, Tabela de Preço por Empresa, **Estoque** (Local + Transação), Quantidade (com `Atualizar Custo Automático`), Comissão, Pessoa. |
| **Financeiro** | Sub-abas: Financeiro 1, Financeiro 2, Portador. Gera ou não conta a pagar/receber e define Plano de Contas, Centro de Custo, Tipo de Documento, Condição de Pagamento. |
| **Finalizar** | Comportamento na finalização do movimento, incluindo sub-fluxo de mudança automática para outro tipo. |
| **Mudar** | Configura uma mudança automática deste tipo para outro durante o ciclo (orçamento → pedido → venda). |
| **Agrupar** | Regras de agrupamento de movimentos (juntar vários pedidos em uma única nota). |
| **Relatórios** | Modelos de relatório, DANFE e etiquetas promocionais vinculados ao tipo. |
| **Campos Complementares** | Campos extras específicos a este tipo — Movimento, Produtos, Serviços. |
| **Outras Operações** | Flags variados: PDV, Mobile, OS × OS Requisição, Devolução, Crédito Pessoa, Quitar Crédito Automaticamente, comportamentos por empresa-destino. |
| **Agrotóxico** | Configurações específicas para tipos que movimentam produtos agrotóxicos (módulo Agronômico). |

> 💡 **Como ler a tela.** Quem está vendo um Tipo de Movimento pela primeira vez ganha tempo nesta ordem: **Dados Cadastrais** (o que é o tipo) → **Cabeçalho → Características** (compra/venda, próprio/terceiro, fiscal) → **Itens → Estoque** (Local + Transação) → **Financeiro** (gera conta?) → **Outras Operações** (PDV, mobile, devolução). As outras abas são afinações.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de Suporte / Consultores de Implantação Sol.NET
