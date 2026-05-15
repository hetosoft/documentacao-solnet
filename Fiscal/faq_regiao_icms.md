# ❓ FAQ — Região ICMS Saída

Perguntas frequentes sobre o **Cadastro de Região ICMS Saída** (código `93`) do Sol.NET. Para a referência completa, abra a [Documentação da Região ICMS Saída](documentacao_regiao_icms.md).

---

## 📋 Conceito e estrutura

### ❓ O que a tela Região ICMS Saída faz exatamente?

Ela define, durante a emissão de um movimento (venda, devolução, etc.), **qual Natureza de Operação** o sistema deve aplicar em cada item, dependendo do contexto: empresa emissora, UF do destinatário, regime tributário do destinatário, atividade comercial, indicador de inscrição estadual e tipo de item.

A Região **não armazena alíquotas ou CFOPs em si** — ela é um mapa de "se o contexto for X, use a Natureza Y". Os valores fiscais (CST, alíquota, CSOSN, CFOP, CBS/IBS) que aparecem no detalhe vêm da Natureza vinculada.

### ❓ Qual a diferença entre Tipo `PESSOA` e Tipo `PRODUTO`?

- **PRODUTO**: a regra é determinada pelo produto ou pelo NCM do produto. Aceita preenchimento de `CST ICMS Prod.` e `Operação`. É a forma mais comum.
- **PESSOA**: a regra é determinada pelo perfil do destinatário (cliente). **Não aceita** `CST ICMS Prod.` nem `Operação` preenchidos — o sistema valida isso ao salvar e devolve mensagem específica.

### ❓ Por que o cadastro tem duas partes: cabeçalho e configurações?

- **Cabeçalho** é a identidade da regra (Tipo, Descrição, CSTs cobertos, Operação, vigência).
- **Configurações** são as linhas de detalhe, cada uma vinculando uma Natureza de Operação a um contexto específico (combinação de loja, estado, regime, atividade, IE, tipo de item).

Uma mesma Região pode ter várias linhas de detalhe — o sistema escolhe a mais específica que combina com o contexto da operação.

### ❓ Para que serve o campo "Nº Reg." no detalhe?

É só um identificador sequencial interno da linha de detalhe — sem significado de negócio. Pode ignorar.

---

## 🧮 Filtros e prioridade

### ❓ Como o sistema escolhe entre várias linhas de detalhe que combinam?

Ele ordena as linhas por especificidade decrescente — quanto mais filtros preenchidos (sem `-1` ou vazio), mais específica a linha. A primeira que combina com o contexto da operação ganha.

Exemplo: se você tem duas linhas, uma com `Sigla Estados = /BA/SP/` e outra com `Sigla Estados` em branco, e está vendendo para a BA, a primeira ganha.

### ❓ O que significa `-1` ou vazio nos filtros do detalhe?

Curinga: "qualquer valor". Em `Regime Tributário`, por exemplo, `-1` significa "vale para qualquer regime". Em `Sigla Estados`, vazio significa "vale para qualquer UF".

### ❓ Como funciona o filtro de Estados quando preencho `/BA/SP/`?

O sistema procura literalmente pela UF do destinatário entre as barras (`%/BA/%` ou `%/SP/%`). Por isso é importante:
- Manter as barras no início e no fim
- Não esquecer de incluir UFs que possam aparecer no movimento

### ❓ O mesmo vale para Nº Lojas?

Sim, formato idêntico: `/1/2/` significa que a linha vale para as filiais com `ID 1` e `ID 2`. Vazio = qualquer filial.

---

## 🔁 Aplicação durante a operação

### ❓ Como a Região ICMS é acionada em uma venda?

Em ordem:

1. O **Tipo de Movimento** (`37`) precisa ter `EXECUTAR_REGIAO_ICMS` ligado ou ser um tipo que aceita Região por padrão, e não estar marcado com `NAO_EXECUTAR_REGIAO_ICMS`.
2. Para cada item da venda, o sistema procura a Região:
   - **Direta**: se o produto está vinculado a uma `Região ICMS` no cadastro de Produtos, usa essa.
   - **Por CST do NCM**: se o produto não aponta uma Região, busca uma Região cujo `CST ICMS Prod.` inclua o CST do NCM do produto.
3. Dentro da Região, escolhe a linha de detalhe mais específica pelo contexto (loja, UF, IE, atividade, regime, tipo de item).
4. CFOP da Natureza vinculada é aplicado no item.
5. As flags **Manter CST/CSOSN**, **Manter Base/Aliq.** e **Manter Red/Aliq. IBS/CBS** decidem se também são copiados os respectivos valores.

### ❓ Tem como uma operação ignorar a Região ICMS?

Sim, em três cenários:
1. O **Tipo de Movimento** está com `NAO_EXECUTAR_REGIAO_ICMS` ligado, ou simplesmente não tem `EXECUTAR_REGIAO_ICMS` em um tipo onde ela não roda por padrão.
2. A **Natureza de Operação** aplicada ao item já está com `TP_FIXO` marcado — nesse caso, ela mantém os próprios valores e a Região é pulada.
3. Nenhuma Região nem o NCM combinam com o contexto.

### ❓ Como a Operação 4–10 ("Regra 5" até "Regra 10") é usada?

São casos genéricos pré-configurados, referenciados pelas configurações dos **Tipos de Movimento** (`37`). Um Tipo de Movimento pode dizer "use a Operação 5 dessa Região", permitindo cenários específicos sem precisar criar uma operação nominada.

---

## 🔒 Flags "Manter"

### ❓ Quando devo marcar "Manter CST/CSOSN"?

Quando a Região ICMS deve **forçar** o CST e o CSOSN da Natureza no item, ignorando o que viria do NCM. Cenário típico: vendas para um estado específico onde o CST muda em relação ao padrão tributário do produto.

### ❓ E "Manter Base/Aliq."?

Quando a Região deve forçar a **Base de Cálculo e a Alíquota ICMS** da Natureza no item. Útil para regimes de redução ou benefícios fiscais por região.

### ❓ "Manter Red/Aliq. IBS/CBS" também sobrescreve o NCM?

Sim — força CST CBS/IBS, alíquotas CBS / IBS UF / IBS Mun. e respectivas reduções da Natureza no item, sobrescrevendo o que vier da aba `IVA` do NCM.

### ❓ Posso deixar as três flags desmarcadas e ainda usar a Região?

Pode. Nesse caso, a Região só aplica o **CFOP** da Natureza no item (que sempre sobrescreve), e os valores fiscais continuam vindo do NCM do produto. É uma forma de centralizar a escolha de CFOP por contexto sem tocar nos impostos.

---

## 🚦 Validações

### ❓ Por que recebi "Não Permitido! Natureza de Operação Já Usada em outra Região ICMS"?

O sistema impede vincular a mesma Natureza em duas Regiões ICMS diferentes — evita ambiguidade na escolha. Soluções:
- Mudar a Natureza para outra equivalente
- Clonar a Natureza existente com outro CFOP e usar a cópia

### ❓ Por que recebi "CFOP não é de saída!" / "CFOP não é Exterior!" etc.?

A Natureza de Operação vinculada na linha tem CFOP incompatível com o `Tipo` (Saída/Entrada) e/ou `Selecione` (Dentro do Estado / Fora / Exterior) que estão marcados no detalhe. Regras do CFOP:

- Saída → começa com `5` (dentro), `6` (fora) ou `7` (exterior)
- Entrada → começa com `1` (dentro), `2` (fora) ou `3` (exterior)

Trocar a Natureza para uma com CFOP coerente, ou ajustar o cadastro da Natureza.

### ❓ A data inicial / final é sempre verificada?

Sim. O sistema só aplica a Região se a data corrente estiver dentro da janela. Datas vazias significam "sem limite" — o filtro continua passando.

> O `.dfm` traz um Hint dizendo *"A data só é levada em consideração quando a Região está definida individualmente no Produto"*. Esse Hint está obsoleto — a vigência se aplica em qualquer cenário de busca da Região.

---

## 🔗 Telas e documentos relacionados

- **[Documentação da Região ICMS Saída](documentacao_regiao_icms.md)** — referência completa
- **[Guia Rápido — Região ICMS Saída](guia_rapido_regiao_icms.md)** — checklist da rotina
- **[Cadastro de NCM](documentacao_ncm.md)** (`21`) — fonte padrão dos valores fiscais por NCM
- **Natureza de Operação** (`36`) — pivô das linhas de detalhe
- **Região ICMS ST Saída** (`94`) — análogo para Substituição Tributária
- **Tipos de Movimento** (`37`) — controla a execução da Região
- **Cadastro de Produtos** (`32`) — onde a Região ICMS pode ser vinculada direto ao produto

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Configuradores fiscais, contadores e equipe de suporte
