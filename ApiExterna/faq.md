# ❓ FAQ — API Externa - Sol.NET

Perguntas que o suporte recebe com frequência sobre a **API Externa** do Sol.NET. Para o passo a passo completo, veja a [documentação principal](documentacao_api_externa.md); para o cartão de referência durante atendimento, veja o [guia rápido](guia_rapido.md).

---

## 🌐 Sobre a arquitetura

### Onde fica a URL da API que o parceiro vai usar?

A API é **distribuída** — não tem URL central da Hetosoft. Cada cliente do Sol.NET tem sua própria instalação do serviço, em servidor próprio. Para descobrir a URL aplicável, **fale com o time técnico responsável pela instalação do serviço no cliente Sol.NET**.

### Por que cada cliente tem uma URL diferente?

Porque a API roda no ambiente de cada cliente, próximo ao banco do Sol.NET dele. Isso protege os dados (não saem da infraestrutura do cliente), permite ajustes específicos e evita um ponto único de falha na Hetosoft.

### O Sol.NET precisa estar aberto para a API funcionar?

Não. A API é um serviço independente, instalado em servidor. Quando ela está rodando, atende às chamadas mesmo que ninguém esteja com o Sol.NET aberto.

---

## 🔑 Sobre a credencial

### Posso ver de novo a Secret Key de uma credencial já criada?

Não. A Secret Key aparece **uma única vez**, no momento da geração. O Sol.NET guarda apenas um resumo criptográfico — não tem como reconstruir o valor original. Isso é proteção: se o banco vazar, ninguém recupera as Secret Keys dos parceiros.

### O parceiro perdeu a Secret Key. O que faço?

Crie uma **nova credencial** com a mesma configuração de permissões. Inative ou exclua a credencial antiga. Entregue ao parceiro o novo `Client ID` e a nova `Secret Key`.

### Por que o parceiro não recebeu o e-mail com a Secret Key?

O envio depende do servidor de e-mail configurado no Sol.NET. Quando o envio falha, **o sistema copia a Secret Key para a área de transferência** e exibe uma mensagem no momento do salvamento — repare se esse aviso apareceu. Se nem o e-mail nem a área de transferência conseguiram entregar (caso raro), a única saída é criar uma nova credencial.

### Posso editar o Client ID?

Não. O `Client ID` é gerado pelo sistema na criação e fica fixo enquanto a credencial existir.

### Editar o cadastro do parceiro invalida a Secret Key?

Não. A Secret Key só é gerada na criação. Editar dados de contato, IP Whitelist, limite de requisições ou permissões mantém a Secret Key existente.

---

## 🛂 Sobre permissões

### O parceiro precisa de mais contextos do que combinado. O que faço?

Confirme com o responsável interno (gestor, comercial) se a liberação está aprovada. Em seguida, abra a credencial na tela `150`, em **Permissões** clique em **Novo**, adicione o contexto pedido com os verbos combinados e salve. A liberação passa a valer imediatamente.

### Como bloquear temporariamente um parceiro?

Não exclua nada. Abra a credencial e marque **Inativo** em cada permissão. A credencial continua existindo, mas o parceiro recebe erro de autorização em todas as chamadas. Para liberar de volta, desmarque `Inativo`.

### Posso definir um prazo de validade para a liberação?

Sim, por permissão. No campo **Data de expiração** da permissão, informe a data de fim. Passada essa data, a permissão para de funcionar automaticamente. Útil para POC e projetos com escopo de tempo definido.

### Qual a diferença entre `Inativo` e excluir a permissão?

`Inativo` mantém o registro e o histórico — é reversível. Excluir apaga em definitivo. Prefira `Inativo` para bloqueios temporários e exclusão apenas quando se tem certeza de que a permissão não voltará.

### Para que serve o campo `Claims customizadas`?

Para configurações específicas combinadas com o time técnico (regras especiais não cobertas pelos contextos padrão). Em uso normal, **deixe em branco** — só preencha sob orientação técnica.

---

## 🔒 Sobre segurança e limites

### O parceiro está sendo bloqueado por IP — onde ajusto?

Na credencial dele, atualize o campo **IP Whitelist** incluindo o IP atual da aplicação do parceiro. Confirme com ele qual é o IP de saída real (pode ser diferente do IP de escritório). Se houver mais de um servidor, coloque todos.

### Posso deixar a IP Whitelist em branco?

Tecnicamente sim — vazio significa "qualquer IP". Em produção **não recomendamos**, porque qualquer um com a Secret Key passa a ter acesso. Sempre prefira preencher.

### Quantas requisições por minuto definir?

Depende do uso:
- Sincronização periódica (a cada minutos): `20` a `60`/minuto resolve com folga.
- Consulta sob demanda esporádica: `30` a `60`/minuto.
- Tempo real (PDV, mobile): converse com o time técnico antes de liberar valor alto.

### O que acontece quando o parceiro estoura o limite?

As requisições adicionais são recusadas pelo serviço até a janela de tempo (próximo minuto) passar. O parceiro recebe um erro indicando excesso de chamadas. Não há bloqueio definitivo — o limite reinicia a cada janela.

### Como sei se um parceiro está usando a credencial?

Os campos **Contagem de Requisições** e **Última Requisição** da credencial mostram o uso. Se a contagem está alta e a última requisição é recente, o parceiro está ativo. Se está zerada ou parada há muito tempo, é candidato a revisão (parceiro abandonou? credencial nunca foi entregue?).

---

## 🔄 Sobre operação no dia a dia

### Posso reutilizar uma credencial antiga para um parceiro novo?

Tecnicamente é possível (editando os dados), mas **não recomendamos** — a `Contagem de Requisições` e a `Última Requisição` carregam o histórico do parceiro antigo e confundem o controle. Prefira sempre criar uma credencial nova.

### Como achar uma credencial específica?

Na tela `150`, use a busca pelo `Nome do Cliente` ou pelo `Client ID`. A lista mostra todas as credenciais cadastradas; clique para abrir.

### O parceiro mudou de IP. Tenho que gerar credencial nova?

Não. Basta atualizar a `IP Whitelist` da credencial existente com o novo IP (ou adicionar o novo ao lado do antigo, durante a transição). A Secret Key continua a mesma.

### A API permite o parceiro lançar pedidos (criar dados) no Sol.NET?

Hoje a API é focada em **consulta**. Inclusão de dados (pedidos, orçamentos) está prevista para a evolução do serviço. Quando ficar disponível, será liberada por permissões adicionais com verbo `POST` nos contextos correspondentes.

### Qual contexto liberar para o parceiro consultar produtos e estoque?

Adicione duas permissões: uma no contexto **Produtos** com `GET` e outra no contexto **Estoque** com `GET`. São independentes — liberar um não libera o outro.

### Quem documenta os endpoints (URLs e formatos) da API para o parceiro?

A própria API publica uma página de documentação técnica na instalação do serviço, com a lista de endpoints, parâmetros e formatos de resposta. Solicite o endereço ao time técnico responsável pela instalação no cliente.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 1.0
**🎯 Público-alvo**: Equipe de suporte Hetosoft
