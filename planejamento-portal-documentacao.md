# Planejamento — Portal de Documentação Sol.NET

## Visão geral

Portal de conhecimento do Sol.NET em Blazor SSR (.NET 10), com conteúdo em Markdown versionado no Git, busca semântica, chatbot IA e área interna autenticada. Construído em fases incrementais, cada uma entregando valor independente.

**Stack definida**

| Camada | Tecnologia | Observação |
|---|---|---|
| Frontend/Backend | Blazor SSR (.NET 10) | |
| Componentes UI | MudBlazor | Material Design — navegação, busca, chat, cards, avaliações |
| Conteúdo | Arquivos `.md` no repositório | Mesmo fluxo Git atual |
| Vetores / busca semântica | Azure Cosmos DB for NoSQL (free tier) | 400 RU/s + 5 GB — vetores persistidos entre restarts |
| Autenticação | SQLite + ASP.NET Core Identity | Permanece SQLite; não migra para Azure SQL |
| Analytics e dados relacionais | SQLite | Volume interno não justifica Azure SQL |
| IA | Gemini API (free tier) | Embeddings via `text-embedding-004` (768 dimensões) |
| Hospedagem | Azure App Service (B1) | |
| Observabilidade | Azure Application Insights | |

---

## Arquitetura de conteúdo do repositório

- Repositório privado único na organização `hetosoft`, com pastas separadas `/public/` e `/internal/`. A fonte do conteúdo não fica pública.
- Cada `.md` aceita front matter com: `title`, `permalink`, `nav_label`, `order`, `audience: [public|internal]`, `type: [page|trilha|indice|glossario|visao_geral]`, `tags`.
- Navegação principal: arquivo `nav.yaml` na raiz do repo, curado editorialmente. O portal lê o arquivo no build — mantém o controle de ordem, agrupamento e labels customizadas que hoje existe na sidebar do Jekyll.
- Conteúdo de header (entry points): `quero.md`, `glossario.md` e `visao_geral_sol_net.md` ficam acessíveis pela barra superior do portal, não pela sidebar de módulo.
- `llms.txt` é gerado pelo build a partir da árvore + front matter — não é editado à mão.
- Trilhas (`Movimentacao/Trilhas/`) ficam como páginas normais com `type: trilha` no front matter; a estilização específica (numeração, próximo/anterior) entra apenas na fase 5.
- `indice_mensagens.md` é indexado normalmente para busca/RAG — é referência crítica para suporte.

---

## Arquitetura de embeddings (decisão consolidada)

A aplicação **nunca gera embeddings em runtime**. A geração é responsabilidade exclusiva do pipeline CI/CD:

1. Desenvolvedor edita um `.md` e faz push para `main`.
2. O GitHub Actions detecta, via `git diff`, quais arquivos `.md` mudaram no commit.
3. Para cada arquivo alterado, divide o conteúdo em chunks por cabeçalho `##` (H2):
   - Seções < 80 tokens são fundidas com a próxima.
   - Seções > 1500 tokens são divididas por `###` (H3) até caberem.
   - Cada chunk recebe hash de conteúdo; só chunks com hash novo (ou inexistente no Cosmos DB) vão para a API Gemini.
4. Chama a Gemini Embeddings API (`text-embedding-004`) apenas para chunks novos ou alterados.
5. Faz upsert dos vetores no Cosmos DB. Document ID = `{caminho-do-arquivo}#{slug-do-H2}`. Metadata inclui: `audience`, `type`, `module`, `title_section`, `title_page`, `last_commit_sha`, `content_hash`.
6. A aplicação, ao receber uma query de busca ou do chatbot, lê os vetores do Cosmos DB e calcula a similaridade — sem nenhuma chamada de geração.

Benefícios: cold starts rápidos, sem consumo de cota Gemini em produção, atualização incremental (apenas as seções que mudaram são re-processadas), e respostas do chatbot citam a seção exata em vez do arquivo inteiro.

**Configuração do container Cosmos DB:**
- Modelo: `text-embedding-004` → 768 dimensões
- Função de distância: cosseno
- Tipo de índice: flat (adequado para o volume atual; revisar para HNSW se o corpus ultrapassar ~5.000 chunks)
- Particionamento por `module` (Financeiro, Fiscal, Movimentacao, etc.) para distribuir custo de RU/s.
- TTL não é usado — o pipeline apaga document IDs órfãos (arquivos ou seções removidos no commit).

---

## URLs e migração do site atual

- O esquema de URL do novo portal é decisão isolada do início da fase 1.1 (não bloqueia o restante).
- **Sem redirect 301 do GitHub Pages.** O go-live do portal Blazor encerra o site Jekyll; links externos para `hetosoft.github.io/documentacao-solnet/...` quebram intencionalmente.
- Comunicação prévia (canais Hetosoft, notas de release, banner no site atual nas semanas anteriores) é responsabilidade do time de produto, fora do escopo técnico deste plano.

---

## Fase 1 — Fundação pública + Busca + Chatbot

**Objetivo:** portal público funcional, com o conteúdo atual migrado e os dois recursos mais importantes no ar.

### 1.1 Projeto base Blazor SSR

- Criar projeto Blazor SSR (.NET 10) com MudBlazor configurado
- Configurar pipeline CI/CD (GitHub Actions → Azure App Service)
- Definir estrutura de pastas para os arquivos Markdown (espelhando os módulos do Sol.NET)
- Migrar os Markdowns existentes do repositório atual para o novo projeto
- Implementar leitura e renderização dos arquivos `.md` em tempo de execução
- Suporte a diagramas Mermaid via `PSC.Blazor.Components.MarkdownEditor` 10.0.9 (publicado em 14/05/2026, target framework `net10.0`). A funcionalidade Mermaid do autor PSC vem embutida nesse pacote — o `PSC.Blazor.Components.Mermaid` standalone citado em rascunhos anteriores não existe no NuGet.
- **Critério de aceitação técnica da fase 1.1**: renderizar com sucesso pelo menos um diagrama complexo do portal atual (ex.: o `flowchart` de `Movimentacao/README.md`) antes de fechar a fase.
- Navegação lateral por módulo com hierarquia (módulo > seção > página)
- Breadcrumbs de navegação
- Layout responsivo (desktop e mobile)

### 1.2 Busca semântica

- Configurar container no Cosmos DB (free tier) com suporte a vector search
- Implementar pipeline CI/CD de embedding: detecta arquivos `.md` alterados → chama Gemini → upsert no Cosmos DB
- Implementar campo de busca global no header
- Ao buscar: gera embedding da query via Gemini → consulta Cosmos DB → retorna páginas rankeadas por similaridade cosseno
- Página de resultados com título, trecho relevante e link para a página completa

### 1.3 Chatbot RAG

- Interface de chat flutuante (botão no canto da tela)
- Fluxo da pergunta: embed a query → recupera chunks relevantes do Cosmos DB → monta prompt com contexto → Gemini gera resposta → exibe com link para a página de origem
- Suporte a perguntas de acompanhamento (histórico da conversa no contexto)
- Modo guiado: se a pergunta for vaga ("como faço para fechar o mês?"), o bot faz perguntas de refinamento antes de responder

**Critério de conclusão da fase 1:** qualquer usuário consegue navegar por módulo, buscar por termos em linguagem natural e conversar com o chatbot sem precisar de login.

---

## Fase 2 — Área interna autenticada

**Objetivo:** time de suporte e implantação acessa conteúdo restrito no mesmo portal.

### 2.1 Autenticação

- ASP.NET Core Identity + SQLite mantêm sessão local (cookie do portal), mas a validação de credencial é delegada à **API Hetosoft existente**.
- Fluxo: usuário envia login/senha no portal → portal chama a API Hetosoft → API retorna `200 OK` (válido) ou `401` (inválido) → no primeiro login bem-sucedido o portal cria registro local no SQLite (sem senha).
- Roles (`suporte`, `implantacao`, `dev`, etc.) ficam **apenas no SQLite local** do portal, atribuídos por painel admin. A API Hetosoft retorna apenas booleano — não retorna roles nem perfil.
- Tela de login (usuário e senha) com mensagens genéricas para falha.
- Painel admin simples para listar/desativar usuários e atribuir roles.
- Proteção de rotas com `[Authorize]`.
- **Pendência rastreada**: contrato e endpoint da API Hetosoft de validação precisam estar confirmados antes do início da fase 2 (ver "Decisões pendentes").

### 2.2 Conteúdo interno

- Conteúdo interno fica em `/internal/` no mesmo repo privado, ao lado de `/public/`.
- Front matter `audience: internal` é checado em runtime; rotas correspondentes são protegidas por `[Authorize]`.
- Conteúdo inicial: procedimentos de implantação, scripts e queries de suporte, documentação técnica de integrações.
- Pipeline de embedding marca os vetores com `metadata.audience = "internal"`; queries de usuário não autenticado filtram `audience = "public"` para nunca retornar resultado interno.
- Navegação lateral própria para a área interna, controlada por uma seção dedicada do `nav.yaml`, visível apenas após login.

### 2.3 Chatbot interno

- Ao autenticar, o contexto do RAG inclui também os documentos internos (consulta Cosmos DB sem filtro de `interno`)
- O chatbot do usuário autenticado responde com base em todo o conteúdo (público + interno)

**Critério de conclusão da fase 2:** usuário interno acessa o portal com login, navega pelos procedimentos e consulta o chatbot com acesso ao conteúdo completo.

---

## Fase 3 — Interação dos usuários + Integração com suporte

**Objetivo:** usuários finais podem dar feedback nas páginas; feedback problemático vira chamado automaticamente.

### 3.1 Avaliação de páginas

- Botão "Esta página foi útil?" no rodapé de cada artigo (👍 / 👎)
- Avaliações registradas no SQLite com a página de origem (volume não justifica banco externo)

### 3.2 Comentários

- Caixa de comentário ao final de cada página (sem login obrigatório)
- Moderação simples: comentários ficam visíveis após aprovação (painel interno)

### 3.3 Reporte de erros

- Botão "Reportar problema nesta página"
- Formulário simples: descrição do problema + campo opcional de contato
- Ao submeter: cria chamado via API do sistema de suporte da Hetosoft
- Fallback: se a API estiver indisponível, abre Issue no GitHub

**Critério de conclusão da fase 3:** um cliente encontra um erro na documentação, reporta pelo portal e o chamado aparece no sistema de suporte sem intervenção manual.

---

## Fase 4 — Analytics

**Objetivo:** dados para priorizar o que documentar e identificar pontos de confusão dos usuários.

### 4.1 Instrumentação

- Integrar Azure Application Insights
- Rastrear: page views, tempo na página, buscas realizadas, resultados clicados, perguntas ao chatbot, avaliações negativas

### 4.2 Dashboard interno

- Página no portal (autenticada) com os dados principais:
  - Páginas mais acessadas
  - Termos mais buscados (com e sem resultado)
  - Páginas com mais avaliações negativas
  - Perguntas frequentes ao chatbot sem resposta satisfatória

**Critério de conclusão da fase 4:** é possível abrir o dashboard e identificar quais módulos têm a documentação mais fraca baseado em dados reais de uso.

---

## Fase 5 — Refinamento e recursos secundários

**Objetivo:** aproximar o portal do nível de maturidade de um Confluence.

- Templates de página: estruturas padronizadas por tipo de conteúdo (tutorial passo a passo, referência de campo, FAQ do módulo)
- "Última atualização" por página (extraído do histórico Git)
- Páginas relacionadas: sugestões automáticas no rodapé com base em similaridade semântica (já disponível via Cosmos DB)
- Tags/etiquetas por página para filtros cruzados entre módulos
- Notificações via Teams quando páginas críticas forem atualizadas
- Otimização de SEO: meta tags, sitemap automático, Open Graph
- Modo de impressão/visualização limpa por página (sem chatbot, sem navegação lateral)

---

## Privacidade e LGPD

- Banner de **opt-in de cookies** obrigatório no go-live público (fase 1). Sem opt-in, o Application Insights não dispara telemetria de cliente.
- Página `/privacidade` listando: dados coletados (Application Insights — IP truncado, user agent, páginas visitadas; comentários — texto + contato opcional; reporte de erros — descrição + contato opcional), finalidade, base legal e contato do DPO da Hetosoft.
- Application Insights configurado com IP truncado / desligado e PII desligado por padrão.
- Em comentários e reporte de erros (fase 3), o campo de contato é **opcional**, nunca obrigatório.

---

## Decisões pendentes (não bloqueiam o início)

| Decisão | Impacto | Quando resolver |
|---|---|---|
| Esquema de URL do portal (padrão de rotas) | Experiência e SEO | Início da fase 1.1 |
| Nome de domínio do portal | Experiência do usuário | Antes do go-live da fase 1 |
| Contrato e endpoint da API Hetosoft de validação de login | Bloqueia fase 2.1 | Antes de iniciar fase 2 |
| Quem gerencia os usuários internos (fase 2) | Processo operacional | Antes de iniciar fase 2 |
| Threshold de avaliação negativa para abrir chamado automático | Regra de negócio | Antes de iniciar fase 3 |
| Política de moderação de comentários | Processo operacional | Antes de iniciar fase 3 |
| Endpoint e autenticação da API do sistema de suporte | Técnico — fase 3.3 | Antes de iniciar fase 3 |

---

## Decisões já tomadas

| Decisão | Resolução |
|---|---|
| Repositório | Novo repositório privado único na organização `hetosoft`. Fonte não fica pública. GitHub Pages continua no ar até o go-live do portal. |
| Layout do repositório | Pastas `/public/` e `/internal/` no mesmo repo, com flag `audience` no front matter. |
| Armazenamento de vetores | Azure Cosmos DB for NoSQL (free tier) — vetores persistidos, sem geração em runtime |
| Banco relacional | SQLite para autenticação e dados relacionais. Sem migração para Azure SQL. |
| Pipeline de embedding | CI/CD incremental via GitHub Actions — reprocessa apenas chunks com hash alterado |
| Chunking | Por seção `##` (H2) com caps: fundir < 80 tokens, dividir por `###` quando > 1500 tokens. |
| Dimensões do embedding | 768 (`text-embedding-004`) com similaridade cosseno |
| Mermaid no Blazor | `PSC.Blazor.Components.MarkdownEditor` 10.0.9 (TFM `net10.0`). |
| Sidebar/navegação | `nav.yaml` curado e versionado na raiz do repo. |
| URLs legadas (GH Pages) | Não preservadas — site Jekyll é encerrado no go-live. |
| Autenticação (fase 2) | API Hetosoft valida credencial (booleano); roles ficam no SQLite local do portal. |
| Versionamento de docs | Sem snapshots por release — portal reflete sempre a versão corrente. |
| Authoring pós-migração | PR-flow puro continua — sem editor in-app. |
| LGPD | Banner de opt-in de cookies + página `/privacidade` antes do go-live; PII desligado no Application Insights. |

---

## Ordem de prioridade confirmada

1. Fase 1 — Fundação + Busca semântica + Chatbot *(mais valor imediato)*
2. Fase 2 — Área interna autenticada
3. Fase 3 — Interação + Suporte
4. Fase 4 — Analytics
5. Fase 5 — Refinamentos
