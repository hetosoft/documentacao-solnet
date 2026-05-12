# 📄 Cadastro de Locais de Estoque - Sol.NET

## 🎯 Visão Geral

**Local de Estoque** é a divisão interna onde o produto fica fisicamente armazenado dentro de uma empresa — por exemplo `LOJA`, `DEPÓSITO`, `GALPÃO 1`, `FILIAL CENTRO`. Cada movimento de estoque (entrada, saída, ajuste, transferência, produção) é gravado **com a indicação do Local** afetado, o que permite saber **onde** está cada unidade do produto, não apenas quanto há no total.

Um e apenas um dos locais é marcado como **Principal**: ele é o destino padrão de operações que não especificam Local — por exemplo, lançamentos via mobile ou e-commerce que não trazem essa informação. Quando você lança um movimento manualmente, o sistema sugere o Local Principal e permite trocar.

> ℹ️ **Acesso restrito.** Esta é uma tela operada normalmente pela **equipe de suporte / administração**. Usuários comuns não têm permissão para alterar Locais de Estoque, e mudanças aqui afetam a leitura de todo o histórico de movimentação. Solicite ao suporte Hetosoft antes de criar ou inativar locais.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Locais de Estoque |
| **Código (`F1`)** | `28` |

Abra a pesquisa universal (atalho `F1`) e digite **`28`** ou parte do nome **`Locais de Estoque`**.

---

## 📝 Campos

| Campo | Para quê serve |
|-------|----------------|
| **Descrição** | Nome do local (até 80 caracteres, gravado em maiúsculas). Use nomes que o operador reconheça sem dúvida: `LOJA`, `DEPÓSITO`, `FILIAL CENTRO`. |
| **Principal** | Marca o local como destino padrão de operações que não especificam um Local. Apenas **um** local deve ficar como Principal. |
| **Inativo** | Quando marcado, o local some das telas que oferecem escolha (lançamento de movimento, ajuste de estoque, transferência). O **histórico** continua mostrando o local inativado nos movimentos antigos. |

---

## ✅ Validações automáticas ao salvar

| Quando você grava | O sistema verifica |
|-------------------|--------------------|
| Sempre | A `Descrição` precisa estar preenchida. |
| Ao marcar `Inativo` | É preciso existir **pelo menos um outro local ativo**. Inativar o último local ativo é bloqueado com a mensagem *"Não Permitido! Obrigatório pelo menos um Ativo."*. |

A duplicidade de `Descrição` **não** é validada — o sistema permite cadastrar dois locais com o mesmo nome. Use nomes distintos para evitar confusão.

---

## 🚫 Exclusão

A exclusão é bloqueada se o local já foi referenciado em outras partes do sistema:

- ❌ **Algum Tipo de Movimento configurou este local como origem/destino padrão** — mensagem *"Existe Tipo de Movimento com esse Local de Estoque!"*. Resolva trocando o local no `Cadastro de Tipos de Movimento` (código `37`) antes de tentar excluir.

  > ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Tipos de Movimento` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nesta tela.

- ❌ **Há movimentos no histórico de estoque com este local** — mensagem *"Existe Movimentação de Estoque com esse Local de Estoque!"*. Locais que já receberam qualquer movimento **não** podem ser excluídos. Para tirá-los de uso, marque como **Inativo** em vez de tentar excluir.

---

## 💡 Exemplos práticos

### Exemplo 1 — Criar um novo Depósito

1. Pesquisa `F1` → `28` → abre `Cadastro de Locais de Estoque`.
2. Clique em **Novo**.
3. `Descrição`: `DEPÓSITO`.
4. Deixe **Principal** desmarcado (já existe um Principal cadastrado — `LOJA`).
5. **Gravar**.

A partir deste momento, ao lançar uma entrada ou ajuste de estoque, o operador passa a ver o novo local no combo de escolha.

### Exemplo 2 — Trocar qual local é o Principal

1. Pesquisa `F1` → `28`.
2. Localize na lista o local **atualmente** Principal (ex.: `LOJA`). Abra, desmarque **Principal**, **Gravar**.
3. Localize o novo local que será o Principal (ex.: `DEPÓSITO`). Abra, marque **Principal**, **Gravar**.

> A partir daí, lançamentos automáticos (mobile, e-commerce, integrações) que não informam Local passam a usar o novo Principal.

### Exemplo 3 — Aposentar um local antigo sem perder o histórico

1. Pesquisa `F1` → `28`. Localize o local a aposentar (ex.: `GALPÃO ANTIGO`).
2. Abra o cadastro, marque **Inativo**, **Gravar**.
3. Confira que ainda há ao menos um outro local ativo — caso contrário, a gravação é recusada.

O local **continua** aparecendo nos relatórios e no histórico, mas não é mais oferecido em novas operações.

---

## ❓ FAQ / Problemas comuns

**Posso ter mais de um local marcado como Principal?**
Operacionalmente, **não** — só faz sentido um. A tela não bloqueia a marcação de dois, mas o sistema usa apenas o primeiro Principal encontrado para preencher automaticamente os campos. Mantenha exatamente um.

**Inativei o local errado e agora não consigo desativar o novo. O que aconteceu?**
A regra exige pelo menos um local ativo. Se você inativou o único ativo, abra-o, desmarque **Inativo** e grave de novo — depois faça a alteração correta.

**Por que o local que eu acabei de criar não aparece no `Tipo de Movimento`?**
O combo de Local no `Cadastro de Tipos de Movimento` (código `37`) carrega apenas locais **ativos**. Confirme que o `Inativo` está desmarcado. Se ainda não aparecer, feche e reabra o `Tipo de Movimento`.

**Posso ter um local diferente em cada empresa?**
Sim — o vínculo de Local × Empresa é feito no `Cadastro de Tipos de Movimento` (sub-aba `Local Estoque por Empresa`), não nesta tela. Aqui você só cadastra o **catálogo** geral de Locais.

**Excluí o local errado por engano. Como recuperar?**
Se o local nunca foi usado, a exclusão é definitiva e basta recriá-lo (o histórico não tem o que recuperar). Se ele já tinha movimentos, a exclusão **foi bloqueada** pelo próprio sistema — o cadastro continua intacto.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Como se relaciona |
|------|---------------|--------------------|
| `Tipos de Movimento` | `37` | Cada Tipo de Movimento define qual Local é a **origem** e qual o **destino** padrão da operação. |
| `Movimentos de Compras` | `201` | Cada movimento de compra carrega o Local de Estoque afetado. |
| `Movimentos de Vendas` | `202` | Cada venda carrega o Local de Estoque afetado. |
| `Outros Movimentos` | `203` | Demais movimentos (transferências, ajustes via Tipos de Movimento) também carregam o Local. |
| `Saldo Estoque` | `78` | Consulta o saldo do produto **por Local** — é onde a separação faz diferença. |
| `Ajuste de Estoque` | `79` | O ajuste manual de saldo é feito **dentro de um Local** específico. |
| `Histórico de Movimentações` | `205` | Lista todos os movimentos por Local, inclusive de Locais já inativados. |

---

## ⚠️ Limites desta documentação

- Não cobre a configuração de **Local × Empresa** (em qual empresa cada local está disponível) — isso fica no `Cadastro de Tipos de Movimento`.
- Não trata regras de **rastreabilidade interna** (corredor, prateleira, posição) — essa granularidade fica na tela `Localização de Estoque` (código `29`), que será documentada em parte.
- Operações que **transferem** saldo entre locais usam Tipos de Movimento específicos (geralmente um par "saída do local A" + "entrada no local B"), configurados em `Tipos de Movimento`, fora do escopo desta tela.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de Suporte / Administradores Sol.NET
