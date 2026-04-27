# 📄 FAQ - Receituário Agronômico - Sol.NET

## 🎯 Visão Geral

Perguntas frequentes sobre o Módulo Agronômico do Sol.NET ERP. Para o passo a passo completo veja a **[Documentação Receituário Agronômico](documentacao_receituario_agronomico.md)** e para o checklist diário veja o **[Guia Rápido](guia_rapido.md)**.

---

## 🧭 Conceitos e Cadastros

### O que é o Módulo Agronômico do Sol.NET?
É o conjunto de cadastros e a tela de emissão que permitem produzir o **receituário agronômico** exigido por lei para a comercialização e aplicação de defensivos agrícolas. Cobre cadastros (culturas, alvos, formulados, bulas, embalagens, profissionais, ARTs, locais), validações automáticas, emissão integrada à venda, impressão e cancelamento.

### Qual a diferença entre **Cultura**, **Diagnóstico** e **Formulado**?
- **Cultura** é a planta cultivada (Soja, Milho, Café…).
- **Diagnóstico** é o alvo biológico (uma praga, doença, planta daninha ou nematóide).
- **Formulado** é o defensivo registrado no MAPA.

A **Configuração de Bula** liga os três: define quais combinações são permitidas e em que dose.

### O que é uma "Bula" no Sol.NET?
É o registro digital da bula oficial: para cada **Formulado × Cultura × Diagnóstico**, define a **Dose Mínima**, **Dose Máxima**, **Unidade de Medida**, **Modalidade de Aplicação** e **Dias de Carência**. Sem essa entrada, a combinação **não pode** ser receitada.

### O que é uma ART/TRT?
É a **Anotação de Responsabilidade Técnica** (ART, no CREA) ou **Termo de Responsabilidade Técnica** (TRT, no CFTA). No Sol.NET, cada bloco numerado liberado pelo conselho é cadastrado com número inicial, número final, saldo, validade e a empresa do grupo a que pertence.

### Eu tenho que cadastrar todos os defensivos do MAPA?
Não. Cadastre **apenas os que a sua revenda comercializa**. Quando entrar um produto novo, cadastre o formulado e suas bulas antes de vender.

---

## 👤 Profissional Responsável

### Quem pode assinar receituários?
Profissionais com habilitação legal:
- **Engenheiro Agrônomo** — registro no **CREA**
- **Técnico Agrícola** — registro no **CFTA**

Cada um tem suas atribuições específicas, definidas pelo conselho de classe e pela legislação federal/estadual.

### O profissional precisa ser funcionário da empresa?
Não. O Sol.NET tem o conceito de **profissional externo** (com endereço, cidade e estado), o que permite assinar receitas para uma revenda sem ter vínculo CLT.

### Posso cadastrar várias UFs para o mesmo profissional?
Cadastre o profissional uma vez e indique a **UF do registro** principal. Se ele atua em várias UFs com registros separados, faça cadastros separados — assim cada bloco de ART correto fica vinculado à UF correspondente.

---

## 📋 ART/TRT

### Por que a ART precisa ser vinculada à empresa?
Porque cada empresa do grupo (matriz, filial) opera com seu próprio bloco. A validação automática garante que a receita emitida em uma filial **consuma a ART da própria filial** — não a ART de outra unidade.

### Posso lançar um receituário avulso sem vincular movimentação?
**Sim, para o cadastro/lançamento.** Mas para **emitir/imprimir** definitivamente, o vínculo a uma movimentação **é obrigatório**. O fluxo típico é: preencher os dados em campo (sem movimentação), salvar, e depois — ao retornar à revenda — vincular a movimentação correspondente e imprimir.

### Cadastrei a ART, mas ela não aparece na seleção da emissão. Por quê?
Possíveis causas (verifique na tela `Gestão ART/TRT`, código **136**):
- A ART **não está ativa** (`Situação = Inativo`)
- O **saldo é zero**
- A **data de validade já passou**
- A ART está **vinculada a outra empresa** (e você está logado na empresa errada)
- Já está marcada como **em uso** por outra emissão

A pesquisa de seleção mostra apenas ARTs ativas, da empresa logada e com saldo.

### Como o sistema decide qual ART sugerir automaticamente?
A primeira ART **ativa**, **com saldo**, **dentro da validade** e **vinculada à empresa logada** para o profissional informado.

### Como recebo aviso quando uma ART está acabando?
Defina o campo **Quantidade de Aviso** no cadastro da ART (ex.: 5). Quando o saldo atinge esse valor, o Sol.NET exibe um aviso ao emitir e a ART aparece na lista de "ARTs acabando".

### Posso editar o número inicial/final depois de cadastrar?
Pode, **enquanto a ART não tiver receitas emitidas**. Após o primeiro consumo, evite alterar a numeração — perde-se a rastreabilidade.

### Excluí uma receita por engano e o saldo da ART não voltou. O que fazer?
Você não deve **excluir**, apenas **cancelar**. O cancelamento é a única operação que retorna o saldo. Se foi excluída via banco, abra chamado com o suporte.

---

## 🧾 Emissão

### Posso emitir receituário sem ter NF-e autorizada?
Sim. O Sol.NET **não exige protocolo de NF-e autorizado** para emitir. A receita pode ser produzida antes da SEFAZ autorizar a NF — desde que a movimentação fiscal já esteja lançada e com os itens necessários.

### Como abro a tela de Receituário?
Pela **pesquisa universal de telas** do Sol.NET (atalho **F1**). Digite o código da tela `Receituário Agronômico` (consulte os códigos atuais em [`uFrmProcessoAtualizacaoPrincipal.pas`](https://github.com/hetosoft/ProjetosSol.NET/blob/develop/Sol.NET/Form/uFrmProcessoAtualizacaoPrincipal.pas)) ou parte do nome.

Para **emissão integrada à venda**, **não precisa abrir nada manualmente**: ao avançar uma movimentação fiscal com itens que exigem receita, o Sol.NET dispara a tela automaticamente.

### A movimentação tem produto que exige receita, mas o Sol.NET não abriu o Receituário automaticamente. Por quê?
O gatilho automático ocorre **somente em movimentos do tipo fiscal**. Verifique:
- A movimentação foi lançada como movimento fiscal (NF-e, NFC-e ou equivalente).
- O produto comercial está vinculado a um **Formulado** no `Cadastro de Produtos` (aba "Receituário Agronômico").

Se a venda não é fiscal e ainda assim você precisa de receita, use a **emissão avulsa** pela tela `Receituário Agronômico` (F1).

### Por que aparece "Combinação Produto × Cultura × Alvo não permitida"?
Não existe entrada na Configuração de Bula para essa tríade. Duas situações:
1. A combinação está na bula MAPA mas ainda não foi cadastrada → cadastre em `Cadastros > Configuração de Bula`.
2. A combinação **não está** na bula registrada → é uso off-label, **não emita**.

### Por que aparece "Dosagem fora do permitido"?
A dose informada está abaixo de `Dose Mínima` ou acima de `Dose Máxima` cadastradas na bula. Reveja o valor digitado. Se o limite cadastrado estiver desatualizado, atualize a bula com base no rótulo oficial.

### A área tratada precisa ser exata?
Sim, a partir dela o sistema calcula a quantidade total. Erros aqui resultam em quantidade prescrita incorreta. Use a medição da fazenda do cliente, não estimativas.

### Posso emitir receita para "Consumidor Padrão" do balcão?
Não. O Sol.NET bloqueia clientes genéricos e nomes com caracteres especiais inválidos. Identifique o produtor (CPF/CNPJ).

### A modalidade de aplicação é obrigatória?
Sim. Defina se é foliar, em sulco, tratamento de sementes, jato dirigido, etc. — esse campo é validado.

---

## 🏞️ Locais de Aplicação

### Preciso cadastrar local mesmo quando o produto vai ser aplicado em uma fazenda só?
Sim. O receituário **sempre** indica o local. Se o cliente tem só uma fazenda, basta cadastrar uma vez.

### Cadastrei um local para o cliente errado. O que fazer?
Edite o local em `Cadastros > Locais de Aplicação` e altere o cliente, ou inative-o e cadastre novo no cliente correto.

### Posso reaproveitar o mesmo local entre clientes?
Não. Cada local é vinculado a **um cliente**. Se duas pessoas dividem a mesma fazenda, cadastre dois locais (um por cliente) com a mesma descrição/endereço.

---

## 🖨️ Impressão e Vias

### Quantas vias devo imprimir?
Em geral **3 vias**: comprador, vendedor e responsável técnico. Verifique a regra do órgão estadual de defesa agropecuária da sua UF — pode haver exigências específicas (ex.: via para o agente fiscal).

### O texto de devolução de embalagens mudou. As receitas antigas saem com o novo texto?
Não. O texto é registrado como **snapshot** no momento da emissão. Receitas antigas mantêm o texto que estava em vigor naquele momento. Receitas novas usarão o texto atual.

### Posso reimprimir uma via?
Sim. Abra a receita e use o botão **Relatórios**.

### O layout do receituário é editável?
Sim, via **ReportBuilder**. Cuidado: o modelo deve atender ao formato exigido pelo MAPA e pelo órgão estadual. Antes de modificar, valide com o responsável técnico.

---

## ↩️ Cancelamento

### Como cancelo uma receita errada?
Abra a receita e clique em **Cancelar Receituário**. O sistema:
- Marca a situação como **Cancelada** (não exclui).
- Estorna o saldo da ART.
- Reserva o número (não reaproveita).
- Desvincula a movimentação.

### Por que o número não é reaproveitado?
Para preservar a rastreabilidade legal. Cada número emitido fica registrado para sempre, mesmo cancelado, e fica disponível para auditoria.

### Posso cancelar uma receita de meses atrás?
Tecnicamente sim. Mas verifique a política da sua empresa e a posição do órgão estadual antes — em alguns estados, o cancelamento tardio pode exigir documentação adicional.

### Cancelei a receita mas a movimentação ainda existe. Por quê?
Porque o cancelamento da receita **não cancela** a venda. Se a venda também precisa ser cancelada, faça-o em separado, na Movimentação.

---

## 🔗 Integração com a Venda

### O receituário fica anexado à NF-e?
A receita fica **vinculada à movimentação** (e ao item específico, quando há mais de um). Os dados da receita são preservados no movimento, e a impressão segue o modelo do receituário separadamente.

### Posso clonar uma movimentação que tem receituário?
Sim. A clonagem da movimentação **não copia** o receituário associado — ele continua atrelado ao movimento original. Você precisa emitir novo receituário para o movimento clonado.

### Posso emitir várias receitas para a mesma movimentação?
Não pela emissão automática a partir da movimentação. Cada item de movimento tem **uma** associação a receituário. Se a venda tem múltiplos produtos com receita, todos saem em **um único receituário com vários itens**.

---

## 📊 Relatórios e Histórico

### Como vejo todas as receitas de um cliente?
Abra `Receituário Agronômico` (F1, código **142**) e filtre por cliente. Há um índice otimizado para isso (busca rápida).

### Como vejo o consumo de ART de um profissional?
Abra `Gestão ART/TRT` (F1, código **136**). A coluna `Saldo Atual` versus `Número Inicial`/`Final` mostra quantas receitas já foram consumidas.

### Os usuários que criaram e emitiram a receita ficam registrados?
Sim. Cada receita guarda **usuário que criou** e **usuário que emitiu**, além de data e hora. Use no auditoria interna.

---

## 🏛️ Conformidade Legal

### O Sol.NET transmite o receituário automaticamente para a defesa agropecuária estadual?
Não. A impressão segue o modelo legal, mas a entrega/transmissão a ADAPAR (PR), IDARON (RO), IAGRO (MS), SEAPDR (RS), IDAF (ES) e equivalentes é feita conforme as regras de cada órgão (em geral por sistemas próprios ou entrega física). Consulte a defesa do seu estado.

### O receituário é emitido em nome da empresa ou do agrônomo?
O **responsável técnico** é o profissional (com seu CREA/CFTA). A empresa emissora aparece como estabelecimento comercial. A ART pertence a um profissional **e** a uma empresa específica.

### Preciso de receita para venda balcão de qualquer agrotóxico?
Em geral, sim — agrotóxicos no Brasil exigem receituário independente do canal. Há exceções pontuais para alguns produtos de uso doméstico/jardinagem (ex.: certos formulados específicos liberados sem receita). Consulte sempre o rótulo e a legislação atual.

### Quanto tempo devo guardar as receitas?
A legislação vigente (Decreto 4.074/2002 e atualizações estaduais) exige guarda por anos. Como o Sol.NET preserva o registro digital de toda receita (inclusive canceladas), o histórico fica disponível para auditoria. Mantenha as **vias físicas** conforme a regra do seu estado.

---

## 🔒 Permissões e Acesso

### Quem pode emitir receita no sistema?
Qualquer usuário com permissão para o módulo. A **assinatura legal** é do responsável técnico (profissional cadastrado), independentemente de quem operou o sistema. O Sol.NET registra os dois (usuário que criou + usuário que emitiu).

### Posso restringir cancelamento a supervisores?
Use o sistema de perfis e permissões do Sol.NET para limitar a ação **Cancelar Receituário** apenas aos perfis autorizados.

---

## 🆘 Suporte

### A configuração de bula está cadastrada e mesmo assim o sistema bloqueia. O que fazer?
1. Confira se o produto da venda está vinculado ao **formulado** correto.
2. Confira se a **cultura** e o **diagnóstico** selecionados são exatamente os mesmos da bula cadastrada.
3. Verifique se a entrada de bula está com situação **Ativa**.

### Onde abro chamado de suporte?
Pelo canal oficial Hetosoft. Inclua: print da mensagem de erro, número da receita (se houver), nome do produto/cultura/alvo e nome da empresa logada.

---

## 🔗 Documentação Complementar

- **[Documentação Receituário Agronômico](documentacao_receituario_agronomico.md)** — referência completa
- **[Guia Rápido](guia_rapido.md)** — checklist diário
- **[Índice do Módulo](README.md)**
- **[Portal Sol.NET](../README.md)**

---

**📅 Última atualização**: Abril de 2026
**📦 Versão**: 1.0
**🎯 Público-alvo**: Vendedores de revenda agropecuária, responsáveis técnicos, administradores Sol.NET
