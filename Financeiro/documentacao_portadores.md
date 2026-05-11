# 📄 Cadastro de Portadores - Sol.NET

## 🎯 Visão Geral

O **Portador** no Sol.NET representa o **mecanismo de cobrança ou pagamento** associado a um título do Financeiro. Cada portador concentra a configuração necessária para que o sistema saiba como **emitir**, **transmitir** e **dar baixa** em títulos — banco, agência, conta corrente, layout do arquivo (CNAB), tipo de documento (boleto / carnê / nota promissória / convênio), tarifas, valores e dias de juros, multa, desconto e abatimento, integrações on-line (Hetobank, PIX) e regras de comissão.

É o portador que determina, por exemplo, *qual banco* emite um boleto, *qual layout* o arquivo de remessa segue, ou *que mensagem* aparece impressa.

---

## 🔑 Como acessar

| | |
|---|---|
| **Tela** | Cadastro de Portadores |
| **Código (`F1`)** | `12` |

Abra a pesquisa universal (atalho `F1`) e digite **`12`** ou parte do nome **`Portadores`**.

---

## 🧭 Estrutura da tela

A tela tem duas áreas principais (padrão dos cadastros do Sol.NET):

1. **Tab `Visualizar`** — grid de busca com colunas `Descrição`, `Código`, `Tipo Documento`, `Descrição da Loja` e filtro de status (ativo/inativo). Duplo clique numa linha leva direto à edição.
2. **Tab `Cadastrar`** — formulário organizado em sub-abas conforme o tipo de portador e a profundidade da configuração.

### Sub-abas do `Cadastrar`

| Aba | Para quê serve |
|------|----------------|
| **Boleto** | Configuração principal para portadores do tipo Boleto (banco, layout, beneficiário, valores) |
| **Carnê** | Configuração específica de carnês |
| **Nota Promissória** | Configuração específica de notas promissórias |
| **Convênio** | Configuração específica de convênios |
| **Boleto Extra** | Configurações adicionais do boleto (subdividida em: `Geral`, `On-Line`, `Cob. Bancaria`, `Instrução Desabilitadas`) |
| **Comissão** | Percentuais de comissão (PC_COMISSAO1, PC_COMISSAO2) |
| **Empresas** | Multi-empresa: permite vincular o mesmo portador a várias empresas com regras distintas |
| **HetoBank** | Configuração para integração via HetoBank |
| **Bancária** | Padrões usados quando o portador gera lançamento no plano de contas (Plano de Contas, Centro de Custo, Tipo de Conta) |

---

## 📝 Campos principais

### Identificação (painel sempre visível no topo do `Cadastrar`)

| Label | Para quê serve |
|-------|----------------|
| **Código** | Código interno do portador (até 30 caracteres) |
| **Descrição** | Nome amigável (até 50 caracteres) |
| **Tipo Documento** | Define o comportamento principal: `Boleto`, `Carnê`, `Nota Promissória` ou `Convênio` |
| **Empresa** | Empresa proprietária deste portador |
| **Empresa Remessa** | Empresa usada na geração do arquivo de remessa (alternativa exclusiva à `Empresa`) |
| **Conta Corrente** | Conta corrente vinculada |
| **Caixa** | Caixa Geral vinculado |
| **Condição de Pagamento** | Condição padrão |
| **Quant. Digito Nosso Numero** | Quantidade de dígitos usados pelo nosso número |

### Aba `Boleto`

Campos vinculados ao layout bancário (CNAB):

| Label | Observação |
|-------|------------|
| **Banco cobrança** | Identifica o banco/instituição que recebe a cobrança |
| **Remessa** | Tipo de remessa (formato CNAB) |
| **Layout** | Layout do arquivo de remessa (varia por banco) |
| **Beneficiário** | Identificação do beneficiário no boleto |
| **Convenio** | Número do convênio com o banco |
| **Mensagem para local do pagamento** | Mensagem impressa no campo "local do pagamento" do boleto |
| **Espécie Doc.** | Espécie de documento (ex.: `DS/04`) |
| **Espécie Moeda** | Espécie de moeda (ex.: `$`) |
| **Carteira** | Identificação da carteira (ex.: `RG/SR/CNR`) |
| **Aceite** | Indica se o boleto tem aceite |
| **Valor Mora/Juros %** | Percentual de mora/juros mensal |
| **Valor Desconto %** | Percentual de desconto |
| **Valor Abatimento %** | Percentual de abatimento |
| **Valor Multa %** | Percentual de multa por atraso |
| **Dias Multa/Juros** | Dias para começar a cobrar multa/juros |
| **Dias Desconto** | Prazo para conceder desconto |
| **Dias Abatimento** | Prazo para conceder abatimento |
| **Tipo de Protesto** | Define o tipo de protesto (combinado com `Dias Protesto`) |
| **Dias Protesto** | Dias até envio para protesto (válido para tipos de protesto 1, 2 ou 4) |
| **Característica Boleto** | Característica do boleto |
| **Salvar PDF no Banco de Dados** | Marca se o PDF gerado fica armazenado no banco |

### Aba `Boleto Extra → Geral`

Configurações suplementares:

- **Ajustar Valor Recebido pela Taxa de Cobrança** — aplica a taxa cobrada pelo banco no valor recebido
- **Colocar Referência Boleto Anterior** — inclui referência ao boleto anterior na emissão
- **Colocar Descrição Tipo de Contas** — inclui a descrição do tipo de conta na emissão
- **Obs E-Mail** — texto observação enviado por e-mail
- **Obs Boleto** — texto observação impresso no boleto
- **Pasta Padrão Abrir Arquivos (Retorno)** — pasta onde o sistema procura arquivos de retorno bancário
- **Pasta Padrão Salvar Arquivos (Remessa)** — pasta onde o sistema grava arquivos de remessa
- **Baixa de Quitação Remessa e Avisos**
- **Código Transmissão Remessa** — código de transmissão usado no arquivo
- **Ajustar Valor Quitação pelo Desc. e Abat.**
- **Instrução 1**, **Instrução 2** — códigos de instrução bancária (2 caracteres)
- **Adicionar Num. Doc. em Obs** — incluir número do documento na observação
- **Aceitar Recebimento Parcial**
- **Taxa de Cobrança ao processar boleto registrado**
- **Remover último dígito Nosso Número**

### Aba `Boleto Extra → On-Line`

Integração com APIs bancárias (boletos registrados):

| Label | Observação |
|-------|------------|
| **WebService** | Tipo de webservice (varia por banco) |
| **ClientID** | Identificador do cliente na API (até 500 caracteres) |
| **ClientSecret** | Segredo de autenticação (até 500 caracteres) — informação sensível |
| **KeyUser** | Chave do usuário (até 200 caracteres) |
| **Enviar ao Imprimir** | Envia o boleto à API no momento da impressão |
| **Incluir PIX** | Habilita inclusão de PIX no boleto |
| **Tipo chave PIX** | Tipo da chave PIX |
| **Chave PIX** | Chave PIX (até 255 caracteres) |
| **Consulta automática** | Consulta status automaticamente |

### Aba `Boleto Extra → Cob. Bancaria`

Quando o portador gera lançamento no plano de contas (cobrança bancária registrada):

- **Plano de Contas** — plano de contas padrão
- **Centro de Custo** — centro de custo padrão
- **Tipo de Conta** — tipo de conta PR padrão
- **Não gerar registro de Tarifa Bancaria**

### Aba `HetoBank`

Para portadores integrados com a plataforma HetoBank:

- **Forma de Pagamento Hetobank** — vínculo com forma de pagamento específica do HetoBank (validação adicional: a forma escolhida precisa ser do tipo HetoBank, caso contrário o sistema bloqueia com a mensagem *"Forma de pagamento deve ser do tipo Hetobank!"*)

### Aba `Empresas`

Permite associar o mesmo portador a múltiplas empresas com configurações específicas por empresa. Tem grid próprio (inserção, edição e remoção via menu de contexto). Quando alguma linha desta aba está marcada como ativa, a tela bloqueia o uso simultâneo do campo `Empresa` global da aba de identificação.

---

## ✅ Regras de validação automática (na hora de salvar)

A função `Validar` da tela aplica as seguintes regras de forma rígida; o salvamento é abortado caso alguma falhe:

1. **Descrição única**: não pode haver dois portadores com a mesma `Descrição`.
2. **Código único**: não pode haver dois portadores com o mesmo `Código`.
3. **Boleto exige Tipo de Protesto**: se `Tipo Documento = Boleto`, o campo `Tipo de Protesto` é **obrigatório**. Mensagem: *"Obrigatório Preecher 'Tipo de Protesto'!"*.
4. **Remover Juros/Multa não vale para Boleto**: o flag `Remover Juros/Multa` não pode estar marcado se `Tipo Documento = Boleto`. Mensagem: *"Não Permitido! 'Remover Juros/Multa' para Tipo Documento: Boleto"*.
5. **Dias de Protesto só para tipos específicos**: `Dias Protesto > 0` só é aceito quando `Tipo de Protesto` é um dos valores **1, 2 ou 4** (interpretação interna). Para outros tipos de protesto, o campo deve ficar zerado.
6. **Convênio exige "Portador Mudar"**: se `Tipo Documento = Convênio`, o campo `Portador Mudar` é obrigatório. Mensagem: *"Obrigatório Preecher 'Portador Mudar'! Para Tipo Documento: CONVÊNIO"*.
7. **`Empresa` e `Empresa Remessa` são mutuamente exclusivos**: não se pode preencher os dois ao mesmo tempo.
8. **Boleto exige uma das duas**: se `Tipo Documento = Boleto`, é obrigatório preencher `Empresa` **ou** `Empresa Remessa`.
9. **Aba `Empresas` vs campo `Empresa`**: se a aba Empresas tem alguma linha com a opção marcada, o campo `Empresa` global não pode ser usado. Use uma forma **ou** a outra.

> ℹ️ As mensagens exibidas usam o rótulo exato do campo na tela, então podem variar levemente conforme a versão do sistema, mas o sentido é o que está descrito acima.

---

## 🚫 Regras de exclusão

A exclusão é bloqueada quando o portador está em uso. A tela verifica três tabelas antes de excluir:

| Situação | Mensagem |
|----------|----------|
| Existe **pessoa** vinculada a este portador | *"Não permitido, Existe Pessoa(s) com este Portador!"* |
| Existe **conta** (a pagar ou a receber) com este portador | *"Não permitido, Existe Conta(s) com este Portador!"* |
| Existe **movimento** (compra, venda, outros) com este portador | *"Não permitido, Existe Movimento(s) com este Portador!"* |

Em qualquer um desses casos, o portador deve ser **inativado** (marcação de inativo no próprio cadastro) em vez de excluído, preservando o histórico.

---

## 💡 Exemplos práticos

### Criar um portador de Boleto Registrado

1. Pesquisa `F1` → digite `12` → abre o `Cadastro de Portadores`.
2. Clique em **Novo**.
3. Preencha **Código** (ex.: `BB001`) e **Descrição** (ex.: `Banco do Brasil — Boleto Registrado`).
4. Em **Tipo Documento**, escolha `Boleto`.
5. Selecione **Empresa** (ou **Empresa Remessa**, mas não as duas).
6. Selecione **Conta Corrente** e **Caixa**.
7. Na aba **Boleto**:
   - **Banco cobrança**: identificação do banco
   - **Layout**: layout CNAB compatível (ex.: BB 240)
   - **Beneficiário**, **Convenio**, **Carteira**: conforme o convênio com o banco
   - **Tipo de Protesto** (obrigatório para Boleto)
   - Valores de Mora/Juros, Multa, Desconto e Abatimento conforme política comercial
8. Na aba **Boleto Extra → On-Line** (se o boleto for registrado via API):
   - **WebService**, **ClientID**, **ClientSecret**, **KeyUser** fornecidos pelo banco
9. Salve.

### Inativar (em vez de excluir) um portador antigo

1. Localize o portador na aba **Visualizar**.
2. Abra para edição.
3. Marque a opção de inativar o cadastro.
4. Salve.

Isso preserva o histórico de títulos, pessoas e movimentos sem permitir novos lançamentos com esse portador.

---

## ❓ FAQ / Problemas comuns

**Por que não consigo excluir o portador?**
Ele está em uso por pessoa, conta ou movimento. Use a inativação em vez de excluir.

**Posso usar o mesmo portador para várias empresas?**
Sim — use a aba **Empresas**. Lembre-se: quando alguma linha desta aba está marcada como ativa, **não** preencha o campo `Empresa` global da aba de identificação.

**Marquei "Remover Juros/Multa" mas o sistema não deixa salvar.**
Esse flag é proibido em portadores do tipo Boleto. Use apenas em outros tipos de documento.

**O campo `Dias de Protesto` aceita qualquer número?**
Não. Só é aceito quando o `Tipo de Protesto` tem código 1, 2 ou 4. Para outros tipos, deixe zerado.

**O sistema bloqueia ao escolher a forma de pagamento no HetoBank.**
A forma de pagamento associada precisa ser do tipo HetoBank. Cadastre/ajuste em `Formas de Pagamento` (código `7`).

**O Sol.NET emite o boleto registrado direto no banco?**
Depende do **WebService** configurado na aba `Boleto Extra → On-Line`. As credenciais (ClientID, ClientSecret, KeyUser) precisam ter sido emitidas pelo banco para o convênio em questão.

---

## 🔗 Telas relacionadas

| Tela | Código (`F1`) | Relação |
|------|:---:|---------|
| Bancos | `9` | Cadastro do banco usado pelo portador |
| Agências | `10` | Agências usadas pela conta corrente |
| Contas Correntes | `11` | Conta corrente vinculada |
| Formas de Pagamento | `7` | Forma de pagamento (inclusive HetoBank) |
| Cond. de Pagamento | `8` | Condição de pagamento padrão |
| Tipos de Contas PR | `82` | Tipo de Conta usado na aba `Cob. Bancaria` |
| Plano de Contas | `14` | Plano de contas padrão da aba `Cob. Bancaria` |
| Centros de Custos | `15` | Centro de custo padrão da aba `Cob. Bancaria` |
| Pagar e Receber | `301` | Onde o portador efetivamente é usado em títulos |

---

## ⚠️ Limites desta documentação

Esta documentação foi construída a partir da inspeção direta do comportamento da tela no Sol.NET. **Não cobre**:

- **Regras automáticas que rodam dentro do banco de dados** ao salvar/alterar/excluir o registro — podem ajustar ou complementar o que está descrito aqui.
- **Comportamento padrão das caixas de edição, listas e grids** do sistema — esta documentação descreve apenas o que é configurado especificamente neste cadastro.
- **Variações por release** — versões mais novas do Sol.NET podem ter campos adicionais.
- **Comunicação efetiva com bancos e serviços externos** (HetoBank, integrações bancárias para emissão registrada, retorno de cobrança) — esta documentação descreve as configurações disponíveis; o resultado real de cada operação depende da resposta do serviço externo.
- **Modelos de impressão** usados para gerar carnê, nota promissória e convênio.

Para informações fora desse escopo, consulte o suporte Hetosoft.

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 5.0 (refeito do zero descartando a documentação anterior)
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo Financeiro
