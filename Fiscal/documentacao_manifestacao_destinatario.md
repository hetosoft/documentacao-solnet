# 📄 Manifestação do Destinatário - Sol.NET

## 🎯 Visão Geral

A **Manifestação do Destinatário** (também chamada de **MD-e**) é a obrigação fiscal de a empresa **reconhecer ou rejeitar** uma nota fiscal eletrônica emitida contra o seu CNPJ. Toda NF-e que um fornecedor emite passa pela SEFAZ, e a empresa destinatária precisa "manifestar-se" sobre ela informando se a operação realmente ocorreu, se está apenas tomando ciência, se desconhece a emissão ou se a operação não se concretizou.

O Sol.NET concentra essa rotina em uma única tela, que faz o **download das notas disponíveis na SEFAZ**, mostra a situação atual de cada uma e permite enviar a manifestação com um clique.

### Para que serve

- ✅ Baixar da SEFAZ a lista de NF-e e CT-e emitidas contra os CNPJs das lojas da empresa
- ✅ Aplicar uma das quatro manifestações previstas (Confirmação, Ciência, Desconhecimento, Operação Não Realizada)
- ✅ Acompanhar quais notas já foram manifestadas e quais ainda estão pendentes
- ✅ Cruzar as NF-e baixadas com as entradas já lançadas na movimentação interna
- ✅ Identificar notas fora do prazo de manifestação, já negadas ou já manifestadas

### Quando o suporte é acionado

- Cliente reclama que "a nota não aparece" → quase sempre é NSU desatualizado ou loja errada na busca
- Cliente quer manifestar em lote → uso de "Selecionar Todos" + botão da manifestação
- SEFAZ marcou a nota como "Fora do Prazo" → manifestação só serve para registro interno; explicar limitação
- Cliente acidentalmente confirmou nota errada → orientar sobre Desconhecimento posterior e contato com fornecedor

---

## 🚪 Como acessar

A tela é aberta pela pesquisa universal:

1. Pressione **F1** em qualquer ponto do Sol.NET.
2. Digite **`401`** (código da tela) ou parte do nome **Manifestação**.
3. Confirme para abrir a tela `Manifestação do Destinatário`.

---

## 🤖 Como as notas chegam à tela

O download das NF-e e CT-e disponíveis na SEFAZ **não é feito por esta tela** — é feito por uma **aplicação à parte que roda em background**, o **Sol.NET MonitorNFCe**. O Monitor consulta a SEFAZ em intervalos configuráveis e grava as notas encontradas no banco; a tela `Manifestação do Destinatário` apenas **lista** o que o Monitor já trouxe.

- **Periodicidade padrão**: o Monitor consulta a SEFAZ por novas notas para Manifestação a cada **59 minutos**. Esse valor é configurável nas configurações do Sincronizador.
- **Por que não baixar manualmente**: a SEFAZ limita o volume de consultas por CNPJ. Consultas em excesso podem causar **suspensão do manifesto da empresa por até 24 horas** e, em casos mais graves, **suspensão da Inscrição Estadual e aplicação de multa**.

Se uma nota recente não está na lista, o caminho normal é **aguardar o próximo ciclo do Monitor** (no máximo ~1 hora). Se mesmo assim não aparecer, verifique se o Monitor está rodando no servidor — não tente forçar o download pela tela.

> ⚠️ Os botões `NF-e` e `CT-e` à **esquerda** da faixa de botões existem por compatibilidade, mas estão **descontinuados**. Ao serem clicados exibem o aviso *"Essa Função foi Automatizada"* e bloqueiam a sincronização manual. **Não devem ser usados.**

---

## 🔄 Os quatro tipos de manifestação

Cada NF-e pode receber **uma** das manifestações abaixo. O código entre parênteses é o número que aparece nos botões da tela e nos relatórios.

### ✅ Confirmação da Operação (`1`)

**Significa**: "Recebi a mercadoria/serviço e a operação aconteceu exatamente como a nota descreve."

- Quando usar: nota corresponde a uma compra real, mercadoria entregue, serviço prestado, valores conferidos.
- Botão: **`Confirmar(1)`**.
- Efeito legal: a partir daí, **a nota não pode mais ser cancelada pelo fornecedor**. Manifestação definitiva.

### 👁️ Ciência da Emissão (`4`)

**Significa**: "Tomei conhecimento de que essa nota foi emitida contra o meu CNPJ, mas ainda não validei a operação."

- Quando usar: passo inicial obrigatório em vários cenários; ainda não há condição de confirmar nem rejeitar (mercadoria não chegou, falta conferência).
- Botão: **`Ciência(4)`**.
- Efeito legal: permite o **download do XML** da nota mesmo sem ter ainda uma decisão final. **Não é definitiva** — deve ser seguida por uma das outras três manifestações.

### ❌ Desconhecimento da Operação (`2`)

**Significa**: "Eu não reconheço essa nota. Não autorizei essa compra, não recebi essa mercadoria."

- Quando usar: emissão indevida, possível fraude, CNPJ usado por engano.
- Botão: **`Descon.(2)`**.
- Efeito legal: a nota fica registrada como **rejeitada pelo destinatário**. O fornecedor é notificado.

### 🚫 Operação Não Realizada (`3`)

**Significa**: "Conheço essa nota, mas a operação que ela representa **não se efetivou** (entrega recusada, devolução total na origem, contrato cancelado)."

- Quando usar: a empresa sabe do pedido, mas a entrega não ocorreu ou foi rejeitada antes do recebimento.
- Botão: **`Não Real.(3)`**.
- Efeito legal: registra a não concretização na SEFAZ.

> ℹ️ **Sobre prazos**: a SEFAZ define prazos próprios para cada manifestação. Notas que ultrapassam o prazo ficam marcadas no Sol.NET como `Fora do Prazo` (código `97`) ou `Fora do Prazo - Ciência` (código `96`) — nesses casos a manifestação ainda pode ser registrada para controle interno, mas o efeito na SEFAZ é limitado. Consulte o contador da empresa para os prazos vigentes.

---

## 🔍 Consultando documentos na tela

A parte de cima da tela traz **dois grupos de filtros** organizados em sub-abas: `Notas Fiscais` e a aba de filtros relacionados a movimento. Quem opera a tela usa a primeira para a rotina diária.

### Filtros principais (sub-aba `Notas Fiscais`)

| Filtro | O que filtra |
|--------|--------------|
| `Descrição da Loja` | CNPJ/empresa que estará recebendo as manifestações |
| `Modelo` | `NF-e` ou `CT-e`. Cada modelo é consultado e manifestado separadamente |
| `Situação da NF-e` | Situação cadastral do documento na SEFAZ: `Todos`, `Autorizado`, `Cancelada`, `Canc.Manual`, `Denegado` |
| `Situação da Manifestação` | Última manifestação registrada: `Sem manifestação`, `Confirmada`, `Ciência`, `Desconhecida`, `Operação Não Realizada`, `Fora do Prazo - Ciência`, `Fora do Prazo`, `Já Negada`, `Já Manifestada` |
| `Campo a pesquisar` | Coluna que será usada para busca livre: `Código do Manifesto`, `Chave de Acesso`, `CNPJ do Emitente`, `UF`, `Fornecedor`, `Valor`, `Número` |
| `Condição` | `Contém`, `Inicia com`, `=`, `>`, `<`, `>=`, `<=`, `<>`, `Vazio`, `Não Vazio`, `Entre`, `Lista` |
| `Data` | Coluna de data usada no intervalo: `Data Emissão`, `Data Atualização`, `Data Entrada (Mov.)`, `Data Pesquisa`, `Data Manifestação` |
| `Inicial` / `Final` | Período do filtro de data |

Depois de ajustar os filtros, clique em **`Buscar`** para atualizar a lista.

### O que cada coluna do grid representa

O grid do meio da tela exibe uma linha por documento. As colunas mais importantes para o suporte são:

- `Sel.` — caixa de seleção (usada para manifestar em lote)
- `Modelo` — `NF-e` ou `CT-e`
- `Situação da Manifestação` — última manifestação aplicada (vazio = ainda sem manifestação)
- `Data Emissão` — quando o fornecedor emitiu a NF-e
- `Data Atualização` — última vez que o Sol.NET sincronizou essa nota com a SEFAZ
- `Situação do Documento` — status SEFAZ da NF-e (Autorizada, Cancelada, Denegada…)
- `Número do Documento` / `Valor` / `Razão Social` — dados da NF-e
- `Chave de Acesso` — chave de 44 dígitos para consulta cruzada
- `UF` — estado do emitente
- `Tipo de Operação` — entrada, saída, etc.
- Colunas começando com **`M-`** (ex.: `M-Situação da NF-e`, `M-Número NF-e`) — dados da **movimentação interna** do Sol.NET, quando a nota já foi lançada como entrada
- `Data Pesquisa` — quando o Sol.NET viu essa nota pela primeira vez na SEFAZ
- `Data Manifestação` — quando a manifestação foi enviada

---

## 🖱️ Botões e ações

A faixa de botões na parte inferior reúne as ações disponíveis. **Atenção**: existem dois pares de botões com os mesmos rótulos (`NF-e` e `CT-e`), com funções diferentes — a posição na faixa indica para que servem.

### Ações de manifestação

- **`Confirmar(1)`** — envia Confirmação da Operação para a(s) nota(s) selecionada(s)
- **`Ciência(4)`** — envia Ciência da Emissão
- **`Descon.(2)`** — envia Desconhecimento
- **`Não Real.(3)`** — envia Operação Não Realizada

A manifestação pode ser feita uma a uma ou em **lote**, marcando várias linhas em `Sel.` antes de clicar no botão.

### Importação do documento selecionado (entre `Zerar NSU` e `Confirmar`)

Esses botões iniciam o **lançamento da nota selecionada como entrada** na Movimentação, a partir do XML obtido junto à SEFAZ.

- **`NF-e`** — inicia a importação/lançamento da **NF-e** selecionada
- **`CT-e`** — mesma operação, para um **CT-e** específico (uma nota por vez)

Pré-requisito: a nota precisa estar com **Ciência** ou **Confirmação** já enviada — sem isso a SEFAZ não libera o XML.

### Consulta e auditoria

- **`Status`** — consulta a situação atual do documento selecionado na SEFAZ (útil para verificar cancelamento posterior pelo emitente)
- **`(Web)`** — abre o **portal da SEFAZ** no navegador para consulta visual da nota

### Controle e manutenção

- **`NF-e` / `CT-e` à esquerda da faixa** — **descontinuados**. Eram os antigos botões de download em massa. Hoje exibem o aviso *"Essa Função foi Automatizada"* e bloqueiam a sincronização manual (o download é feito pelo Sol.NET MonitorNFCe — ver [Como as notas chegam à tela](#-como-as-notas-chegam-à-tela)). **Não devem ser usados.**
- **`Parar`** — interrompe um processamento de manifestação em andamento (por exemplo, manifestação em lote pesada que precisa ser cancelada)
- **`Zerar NSU NF-e`** — zera o **contador NSU** da loja para que o Monitor reconsulte **todas as notas dos últimos 180 dias**. Operação pesada — o sistema exibe aviso explícito sobre risco SEFAZ (suspensão de manifesto, multa). Use **somente sob orientação direta**. Funciona apenas para NF-e (CT-e exibe `Não Permitido para CT-e!`).
- **`Relatórios`** — abre listagens detalhadas das manifestações realizadas
- **`Sair`** — fecha a tela

### Menu do botão direito (sobre o grid)

Clicando com o botão direito no grid, aparecem ações rápidas:

- `Copiar Chave de Acesso` — copia para a área de transferência a chave da linha atual
- `Selecionar Todos` / `Desmarcar Todos`
- `Mostrar Só Selecionados` / `Mostrar todos`
- `Ir para Movimentação` — abre a entrada já lançada que está vinculada à nota
- `Ir para Movimentação Financeiro` — abre a aba financeira do movimento vinculado
- `Alterar Situação da NF-e (Cancelado Manual)` — marca **manualmente** a NF-e como cancelada no Sol.NET (sem efeito na SEFAZ)
- `Desfazer Situação da NF-e (Autorizada)` — reverte o status manual para `Autorizada`

> ⚠️ As opções `Alterar/Desfazer Situação` afetam **apenas o cadastro interno** do Sol.NET, não enviam nada para a SEFAZ. Use só quando o cliente entende que o status na SEFAZ continua o que for.

---

## 🔗 Vínculo com movimentos do Sol.NET

Quando uma NF-e baixada já foi importada como **entrada** na movimentação (via [Importar XML](documentacao_importar_xml.md) ou lançada manualmente), o Sol.NET cria o vínculo automaticamente. Esse vínculo aparece de duas formas:

1. **Colunas `M-` no grid** — replicam os dados do movimento ao lado dos dados da nota, permitindo conferir divergências (valor, data de emissão, número) entre o que o fornecedor emitiu e o que foi lançado.
2. **Atalho `Ir para Movimentação`** (botão direito) — abre a entrada correspondente para consulta ou ajuste.

Notas **sem `M-`** preenchido são notas baixadas da SEFAZ que ainda **não foram lançadas como entrada**. É um indicador útil para verificar pendências de digitação ou de importação.

---

## 🧰 Manutenção

### Quando "zerar o NSU" é justificado

O **NSU** é o número sequencial que a SEFAZ usa para controlar quais notas a empresa já recebeu. Cada vez que o Sol.NET baixa um lote, ele anota o último NSU recebido — na próxima consulta, pede só os NSUs maiores.

Zerar o NSU faz a SEFAZ reenviar **tudo desde o início**. Útil em três cenários:

- Migração para um banco novo ou backup restaurado em que o NSU local ficou defasado
- Suspeita de notas perdidas em uma sincronização anterior
- Auditoria histórica completa solicitada pelo contador

Fora desses casos, **evite zerar o NSU** — o processamento de centenas ou milhares de notas pode demorar e consumir banda.

### Alterar/Desfazer Situação da NF-e (manual)

Essas opções existem para casos atípicos em que o status no Sol.NET diverge da realidade fiscal (por exemplo, fornecedor cancelou a NF-e fora do prazo legal por meio de inutilização ou comunicado externo). Aplicam status **apenas no Sol.NET** — a SEFAZ continua mostrando o status real.

---

## 💡 Exemplos Práticos

### Exemplo 1 — Manifestar uma entrada de compra do dia

1. Abra a tela `Manifestação do Destinatário` (F1 → `401`).
2. Em `Descrição da Loja`, selecione a loja que recebeu a mercadoria.
3. Confirme `Modelo = NF-e`.
4. Clique em **`Buscar`** para atualizar a lista com o que o Monitor já trouxe.
5. Localize a nota do fornecedor na lista (use o campo `Fornecedor` + `Contém` se preferir buscar).
6. Marque a caixa `Sel.` na linha.
7. Clique em **`Confirmar(1)`**.
8. A coluna `Situação da Manifestação` passa para `Confirmada` e a `Data Manifestação` é preenchida.

> Se a nota recente ainda não aparece, aguarde o próximo ciclo do Sol.NET MonitorNFCe (~1 hora). Não tente forçar pelos botões `NF-e`/`CT-e` à esquerda — estão descontinuados.

### Exemplo 2 — Receber ciência em lote no início do dia

1. Em `Situação da Manifestação`, escolha `Sem manifestação`.
2. Defina o período em `Data Emissão` (ex.: últimos 7 dias).
3. Clique em **`Buscar`**.
4. Clique com o botão direito no grid → **`Selecionar Todos`**.
5. Clique em **`Ciência(4)`**.
6. Aguarde o processamento. Depois, retorne aos casos um a um para Confirmar, Desconhecer ou marcar Não Realizada.

> Esse é o fluxo mais comum: dar Ciência em massa para liberar o XML das notas e depois tratar cada uma individualmente.

### Exemplo 3 — Recusar uma nota emitida por engano

1. O fornecedor avisa que emitiu nota com CNPJ errado.
2. Localize a nota (filtro por `Chave de Acesso` ou `Número`).
3. Confirme com o cliente que a operação **não existe**.
4. Marque a linha e clique em **`Descon.(2)`**.
5. A nota fica registrada como `Desconhecida` — o fornecedor é notificado pela SEFAZ.

### Exemplo 4 — Identificar notas baixadas mas não lançadas

1. Em `Situação da Manifestação`, deixe `Confirmada`.
2. Defina o período do mês atual.
3. Clique em `Buscar`.
4. Olhe a coluna `M-Número NF-e`: linhas com a célula **vazia** são notas confirmadas que **ainda não foram lançadas** como entrada na Movimentação.
5. Lance a entrada (importando o XML ou manualmente) e o vínculo aparecerá automaticamente na próxima busca.

---

## ❓ FAQ / Problemas Comuns

### ❓ Cliente diz que "uma nota não está aparecendo na tela". Por onde começar?

1. Confirmar que a `Descrição da Loja` selecionada é a loja que receberia a nota.
2. Limpar filtros de data — pode ser que a emissão esteja fora do intervalo padrão.
3. Conferir há quanto tempo a nota foi emitida — o Monitor consulta a SEFAZ a cada **~1 hora**; uma nota emitida nos últimos minutos pode simplesmente ainda não ter sido baixada.
4. Verificar com o responsável do servidor se o **Sol.NET MonitorNFCe** está rodando.
5. Se mesmo após o próximo ciclo a nota não aparecer, peça a `Chave de Acesso` ao fornecedor e use **`(Web)`** para confirmar na SEFAZ que a nota foi mesmo autorizada contra esse CNPJ.

### ❓ Manifestar pode ser desfeito?

Não. As manifestações enviadas à SEFAZ **não podem ser canceladas**. O que se pode fazer é enviar uma manifestação posterior diferente (ex.: deu `Confirmação` por engano → enviar `Desconhecimento` em seguida não reverte a Confirmação anterior; o histórico fica). Sempre confirme com o cliente **antes** de clicar nos botões de manifestação em lote.

### ❓ A nota apareceu como `Fora do Prazo`. O que fazer?

Manifestar mesmo assim funciona apenas para **controle interno** — o Sol.NET aceita o registro, mas a SEFAZ não considera a manifestação dentro do prazo. Oriente o cliente a falar com o contador para entender o impacto fiscal e, se necessário, registrar uma justificativa por outro meio.

### ❓ A nota aparece como `Já Manifestada` ou `Já Negada`. Por quê?

Significa que a SEFAZ **já tem uma manifestação registrada** para essa nota. As causas mais comuns são:

- O usuário tentou manifestar de novo uma nota que ele próprio já havia manifestado antes.
- Outro sistema, outra instalação do Sol.NET ou o portal da SEFAZ registrou a manifestação anteriormente (cliente que migrou de servidor, por exemplo).

Em qualquer dos casos, não é possível sobrescrever — a manifestação existente prevalece.

### ❓ A coluna `Situação da NF-e` mostra `Canc.Manual` — o que é?

É um status **exclusivo do Sol.NET**, atribuído manualmente pelo botão direito (`Alterar Situação da NF-e (Cancelado Manual)`). Para a SEFAZ a nota continua no estado real (geralmente `Autorizado`). Sirva como sinal de que o cliente fez uma marcação local — pergunte por que antes de mexer.

### ❓ O Monitor parou de baixar notas — o que verificar?

A tela em si **não baixa notas** — quem baixa é o aplicativo **Sol.NET MonitorNFCe** que roda no servidor. Quando notas param de chegar:

1. Confirmar com o responsável que o `Sol.NET MonitorNFCe` está aberto e rodando no servidor.
2. Verificar a conexão de internet do servidor com a SEFAZ.
3. Conferir a validade do **certificado digital** da empresa — sem certificado válido a SEFAZ não autoriza a consulta.
4. Verificar se a empresa não está em **suspensão de manifesto** (ocorre se o Monitor — ou alguém usando os botões antigos — fizer consultas em excesso).

Na tela `Manifestação do Destinatário`, o botão **`Parar`** serve apenas para interromper uma manifestação em lote em andamento — não tem efeito sobre o download.

### ❓ Qual a diferença entre "Data Pesquisa" e "Data Manifestação"?

- `Data Pesquisa` — quando o Sol.NET viu a nota pela primeira vez (download da SEFAZ).
- `Data Manifestação` — quando o usuário enviou a manifestação efetiva (Confirmação, Ciência, etc.).

Pode haver dias de diferença entre as duas: a nota foi baixada hoje, mas só será manifestada depois de conferência.

### ❓ Manifesto CT-e (Conhecimento de Transporte) funciona igual a NF-e?

Sim, a mesma tela atende os dois. Basta trocar o `Modelo` para `CT-e` e usar os botões **`CT-e`** (download) e os mesmos botões de manifestação. O fluxo legal das quatro manifestações também é idêntico.

---

**Última atualização**: Maio de 2026  
**Versão**: 1.1  
**Público-alvo**: Equipe de suporte Sol.NET, usuários do módulo Fiscal
