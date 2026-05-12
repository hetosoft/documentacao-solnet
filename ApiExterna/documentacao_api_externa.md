# 📄 API Externa — Cadastro de Acessos e Geração de Credenciais - Sol.NET

## 🎯 Visão Geral

A **API Externa** é a nova modalidade de integração que a Hetosoft disponibiliza a parceiros do Sol.NET. Em vez de instalar um aplicativo ou abrir o banco do cliente, o parceiro recebe uma **credencial** gerada pela equipe de suporte e a usa para acessar um conjunto de serviços REST que consultam dados do ERP.

A credencial é composta por:

- **Client ID** — identificador público do parceiro (uma espécie de "usuário" da integração)
- **Secret Key** — segredo equivalente à senha; só aparece **uma única vez**, no momento da geração

Cada credencial é configurada com:

- **Contextos liberados** (Produtos, Estoque, Pessoas, Movimentos, Empresas, Condições de Pagamento, Tabelas de Preço, Fretes, Admin) e quais operações são permitidas em cada um (consulta, inclusão futura, etc.)
- **Lista de IPs autorizados** (`IP Whitelist`)
- **Limite de requisições por minuto** (rate limit)
- **Data de expiração** opcional, por contexto

A geração e a manutenção das credenciais acontecem em uma **tela do Sol.NET**, operada pelo suporte. O parceiro nunca acessa essa tela — apenas recebe a credencial pronta.

> 📡 **Arquitetura distribuída** — o serviço da API é instalado em cada cliente do Sol.NET. Não há URL central da Hetosoft. A URL real à qual o parceiro vai apontar deve ser solicitada ao time técnico responsável pela instalação. O Sol.NET gera a credencial; a URL fica fora do escopo desta tela.

### Principais características

- ✅ Credencial pessoal por parceiro, com revogação independente
- ✅ Controle fino de permissões por contexto e por operação
- ✅ Rate limit configurável para proteger o serviço
- ✅ Lista de IPs autorizados para reduzir risco em caso de vazamento de credencial
- ✅ Auditoria automática de uso (data/hora da última requisição, contagem de chamadas)
- ✅ Secret Key armazenada apenas como resumo criptográfico — não há como recuperar depois de gerada

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Acessos WebAPI Externa |
| **Código (`F1`)** | `150` |

Abra a pesquisa universal (atalho `F1`) e digite **`150`** ou parte do nome **`Acessos WebAPI`**.

---

## 📝 Campos do cadastro do parceiro

A tela é dividida em duas áreas: a **identificação do parceiro** (dados de contato, controles operacionais) e o **par credencial** (Client ID e Secret Key). Os campos abaixo aparecem na ordem da tela:

### Identificação e contato

| Label | Para quê serve |
|-------|----------------|
| **Nome do Cliente** | Nome do parceiro (empresa ou pessoa) que vai usar a credencial. Aparece como referência principal na lista de credenciais. |
| **E-mail** | Endereço de e-mail do parceiro. É usado tanto como contato quanto como destino do envio automático da Secret Key (ver `Fluxo` abaixo). |
| **Contato** | Nome da pessoa responsável pela integração no parceiro (quem o suporte aciona para tratar a credencial). |
| **Telefone** | Telefone de contato do parceiro. |
| **Descrição** | Campo de texto livre para anotações sobre o parceiro e a finalidade da credencial. Útil para registrar contrato, projeto, módulo do parceiro, etc. |

### Operação e limites

| Label | Para quê serve |
|-------|----------------|
| **Limite de Requisições/minuto** | Quantas chamadas por minuto esta credencial pode fazer antes de ser temporariamente bloqueada pelo serviço. |
| **IP Whitelist** | Lista de IPs (ou faixas) a partir dos quais a credencial pode ser usada. Requisições vindas de IPs fora desta lista são recusadas. Quando deixado em branco, qualquer IP é aceito (use com cautela). |

### Indicadores de uso (somente leitura)

| Label | Para quê serve |
|-------|----------------|
| **Contagem de Requisições** | Total acumulado de chamadas que a credencial fez até agora. Útil para identificar parceiros muito ativos ou inativos. |
| **Última Requisição** | Data e hora da última chamada bem-sucedida. Se está em branco, a credencial nunca foi usada. |
| **Criado Em** | Data e hora em que a credencial foi gerada. |
| **Atualizado Em** | Data e hora da última alteração no cadastro. |

### Credencial (somente leitura)

| Label | Para quê serve |
|-------|----------------|
| **Client ID** | Identificador público da credencial, gerado automaticamente ao clicar em **Novo**. Pode ser copiado a qualquer momento (a tela tem botão para copiar). |
| **Secret Key** | Segredo criptográfico da credencial. **Aparece em texto claro apenas no momento da geração**, antes de salvar. Após o salvamento, o sistema armazena apenas o resumo criptográfico — não há como ver o valor original novamente. |

> ⚠️ **A Secret Key não pode ser recuperada depois de salva.** Se o parceiro perder, é necessário criar uma **nova credencial** e descartar a antiga (inativando ou excluindo). Não existe função de "mostrar Secret Key novamente" — isso é proteção contra vazamento.

---

## 🛂 Permissões por contexto

Não basta gerar a credencial: é preciso definir **o que ela pode fazer**. Isso é feito na sub-área de **Permissões**, dentro do próprio cadastro. Cada permissão liga a credencial a um **contexto** (uma área de dados do Sol.NET) e a um conjunto de **operações HTTP** que ficam liberadas naquele contexto.

### Contextos disponíveis

| Contexto | O que libera |
|----------|--------------|
| **Produtos** | Acesso ao cadastro de produtos do Sol.NET. |
| **Estoque** | Acesso à posição de estoque dos produtos. |
| **Pessoas** | Acesso ao cadastro de pessoas (clientes, fornecedores, transportadores, etc.). |
| **Movimentos** | Acesso aos movimentos (compras, vendas, devoluções, etc.). |
| **Empresas** | Acesso ao cadastro de empresas. |
| **CondicoesPagamento** | Acesso ao cadastro de condições de pagamento. |
| **TabelasPreco** | Acesso às tabelas de preço configuradas. |
| **Fretes** | Acesso aos dados de frete. |
| **Admin** | Funções administrativas reservadas (uso interno; só liberar quando explicitamente combinado). |

### Operações HTTP

Em cada permissão, o suporte escolhe **quais verbos HTTP** ficam liberados no contexto. Em linguagem de uso:

- **GET** — leitura/consulta dos dados (é o que está disponível hoje na maioria dos contextos)
- **POST** — inclusão de dados (em desenvolvimento; será usado, por exemplo, em pedidos e orçamentos)
- **PUT** — atualização de dados existentes
- **PATCH** — atualização parcial de dados existentes
- **DELETE** — exclusão de dados

> ℹ️ Hoje o foco oficial da API é **consulta**. Marque apenas **GET** salvo combinação explícita em contrário. Inclusão (POST) está prevista para evolução posterior e deve ser tratada caso a caso com o time técnico.

### Campos adicionais da permissão

| Label | Para quê serve |
|-------|----------------|
| **Contexto** | Qual área de dados a permissão libera (lista acima). |
| **Operações (verbos HTTP)** | Quais verbos ficam liberados naquele contexto. |
| **Claims customizadas** | Texto livre para configurações específicas combinadas com o time técnico. Em uso normal, **deixe em branco**. |
| **Observações** | Notas internas sobre a permissão (motivo, contrato, restrições). |
| **Data de expiração** | Se preenchida, a permissão deixa de funcionar automaticamente nessa data, mesmo que a credencial permaneça ativa. Útil para liberar acesso temporário (POC, projeto). |
| **Inativo** | Marca a permissão como inativa sem precisar excluir — uma forma de bloquear temporariamente um contexto sem perder o histórico. |

### Como gerenciar permissões

Dentro do cadastro do parceiro:

1. Em **Permissões**, clique em **Novo** para adicionar um contexto.
2. Escolha o **Contexto** e marque as **operações** combinadas.
3. Salve a permissão.
4. Repita para cada contexto que o parceiro precisa.
5. Para bloquear sem perder histórico, marque **Inativo**. Para liberar de novo, basta desmarcar.

---

## 🔒 Segurança e limites

### IP Whitelist

A `IP Whitelist` lista os IPs (públicos) a partir dos quais a credencial pode ser usada.

- Preencha com **os IPs reais do parceiro** — normalmente o IP da aplicação ou servidor que vai consumir a API.
- Quando vazio, o serviço aceita qualquer IP. Use vazio apenas em ambientes controlados.
- Requisições vindas de IPs fora da lista são **recusadas** com erro de autorização — peça ao parceiro o IP correto antes de gerar a credencial.

### Limite de requisições por minuto

O campo **Limite de Requisições/minuto** define quantas chamadas por minuto a credencial pode fazer. Estourado o limite, requisições adicionais são recusadas pelo serviço até a janela de tempo passar.

- Use valores compatíveis com o caso de uso. Para integrações de consulta esporádica (relatórios, sincronização noturna), 30 a 60/minuto costuma ser folgado.
- Para integrações de tempo real (PDV, mobile), conversar com o time técnico para definir um valor seguro.
- Não deixe em branco em produção — o limite serve para proteger o serviço do parceiro contra abuso e contra loops mal calibrados.

### Expiração

A expiração é configurada **por permissão**, não pela credencial inteira. Use quando:

- O acesso é para um projeto com prazo definido.
- O parceiro está em fase de teste e a liberação não é definitiva.
- Há uma data combinada em contrato para revisão de escopo.

Passada a data, a permissão para de funcionar mesmo que o resto do cadastro continue ativo.

---

## 🛠️ Como gerar uma credencial para um parceiro (fluxo completo)

Este é o roteiro operacional do suporte para emitir uma nova credencial.

### Antes de começar — colete do parceiro

- Nome do parceiro (empresa) e nome da pessoa responsável
- E-mail e telefone de contato
- **IPs públicos** que vão consumir a API
- **Contextos** que o parceiro precisa acessar (ex.: Produtos + Estoque)
- **Operações** combinadas (normalmente só consulta = GET)
- Limite de requisições/minuto combinado (ou orientação para usar um valor padrão)
- Se há prazo de validade combinado

### Na tela `Cadastro de Acessos WebAPI Externa` (`150`)

1. Abra a pesquisa universal (`F1`) e digite `150`.
2. Clique em **Novo**. O sistema gera automaticamente o **Client ID** (identificador público) e a **Secret Key** (segredo) — eles aparecem nos respectivos campos da tela.
3. Preencha **Nome do Cliente**, **E-mail**, **Contato**, **Telefone** e **Descrição** (opcional, mas recomendado para rastrear o contrato/projeto).
4. Preencha **IP Whitelist** com os IPs do parceiro.
5. Preencha **Limite de Requisições/minuto** conforme combinado.
6. Em **Permissões**, adicione cada contexto que o parceiro vai usar, marcando apenas as operações combinadas. Use **Data de expiração** quando o acesso for por prazo.
7. **Salve.** No momento do salvamento, o sistema:
   - Calcula o resumo criptográfico da `Secret Key` e armazena apenas esse resumo no banco — o valor em texto claro **não é guardado**.
   - Tenta **enviar a `Secret Key` em texto claro por e-mail** ao endereço cadastrado no parceiro.
   - Se o envio do e-mail falhar (servidor de e-mail indisponível, endereço inválido, etc.), o sistema **copia a `Secret Key` para a área de transferência** e exibe uma mensagem orientando a entrega manual.

> ⚠️ **Atenção — esta é a única chance de ver a Secret Key.** Confirme com o parceiro que ele recebeu o e-mail (ou anote a Secret Key vinda da área de transferência em local seguro para entrega). Depois deste momento, **o sistema não consegue mais mostrar o valor original** — para gerar outra Secret é preciso criar uma nova credencial.

### Entrega ao parceiro

O parceiro precisa receber:

- O **Client ID** (pode ser entregue por qualquer canal, é informação pública)
- A **Secret Key** (informação sensível — entregue pelo canal mais seguro disponível)
- A **URL da API** (obtida com o time técnico responsável pela instalação no cliente Sol.NET — não fica nesta tela)
- A lista de **contextos e operações** liberados (para que ele saiba o que pode chamar)

---

## 🌐 O que o parceiro faz com a credencial

Este bloco é alto nível, só para o suporte entender o lado do parceiro. A referência técnica completa fica na própria API, em uma página de documentação publicada pelo serviço.

1. O parceiro **autentica** enviando `Client ID` + `Secret Key` para um endpoint de autenticação. O serviço devolve um **token** com validade limitada.
2. O parceiro **usa esse token** como autorização em cada chamada subsequente (consulta de produtos, de estoque, etc.).
3. A cada chamada, o serviço verifica:
   - Se o token é válido e está dentro do prazo
   - Se o IP da requisição está na **IP Whitelist**
   - Se o **contexto** e o **verbo HTTP** da chamada estão liberados nas permissões da credencial
   - Se o **limite por minuto** ainda não foi atingido
   - Se a permissão específica não está marcada como **Inativo** nem com **Data de expiração** vencida
4. Atendidas as regras, a chamada é processada e os indicadores `Contagem de Requisições` e `Última Requisição` da credencial são atualizados.

> 📘 **A URL da API e a documentação técnica completa (lista de endpoints, formatos de resposta)** ficam disponíveis na própria instalação do serviço, em uma página de documentação publicada pela aplicação. Solicite ao time técnico do cliente Sol.NET o endereço aplicável e repasse ao parceiro.

---

## 🔄 Manutenção da credencial

### Editar dados do parceiro

Localize a credencial pelo `Nome do Cliente` na lista de busca da tela `150`, abra para edição e altere o que for necessário (contato, e-mail, IPs, limite de requisições, permissões). Salve.

> ℹ️ **Editar não regera a Secret Key.** A `Secret Key` só é gerada na criação. Editar o cadastro mantém o segredo já existente.

### Bloquear temporariamente um parceiro

Em vez de excluir, marque como **Inativo** cada permissão da credencial. A credencial continua existindo, mas todos os contextos ficam bloqueados — o parceiro recebe erro de autorização em qualquer chamada. Para reativar, desmarque `Inativo` nas permissões.

### Trocar a Secret Key (parceiro perdeu / vazou)

Como o valor original não é guardado, **não é possível "redefinir" a Secret Key**. O procedimento é:

1. Inative todas as permissões da credencial antiga (para impedir uso imediato) ou exclua a credencial.
2. Crie uma **nova credencial** seguindo o fluxo normal.
3. Refaça as permissões com a mesma configuração.
4. Entregue a nova credencial ao parceiro.
5. Confirme com o parceiro que a antiga não está mais em uso e exclua-a do cadastro.

### Excluir uma credencial

Localize a credencial na lista, abra e use a função de exclusão. Esse procedimento é definitivo — perde-se o histórico de uso (contagem, última requisição). Para preservar histórico, prefira **inativar**.

---

## 💡 Exemplos práticos

### Parceiro X precisa consultar produtos e estoque para abastecer um e-commerce

1. Colete do parceiro: nome (`E-commerce ACME`), e-mail, telefone, IP público da aplicação (`203.0.113.10`), volume estimado (uma sincronização a cada 5 minutos ≈ ~12 chamadas/minuto pico).
2. Confirme com o time técnico do cliente Sol.NET a URL da API a entregar.
3. Na tela `150` (`F1`), clique em **Novo**. Anote o `Client ID` e a `Secret Key` que apareceram.
4. Preencha os dados do parceiro, IP Whitelist (`203.0.113.10`), Limite de Requisições/minuto (`30`) — folga sobre o pico estimado.
5. Em **Permissões**:
   - Adicione `Produtos` com **GET** marcado.
   - Adicione `Estoque` com **GET** marcado.
6. Salve. Confirme o envio da Secret Key por e-mail; se falhar, recupere da área de transferência.
7. Envie ao parceiro: Client ID, Secret Key, URL da API, e a lista de contextos liberados (`Produtos GET`, `Estoque GET`).

### Parceiro perdeu a Secret Key

1. Confirme com o parceiro que o problema é mesmo perda (não é IP novo, não é prazo expirado).
2. Localize a credencial atual na tela `150`.
3. Inative todas as permissões dela (ou exclua a credencial se já está claro que será substituída).
4. Siga o fluxo normal para criar **nova credencial** com a mesma configuração de permissões.
5. Entregue o novo `Client ID` e nova `Secret Key` ao parceiro.

### Acesso temporário para POC

1. Crie a credencial normalmente.
2. Nas **Permissões**, preencha **Data de expiração** com a data de fim do POC (ex.: 30 dias à frente).
3. Após a data, a permissão para de funcionar automaticamente. Não é necessário acompanhar o vencimento manualmente.

---

## ❓ FAQ / Problemas comuns

**O parceiro disse que está recebendo erro de autorização — por onde começo?**
Verifique, nesta ordem: (1) a credencial não foi excluída ou inativada; (2) o IP do parceiro está na `IP Whitelist`; (3) o contexto chamado está liberado para ele com o verbo HTTP correto; (4) nenhuma das permissões está marcada como `Inativo` ou com `Data de expiração` vencida.

**Onde fica a URL da API que o parceiro vai consumir?**
Não fica nesta tela. A API é distribuída — cada cliente Sol.NET tem sua própria instalação. Solicite a URL ao time técnico responsável pela instalação do serviço no cliente.

**Posso ver de novo a Secret Key de uma credencial já criada?**
Não. O sistema guarda apenas o resumo criptográfico, não o valor original. Se a Secret Key foi perdida, é preciso criar uma nova credencial.

**Editei o cadastro do parceiro e ele perdeu acesso. O que aconteceu?**
Verifique se alguma permissão foi removida, se alguma foi marcada como `Inativo`, ou se a `Data de expiração` foi alterada. Editar dados de contato ou IP Whitelist não invalida a credencial, mas alterar a IP Whitelist sem incluir o IP atual do parceiro bloqueia o acesso imediatamente.

**Quantas requisições por minuto devo definir?**
Depende do caso de uso. Para integrações de sincronização periódica (a cada X minutos), 20 a 60/minuto resolve. Para integrações em tempo real (PDV, mobile), conversar com o time técnico antes de liberar um valor alto.

**O parceiro pode usar a credencial de IPs diferentes?**
Sim, desde que todos estejam na `IP Whitelist`. Se o parceiro tem servidores em locais diferentes ou IP dinâmico, peça a lista completa e cadastre todas.

**A API permite o parceiro lançar pedidos no Sol.NET?**
Hoje a API é focada em **consulta**. Inclusão de dados (pedidos, orçamentos) é parte da evolução prevista. Quando estiver disponível, será liberada via permissões adicionais (verbos `POST`) nos contextos correspondentes.

**Por que o parceiro não recebeu o e-mail com a Secret Key?**
O envio depende da configuração de e-mail do ambiente Sol.NET. Quando falha, o sistema copia a Secret Key para a área de transferência e exibe uma mensagem — verifique se o aviso apareceu na hora de salvar. Se nem o e-mail nem a área de transferência conseguiram entregar (raríssimo), a única saída é gerar uma nova credencial.

**Posso reutilizar uma credencial antiga para um novo parceiro?**
Tecnicamente sim (editando os dados), mas **não é recomendado** — a contagem de requisições e a última requisição da credencial antiga ficam no histórico e confundem o controle. Prefira criar uma credencial nova para cada parceiro.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Relação |
|------|:---:|---------|
| Movimentação | Ver módulo Movimentação | Contexto `Movimentos` da API consulta esses dados |
| Cond. de Pagamento | `8` | Contexto `CondicoesPagamento` da API |
| Pessoas | Cadastro do módulo Pessoas | Contexto `Pessoas` da API |

---

## ⚠️ Limites desta documentação

Esta documentação descreve a operação da tela `Cadastro de Acessos WebAPI Externa` (`150`) e o fluxo do suporte para emitir e manter credenciais. **Não cobre**:

- **Referência técnica dos endpoints da API** (formato exato de cada chamada, estrutura de resposta) — fica disponível na própria instalação da API, em uma página de documentação publicada pelo serviço. Solicite o endereço ao time técnico do cliente.
- **Configuração de envio de e-mail** do Sol.NET — o envio da Secret Key por e-mail depende de o ambiente ter SMTP configurado corretamente; se isso não estiver pronto, sempre haverá fallback pela área de transferência, mas a entrega ao parceiro precisará ser manual.
- **Instalação e operação do serviço da API** no cliente — atividade do time técnico/infraestrutura, fora do escopo desta tela.
- **Detalhes de funcionamento do controle de IP, rate limit e validação de token** — o que importa para o suporte está descrito acima; ajustes finos são feitos pelo time técnico.
- **Comunicação real com a aplicação do parceiro** — esta documentação descreve as configurações disponíveis no Sol.NET; o resultado prático da integração depende também do código do parceiro.

Para informações fora desse escopo, consulte o time técnico responsável pela API e o suporte Hetosoft.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 1.0
**🎯 Público-alvo**: Equipe de suporte Hetosoft
