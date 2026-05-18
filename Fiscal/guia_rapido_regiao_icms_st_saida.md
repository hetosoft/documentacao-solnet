# ⚡ Guia Rápido — Região ICMS ST Saída

## 🎯 Para que serve

Cartão de referência para configurar e diagnosticar regras de ICMS-ST. Para a explicação completa, abra a [Documentação da Região ICMS ST Saída](documentacao_regiao_icms_st_saida.md).

A tela `Região ICMS ST Saída` (`94`) armazena **percentuais de ICMS-ST** (Base, MVA, Alíquota) que o Sol.NET aplica em cada item conforme o contexto da operação combina com os filtros das linhas de detalhe.

---

## 🚪 Como abrir

Pela pesquisa universal (`F1`), digite `Região ICMS ST Saída` ou o código `94`.

---

## 📋 Checklist — cadastrar uma Região ICMS-ST

1. ☐ Definir o **Tipo**: `PRODUTO` (regra vai depender do item) ou `PESSOA` (regra vai depender do destinatário).
2. ☐ Preencher **Descrição** (até 80 caracteres, obrigatório). Pode repetir entre Tipos diferentes.
3. ☐ Em `Configurações`, clicar **Inserir** para criar a primeira linha de detalhe.
4. ☐ Definir os filtros: `Nº Lojas`, `Sigla Estados`, `CNAE - Fiscal`, `Indicador IE`, `Atividade Comercial`, `Regime Tributário`. Vazio ou `-1` = qualquer.
5. ☐ Escolher o **Cálculo** (`Normal` ou `Industria MT`).
6. ☐ Marcar o **Tipo** (Saída ou Entrada) e a localização (`Dentro do Estado`, `Fora do Estado`, `Exterior`).
7. ☐ Informar **B.C. ICMS ST** (% da base após redução), **MVA** (% de agregação) e **ICMS ST Aliq.** (% da alíquota).
8. ☐ Se a MVA já está mantida no NCM dos itens, marcar **Usar MVA NCM** para o sistema buscar lá.
9. ☐ Clicar **Atualizar** para gravar a linha de detalhe.
10. ☐ Repetir os passos 3–9 para cada contexto que precisa de regra própria.
11. ☐ Salvar o cadastro completo no botão `Salvar` da barra inferior.
12. ☐ Vincular a Região no cadastro de **Produtos** (Tipo `PRODUTO`) ou no cadastro de **Pessoas** (Tipo `PESSOA`).

---

## 🧮 Anatomia da tela

| Bloco | O que define |
|---|---|
| **Cabeçalho** | Identidade da regra: `Tipo` (PRODUTO/PESSOA) + `Descrição`. |
| **Configurações** (sub-CRUD com Inserir / Atualizar / Deletar / Cancelar) | Linhas com filtros de contexto + percentuais de ICMS-ST + modo de cálculo. |

---

## ✏️ Operações no detalhe

| Botão | Quando usar |
|---|---|
| **Inserir** | Iniciar uma nova linha de detalhe. Foca em `Nº Lojas` e habilita a edição. |
| **Atualizar** | Gravar as alterações da linha em edição. Roda as validações antes de aceitar. |
| **Deletar** | Excluir a linha atualmente selecionada (pede confirmação). |
| **Cancelar** | Descartar as alterações da linha em edição e voltar ao estado anterior (pede confirmação). |

---

## 🧷 Atalhos de listas

| Campo | Formato | Exemplo |
|---|---|---|
| Nº Lojas | Códigos de filial separados por `/` | `/1/2/` |
| Sigla Estados | UFs separadas por `/` | `/BA/SP/MG/` |
| CNAE - Fiscal | Selecionado por busca (duplo clique ou tecla de busca) | — |

O Sol.NET adiciona automaticamente as barras `/` no início e no fim ao sair do campo.

---

## 🚨 Erros mais comuns

| Mensagem / sintoma | Diagnóstico rápido |
|---|---|
| *"Não permitido, Existe Produto(s) com essa Região!"* | A Região (Tipo `PRODUTO`) está vinculada a produtos. Abra o cadastro dos produtos, troque a Região e tente excluir novamente. |
| *"Existe cadastro em edição"* ao trocar de seção | Há uma linha de detalhe sendo inserida sem confirmação. Clique `Atualizar` para gravar ou `Cancelar` para descartar. |
| ICMS-ST do movimento não bate com o esperado | Conferir, na ordem: (1) Tipo da Região vinculada (PRODUTO × PESSOA), (2) qual linha do detalhe casa com o contexto do movimento, (3) se o modo é `Normal` ou `Industria MT`, (4) se `Usar MVA NCM` está marcado e se o NCM tem MVA. |
| Linha gravada mas não aplica em movimento de fora do estado | Confirme o radio `Selecione`: precisa estar `Fora do Estado` para operações interestaduais. |
| MVA da linha ignorada no cálculo | O `Usar MVA NCM` está marcado — o sistema buscou a MVA no NCM do item. |

---

## 📎 Telas relacionadas

- `Cadastro de NCM` (`21`) — fonte da MVA quando `Usar MVA NCM` está marcado.
- `Cadastro de Produtos` (`32`) — onde a Região do tipo `PRODUTO` é vinculada.
- `Cadastro de Pessoas` (`5`) — onde a Região do tipo `PESSOA` é vinculada.
- `Cadastro de CNAE` (`156`) — origem da busca do campo `CNAE - Fiscal`.
- `Região ICMS Saída` (`93`) — regra paralela para ICMS normal (Natureza de Operação por contexto).

---

**Última atualização**: Maio de 2026
**Versão**: 1.0
**Público-alvo**: Equipe de Suporte / Usuários do Sol.NET
