# 📄 Guia Rápido — Manifestação do Destinatário - Sol.NET

## 🎯 Visão Geral

Cartão de referência para a rotina diária de manifestação de NF-e e CT-e na tela `Manifestação do Destinatário` (código **`401`** na pesquisa F1). Use junto com a [documentação completa](documentacao_manifestacao_destinatario.md) para entender cada conceito a fundo.

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
- [ ] Clicar em **`NF-e`** (ou **`CT-e`**) para baixar novas notas
- [ ] Filtrar `Situação da Manifestação = Sem manifestação`
- [ ] Selecionar tudo (botão direito → `Selecionar Todos`)
- [ ] Clicar em **`Ciência(4)`** para liberar o XML
- [ ] Conferir cada nota: confirmar, desconhecer ou marcar não realizada
- [ ] Verificar coluna `M-Número NF-e` para identificar notas confirmadas que ainda não foram lançadas

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

## 🛠️ Botões de manutenção

| Botão | Quando usar |
|-------|-------------|
| `Status` | Verificar situação atual de uma nota na SEFAZ (cancelamento posterior, divergência) |
| `(Web)` | Abrir a nota no portal da SEFAZ para conferência visual |
| `Parar` | Interromper download/manifestação em andamento que travou |
| `Zerar NSU NF-e` / `Zerar NSU CT-e` | Forçar a SEFAZ a reenviar **tudo desde o início**. **Pesado** — só sob orientação |
| `Relatórios` | Listagens detalhadas das manifestações realizadas |

---

## 🚨 Diagnóstico rápido

| Sintoma | Verificar primeiro |
|---------|-------------------|
| "A nota não aparece" | Loja correta? Filtros limpos? Clicou em `NF-e` para baixar? |
| "Travou no download" | Conexão de internet, certificado digital, clicar `Parar` e tentar de novo |
| "Manifestei a nota errada" | Não dá pra reverter — manifestar a correta e orientar o cliente; histórico fica |
| "Não consigo lançar a entrada" | Conferir primeiro se a nota tem `Ciência(4)` ou `Confirmar(1)` — sem isso o XML não está liberado |
| "Diz `Já Manifestada` mas eu nunca manifestei" | Tentativa de re-manifestar a mesma nota, ou manifestação feita antes por outro sistema/instalação ou pelo portal SEFAZ. Manifestação é única por CNPJ na SEFAZ |
| "Fora do Prazo" | Aceita o registro local, mas não tem efeito legal na SEFAZ. Orientar cliente a falar com o contador |

---

## 💡 Boas práticas

- ✅ Conferir o CNPJ da loja **antes** de manifestar em lote
- ✅ Dar `Ciência(4)` em massa pela manhã, conferir manualmente ao longo do dia
- ✅ Usar `Mostrar Só Selecionados` para revisar antes de clicar no botão de manifestação
- ❌ **Não** clicar em `Zerar NSU` sem motivo concreto — gera processamento enorme
- ❌ **Não** confundir `Canc.Manual` com cancelamento real — é status interno

---

**Última atualização**: Maio de 2026  
**Versão**: 1.0  
**Público-alvo**: Equipe de suporte Sol.NET
