---
title: "FAQ: Lançamentos de RH - Sol.NET"
permalink: /RH/faq/
---
# ❓ FAQ - Perguntas Frequentes: Lançamentos de RH

## 📑 Índice

- [🎯 Sobre o Módulo](#-sobre-o-módulo)
- [📝 Lançamentos](#-lançamentos)
- [�� Valores e Cálculos](#-valores-e-cálculos)
- [🔗 Integração com DRE](#-integração-com-dre)
- [👥 Cadastros](#-cadastros)
- [🛠️ Problemas Técnicos](#️-problemas-técnicos)

---

## 🎯 Sobre o Módulo

### **P: O que é o módulo RH do Sol.NET?**
**R:** É um módulo para **lançamento de valores** da folha de pagamento, com objetivo de integrar as despesas de RH com o DRE. Não é um sistema completo de folha de pagamento.

### **P: O que o módulo RH FAZ?**
**R:** 
- ✅ Registra valores de folha de pagamento
- ✅ Integra com DRE automaticamente
- ✅ Permite controle por centro de custo/departamento
- ✅ Gera relatórios de despesas com pessoal

### **P: O que o módulo RH NÃO FAZ?**
**R:**
- ❌ Cálculo de INSS, IRRF, FGTS
- ❌ Processamento de folha de pagamento
- ❌ Emissão de holerites
- ❌ Integração com eSocial ou órgãos externos
- ❌ Geração de guias de impostos
- ❌ Controle de ponto eletrônico
- ❌ Cálculo de férias ou rescisões

### **P: Preciso de um contador para usar o módulo RH?**
**R:** Sim. A contabilidade (escritório contábil) processa a folha completa e fornece os valores que você lança no Sol.NET.

### **P: O Sol.NET substitui um sistema de folha de pagamento?**
**R:** Não. O Sol.NET serve apenas para controle gerencial interno. Para processamento completo de folha, use um sistema especializado ou contrate uma contabilidade.

---

## 📝 Lançamentos

### **P: Como faço um lançamento de folha no Sol.NET?**
**R:**
1. Receba o resumo da contabilidade com valores por categoria
2. Menu RH → Lançamentos de Folha → Novo
3. Lance cada categoria (salários, encargos, benefícios)
4. Salve os lançamentos
5. Confira no DRE

### **P: Preciso lançar valor por valor de cada funcionário?**
**R:** Não. Lance apenas os **valores totais** por categoria e departamento. Exemplo:
- Total Salários Administrativo: R$ 50.000,00
- Total Encargos: R$ 14.000,00

Não é necessário detalhar por funcionário individual.

### **P: Com que frequência devo fazer lançamentos?**
**R:** Mensalmente, após receber as informações da contabilidade referentes à folha do mês.

### **P: Posso lançar valores estimados?**
**R:** Sim. Se a contabilidade atrasar, você pode lançar valores estimados baseados em meses anteriores. Depois ajuste com os valores reais.

### **P: Como corrijo um lançamento errado?**
**R:**
1. Menu RH → Lançamentos de Folha
2. Localize o lançamento
3. Edite ou exclua
4. Faça o lançamento correto
5. Regere o DRE para atualizar

### **P: Posso excluir lançamentos de meses anteriores?**
**R:** Tecnicamente sim, mas não é recomendado. Mantenha histórico de pelo menos 12 meses para análises comparativas.

### **P: Qual data devo usar nos lançamentos?**
**R:** Use o **último dia do mês de competência**. Exemplo: Para folha de março/2024, use data 31/03/2024.

---

## 💰 Valores e Cálculos

### **P: O Sol.NET calcula INSS, IRRF e FGTS automaticamente?**
**R:** **Não**. O Sol.NET não faz cálculos tributários. Você lança os valores que a contabilidade calculou e informou.

### **P: Como sei quais valores lançar?**
**R:** A contabilidade deve fornecer um resumo mensal do tipo:
```
Salários: R$ 50.000,00
Encargos INSS: R$ 11.000,00
FGTS: R$ 4.000,00
Benefícios: R$ 3.000,00
Provisão 13º: R$ 4.166,67
Provisão Férias: R$ 5.555,56
```

Lance esses valores exatamente como informados.

### **P: Preciso separar INSS de FGTS?**
**R:** Depende da sua necessidade gerencial. Você pode:
- Lançar tudo junto como "Encargos Sociais"
- Ou separar em contas diferentes (INSS, FGTS)

Consulte sua contabilidade sobre a melhor prática.

### **P: O que são provisões de 13º e férias?**
**R:** São valores que você lança mensalmente (1/12 do custo anual) para distribuir o impacto ao longo do ano. Assim o DRE fica mais realista.

**Exemplo:**
- Custo anual de 13º: R$ 50.000
- Provisão mensal: R$ 50.000 ÷ 12 = R$ 4.166,67

### **P: Sou obrigado a provisionar 13º e férias mensalmente?**
**R:** Não é obrigatório no Sol.NET, mas é uma boa prática gerencial. Consulte sua contabilidade.

### **P: Como calculo os valores de provisão?**
**R:** Não calcule. A contabilidade deve informar os valores corretos considerando todas as variáveis (médias, encargos, etc.).

---

## 🔗 Integração com DRE

### **P: Os lançamentos de RH aparecem automaticamente no DRE?**
**R:** Sim. Quando você lança com as contas contábeis corretas, os valores aparecem automaticamente no DRE do período.

### **P: Em que contas os lançamentos aparecem no DRE?**
**R:** Nas contas de despesa que você configurou:
```
6.2.01 - Salários
6.2.02 - Encargos Sociais
6.2.03 - Benefícios
6.2.04 - Provisão 13º
6.2.05 - Provisão Férias
```

### **P: Como vejo as despesas de RH separadas por departamento?**
**R:** 
1. Lance os valores com centro de custo diferente para cada departamento
2. No DRE, filtre ou visualize por centro de custo
3. O sistema mostrará os valores separados

### **P: Valores não aparecem no DRE, o que fazer?**
**R:** Verifique:
- A conta contábil usada está no plano de contas?
- O período do DRE corresponde à competência do lançamento?
- O lançamento foi salvo corretamente?
- A conta está vinculada a um agrupamento DRE?

### **P: Posso fazer lançamentos direto no módulo Financeiro?**
**R:** Sim. Em vez de usar RH → Lançamentos de Folha, você pode usar Financeiro → Lançamentos Contábeis. O efeito no DRE é o mesmo.

---

## 👥 Cadastros

### **P: Preciso cadastrar todos os funcionários no Sol.NET?**
**R:** Não é obrigatório. O cadastro de funcionários no Sol.NET é simplificado e serve apenas para controle interno. Cadastre se quiser ter uma lista de nomes e departamentos.

### **P: Quais informações são necessárias no cadastro?**
**R:** Mínimo:
- Nome do funcionário
- Departamento/Centro de custo
- Cargo (opcional)
- Status (Ativo/Inativo)

Não é necessário CPF, RG, dados bancários, etc.

### **P: Preciso cadastrar dependentes?**
**R:** Não. O Sol.NET não processa cálculos de IRRF ou salário família, então não precisa de informações de dependentes.

### **P: Como organizo funcionários por departamento?**
**R:**
1. Primeiro cadastre os departamentos: RH → Cadastros → Departamentos
2. Depois vincule cada funcionário a um departamento
3. Use isso para separar custos no DRE

### **P: O cadastro no Sol.NET precisa estar igual ao da contabilidade?**
**R:** Não necessariamente. Como você lança valores totais (não individuais), o cadastro detalhado fica com a contabilidade. No Sol.NET é apenas para controle interno.

---

## 🛠️ Problemas Técnicos

### **P: Lançamento aparece duplicado no DRE**
**R:** Você salvou o mesmo lançamento duas vezes. Solução:
1. RH → Lançamentos de Folha
2. Localize o duplicado
3. Exclua um deles
4. Regere o DRE

### **P: Total lançado diferente do informado pela contabilidade**
**R:** Confira:
1. Some todos os lançamentos do período
2. Compare categoria por categoria com o resumo da contabilidade
3. Verifique se não esqueceu de lançar alguma categoria
4. Confirme se não há lançamentos duplicados

### **P: Valores aparecendo no departamento/centro de custo errado**
**R:**
1. Edite o lançamento
2. Corrija o campo "Centro de Custo"
3. Salve
4. Regere o DRE

### **P: Não consigo excluir um lançamento**
**R:** Possíveis causas:
- Período já fechado contabilmente
- Falta de permissão de usuário
- Lançamento vinculado a outro módulo

Consulte o administrador do sistema.

### **P: Como desfaço todos os lançamentos de um mês?**
**R:** 
1. RH → Lançamentos de Folha
2. Filtre pela competência (mês/ano)
3. Selecione todos os lançamentos
4. Exclua em lote (se disponível) ou um por um
5. Refaça os lançamentos corretos

### **P: Posso importar lançamentos de uma planilha?**
**R:** Depende da versão do Sol.NET. Consulte a documentação técnica ou suporte para verificar se há funcionalidade de importação.

---

## 🎯 Cenários Específicos

### **P: Como lanço o 13º salário (1ª e 2ª parcela)?**
**R:** Há duas abordagens:

**Opção 1 - Com Provisão:**
- Todo mês: Provisiona 1/12 do custo
- Novembro (1ª parcela): Baixa 50% da provisão
- Dezembro (2ª parcela): Baixa 50% restante + encargos

**Opção 2 - Sem Provisão:**
- Novembro: Lança 50% do 13º
- Dezembro: Lança 50% restante + encargos

Consulte sua contabilidade sobre qual usar.

### **P: Como lanço férias pagas?**
**R:** Similar ao 13º:
- Se provisiona: Baixa da provisão quando paga
- Se não provisiona: Lança como despesa no mês de pagamento

A contabilidade deve informar os valores e forma de lançamento.

### **P: Como lanço rescisões?**
**R:** Lance as verbas rescisórias como despesa do mês:
```
D - 6.2.06 - Rescisões e Indenizações
C - 2.1.2.05 - Rescisões a Pagar
Valor: Conforme informado pela contabilidade
```

### **P: Empresa tem múltiplas filiais, como organizar?**
**R:**
1. Crie centros de custo para cada filial
2. Lance valores separadamente por filial
3. No DRE, filtre por centro de custo para análise individual
4. Ou visualize consolidado de todas as filiais

### **P: Como faço para comparar custo de RH mês a mês?**
**R:**
1. Menu Financeiro → DRE
2. Selecione "DRE Comparativo"
3. Escolha os períodos (ex: últimos 6 meses)
4. O sistema mostra evolução das despesas com pessoal

### **P: Como calculo o percentual de RH sobre a receita?**
**R:**
1. Gere o DRE do período
2. Visualize:
   - Total de Receitas: R$ X
   - Total Despesas RH: R$ Y
3. Calcule: (Y ÷ X) × 100 = percentual

Muitos DREs já mostram isso automaticamente como "Análise Vertical".

---

## 💡 Boas Práticas

### **P: Qual a melhor forma de organizar os lançamentos?**
**R:**
- Use históricos padronizados
- Separe por departamento/centro de custo
- Provisione mensalmente 13º e férias
- Confira sempre o DRE após lançar
- Mantenha documentação (resumo da contabilidade)

### **P: Devo lançar na data de pagamento ou competência?**
**R:** Use a data de **competência** (último dia do mês de referência da folha), não a data de pagamento. Isso garante que o DRE reflita corretamente as despesas do período.

### **P: Como garantir que não esqueço de lançar nenhum mês?**
**R:**
- Crie um checklist mensal
- Defina um responsável
- Estabeleça um prazo (ex: até dia 10 de cada mês)
- Confira o DRE mês a mês para identificar falhas

---

**📅 Última atualização**: Janeiro de 2025  
**🎯 Público-alvo**: Usuários do módulo RH Sol.NET

*Para dúvidas não cobertas neste FAQ, consulte a [Documentação Completa](Documentacao Folha de Pagamento.md) ou entre em contato com o suporte técnico.*
