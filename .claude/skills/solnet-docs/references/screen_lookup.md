# Procedimento de Lookup de Código de Tela

Toda tela do Sol.NET tem um `ID_FORMULARIO` que o usuário digita na pesquisa F1. Antes de documentar qualquer tela, você **deve** verificar o código. Nunca invente, suponha ou reutilize um código de memória — a tabela é atualizada a cada release.

---

## Passo 1 — GitHub MCP (tentativa principal)

Tente primeiro via GitHub MCP com `get_file_contents`:

| Campo | Valor |
|-------|-------|
| `owner` | `hetosoft` |
| `repo` | `ProjetosSol.NET` |
| `path` | `Sol.NET/Dal/ProcessosAtualizacao/uProcessosAtualizacaoPrincipal.pas` |
| `ref` | `develop` |

O arquivo contém comandos `INSERT INTO FORMULARIO`. Cada linha tem o padrão:

```
VALUES (ID, ID_FORMULARIO, DESCRICAO, NAOEDITAR, NOME_FORMULARIO, PESQUISAR, HETOSOFT)
```

- **2º campo** (`ID_FORMULARIO`) = código que o usuário digita na pesquisa F1
- **3º campo** (`DESCRICAO`) = nome amigável exibido na pesquisa
- **5º campo** (`NOME_FORMULARIO`) = nome interno do formulário Delphi (não usar na doc)

Pesquise por parte do nome da tela no campo `DESCRICAO` para localizar o registro correto. A busca é exata — use o nome sem acentos ou com variações se a primeira tentativa não retornar.

Se esta chamada retornar **403**, vá para o Passo 2.

---

## Passo 2 — Fallback com PAT

Leia o arquivo `.claude\settings.local.json` na pasta do usuário atual. Procure por uma chave contendo um token GitHub (PAT). Se encontrar, use-o com o GitHub MCP ou via bash:

```bash
curl -H "Authorization: Bearer $TOKEN" \
     -H "Accept: application/vnd.github.raw" \
     "https://api.github.com/repos/hetosoft/ProjetosSol.NET/contents/Sol.NET/Dal/ProcessosAtualizacao/uProcessosAtualizacaoPrincipal.pas?ref=develop"
```

O token precisa ter permissão **`Contents: Read`** no repositório `ProjetosSol.NET`. A permissão `Metadata: Read` sozinha retorna 403.

Se o token não estiver disponível ou também retornar erro, vá para o Passo 3.

---

## Passo 3 — Perguntar ao usuário

Se ambos os passos falharem, **pare** e pergunte:

> "Não consegui acessar o repositório ProjetosSol.NET para validar o código da tela **[Nome da Tela]**. Você pode me informar o `ID_FORMULARIO` dessa tela? Ele fica no arquivo `uProcessosAtualizacaoPrincipal.pas`, na linha `INSERT INTO FORMULARIO VALUES (_, CÓDIGO, ...)` correspondente ao formulário."

**Nunca documente um código de tela sem tê-lo verificado.** Se o usuário também não souber, deixe um placeholder explícito na documentação: `[CÓDIGO A CONFIRMAR]` e liste como pendência no corpo do PR.

---

## Dicas de busca no arquivo .pas

- A tabela usa **singular**: `INSERT INTO FORMULARIO` (não `FORMULARIOS`).
- Nomes compostos aparecem como `'Lançamentos Financeiros'`, `'Receituário Agronômico'` — pesquise por parte do nome.
- Quando há múltiplas telas com nome parecido, liste todas para o usuário confirmar qual é a correta.
- O arquivo tem centenas de linhas — use `search_code` do GitHub MCP com `q=DESCRICAO+repo:hetosoft/ProjetosSol.NET` se precisar de uma busca mais rápida (lembre: busca exata, sem acentos pode ajudar).
