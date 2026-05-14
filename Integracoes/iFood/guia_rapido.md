# 📄 Guia Rápido: Pedidos iFood - Sol.NET

## 🎯 Visão Geral

Cartão de operação do atendente no `Monitor de Pedidos iFood` (código `151`). Tenha à mão durante o turno.

> **F1 → `151` → Enter** abre o monitor.

---

## ⚡ Antes de começar o turno

- [ ] `Sol.NET Monitor de Integração` está em execução no servidor
- [ ] Empresa está com `Merchant ID iFood` preenchido no `Cadastro de Empresas` (código `1`)
- [ ] Tipo de Movimento iFood está configurado na aba `iFood` do `Cadastro de Empresas`

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Empresas` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nesta tela.

Se algum item acima falhar, **pedidos não chegam**.

---

## 🎨 Significado das cores

### No grid de pedidos

| Cor da linha | Status | O que fazer |
|--------------|--------|-------------|
| 🟡 **Amarelo** | `Aguardando` | Aceitar ou Recusar |
| 🔵 **Azul** | `Em Preparação` | Separar; ajustar itens se necessário |
| ⚪ **Branco** | Outros (Confirmado, Pronto, Cancelado) | Conforme o status do painel de detalhe |

### No grid de itens

| Cor da linha | O que significa |
|--------------|-----------------|
| 🔴 **Vermelho** | Item **sem vínculo** com produto — precisa vincular OU excluir antes de finalizar |
| ⚪ **Cinza tachado** | Item **excluído por ruptura** — vai ser ignorado na finalização |

---

## 🔁 Fluxo do pedido (passo-a-passo)

### 1. 🟡 Pedido `Aguardando` (linha amarela)

- Seleciona o pedido no grid
- Confere itens (todos verdes/vinculados?), nome, observação
- ✅ **`Aceitar Pedido`** (verde) → sinaliza para o iFood que aceitou
- ❌ **`Recusar Pedido`** (vermelho) → abre tela de motivo (combo obrigatório + descrição opcional)

> Empresa com `Confirmação = Automático`? O pedido **já chega em `Em Preparação`** (linha azul) — pule os passos 1 e 2 e vá direto para o passo 3 (ajustes de itens) ou 4 (Pronto p/ Retirada / Finalizar).

### 2. ⚪ Pedido `Confirmado`

- ✅ **`Iniciar Preparação`** (âmbar) → avisa o iFood; pedido vira azul
- A partir daqui ficam habilitados os botões de ajustar itens

### 3. 🔵 Pedido `Em Preparação` (linha azul)

**Durante a separação**, se precisar:

- 🔗 **`Vincular Produto`** — para itens vermelhos, informa código/ID do produto no Sol.NET
- ⚖️ **`Ajustar Quantidade`** — informa a nova quantidade (>0). Sincroniza com o iFood.
- ❌ **`Excluir Item (Ruptura)`** — item some do pedido. Sincroniza com o iFood (cliente é reembolsado pelo item).

**Quando o pedido estiver pronto:**

- ✅ **`Pronto p/ Retirada`** (azul) → avisa o iFood. Cliente vê "Aguardando entregador" no app.

### 4. ✅ Pedido `Pronto p/ Retirada` (ou ainda `Em Preparação`)

- ✅ **`Finalizar Separação`** (azul) → cria o movimento de venda no Sol.NET

> ⚠️ Não permite finalizar se houver **item vermelho** (sem vínculo). Resolva o vínculo ou exclua o item.

---

## 🚫 Recusar pedido — passo a passo

1. Selecione o pedido amarelo
2. Clique em **`Recusar Pedido`**
3. Na tela `Recusar Pedido iFood`:
   - Escolha um motivo no combo **`Motivo *`** (obrigatório, lista vem da API do iFood)
   - Se quiser, preencha **`Descrição adicional`** (opcional)
   - Clique em **`Ok`**
4. O Sol.NET chama a API; em sucesso, o pedido vira `Cancelado`

> Se a API rejeitar (ex.: pedido já foi cancelado pelo cliente), o sistema avisa e nada é gravado. Atualize o grid e veja o novo status.

---

## 🔄 Forçar uma rodada de captura manual

Quando você fez um pedido teste e quer ver chegar agora:

1. Vá ao **`Sol.NET Monitor de Integração`** (a janela que fica rodando no servidor)
2. Clique com **botão direito** na área de log
3. Escolha **`eCommerce → Pedidos IFood`**
4. Volte ao `Monitor de Pedidos iFood` no Sol.NET e atualize com o botão **`Atualizar`**

---

## 📅 Filtrar por data

O `Monitor de Pedidos iFood` carrega o **dia atual** automaticamente. Para ver outros dias:

- Mude o campo **`Data:`** no topo da tela — o grid recarrega sozinho.

Útil para conferência fim de turno, auditoria fiscal ou revisão de cancelados.

---

## 🆘 Travou? Caminho rápido

| Sintoma | Caminho rápido |
|---------|----------------|
| Pedido não aparece | Monitor de integração está rodando? Filtro de data está hoje? |
| Botão Aceitar apagado | Pedido já está `Confirmado`. Próximo passo é `Iniciar Preparação`. |
| Item vermelho | `Vincular Produto` ou `Excluir Item (Ruptura)` |
| Bloqueou no finalizar | Tem item vermelho. Resolva todos antes. |
| Cliente cancelou no app | Não precisa fazer nada. Próxima rodada do monitor cancela movimento+parcela automaticamente. |
| Pedido em disputa | Acompanhar pelo painel do iFood; Sol.NET só registra. |

Para casos não cobertos aqui, veja o [FAQ](faq.md) ou a [Documentação completa](documentacao_pedidos_ifood.md).

---

**Última atualização**: Maio de 2026  
**Versão**: 1.0  
**Público-alvo**: Atendentes de balcão e usuários do Sol.NET
