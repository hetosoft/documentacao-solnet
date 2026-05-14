# 📄 FAQ: Pedidos iFood - Sol.NET

## 🎯 Visão Geral

Perguntas que aparecem com mais frequência no atendimento da integração de pedidos iFood. Para o passo-a-passo de operação, veja o [Guia Rápido](guia_rapido.md); para a referência completa, veja a [Documentação](documentacao_pedidos_ifood.md).

---

## ⚙️ Configuração inicial

### ❓ Quais cadastros preciso fazer antes de começar a receber pedidos?

Quatro pré-requisitos:

1. **Licença SAC iFood** ativa na Hetosoft para a empresa
2. **Merchant ID iFood** preenchido na aba `iFood` do `Cadastro de Empresas` (código `1`) — esse ID vem do iFood
3. **Tipo de Movimento** configurado no `Cadastro de Tipos de Movimento` para representar a venda iFood, e selecionado na aba `iFood` do `Cadastro de Empresas`
4. **`Sol.NET Monitor de Integração`** em execução no servidor

Sem qualquer um deles, **pedidos não chegam**.

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Empresas` e no `Cadastro de Tipos de Movimento` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nessas telas.

### ❓ Qual a diferença entre Confirmação `Manual` e `Automático` na aba iFood?

- **`Manual`** — o atendente precisa clicar em **`Aceitar Pedido`** no monitor para que o Sol.NET sinalize ao iFood que a loja aceita. O pedido chega em status `Aguardando` (linha amarela), depois passa por `Confirmado` (Aceitar) e `Em Preparação` (Iniciar Preparação).
- **`Automático`** — assim que o Sol.NET captura o pedido pela API, ele **já confirma** no iFood automaticamente e marca o pedido como `Em Preparação` (linha azul) no monitor — pulando os botões Aceitar Pedido e Iniciar Preparação. O atendente entra direto na separação dos itens.

Os outros passos (Pronto p/ Retirada, Finalizar Separação, ajustes de itens) **continuam manuais** nos dois modos.

### ❓ Posso usar a integração iFood em várias empresas do mesmo Sol.NET?

Sim. Cada empresa configura seu próprio `Merchant ID iFood`, sua própria licença, seu próprio `Tipo de Movimento iFood` e seu próprio modo de `Confirmação`. O `Sol.NET Monitor de Integração` varre todas as empresas configuradas em cada rodada. No grid do `Monitor de Pedidos iFood` (código `151`), a coluna `Empresa` identifica de qual empresa é cada pedido.

### ❓ Preciso configurar uma forma de pagamento específica na aba iFood?

Não. A forma de pagamento da venda iFood vem do **`Tipo de Movimento`** configurado para a empresa — toda regra financeira (forma, condição, plano de contas) está definida lá. Use um tipo de movimento específico para iFood, com a forma adequada (ex.: "iFood — Crédito on-line"), e tudo se resolve automaticamente.

---

## 📥 Captura de pedidos

### ❓ Recebi um pedido pelo app, mas ele não aparece no Monitor de Pedidos. Por quê?

Verifique nessa ordem:

1. O `Sol.NET Monitor de Integração` está em execução? Sem ele, **nenhum pedido entra**.
2. O filtro `Data:` no topo do monitor está no dia certo?
3. A empresa que recebeu o pedido tem `Merchant ID iFood` preenchido?
4. A licença SAC iFood está ativa para essa empresa? Confirme com a Hetosoft.
5. **Force uma rodada manual**: no `Sol.NET Monitor de Integração`, clique direito na janela de log → `eCommerce → Pedidos IFood`.

### ❓ Como faço para forçar uma captura imediata sem esperar o próximo ciclo?

No `Sol.NET Monitor de Integração`, clique com o **botão direito** na área de log e escolha **`eCommerce → Pedidos IFood`**. O processo executa imediatamente para todas as empresas configuradas. Volte ao `Monitor de Pedidos iFood` no Sol.NET e clique em **`Atualizar`** para ver os novos pedidos.

### ❓ Se o Monitor de Integração ficar fora do ar, perco pedidos?

**Não.** Os pedidos continuam entrando no iFood normalmente; só não chegam ao Sol.NET enquanto o monitor de integração estiver parado. Quando o monitor voltar a rodar, ele puxa o acúmulo da API de uma vez. Se a pausa for longa (mais de algumas horas), pode haver atraso no aceite — converse com o cliente sobre alarme de monitoração do serviço.

### ❓ O pedido apareceu duas vezes no grid. É bug?

Não. A captura tem proteção contra duplicação por chave única (`Empresa + ID do Pedido`). Se você vê duas linhas, são dois pedidos diferentes do mesmo cliente. Confirme pelo `Código` (short code do iFood) na primeira coluna — ele é único por pedido.

---

## 🔁 Operação no monitor

### ❓ O botão `Aceitar Pedido` está apagado/cinza. Por quê?

`Aceitar Pedido` só fica disponível para pedidos em status **`Aguardando`** (linha amarela). Se o pedido já passou para `Confirmado` (porque a empresa está com `Confirmação = Automático` ou outro atendente já aceitou), o próximo passo é `Iniciar Preparação`.

### ❓ Não consigo finalizar a separação — a tela avisa que tem item sem vínculo.

Algum item está com linha **vermelha** no grid de itens. O Sol.NET não permite gerar o movimento com itens não vinculados (não saberia que produto colocar no movimento).

Resolva uma das duas formas:

- 🔗 **Vincular** o item com `Vincular Produto`, informando o `Código` ou `ID` do produto certo
- ❌ **Excluir** o item com `Excluir Item (Ruptura)` — o cliente é reembolsado pelo iFood

### ❓ Quando posso ajustar quantidade ou excluir um item?

Somente quando o pedido está em **`Em Preparação`** (linha azul). Antes disso (`Aguardando`, `Confirmado`) e depois (`Pronto p/ Retirada`, `Finalizado`) os botões de ajuste ficam desabilitados.

Por isso o passo `Iniciar Preparação` é importante: ele "destrava" os botões de manipulação de itens.

### ❓ Posso pular o `Pronto p/ Retirada` e ir direto para `Finalizar Separação`?

Sim. O Sol.NET aceita finalizar a partir de `Em Preparação`. Mas o cliente final no app **não vai ver** o status "Aguardando entregador" — o pedido vai sumir das atualizações dele direto. Use `Pronto p/ Retirada` sempre que possível, é uma melhor experiência para o cliente.

### ❓ Recusei o pedido errado. Como reverto?

**Não há como reverter pela tela.** A recusa é enviada à API do iFood imediatamente, e o cliente é notificado. Se foi engano, entre em contato com o cliente por outro canal (telefone, observação do pedido se houver) — o pedido não volta para o monitor. Para vender o item, o cliente precisa fazer um novo pedido no app.

---

## 👤 Cliente e movimento

### ❓ A venda saiu no nome de "Consumidor iFood". Como mudo para o nome real do cliente?

Pedidos sem CPF/CNPJ no app são lançados em **"Consumidor iFood"** para permitir que a venda aconteça. Se o cliente depois informar o documento, você pode alterar a pessoa do movimento na tela `Vendas` (código `202`) — desde que o movimento ainda esteja em estado editável e a permissão de alteração esteja liberada.

### ❓ O CPF vem do iFood, mas o cliente nunca tinha comprado aqui. O Sol.NET cria a pessoa?

Sim. Quando o pedido traz CPF (11 dígitos) ou CNPJ (14 dígitos) e não existe pessoa cadastrada com aquele documento, o Sol.NET cria automaticamente uma **pessoa mínima** com o nome e o documento que vieram do app. Demais campos (endereço, telefone, e-mail) ficam vazios e podem ser preenchidos depois no `Cadastro de Pessoas` (código `5`).

### ❓ Em que momento o estoque é baixado?

Depende do `Tipo de Movimento` configurado para iFood:

- Se o tipo **finaliza automaticamente** o movimento (emite documento fiscal, gera parcela financeira, baixa estoque), tudo isso acontece já no momento do `Finalizar Separação` no monitor.
- Se o tipo deixa o movimento **em aberto** para conferência manual, a baixa de estoque só acontece quando o financeiro/atendente finalizar pela tela `Vendas` (código `202`).

A integração não impõe um modo nem outro — ela respeita o tipo de movimento. Alinhe com o cliente qual o comportamento esperado e configure o tipo de acordo.

### ❓ O movimento gerado fica em aberto. É normal?

Sim — o `Finalizar Separação` do monitor iFood **cria o movimento em aberto**. A regra de finalização (emissão de NFC-e, conta a receber, baixa de estoque) é toda definida pelo `Tipo de Movimento iFood` configurado na empresa. Confira a configuração do tipo: se ele está marcado para finalizar/emitir automaticamente, isso já acontece junto da criação; senão, a finalização precisa ser manual em `Vendas`.

---

## 🚫 Cancelamentos e disputas

### ❓ O cliente cancelou no app. Preciso fazer algo manualmente?

**Não.** O processo automático trata sozinho:

1. O monitor de integração captura o evento de cancelamento na próxima rodada
2. Marca o pedido como `Cancelado` no banco
3. Se o movimento já existia, cancela o movimento e a parcela em Contas a Receber

Você só precisa intervir se notar que o cancelamento não foi pego. Nesse caso confirme que o monitor de integração está rodando.

### ❓ O iFood abriu uma disputa. O que acontece com a venda no Sol.NET?

O pedido é marcado como **`Em Disputa`** no banco, mas o movimento **NÃO é cancelado** automaticamente — a disputa pode ser resolvida a favor da loja no próprio iFood, e nesse caso a venda continua válida. Acompanhe a disputa pelo painel do iFood. Se a disputa for resolvida contra a loja, faça o cancelamento manual do movimento por dentro do Sol.NET.

### ❓ Tem como reabrir um pedido cancelado?

**Não.** Cancelamento (pela loja ou pelo cliente) é definitivo do ponto de vista da integração. Para vender de novo, o cliente precisa fazer um novo pedido no iFood.

---

## 🐞 Erros e bloqueios

### ❓ Cliquei em `Aceitar Pedido` e o sistema avisou "Não foi possível confirmar o pedido na API do iFood". O que faz?

A API do iFood rejeitou a confirmação. Causas comuns:

- **Pedido já foi cancelado pelo cliente** entre a captura e o seu clique. Atualize o grid (`Atualizar`) e veja o novo status.
- **Credencial expirada** — a integração faz refresh automático do token, mas se o iFood tiver feito alguma alteração recente, pode ser necessário re-autenticar a conta da loja no iFood antes que a confirmação volte a funcionar.
- **Pedido com restrição na conta iFood** (cardápio fechado, loja pausada). Confira o painel do iFood.

### ❓ Aceitei o pedido, separei, e na hora de finalizar deu erro "Falha ao criar movimento". E agora?

O Sol.NET tentou criar o movimento mas algo bloqueou — provavelmente uma regra do `Tipo de Movimento iFood` (campo obrigatório não preenchido, configuração fiscal incompleta, falta de parâmetro). Recomendações:

1. Anote o `Código` do pedido e a mensagem de erro exibida
2. Revise a configuração do `Tipo de Movimento iFood` no `Cadastro de Tipos de Movimento` — corrija o que estiver faltando (forma de pagamento padrão, série fiscal, parâmetros fiscais)
3. O pedido continua no monitor com status `Em Preparação` (ou `Pronto p/ Retirada`) — quando o tipo for corrigido, basta tentar `Finalizar Separação` de novo

Não há **perda de dados** — o pedido fica em separação até alguém conseguir finalizar.

### ❓ Vejo o pedido amarelo, mas ele tem status diferente quando seleciono. Por quê?

A cor da linha é atualizada a cada `Atualizar`/recarga do grid. Se o pedido mudou de status entre a última atualização e agora (por exemplo, o cliente cancelou no app e o monitor de integração já capturou o cancelamento), clique em **`Atualizar`** para o grid refletir o status atual.

---

## 🧭 Acompanhamento e auditoria

### ❓ Como vejo os pedidos cancelados/finalizados do dia inteiro para conferência fim de turno?

Mantenha o `Monitor de Pedidos iFood` aberto com o filtro `Data:` no dia desejado. O grid mostra **todos os pedidos do dia**, em qualquer status, e a coluna `Status` (junto com a cor da linha) indica em que estado cada um está.

### ❓ Como acho um pedido de dias anteriores?

Mude o campo `Data:` no topo da tela para o dia que quer consultar. O grid recarrega automaticamente filtrando por aquela data.

### ❓ Vou auditar a venda iFood do mês. Onde encontro os movimentos gerados pela integração?

Os movimentos vão para a tela `Vendas` (código `202`) como qualquer outra venda — mas no `Tipo de Movimento` que você configurou para iFood. **Filtre por esse tipo** na consulta de movimentos para isolar só as vendas iFood do período.

---

**Última atualização**: Maio de 2026  
**Versão**: 1.0  
**Público-alvo**: Usuários do Sol.NET e atendentes de balcão
