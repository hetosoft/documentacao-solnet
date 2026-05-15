# ❓ FAQ — Cadastro de NCM

Respostas para as dúvidas que aparecem mais no dia a dia sobre o **Cadastro de NCM** (código `21`) e a **Tabela NCM** federal (código `121`) no Sol.NET.

Para a referência completa, consulte a [Documentação do Cadastro de NCM](documentacao_ncm.md).

---

## 📋 Conceito e diferenças

### ❓ Qual a diferença entre Cadastro de NCM (`21`) e Cadastro Tabela NCM (`121`)?

- **Cadastro de NCM (`21`)** é a **lista da sua empresa**: os NCMs que você de fato usa, com a parametrização tributária local (CST, alíquotas, MVA, CBS/IBS etc.). É essa lista que o cadastro de Produtos consulta.
- **Cadastro Tabela NCM (`121`)** é a **base federal**: tabela oficial publicada pela Receita, atualizada periodicamente. Ela é uma **fonte de consulta** — alimenta automaticamente a descrição, o tipo e o CNI quando você inclui um NCM novo no cadastro `21`, mas não armazena as regras tributárias da sua empresa.

### ❓ Por que existem dois cadastros separados?

Porque a parametrização tributária (CST, alíquotas, FCP, MVA…) é específica da empresa e do regime. A tabela oficial só publica o código e a descrição — quem decide como tributar é o configurador. Manter as duas separadas evita que uma atualização da base oficial sobrescreva configurações que a empresa ajustou.

### ❓ O que é o campo "Tipo"?

Indica se o NCM é de **Produto** ou **Serviço**. O valor é preenchido automaticamente quando o NCM é carregado da Tabela NCM `121` — você normalmente não digita manualmente.

### ❓ O que é o campo "CNI"?

CNI é o **Código de Não Incidência**, usado em produtos com tributação zerada, monofásica ou em suspensão. Também costuma vir preenchido a partir da Tabela NCM `121` quando aplicável.

### ❓ Para que serve o campo "EX"?

A EX é o **código de exceção do NCM** — usado quando um mesmo NCM precisa de desdobramento por finalidade ou característica do produto. Sem ela, a SEFAZ pode rejeitar a NF-e como "NCM inválido" mesmo que o código esteja correto.

---

## 🧮 Tributação clássica (aba `Principal`)

### ❓ Quando devo usar o combo "Tributação Federal" do cabeçalho?

Sempre que existir um **perfil pré-cadastrado** de PIS/COFINS/IPI que se aplique àquele NCM. Quando esse combo está preenchido, ele **prevalece** sobre os campos PIS/COFINS/IPI da aba `Principal` — esses campos viram fallback para quando o combo está vazio.

### ❓ Posso deixar o combo Tributação Federal vazio e usar só os campos da aba `Principal`?

Pode. É comum em empresas pequenas que não criaram perfis fiscais. Mas a maioria das implantações maiores prefere centralizar a parametrização em perfis (combo) para evitar que a mesma alíquota fique repetida em dezenas de NCMs.

### ❓ Quando o CSOSN é usado em vez do CST?

Quando a empresa é optante pelo **Simples Nacional**. O CST é usado em empresas do Lucro Real ou Lucro Presumido; o CSOSN, em empresas do Simples.

### ❓ Preciso preencher MVA se a operação não tem Substituição Tributária?

Não. Os campos de MVA (Margem de Valor Agregado) só fazem sentido em operações com ICMS-ST. Se o NCM não tem ST, deixe em branco.

### ❓ Como funciona o grupo "Crédito Outorgado"?

Alguns estados concedem **crédito presumido de ICMS** em operações específicas (geralmente para incentivar setores ou atividades). Os campos Crédito — Interno / Externo registram o percentual aplicável, e o Código do Crédito identifica o benefício fiscal que ampara a operação.

### ❓ Para que serve o "Código de Desoneração"?

Identifica o motivo legal da desoneração de ICMS quando o NCM tem alíquota reduzida ou zerada por decisão fiscal. Esse código é exigido no XML da NF-e.

---

## 🆕 Reforma Tributária (aba `IVA`)

### ❓ O que significa "IVA" no nome da aba?

**IVA** é **Imposto sobre Valor Agregado** — o conceito que está por trás da Reforma Tributária brasileira (EC 132/2023). A aba traz os parâmetros dos dois novos tributos: CBS (federal) e IBS (estadual + municipal).

### ❓ A aba `IVA` substitui a aba `Principal`?

Não — pelo menos não imediatamente. Durante o **período de transição (2026–2033)**, as duas convivem: a `Principal` continua valendo para os impostos atuais (ICMS, PIS/COFINS, IPI) e a `IVA` passa a valer conforme as fases da Reforma vão entrando em vigor. Quando a Reforma estiver plenamente implementada, a aba `Principal` perde uso para a maioria dos casos.

Consulte a [Documentação da Reforma Tributária](documentacao_reforma_tributaria.md) para o cronograma completo.

### ❓ Onde configuro a alíquota CBS — no Tributação Federal ou na aba IVA?

Sempre na **aba IVA**. O combo `Tributação Federal` do cabeçalho continua sendo usado apenas para PIS/COFINS e IPI (regime antigo). CBS é um tributo da Reforma e mora em outra estrutura.

### ❓ O que é o "Código Classificação" da aba IVA?

É a **Classificação Tributária** (`cClassTrib`) — um código fiscal de 6 caracteres que vai no XML dos novos documentos fiscais da Reforma. Identifica a regra tributária CBS/IBS aplicável àquele NCM.

### ❓ Quando preencher Redução de Alíquota CBS / IBS?

Quando o NCM se enquadra em algum **regime diferenciado** previsto na Reforma — cesta básica, medicamentos, setores específicos, regime simplificado etc. A **Alíquota** continua sendo a cheia; a **Redução** é o percentual descontado.

### ❓ O IBS tem duas partes (UF e Município) — preciso preencher as duas?

Sim. O IBS substitui simultaneamente o ICMS (estadual) e o ISS (municipal), então a alíquota é composta por uma parte estadual (UF) e uma parte municipal. Cada UF e município define a sua parte, dentro do teto fixado pela LC.

---

## 🚧 SEFAZ rejeitou — o que fazer

### ❓ Recebi um retorno "NCM inválido" na transmissão da NF-e. O que verificar?

Em ordem de probabilidade:

1. **Falta a EX** — confira se o NCM tem código de exceção na tabela da Receita e preencha o campo correspondente.
2. **NCM desatualizado** — confira se o código existe na Tabela NCM `121`. Se não existir, peça atualização da base à Hetosoft.
3. **CST incompatível** — em alguns casos a SEFAZ rejeita combinação de NCM + CST que ela considera inconsistente.
4. **Marque o NCM como inválido** no grupo `SEFAZ REJEITOU` e cole o retorno no campo correspondente — isso evita reenvio enquanto a regularização não termina.

### ❓ Como desmarco "NCM Inválido" depois de regularizar?

Edite o registro, desmarque o checkbox **NCM Inválido**, limpe (ou mantenha como histórico) o campo **Retorno da NF-e/NFC-e** e salve. O NCM volta a ser aceito nas próximas emissões.

---

## 🔁 Tabela NCM federal

### ❓ Quem atualiza a Tabela NCM (`121`)?

Normalmente a **Hetosoft** publica a atualização junto com versões do sistema, refletindo as publicações da Receita. Em algumas implantações, a equipe interna de TI da empresa também pode atualizar manualmente.

### ❓ Encontrei um NCM no cadastro `21` que não existe mais na tabela da Receita. Como tratar?

Cenário comum quando a Receita reorganiza a NCM. Verifique na Tabela NCM `121` se o código foi substituído por outro. Se foi:

1. Cadastre o NCM novo no `21` com a parametrização equivalente.
2. Reaponte os produtos afetados para o NCM novo (no cadastro de Produtos, código `32`).
3. Marque o NCM antigo como inválido para evitar uso indevido.

### ❓ Posso editar manualmente a Tabela NCM `121` ou só consultar?

Em geral, esse cadastro é mantido pela Hetosoft. Edições manuais são possíveis, mas não recomendadas — qualquer atualização futura da base pode sobrescrever o ajuste. Quando precisar de uma correção, abra um chamado.

---

## 🏢 Multi-empresa e operação

### ❓ O cadastro de NCM é compartilhado entre filiais?

Sim. O Cadastro de NCM (`21`) é único para todas as filiais da empresa no Sol.NET. As regras que variam por estado vão para as telas de **Região ICMS Saída** (`93`) e **Região ICMS ST Saída** (`94`), referenciadas pelo NCM.

### ❓ Como vincular um NCM ao produto?

No cadastro de Produtos (código `32`), há um campo de NCM que abre o seletor para a lista do `21`. Cada produto aponta para exatamente um NCM, e é dali que o sistema busca a regra tributária no momento da emissão.

### ❓ Posso ter dois NCMs idênticos com configurações diferentes?

Não — a combinação **NCM + EX** é única no cadastro `21`. Se você precisa de duas regras diferentes para o mesmo código, é provavelmente porque ele tem EX distintas (uma "00" e outras numeradas) — cada uma vira um registro próprio.

---

## 🔗 Telas e documentos relacionados

- **[Documentação do Cadastro de NCM](documentacao_ncm.md)** — referência completa
- **[Guia Rápido — Cadastro de NCM](guia_rapido_ncm.md)** — checklist da rotina
- **[Reforma Tributária — Documentação](documentacao_reforma_tributaria.md)** — contexto da CBS/IBS
- **Região ICMS Saída** (`93`) — regras de ICMS por região
- **Região ICMS ST Saída** (`94`) — regras de Substituição Tributária por região
- **Natureza de Operação** (`36`) — classificação fiscal de cada movimento
- **Cadastro de Produtos** (`32`) — onde o NCM é vinculado ao produto

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Configuradores fiscais, contadores e equipe de suporte
