# 📄 FAQ — Manifestação do Destinatário - Sol.NET

## 🎯 Visão Geral

Perguntas e respostas práticas sobre a tela `Manifestação do Destinatário` (código **`401`** na pesquisa F1). Veja também a [documentação completa](documentacao_manifestacao_destinatario.md) e o [guia rápido](guia_rapido_manifestacao_destinatario.md).

---

## Conceitos básicos

### ❓ O que é Manifestação do Destinatário?

É a obrigação fiscal de a empresa **reconhecer ou rejeitar formalmente** uma NF-e ou CT-e emitida contra o seu CNPJ. Existem quatro tipos: Confirmação da Operação, Ciência da Emissão, Desconhecimento da Operação e Operação Não Realizada. O envio é feito direto para a SEFAZ.

### ❓ Toda empresa precisa manifestar?

A obrigatoriedade varia por **UF, regime de tributação e CNAE**. A SEFAZ define quem é obrigado a manifestar e quem pode fazer só por opção. Em caso de dúvida, oriente o cliente a falar com o contador — o Sol.NET permite manifestar mesmo quando não é obrigatório, como controle interno.

### ❓ Qual a diferença entre as quatro manifestações?

- **Confirmação (`1`)** — Recebi e a operação aconteceu como descrito.
- **Ciência (`4`)** — Sei que a nota existe, mas ainda não validei.
- **Desconhecimento (`2`)** — Não reconheço essa nota.
- **Operação Não Realizada (`3`)** — Conheço, mas a operação não se efetivou.

A Ciência é um **passo intermediário** e deve ser seguida por uma das outras três quando a situação estiver clara.

### ❓ A manifestação é definitiva?

- `Confirmação` e `Desconhecimento` são **definitivas** — depois delas o fornecedor não pode mais cancelar a NF-e.
- `Ciência` é **intermediária** — deve ser complementada depois.
- `Operação Não Realizada` também é definitiva.

> ⚠️ Mesmo que o sistema permita enviar uma manifestação diferente depois, **nenhuma anula a anterior** — o histórico permanece registrado na SEFAZ.

---

## Acesso e operação

### ❓ Como abrir a tela?

Pressione **F1** em qualquer lugar do Sol.NET, digite **`401`** (ou parte do nome `Manifestação`) e confirme.

### ❓ Por que a nota não aparece na lista?

Verifique nesta ordem:

1. A `Descrição da Loja` filtrada é a loja que receberia a nota?
2. O período em `Data` cobre a data de emissão da NF-e?
3. Os outros filtros (`Situação da NF-e`, `Situação da Manifestação`, `Modelo`) estão restritivos demais?
4. A nota foi emitida há mais de **1 hora**? O download da SEFAZ é feito pelo aplicativo **Sol.NET MonitorNFCe** em ciclos (padrão **59 minutos**); notas muito recentes podem ainda não ter sido baixadas.
5. O `Sol.NET MonitorNFCe` está rodando no servidor?

Se nada disso resolveu, peça a `Chave de Acesso` ao fornecedor e use **`(Web)`** para conferir o status diretamente no portal da SEFAZ.

> ⚠️ **Não tente** clicar nos botões `NF-e` / `CT-e` à esquerda da faixa para forçar o download — estão descontinuados e exibem aviso bloqueando a operação. Consultas em excesso à SEFAZ podem causar suspensão do manifesto da empresa.

### ❓ Como manifestar várias notas de uma vez?

1. Filtrar as notas desejadas (por loja, situação ou período).
2. Botão direito no grid → `Selecionar Todos` (ou marcar manualmente as caixas `Sel.`).
3. Opcional: `Mostrar Só Selecionados` para revisar antes.
4. Clicar no botão da manifestação desejada (`Confirmar(1)`, `Ciência(4)`, etc.).

### ❓ Existem dois botões `NF-e` na tela — qual é qual?

Sim, e a posição na faixa define a função:

- **`NF-e` à esquerda da faixa** — **descontinuado**. Era o antigo botão de download em massa. Hoje exibe o aviso "Essa Função foi Automatizada" e bloqueia a operação. **Não usar.**
- **`NF-e` entre `Zerar NSU` e `Confirmar`** — ativo. Inicia o **lançamento da NF-e selecionada** como entrada na Movimentação, usando o XML obtido junto à SEFAZ.

O mesmo vale para os dois botões `CT-e`. O da esquerda é o descontinuado; o que aparece junto da faixa central de ações é o que lança uma CT-e específica (uma por vez).

### ❓ Como cancelar uma manifestação enviada por engano?

**Não é possível cancelar** — a SEFAZ não aceita cancelamento de manifestação. O histórico fica registrado. O que se pode fazer:

- Conversar com o fornecedor sobre o erro.
- Enviar uma manifestação posterior diferente — ela ficará registrada **junto** com a anterior, sem anulá-la.

Sempre confirme antes de manifestar em lote.

---

## Vínculo com a Movimentação

### ❓ O que são as colunas começando com `M-` no grid?

São dados da **entrada já lançada** no Sol.NET para aquela NF-e. Quando a nota foi importada/digitada como entrada na Movimentação, o Sol.NET vincula automaticamente e exibe essas colunas (`M-Número NF-e`, `M-Valor NF-e`, `M-Data Emissão`, etc.) para conferência.

### ❓ E quando as colunas `M-` estão vazias?

A nota foi baixada da SEFAZ, mas **ainda não foi lançada como entrada** — geralmente uma pendência de digitação. Lance a entrada importando o XML ou cadastrando manualmente; o vínculo aparece na próxima busca.

### ❓ Como ir da manifestação para a entrada lançada?

Botão direito sobre a linha → `Ir para Movimentação` (ou `Ir para Movimentação Financeiro` para abrir direto a aba financeira).

### ❓ Preciso manifestar antes de lançar a entrada?

Tecnicamente não, mas o XML só fica liberado para download a partir da `Ciência(4)`. O fluxo recomendado é: dar Ciência → importar o XML → conferir → Confirmar.

---

## Download das notas, NSU e Monitor

### ❓ Quem baixa as notas da SEFAZ?

**Não é a tela `Manifestação do Destinatário`** — quem baixa é o aplicativo **Sol.NET MonitorNFCe**, que roda em background no servidor. A tela apenas **lista** o que já foi baixado e permite manifestar.

### ❓ De quanto em quanto tempo o Monitor consulta a SEFAZ?

A periodicidade é configurável. **O valor padrão é 59 minutos** (na prática, ~1 vez por hora) para a consulta à SEFAZ de novas notas para Manifestação. O ciclo principal interno do Monitor é de 5 minutos, e a rotina de Manifestação roda em ~12 desses ciclos.

### ❓ Por que os botões antigos de download (`NF-e` / `CT-e` à esquerda) foram desativados?

Para evitar **alto consumo de dados** com consultas repetidas à SEFAZ. Quando o download era manual, era comum o usuário clicar repetidas vezes para ver se "veio mais alguma" — esse padrão pode causar **suspensão do manifesto da empresa por até 24 horas** e, em casos mais graves, **suspensão da Inscrição Estadual e aplicação de multa**. Hoje o Monitor faz o download em ritmo controlado e os botões antigos só exibem o aviso explicativo.

### ❓ O que é o "NSU"?

NSU é o **Número Sequencial Único** que a SEFAZ usa para controlar quais documentos cada CNPJ já recebeu. Cada NF-e ou CT-e recebe um NSU. O Sol.NET guarda o último NSU baixado por empresa e, no próximo ciclo do Monitor, pede só os números maiores — para não baixar tudo de novo.

### ❓ Quando faz sentido `Zerar NSU`?

Apenas em situações específicas:

- Migração para um banco novo ou backup restaurado em que o NSU local ficou para trás.
- Suspeita de notas perdidas em sincronizações anteriores.
- Auditoria histórica completa solicitada pelo contador.

Fora desses casos, **evite** — o Monitor passa a reconsultar notas dos últimos 180 dias, com risco real de suspensão na SEFAZ (o sistema mostra aviso explícito ao clicar).

### ❓ Posso zerar NSU de CT-e pela tela?

Não. O botão **`Zerar NSU NF-e`** funciona apenas para NF-e; para CT-e o sistema responde *"Não Permitido para CT-e!"*.

### ❓ O Monitor parou de baixar notas. O que verificar?

1. Confirmar que o aplicativo **Sol.NET MonitorNFCe** está aberto e rodando no servidor.
2. Verificar a conexão de internet do servidor com a SEFAZ.
3. Conferir validade do **certificado digital** da empresa — sem ele a SEFAZ não autoriza consulta.
4. Verificar se a empresa não está em **suspensão de manifesto** (cliente fez consultas demais antes da automatização, ou o Monitor está em estado anormal).

O botão `Parar` da tela **não para o download** — para apenas uma manifestação em lote em andamento.

---

## Situações especiais

### ❓ A nota apareceu como `Fora do Prazo`. Posso manifestar mesmo assim?

Sim — o Sol.NET aceita o registro local. Mas a SEFAZ **não considera** a manifestação como dentro do prazo legal. Oriente o cliente a falar com o contador sobre o impacto fiscal específico antes de manifestar.

### ❓ A nota apareceu como `Já Manifestada` ou `Já Negada`. O que isso significa?

A SEFAZ **já tem uma manifestação registrada** para essa nota. As duas causas mais comuns são:

- O usuário tentou manifestar de novo a mesma nota (clique repetido, manifestação em lote que pegou notas já tratadas).
- A manifestação veio de outro sistema, de outra instalação do Sol.NET (cliente que migrou de servidor) ou foi feita direto no portal da SEFAZ.

Em qualquer dos casos, **não é possível sobrescrever** — a manifestação existente prevalece. Se o cliente acha que a manifestação atual está errada, oriente-o a tratar com o fornecedor (e, se for o caso, com o contador).

### ❓ O que é `Canc.Manual` na coluna `Situação da NF-e`?

É um status **exclusivo do Sol.NET**, atribuído manualmente pelo menu do botão direito (`Alterar Situação da NF-e (Cancelado Manual)`). **Não tem efeito na SEFAZ** — para a SEFAZ a nota continua no status real (normalmente `Autorizada`). Use só quando o cliente entender essa limitação.

### ❓ E `Desfazer Situação da NF-e (Autorizada)`?

Reverte o `Canc.Manual` para `Autorizada`. Também é uma alteração **interna** do Sol.NET, sem impacto na SEFAZ.

### ❓ Como manifesto CT-e (Conhecimento de Transporte)?

A mesma tela atende NF-e e CT-e. Troque `Modelo` para `CT-e`, clique em **`CT-e`** para baixar, depois use os mesmos botões de manifestação. O fluxo legal das quatro manifestações é idêntico.

---

## Relatórios e auditoria

### ❓ Como gerar um relatório das manifestações feitas?

Clique em **`Relatórios`** na faixa de botões inferior. As listagens disponíveis incluem manifestações por período, por loja e por tipo.

### ❓ É possível ver o histórico completo de uma nota?

Sim — selecione a linha no grid e clique em **`Status`** para consultar a situação atual e o histórico de eventos da nota direto na SEFAZ. Também é possível abrir o **portal da SEFAZ** via botão **`(Web)`** para conferência visual.

### ❓ Há diferença entre `Data Pesquisa` e `Data Manifestação`?

Sim:

- `Data Pesquisa` — quando o Sol.NET baixou a nota da SEFAZ pela primeira vez.
- `Data Manifestação` — quando o usuário efetivamente enviou a manifestação.

Pode haver dias entre uma e outra (nota baixada hoje, manifestada após conferência).

---

**Última atualização**: Maio de 2026  
**Versão**: 1.1  
**Público-alvo**: Equipe de suporte Sol.NET
