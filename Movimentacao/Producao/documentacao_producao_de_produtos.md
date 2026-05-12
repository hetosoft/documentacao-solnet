# 📄 Cadastro de Produção de Produtos - Sol.NET

## 🎯 Visão Geral

A tela de **Produção de Produtos** é onde a fórmula vira movimento de estoque. Cada produção parte de uma **Fórmula de Produto** (cadastrada em `Cadastro de Fórmula de Produtos`, código `143`), informa **quanto** será produzido na rodada e, ao ser finalizada, **gera automaticamente os três movimentos de estoque** que materializam a operação:

1. **Saída** dos ingredientes (com o Tipo de Movimento configurado para insumos consumidos).
2. **Entrada** do produto acabado (com o Tipo de Movimento configurado para o que sai pronto).
3. **Saída de Perda** (quando a fórmula tem itens marcados como Perda), com um Tipo de Movimento próprio.

A produção pode ficar em três estados — **Iniciada**, **Finalizada** ou **Cancelada** — e o usuário controla a transição pelos botões da própria tela. Os movimentos só são gerados na **Finalização**; antes disso, o registro é apenas uma intenção que pode ser ajustada ou cancelada sem afetar o estoque.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Produção de Produtos |
| **Código (`F1`)** | `144` |

Abra a pesquisa universal (atalho `F1`) e digite **`144`** ou parte do nome **`Produção de Produtos`**.

---

## 🧭 Sub-abas do formulário

| Aba | O que mostra |
|-----|--------------|
| **Principal** | Configuração da produção + ingredientes + saldo de estoque dos insumos (lateral). |
| **Movimento** | Resumo dos três movimentos gerados pela finalização (Entrada, Saída, Perda). Só faz sentido depois da produção estar Finalizada. |

A aba **Principal** é subdividida em:

| Painel | Conteúdo |
|--------|----------|
| **Configuração** | Tipos de Movimento de Entrada, Saída e Perda + Situação e Local de Estoque alvo. |
| **Dados da Produção** | Código, Loja, datas (Início, Fim, Cadastro) e Status. |
| **Dados do Produto Acabado** | Fórmula escolhida, produto acabado, quantidades de produção e fator de conversão. |
| **Ingredientes** | Grade dos insumos consumidos (puxada da fórmula e ajustada à quantidade real). |
| **Estoque** (lateral) | Saldo físico, saldo por Local, Prateleira / Localização e Estoque Mínimo do insumo selecionado — útil para conferir se há estoque suficiente antes de finalizar. |

---

## 📝 Campos

### Filtros da consulta (lista de produções)

| Filtro | O que faz |
|--------|-----------|
| **Inicial / Final** | Faixa de datas (Início Produção) das produções listadas. |
| **Status Produção** | Filtra por estado (Iniciado / Finalizado / Cancelado / Todos). |
| **Descrição da Loja** | Empresa onde a produção foi/será feita. |
| **Produto Acabado** | Filtra produções pelo produto final. |

### Bloco `Configuração` (define onde a produção age)

| Campo | Para quê serve |
|-------|----------------|
| **Situação Estoque** | Camada de saldo afetada pelos movimentos (geralmente `FISICO`). |
| **Local Estoque** | Local de Estoque onde os movimentos serão lançados. |
| **Tipo de Movimento — Entrada** | Tipo usado para o movimento de entrada do produto acabado no estoque. |
| **Tipo de Movimento — Saída** | Tipo usado para o movimento de saída dos ingredientes. |
| **Tipo de Movimento — Perda** | Tipo usado para o movimento de perda (só obrigatório se a fórmula tiver itens marcados como Perda). |

> ⚠️ **Acesso de suporte necessário:** os Tipos de Movimento usados aqui são configurados no `Cadastro de Tipos de Movimento` (código `37`), que requer permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de criar ou alterar Tipos de Movimento dedicados à produção.

### Bloco `Dados da Produção`

| Campo | Para quê serve |
|-------|----------------|
| **Código** | Código identificador da produção (numérico, gerado automaticamente). |
| **Descrição da Loja** | Empresa onde a produção é feita. **Obrigatória antes de escolher a Fórmula** — ao tentar aplicar a fórmula sem loja, o sistema exibe *"Selecione a Empresa para continuar"*. |
| **Início Produção** | Data/hora de início. Preenchida ao clicar em **Iniciar Produção**. |
| **Fim Produção** | Data/hora de fim. Preenchida ao clicar em **Finalizar Produção**. |
| **Data Cadastro** | Quando o registro foi criado. |
| **Status Produção** | Estado atual (`Iniciada`, `Finalizada`, `Cancelada`). Só leitura — muda pelos botões de ação. |

### Bloco `Dados do Produto Acabado`

| Campo | Para quê serve |
|-------|----------------|
| **Fórmula** | A fórmula que será executada. Dois cliques abrem a pesquisa de fórmulas (cadastradas em `Cadastro de Fórmula de Produtos`, código `143`). |
| **Produto Acabado** | Carregado da fórmula — não é editável aqui. |
| **Qtd. Produção Fórmula** | Valor de referência vindo da fórmula (`Total Produzido` do cadastro). Só leitura. |
| **UN** (ao lado de Qtd. Produção Fórmula) | Unidade de produção (do cadastro da fórmula). |
| **Qtd. Produção Real** | **Quanto será efetivamente produzido nesta rodada.** Aceita valor diferente do Qtd. Produção Fórmula — o sistema recalcula automaticamente as quantidades dos ingredientes. |
| **Qtd. Produto Acabado** | Itens do produto acabado que essa produção vai gerar. Recalculado a partir de `Qtd. Produção Real ÷ Fator` ou pode ser digitado diretamente (e o sistema ajusta a Qtd. Produção Real). |
| **UN** (ao lado de Qtd. Produto Acabado) | Unidade do produto acabado. |
| **Fator** | Fator de conversão herdado da fórmula. |

> 💡 **Quando muda a quantidade.** Se você altera `Qtd. Produção Real`, o sistema multiplica todas as quantidades de ingredientes pelo mesmo fator, mantendo a proporção da receita. Mesma coisa se você altera `Qtd. Produto Acabado` — o cálculo refaz pelo caminho inverso.

> ⚠️ **Unidade fracionável.** Se a unidade do produto acabado não permite fração (`UN`, `PEÇA`), o sistema arredonda `Qtd. Produto Acabado` para cima e ajusta `Qtd. Produção Real` correspondente, com a mensagem *"A quantidade de produto acabado deve ser um número inteiro, a unidade de medida não é fracionável"*.

---

## 🔧 Grade `Ingredientes`

A grade carrega os ingredientes da fórmula (composição + perdas) já recalculados para a `Qtd. Produção Real` digitada. Cada linha exibe:

| Coluna | O que mostra |
|--------|--------------|
| `Tipo Item` | Composição ou Perda. |
| `Produto` | O insumo consumido. |
| `Qtd.` | Quantidade já recalculada para a produção real. |
| `UN` | Unidade do ingrediente. |
| `Custo Unitário` | Custo do insumo no momento (recalculável). |
| `Custo Total` | Quantidade × custo. |

### Painel de Totais

| Campo | O que mostra |
|-------|--------------|
| **Total Qtd. Ingredientes** | Soma das quantidades dos itens de composição, quando todos estão na mesma unidade. |
| **Total Custo Ingredientes** | Soma do custo total das linhas (composição). É a base usada para apurar o **custo do produto acabado** ao finalizar a produção. |
| **Total Perdas** | Soma das quantidades das linhas marcadas como Perda. |

### Atualizar Custos

A opção **`Atualizar Todos Custos`** (clique-direito sobre a grade) força o sistema a reler o custo atual de cada ingrediente a partir do cadastro do produto. Útil quando o custo foi reajustado depois de você ter aberto a produção — antes de finalizar, atualize para garantir que o produto acabado receba o custo correto.

---

## 📦 Painel `Estoque` (lateral)

Ao selecionar um ingrediente na grade, o painel lateral mostra **em tempo real** o que está disponível para aquele insumo na loja escolhida:

| Sub-painel | O que mostra |
|-----------|--------------|
| **Estoque** | Saldo físico geral do produto. |
| **Local** | Saldo por Local de Estoque. |
| **Prateleira / Estoque Mínimo** | Posição física (corredor / prateleira) cadastrada em `Localização de Estoque` (código `29`) e estoque mínimo definido no cadastro do produto. |

É uma checagem rápida — se a produção precisa de 50 kg de farinha e o painel mostra apenas 30 kg físico, vale conferir antes de finalizar.

---

## ⚡ Botões de ação

| Botão | Quando aparece | O que faz |
|-------|----------------|-----------|
| **Iniciar Produção** | Em uma produção nova ou ainda não iniciada. | Carimba `Início Produção` e muda o Status para `Iniciada`. **Não gera movimentos** — só marca o início. |
| **Finalizar Produção** | Quando a produção está Iniciada. | Carimba `Fim Produção`, muda o Status para `Finalizada` e **gera os três movimentos** automáticos (Entrada do acabado, Saída dos ingredientes, Perda se houver). Mensagem de sucesso: *"Produção Finalizada! Todos os movimentos foram criados com sucesso."* |
| **Cancelar Produção** | Em qualquer estado anterior à finalização. | Muda o Status para `Cancelada`. Não gera nem desfaz movimentos. |

Ao clicar em **Excluir** da barra padrão, a produção é **cancelada** (Status = Cancelada) — não há exclusão física do registro.

---

## ✅ Validações automáticas ao gravar / finalizar

| Quando você grava ou avança o status | O sistema verifica |
|--------------------------------------|--------------------|
| Sempre | Não pode haver ingrediente em edição não confirmado. |
| Sempre | Os campos obrigatórios do cabeçalho estão preenchidos (Loja, Fórmula, Tipos de Movimento, Situação e Local de Estoque). |
| Sempre | A produção tem **ao menos um ingrediente**. Tentar gravar uma produção vazia é recusado. |
| Ao escolher Fórmula | A **Loja** precisa estar selecionada — caso contrário, o sistema mostra *"Selecione a Empresa para continuar"*. |
| Ao alterar a loja com itens já adicionados | A troca é recusada com *"Não é possível alterar a empresa com itens adicionados"*. Limpe os ingredientes ou cancele e recomece a produção em outra loja. |
| Ao recalcular `Qtd. Produto Acabado` | A unidade do produto acabado é fracionável? Se não, o valor é arredondado e a Qtd. Produção Real é ajustada na mesma proporção. |

---

## 💡 Exemplos práticos

### Exemplo 1 — Produção padrão pela fórmula

1. Pesquisa `F1` → `144` → abre `Cadastro de Produção de Produtos`.
2. Clique em **Novo**.
3. Preencha **Configuração**:
   - `Situação Estoque`: `FISICO`.
   - `Local Estoque`: o local destino (ex.: `LOJA`).
   - `Tipo de Movimento — Entrada`: o tipo configurado para produto acabado entrar.
   - `Tipo de Movimento — Saída`: o tipo configurado para baixa de insumo.
   - `Tipo de Movimento — Perda`: o tipo configurado para perda (deixe vazio se a fórmula não tem perdas).
4. **Dados da Produção**:
   - `Descrição da Loja`: a empresa.
5. **Dados do Produto Acabado**:
   - `Fórmula`: clique duplo → escolha a fórmula. A grade de ingredientes carrega automaticamente.
6. Confirme `Qtd. Produção Real` (ou ajuste).
7. Clique **Iniciar Produção**.
8. Quando a produção física estiver pronta, volte na tela, abra a produção pelo grid de busca e clique **Finalizar Produção**.
9. Os três movimentos são gerados e podem ser inspecionados na aba **Movimento**.

### Exemplo 2 — Ajustar quantidade real (produção parcial)

A fórmula prevê 2 kg gerando 20 unidades, mas hoje será produzido só 1 kg (10 unidades).

1. Siga os passos 1-5 do Exemplo 1.
2. Em `Qtd. Produção Real`, digite `1`.
3. O sistema recalcula automaticamente:
   - `Qtd. Produto Acabado`: `10`.
   - Quantidade de cada ingrediente na grade: metade do valor original.
4. **Iniciar Produção** → finalize quando for o caso.

### Exemplo 3 — Atualizar custos antes de finalizar

A produção foi iniciada na semana passada; o custo da matéria-prima subiu nos últimos dias.

1. Pesquisa `F1` → `144` → localize a produção em Status `Iniciada` e abra.
2. Clique-direito sobre a grade de ingredientes → **Atualizar Todos Custos**.
3. Os custos das linhas são reescritos com os valores atuais; o `Total Custo Ingredientes` é recalculado.
4. Clique **Finalizar Produção**.

O produto acabado entra no estoque com o custo calculado a partir do total atualizado — e não com o custo antigo.

### Exemplo 4 — Inspecionar os movimentos gerados

1. Abra uma produção em Status `Finalizada` pelo grid de busca.
2. Clique na aba **Movimento** — os três blocos aparecem:
   - **Movimento de Entrada do Produto Acabado**
   - **Movimento de Saída dos Ingredientes**
   - **Movimento de Perda** (se houver)
3. Para ver os movimentos na tela principal, clique-direito sobre qualquer linha → `Ir para Movimentação` — abre o `Cadastro de Movimentos` (código `53`) já filtrado nos três movimentos gerados.

---

## ❓ FAQ / Problemas comuns

**Tentei trocar a Loja e o sistema bloqueou.**
Mensagem *"Não é possível alterar a empresa com itens adicionados"* aparece porque a fórmula já foi carregada para a Loja inicial. Para mudar de loja, **cancele a produção** (Status → Cancelada) e crie outra do zero na loja correta — ou apague os ingredientes da grade primeiro.

**Finalizei a produção mas os saldos não bateram.**
Confira a configuração das Transações de Estoque dos Tipos de Movimento usados. Por exemplo, o Tipo de Movimento de Saída dos ingredientes precisa **subtrair** das camadas certas. Veja o doc de `Cadastro de Tipos de Movimento` (código `37`) e `Transações de Estoque` (código `33`).

**O custo do produto acabado ficou diferente do esperado.**
O custo do produto acabado é apurado a partir do `Total Custo Ingredientes` no momento da finalização. Se você não rodou **Atualizar Todos Custos** antes de finalizar e algum insumo teve o custo reajustado entre a abertura e a finalização, o produto acabado pode ter sido custeado com o valor antigo. Para casos retroativos, abra o produto acabado em `Cadastro de Produtos` (código `32`) e ajuste manualmente — não é possível "refinalizar" uma produção.

**A grade de ingredientes ficou vazia depois de escolher a fórmula.**
Confira se a fórmula tem ingredientes cadastrados — abra-a em `Cadastro de Fórmula de Produtos` (código `143`). Fórmulas sem ingredientes não podem ser usadas em produção.

**Posso modificar a quantidade de um ingrediente individualmente?**
Sim — mas tenha cautela: o sistema deixa editar a coluna `Qtd.` na grade. Isso quebra a proporção definida pela fórmula. Use só em casos de ajuste pontual (rendimento diferente do esperado).

**Cancelei uma produção. Posso reaproveitar?**
Não — produções canceladas ficam como histórico permanente. Crie uma nova produção do zero.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Como se relaciona |
|------|---------------|--------------------|
| `Cadastro de Fórmula de Produtos` | `143` | Fornece a receita (ingredientes + proporção + produto acabado) que esta produção executa. |
| `Cadastro de Produtos` | `32` | Cadastro do produto acabado e dos insumos. O custo do acabado é atualizado a partir do custo apurado aqui. |
| `Tipos de Movimento` | `37` | Define os três Tipos de Movimento usados na finalização (Entrada, Saída, Perda). |
| `Transações de Estoque` | `33` | Por trás dos Tipos de Movimento — define em quais camadas (FISICO, DISPONIVEL, etc.) o saldo é afetado. |
| `Locais de Estoque` | `28` | Origem do combo `Local Estoque`. |
| `Situação de Estoque` | `30` | Origem do combo `Situação Estoque`. |
| `Saldo Estoque` | `78` | Onde o efeito final da produção é visível (queda dos insumos + entrada do acabado). |
| `Movimentos` | `53` | Onde aparecem os três movimentos gerados. O atalho `Ir para Movimentação` abre direto. |

---

## ⚠️ Limites desta documentação

- Não cobre como **apurar custo médio** do produto acabado a partir dos ingredientes — o cálculo é feito automaticamente na finalização e o detalhe está no guia "Atualização de Custo Automática".
- Não detalha o que cada Tipo de Movimento precisa estar configurado para servir como Entrada/Saída/Perda — isso é assunto do `Cadastro de Tipos de Movimento` (código `37`).
- Produções **canceladas** não disparam nenhum movimento; produções **finalizadas** não podem ser "refinalizadas". Estornos exigem lançamento manual em `Cadastro de Movimentos` (código `53`).

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de Suporte / Setor de Produção / Administradores Sol.NET
