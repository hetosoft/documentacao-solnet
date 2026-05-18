# ❓ FAQ — Região ICMS ST Saída

Perguntas frequentes sobre o **Cadastro de Região ICMS ST Saída** (código `94`) do Sol.NET. Para a referência completa, abra a [Documentação da Região ICMS ST Saída](documentacao_regiao_icms_st_saida.md).

---

## 📋 Conceito e estrutura

### ❓ O que a tela `Região ICMS ST Saída` faz exatamente?

Armazena conjuntos de **percentuais de ICMS-ST** (`B.C. ICMS ST`, `MVA`, `ICMS ST Aliq.`) e os aplica em cada item da operação cujo contexto combina com os filtros de uma linha de detalhe (loja emissora, UF do destinatário, perfil do destinatário, CNAE, regime, etc.).

### ❓ Qual a diferença para a tela `Região ICMS Saída` (`93`)?

A `93` é um **mapa de Natureza de Operação** — diz qual Natureza usar em cada contexto, e os valores fiscais (CST, alíquota, CSOSN, CFOP, CBS, IBS) vêm da Natureza vinculada. A `94` **armazena diretamente os percentuais** de ICMS-ST e os aplica. As duas convivem: a `93` cuida do ICMS normal e da escolha de CFOP; a `94` cuida especificamente do cálculo do ICMS-ST.

### ❓ Qual a diferença entre Tipo `PRODUTO` e Tipo `PESSOA`?

- **`PRODUTO`** — a Região é apontada pelo **cadastro do produto**. Use quando a regra de ICMS-ST varia mais pela natureza do item do que pelo destinatário.
- **`PESSOA`** — a Região é apontada pelo **cadastro da pessoa** (cliente). Use quando o cliente tem uma regra fixa que vale para qualquer produto que ele compra.

Ambos os modos podem coexistir no mesmo Sol.NET — basta cadastrar uma Região para cada modo.

### ❓ Por que o cadastro tem duas partes: cabeçalho e configurações?

O **cabeçalho** identifica a regra como um todo (`Tipo`, `Descrição`). As **configurações** são as linhas de detalhe — cada uma cobre um contexto fiscal específico. Uma mesma Região pode ter várias linhas, e o Sol.NET escolhe a mais específica que casa com o contexto do movimento.

### ❓ A tela vale só para Saída?

Apesar do nome, o radio `Tipo` na linha de detalhe permite marcar `Entrada` também. Na prática, a tela cobre operações em que o sistema precisa calcular ICMS-ST — habitualmente saída, mas com suporte a entradas quando a configuração fiscal exige.

---

## 🧮 Percentuais e cálculo

### ❓ Para que serve o campo `B.C. ICMS ST`?

É o percentual da **base de cálculo do ICMS-ST após redução**. `100,00%` significa que a base completa é usada; `60,00%` significa que apenas 60% da base entra na conta.

### ❓ Para que serve o campo `MVA`?

Margem de Valor Agregado, em percentual. O Sol.NET aplica essa margem sobre o valor do item para compor a base do ICMS-ST. No modo de cálculo `Industria MT`, este mesmo campo é usado como **Margem de Lucro**.

### ❓ Para que serve o campo `ICMS ST Aliq.`?

Alíquota do ICMS-ST em percentual. No modo de cálculo `Industria MT`, este mesmo campo é usado como **Carga Média**.

### ❓ Quando devo marcar `Usar MVA NCM`?

Quando a MVA varia produto a produto e já está mantida no Cadastro de NCM. Com a flag marcada, o sistema **ignora a MVA digitada na linha** e busca a MVA do NCM do item. É útil para regras genéricas que cobrem muitos produtos sem precisar duplicar linhas só por causa da MVA.

### ❓ Marquei `Usar MVA NCM`, mas o cálculo ainda usa a MVA da linha. Por quê?

Verifique se o NCM do item realmente tem MVA cadastrada. Sem MVA no NCM, o cálculo pode cair de volta para a MVA da linha. Confirme também se o produto está apontando para o NCM correto.

### ❓ Quando devo usar `Industria MT` no combo `Cálculo`?

Quando o cliente é uma **indústria estabelecida em Mato Grosso** sujeita ao regime estadual específico que substitui MVA por Margem de Lucro e alíquota por Carga Média. A fórmula exata depende da legislação estadual e deve ser validada com a contabilidade. Em todos os outros cenários, use `Normal`.

### ❓ O combo `Cálculo` mostra um item em branco no final. O que é?

Item descontinuado que sobrou no cadastro. Use somente `Normal` ou `Industria MT`.

---

## 🧷 Filtros e curingas

### ❓ Como faço uma linha valer para qualquer estado?

Deixe `Sigla Estados` em branco. O mesmo vale para qualquer outro filtro: `Nº Lojas`, `CNAE`, `Indicador IE`, `Atividade Comercial`, `Regime Tributário`. Vazio (ou `-1` em combos) significa "qualquer valor".

### ❓ Posso listar vários estados ou várias lojas numa mesma linha?

Sim. Separe os valores por barra `/`, ex.: `/BA/SP/MG/` ou `/1/2/3/`. O Sol.NET acrescenta as barras inicial e final automaticamente ao sair do campo.

### ❓ Qual a relação entre as opções `Indicador IE` (`1`, `2`, `9`) e a SEFAZ?

Seguem o padrão da SEFAZ para Indicador de Inscrição Estadual do destinatário: `1 — Contribuinte`, `2 — Isento`, `9 — Não Contribuinte`. Esse mesmo código vai para a NF-e.

### ❓ E se duas linhas atendem ao mesmo contexto?

O Sol.NET prefere a linha mais específica. Quando há empate de especificidade, a regra é não-determinística e deve ser evitada — refine os filtros para que cada combinação aponte para uma única linha.

---

## ✏️ Cadastro e operação

### ❓ Posso ter duas Regiões com a mesma Descrição?

Sim. A tela não bloqueia duplicidade. O caso comum é uma Região `PRODUTO` e outra `PESSOA` com o mesmo nome para indicar que cobrem o mesmo cenário pelos dois modos de vínculo.

### ❓ Por que ao tentar sair da área `Configurações` o sistema mostra "Existe cadastro em edição"?

Porque há uma linha de detalhe em inserção ou edição que ainda não foi confirmada. Clique `Atualizar` para gravar a linha ou `Cancelar` para descartar antes de mudar de seção ou fechar a tela.

### ❓ Tentei excluir uma Região e apareceu "Existe Produto(s) com essa Região". Como resolver?

A Região (Tipo `PRODUTO`) está vinculada a um ou mais produtos. Abra o `Cadastro de Produtos`, localize quem aponta para essa Região e troque ou limpe o vínculo. Depois disso, a exclusão fica liberada. Para Tipo `PESSOA` não há esse bloqueio — a exclusão é livre, e cabe ao operador atualizar os cadastros de pessoas que ficaram apontando para uma Região inexistente.

### ❓ Onde vinculo a Região cadastrada aos produtos ou pessoas?

- Tipo `PRODUTO` → no `Cadastro de Produtos` (`32`), no campo que aponta para `Região ICMS ST`.
- Tipo `PESSOA` → no `Cadastro de Pessoas` (`5`), no campo equivalente.

### ❓ Mudei os percentuais e o movimento já emitido continua com o valor antigo. É bug?

Não. O Sol.NET calcula o ICMS-ST **no momento da emissão**. Movimentos já gravados mantêm os valores históricos. Para reaplicar a nova regra, o movimento precisa ser refeito.

---

## 🔗 Relação com outras telas

### ❓ Esta tela substitui o cadastro da Natureza de Operação?

Não. As duas convivem: a Natureza de Operação (`36`) define CFOP, CST e tributos gerais; a Região ICMS-ST (`94`) define os percentuais específicos do ICMS-ST. O cálculo final combina as duas fontes.

### ❓ Onde a tela busca o CNAE selecionado no filtro?

A busca abre o `Cadastro de CNAE`. O campo armazena o código `SUBCLASSE` do CNAE selecionado e exibe esse mesmo código para o operador.

### ❓ A configuração depende do Cadastro de Tipo de Movimento?

Indiretamente: o `Cadastro de Tipo de Movimento` decide se uma operação calcula ICMS-ST e em que momento. Quando o cálculo é acionado, o Sol.NET vai buscar nesta tela qual linha aplicar.

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Equipe de Suporte / Usuários do Sol.NET / Contabilidade
