# 📄 Receituário Agronômico - Sol.NET

## 🎯 Visão Geral

O **Módulo Agronômico** do Sol.NET ERP gerencia todo o ciclo de **Receituário Agronômico**, exigência legal para a comercialização e aplicação de defensivos agrícolas no Brasil. O receituário é o documento prescritivo emitido por um responsável técnico habilitado (Engenheiro Agrônomo ou Técnico Agrícola) que autoriza a aplicação de um produto fitossanitário em uma cultura, contra um alvo biológico, na dose indicada pela bula registrada no MAPA.

O Sol.NET cobre:
- **Cadastros de apoio**: culturas, diagnósticos (alvos), produtos formulados, configuração de bula digital, embalagens
- **Cadastros administrativos**: profissionais responsáveis, blocos de ART/TRT, locais de aplicação dos clientes
- **Emissão**: avulsa ou integrada à Movimentação (venda)
- **Validações automáticas**: bula, saldo e validade de ART, vínculo cliente/local, vínculo empresa/ART
- **Impressão** no modelo legal via ReportBuilder
- **Cancelamento** com estorno automático de saldo

### 📜 Base Legal Resumida

- **Lei nº 7.802/1989** e **Decreto nº 4.074/2002**: regulam agrotóxicos e exigem receituário
- **Decreto nº 10.833/2021**: atualiza dispositivos sobre comercialização de defensivos
- **MAPA**: registro nacional dos produtos e suas bulas
- **CREA / CFTA**: conselhos profissionais que autorizam a assinatura

> ⚠️ A entrega das vias da receita e a transmissão a órgãos estaduais (ADAPAR/IDARON/IAGRO/SEAPDR/etc.) seguem regras locais. O Sol.NET imprime no formato exigido; a tramitação física/eletrônica externa fica sob responsabilidade da empresa.

---

## 🧭 Acesso às Telas

Todas as telas do Sol.NET são acessadas pela **tela de pesquisa universal**, aberta com o atalho **F1**. Na pesquisa, digite o **código identificador** (`ID_FORMULARIO`) da tela ou parte do seu nome e confirme.

**Telas do Módulo Agronômico:**

| Tela | Código (`ID_FORMULARIO`) | Para quê serve |
|------|:---:|---|
| Cadastro Cultura Agronômica | **138** | Cultivos atendidos (Soja, Milho, Café…) |
| Cadastro Diagnóstico Agronômico | **139** | Alvos biológicos (pragas, doenças, plantas daninhas, nematóides) |
| Cadastro Formulado Agronômico | **140** | Defensivos comercializados (com nº de registro MAPA) |
| Cadastro Config Bula Agronômico | **141** | Bula digital — combinações `Formulado × Cultura × Diagnóstico` permitidas, dose mín./máx., modalidade e carência |
| Profissionais Externos | **135** | Responsáveis técnicos (Eng. Agrônomos / Téc. Agrícolas) |
| Gestão ART/TRT | **136** | Blocos de ART/TRT vinculados a profissional + empresa |
| Receituário Agronômico | **142** | Emissão avulsa, consulta e cancelamento de receitas |
| Fórmulas de Produtos | **143** | Fórmulas/composições usadas na produção interna de produtos |
| Produção de Produtos | **144** | Apontamento de produção a partir das fórmulas |

> 📚 Fonte dos códigos: [`Sol.NET/Form/uFrmProcessoAtualizacaoPrincipal.pas`](https://github.com/hetosoft/ProjetosSol.NET/blob/develop/Sol.NET/Form/uFrmProcessoAtualizacaoPrincipal.pas) (`INSERT` na tabela `FORMULARIOS`). Os códigos podem ser revisados a cada release — em caso de divergência, prevalece o arquivo no repositório.

> 💡 A **emissão integrada** à venda **não tem entrada própria pelo F1**: ela é disparada **automaticamente** pelo Sol.NET quando uma movimentação do tipo fiscal contém itens que exigem receituário (veja [Emissão Integrada à Movimentação](#-emissão-integrada-à-movimentação-gatilho-automático)).

---

## 🧩 Conceitos Básicos

| Termo | O que é |
|-------|---------|
| **Cultura** | Planta cultivada onde o produto será aplicado (Soja, Milho, Café…). |
| **Diagnóstico** | Alvo biológico a controlar — fungo, inseto, planta daninha ou nematóide. |
| **Formulado** | Defensivo agrícola registrado no MAPA, identificado pelo nº de registro. |
| **Bula (Configuração de Bula)** | Combinação autorizada **Formulado × Cultura × Diagnóstico** com dose mín./máx., unidade, modalidade de aplicação e dias de carência. |
| **Profissional** | Responsável técnico habilitado (Eng. Agrônomo no CREA ou Téc. Agrícola no CFTA). |
| **ART/TRT** | Bloco numerado de receituários liberado pelo conselho profissional para o responsável técnico. Tem **número inicial**, **número final**, **saldo atual** e **data de validade**. |
| **Local de Aplicação** | Fazenda/talhão do cliente onde o produto será efetivamente aplicado. |
| **Calda** | Mistura final aplicada (volume e produtos). |
| **Receituário** | Documento emitido (cabeçalho + itens) que vincula tudo o acima. |

---

## 🔁 Pré-requisitos e Ordem Recomendada

Antes de emitir a primeira receita, conclua os cadastros nesta ordem:

1. **Culturas** atendidas pela revenda
2. **Diagnósticos** (alvos) recorrentes na região
3. **Tipos de Embalagem** e **Embalagens** dos produtos comercializados
4. **Formulados** em estoque (com nº de registro MAPA)
5. **Configuração de Bula** para cada combinação válida (Produto × Cultura × Alvo)
6. **Profissionais** habilitados que assinarão receitas
7. **ART/TRT** de cada profissional, **vinculadas à empresa operadora**
8. **Locais de Aplicação** dos clientes ativos

> 💡 Sem qualquer um destes itens, a emissão é bloqueada e o Sol.NET informa o que está faltando.

---

## 📚 Cadastros de Apoio

### 🌾 Cadastro de Culturas

Registra as plantas cultivadas onde os defensivos serão aplicados.

**Acesso:** F1 → `Cadastro Cultura Agronômica` (código **138**)

**Campos principais:**
- **Nome Comum**: ex. "Soja", "Milho", "Café Arábica"
- **Nome Científico**: ex. "Glycine max" (aceita maiúsculas e minúsculas)
- **Situação**: Ativo / Inativo

**Dicas:**
- Use o **nome comum** que aparece no rótulo do produto e no contrato com o cliente
- Inative culturas que a revenda deixou de atender (não as exclua, para preservar histórico)

---

### 🐛 Cadastro de Diagnósticos

Cadastra os alvos biológicos que podem ser tratados.

**Acesso:** F1 → `Cadastro Diagnóstico Agronômico` (código **139**)

**Campos principais:**
- **Nome Vulgar**: ex. "Ferrugem Asiática", "Lagarta-do-cartucho"
- **Nome Científico**: ex. "Phakopsora pachyrhizi"
- **Tipo de Alvo**: Fungo, Inseto, Planta Daninha ou Nematóide
- **Situação**: Ativo / Inativo

**Dicas:**
- O **Tipo de Alvo** organiza relatórios e filtros por classe agronômica do problema
- Cadastre também sinônimos populares como observação, para facilitar buscas

---

### 🧪 Cadastro de Formulados

Cadastra cada defensivo comercializado, com base no **registro MAPA**.

**Acesso:** F1 → `Cadastro Formulado Agronômico` (código **140**)

**Campos principais:**
- **Nº de Registro MAPA**
- **Marca Comercial**
- **Titular do Registro** e **CNPJ do Titular**
- **Classe Agronômica**: Herbicida, Inseticida, Fungicida, Acaricida, etc.
- **Classificação Toxicológica**
- **Classificação Ambiental**
- **Modo de Ação**
- **Compatibilidade** (com outros produtos)
- **Advertência Ambiental**
- **Embalagem(ns)** comercializada(s) e o respectivo **Tipo de Embalagem**

> O cadastro de Formulados é também acessado a partir da aba "Receituário Agronômico" no **Cadastro de Produtos** — assim, o produto comercial fica vinculado ao formulado correspondente.

---

### 📖 Configuração de Bula (Bula Digital)

É o coração das validações. Define **o que é permitido**: produto, cultura, alvo, dose mín./máx., unidade, modalidade e carência.

**Acesso:** F1 → `Cadastro Config Bula Agronômico` (código **141**)

**Campos principais:**
- **Formulado**, **Cultura**, **Diagnóstico**
- **Dose Mínima** e **Dose Máxima** (no padrão da bula registrada)
- **Unidade de Medida**: L/ha, kg/ha, mL/100L, etc.
- **Modalidade de Aplicação**: foliar, jato dirigido, tratamento de sementes, etc.
- **Dias de Carência**

**Regra:** sem entrada compatível na configuração de bula, a combinação **não pode** ser receitada. Esse bloqueio impede prescrições off-label.

> 💡 Mantenha as bulas atualizadas. Toda renovação de registro do MAPA pode alterar dose, modalidade ou carência.

---

### 📦 Embalagens e Tipos de Embalagem

Permitem registrar as embalagens em que cada produto é vendido. **Tipos de Embalagem** (frasco, bombona, saco, big bag, etc.) e **Embalagens** específicas (com volume/peso) ficam vinculados ao **Formulado** correspondente — o cadastro é feito a partir da própria tela `Cadastro Formulado Agronômico` (código **140**), na aba/abas de embalagens.

A embalagem entra na receita para o cálculo correto da quantidade total a entregar ao produtor rural.

---

## 🧑‍🌾 Cadastros Administrativos

### 👤 Cadastro de Profissionais

Registra os responsáveis técnicos habilitados a assinar receituários (inclusive externos à empresa).

**Acesso:** F1 → `Profissionais Externos` (código **135**)

**Campos principais:**
- **Nome completo**
- **CPF**
- **Tipo de Conselho**: CREA (Eng. Agrônomos) ou CFTA (Técnicos Agrícolas)
- **Registro no Conselho** (nº)
- **UF do Registro**
- **Endereço, Cidade, Estado** (profissionais externos)
- **Situação**: Ativo / Inativo

**Profissionais externos** (que não são da empresa) podem ser cadastrados para casos em que o responsável técnico não é funcionário, mas presta o serviço.

---

### 📋 Cadastro de ART/TRT

Cada bloco de receituário liberado pelo conselho deve ser cadastrado para que o sistema controle saldo e validade.

**Acesso:** F1 → `Gestão ART/TRT` (código **136**)

**Campos principais:**
- **Profissional** responsável
- **Empresa** vinculada (obrigatório — cada bloco pertence a uma empresa do grupo)
- **Número da ART Mãe**
- **Número Inicial** e **Número Final** da sequência
- **Saldo Atual** (quantas receitas ainda podem ser emitidas)
- **Quantidade de Aviso** (limite para alertar reposição)
- **Data de Validade**
- **Situação**: Ativo / Inativo

**Regras:**
- Apenas ARTs **ativas**, com **saldo > 0** e **dentro da validade** aparecem na seleção ao emitir uma receita.
- ARTs já em uso podem ser **inativadas** quando substituídas.
- Em pesquisa de seleção durante a emissão, o sistema mostra **somente as ARTs da empresa logada e com saldo**.
- Ao **emitir**: o saldo é decrementado e o número sequencial é consumido.
- Ao **cancelar** uma receita: o saldo é estornado para a mesma ART (e o número fica reservado historicamente).

> 🔔 **Alerta de saldo:** quando o `Saldo Atual` atinge a `Quantidade de Aviso`, o Sol.NET exibe alerta na tela e na lista de ARTs acabando.

---

### 🏞️ Cadastro de Locais de Aplicação

Cada cliente pode ter várias fazendas/talhões. O receituário sempre indica **onde** o produto será aplicado. Os locais ficam vinculados ao **Cliente** e são mantidos a partir do próprio cadastro do cliente / dentro da emissão do receituário.

**Campos principais:**
- **Cliente** (vinculado obrigatoriamente)
- **Descrição** (ex. "Fazenda Santa Rita - Talhão 4")
- **Endereço completo**
- **Cidade** e **UF**
- **Situação**: Ativo / Inativo

> 💡 Padronize a descrição. Evite duplicidades como "Fazenda Sta. Rita T4" e "Faz. Santa Rita - Talhão 04" para o mesmo lugar.

---

## 🧾 Emissão de Receituário

A emissão pode ocorrer de duas formas: **integrada** ao processo de venda (recomendada) ou **avulsa**.

### 🔁 Emissão Integrada à Movimentação (Gatilho Automático)

É o caminho mais comum. A receita é gerada a partir dos itens da Movimentação que exigem receituário, **sem necessidade de atalho ou comando do operador**: quando a movimentação é do **tipo fiscal** e contém itens vinculados a um formulado agronômico, o Sol.NET **dispara automaticamente** a tela de receituário no momento adequado do fluxo, para que o usuário preencha os dados e finalize a receita.

**Passo a passo:**

1. Lance a **Movimentação** normalmente (movimento fiscal — NF-e, NFC-e ou demais documentos fiscais que comportem venda de defensivos).
2. Inclua os itens. Produtos vinculados a um formulado agronômico são identificados como itens que exigem receita.
3. Ao avançar no fluxo da movimentação, o Sol.NET **abre automaticamente** a tela de Receituário com:
   - Cliente já preenchido
   - Itens que exigem receita já carregados
   - Profissional sugerido (último utilizado)
   - ART sugerida automaticamente (a primeira ativa, com saldo, da empresa)
4. Selecione o **Local de Aplicação** do cliente.
5. Confirme **Cultura**, **Diagnóstico** e **Modalidade de Aplicação** de cada item.
6. Informe a **Dose Aplicada** e a **Área Tratada** — a **Quantidade Total é calculada automaticamente** (Dose × Área).
7. Preencha as observações (se houver).
8. **Salve.** O sistema executa as validações e, se tudo estiver ok, gera o número da receita.
9. **Imprima** as vias.

> 📌 O gatilho automático **só acontece em movimentos do tipo fiscal**. Movimentos não fiscais (orçamento, pedido sem fiscalização etc.) não disparam a emissão automática — para esses casos, use a **emissão avulsa** descrita a seguir.

> 📌 A emissão **não exige protocolo de NF-e autorizado**. A tela é aberta no fluxo da movimentação fiscal, e a receita pode ser concluída antes do retorno da SEFAZ.

> 📎 Cada item de movimentação pode ter sua própria associação ao receituário. O vínculo é por **item de movimento**, não pelo movimento como um todo — útil para vendas mistas (com e sem itens que exigem receita).

---

### 📝 Emissão Avulsa

Use quando não há movimentação fiscal associada no momento (assistência técnica em campo, recomposição de prescrição, recomendação preliminar antes da venda, etc.).

**Acesso:** F1 → `Receituário Agronômico` (código **142**) → **Novo**.

**Regra importante sobre o vínculo com movimentação:**

- **Para lançar/cadastrar** o receituário avulso, **não é obrigatório** vincular uma movimentação. Você pode preencher cliente, profissional, ART, local, itens e doses livremente.
- **Para emitir e imprimir** o receituário, o **vínculo a uma movimentação é obrigatório**. Sem esse vínculo, o sistema permite salvar o cadastro mas **bloqueia a emissão/impressão** definitiva.
- Use esse comportamento quando precisar adiantar o preenchimento técnico (em campo, por exemplo) e completar a vinculação fiscal posteriormente, antes de imprimir.

Os campos disponíveis são os mesmos da emissão integrada.

---

### 🧮 Cálculo Automático da Área Tratada

Ao informar **Dose Aplicada** e **Quantidade Total** (ou **Área Tratada**), o Sol.NET completa automaticamente o terceiro valor:

- `Quantidade Total = Dose Aplicada × Área Tratada`
- `Área Tratada = Quantidade Total ÷ Dose Aplicada`

Isso reduz erros de digitação e garante coerência entre a quantidade vendida e a área a tratar.

---

## ✅ Validações Automáticas

Antes de gerar o número da receita, o Sol.NET verifica:

1. **Empresa × ART** — a ART selecionada deve pertencer à empresa logada.
2. **Cliente × Local** — o local de aplicação deve pertencer ao cliente da venda.
3. **Saldo de ART** — `Saldo Atual` > 0.
4. **Validade da ART** — `Data de Validade` ≥ data atual (validação ignorada se a data não tiver sido preenchida no cadastro).
5. **Combinação Formulado × Cultura × Diagnóstico** — deve existir em **Configuração de Bula**.
6. **Dose dentro do permitido** — `Dose Mínima` ≤ `Dose Aplicada` ≤ `Dose Máxima`.
7. **Modalidade de Aplicação** — campo obrigatório.
8. **Cliente válido** — não permite cliente padrão (ex. "consumidor padrão") nem caracteres especiais inválidos no nome.
9. **Tipo de Aplicação** — campo obrigatório.

Se alguma validação falhar, o Sol.NET exibe a mensagem específica e bloqueia a emissão.

---

## 🖨️ Impressão (ReportBuilder)

A impressão usa o **ReportBuilder** do Sol.NET, com layout próprio do receituário agronômico.

- Acessível pelo botão **Relatórios** da tela do receituário (habilitado após salvar).
- Layout segue o modelo legal exigido pelo MAPA com campos de devolução de embalagens, advertência ambiental e assinatura do responsável técnico.
- O texto de **devolução de embalagens** é registrado no momento da emissão como um *snapshot* — alterações futuras nesse texto **não** afetam receitas já emitidas.
- Em geral imprima **3 vias**: comprador, vendedor e responsável técnico (verifique a regra do órgão estadual).

---

## ↩️ Cancelamento de Receituário

Erros acontecem (cliente errado, dose digitada incorretamente, troca de produto). O Sol.NET permite cancelar receitas já emitidas.

**Como cancelar:**
1. Abra a receita pelo menu de Receituários.
2. Clique em **Cancelar Receituário**.
3. Confirme a operação.

**O que acontece:**
- A receita muda para a situação **Cancelada** (não é excluída, para preservar histórico).
- O **saldo da ART é estornado** automaticamente.
- O número da receita **permanece reservado** — não é reaproveitado.
- A movimentação associada é **desvinculada** da receita.

> ⚠️ Imprima um documento de cancelamento e arquive junto à via cancelada. Algumas defesas estaduais exigem essa rastreabilidade.

---

## 🧭 Integração com Outros Módulos

| Módulo | Ponto de integração |
|--------|---------------------|
| **Cadastro de Produtos** | Aba "Receituário Agronômico" vincula o produto comercial ao formulado MAPA. |
| **Cadastro de Pessoas** | Cliente da venda; locais de aplicação dependem de cliente válido. |
| **Cadastro de Empresas** | A ART é vinculada a uma empresa específica do grupo. |
| **Movimentação** | Em movimentos fiscais com itens que exigem receita, o Sol.NET abre o Receituário automaticamente; vínculo por item. |
| **Profissionais Externos** | Endereço, cidade e estado para receitas assinadas por profissional contratado. |

---

## 🔔 Alertas e Auditoria

- **Alerta de ARTs acabando**: lista as ARTs cujo saldo atingiu a `Quantidade de Aviso`.
- **Usuário que criou** e **Usuário que emitiu** ficam registrados em cada receita (rastreabilidade).
- **Data e hora de emissão** registradas automaticamente.
- **Histórico de cancelamentos** preservado mesmo após estorno.

---

## 💡 Exemplos Práticos

### Exemplo 1 — Venda de fungicida para soja

**Contexto:** revenda em Maringá (PR), cliente "Fazenda Boa Vista", 50 ha de soja com Ferrugem Asiática.

**Passos:**
1. Lança Movimentação fiscal (NF-e) de venda.
2. Adiciona o item "Fungicida XYZ 1L" — quantidade 25 frascos.
3. Ao avançar no fluxo da venda, o Sol.NET **abre o Receituário automaticamente** com cliente e item já preenchidos.
4. Profissional sugerido: "João Eng. Agrônomo - CREA-PR 12345" (último usado).
5. ART sugerida: "Bloco 2026/1, saldo 38 receitas".
6. Local de Aplicação: "Fazenda Boa Vista - Talhão Norte".
7. Cultura: Soja • Diagnóstico: Ferrugem Asiática • Modalidade: Foliar.
8. Dose: 0,5 L/ha • Área: 50 ha → Quantidade Total: 25 L (calculada).
9. Salva. Sistema valida bula (0,4 a 0,8 L/ha — ok) e gera receita **nº 12463**.
10. Imprime 3 vias e entrega ao cliente.

### Exemplo 2 — Bula bloqueia combinação

**Contexto:** mesmo cliente quer usar o mesmo fungicida em "Lagarta-da-soja" (alvo errado).

**Resultado:** ao salvar, Sol.NET informa: *"Combinação Produto × Cultura × Alvo não permitida. Verifique a Configuração de Bula."*

**Solução:** consultar o rótulo do produto. Se a recomendação contra o alvo realmente não existe na bula registrada, **não cadastre** uma exceção para a venda — recomende ao cliente um inseticida adequado, com bula correspondente.

### Exemplo 3 — ART acabando

**Contexto:** ART "Bloco 2026/1" começou com 50 receitas, está em 5. Quantidade de Aviso configurada: 5.

**Resultado:** ao emitir a próxima receita, o sistema mostra alerta na tela:
> *"Atenção: restam apenas 4 receitas nesta ART. Providencie nova ART junto ao conselho."*

A receita é emitida normalmente, mas o gestor já é avisado.

### Exemplo 4 — Cancelamento por engano de dose

**Contexto:** receita 12463 saiu com 1,5 L/ha (acima do permitido — só passou porque a bula estava errada). Bula corrigida; receita precisa ser refeita.

**Passos:**
1. Abrir a receita 12463 → **Cancelar**.
2. Saldo da ART volta de 37 para 38.
3. Emitir nova receita com a dose correta. Receberá o próximo número disponível (12464).

---

## ❓ FAQ / Problemas Comuns

**"Não há ART disponível para a empresa atual."**
→ Cadastre uma ART na tela `Gestão ART/TRT` (F1, código **136**) vinculando o profissional **e a empresa logada**.

**"Combinação Produto × Cultura × Alvo não permitida!"**
→ Não há bula cadastrada para essa combinação. Consulte o rótulo oficial do produto: se houver, cadastre na tela `Cadastro Config Bula Agronômico` (F1, código **141**); se não houver, a aplicação é off-label e não pode ser receitada.

**"Dosagem fora do permitido!"**
→ O valor digitado está abaixo da `Dose Mínima` ou acima da `Dose Máxima` da bula. Ajuste a dose ou revise a bula (se foi cadastrada com erro).

**"A ART está vencida."**
→ Renove o bloco junto ao conselho profissional, cadastre a nova ART e inative a anterior.

**"Local de aplicação não pertence ao cliente."**
→ Verifique se o local foi cadastrado para o cliente correto. Edite o cadastro se necessário.

**Para mais perguntas, consulte o [FAQ completo](FAQ.md).**

---

## 🔗 Documentação Complementar

- **[Guia Rápido](Guia%20Rapido.md)** — checklist e atalhos
- **[FAQ](FAQ.md)** — perguntas frequentes
- **[Movimentação](../Movimentacao/Documentacao%20Movimentacao.md)** — fluxo da venda
- **[Portal de Documentação](../README.md)** — visão geral do Sol.NET

---

**📅 Última atualização**: Abril de 2026
**📦 Versão**: 1.0
**🎯 Público-alvo**: Vendedores de revenda agropecuária, responsáveis técnicos, administradores Sol.NET
