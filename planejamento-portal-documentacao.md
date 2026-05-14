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

## Arquitetura de embeddings (decisão consolidada)

A aplicação **nunca gera embeddings em runtime**. A geração é responsabilidade exclusiva do pipeline CI/CD:

1. Desenvolvedor edita um `.md` e faz push para `main`.
2. O GitHub Actions detecta, via `git diff`, quais arquivos `.md` mudaram no commit.
3. Para cada arquivo alterado, chama a Gemini Embeddings API (`text-embedding-004`).
4. Faz upsert dos vetores no Cosmos DB (document ID = caminho do arquivo).
5. A aplicação, ao receber uma query de busca ou do chatbot, lê os vetores do Cosmos DB e calcula a similaridade — sem nenhuma chamada de geração.

Benefícios: cold starts rápidos, sem consumo de cota Gemini em produção, atualização incremental (apenas os arquivos que mudaram são re-processados).

**Configuração do container Cosmos DB:**
- Modelo: `text-embedding-004` → 768 dimensões
- Função de distância: cosseno
- Tipo de índice: flat (adequado para o volume atual; revisar para HNSW se o corpus ultrapassar ~5.000 chunks)

---

## Fase 1 — Fundação pública + Busca + Chatbot

**Objetivo:** portal público funcional, com o conteúdo atual migrado e os dois recursos mais importantes no ar.

### 1.1 Projeto base Blazor SSR

- Criar projeto Blazor SSR (.NET 10) com MudBlazor configurado
- Configurar pipeline CI/CD (GitHub Actions → Azure App Service)
- Definir estrutura de pastas para os arquivos Markdown (espelhando os módulos do Sol.NET)
- Migrar os Markdowns existentes do repositório atual para o novo projeto
- Implementar leitura e renderização dos arquivos `.md` em tempo de execução
- Suporte a diagramas Mermaid via pacote NuGet (ex.: `PSC.Blazor.Components.Mermaid`) — sem JavaScript explícito no projeto; validar compatibilidade com .NET 10 antes de commitar a escolha
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

- Adicionar SQLite + ASP.NET Core Identity ao projeto
- Tela de login (usuário e senha)
- Gerenciamento de usuários internos via seed ou painel admin simples
- Proteção de rotas com `[Authorize]`

### 2.2 Conteúdo interno

- Criar seção de Markdowns internos (fora do diretório público)
- Conteúdo inicial: procedimentos de implantação, scripts e queries de suporte, documentação técnica de integrações
- Pipeline de embedding estendido: ao processar `.md` internos, grava no Cosmos DB com flag `interno: true`
- Navegação lateral própria para a área interna, separada da pública

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

## Decisões pendentes (não bloqueiam o início)

| Decisão | Impacto | Quando resolver |
|---|---|---|
| Nome de domínio do portal | Experiência do usuário | Antes do go-live da fase 1 |
| Quem gerencia os usuários internos (fase 2) | Processo operacional | Antes de iniciar fase 2 |
| Threshold de avaliação negativa para abrir chamado automático | Regra de negócio | Antes de iniciar fase 3 |
| Política de moderação de comentários | Processo operacional | Antes de iniciar fase 3 |
| Endpoint e autenticação da API do sistema de suporte | Técnico — fase 3.3 | Antes de iniciar fase 3 |

---

## Decisões já tomadas

| Decisão | Resolução |
|---|---|
| Repositório | Novo repositório na organização `hetosoft`. GitHub Pages continua no ar até o go-live do portal. |
| Armazenamento de vetores | Azure Cosmos DB for NoSQL (free tier) — vetores persistidos, sem geração em runtime |
| Banco relacional | SQLite para autenticação e dados relacionais. Sem migração para Azure SQL. |
| Pipeline de embedding | CI/CD incremental via GitHub Actions — reprocessa apenas arquivos `.md` alterados no commit |
| Dimensões do embedding | 768 (`text-embedding-004`) com similaridade cosseno |
| Mermaid no Blazor | Pacote NuGet (sem JavaScript explícito no projeto) — candidato: `PSC.Blazor.Components.Mermaid`; validar compatibilidade com .NET 10 antes do início |

---

## Ordem de prioridade confirmada

1. Fase 1 — Fundação + Busca semântica + Chatbot *(mais valor imediato)*
2. Fase 2 — Área interna autenticada
3. Fase 3 — Interação + Suporte
4. Fase 4 — Analytics
5. Fase 5 — Refinamentos
