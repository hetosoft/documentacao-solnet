# 📄 Cadastro de Formas de Pagamento - Sol.NET

## 🎯 Visão Geral

A **Forma de Pagamento** define **como** o dinheiro entra ou sai da empresa: dinheiro, cheque, cartão de crédito ou débito, PIX ou "outros" (notas promissórias, vales, escambo, etc.). Cada forma de pagamento é também classificada como **Receber**, **Pagar** ou **Ambos**, e carrega comportamento específico para diversos pontos do sistema:

- **PDV** — controle de troco, permissão de uso no PDV, abertura de gaveta, mostrar detalhes na tela, agrupamento, troca de condição de pagamento.
- **TEF** — tipo de rede, busca automática, parcelas e parâmetros automáticos para débito/crédito.
- **Cheque** — pré-datado, solicita dados, compensar, vencimento por data pré-datada.
- **Cartão** — todo o **Controle de Cartão** (operadoras, taxas, plano de contas, centro de custo, parcelas, tarifa fixa/mínima/máxima, modo de parcelamento, vencimento em finais de semana).
- **HetoBank / PIX** — integração com a plataforma HetoBank, exclusiva para tipo PIX.
- **Condições de Pagamento** — permitido mudar para uma condição específica.

É um cadastro central do financeiro: praticamente todo título e toda operação que envolve recebimento ou pagamento referencia uma forma de pagamento. Por isso a tela tem muitas regras cruzadas — várias combinações são bloqueadas por validação.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Formas de Pagamento |
| **Código (`F1`)** | `7` |

Abra a pesquisa universal (atalho `F1`) e digite **`7`** ou parte do nome **`Formas de Pagamento`**.

---

> 🔎 **Na lista de busca** — filtros próprios são `Nº Grupo` e `Tipo`. As colunas `Tipo`, `Tipo Contas PR` e `Tipo de Troco` aparecem com descrição textual (não com o número interno).

## 🧭 Sub-abas do formulário

O formulário é dividido em duas grandes abas:

- **`Geral`** — identificação + Tipo + Tipo Contas PR + opções (com sub-abas internas)
- **`Controle De Cartão`** — regras de operadoras de cartão (grid com inserção/edição de detalhes)

### Sub-abas internas da aba `Geral` → `pagOpcoes`

| Sub-aba | Para quê serve |
|---------|----------------|
| **Troco** | Configura como o troco é tratado (só visual / em registro) e quais formas de troco podem ser usadas (dinheiro, crédito em conta da pessoa) |
| **Cheque** | Comportamento específico de cheque ao quitar contas a pagar |
| **Extras** | Opções avançadas: quitar individual, permissão (PDV), data de vencimento, validação pós-venda |
| **PDV** | Permissão e comportamento no PDV (permitido, abrir gaveta, mostrar detalhes, agrupamento, mudar para condição de pagamento) |
| **TEF** | Parâmetros de TEF (envio automático crédito/débito, parcelas, carteira digital) |

---

## 📝 Campos principais (aba `Geral`)

### Identificação (sempre visível na aba)

| Label | Para quê serve |
|-------|----------------|
| **Código** | Número interno da forma (auto-preenchido com o próximo disponível ao clicar em **Novo**; pode ser editado) |
| **Descrição** | Nome amigável (obrigatório) |
| **Contas PR** | Define em qual lado a forma é usada: `Receber`, `Pagar` ou `Ambos` (obrigatório) |
| **Tipo** | Tipo da forma — controla a maior parte das regras: `Dinheiro`, `Cheque`, `Cartão de Crédito`, `Cartão de Débito`, `Pix` ou `Outros` (obrigatório) |
| **TEF - Rede** | Identificador da rede TEF (texto livre) |

### Caixa `Cheque` (válida quando o tipo permite cheque)

- **Não compensar** — não compensar automaticamente
- **Solicita Dados** — solicita os dados do cheque na operação
- **Pré-Datado** — marcar quando esta forma é pré-datada
- **Sem Troco** — não permite troco
- **TEF** — integra com TEF
- **Fiscal** — entra no cupom fiscal
- **Liberar Pontos** — libera pontos do programa de fidelidade
- **TEF - Buscar** — busca o registro do TEF antes de confirmar
- **Mobile** — operação via mobile
- **e-Sitef Express** — usar e-Sitef Express
- **Não Exib. Sangria** — não exibe na sangria do caixa
- **Obrigatório** — preenchimento obrigatório
- **Permitir Alteração** — permite alterar
- **HetoBank** — habilita integração com HetoBank (válido apenas para tipo `Pix`)

### Sub-aba `Troco`

- **Troco Só Visual** — quando o troco é apenas exibido
- **Troco Em Registro** — quando o troco é registrado no movimento
- **Opção**: `Só Visual` ou `Em Registro`
- **Gerar Crédito Pessoa** — gera crédito em nome da pessoa
- **Dinheiro** / **Crédito Pessoa** — formas de troco aceitas (uma delas é obrigatória quando o troco é `Em Registro`)

### Sub-aba `Cheque`

- **Contas a Pagar - Quitar Cheque tem que constar como Entrada**
- **Contas a Pagar - Compensar Cheque de Entrada ao Quitar**

### Sub-aba `Extras`

- **Quitar Contas Individual - Se Pagamento Único** — válido só para tipo `Dinheiro` ou `Outros`
- **Permissão (Pedi Autorização - PDV)**
- **Data Vencimento = Data Pré-Datado (Cheque Caixa Geral)**
- **Validar Forma de Pagamento para Impressão de Cupom Pós-Venda**

### Sub-aba `PDV`

- **Permitido PDV** — permite uso desta forma no PDV
- **Tipo Convênio** — marca como tipo convênio
- **Não Abrir Gaveta** — não abre a gaveta do caixa
- **Mostrar Detalhes Pagamento**
- **Pai Grupo** — quando esta forma é "pai" de um agrupamento de formas
- **Nº Grupo** — número do grupo (quando faz parte de agrupamento)
- **Mudar para Condição de Pagamento** — quando informada, força a operação a usar esta condição de pagamento (ver validação 8 abaixo)

### Sub-aba `TEF`

- **Enviar Parâmetro Crédito/Débito TEF Automático**
- **Parcelas TEF** — quantidade de parcelas (válido apenas para tipo `Cartão de Crédito` quando > 1)
- **Carteira Digital**

---

## 📝 Aba `Controle De Cartão` (grid de detalhes)

Disponível **apenas** para formas do tipo `Cartão de Crédito`, `Cartão de Débito`, `Pix` ou `Outros` (não para `Dinheiro` ou `Cheque`).

Cada linha do grid configura **uma regra de operadora de cartão** com os campos:

| Label | Observação |
|-------|------------|
| **Operadora de Cartão** | Pessoa (do tipo Fornecedor) que representa a operadora — exige Código TEF configurado nesse cadastro de pessoa |
| **De** / **Até** | Faixa de parcelas (ex.: `De 1 Até 1`, `De 2 Até 6`, `De 7 Até 12`) — permite cobrar taxas diferentes por número de parcelas |
| **Taxa %** | Percentual cobrado |
| **1º** | Dias até o crédito da 1ª parcela |
| **Demais** | Dias até o crédito das demais parcelas |
| **Plano de Contas** | Plano de contas a lançar a taxa cobrada |
| **Centro de Custo** | Centro de custo da taxa |
| **Caixa** | Caixa Geral usado |
| **Nº Lojas (formato `/1/2/`)** | Lista de empresas onde esta regra vale, sempre cercada por `/` (ex.: `/1/3/` para valer nas lojas 1 e 3) |
| **Cód. Adm** | Código administrador (preenchido automaticamente a partir da operadora) |
| **Vencimento "Sab/Dom"** | O que fazer quando o vencimento cai num final de semana: `Segunda-Feira` ou `Terça-Feira` |
| **Tarifa Fixa** | Tarifa fixa (em valor) cobrada |
| **Tarifa Máxima** | Limite máximo da tarifa |
| **Modo Parcelamento** | `LOJA` ou `ADMINISTRADORA` |
| **Apenas Dias Úteis** | Considera apenas dias úteis |
| **Compensar** | Compensar automaticamente |
| **Tarifa Mínima** | Aplica tarifa mínima |

O grid tem botões próprios: **Inserir**, **Atualizar**, **Deletar**, **Cancelar**.

> ℹ️ Ao salvar a forma, o sistema marca automaticamente o flag interno `Controlar Cartão` como ativo se houver pelo menos uma linha nesta aba. Não é necessário marcar manualmente.

---

## ✅ Regras de validação automática (ao salvar)

A função `Validar` da tela aplica as seguintes regras de forma rígida; o salvamento é abortado caso alguma falhe:

1. **Detalhes não podem estar em edição** — feche a edição em curso na aba `Controle De Cartão` antes de salvar.
2. **Campos obrigatórios preenchidos** — `Descrição`, `Tipo`, `Contas PR` etc.
3. **Descrição única** — não pode haver duas formas com a mesma `Descrição`. Mensagem: *"Descrição (VALOR) Já Existe!"*.
4. **Número único** — não pode haver duas formas com o mesmo `Código`. Mensagem: *"Código (VALOR) Já Existe!"*.
5. **Controle de Cartão exige tipo compatível** — se existir alguma linha em `Controle De Cartão`, o `Tipo` precisa ser `Cartão de Crédito`, `Cartão de Débito`, `Pix` ou `Outros`. Mensagem: *"Não permitido Controle De Cartão com esse tipo de pagamento!"*.
6. **Troco "Em Registro" exige forma** — se a `Opção` da sub-aba Troco está em `Em Registro`, pelo menos um entre `Dinheiro` e `Crédito Pessoa` precisa estar marcado.
7. **Detalhes de cartão implicam `Receber`** — quando há linhas em `Controle De Cartão`, `Contas PR` precisa ser `Receber`.
8. **`Quitar Contas Individual`** — só permitido para tipos `Dinheiro` ou `Outros`.
9. **Inativar — forma em uso em Tipos de Documentos** — não é possível inativar se a forma está vinculada a algum tipo de documento. Mensagem: *"Não permitido inativar! A forma de pagamento está sendo utilizada em Tipos de Documentos."*.
10. **`Parcelas TEF > 1` exige `Cartão de Crédito`** — para outras formas, mantenha em 1 (ou em branco).
11. **`HetoBank` exige `Pix`** — só pode marcar quando `Tipo = Pix`. Mensagem: *"Não permitido selecionar HetoBank com o tipo diferente de PIX"*.
12. **`Mudar para Condição de Pagamento` precisa estar autorizada** — se a condição escolhida tem uma lista restrita de formas, esta forma precisa estar nessa lista. Mensagem: *"Condição de Pagamento ... Não permite forma de pagamento ..."*.
13. **Inativar — forma em uso em Condição de Pagamento** — não é possível inativar se a forma está vinculada a alguma condição de pagamento. Mensagem: *"Não permitido inativar. A forma de Pagamento está sendo usada na configuração de Condição de Pagamento: ..."*.
14. **Confirmação ao clonar** — se você está clonando, o sistema confirma antes de salvar.

---

## 🚫 Regras de exclusão

A exclusão é bloqueada quando a forma está em uso. A tela verifica três tabelas antes de excluir:

| Situação | Mensagem |
|----------|----------|
| Existe **portador** vinculado a esta forma | *"Não permitido, Existe Portadores com esta Forma de Pagamento!"* |
| Existe **recebimento** com esta forma | *"Não permitido, Existe Recebimento(s) com esta Forma de Pagamento!"* |
| Existe **movimento** com esta forma usada como troco | *"Não permitido, Existe Movimento(s) com esta Forma de Pagamento!"* |

Em qualquer um desses casos, a forma deve ser **inativada** (com as ressalvas das validações 9 e 13 acima) em vez de excluída, preservando o histórico.

---

## 💡 Exemplos práticos

### Criar uma forma de pagamento "Dinheiro"

1. Pesquisa `F1` → digite `7` → abre o `Cadastro de Formas de Pagamento`.
2. Clique em **Novo** (o **Código** é preenchido automaticamente com o próximo disponível).
3. **Descrição**: `DINHEIRO`
4. **Contas PR**: `Ambos`
5. **Tipo**: `Dinheiro`
6. (Opcional) Configure `Troco`, `PDV` e outras opções conforme política da loja.
7. Salve.

### Criar uma forma de pagamento "Cartão de Crédito — Visa"

1. Cadastre a operadora (Visa) antes em **Pessoas** como pessoa do tipo **Fornecedor** com o **Código TEF** preenchido.
2. Pesquisa `F1` → digite `7` → abre o `Cadastro de Formas de Pagamento`.
3. Clique em **Novo**.
4. **Descrição**: `CARTAO DE CREDITO - VISA`
5. **Contas PR**: `Receber`
6. **Tipo**: `Cartão de Crédito`
7. Marque os checkboxes conforme operação (TEF, Fiscal, etc.).
8. Vá para a aba **Controle De Cartão** → **Inserir**:
   - **Operadora de Cartão**: selecione `VISA`
   - **De/Até**: `1` / `1` (regra para pagamento à vista)
   - **Taxa %**: percentual cobrado à vista
   - **1º** e **Demais**: dias até o crédito
   - **Plano de Contas**, **Centro de Custo**, **Caixa**: configurar lançamento da taxa
   - **Nº Lojas**: `/1/` (vale na loja 1) ou em branco para valer em todas
   - **Vencimento "Sab/Dom"**: `Segunda-Feira`
   - Em **Atualizar**.
9. Repita para outras faixas de parcelas (ex.: `De 2 Até 6`, `De 7 Até 12`) com taxas diferentes se for o caso.
10. Salve a forma.

### Criar uma forma de pagamento "PIX HetoBank"

1. Pesquisa `F1` → digite `7` → abre o cadastro.
2. Clique em **Novo**.
3. **Descrição**: `PIX HETOBANK`
4. **Contas PR**: `Receber`
5. **Tipo**: `Pix` (obrigatório para HetoBank)
6. Marque **HetoBank**.
7. Salve.

---

## ❓ FAQ / Problemas comuns

**Não consigo marcar `HetoBank`. O sistema bloqueia.**
HetoBank só é permitido para `Tipo = Pix`. Mude o tipo primeiro e tente novamente.

**Quero colocar 3 parcelas no TEF mas o sistema bloqueia.**
`Parcelas TEF > 1` só é permitido para `Tipo = Cartão de Crédito`. Para débito e PIX deixe em 1.

**Adicionei detalhes em `Controle De Cartão` mas mudei o tipo para `Cheque` e não salva.**
Correto: controle de cartão exige `Cartão de Crédito/Débito`, `Pix` ou `Outros`. Apague as linhas da aba Controle De Cartão antes de mudar para `Cheque` ou `Dinheiro`.

**Marquei `Quitar Contas Individual - Se Pagamento Único` e não salva.**
Esse flag só vale para `Tipo = Dinheiro` ou `Outros`. Para os demais tipos, deixe desmarcado.

**Tentei inativar e o sistema reclama de "Tipos de Documentos".**
A forma está sendo usada em algum tipo de documento (tela `82`). Remova essa vinculação antes ou ajuste no `Tipo de Documento`.

**Tentei inativar e o sistema reclama de "Condição de Pagamento".**
A forma está presente em alguma condição de pagamento (tela `8`). Abra a condição mencionada e remova esta forma de pagamento, depois inative.

**Não consigo excluir a forma.**
Há `Portadores`, `Recebimentos` ou `Movimentos` usando-a. Mantenha o cadastro e use a inativação (com as ressalvas das duas FAQs anteriores).

**O `Código` é editável?**
Sim. O sistema preenche com o próximo disponível ao clicar em **Novo**, mas você pode alterar. Apenas precisa ser único.

**O que significa `Nº Lojas` no formato `/1/2/`?**
É a lista de empresas onde aquela regra de operadora vale. Sempre cercada por `/`. Por exemplo: `/1/3/` significa "vale nas empresas 1 e 3". Deixar em branco geralmente significa "vale em todas".

**Onde configuro a operadora (ex.: Visa, Master, Cielo) que aparece em `Operadora de Cartão`?**
No cadastro de **Pessoas**, marcando a pessoa como **Fornecedor** e preenchendo o **Código TEF**. Sem o Código TEF preenchido, a operadora não é aceita aqui.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Relação |
|------|:---:|---------|
| Cond. de Pagamento | `8` | Forma pode ser obrigada a mudar para uma condição específica (sub-aba PDV) |
| [Portadores](documentacao_portadores.md) | `12` | Portadores referenciam forma (e bloqueiam exclusão) |
| Plano de Contas | `14` | Plano usado nas linhas de Controle De Cartão |
| Centros de Custos | `15` | Centro usado nas linhas de Controle De Cartão |
| Tipos de Contas PR | `82` | Vincula forma a tipo de documento (bloqueia inativação) |
| Caixa Geral | `13` | Caixa Geral usado nas linhas de Controle De Cartão |
| Operadoras Cartão | `122` | Cadastro auxiliar de operadoras |

---

## ⚠️ Limites desta documentação

Esta documentação foi construída a partir da inspeção direta do comportamento da tela no Sol.NET. **Não cobre**:

- **Regras automáticas que rodam dentro do banco de dados** ao salvar/alterar/excluir o registro — podem ajustar ou complementar o que está descrito aqui.
- **Comportamento detalhado de cada flag no PDV/TEF** — alguns flags ativam fluxos no PDV, no caixa ou na integração TEF que são tratados em outras telas.
- **Configuração da integração TEF/HetoBank** — esta documentação descreve apenas o que é configurado na forma de pagamento; a comunicação efetiva com os serviços externos é tratada em outras telas e depende de parâmetros do convênio.
- **Variações por release** — versões mais novas do Sol.NET podem ter campos adicionais.

Para informações fora desse escopo, consulte o suporte Hetosoft.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 5.0 (refeito do zero descartando a documentação anterior)
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo Financeiro
