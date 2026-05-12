# 📄 Histórico de Movimentações - Sol.NET

## 🎯 Visão Geral

O **Histórico de Movimentações** é a tela de **análise** do que foi movimentado no Sol.NET — vendas, compras, devoluções, transferências, ajustes e qualquer outro lançamento gravado em `Cadastro de Movimentos` (código `53`). A consulta combina dezenas de filtros (data, loja, vendedor, operador, tipo de movimento, condição de pagamento, portador, turno, PDV etc.) com sub-abas de **totais agregados** por diferentes dimensões — data, mês, pessoa, tipo de movimento, portador, condição de pagamento, vendedor, operador e tabela de preço — e ainda calcula **comissões** sobre vendas e devoluções.

A tela não altera dados; é leitura e análise. Os filtros podem ser **salvos como pesquisas reutilizáveis** (aba `Pesquisa Salva`), o que poupa retrabalho de quem consulta sempre os mesmos cortes.

> 💡 **Foco da tela.** O Histórico de Movimentações enxerga o movimento **como um todo** (cabeçalho da venda/compra). Para análise dentro do item — saldo por produto, custo, margem por SKU — use o `Histórico de Produtos` (código `206`).

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Histórico de Movimentações |
| **Código (`F1`)** | `205` |

Abra a pesquisa universal (atalho `F1`) e digite **`205`** ou parte do nome **`Histórico de Movimentações`**.

---

## ⌨️ Atalhos da tela

| Tecla | O que faz |
|-------|-----------|
| `F1` | Pesquisa universal. |
| `F3` | Abre o **Relatório** do resultado consultado. |
| `F5` | **Atualiza** a consulta com os filtros atuais. |

---

## 🎚️ Filtros principais

Os filtros ficam concentrados na parte superior da tela. O sistema lembra dos valores escolhidos por usuário; também é possível configurar comportamento de entrada (loja padrão, datas padrão) nos menus de contexto dos próprios campos.

| Filtro | Para quê serve |
|--------|----------------|
| **Descrição da Loja** | Empresa cujos movimentos são exibidos. Aceita seleção de uma loja, todas, ou abrir vazio (sem filtro de loja). |
| **Inicial / Final** | Faixa de datas dos movimentos. |
| **Data** | Define qual data do movimento é usada (emissão, saída, faturamento etc.) — depende da configuração da operação. |
| **Status** | Movimentos ativos, cancelados, faturados, em conferência etc. |
| **Campo a pesquisar** + **Condição** + caixa de pesquisa | Trio de filtro flexível — escolha qual atributo do movimento (Cliente, Produto, Nº, Vendedor, etc.) é comparado e como (IGUAL, CONTÉM, INICIA COM, ENTRE, LISTA, FORA DA LISTA). |
| **Tipo de Movimento** | Limita a um Tipo de Movimento específico (clique duplo abre a pesquisa). |
| **Tipo Movimento / Movimento / Estatística** | Combos auxiliares que segmentam Compras × Vendas × Outros, e o subtipo da operação. |
| **Devolução / Crédito** | Mostra apenas as devoluções, apenas as vendas que **geraram** crédito, ou ambos. |
| **Tipo Produto/Serviço** | Filtra por classificação do item movimentado. |
| **Tipo Documento** | Tipo do documento fiscal (NF-e, NFC-e, NFS-e, Cupom etc.). |
| **Vendedor** | Pessoa marcada como vendedora no movimento. |
| **Usuário** | Usuário logado que registrou o movimento. |
| **Turno** | Turno de operação (configurado por empresa). |
| **PDV** | Equipamento de ponto de venda. |
| **Hora Inicial / Hora Final** *(aba `Outros 2`)* | Recorte por janela de horário dentro do dia. |
| **Tipo Venda** *(aba `Outros 2`)* | Recorte adicional pelo tipo da venda. |

> ⚠️ **Validação Hora Inicial / Final.** Se você preencher uma das horas, **as duas** precisam estar preenchidas — o sistema acusa *"Obrigatório preencher Hora Inicial e Hora Final!"*.

> ℹ️ **Combinações bloqueadas.** Algumas combinações de filtros são inválidas (ex.: `Devolução = Sim` com `Tipo Movimento` que não suporta devolução). O sistema avisa com mensagem clara e impede a consulta.

---

## 🧭 Sub-abas da tela

Cada sub-aba mostra o **mesmo conjunto de movimentos filtrados**, agregado por uma dimensão diferente. Trocar de aba **não** refaz a busca — usa o resultado já consultado.

| Aba | O que mostra |
|-----|--------------|
| **Pesquisar** (e **Outros 2**) | Filtros da consulta (já descritos acima). |
| **Pesquisa Salva** | Salva o conjunto atual de filtros como uma "pesquisa" reutilizável (botões `Salvar Pesquisa`, `Localizar...`, `Opções`). Útil para análises recorrentes. |
| **Total de Vendas → Data** | Soma por dia da operação. |
| **Total de Vendas → Mês** | Agrupa por mês (com opção `Mês igual juntos` para comparar mesmo mês entre anos). |
| **Total de Vendas → Pessoa** | Soma por cliente. |
| **Total de Vendas → Tipo de Movimento** | Quanto cada Tipo de Movimento somou. |
| **Portador** | Total por portador (forma de cobrança). |
| **Condição de Pagamento** | Total por condição de pagamento. |
| **Vendedor** | Total por vendedor. |
| **Operador** | Total por operador (caixa). |
| **Tabela de Preço** | Total por Tabela de Preço usada. |
| **Comissão → Vendas / Devolução** | Calcula a comissão dos vendedores sobre as vendas (e o estorno na aba de Devolução). |
| **Gráficos** | Visões gráficas das principais agregações. |

> ℹ️ **Aba `Comissão`.** Só funciona se houver `Vendedor` selecionado nos filtros e se a configuração de comissão (Cargo / Empresa) estiver completa. As validações são detalhadas ao acionar a aba — o sistema diz exatamente o que está faltando.

---

## 💾 Pesquisa Salva

A aba `Pesquisa Salva` permite **guardar um conjunto de filtros** com um nome e reutilizá-lo depois. Útil para análises recorrentes (fechamento mensal, comissão semanal, vendas por canal etc.).

| Botão | O que faz |
|-------|-----------|
| **Salvar Pesquisa** | Salva os filtros atuais com nome livre. |
| **Localizar...** | Abre a lista de pesquisas salvas pelo usuário. |
| **Opções** | Renomear, excluir e gerenciar pesquisas existentes. |

> 💡 **Configuração de entrada da tela.** Os menus de contexto sobre os campos `Descrição da Loja` e das datas permitem definir comportamento padrão: abrir com a loja logada **ou** sem loja; abrir com data de hoje **ou** com as últimas datas usadas (`Salvar datas`). Configure uma vez e o sistema lembra.

---

## ✅ Validações da consulta

| Quando você aciona a busca | O sistema verifica |
|---------------------------|--------------------|
| Sempre | Os campos da consulta passam pelo `ValidarCampo` padrão (campos obrigatórios preenchidos). |
| Se preencher uma hora | A outra também precisa estar preenchida. |
| Combinações `Devolução` × `Tipo Movimento` | Não pode marcar `Devolução` em Tipo de Movimento que não suporta devolução. |
| Combinações `Devolução` × `Movimento` | Idem — a combinação precisa ser coerente. |
| Aba `Comissão` | Exige `Vendedor` selecionado, configuração de comissão na empresa e função apropriada do vendedor. Mensagens específicas indicam o que falta. |

---

## 💡 Exemplos práticos

### Exemplo 1 — Vendas de uma loja no mês

1. Pesquisa `F1` → `205` → abre `Histórico de Movimentações`.
2. Filtros:
   - `Descrição da Loja`: a empresa.
   - `Inicial` / `Final`: primeiro e último dia do mês.
   - `Tipo Movimento`: `Vendas`.
3. `F5` para atualizar.
4. Veja o totalizador no rodapé do grid. Para abrir por dia, vá à aba **Total de Vendas → Data**.

### Exemplo 2 — Devoluções no período

1. Pesquisa `F1` → `205`.
2. Filtros como no Exemplo 1.
3. `Devolução / Crédito`: `Apenas devoluções`.
4. `F5`.

### Exemplo 3 — Comissão de um vendedor

1. Pesquisa `F1` → `205`.
2. Filtros:
   - Loja, datas, `Tipo Movimento`: `Vendas`.
   - `Vendedor`: o vendedor desejado.
3. `F5` → vá à aba **Comissão → Vendas**.
4. A aba mostra `Total (sem custos)`, `Total`, `Comissão %`, `Total Vendas` e `Total Comissão`. Para incluir o estorno por devoluções no mesmo período, alterne para **Comissão → Devolução**.

### Exemplo 4 — Salvar pesquisa de fechamento mensal

1. Configure todos os filtros do fechamento (lojas, datas, tipo movimento, status).
2. Vá à aba **Pesquisa Salva** → **Salvar Pesquisa**.
3. Dê um nome (ex.: `FECHAMENTO MENSAL`).
4. No próximo mês, abra a tela, vá à aba **Pesquisa Salva** → **Localizar...** → escolha `FECHAMENTO MENSAL` → ajuste só as datas e rode `F5`.

---

## ❓ FAQ / Problemas comuns

**A consulta não trouxe nada e eu sei que houve vendas no período.**
Confira: (1) `Status` — talvez você esteja filtrando só "Faturado" e os movimentos estejam em outro status; (2) `Descrição da Loja` — confira se a loja correta está selecionada; (3) `Tipo Movimento` / `Movimento` / `Tipo de Movimento` — filtros restritivos demais podem excluir o que você quer ver; (4) datas — confirme `Inicial` e `Final` e qual `Data` está sendo considerada.

**As abas de Total estão vazias mas o grid principal mostra movimentos.**
Algumas abas dependem de informações específicas do movimento — `Vendedor` precisa estar preenchido nos movimentos; `Comissão` precisa de configuração na empresa. Confira a mensagem que aparece ao entrar na aba — o sistema explica o que falta.

**Onde vejo o detalhe do que foi vendido em cada movimento?**
Aqui você vê o movimento (cabeçalho). Para abrir o detalhe item a item, abra o `Cadastro de Movimentos` (código `53`) ou o `Histórico de Produtos` (código `206`).

**Como exporto o resultado?**
Use `F3` (Relatórios). O Sol.NET oferece modelos pré-definidos e a opção de exportar a grade atual (XLS, PDF) conforme o modelo escolhido.

**A comissão calculada está diferente do que paguei.**
A comissão depende da configuração feita em três pontos: o **Cargo** do vendedor, a **aba Configuração / Geral** da empresa (Tipo Comissão) e a **regra de comissão por venda**. Quando alguma configuração está ausente, o sistema avisa ao entrar na aba — corrija lá antes de exigir o número desta tela.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Como se relaciona |
|------|---------------|--------------------|
| `Cadastro de Movimentos` | `53` | Origem dos dados — onde os movimentos são lançados. |
| `Histórico de Produtos` | `206` | Mesma análise, mas item a item — útil para margem, custo, vendas por SKU. |
| `Saldo Estoque` | `78` | Mostra o saldo resultante dos movimentos listados aqui. |
| `Tipos de Movimento` | `37` | Define os tipos que aparecem nos filtros. |
| `Tabela de Preço` | `27` | Origem da Tabela de Preço usada — aparece na aba `Tabela de Preço`. |
| `Cadastro de Pessoas` | `1` | Cliente / vendedor / operador referenciados em cada movimento. |

---

## ⚠️ Limites desta documentação

- Não cobre a **configuração de Comissão** (Cargo, Tipo Comissão na empresa) — essa configuração é assunto de outras telas (RH / Empresa).
- Não detalha o conteúdo de cada `Status` de movimento — isso depende da configuração de Tipos de Movimento.
- A consulta tem custo proporcional à faixa de datas e ao volume de movimentos — em bases grandes, prefira filtros estreitos.

---

**Última atualização**: Maio de 2026
**Versão**: 5.0
**Público-alvo**: Equipe de Suporte / Gestores Comerciais / Administração
