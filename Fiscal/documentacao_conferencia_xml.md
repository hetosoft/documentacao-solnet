# 📄 Conferência de XML - Sol.NET

## 🎯 Visão Geral

A **Conferência de XML** é um mecanismo opcional do Sol.NET para **confrontar a mercadoria recebida fisicamente com o que veio no XML do fornecedor** *antes* de a NF-e virar movimento de entrada.

Quando habilitada na loja, a tela [Importar XML NF-e](documentacao_importar_xml.md) (código `204`) ganha uma aba **`Conferência`**, e o grid principal passa a mostrar o `Status Conferência` de cada XML. A conferência funciona como uma **etapa intermediária** entre carregar o XML e clicar em `Lançar NF-e`:

1. XML chega na tela `Importar XML` (manualmente ou via Manifestação do Destinatário).
2. Conferente físico abre o registro, vai na aba `Conferência` e marca o que efetivamente recebeu (por item).
3. O Sol.NET classifica como `Sem Divergência` ou `Com Divergência`.
4. Lançamento na movimentação é feito depois, já ciente do que bate ou não com o XML.

### Para que serve

- ✅ Garantir que a entrada na movimentação só ocorre após conferência física da mercadoria
- ✅ Detectar divergências de quantidade ou de código entre o XML e o recebido
- ✅ Bloquear lançamento (ou pelo menos sinalizar) quando o conferente registrar diferença
- ✅ Auditar quem conferiu cada nota e quando
- ✅ Servir como base de negociação com fornecedor em caso de falta ou excedente

### Quando o suporte é acionado

- "A aba `Conferência` não aparece" → loja não está com o tipo de conferência habilitado.
- "Status Conferência ficou em `Em Andamento` para sempre" → conferente não finalizou a conferência; orientar como retomar.
- "Preciso reabrir a conferência" → conferente terminou mas precisa ajustar; explicar o fluxo de voltar para `Em Andamento`.
- "Quero saber por que o lançamento da NF-e foi feito sem conferência" → loja não usa o recurso ou foi desabilitado.

---

## 🚪 Como habilitar a conferência

A conferência é **configurada por loja** (não é um parâmetro global do sistema). A configuração fica no `Cadastro de Empresas`:

1. Pressione F1 e abra o `Cadastro de Empresas` (código `100`).
2. Localize a loja desejada no grid de busca.
3. Abra o registro e localize o campo **`Tipo Conferência XML`** (ou rótulo equivalente).
4. Habilite e grave.

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Empresas` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nesta tela.

A partir da habilitação:

- Todo XML carregado na tela `Importar XML` para essa loja passa a exigir conferência antes do lançamento.
- A aba `Conferência` aparece na tela `204` para registros dessa loja.
- O grid principal da tela `204` mostra a coluna `Status Conferência` preenchida.

Para **desabilitar**, basta desmarcar o campo no `Cadastro de Empresas`. XMLs já em conferência permanecem com seu status registrado, mas novos XMLs daquela loja passam direto.

---

## 🔍 Os estados da conferência

A conferência tem **dois campos** que andam juntos no grid e nos relatórios.

### `Status Conferência` (de andamento)

Indica em que ponto do fluxo o XML está.

| Texto exibido | Significa | O que pode fazer |
|---------------|-----------|------------------|
| `NÃO CONFERIDO` | Conferência não iniciada. | Abrir o registro e iniciar. |
| `EM ANDAMENTO` | Conferência aberta, alguns itens já tratados, mas não finalizada. | Retomar e concluir. |
| `FINALIZADA SEM DIVERGÊNCIA` | Conferente concluiu e tudo bateu com o XML. | Pode lançar a NF-e. |
| `FINALIZADA COM DIVERGÊNCIA` | Conferente concluiu e marcou pelo menos um item como divergente. | Avaliar antes de lançar; possivelmente usar `Lançar Parcial`. |

### Indicador no grid

Na grid principal da tela `204`, a coluna `Status Conferência` muda de cor conforme o estado — divergências são sinalizadas em vermelho/destaque, conferências finalizadas sem divergência em verde. Isso ajuda a varrer rapidamente o que precisa de atenção.

---

## 🧭 A aba `Conferência` dentro do `Importar XML`

A aba **`Conferência`** só fica visível quando a loja tem o recurso habilitado e o XML está aberto. Ela exibe um grid (`dbgItensConferencia`) com **uma linha por item da NF-e**, focado no que o conferente precisa marcar.

### Colunas do grid

| Coluna | Para que serve |
|--------|----------------|
| `Sel.` | Marcação manual de itens (uso operacional). |
| `Nº` | Número sequencial do item dentro da NF-e. |
| `Cód. Forn.` | Código do produto no fornecedor (vem do XML). |
| `EAN Forn.` | EAN do produto no fornecedor. |
| `Produto do Fornecedor` | Descrição como aparece na nota do fornecedor. |
| `Código` | Código do produto **no cadastro do Sol.NET** (após vínculo). |
| `Conf.` | Marcação de conferido — alimentada pela conferência física. |
| `Descrição` | Descrição do produto no cadastro. |
| `Quantidade` (várias colunas: `Q.De`, `Q.Na`, `Quant.`) | Quantidades e suas conversões de unidade. |
| `Vl. Unitário`, `Custo I. Nota`, `Custo I. Atual`, `Dif. Custo %` | Análise de custo entre o que o XML traz e o cadastro. |
| `Vl. Total`, `Bs. ICMS`, `Vl. ICMS`, `Bs. ICMS ST`, `Vl. ICMS ST`, `Vl. IPI` | Valores fiscais para conferência. |

> 💡 As colunas de tributos servem mais para auditoria que para conferência física — o foco da operação é nas colunas de **quantidade** e **código**.

### O que o conferente faz

Em geral o fluxo manual é:

1. Item a item, comparar o que está no XML com a mercadoria física à frente.
2. Marcar a coluna `Conf.` quando o item bate (quantidade e identificação).
3. Quando há diferença (falta, excesso, item diferente), **registrar a divergência** — o sistema marca `TP_DIVERGENCIA = 1` na linha.
4. No final, finalizar a conferência (botão correspondente na tela, ver próxima seção).

> ⚠️ Telas auxiliares de leitor de código de barras podem ser usadas para alimentar essa conferência automaticamente — o resultado, porém, chega ao mesmo grid e segue as mesmas regras.

---

## 🚦 O ciclo da conferência

O fluxo completo, da chegada da mercadoria ao lançamento, fica assim:

```
[XML carregado] 
       │ Status Conferência: NÃO CONFERIDO
       ▼
[Conferente abre o registro]
       │ Status Conferência: EM ANDAMENTO
       ▼
[Marca/desmarca itens, registra divergências]
       │
       ▼
[Finaliza a conferência]
       │ STATUS_CONFERENCIA_ANDAMENTO = 2
       │  ├── Sem divergência → FINALIZADA SEM DIVERGÊNCIA
       │  └── Com divergência → FINALIZADA COM DIVERGÊNCIA
       ▼
[Operador decide lançar a NF-e]
       └── Lançar NF-e / Lançar Parcial conforme o caso
```

### Reabrir uma conferência finalizada

Quando o conferente conclui mas precisa ajustar (item esquecido, divergência registrada errada), é possível **voltar a conferência para `Em Andamento`**:

- A operação exige permissão (consulta interna `375`); usuários sem acesso são bloqueados.
- O sistema mostra `Conferencia não está finalizada!` se tentar reabrir uma conferência que ainda está em andamento — o objetivo é reabrir uma já finalizada.
- Ao confirmar a reabertura, o status volta para `EM ANDAMENTO` e a mensagem `Status de Conferencia Alterado para EM ANDAMENTO.` é exibida.

A reabertura é uma exceção operacional — o caminho normal é finalizar uma única vez.

---

## 🔗 Interação com o lançamento da NF-e

O `Status Conferência` **não bloqueia** automaticamente o lançamento da NF-e — o operador tem autonomia para decidir. Mas a informação serve de gate:

| Situação | Recomendação |
|----------|--------------|
| `Não Conferido` em loja com conferência habilitada | Pedir conferência antes de lançar. Lançar sem conferir contraria o propósito do recurso. |
| `Em Andamento` | Conferência incompleta. Concluir primeiro. |
| `Finalizada Sem Divergência` | Pode lançar com `Lançar NF-e` sem ressalvas. |
| `Finalizada Com Divergência` | Decidir entre: |
| | • `Lançar NF-e` — entrar tudo igual ao XML (assume divergência como erro de conferência). |
| | • `Lançar Parcial` — entrar somente o efetivamente recebido. |
| | • Não lançar e contatar fornecedor. |

A operação de `Lançar` em si é a mesma descrita em [Importar XML — Lançar a NF-e na movimentação](documentacao_importar_xml.md).

---

## 💡 Exemplos Práticos

### Exemplo 1 — Conferência sem divergência

**Cenário**: chegou um caminhão com 12 caixas conforme NF-e. Cada caixa contém um item que está no XML, na quantidade certa.

1. O XML já está no Sol.NET (importado pela Manifestação ou carregado manualmente).
2. O conferente abre o registro na tela `204`, vai na aba `Conferência`.
3. Confere item a item. Tudo bate.
4. Marca `Conf.` em todos os itens.
5. Finaliza a conferência. `Status Conferência` vira `FINALIZADA SEM DIVERGÊNCIA`.
6. O operador (mesmo usuário ou outro) clica em `Lançar NF-e`. Entrada gerada normalmente.

### Exemplo 2 — Conferência com divergência de quantidade

**Cenário**: XML lista 10 unidades de um produto; chegaram apenas 8.

1. Conferente abre o registro, vai na aba `Conferência`.
2. Confere os itens. No item divergente, registra a quantidade efetiva (8) — o item fica marcado como divergente (`TP_DIVERGENCIA = 1`).
3. Finaliza a conferência. `Status Conferência` vira `FINALIZADA COM DIVERGÊNCIA` e a coluna no grid principal aparece em destaque.
4. Operador decide:
   - **Opção A**: lançar tudo igual ao XML (`Lançar NF-e`) e tratar a falta com o fornecedor depois — gera um excedente fiscal de 2 unidades que precisará de ajuste.
   - **Opção B**: lançar parcial (`Lançar Parcial`), entrando só as 8 unidades; o XML permanece registrado e a divergência é histórico.
5. Sempre comunicar o fornecedor para correção (carta de correção, retorno de mercadoria, abatimento).

### Exemplo 3 — Conferência por código diferente

**Cenário**: XML lista o produto X, mas chegou o produto Y (código diferente).

1. Conferente abre a aba `Conferência`.
2. Marca o item como divergente — o EAN ou código que chegou não bate.
3. Finaliza a conferência como `Com Divergência`.
4. Esse caso normalmente **não deve virar movimento** — a mercadoria errada precisa voltar para o fornecedor e uma nota corretiva precisa ser emitida.

### Exemplo 4 — Reabrir conferência por engano

**Cenário**: conferente finalizou a conferência, mas percebeu que esqueceu de marcar um item.

1. Operador com permissão abre o registro pelo grid (estado de visualização).
2. Aciona a função de reabrir conferência (ver `Reabrir uma conferência finalizada` acima).
3. Confirma. Status volta para `EM ANDAMENTO`.
4. Conferente reentra, ajusta, e finaliza de novo.

---

## ❓ FAQ / Problemas Comuns

### ❓ A aba `Conferência` não aparece para mim. Por quê?

A aba só é exibida quando a loja (registro do XML) tem o `Tipo Conferência XML` habilitado no `Cadastro de Empresas`. Verifique a loja do XML aberto e a configuração da loja.

### ❓ Posso usar conferência em uma loja e em outra não?

Sim. A configuração é **por loja**. Lojas onde o recurso não faz sentido (ex.: ponto de venda sem recebimento físico) podem ficar sem.

### ❓ Quem pode finalizar uma conferência? E reabrir?

Qualquer usuário com acesso à tela `Importar XML` pode iniciar e finalizar uma conferência. **Reabrir** uma conferência já finalizada exige permissão específica (controle de acesso interno `375`) — se o usuário não tem, recebe bloqueio de permissão.

### ❓ Conferência finalizada pode ser apagada?

Não. O histórico de conferência fica no registro do XML mesmo após o lançamento da NF-e. É possível reabrir (ver acima) para ajustar antes do lançamento.

### ❓ O sistema bloqueia o lançamento da NF-e se a conferência estiver pendente?

O Sol.NET **não bloqueia automaticamente** — mas o `Status Conferência` no grid e na tela serve de aviso visual. A política de "não lançar sem conferir" é uma regra **operacional** da empresa, não uma restrição do sistema. Se quiser bloqueio rígido, a equipe Hetosoft pode avaliar uma configuração específica.

### ❓ Posso ver quem conferiu cada nota?

Sim. A coluna `Usuário Conferencia` no grid mostra o operador que finalizou a conferência. O carimbo é gravado no momento da finalização.

### ❓ Conferência funciona para NF-e de saída (emissão própria)?

Não no mesmo modelo. A conferência aqui descrita serve para **recebimento de mercadoria** — confronta XML do fornecedor com o que entrou no estoque. Em NF-e própria (saída), a tela `Importar XML` opera com o botão `Lançar Próprio`, sem fluxo de conferência.

---

## 🔗 Documentos relacionados

- [Documentação Importar XML](documentacao_importar_xml.md) — onde a conferência se encaixa
- [Guia Rápido — Importar XML](guia_rapido_importar_xml.md) — atalhos para suporte
- [FAQ — Importar XML](faq_importar_xml.md) — perguntas mais frequentes
- [Manifestação do Destinatário](documentacao_manifestacao_destinatario.md) — porta de entrada dos XMLs

---

**Última atualização**: Maio de 2026  
**Versão**: 1.0  
**Público-alvo**: Equipe de suporte Sol.NET, conferentes e administradores de loja
