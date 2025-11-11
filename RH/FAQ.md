---
title: "FAQ: Lançamentos de RH - Sol.NET"
permalink: /RH/faq/
---
# ❓ FAQ - Perguntas Frequentes: Lançamentos de RH

## 🎯 Regra Fundamental

**⚠️ TODO LANÇAMENTO DE RH DEVE ESTAR VINCULADO A UM FUNCIONÁRIO ESPECÍFICO**

Não é possível lançar valores totais sem associação a funcionários individuais.

---

## 📑 Índice

- [🎯 Sobre Vinculação a Funcionários](#-sobre-vinculação-a-funcionários)
- [👥 Cadastro de Funcionários](#-cadastro-de-funcionários)
- [📝 Lançamentos](#-lançamentos)
- [💰 Valores](#-valores)
- [🔗 Integração com DRE](#-integração-com-dre)
- [🛠️ Problemas Técnicos](#️-problemas-técnicos)

---

## 🎯 Sobre Vinculação a Funcionários

### **P: Posso lançar valores totais da folha sem vincular a funcionários?**
**R:** **NÃO**. Todo lançamento no módulo RH do Sol.NET **deve estar vinculado a um funcionário específico**. Esta é uma característica obrigatória do sistema.

### **P: Por que preciso vincular cada lançamento a um funcionário?**
**R:** 
- O sistema foi projetado para controle detalhado por funcionário
- Permite análises individuais e por departamento
- Facilita relatórios gerenciais específicos
- Mantém rastreabilidade dos custos

### **P: Posso lançar um valor total para todo o departamento?**
**R:** **NÃO**. Você deve lançar individualmente para cada funcionário do departamento. O sistema então totaliza automaticamente por departamento no DRE.

### **P: A contabilidade me passou só valores totais. E agora?**
**R:** Solicite à contabilidade uma **planilha detalhada com valores individuais de cada funcionário**. Explique que o Sol.NET exige essa informação para funcionar corretamente. Não há como contornar esta exigência.

### **P: Quantos lançamentos preciso fazer por mês?**
**R:** Um conjunto de lançamentos (salário, encargos, benefícios) **para cada funcionário** da folha. Exemplo: empresa com 10 funcionários = 10 conjuntos de lançamentos.

---

## 👥 Cadastro de Funcionários

### **P: Preciso cadastrar todos os funcionários antes de lançar?**
**R:** **SIM, obrigatoriamente**. Você não conseguirá fazer lançamentos sem ter os funcionários cadastrados, pois cada lançamento precisa estar vinculado a um funcionário existente.

### **P: Quais informações são obrigatórias no cadastro?**
**R:** Informações essenciais:
- Nome completo
- CPF (identificação única)
- Matrícula
- Departamento/Setor
- Centro de Custo
- Contas Contábeis (Salário, Encargos, Benefícios)
- Status (Ativo/Inativo)

### **P: Como cadastro um funcionário?**
**R:**
1. Menu RH → Cadastros → Funcionários
2. Clicar em "Novo"
3. Preencher dados pessoais (nome, CPF, matrícula)
4. Preencher dados trabalhistas (admissão, cargo, departamento)
5. Configurar contas contábeis e centro de custo
6. Salvar

Veja detalhes em: [Cadastro de Funcionários](Documentacao Folha de Pagamento.md#-cadastro-de-funcionários-pessoa-rh)

### **P: Preciso cadastrar funcionários demitidos?**
**R:** Sim, mas altere o status para "Inativo" e informe a data de demissão. Mantenha o cadastro para histórico.

### **P: Posso ter dois funcionários com mesmo nome?**
**R:** Sim, cada funcionário é identificado unicamente por CPF e Matrícula, não pelo nome.

### **P: O que acontece se eu não configurar as contas contábeis no cadastro?**
**R:** Os lançamentos não saberão para quais contas do DRE devem ir. Configure sempre as contas contábeis no cadastro do funcionário.

---

## 📝 Lançamentos

### **P: Como faço um lançamento de folha?**
**R:**
1. Menu RH → Lançamentos de Folha → Novo
2. **Selecionar o funcionário** (obrigatório)
3. Informar competência (mês/ano)
4. Lançar valores (salário, encargos, benefícios)
5. Salvar
6. **Repetir para cada funcionário**

### **P: Preciso lançar funcionário por funcionário?**
**R:** **SIM**. Cada funcionário da folha precisa ter seus lançamentos individuais. Não há atalho para lançamento em lote.

### **P: Posso fazer um lançamento sem selecionar funcionário?**
**R:** **NÃO**. O sistema não permitirá salvar. A vinculação ao funcionário é campo obrigatório.

### **P: Como sei quais valores lançar para cada funcionário?**
**R:** A contabilidade deve fornecer uma planilha detalhada do tipo:
```
Funcionário: João Silva
- Salário: R$ 5.000,00
- INSS: R$ 1.000,00
- FGTS: R$ 400,00

Funcionário: Maria Santos
- Salário: R$ 3.500,00
- INSS: R$ 700,00
- FGTS: R$ 280,00
...
```

### **P: Quantos lançamentos faço por funcionário?**
**R:** Depende da folha. Tipicamente:
- 1 lançamento de salário
- 1 lançamento de INSS patronal
- 1 lançamento de FGTS
- Lançamentos adicionais: comissões, horas extras, benefícios (conforme o caso)

### **P: Posso editar um lançamento já feito?**
**R:** Sim. Localize o lançamento em RH → Lançamentos, edite os valores e salve.

### **P: Como corrijo um lançamento feito no funcionário errado?**
**R:** Você precisa:
1. Excluir o lançamento incorreto
2. Criar novo lançamento vinculado ao funcionário correto

---

## 💰 Valores

### **P: O Sol.NET calcula os valores automaticamente?**
**R:** **NÃO**. O Sol.NET não calcula INSS, IRRF, FGTS ou qualquer outro valor. Você lança os valores que a contabilidade calculou e informou.

### **P: Preciso saber quanto cada funcionário ganha?**
**R:** Não necessariamente para o cadastro inicial, mas sim para os lançamentos mensais. A contabilidade deve fornecer os valores exatos de cada funcionário.

### **P: Os valores variam de funcionário para funcionário?**
**R:** Sim, cada funcionário tem seus próprios valores de salário, encargos e benefícios. Por isso cada um precisa ter lançamentos individuais.

### **P: Como lanço provisões (13º e férias)?**
**R:** Também **por funcionário**:
- Calcule 1/12 do salário + encargos de cada funcionário
- Lance individualmente para cada um
- O sistema totaliza no DRE

---

## 🔗 Integração com DRE

### **P: Como os lançamentos por funcionário aparecem no DRE?**
**R:** O sistema soma automaticamente todos os lançamentos:
- Funcionários do mesmo departamento
- Na mesma conta contábil
- Do mesmo período

Resultado: total por departamento no DRE.

### **P: Posso ver despesas por funcionário individual no DRE?**
**R:** O DRE mostra totais por conta e centro de custo. Para detalhamento por funcionário, use os relatórios específicos de RH.

### **P: Valores aparecem no departamento errado, como corrijo?**
**R:** O departamento vem do cadastro do funcionário. Corrija:
1. RH → Cadastros → Funcionários
2. Edite o funcionário
3. Corrija o centro de custo
4. Próximos lançamentos irão para o centro correto

### **P: O total no DRE não bate com a contabilidade**
**R:** Verifique:
- Lançou todos os funcionários?
- Valores individuais estão corretos?
- Não há lançamentos duplicados?
- Competência está correta?

---

## 🛠️ Problemas Técnicos

### **P: Erro ao salvar: "Funcionário não informado"**
**R:** Você esqueceu de selecionar o funcionário. Selecione no campo apropriado antes de salvar.

### **P: Funcionário não aparece na lista para seleção**
**R:** Possíveis causas:
- Funcionário não cadastrado → Cadastre primeiro
- Funcionário inativo → Ative em Cadastros
- Filtro ativo → Remova filtros de pesquisa

### **P: Não consigo editar dados do funcionário**
**R:** Verifique:
- Tem permissão para editar cadastros?
- Funcionário não está em uso em lançamento em edição?
- Sistema não está em modo somente leitura?

### **P: Total por departamento está errado**
**R:** Confira:
1. Centro de custo de cada funcionário está correto?
2. Todos os funcionários do departamento foram lançados?
3. Não há funcionários do departamento em centro de custo errado?

### **P: Valores duplicados no DRE**
**R:** Você lançou o mesmo funcionário duas vezes. Exclua os lançamentos duplicados.

### **P: Como desfaço todos os lançamentos do mês?**
**R:** 
1. RH → Lançamentos
2. Filtre por competência
3. Exclua lançamento por lançamento (de cada funcionário)
4. Refaça os lançamentos corretos

---

## 🎯 Cenários Específicos

### **P: Funcionário mudou de departamento no meio do mês**
**R:** 
- Atualize o cadastro com o novo departamento
- Lançamentos futuros irão para o novo centro de custo
- Lançamentos anteriores permanecem no centro antigo

### **P: Funcionário foi admitido no meio do mês**
**R:**
1. Cadastre o funcionário
2. Lance os valores proporcionais informados pela contabilidade
3. Valores proporcionais já calculados pela contabilidade

### **P: Funcionário foi demitido no meio do mês**
**R:**
1. Lance os valores até a demissão (informados pela contabilidade)
2. Lance verbas rescisórias (se houver)
3. Altere status para "Inativo" e informe data de demissão

### **P: Empresa tem 100 funcionários. Preciso lançar os 100?**
**R:** **SIM**. Cada um dos 100 funcionários precisa ter seus lançamentos individuais. É trabalhoso, mas é assim que o sistema funciona.

### **P: Posso importar de uma planilha Excel?**
**R:** Verifique com o suporte técnico se há funcionalidade de importação. Se houver, ainda assim cada linha da planilha representará um funcionário.

### **P: Como facilito o trabalho com muitos funcionários?**
**R:**
- Organize a planilha da contabilidade por ordem alfabética
- Lance na mesma ordem
- Use checklist para marcar funcionários já lançados
- Divida o trabalho por departamento
- Confira totais por departamento antes de passar para o próximo

---

## 💡 Boas Práticas

### **P: Qual a melhor forma de organizar os lançamentos?**
**R:**
1. Cadastre todos os funcionários primeiro
2. Configure contas contábeis no cadastro
3. Organize planilha da contabilidade por departamento
4. Lance departamento por departamento
5. Confira total de cada departamento antes de passar ao próximo
6. Confira total geral no final

### **P: Como evito erros?**
**R:**
- Confira nome e matrícula antes de lançar
- Use checklist dos funcionários
- Lance em ambiente silencioso
- Peça segunda pessoa para conferir
- Compare totais por departamento com contabilidade

### **P: Como preparo a contabilidade para fornecer dados corretos?**
**R:** Explique que precisa de:
- Planilha com nome e matrícula de cada funcionário
- Valores individuais de cada um
- Separado por tipo (salário, encargos, benefícios)
- Total por funcionário e total geral

---

**📅 Última atualização**: Janeiro de 2025  
**🎯 Público-alvo**: Usuários do módulo RH Sol.NET  
**⚠️ Lembre-se: Vinculação a funcionário é OBRIGATÓRIA**

*Para informações detalhadas sobre cadastro de funcionários, consulte a [Documentação Completa - Cadastro de Pessoa RH](Documentacao Folha de Pagamento.md#-cadastro-de-funcionários-pessoa-rh).*
