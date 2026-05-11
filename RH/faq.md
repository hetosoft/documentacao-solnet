---
title: "FAQ: Lançamentos de RH - Sol.NET"
permalink: /RH/faq/
---
# ❓ FAQ: Lançamentos de RH

## 🎯 Regra fundamental

**Todo lançamento de RH é vinculado a uma pessoa** (funcionário), e essa pessoa precisa estar cadastrada na tela `Cadastro de Pessoas` (código `5`) com a classificação **`Funcionário`**.

---

## 📑 Índice

- [🧭 Onde fica cada tela](#-onde-fica-cada-tela)
- [👥 Cadastro de Funcionários](#-cadastro-de-funcionários)
- [📝 Lançamentos](#-lançamentos)
- [💰 Valores](#-valores)
- [🗂️ Configuração RH e modelos recorrentes](#-configuração-rh-e-modelos-recorrentes)
- [💳 Integração com Contas a Pagar/Receber](#-integração-com-contas-a-pagarreceber)
- [📊 Integração com o DRE](#-integração-com-o-dre)
- [📥 Holerite Excel](#-holerite-excel)
- [🛠️ Problemas técnicos](#-problemas-técnicos)
- [🎯 Cenários específicos](#-cenários-específicos)

---

## 🧭 Onde fica cada tela

### **P: Como abro qualquer tela do Sol.NET?**

**R:** Pressione **`F1`** em qualquer parte do sistema — abre a pesquisa universal. Digite o **código** da tela (ex.: `84`) ou parte do **nome** (ex.: "Lançamento de RH") e confirme.

### **P: Quais são as telas do módulo RH?**

**R:** As principais:

- **`Cadastro de Pessoas`** — código `5` (cadastra funcionários)
- **`Cadastro de Lançamento de RH`** — código `84` (lança os valores mensais)
- **`Configuração RH`** — código `222` (modelos recorrentes)
- **`Holerite Excel`** — código `134` (importa planilhas de holerite)
- **`Pessoa Rateio`** — código `133` (modelos de rateio por pessoa)

### **P: Existe uma tela chamada "Cadastro de Funcionários"?**

**R:** **Não existe** uma tela dedicada. Funcionários são cadastrados na própria tela **`Cadastro de Pessoas`** (código `5`), marcando a pessoa com a classificação `Funcionário`.

---

## 👥 Cadastro de Funcionários

### **P: Como cadastro um novo funcionário?**

**R:**

1. Abra a pesquisa `F1`, digite `5` (ou "Pessoas") e abra **`Cadastro de Pessoas`**.
2. Crie um novo registro.
3. Preencha **dados pessoais** (nome, CPF, contato).
4. Marque a **classificação** como `Funcionário`.
5. Defina o **Centro de Custo** padrão (importante para o DRE).
6. Salve.

### **P: Preciso preencher todos os campos da pessoa?**

**R:** Os essenciais para o módulo RH são: nome, CPF, classificação `Funcionário` e centro de custo. Os demais (endereço, contatos, observações) são úteis para a gestão, mas não interferem na contabilização.

### **P: Como trato um funcionário desligado?**

**R:** Mantenha o registro em `Cadastro de Pessoas` (código `5`) para preservar histórico, mas inative o registro. Ele deixa de aparecer nas listas de seleção do lançamento mensal sem perder os dados antigos.

### **P: Posso ter dois funcionários com o mesmo nome?**

**R:** Sim. Cada pessoa é identificada de forma única pelo seu código interno (e CPF). O nome é apenas descritivo.

---

## 📝 Lançamentos

### **P: Como faço o lançamento mensal de um funcionário?**

**R:**

1. `F1` → `84` → abre **`Cadastro de Lançamento de RH`**.
2. Aba **`Registro → Principal`**: preencha `Competência` e selecione `Pessoas`.
3. Insira uma linha para cada evento (salário, encargos, descontos, benefícios) com `Valor`, `Plano de Contas`, `Centro de Custo`, `Tipo de Conta`, `Operação`.
4. Se houver rateio, vá na aba `Rateio` e distribua o valor.
5. Se quiser gerar título financeiro, vá na aba `ContasPR - Manual` e clique em `Criar`.
6. Salve.

### **P: Posso lançar um valor total para todo o departamento?**

**R:** **Não**. O lançamento exige vínculo com uma pessoa. O sistema então totaliza por centro de custo no DRE com base na soma dos lançamentos individuais.

### **P: Posso lançar sem selecionar a pessoa?**

**R:** Não. O campo `Pessoas` é obrigatório — sem ele o sistema não fecha o registro.

### **P: Quantas linhas faço por funcionário?**

**R:** Depende dos eventos do mês. Tipicamente:

- 1 linha por evento de **vencimento** (salário, comissões, horas extras…)
- 1 linha por **desconto** (INSS, IRRF, vale-transporte…)
- 1 linha por **encargo patronal** (INSS patronal, FGTS…)
- 1 linha por **benefício** custeado pela empresa

Não há limite — quanto mais detalhe, melhor a análise no DRE.

### **P: Posso editar um lançamento já salvo?**

**R:** Sim. Localize o registro pela aba `Pesquisar` da tela `84`, abra o registro, ajuste o que for necessário e salve.

### **P: Lancei no funcionário errado, como corrijo?**

**R:** Edite o lançamento e corrija o campo `Pessoas`, ou exclua o lançamento e crie um novo no funcionário certo.

### **P: O que é a aba `Lançamento em Massa`?**

**R:** Permite inserir/excluir várias linhas de uma vez. Útil quando o mesmo evento se repete para vários funcionários — por exemplo, lançar o FGTS de todos no mesmo movimento. Mesmo assim cada linha continua vinculada a uma pessoa específica.

---

## 💰 Valores

### **P: O Sol.NET calcula INSS, IRRF, FGTS?**

**R:** **Não**. Os valores vêm prontos da contabilidade externa. O Sol.NET registra os valores informados e os organiza contabilmente.

### **P: Como lanço provisões (13º e férias)?**

**R:** Como qualquer outro lançamento de RH: uma linha por funcionário, com o valor da provisão (1/12 do salário mais encargos, por exemplo), `Plano de Contas` de provisão e `Centro de Custo` adequado. Para automatizar, cadastre a provisão em `Configuração RH` (código `222`).

### **P: A contabilidade só me envia o total. O que faço?**

**R:** Solicite o detalhamento por funcionário. Sem ele o módulo não consegue alimentar o DRE por centro de custo nem gerar títulos individuais em Contas a Pagar — todo o valor agregado perde rastreabilidade.

---

## 🗂️ Configuração RH e modelos recorrentes

### **P: Para que serve a `Configuração RH` (código `222`)?**

**R:** Para criar **modelos de lançamento recorrente** — itens fixos que se repetem todo mês (salário base, vale-transporte patronal, plano de saúde). Cada modelo guarda `Pessoas`, `Valor`, `Plano de Contas`, `Centro de Custo`, `Operação`, vigência (`Data Mês Início`/`Data Mês Fim`), `Dia` da competência, opção `Proporcional`, `Criar PR` (gerar ou não Contas a Pagar) e até o **rateio** padrão.

### **P: Preciso usar `Configuração RH`?**

**R:** Não é obrigatório, mas economiza muito tempo. Para empresas com poucos funcionários e folha estável, vale a pena cadastrar os itens fixos como modelos.

### **P: O modelo está vencido — o lançamento parou de aparecer**

**R:** Confira a vigência do modelo em `Configuração RH` (código `222`). Se a `Data Mês Fim` é anterior à competência atual, prorrogue ou crie um novo modelo.

---

## 💳 Integração com Contas a Pagar/Receber

### **P: Como o lançamento de RH gera um título no financeiro?**

**R:** Pela aba **`Registro → ContasPR - Manual`** da tela `Cadastro de Lançamento de RH` (código `84`). Preencha `Tipo de Documento`, `Portador`, `Vencimento` e clique em **`Criar`** — o título aparece no módulo financeiro.

### **P: Sou obrigado a gerar título de Contas a Pagar?**

**R:** Não. Se o objetivo é apenas o controle gerencial via DRE, basta salvar o lançamento sem usar a aba `ContasPR - Manual`. A geração de título é opcional, decidida lançamento a lançamento.

### **P: Já salvei o lançamento e esqueci de criar o título — perdi?**

**R:** Não. Reabra o lançamento pela aba `Pesquisar`, vá em `ContasPR - Manual`, preencha os campos e clique em `Criar`.

---

## 📊 Integração com o DRE

### **P: Como os valores aparecem no DRE?**

**R:** O sistema soma automaticamente os lançamentos por **Plano de Contas** + **Centro de Custo** + **Competência**. O DRE mostra os totais consolidados.

### **P: Posso ver gasto por funcionário individual no DRE?**

**R:** O DRE consolida por conta e centro de custo. Para ver por funcionário, use a aba `Pesquisar` da tela `84` filtrando por `Pessoas`.

### **P: Valor caiu no centro de custo errado**

**R:** Causa típica: o centro de custo cadastrado na pessoa estava errado. Corrija no `Cadastro de Pessoas` (código `5`) para que **novos** lançamentos peguem o centro certo, e ajuste manualmente o lançamento já feito (edite a linha ou use rateio).

### **P: O total do DRE não bate com a contabilidade**

**R:** Verifique:

- Algum funcionário não foi lançado?
- Existe lançamento duplicado?
- Os valores foram digitados corretamente?
- A competência está correta?

Filtre os lançamentos do mês na aba `Pesquisar` da tela `84` e compare linha por linha com a planilha da contabilidade.

---

## 📥 Holerite Excel

### **P: O Sol.NET emite holerite?**

**R:** O Sol.NET **não calcula nem emite** holerites — o cálculo continua sendo da contabilidade ou de software dedicado de folha. **O que existe** é a tela **`Holerite Excel`** (código `134`), que **importa** holerites a partir de planilha Excel para complementar os lançamentos contábeis do módulo.

### **P: Como uso a tela `Holerite Excel` (código `134`)?**

**R:**

1. `F1` → `134` → abre **`Holerite Excel`**.
2. Importe a planilha no layout aceito (confirme com o suporte o template vigente para sua versão).
3. Após a importação, confira que os funcionários e valores chegaram corretamente.

### **P: A importação substitui o lançamento manual da tela 84?**

**R:** Não necessariamente — a `Holerite Excel` serve como fonte de dados e ponto de conferência. Os lançamentos contábeis (Plano de Contas, Centro de Custo, integração com ContasPR) continuam sendo trabalhados na tela `84`.

---

## 🛠️ Problemas técnicos

### **P: "Funcionário não informado" ao salvar**

**R:** Selecione o funcionário no campo `Pessoas` na aba `Registro → Principal`.

### **P: Funcionário não aparece na pesquisa**

**R:** Possíveis causas:

- Não cadastrado em `Cadastro de Pessoas` (código `5`)
- Marcado como inativo
- Sem a classificação `Funcionário`
- Filtro de pesquisa ativo na aba `Pesquisar` da tela `84`

### **P: Mensagem de "Diferença" no rateio**

**R:** A soma das linhas de rateio precisa ser igual ao valor total do lançamento. Ajuste valores ou percentuais até zerar o campo `Diferença` na aba `Rateio`.

### **P: Valor duplicado no DRE**

**R:** O lançamento foi feito duas vezes para o mesmo funcionário/competência. Filtre pela aba `Pesquisar` da tela `84` (Competência + Pessoas) e exclua o duplicado.

### **P: Como desfaço todos os lançamentos de um mês?**

**R:**

1. Filtre por competência na aba `Pesquisar` da tela `84`.
2. Exclua cada lançamento (ou use ação em lote, se a tela oferecer).
3. Refaça os lançamentos corretos.

Se o lançamento já gerou ContasPR, providencie também a exclusão/baixa do título no módulo financeiro.

---

## 🎯 Cenários específicos

### **P: Funcionário mudou de departamento no meio do mês**

**R:** Ajuste o **Centro de Custo** no `Cadastro de Pessoas` (código `5`). Lançamentos futuros herdam o novo centro. Para o mês de transição, edite manualmente o lançamento (ou faça rateio) para refletir o tempo em cada centro de custo.

### **P: Funcionário admitido no meio do mês**

**R:**

1. Inclua o registro em `Cadastro de Pessoas` (código `5`) com classificação `Funcionário`.
2. Lance os valores proporcionais que a contabilidade informar.
3. (Opcional) Cadastre o modelo recorrente em `Configuração RH` (código `222`) marcando `Proporcional` se for o caso.

### **P: Funcionário demitido no meio do mês**

**R:**

1. Lance os valores até a demissão (informados pela contabilidade).
2. Lance verbas rescisórias como lançamentos adicionais.
3. Atualize o status do registro em `Cadastro de Pessoas` (código `5`) para inativo.

### **P: Empresa com 100 funcionários — preciso lançar todos individualmente?**

**R:** Sim, cada funcionário tem seu lançamento. Para escalar:

- Use `Configuração RH` (código `222`) para os itens fixos — eles deixam de ser digitados manualmente.
- Use a aba `Lançamento em Massa` da tela `84` para os eventos repetitivos do mês (ex.: FGTS).
- Use `Holerite Excel` (código `134`) quando a contabilidade fornecer os dados em planilha.

### **P: Posso importar lançamentos de planilha Excel?**

**R:** Sim — a tela **`Holerite Excel`** (código `134`) faz isso. Confirme com o suporte o template de planilha aceito.

---

## 💡 Boas práticas

- **Cadastre primeiro, lance depois.** Funcionários novos sempre antes do primeiro lançamento do mês.
- **Configure Centro de Custo no cadastro da pessoa.** Reduz erros e padroniza o DRE.
- **Modelos recorrentes para itens fixos.** Salário, vale-transporte, plano de saúde — tudo em `Configuração RH` (código `222`).
- **Padronize descrições.** Mesmas palavras para o mesmo evento — facilita filtros e relatórios.
- **Confira incrementalmente.** Departamento por departamento, não espere o mês inteiro.
- **Quatro olhos no fechamento.** Conferir o DRE antes de declarar o mês fechado evita retrabalho.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 2.0
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo RH

*Para detalhes técnicos completos, consulte a **[Documentação principal](documentacao_folha_de_pagamento.md)** e o **[Processo Mensal](processo_mensal.md)**.*
