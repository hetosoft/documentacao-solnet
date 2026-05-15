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

Indica se o NCM é de **Produto** ou **Serviço**. É um campo **somente leitura** preenchido automaticamente quando o NCM é carregado da Tabela NCM `121`. Você não digita manualmente.

### ❓ O que é o campo "CNI"?

CNI é o **Código Não Incidência**, usado em produtos com tributação zerada, monofásica ou em suspensão. **É preenchido manualmente pelo configurador** — diferente da Descrição, EX e Tipo, ele **não vem** automaticamente da Tabela NCM `121`.

### ❓ Para que serve o campo "EX"?

A EX é o **código de exceção do NCM** — usado quando um mesmo NCM precisa de desdobramento por finalidade ou característica do produto. Sem ela, a SEFAZ pode rejeitar a NF-e como "NCM inválido" mesmo que o código esteja correto.

---

## 🧮 Tributação clássica (aba `Principal`)

### ❓ Como o combo "Tributação Federal" do cabeçalho se relaciona com os campos da aba?

O combo é um **atalho de preenchimento**, não uma regra de prioridade. Ao selecionar um perfil:

- O sistema **copia** para os campos da aba `Principal` os valores do perfil: CST PIS/COFINS Entrada / Saída / Entrada Dev., Alíq. PIS, Alíq. COFINS, Alíq. PIS Externa, Alíq. COFINS Externa, CST IPI, Alíq. IPI.
- Depois de copiar, você pode **ajustar os campos manualmente** — eles é que efetivamente vão para a emissão.
- Se você **limpar** o combo, o sistema **zera** os mesmos campos.

### ❓ Posso deixar o combo Tributação Federal vazio e preencher só os campos da aba?

Pode. Empresas menores costumam fazer assim. Implantações maiores preferem centralizar a parametrização em perfis cadastrados para evitar repetir a mesma alíquota em dezenas de NCMs.

### ❓ Quando o CSOSN é usado em vez do CST?

Quando a empresa é optante pelo **Simples Nacional**. O CST é usado em empresas do Lucro Real ou Lucro Presumido; o CSOSN, em empresas do Simples.

### ❓ Preciso preencher MVA se a operação não tem Substituição Tributária?

Não. Os campos de MVA (Margem de Valor Agregado) só fazem sentido em operações com ICMS-ST. Se o NCM não tem ST, deixe em branco.

**Cuidado**: se o **CST Entrada = `060`** (ICMS-ST), o sistema **exige MVA preenchido** ao salvar — a menos que a empresa esteja configurada para não usar Substituição Tributária.

### ❓ Por que o campo "Redução BC ICMS" está bloqueado?

Porque ele é calculado automaticamente como `100 − Base de Cálculo ICMS Interno` ao sair do campo de Base. Se você quer reduzir a base para 80%, basta lançar `80` em Base — o Redução vira `20` automaticamente.

### ❓ As alíquotas internas e externas que o sistema preencheu de onde vêm?

Da tela `Empresas` (código `1`). Quando você seleciona um NCM novo na Tabela NCM, o sistema lê os parâmetros padrão da empresa (`CSOSN_EXCEL`, `ICMS_ALIQ_I`, `ICMS_ALIQ_E`, `ICMS_ALIQ_STE`) e pré-preenche os campos da aba `Principal`. Se aparecer a mensagem *"Configure os Parâmetros dos Impostos em Empresa! Aba Fiscal/SPED/Imp. Excel"*, é porque esses parâmetros não estão preenchidos na tela `Empresas`.

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Empresas` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nesta tela.

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

Duplo clique no campo abre a tabela de classificações tributárias. Ao escolher uma linha, o sistema autocompleta o **CST** da aba IVA, o **Código Classificação** e os percentuais de **Redução de Alíquota** para CBS, IBS UF e IBS Mun.

### ❓ Quando preencher Redução de Alíquota CBS / IBS?

Quando o NCM se enquadra em algum **regime diferenciado** previsto na Reforma — cesta básica, medicamentos, setores específicos, regime simplificado etc. A **Alíquota** continua sendo a cheia; a **Redução** é o percentual descontado.

### ❓ O IBS tem duas partes (UF e Município) — preciso preencher as duas?

Sim. O IBS substitui simultaneamente o ICMS (estadual) e o ISS (municipal), então a alíquota é composta por uma parte estadual (UF) e uma parte municipal. Cada UF e município define a sua parte, dentro do teto fixado pela LC.

---

## 🚧 SEFAZ rejeitou — o que fazer

### ❓ Recebi um retorno "NCM inválido" na transmissão da NF-e. O que verificar?

Quando isso acontece, **o próprio sistema marca o NCM como inválido** e registra o motivo no campo `Retorno da NF-e/NFC-e` automaticamente. O que fazer:

1. Abrir o NCM no cadastro `21` e **ler o motivo** apontado pela SEFAZ no campo de retorno.
2. **Falta a EX** — é a causa mais comum; confira se o NCM tem código de exceção na tabela oficial e preencha o campo correspondente.
3. **NCM desatualizado** — confira se o código existe na Tabela NCM `121`. Se não existir, peça atualização da base à Hetosoft.
4. **CST incompatível** — em alguns casos a SEFAZ rejeita combinação de NCM + CST que ela considera inconsistente.

### ❓ Como desmarco "NCM Inválido" depois de regularizar?

Você **não precisa desmarcar manualmente**. Quando você corrige o `CODIGO` do NCM e salva, o sistema **desmarca automaticamente** o flag. Se a regularização não envolveu mudar o código (só ajustar CST, alíquota, etc.), edite o checkbox manualmente após confirmar que a configuração está correta.

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

Pode — a chave de unicidade do cadastro `21` é composta e abrange **NCM + EX + CST Entrada + CST Saída + CSOSN + Tributação Federal + MVA + Base ICMS Interno/Externo + Alíq. ICMS Interno/Externo**. Dois registros com o mesmo NCM podem coexistir desde que se diferenciem em pelo menos um desses campos. Cenário típico: um mesmo NCM com EX `00` e outros com EX numeradas — cada combinação vira um registro próprio.

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
