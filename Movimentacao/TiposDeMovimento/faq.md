# ❓ FAQ — Cadastro de Tipos de Movimento - Sol.NET

Este FAQ concentra as **mensagens de validação** que aparecem ao salvar um Tipo de Movimento e as **perguntas mais frequentes** sobre o comportamento da tela. Para a referência completa de cada aba, veja a [Documentação](documentacao_tipos_de_movimento.md). Para o panorama do módulo, veja a [Visão Geral](README.md).

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Tipos de Movimento` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nesta tela.

---

## 🛡️ Validações ao salvar — guia de troubleshooting

A função `Validar` faz **mais de 50 verificações** antes de gravar. Quando uma falha, o sistema **abre automaticamente** a aba/sub-aba onde o problema está e foca o componente que causou. A tabela abaixo lista as mensagens mais frequentes e onde resolver cada uma.

### Identificação e Conta (aba `Dados Cadastrais`)

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Esse tipo de conta só pode ser Analítica!"* | Você definiu `Tipo de Conta = Sintética` mas preencheu `Complemento`. Sintética não pode ter complemento. | `Dados Cadastrais` — ajuste `Tipo de Conta` ou remova o `Complemento`. |
| *"Esse tipo de conta só pode ser Sintética!"* | Inverso — `Tipo de Conta = Analítica` sem `Complemento`. | `Dados Cadastrais` — preencha o `Complemento` ou troque para Sintética. |

### Fiscal (aba `Cabeçalho → Fiscal`)

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Tipo Emissão Terceiro não permitido… ( … )!"* | Tipo Emissão = Terceiro exige um `Tipo de Sequência` específico. | `Cabeçalho → Características` — ajuste o combo de sequência. |
| *"Não Permitido, CFOP em Natureza de Op. Não é de entrada!"* | Comportamento = Entrada com CFOPs fora da faixa 1/2/3. | `Cabeçalho → Fiscal → Natureza Operação` — usar CFOPs 1xxx/2xxx/3xxx. |
| *"Não Permitido, CFOP em Natureza de Op. Não é de Saída!"* | Comportamento = Saída com CFOPs fora da faixa 5/6/7. | `Cabeçalho → Fiscal → Natureza Operação` — usar CFOPs 5xxx/6xxx/7xxx. |
| *"Selecione ao menos uma série!"* | Tipo com Emissão Própria sem nenhuma série fiscal marcada. | `Cabeçalho → Fiscal → Série` — marque ao menos uma. |
| *"Selecione ao menos uma série padrão!"* | Há séries marcadas, mas nenhuma é a padrão. | `Cabeçalho → Fiscal → Série` — marque uma como Padrão. |
| *"série padrão tem que está selecionada!"* | A série padrão configurada não está com a flag `OPCAO` ativa — incoerência interna. | `Cabeçalho → Fiscal → Série` — desmarque a padrão atual e marque outra. |
| *"Tipos de Séries (Fiscal/Não Fiscal) devem ser iguais Ao Tipo do Modelo de Documento!"* | A série marcada é fiscal mas o modelo é não fiscal (ou vice-versa). | `Cabeçalho → Fiscal` — alinhar fiscal/não fiscal entre série e modelo. |
| *"Série RPS e Série Lote é Obrigatório para NFS-e!"* | Modelo NFS-e exige as duas séries adicionais. | `Cabeçalho → Serviço` — preencha. |
| *"Obrigatório marcar a Tag Consumo em Outras Operações para o Modelo de Documento selecionado."* | Modelo escolhido (geralmente Cupom Fiscal) exige a flag `Consumo` em Outras Operações. | `Outras Operações → Sistema` — marcar a tag. |

### Tabela de Preço (aba `Itens → Tabela de Preço`)

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Não permitido, Selecione uma forma de buscar o preço! Selecione uma Tabela de Preço!"* | Nenhuma tabela com `OPCAO = 1` marcada. | `Itens → Tabela de Preço` — marque ao menos uma tabela como disponível. |
| *"Não permitido, selecione uma Tabela de Preço Padrão!"* | Tabelas marcadas mas nenhuma é a Padrão. | `Itens → Tabela de Preço` — marque uma como Padrão. |

### Estoque (aba `Itens → Estoque`)

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Não Permitido, Obrigatório Local de Estoque!"* | Tipo que movimenta estoque sem Local padrão. | `Itens → Estoque → Itens Estoque`. |
| *"Não Permitido, Obrigatório Transação de Estoque!"* | Idem, sem Transação. | `Itens → Estoque → Itens Estoque`. |
| *"Não Permitido, '…' Sem Transação de Estoque!"* | Você marcou `Estatística de Estoque` ou `Baixar Quantidade na Promoção` sem Transação configurada. | `Itens → Estoque → Itens Estoque` — definir Transação ou desmarcar a opção. |
| *"Selecione 'Vender Sem Estoque'!"* | Tipo com Transação de Estoque mas a opção `Vender Sem Estoque` está sem escolha. | `Itens → Quantidade` — escolher Sim/Não. |

### Quantidade e Custo (aba `Itens → Quantidade`)

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Não permitido, '…Atualizar Custo Automático', Somente para Compras/Outros!"* | Você marcou `Atualizar Custo Automático` num Tipo de Vendas — Vendas não atualizam custo. | `Itens → Quantidade` — desmarcar OU mudar Comportamento para Entrada/Outros. |

### Devolução e Crédito (aba `Outras Operações → Sistema`)

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Não permitido, '…Devolução…' Em uma devolução!"* | Combinação inválida de flags de devolução. | `Outras Operações → Sistema` — revisar `Devolução` × `Devolução Crédito`. |
| *"Não permitido, '…Devolução…' Não é devolução!"* | Idem. | Mesma aba. |
| *"Não permitido, Sem '…Devolução Crédito…'!"* | Você desmarcou `Devolução Crédito` em um tipo que deveria gerar crédito. | `Outras Operações → Sistema`. |
| *"Não permitido, '…Devolução Crédito…' se não gerar Crédito!"* | Configurações incoerentes — gerar crédito sem ser devolução. | Mesma aba. |
| *"Não permitido, 'Quitar Crédito Automaticamente' se não gerar Crédito!"* | Quitar Crédito Automaticamente sem gerar crédito. | Mesma aba. |
| *"Não permitido, 'Quitar Crédito Automaticamente' se não for Tipo de Mov. 'PDV'!"* | Esta flag só é válida para tipos PDV. | Marcar `PDV` ou desmarcar `Quitar Crédito Automaticamente`. |

### Origem / Destino (aba `Cabeçalho → Origem/Destino`)

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Não permitido, 'Empresa' Destino do Movimento do Tipo Pessoa!"* | Você marcou Destino Empresa com a empresa-destino numa configuração que espera Pessoa. | `Cabeçalho → Origem/Destino`. |
| *"Não permitido, Preencher 'Empresa'!"* / *"Não permitido, Não Preenchido 'Empresa'!"* | Incoerência entre `Tipo Empresa Destino` e a empresa selecionada. | `Cabeçalho → Origem/Destino`. |
| *"Não Permitido Credito pessoa para Tipo de Movimento com Destino à Empresas!"* | Crédito pessoa não combina com destino Empresa. | `Outras Operações → Sistema` × `Cabeçalho → Origem/Destino`. |

### PDV e Comportamento (aba `Outras Operações → Sistema`)

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Não permitido, Não Consultar em Lancamento para Tipo de Mov. 'PDV'!"* | Tipo PDV não pode ter `Não Consultar`. | `Outras Operações → Sistema`. |
| *"Não Permitido, '…Memorizar Vendedor…' com a opção '…Vínculo com Usuário…'!"* | Memorizar Vendedor e Vínculo com Usuário são exclusivos. | `Cabeçalho → Funcionários`. |
| *"Não Permitido, '…Memorizar Vendedor…' com a opção 'Funcionário Padrão'!"* | Idem com Funcionário Padrão. | `Cabeçalho → Funcionários`. |
| *"Não Permitido, '…Permitir Tipo Mov…' com a opção '…Devolução Crédito…'!"* | Incompatibilidade. | `Outras Operações → Sistema`. |
| *"Não Permitido, '…Permitir Financeiro Aberto…' com a opção '…Devolução Crédito…'!"* | Incompatibilidade. | `Outras Operações → Sistema`. |
| *"Não Permitido, '…Movimento Parcial…' com a opção 'Venda Parcial'!"* | Incompatibilidade. | `Outras Operações → Sistema`. |
| *"Não Permitido!, A Opção 'SEPARAR ITENS DO MOVIMENTO (Global)' Esta Ativada em Configuração Geral."* | A configuração global da empresa bloqueia esta combinação. | Configuração da empresa, fora desta tela — desativar lá primeiro. |
| *"Não Permitido!, A Opção 'Promoção com Atualização em Grupo (MAIOR= ou A CADA)' Esta Ativada em Configuração Geral."* | Idem. | Configuração da empresa, fora desta tela. |

### OS / OS Requisição (aba `Outras Operações → Sistema`)

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Não permitido! '…OS…' e '…OS Requisição…' ao mesmo tempo."* | Tipo não pode ser OS **e** OS Requisição simultaneamente. | `Outras Operações → Sistema` — manter apenas um. |

### Financeiro (aba `Financeiro → Financeiro 1`)

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"Plano de Contas e Centro de Custo Obrigatório para Tipo de Movimento com Financeiro!"* | `Gerar Lançamento` ativa geração de financeiro sem Plano/Centro padrão. | `Financeiro → Financeiro 1` — preencher. |
| *"Não permitido, 'Não Estornar Financeiro', Somente para Compras/Outros!"* | Flag só vale para tipos de Entrada/Outros. | `Financeiro → Financeiro 1`. |

### Funcionário e Outros

| Mensagem | Causa | Onde resolver |
|----------|-------|---------------|
| *"…Só permitido para Funcionário!"* | Configuração que só faz sentido com funcionário, atribuída a outro tipo de pessoa. | `Cabeçalho → Funcionários`. |
| *"Obrigatório Editar 'Chave Protocolo'!"* | Configuração de protocolo exige edição manual. | `Cabeçalho → Características`. |

> 💡 **Como navegar as validações.** Ao receber qualquer uma dessas mensagens, o sistema **automaticamente** abre a aba/sub-aba onde o problema está e foca o componente que causou. Corrija e tente gravar de novo.

---

## ❓ Perguntas frequentes

### Comportamento geral

**Criei um Tipo de Movimento e ele não aparece para seleção nas telas operacionais.**
Confira nesta ordem:
1. `Inativo` está desmarcado?
2. O Comportamento bate com o que o usuário está tentando lançar — `Entrada` aparece em `Movimentos de Compras` (código `201`); `Saída` em `Movimentos de Vendas` (código `202`); `Outros` em `Outros Movimentos` (código `203`).
3. O `Tipo Movimento` (Vendas/Compras/Outros) está na hierarquia esperada?
4. O usuário tem permissão de acesso ao grupo (`TMOV_GRUPOS_ACESSOS`) que inclui este Tipo?

**O movimento foi gravado mas o saldo do produto não baixou.**
A `Transação de Estoque` amarrada ao Tipo não está configurada para subtrair as camadas certas (`FISICO`, `DISPONIVEL`). Abra `Transações de Estoque` (código `33`), localize a Transação e confira as marcações `+`/`-`/`Nenhum` para cada situação. Confira também a aba **Itens → Estoque** deste Tipo para garantir que está apontando para a Transação correta.

**Gravei e a SEFAZ recusou o XML.**
Causas mais comuns:
1. CFOP incompatível com o Comportamento (entrada × saída) — corrija em `Cabeçalho → Fiscal → Natureza Operação`.
2. CFOP fora da Natureza de Operação esperada.
3. Modelo de Documento e Série padrão em tipos diferentes (fiscal × não fiscal) — corrija em `Cabeçalho → Fiscal → Série`.
4. Tag `Consumo` faltando em `Outras Operações` para o modelo escolhido.

**Está dando "Plano de Contas e Centro de Custo Obrigatório".**
O `Gerar Lançamento` da aba `Financeiro → Financeiro 1` está ativando criação de conta a pagar/receber, mas você não definiu Plano e Centro padrão. Preencha os dois ou desligue `Gerar Lançamento`.

**Tentei marcar `Atualizar Custo Automático` numa venda e foi bloqueado.**
É comportamento esperado — atualização automática de custo só faz sentido em **Compras/Outros** (entradas), porque é a entrada que define o custo. Vendas consomem o custo, não o atualizam.

**A tela tem regras que conflitam com configurações globais (mensagens "Configuração Geral").**
Algumas opções desta tela ficam bloqueadas quando a empresa tem flags globais antagônicas — por exemplo, `SEPARAR ITENS DO MOVIMENTO (Global)` ou `Promoção com Atualização em Grupo`. Nesses casos, a configuração da **empresa** precisa ser ajustada primeiro (fora desta tela), e isso também exige acesso de suporte.

### Devolução e Crédito

**Quando usar `Devolução Crédito`?**
Quando a devolução deve **gerar um crédito** ao cliente em vez de devolver dinheiro/refazer pagamento. O crédito fica disponível na pessoa e pode ser usado para abater compras futuras.

**Devolução de PDV está reclamando que `Quitar Crédito Automaticamente` exige PDV.**
A flag `Quitar Crédito Automaticamente` só é válida em tipos com a flag PDV marcada. Se o tipo não é PDV, desligue `Quitar Crédito Automaticamente` ou marque `PDV`.

### Clonagem e Histórico

**Posso editar um Tipo já usado em movimentos antigos sem afetar o histórico?**
Sim — as alterações afetam **apenas** os movimentos lançados **a partir** da gravação. O histórico de movimentos passados continua referenciando o Tipo, mas o cálculo já gravado em cada movimento antigo permanece intacto. Para evitar surpresas, prefira **clonar** o Tipo e ajustar a cópia, ativando-a quando for o momento.

**Excluir um Tipo apaga os movimentos antigos?**
Não — a exclusão é bloqueada se houver movimentos vinculados. A recomendação é **inativar** o Tipo (campo `Inativo` no cabeçalho do formulário) — assim ele some dos combos de seleção em novos movimentos, mas o histórico continua referenciando.

### Visibilidade e Acesso

**Como controlar quais usuários veem este Tipo?**
Os grupos de acesso (`TMOV_GRUPOS`, `TMOV_GRUPOS_ACESSOS`, `TMOV_USUARIOS_GRUPOS`) controlam a visibilidade do Tipo por grupo de usuário. Essa configuração é feita em telas de permissão **fora** deste cadastro — solicite ao administrador / suporte.

**Posso ter Tipos diferentes por empresa?**
Sim. As sub-abas `Empresa` e `Local Estoque por Empresa` permitem overrides por empresa. Se a regra inteira é diferente entre lojas, prefira **clonar o Tipo** por empresa, em vez de tentar parametrizar tudo via overrides.

---

## 🔗 Links

- [Visão Geral](README.md) — papel do Tipo de Movimento, mapa das 12 abas.
- [Documentação](documentacao_tipos_de_movimento.md) — referência completa de cada aba e seus campos, exemplos práticos, exclusão, clonagem.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de Suporte / Consultores de Implantação Sol.NET
