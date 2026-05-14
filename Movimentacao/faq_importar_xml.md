# 📄 FAQ — Importar XML NF-e - Sol.NET

## 🎯 Visão Geral

Perguntas frequentes sobre a tela `Importar XML NF-e` (código `204` na pesquisa F1). Para o detalhamento dos fluxos, consulte a [Documentação Importar XML](documentacao_importar_xml.md) e o [Guia Rápido](guia_rapido_importar_xml.md).

---

## 📥 Carregamento do XML

### ❓ Qual é o fluxo "certo" para lançar uma NF-e que chegou?

**Sempre comece pela Manifestação do Destinatário** (tela `401`), não pelo `Importar XML` direto. Localize a nota no grid da Manifestação, manifeste-a se ainda não foi, e clique no botão **`NF-e`** (entre `Zerar NSU` e `Confirmar`) — a tela `Importar XML` abre automaticamente em inclusão com o XML já carregado.

Abrir o `Importar XML` (F1 → `204`) e clicar em `Novo` é o **caminho excepcional**: serve apenas para XMLs que chegaram por fora da SEFAZ (e-mail, pendrive, outra loja).

### ❓ E quando o XML não veio pela SEFAZ?

Depende da origem:

- **Veio por e-mail/anexo**: salve o `.xml` em uma pasta de fácil acesso (ex.: `Documentos/XMLs/`) e, na tela `Importar XML` em modo `Novo`, selecione no campo `Caminho` (grupo `Arquivo`).
- **Veio em pendrive**: copie para o disco local antes de carregar; o seletor aceita qualquer caminho válido.

### ❓ Posso digitar a chave de acesso no campo `Chave de Acesso` para o sistema baixar o XML?

**Não.** O campo `Chave de Acesso` dentro do grupo `Manifesto` é apenas **informativo** — ele exibe a chave do XML já carregado (vindo da Manifestação ou de um arquivo). Não há ação de "baixar XML pela chave" disparada por esse campo.

O caminho para trazer um XML é sempre: ou clicar `NF-e` na Manifestação, ou selecionar o `.xml` no grupo `Arquivo`.

### ❓ Posso carregar XML de NFC-e (cupom fiscal eletrônico)?

Não. A tela é exclusiva para **NF-e** (modelo 55). Cupons fiscais têm fluxo próprio. Tentar carregar uma NFC-e resulta em `Arquivo XML Inválido!`.

### ❓ Por que aparece "Arquivo XML Inválido!"?

Causas mais comuns:

- Arquivo corrompido (corte de transferência, e-mail truncado).
- Arquivo é de outro modelo de documento (NFC-e, CT-e, NFS-e, MDF-e).
- O `.xml` foi salvo como texto (extensão errada).
- XML alterado manualmente em editor de texto e perdeu a assinatura.

Solução: peça um novo XML diretamente ao fornecedor (ou redownload pela Manifestação).

### ❓ Aparece "Chave de Acesso já Cadastrada!" mas eu não importei essa nota. Por quê?

Possíveis razões:

- Outro usuário já importou a NF-e antes.
- O XML chegou pela Manifestação do Destinatário e foi pré-cadastrado.
- A nota foi vinculada como entrada manual e o sistema mesmo importou o XML em segundo plano.

Use o filtro `Campo a pesquisar` = `Chave de Acesso` para encontrar o registro existente e dar continuidade lá.

---

## 🏢 Empresa e fornecedor

### ❓ "( razão social ) NÃO É SUA EMPRESA!" — o que isso significa?

O CNPJ do **destinatário** do XML (a empresa que recebeu a nota) não bate com nenhuma loja cadastrada no Sol.NET. Verifique:

1. Se a NF-e foi de fato emitida para a sua empresa (conferir CNPJ no DANFE).
2. Se a loja correta está cadastrada no `Cadastro de Empresas`.
3. Se há autorização para "importar terceiro" — algumas operações (transportadora, depósito) podem precisar dessa configuração; nesse caso o campo `Descrição da Loja` fica habilitado para seleção manual.

### ❓ O fornecedor não existe no meu cadastro. Como cadastrar pelo `Importar XML`?

Na aba `Cabeçalho`, clique no botão **`Cadastrar fornecedor`** (à direita do campo `Fornecedor`). O `Cadastro de Pessoas` abre em modo de inclusão com **CNPJ, razão social, endereço e demais campos do XML já preenchidos**. Complete o que faltar (tipo de pessoa, contato), salve, e o vínculo é gravado no XML automaticamente.

### ❓ Existem dois fornecedores no cadastro com o mesmo CNPJ. Qual o sistema escolhe?

Quando o sistema detecta múltiplos fornecedores com o mesmo CNPJ/CPF, abre uma janela auxiliar listando os possíveis e pede que o usuário **escolha qual deve ser vinculado**. Não há escolha automática — é decisão manual do operador.

---

## 🛒 Vínculo de itens

### ❓ Por que alguns itens vêm vinculados automaticamente e outros não?

O Sol.NET tenta casar pelo **código do fornecedor** (`Cód. Forn.` que veio no XML) com o que está cadastrado no produto. Se o produto **já foi comprado antes** desse mesmo fornecedor, o vínculo existe e o sistema reconhece. Para fornecedores ou produtos novos, o vínculo precisa ser feito manualmente uma vez — depois disso, fica automático.

### ❓ Posso vincular um item de XML a vários produtos do cadastro (ou vice-versa)?

Não. O vínculo é **um para um** por combinação (fornecedor + código do fornecedor → produto cadastrado). Se o fornecedor passa a entregar o mesmo código com características diferentes, o produto precisa ser desmembrado no cadastro.

### ❓ "Não Permitido, Tipo Serviço!" ao vincular item — o que fazer?

A nota é de mercadoria mas o usuário selecionou um produto cadastrado como **Serviço**. Soluções:

- Confirme que o item realmente é mercadoria (não serviço); se for, encontre o produto correto.
- Se realmente é um serviço, a NF-e não devia estar nessa tela — serviços têm fluxo próprio (NFS-e).

### ❓ "Não Permitido, Produto configurado para desagregação!" — por que aparece?

Produtos marcados para **desagregação** (kits, fardos que viram unidades) têm fluxo próprio na entrada. Não podem ser vinculados diretamente a um item de XML — o sistema bloqueia para evitar inconsistência de estoque. Se o item realmente é o produto desagregável, a entrada precisa seguir o fluxo específico.

### ❓ Como saber se um item está vinculado?

Olhando a coluna `Descrição` na aba `Itens`:

- **Preenchida com a descrição do cadastro** → item vinculado.
- **Em branco ou só com a descrição do fornecedor** → ainda precisa vincular.

### ❓ Vinculei errado um item. Como corrigir?

Enquanto o XML estiver com `Status = Edição` (ou seja, ainda não virou movimento), basta dar **duplo clique no item** novamente. O sistema reabre a pesquisa de produtos e o vínculo pode ser refeito. Depois do lançamento, ajustes precisam ser feitos diretamente na movimentação.

### ❓ Cadastrei um produto novo a partir do `Importar XML`. Os dados do XML ficam salvos?

Sim. Ao cadastrar o produto, o Sol.NET grava automaticamente:

- O **código do fornecedor** (`Cód. Forn.`) na tabela de códigos de fornecedor.
- O **EAN do fornecedor** (quando vier).
- A **descrição do fornecedor** (a forma como o produto aparece na nota do fornecedor).

Isso garante que **na próxima compra do mesmo produto desse mesmo fornecedor**, o vínculo será automático.

---

## ▶️ Lançamento do movimento

### ❓ Qual a diferença entre os três botões "Lançar"?

| Botão | Quando usar |
|-------|-------------|
| **`Lançar NF-e`** | Caso padrão — entrada de mercadoria conforme a nota. |
| **`Lançar Parcial`** | Apenas parte da mercadoria chegou — marca-se na coluna `Sel.` os itens recebidos. |
| **`Lançar Próprio`** | NF-e em que a empresa é a **emitente** (Emissão = `PROPRIA`). Bloqueado para terceiros. |

### ❓ Posso lançar a NF-e sem vincular todos os itens?

Não. O Sol.NET bloqueia com `Não Existe Nenhum Item com Vinculo!` se houver pelo menos um item sem produto cadastrado. Vincule todos antes de tentar lançar.

### ❓ Lancei a NF-e mas o financeiro não foi gerado. Onde vejo?

A aba `Financeiro` da tela `204` mostra as parcelas que vieram **no XML**. Se essa aba está vazia, o XML não trouxe a tag de cobrança (NF-e à vista, sem parcelamento, ou fornecedor não preencheu). Nesse caso, o financeiro precisa ser lançado manualmente em `Contas a Pagar`.

### ❓ Aparece "Diferença de Custo de X%" no lançamento. Devo cancelar?

É um **aviso**, não um bloqueio. O Sol.NET compara o custo do item no XML com o custo atual cadastrado e, quando passa de um percentual configurado, alerta. Decida com base no contexto:

- **Aumento legítimo** (fornecedor reajustou preço) → confirmar e atualizar custo.
- **Possível erro** (digitação errada do fornecedor, casa decimal trocada) → cancelar e revisar com o fornecedor.

### ❓ Tentei `Lançar Próprio` e apareceu "Somente Emissão PROPRIA". O que fazer?

A NF-e que está aberta é de **terceiro** (algum fornecedor é o emitente). O botão `Lançar Próprio` só funciona para notas emitidas pela própria empresa (típico de retorno de XML de uma saída). Use `Lançar NF-e` (ou `Lançar Parcial`).

### ❓ Lancei o XML, mas vi que o movimento foi excluído depois. O vínculo ainda existe?

Não. Quando o Sol.NET detecta que o movimento vinculado foi **excluído** ou **cancelado**, mostra a mensagem `Movimentação Excluida/Cancelada! Lançar NF-e Novamente.` e **desfaz o vínculo automaticamente**, voltando o XML para o status anterior. Basta clicar em `Lançar NF-e` de novo.

---

## 📨 Manifestação e DANFE

### ❓ Preciso fazer a Manifestação antes de importar o XML?

**Sim, é o fluxo padrão.** Para NF-e de terceiros emitidas contra o seu CNPJ, a `Confirmação da Operação` ou `Ciência da Emissão` precede o lançamento como entrada — e o Sol.NET já entrega isso integrado: depois de manifestar, basta clicar no botão `NF-e` (entre `Zerar NSU` e `Confirmar` na tela `401`) e a importação parte do XML que a SEFAZ disponibilizou.

Carregar um `.xml` diretamente pelo `Importar XML` (modo `Novo` + grupo `Arquivo`) existe como **exceção** para situações em que o XML não veio pela SEFAZ. Não substitui a manifestação.

Veja [Manifestação do Destinatário](../Fiscal/documentacao_manifestacao_destinatario.md).

### ❓ Posso imprimir o DANFE direto pela tela?

Sim. O botão `DANFE` na faixa de botões imprime o documento auxiliar a partir do XML. Funciona tanto:

- **Pelo grid** — selecione a linha da NF-e e clique em `DANFE`.
- **No cadastro** — com o registro aberto, clique em `DANFE`.

Se o XML não estiver no banco (caso raro de carga manual sem persistência), o sistema tenta imprimir a partir do arquivo `.xml` do caminho original.

---

## 🔍 Conferência de XML

### ❓ Onde vejo se a conferência está ativa para minha empresa?

No `Cadastro de Empresas` (código `1`), há a configuração `Tipo Conferência XML`. Quando habilitada, a aba `Conferência` aparece dentro do `Importar XML`. Veja o documento dedicado: [Conferência de XML](documentacao_conferencia_xml.md).

> ⚠️ **Acesso de suporte necessário:** alterações no `Cadastro de Empresas` requerem permissão de acesso de suporte. Entre em contato com o suporte Hetosoft antes de realizar qualquer modificação nesta tela.

### ❓ A coluna `Status Conferência` está vermelha. O que fazer?

`Status Conferência` = `FINALIZADA COM DIVERGÊNCIA` indica que o conferente registrou diferença entre o que chegou e o que está no XML. Antes de lançar a NF-e:

1. Abra o registro pelo grid.
2. Vá para a aba `Conferência`.
3. Veja os itens marcados com `TP_DIVERGENCIA = 1` — quantidade ou código diferente.
4. Decida: lançar tudo conforme o XML, lançar parcial conforme conferência, ou tratar a divergência com o fornecedor.

Detalhes em [Conferência de XML](documentacao_conferencia_xml.md).

---

## 🔗 Documentos relacionados

- [Documentação Importar XML](documentacao_importar_xml.md) — referência completa
- [Guia Rápido — Importar XML](guia_rapido_importar_xml.md) — checklist operacional
- [Conferência de XML](documentacao_conferencia_xml.md) — fluxo da conferência física
- [Manifestação do Destinatário](../Fiscal/documentacao_manifestacao_destinatario.md) — porta de entrada dos XMLs da SEFAZ

---

**Última atualização**: Maio de 2026  
**Versão**: 1.0  
**Público-alvo**: Usuários e administradores do Sol.NET ERP
