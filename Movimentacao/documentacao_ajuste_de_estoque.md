# 📄 Cadastro de Ajuste de Estoque - Sol.NET

## 🎯 Visão Geral

O **Ajuste de Estoque** é a ferramenta de **inventário e correção de saldo** do Sol.NET. Você cadastra uma lista de produtos com a **contagem real** medida na loja, o sistema mostra o **saldo atual** registrado no banco e calcula automaticamente a **diferença** entre os dois. Ao acionar **Criar Ajustes**, o Sol.NET gera os movimentos de estoque necessários para que o saldo registrado passe a refletir a contagem — entrada para diferença positiva, saída para diferença negativa, usando os Tipos de Movimento configurados no próprio ajuste.

O ajuste é controlado por **Status**: começa em `ABERTO` (livre para edição) e, depois de gerar os movimentos, fica vinculado a eles e bloqueia novas alterações. É o jeito padronizado, auditável e reversível de corrigir saldo no Sol.NET — em vez de mexer direto no estoque.

> ℹ️ **Quando usar.** Inventário periódico (mensal, trimestral, anual), inventário rotativo, correção pontual após uma divergência, conciliação pós-importação de dados, regularização depois de uma operação não registrada (ex.: doação, perda fora do fluxo normal).

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Ajuste de Estoque |
| **Código (`F1`)** | `79` |

Abra a pesquisa universal (atalho `F1`) e digite **`79`** ou parte do nome **`Ajuste de Estoque`**.

---

## 📝 Campos do cabeçalho

### Filtros da consulta (lista de ajustes)

| Filtro | O que faz |
|--------|-----------|
| **Status** | Filtra por estado (`ABERTO`, ajustes que ainda geram movimentos vs `FECHADO`/`PROCESSADO` com movimentos já criados). |
| **Inicial / Final** | Data do ajuste. |
| **Descrição da Loja** | Empresa do ajuste. |

### Bloco `Comportamentos`

Define como o ajuste se comporta na **inclusão de produtos**. Esses parâmetros valem para o ajuste em edição.

| Campo | Para quê serve |
|-------|----------------|
| **Entrada Saldo** | Define a regra de inclusão automática do saldo atual quando um produto é adicionado. |
| **Modo Adicionar Itens** | Como o produto é incluído (um por um pela tela, em lote por seleção do popup, por leitura de código de barras). |
| **Pesquisar só por** | Qual atributo o sistema usa para localizar o produto (Código, Descrição, Código de Barra, Referência). |
| **Avisa Se Já Inserido** | Quando marcado, avisa se você tentar inserir o mesmo produto duas vezes no ajuste. |

### Dados do ajuste (aba `Principal`)

| Campo | Para quê serve |
|-------|----------------|
| **Descrição** | Nome livre do ajuste (`INVENTÁRIO MENSAL — OUT/2025`, `CORREÇÃO RÁPIDA SEÇÃO BEBIDAS`). |
| **Data** | Data do ajuste (geralmente a data da contagem física). |
| **Status** | Estado atual (`ABERTO`, etc.). Edição só com status `ABERTO`. |
| **Descrição da Loja** | Empresa em que o ajuste é feito. |
| **Local de Estoque** | Local físico do saldo a corrigir (`LOJA`, `DEPÓSITO`). |
| **Situação do Estoque** | Camada de saldo afetada (geralmente `FISICO`). |
| **Tipo de Movimento — Saída** | Tipo usado para gerar os movimentos de saída quando a diferença é negativa (contagem < saldo atual). |
| **Tipo de Movimento — Entrada** | Tipo usado para gerar os movimentos de entrada quando a diferença é positiva (contagem > saldo atual). |

> ⚠️ **Acesso de suporte necessário:** os Tipos de Movimento usados como Entrada e Saída do ajuste vêm do `Cadastro de Tipos de Movimento` (código `37`), que requer permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de criar ou alterar Tipos de Movimento dedicados a ajustes de estoque.

---

## 🔧 Grade de Produtos do Ajuste

A grade central recebe **um produto por linha** com colunas:

| Coluna | O que mostra |
|--------|--------------|
| **Descrição** | Nome do produto. |
| **Marca / Fabricante** | Marca cadastrada no produto. |
| **Unid.** | Unidade de medida do produto. |
| **Saldo Atual** | Saldo registrado no banco no momento da inclusão. |
| **Contagem** | Quanto foi **medido fisicamente** na contagem (você digita). |
| **Diferença** | `Contagem - Saldo Atual` — calculada pelo sistema. Positiva → entrada; negativa → saída. |

### Botões da grade

| Botão | O que faz |
|-------|-----------|
| **Inserir** | Adiciona um produto à lista (abre pesquisa para localizar). |
| **Atualizar** | Salva as alterações da linha em edição. |
| **Deletar** | Remove a linha selecionada. |
| **Cancelar** | Cancela a inclusão/edição em andamento. |
| **Deletar Todos** | Apaga todos os produtos do ajuste. |

> 💡 **Adicionar em lote.** Use o menu de contexto da grade → **Adicionar Produtos** (atalho do popup) para abrir uma pesquisa e marcar vários produtos de uma vez. Combina com a opção **Selecionar Todos** para inventariar uma família ou grupo inteiro.

### Painel `Estoque` (lateral / inferior)

Ao selecionar uma linha, o painel lateral mostra o estoque **detalhado** daquele produto em sub-abas:

| Sub-aba | O que mostra |
|---------|--------------|
| **Estoque** | Saldo físico geral do produto. |
| **Local** | Saldo por Local de Estoque. |
| **Prateleira** | Posição cadastrada em `Localização de Estoque` (código `29`). |
| **Códigos** | Códigos de barras alternativos cadastrados para o produto. |

---

## ⚡ Ação `Criar Ajustes`

Quando todos os produtos estão com `Contagem` preenchida e a `Diferença` correta, o botão **Criar Ajustes** processa o ajuste:

1. Para cada linha com `Diferença ≠ 0`, o sistema gera um **movimento de estoque** usando o Tipo de Movimento adequado (Entrada se positiva, Saída se negativa).
2. Os movimentos ficam vinculados ao ajuste (campo `ID_AJUSTE_SALDO` em `MOVIMENTOS`).
3. O Status do ajuste muda do `ABERTO` para um estado processado, bloqueando alterações posteriores.
4. A aba **Movimentos** mostra os movimentos gerados para inspeção.

> ℹ️ **Linhas com Diferença = 0.** Linhas em que a contagem confirmou o saldo (diferença zero) **não geram movimento** — ficam apenas como registro do que foi conferido.

---

## ✅ Validações automáticas

### Ao gravar / processar

| Quando | O sistema verifica |
|--------|--------------------|
| Sempre | Não pode haver linha em edição não confirmada. |
| Sempre | Campos obrigatórios do cabeçalho preenchidos (Loja, Local, Situação, Tipos de Movimento). |
| Ao criar ajustes | A grade não pode estar vazia — *"Ajuste de Estoque sem Produtos!"*. |
| Ao adicionar / editar produto | O ajuste precisa estar com Status `ABERTO` — *"Não Permitido! Só Status Aberto."*. |
| Ao adicionar produto | O produto **não pode estar marcado como `Não Movimentar Estoque`** no `Cadastro de Produtos` (código `32`) — *"Produto Configurado para 'Não Movimentar Estoque'!"*. |
| Contagem | Não pode exceder `999.999,99` — *"Não Permitido, Quantidade Máxima Excedida (999.999,99)!"*. |

### Ao excluir um ajuste

| Cenário | Resultado |
|---------|-----------|
| Status diferente de `ABERTO` | Excluir é bloqueado — *"Só com Status 'ABERTO'"*. |
| Há movimentos vinculados ao ajuste | Bloqueado — *"Não permitido, Existe Movimento(s) Vinculado!"*. Para reverter um ajuste já processado, lance um novo ajuste com a contagem invertida em vez de tentar excluir o original. |

---

## 💡 Exemplos práticos

### Exemplo 1 — Inventário mensal de uma loja

1. Pesquisa `F1` → `79` → abre `Cadastro de Ajuste de Estoque`.
2. Clique em **Novo**.
3. Cabeçalho:
   - `Descrição`: `INVENTÁRIO OUT/2025 — LOJA CENTRAL`.
   - `Data`: data da contagem.
   - `Descrição da Loja`: a empresa.
   - `Local de Estoque`: `LOJA`.
   - `Situação do Estoque`: `FISICO`.
   - `Tipo de Movimento — Saída`: o tipo configurado para ajuste negativo.
   - `Tipo de Movimento — Entrada`: o tipo configurado para ajuste positivo.
4. Clique no menu de contexto da grade → **Adicionar Produtos** → marque todos os produtos da loja → confirme.
5. Faça a contagem física (manual, com coletor, com inventariante).
6. Para cada linha, digite o valor medido na coluna **Contagem** — a `Diferença` é calculada automaticamente.
7. Quando terminar, clique **Criar Ajustes**.
8. Confira na aba **Movimentos** quais movimentos foram gerados.

### Exemplo 2 — Inventário rotativo (correção pontual de uma seção)

1. Pesquisa `F1` → `79` → **Novo**.
2. Preencha o cabeçalho como no Exemplo 1, alterando a descrição para refletir a seção (ex.: `INVENTÁRIO BEBIDAS — SEMANA 42`).
3. Menu de contexto da grade → **Adicionar Produtos** → filtre por grupo `BEBIDAS` → **Selecionar Todos**.
4. Faça a contagem, preencha `Contagem` em cada linha.
5. **Criar Ajustes**.

### Exemplo 3 — Correção rápida de um único produto

1. Pesquisa `F1` → `79` → **Novo**.
2. Cabeçalho com `Descrição` curta (`AJUSTE PONTUAL — PRODUTO X`).
3. **Inserir** → busque o produto.
4. Digite a contagem real → **Atualizar**.
5. **Criar Ajustes**.

---

## ❓ FAQ / Problemas comuns

**Lancei a contagem mas o sistema avisa "Produto Configurado para 'Não Movimentar Estoque'!".**
O produto está marcado para não movimentar estoque no cadastro (`Cadastro de Produtos` — código `32`, aba de configurações de estoque). Ajuste de saldo só faz sentido em produtos que movimentam estoque. Se o produto deve passar a movimentar, ajuste o cadastro primeiro; se não deve, ele não deveria estar no inventário.

**Errei a contagem e o ajuste já foi processado. Como corrijo?**
Você **não pode excluir** ou reabrir o ajuste — ele já gerou movimentos. A maneira correta é criar **um novo ajuste** com a contagem corrigida (a `Diferença` vai compensar o erro anterior) ou, em casos pontuais, lançar um movimento direto de correção no `Cadastro de Movimentos` (código `53`) com a justificativa.

**A diferença ficou enorme e desconfio que o saldo no banco estava errado antes da contagem.**
É exatamente o caso de uso de inventário — o ajuste **vai corrigir** o saldo para refletir o real medido. Confira só se algum produto não estava com o saldo zerado por engano antes (por exemplo, um produto novo que ainda não tinha entrada cadastrada). Para esses, lance a entrada normal antes de aplicar o ajuste.

**Posso inventariar produtos com saldo zero (nunca movimentados)?**
Sim, basta adicionar o produto, deixar `Contagem` com o valor real (ex.: `5`) e processar — o sistema gera o movimento de entrada com a diferença.

**Quem gera os relatórios de divergência?**
Use o botão de **Relatório** da tela ou pelo `Histórico de Movimentações` (código `205`) filtrando pelos Tipos de Movimento usados como entrada/saída do ajuste.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Como se relaciona |
|------|---------------|--------------------|
| `Cadastro de Produtos` | `32` | Origem dos produtos do ajuste; o flag `Não Movimentar Estoque` bloqueia inclusão aqui. |
| `Tipos de Movimento` | `37` | Define os tipos usados como Entrada e Saída do ajuste. |
| `Locais de Estoque` | `28` | Origem do combo `Local de Estoque`. |
| `Situação de Estoque` | `30` | Origem do combo `Situação do Estoque`. |
| `Cadastro de Movimentos` | `53` | Destino — onde aparecem os movimentos gerados pelo ajuste. |
| `Saldo Estoque` | `78` | Onde o efeito final do ajuste é visível. |
| `Localização de Estoque` | `29` | Fornece a coluna `Prateleira` do painel de estoque do produto selecionado. |

---

## ⚠️ Limites desta documentação

- Não cobre o uso de **coletores de inventário** (handhelds, código de barras móveis) — esse fluxo existe e alimenta esta tela, mas é assunto de integração específica.
- Não detalha a configuração de **custo** dos movimentos gerados — entrada por ajuste pode ou não atualizar custo médio conforme configurado no Tipo de Movimento (ver guia "Atualização de Custo Automática").
- Ajustes processados não podem ser revertidos pela própria tela; reversões exigem um novo ajuste contrário ou lançamento manual.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de Suporte / Operação de Estoque / Administradores Sol.NET
