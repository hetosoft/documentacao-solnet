# 📄 Guia Rápido - Receituário Agronômico - Sol.NET

## 🎯 Visão Geral

Checklist objetivo para emitir um receituário agronômico no Sol.NET. Use este guia durante o atendimento; para regras detalhadas, consulte a [documentação completa](documentacao_receituario_agronomico.md).

---

## ✅ Antes de começar — confira se está tudo no lugar

- [ ] Profissional cadastrado em **Profissionais Externos** (código `135`)
- [ ] Bloco ART/TRT ativo, com saldo e dentro da validade em **Gestão ART/TRT** (código `136`)
- [ ] Cultura existente em **Cadastro Cultura Agronômica** (código `138`)
- [ ] Diagnóstico (alvo) existente em **Cadastro Diagnóstico Agronômico** (código `139`)
- [ ] Produto comercial vinculado a um **Formulado** (código `140`)
- [ ] **Config Bula** (código `141`) cadastrada para a combinação Formulado + Cultura + Diagnóstico
- [ ] Cliente real (não "Consumidor Padrão") com **endereço** cadastrado na aba `Endereços` do Cadastro de Pessoas (código `5`), com UF compatível com a UF do registro do profissional — esse endereço será o Local de Aplicação

---

## ⚡ Caminho rápido — emissão a partir da venda

1. Abra **Vendas** (código `202` na pesquisa F1) e lance o movimento com o item formulado.
2. Dispare a emissão do receituário a partir do movimento — a tela `Receituário Agronômico` (código `142`) abre com os campos do movimento já preenchidos.
3. Selecione o **ART** ativo do profissional (na aba `Receituário`).
4. Selecione o **Local de Aplicação** do cliente.
5. Vá para a aba `Item`. Escolha **Cultura** e **Diagnóstico**. O sistema preenche Dose, Calda e Dias de Carência da bula.
6. Confirme **Quantidade Total**. O sistema calcula **Área Tratada** automaticamente.
7. Confirme a receita — situação fica `CRIADO`.
8. Pressione **F9** (ou clique em `Gerar/Imprimir`). Receita passa para `EMITIDO` e o relatório da receita abre para impressão.

---

## ⚡ Caminho rápido — emissão direta na tela 142

1. Abra **Receituário Agronômico** (código `142` na pesquisa F1).
2. Clique em `Novo`.
3. Na aba `Receituário`, escolha o **Movimento** já lançado no grupo `Movimento`. Os dados do movimento, cliente e formulado entram automaticamente.
4. Selecione **ART** e **Local de Aplicação**.
5. Aba `Item` — preencha **Cultura**, **Diagnóstico** e ajuste Quantidade/Dose se necessário.
6. Confirme (situação `CRIADO`).
7. **F9** para emitir e imprimir.

---

## ⚡ Reimprimir uma receita já emitida

1. Abra **Receituário Agronômico** (código `142`).
2. Localize a receita no grid (pesquise por número, profissional, cliente, etc.).
3. Abra a receita e pressione **F9**. Como já está `EMITIDO`, o sistema só reabre o relatório da receita.

---

## ⚡ Cancelar uma receita emitida

1. Abra **Receituário Agronômico** (código `142`).
2. Localize a receita e clique em `Excluir`.
3. Confirme. O sistema estorna o saldo do ART e muda a situação para `CANCELADO`.

> Só funciona enquanto a **nota fiscal do movimento ainda não tem Protocolo de Autorização**. Depois disso, o cancelamento é bloqueado.

---

## 🚨 Erros mais comuns e o que conferir

| Mensagem | O que fazer |
|----------|-------------|
| *"Não é possível emitir receituário sem movimento associado!"* | Selecione um movimento de venda no grupo `Movimento`. |
| *"Para emitir o receituário é necessário preencher todos os dados do item!"* | Vá na aba `Item` e preencha Formulado, Cultura, Diagnóstico, Dose, Área e Quantidade. |
| *"O Local selecionado não pertence ao estado do Registro do Profissional."* | UF do Local ≠ UF do registro do profissional. Cadastre Local na UF correta ou troque o profissional. |
| *"O ART/TRT selecionado não é da Empresa do Movimento"* | Use um ART da empresa do movimento (confira em `Gestão ART/TRT` — código `136`). |
| *"Não permitido selecionar Consumidor Padrão"* | Cadastre/use o cliente real. |
| *"Dose aplicada fora dos limites estabelecidos pela Configuração da Bula. Deseja confirmar?"* | Se o técnico autorizou, confirme. Senão, ajuste a dose para a faixa da bula. |
| *"O receituário precisa estar emitido para ser impresso!"* | Emita primeiro (F9). Não dá pra imprimir rascunho. |

---

## 🔍 Atalho de pesquisa do grid (aba inicial da tela 142)

Na lista inicial você pode buscar por:

- Nº Receita
- Observações
- Nº ART Mãe
- Série ART
- Descrição / Endereço / Cidade / UF do Local de Aplicação
- Nome do Profissional
- Registro do Conselho
- Nome / CPF do Cliente

Combine com a condição (`Contém`, `Inicia Com`, `Vazio`, `Não Vazio`) para refinar.

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Usuários do Sol.NET
