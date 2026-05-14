# 📄 Guia Rápido — Importar XML NF-e - Sol.NET

## 🎯 Visão Geral

Cartão de referência para a equipe de suporte durante o atendimento. Para a explicação completa de campos, regras e exemplos, consulte a [Documentação Importar XML](documentacao_importar_xml.md).

> **Tela**: `Importar XML NF-e` — código **`204`** (pesquisa F1).

---

## ⚡ Rotina padrão de importação

Checklist do fluxo "carregar XML → lançar movimento":

1. **Abrir a tela**: F1 → `204`.
2. **Modo de inclusão**: clique em `Novo`.
3. **Carregar o XML**: aba `XML`, campo `Caminho` → botão de busca → selecione o `.xml`.
4. **Conferir cabeçalho**: aba `Cabeçalho` — `Descrição da Loja`, `Fornecedor`, `Comportamento` (Entrada/Saída).
5. **Vincular itens**: aba `Itens` — todos devem aparecer com `Descrição` preenchida. Itens em branco → duplo clique → vincular ou cadastrar.
6. **Conferir financeiro**: aba `Financeiro` — número, vencimento e valor das parcelas.
7. **Lançar**: clique em `Lançar NF-e` (botão padrão).
8. **Confirmar na movimentação**: ajustar tipo de movimento e gravar.

> 💡 Se a empresa tem conferência XML habilitada, ainda há uma etapa de **conferência física** antes do lançamento. Veja [Conferência de XML](documentacao_conferencia_xml.md).

---

## 🔘 Os três botões "Lançar"

| Botão | Quando usar |
|-------|-------------|
| **`Lançar NF-e`** | 95% dos casos — entrada de fornecedor com tudo conforme a nota. |
| **`Lançar Parcial`** | Só parte da mercadoria chegou. Marque os itens recebidos e ajuste quantidades antes. |
| **`Lançar Próprio`** | NF-e em que a empresa é a **emitente** (Emissão = `PROPRIA`). Bloqueado para terceiros. |

E ainda:

| Botão | O que faz |
|-------|-----------|
| **`DANFE`** | Imprime o documento auxiliar a partir do XML (pelo grid ou pelo cadastro). |

---

## 📊 Combos de status — referência rápida

### Filtro `Status`

| Código | Texto | Significa |
|--------|-------|-----------|
| `0` | `Edição` | XML carregado mas com pendência (ex.: itens não vinculados). |
| `1` | `Finalizado` | Pronto para virar movimento. |
| `2` | `Importado` | Já gerou movimento na entrada/saída. |

### Filtro `Status Conferência`

| Texto exibido | Significa |
|---------------|-----------|
| `Não Conferido` | Conferência não iniciada. |
| `Em Andamento` | Conferência aberta, mas ainda não finalizada. |
| `Finalizada Sem Divergência` | Tudo bateu com o XML. |
| `Finalizada Com Divergência` | Conferente registrou diferença — exige atenção antes de lançar. |

### Filtro `Emissão`

| Código | Texto |
|--------|-------|
| `0` | `PROPRIA` (empresa emitiu o XML) |
| `1` | `TERCEIRO` (fornecedor emitiu) |

### Filtro `Financeiro` no grid

| Texto | Significa |
|-------|-----------|
| `LANÇADO` | Já gerou contas a pagar/receber. |
| `NÃO LANÇADO` | XML importado mas sem financeiro gerado. |

---

## 🛒 Vincular item — fluxo mínimo

1. **Duplo clique** na linha do item sem descrição.
2. O `Cadastro de Produtos` abre em pesquisa.
3. Localize o produto **ou** vá para inclusão para criar novo.
4. Confirme — o vínculo é gravado. **Próxima compra do mesmo produto com o mesmo fornecedor já entra vinculado.**

### Bloqueios que aparecem

| Mensagem | Por quê |
|----------|---------|
| `Não Permitido, Tipo Serviço!` | Produto selecionado é serviço — XML de mercadoria não vincula. |
| `Não Permitido, Produto configurado para desagregação!` | Produto tem fluxo próprio. |
| `Não Permitido, Vinculo de produto linkado!` | Configuração geral proíbe vincular produtos linkados. |
| `Produto Linkado Selecionado!` (aviso) | Vínculo permitido, mas chama atenção do usuário. |
| `Pessoa não cadastrada!` | Fornecedor do XML ainda não está no cadastro de pessoas. |

---

## ❌ Mensagens de erro no carregamento

| Mensagem | Resolução |
|----------|-----------|
| `Arquivo XML Inválido!` | Arquivo corrompido / não é NF-e / esquema errado. Pedir novo XML. |
| `Chave de Acesso já Cadastrada!` | XML já foi carregado antes — localizar registro existente. |
| `( razão ) NÃO É SUA EMPRESA!` | CNPJ destinatário não bate com loja. Conferir loja correta. |
| `Não Existe Nenhum Item com Vinculo!` | Tentou lançar com itens não vinculados. Voltar e vincular. |
| `Existem produtos linkados vinculados!` | Configuração proíbe — revisar a vinculação. |
| `Não Permitido! Somente Emissão PROPRIA.` | Usou `Lançar Próprio` em NF-e de terceiro. Trocar para `Lançar NF-e`. |
| `Movimentação Cancelada! Lançar NF-e Novamente.` | Vínculo antigo apontava para movimento cancelado. O sistema desfaz o vínculo automaticamente. |
| `Movimentação Excluida! Lançar NF-e Novamente.` | Idem, mas para movimento excluído. |

---

## 🔍 Combinações úteis de filtros

| Objetivo | Como filtrar |
|----------|--------------|
| XMLs ainda não lançados | `Status` = `Edição` ou `Finalizado` |
| XMLs sem financeiro | 2ª guia → `Financeiro` = `Não Lançados` |
| Notas de uma loja específica no mês | `Descrição da Loja` + `Data` = `Emissão` + intervalo |
| Buscar por chave de acesso | `Campo a pesquisar` = `Chave de Acesso` + `Condição` = `=` + colar a chave |
| Notas com divergência de conferência | `Status Conferência` = `Finalizada Com Divergência` |
| XMLs de saída próprios | 2ª guia → `Operações` = `Externas` |

---

## 🔗 Atalhos para outras telas

| Tela | Código F1 | Quando ir lá |
|------|-----------|--------------|
| `Manifestação do Destinatário` | `401` | Para ver/manifestar NF-e antes de importar. |
| `Cadastro de Produtos` | `40` | Vincular ou cadastrar produto do item do XML. |
| `Cadastro de Pessoas` | `30` | Cadastrar fornecedor novo. |
| `Movimentos de Entrada` | `203` | Onde a entrada gerada pelo `Lançar NF-e` é registrada. |
| `Cadastro de Empresas` | `100` | Habilitar/desabilitar `Tipo Conferência XML` por loja. |

---

## 🧭 Diagnóstico rápido

| Sintoma | Verificar |
|---------|-----------|
| "Botão `Lançar NF-e` está desabilitado" | Está em modo de visualização — entrar no registro pelo grid e abrir para edição. |
| "Não estou vendo a aba `Conferência`" | Empresa não tem `Tipo Conferência XML` ativo. Configurar no `Cadastro de Empresas`. |
| "Vinculei errado um produto" | Abrir o item (duplo clique), o vínculo pode ser refeito enquanto o XML estiver em `Edição`. |
| "Lancei a NF-e mas o estoque não subiu" | A entrada na movimentação não foi gravada — abrir o registro `204`, ver se aparece `Importado` e qual o `ID Movimento`. |

---

**Última atualização**: Maio de 2026  
**Versão**: 1.0  
**Público-alvo**: Equipe de suporte Sol.NET
