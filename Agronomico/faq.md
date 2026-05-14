# 📄 FAQ - Receituário Agronômico - Sol.NET

## 🎯 Visão Geral

Perguntas frequentes sobre o Módulo Agronômico do Sol.NET, organizadas por categoria. Para o passo a passo de emissão, consulte o [Guia Rápido](guia_rapido.md). Para regras detalhadas, veja a [documentação completa](documentacao_receituario_agronomico.md).

---

## Cadastros base

### ❓ Em que ordem cadastrar tudo antes da primeira emissão?

A ordem recomendada é:

1. **Profissionais Externos** (`135`) — engenheiros e técnicos.
2. **Gestão ART/TRT** (`136`) — bloco de receitas do profissional, com empresa, validade e numeração.
3. **Cadastro Cultura Agronômica** (`138`) — culturas que a empresa atende.
4. **Cadastro Diagnóstico Agronômico** (`139`) — pragas, doenças, plantas daninhas.
5. **Cadastro Formulado Agronômico** (`140`) — produtos formulados MAPA. Vincule o produto comercial do ERP ao formulado para que o sistema saiba que ele exige receituário.
6. **Cadastro Config Bula Agronômico** (`141`) — combinação Formulado × Cultura × Diagnóstico com doses, calda, dias de carência e modo de aplicação.
7. **Locais de Aplicação** — cadastrados como endereços do cliente, na aba `Endereços` em **Cadastro de Pessoas** (`5`).

### ❓ Onde cadastro o local onde o defensivo será aplicado?

Na aba **Locais** dentro do **Cadastro de Pessoas** (código `5`), no cliente correspondente. Você cadastra descrição (ex.: "Fazenda Boa Vista – Talhão 2"), endereço, cidade e UF. A UF do local **precisa** ser igual à UF do registro do profissional que vai assinar a receita.

### ❓ Posso usar o mesmo bloco ART para receitas de empresas diferentes da filial?

Não. Cada bloco ART está vinculado a uma empresa específica em **Gestão ART/TRT** (`136`). Se o movimento de venda for de outra empresa, o sistema avisa que o ART não bate e procura/sugere o ART mais antigo ativo da empresa correta.

---

## Emissão

### ❓ Qual é o caminho recomendado para emitir um receituário?

A partir da **Venda** (`202`). Lance o movimento, e a partir dele dispare a emissão — a tela `Receituário Agronômico` (`142`) abre com os dados já preenchidos. Você também pode entrar direto na tela `142` pela pesquisa F1 e amarrar o movimento manualmente, mas o caminho pela venda é mais rápido e tem menos campos para preencher manualmente.

### ❓ O que é a "tríade" Formulado + Cultura + Diagnóstico?

É a combinação obrigatória que o sistema valida contra a bula. Para emitir, a configuração de bula (tela `141`) tem que existir para essa combinação. Se não existir, o sistema não preenche dose nem aceita a emissão.

### ❓ Como o sistema calcula a área tratada?

`Área = (Quantidade Total × 1000) / Dose Aplicada`. O fator `1000` converte mL → L ou g → kg. Sempre que você mexe na Dose ou na Quantidade, a Área é recalculada. Se você digitar uma área diferente da calculada, o sistema pede confirmação antes de aceitar.

### ❓ A dose que preciso aplicar está fora da faixa da bula. Posso emitir?

Sim, mas com confirmação. Ao sair do campo Dose Aplicada, o sistema mostra *"Dose aplicada fora dos limites estabelecidos pela Configuração da Bula. Deseja confirmar?"*. Se o técnico autoriza por escrito, confirme. Caso contrário, o sistema volta a dose para o valor máximo da bula.

### ❓ Tem como emitir um receituário sem ter uma venda lançada?

Não. O receituário precisa estar associado a um movimento de venda com item formulado. Mesmo entrando direto na tela `142`, é obrigatório escolher o movimento no grupo `Movimento`.

### ❓ A tela exige um cliente, mas a venda foi para "Consumidor Padrão". E agora?

Cadastre o cliente real (CPF/CNPJ) em **Cadastro de Pessoas** (`5`) e refaça a venda com esse cliente. Receituário não aceita "Consumidor Padrão" — *"Não permitido selecionar Consumidor Padrão"* — pois a receita é nominal e precisa de cliente identificado por lei.

---

## Situações e ciclo de vida

### ❓ Quais situações um receituário pode ter?

Três:

- `CRIADO` — rascunho, pode editar, não consumiu ART.
- `EMITIDO` — oficializado, número de receita atribuído, saldo do ART consumido, relatório disponível para impressão.
- `CANCELADO` — receita estornada, saldo do ART devolvido.

A transição é sempre `CRIADO → EMITIDO → CANCELADO`. Não volta.

### ❓ Posso editar uma receita já emitida?

Não. *"Não é possível editar receituário Emitido ou Cancelado!"*. Para corrigir, você precisa cancelar a receita emitida (se a nota ainda não estiver autorizada) e emitir uma nova.

### ❓ Cancelei a receita por engano. Como recupero?

Não dá para reverter um `CANCELADO` para `EMITIDO`. Você precisa emitir uma nova receita do zero. O saldo do ART foi devolvido ao bloco, então é só refazer.

---

## Cancelamento

### ❓ Tentei excluir uma receita emitida e o sistema não deixou. Por quê?

Quando a nota fiscal do movimento já tem **Protocolo de Autorização** da SEFAZ, o sistema bloqueia o cancelamento: *"Não é possível alterar status desse Receituário! O movimento associado já possui nota fiscal com Protocolo de Autorização"*. A regra é fiscal — depois que a nota foi autorizada, a receita fica amarrada ao documento fiscal.

### ❓ Excluir uma receita CRIADA é a mesma coisa que cancelar uma EMITIDA?

Não.

- `Excluir` em uma receita **CRIADA** apaga o registro e a desassocia do movimento.
- `Excluir` em uma receita **EMITIDA** dispara o cancelamento: estorna saldo do ART, desassocia movimento e muda situação para `CANCELADO` (o registro fica, agora com `INATIVO=1`).

---

## ART/TRT

### ❓ Como funciona o controle do saldo do ART?

Cada bloco ART em **Gestão ART/TRT** (`136`) tem:

- Número Inicial e Número Final (faixa de receitas que aquele bloco permite)
- Saldo Atual (quantas receitas ainda podem ser emitidas)
- Data de Validade
- Quantidade de Aviso (limiar para alerta de saldo baixo)

Cada emissão consome 1 do saldo; cada cancelamento devolve 1.

### ❓ O sistema avisa quando o ART está acabando?

Sim. Depois de cada emissão, o sistema confere o saldo do ART contra a "Quantidade de Aviso" configurada e exibe um alerta se o saldo estiver baixo.

### ❓ A ART venceu. Posso continuar emitindo?

Não. O sistema bloqueia emissão com ART fora da validade. Renove o bloco em **Gestão ART/TRT** (`136`) ou cadastre um novo bloco.

---

## Impressão

### ❓ Como reimprimir uma receita?

Localize a receita na lista da tela `Receituário Agronômico` (`142`), abra e pressione **F9** (ou clique em `Gerar/Imprimir`). Como já está `EMITIDO`, o sistema só reabre o relatório da receita, sem consumir novo número do ART.

### ❓ Posso imprimir antes de emitir?

Não. *"O receituário precisa estar emitido para ser impresso!"*. Para imprimir, primeiro pressione **F9** para emitir.

### ❓ Os textos de EPI, restrições e advertências da impressão estão errados. Onde corrijo?

Esses textos vêm da configuração da bula. Acesse **Cadastro Config Bula Agronômico** (`141`), localize a combinação Formulado + Cultura + Diagnóstico e ajuste os textos. As próximas emissões saem com o texto atualizado.

---

## Erros e bloqueios

### ❓ *"Selecionei o Local mas o sistema apagou."*

UF do Local ≠ UF do registro do profissional. Solução: cadastre um endereço na UF correta (na aba `Endereços` do **Cadastro de Pessoas** — `5`) ou escolha um profissional com registro na UF do Local.

### ❓ *"Nenhum item do movimento é compatível com os itens do receituário."*

Os itens do movimento e os itens do receituário não compartilham o mesmo `Formulado`. Confira se você escolheu o item certo do movimento ou se o Formulado configurado no produto corresponde ao Formulado escolhido na aba `Item`.

### ❓ *"O ART/TRT preenchido não é da Empresa do Movimento selecionado. Ele será sobrescrito."*

O ART precisa pertencer à mesma empresa do movimento. O sistema tenta substituir pelo ART mais antigo ativo dessa empresa. Verifique em **Gestão ART/TRT** (`136`) se há ART disponível para a empresa correta.

### ❓ *"Não é possível emitir receituário sem item!"*

Você está tentando emitir um receituário que não tem nenhum item lançado. Volte para a aba `Item` e preencha Formulado, Cultura, Diagnóstico, Dose, Área e Quantidade.

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Usuários do Sol.NET
