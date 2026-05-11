---
name: solnet-docs
description: >
  Use este skill para qualquer tarefa de documentação no repositório documentacao-solnet da Hetosoft:
  criar novos documentos, atualizar documentação existente, ou auditar conformidade de docs com as regras
  do projeto. Acione sempre que o usuário mencionar "Criar documentação", "Documentar a tela X",
  "Atualizar documentação de X", "Auditar documentação", "Revisar docs do módulo Y", ou qualquer pedido
  para escrever, editar ou verificar documentação do Sol.NET ERP. Use proativamente sempre que arquivos
  .md no documentacao-solnet precisarem ser criados ou alterados — mesmo que o usuário não diga "skill"
  explicitamente.
---

# 📚 Sol.NET Docs Skill

Este skill orquestra o ciclo completo de documentação do portal Sol.NET ERP (`hetosoft/documentacao-solnet`).

O `CLAUDE.md` na raiz do repositório é a fonte de verdade para convenções de nomenclatura, estilo e estrutura — leia-o sempre que precisar confirmar uma regra. Este skill foca no **workflow**: quais passos executar, em qual ordem, e como tomar decisões.

Para regras detalhadas de HTML do sidebar, leia `references/sidebar_patterns.md`. Para o procedimento de lookup de códigos de tela, leia `references/screen_lookup.md`.

---

## ⚠️ Telas com acesso restrito — regra obrigatória

Sempre que um documento **mencionar alterações** nas telas **`Cadastro de Empresas`** ou **`Cadastro de Tipos de Movimento`** — independentemente do modo (Criar, Atualizar ou Auditar) — inclua imediatamente após a instrução de alteração a seguinte nota de aviso:

```markdown
> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Empresas` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nesta tela.
```

Adapte o nome da tela na nota conforme o contexto (`Cadastro de Empresas` ou `Cadastro de Tipos de Movimento`).

**Onde inserir:** logo após a sentença ou passo que descreve a alteração, nunca no início ou final do documento de forma genérica. O leitor deve encontrar o aviso exatamente quando está prestes a realizar a ação.

**Quando NÃO inserir:** se o documento apenas *consulta* ou *visualiza* dados nessas telas, sem instruir o usuário a modificar nada, a nota não é necessária.

Esta regra se aplica também ao modo Auditar: se um documento existente menciona alterações nessas telas sem a nota de aviso, adicione-a automaticamente como parte da correção.

---

## 🎯 Audiência: escreva para o suporte

Todo documento criado ou editado por este skill é destinado à **equipe de suporte** — pessoas não técnicas que leem como usuários finais. O objetivo é que o suporte consiga:

- Entender uma funcionalidade sem precisar ligar para o analista
- Descobrir como usar uma ferramenta nova por conta própria
- Navegar até qualquer tela usando apenas a pesquisa F1 (nunca caminhos de menu)

Se algo confundiria um atendente de suporte que nunca viu o código-fonte, reescreva. Sem jargão técnico, sem termos Delphi, sem referências a desenvolvimento.

---

## 🔀 Identificando o modo

Leia a mensagem do usuário e classifique:

| Modo | O usuário diz algo como |
|------|-------------------------|
| **Criar** | "Criar documentação para X", "Documentar a tela X", "Novo módulo Y", "Preciso de docs sobre X" |
| **Atualizar** | "Atualizar documentação de X", "A tela X mudou", "Adicionar seção sobre Y na doc de Z" |
| **Auditar** | "Auditar documentação", "Revisar conformidade", "Verificar docs do módulo X", "Tem algo errado nas docs?" |

Se o pedido for ambíguo, pergunte antes de criar qualquer arquivo.

---

## ✨ Modo: CRIAR

### Passo 1 — Coletar entradas

Pergunte em **uma única mensagem** (não uma por vez):

1. **Módulo**: Em qual pasta? (`Financeiro/`, `Fiscal/`, `Movimentacao/`, `RH/`, `Agronomico/`, `SelfCheckout/`, ou novo)
2. **Tema**: Nome da funcionalidade ou tela (ex: "Cashback PDV", "Receituário Agronômico")
3. **Fonte do conteúdo**: De onde vem o conteúdo?
   - Descrição verbal (usuário explica no chat)
   - Issue do GitHub: peça o número da issue em `hetosoft/ProjetosSol.NET` ou `hetosoft/documentacao-solnet`
   - PRs do GitHub: peça o(s) número(s) de PR em `hetosoft/ProjetosSol.NET`
   - Combinação + imagens/screenshots que o usuário vai colar
4. **Subtema existente**: Já existem arquivos sobre esse tema na pasta do módulo? (define se é necessário criar subgrupo no sidebar)

Se o conteúdo vier de issues ou PRs, busque-os via GitHub MCP antes de continuar.

### Passo 2 — Validar códigos de tela

**Antes de escrever qualquer linha da documentação**, consulte o `ID_FORMULARIO` de cada tela que será referenciada. Veja `references/screen_lookup.md` para o procedimento exato. **Nunca invente ou suponha um código.**

### Passo 3 — Decidir estrutura de arquivos

**Módulo novo** (pasta não existe):
- Criar `<Modulo>/README.md`, `<Modulo>/documentacao_<tema>.md`, `<Modulo>/guia_rapido.md`, `<Modulo>/faq.md`
- Adicionar novo grupo no sidebar e link no portal `README.md`

**Novo tema dentro de módulo existente** (sem arquivos para este tema):
- Criar `<Modulo>/documentacao_<tema>.md`, `<Modulo>/guia_rapido_<tema>.md`, `<Modulo>/faq_<tema>.md`
- Atualizar `README.md` do módulo
- Atualizar sidebar (pode exigir subgrupo aninhado — veja `references/sidebar_patterns.md`)

**Tema existente, arquivo(s) faltando** (preencher lacuna):
- Criar apenas o(s) arquivo(s) ausentes
- Atualizar `README.md` do módulo e sidebar

Quando a granularidade for ambígua (tema que poderia ser subtópico ou módulo separado), apresente duas opções com recomendação e peça confirmação antes de criar qualquer arquivo.

### Passo 4 — Escrever os documentos

Siga a estrutura do `CLAUDE.md` (`## Document Style`):

```
# 📄 [Título] - Sol.NET

## 🎯 Visão Geral
[Descrição clara do propósito — o que é, para que serve]

### Principais Características:
- ✅ Característica 1
- ✅ Característica 2

---

## 🔧 [Seções Funcionais]
[Conteúdo detalhado — como usar, passo a passo]

---

## 💡 Exemplos Práticos
[Cenários reais que o suporte encontraria no dia a dia]

---

## ❓ FAQ / Problemas Comuns
[Mínimo 5 perguntas, organizadas por categoria se >8]

---

**Última atualização**: [Mês de Ano]
**Versão**: [X.X]
**Público-alvo**: [Usuários do Sol.NET / Equipe de Suporte / Administradores]
```

**Versionamento**: Novos documentos começam em `1.0`. Sempre informe a versão sugerida e peça confirmação ao usuário antes de commitar.

**Guia Rápido**: formato de checklist — o que clicar, o que confirmar, em qual ordem. Pense nele como um cartão de referência que o suporte consulta durante o atendimento.

**FAQ**: mínimo 5 perguntas. Para >8, organize por categoria com cabeçalho `### Categoria`. Formato de cada entrada:

```markdown
### ❓ Pergunta que o usuário realmente faria?

Resposta prática e direta. Se há mais de um passo, use lista numerada.
```

### Passo 5 — Atualizar infraestrutura

Após escrever os documentos, **sempre** atualize:

1. **`README.md` do módulo**: Adicione links para os novos arquivos no índice existente.
2. **Portal `README.md`** (raiz): Se for módulo novo ou adição significativa, adicione referência.
3. **Sidebar** (`_layouts/default.html`): Adicione as entradas. Consulte `references/sidebar_patterns.md` para os padrões HTML exatos, incluindo como criar subgrupo aninhado quando um tema tem mais de 2 arquivos.

### Passo 6 — Commit e PR

Crie uma branch com nome `docs/<nome-do-tema>` (letras minúsculas, hífens, apenas ASCII, sem acentos).

Exemplo: tema "Cashback PDV" → branch `docs/cashback-pdv`.

Commit de todos os arquivos em um único commit com mensagem em português:
```
docs: cria documentação de [tema] no módulo [Módulo]
```

Abra PR de `docs/<nome-do-tema>` → `main` em `hetosoft/documentacao-solnet`. Título e corpo do PR em português. O corpo deve listar:
- O que foi criado (lista de arquivos)
- Códigos de tela referenciados
- Fontes usadas (números de PR/issue, se aplicável)

---

## ✏️ Modo: ATUALIZAR

### Passo 1 — Identificar escopo

Pergunte:
1. Qual(is) arquivo(s) precisam de atualização?
2. O que mudou? (descrição verbal, número(s) de PR, número(s) de issue)

Busque o conteúdo do GitHub via MCP se forem fornecidos números de PR ou issue.

### Passo 2 — Validar novas referências de tela

Se a atualização introduz telas novas, valide seus códigos (veja `references/screen_lookup.md`).

### Passo 3 — Aplicar mudanças

- Adicione às seções existentes em vez de criar seções paralelas
- Preserve o vocabulário de emojis e a formatação do arquivo existente
- Atualize o rodapé de metadados:
  - `**Última atualização**`: mês e ano atual
  - `**Versão**`: incremente o número menor (ex: `1.0` → `1.1`). Para reestruturações maiores, incremente o maior (`1.x` → `2.0`). Informe a versão sugerida e peça confirmação.

### Passo 4 — Commit e PR

Branch: `docs/<nome-do-tema>` (mesma convenção do modo Criar).

Commit:
```
docs: atualiza documentação de [tema] no módulo [Módulo]
```

PR → `main`. Descreva o que mudou e por quê, referenciando o PR/issue de origem se houver.

---

## 🔍 Modo: AUDITAR

### Passo 1 — Definir escopo

Se o usuário especificou um módulo ou arquivo, audite apenas aquele. Caso contrário, audite o repositório inteiro.

### Passo 2 — Verificar cada arquivo contra estas regras

Para cada arquivo `.md` (pule `CLAUDE.md`, `README.md` raiz, `teste_mermaid.md`):

| Regra | O que verificar |
|-------|-----------------|
| Sem caminhos de menu | Nenhum texto com padrão `Menu >` ou `> Submenu` |
| Referências de tela | Toda tela mencionada inclui código (`código NNN` ou `(código NNN)`) |
| Atalhos de teclado | Somente `F1` é permitido sem validação; qualquer outro (`F4`, `F5`, `Ctrl+X`) é violação |
| Nomenclatura de arquivos | Todos os `.md` são snake_case, apenas ASCII |
| Links internos | Sem `%20` em links relativos |
| Estrutura de emoji | Documento abre com `# 📄`, tem `## 🎯 Visão Geral`, termina com rodapé de metadados |
| Idioma | Sem inglês, espanhol ou jargão de desenvolvimento |
| Público-alvo | Sem referências ao código-fonte, termos Delphi, ou detalhes de implementação |
| Nota de acesso restrito | Toda instrução de alteração em `Cadastro de Empresas` ou `Cadastro de Tipos de Movimento` tem a nota de aviso de acesso de suporte imediatamente após |

### Passo 3 — Corrigir e documentar

Corrija todos os problemas encontrados. Para cada correção, registre uma linha explicando o que foi alterado e por quê — isso vira o corpo do PR.

Para atalhos não validados: remova o atalho e substitua pelo padrão genérico do `CLAUDE.md`:
- *"Acesse a tela `X` (código `NNN` na pesquisa F1)"*
- *"Use o botão equivalente na tela"*

### Passo 4 — Commit e PR

Branch: `docs/auditoria-<modulo>` (ou `docs/auditoria-geral` para o repositório inteiro).

Commit:
```
docs: correções de conformidade — auditoria [módulo/geral]
```

PR → `main`. Corpo: tabela com cada problema encontrado e como foi corrigido.

---

## 📁 Arquivos de referência

Leia estes arquivos quando precisar de detalhes específicos:

- **`references/screen_lookup.md`** — Procedimento exato para buscar códigos de tela via GitHub MCP, incluindo fallback de PAT e o que fazer quando o acesso falha
- **`references/sidebar_patterns.md`** — Padrões HTML do sidebar: itens simples, grupos de primeiro nível, subgrupos aninhados com CSS para quando um tema tem >2 arquivos
