# 📄 Guia Rápido — Manifestação do Destinatário - Sol.NET

## 🎯 Visão Geral

Cartão de referência para a rotina diária de manifestação de NF-e e CT-e na tela `Manifestação do Destinatário` (código **`401`** na pesquisa F1). Use junto com a [documentação completa](documentacao_manifestacao_destinatario.md) para entender cada conceito a fundo.

> 🤖 **Download é automático**: a tela apenas **lista** as notas. Quem baixa da SEFAZ é o aplicativo **Sol.NET MonitorNFCe** (background, ciclo padrão **~1 hora**). Se a nota recente não está na lista, aguarde o próximo ciclo. **Não use** os botões `NF-e`/`CT-e` à esquerda da faixa — estão descontinuados.

---

## ⚡ Os quatro botões de manifestação

| Botão | Código | Quando usar |
|-------|--------|-------------|
| `Confirmar(1)` | 1 | A operação aconteceu de verdade — mercadoria recebida, serviço prestado |
| `Ciência(4)` | 4 | Tomei conhecimento, mas ainda não validei — passo inicial mais comum |
| `Descon.(2)` | 2 | Não reconheço essa nota — possível erro ou fraude |
| `Não Real.(3)` | 3 | Conheço, mas a operação não se concretizou (entrega recusada, contrato cancelado) |

> Manifestação enviada à SEFAZ **não pode ser cancelada**. Confirme antes de clicar em lote.

---

## ✅ Checklist — Rotina diária

- [ ] Abrir a tela: **F1 → `401` → Enter**
- [ ] Selecionar a `Descrição da Loja` correta
- [ ] Confirmar `Modelo = NF-e` (ou `CT-e`)
- [ ] Filtrar `Situação da Manifestação = Sem manifestação` e clicar em **`Buscar`**
- [ ] Selecionar tudo (botão direito → `Selecionar Todos`)
- [ ] Clicar em **`Ciência(4)`** para liberar o XML
- [ ] Conferir cada nota: confirmar, desconhecer ou marcar não realizada
- [ ] Verificar coluna `M-Número NF-e` para identificar notas confirmadas que ainda não foram lançadas
- [ ] Para lançar uma entrada a partir do XML, selecione a nota e clique no botão **`NF-e`** (ou **`CT-e`**) localizado **entre `Zerar NSU` e `Confirmar`**

---

## 🔍 Filtros — combinações úteis

| Objetivo | Filtros |
|----------|---------|
| Notas pendentes do dia | `Sit. Manifestação = Sem manifestação` + `Data Emissão` = hoje |
| Pendências do mês | `Sit. Manifestação = Sem manifestação` + `Data Emissão` = mês corrente |
| Notas confirmadas sem entrada lançada | `Sit. Manifestação = Confirmada` + olhar coluna `M-Número NF-e` vazia |
| Caçar uma nota específica | `Campo a pesquisar = Chave de Acesso` + `Condição = Contém` + colar a chave |
| Tudo de um fornecedor | `Campo a pesquisar = Fornecedor` + `Condição = Contém` + nome |

---

## 📋 Valores da `Situação da Manifestação`

| Display | Código | Significado |
|---------|--------|-------------|
| (vazio) / Sem manifestação | 0 | Ainda não manifestada |
| Confirmada | 1 | Confirmação da Operação enviada |
| Ciência | 4 | Ciência da Emissão enviada |
| Desconhecida | 2 | Desconhecimento enviado |
| Operação Não Realizada | 3 | Não Realizada enviada |
| Fora do Prazo - Ciência | 96 | Passou do prazo de Ciência |
| Fora do Prazo | 97 | Passou do prazo geral |
| Já Negada | 98 | SEFAZ já tinha registro de desconhecimento |
| Já Manifestada | 99 | SEFAZ já tinha outra manifestação registrada |

---

## 📋 Valores da `Situação da NF-e`

| Display | Significado |
|---------|-------------|
| Autorizado | NF-e autorizada na SEFAZ — operação fiscal regular |
| Cancelada | NF-e cancelada pelo emitente dentro do prazo |
| Denegado | NF-e não autorizada (problema cadastral, geralmente IE) |
| Canc.Manual | Marcação **interna do Sol.NET** — não tem efeito na SEFAZ |

---

## 🖱️ Atalhos do botão direito (sobre o grid)

| Item do menu | Quando ajuda |
|--------------|--------------|
| `Copiar Chave de Acesso` | Para colar em e-mail, planilha ou portal externo |
| `Selecionar Todos` / `Desmarcar Todos` | Operação em lote |
| `Mostrar Só Selecionados` | Revisar antes de manifestar em lote |
| `Ir para Movimentação` | Abre a entrada já lançada da nota selecionada |
| `Ir para Movimentação Financeiro` | Abre a aba financeira do movimento vinculado |
| `Alterar Situação da NF-e (Cancelado Manual)` | Marcar manualmente como cancelada **só no Sol.NET** |
| `Desfazer Situação da NF-e (Autorizada)` | Reverte o cancelamento manual |

---

## 🛠️ Botões de consulta e manutenção

| Botão | Quando usar |
|-------|-------------|
| `Status` | Verificar situação atual de uma nota na SEFAZ (cancelamento posterior, divergência) |
| `(Web)` | Abrir a nota no portal da SEFAZ para conferência visual |
| `Parar` | Interromper manifestação em lote em andamento |
| `Zerar NSU NF-e` | Reseta o contador NSU da loja para que o Monitor reconsulte notas dos últimos 180 dias. **Risco SEFAZ** (suspensão de manifesto, multa) — só sob orientação direta. Não funciona para CT-e |
| `Relatórios` | Listagens detalhadas das manifestações realizadas |

## 🧩 Os dois pares `NF-e` / `CT-e`

A faixa tem **dois botões com o mesmo rótulo** `NF-e` (e idem para `CT-e`). Posição importa:

| Posição | Botões | Função |
|---------|--------|--------|
| **À esquerda** da faixa | `NF-e`, `CT-e` | **Descontinuados.** Antigos botões de download em massa. Exibem aviso "Função Automatizada" e bloqueiam. **Não usar.** |
| **Entre `Zerar NSU` e `Confirmar`** | `NF-e`, `CT-e` | **Iniciam a importação/lançamento** do documento selecionado como entrada na Movimentação |

---

## 🚨 Diagnóstico rápido

| Sintoma | Verificar primeiro |
|---------|-------------------|
| "A nota não aparece" | Loja correta? Filtros limpos? Nota emitida há menos de 1 hora? Sol.NET MonitorNFCe rodando no servidor? |
| "Monitor não está baixando" | MonitorNFCe aberto? Internet do servidor? Certificado digital válido? Empresa não está em suspensão de manifesto? |
| "Manifestei a nota errada" | Não dá pra reverter — manifestar a correta e orientar o cliente; histórico fica |
| "Não consigo lançar a entrada" | Conferir primeiro se a nota tem `Ciência(4)` ou `Confirmar(1)` — sem isso o XML não está liberado |
| "Diz `Já Manifestada` mas eu nunca manifestei" | Tentativa de re-manifestar a mesma nota, ou manifestação feita antes por outro sistema/instalação ou pelo portal SEFAZ. Manifestação é única por CNPJ na SEFAZ |
| "Fora do Prazo" | Aceita o registro local, mas não tem efeito legal na SEFAZ. Orientar cliente a falar com o contador |

---

## 💡 Boas práticas

- ✅ Conferir o CNPJ da loja **antes** de manifestar em lote
- ✅ Dar `Ciência(4)` em massa pela manhã, conferir manualmente ao longo do dia
- ✅ Usar `Mostrar Só Selecionados` para revisar antes de clicar no botão de manifestação
- ❌ **Não** clicar nos botões `NF-e`/`CT-e` à esquerda da faixa — descontinuados, podem causar suspensão SEFAZ
- ❌ **Não** clicar em `Zerar NSU` sem motivo concreto — risco SEFAZ
- ❌ **Não** confundir `Canc.Manual` com cancelamento real — é status interno

---

**Última atualização**: Maio de 2026  
**Versão**: 1.1  
**Público-alvo**: Equipe de suporte Sol.NET
