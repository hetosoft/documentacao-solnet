---
title: "Guia Rápido: Lançamentos de RH - Sol.NET"
permalink: /RH/guia-rapido/
---
# 🚀 Guia Rápido: Lançamentos de RH

## ⚠️ Regra de ouro

**Todo lançamento de RH é vinculado a uma pessoa** classificada como `Funcionário` no `Cadastro de Pessoas`. Sem essa vinculação, o registro não fecha.

---

## 🧭 Telas (todas pela pesquisa `F1`)

| Tela | Código | Para quê |
|------|--------|----------|
| `Cadastro de Pessoas` | `5` | Cadastrar/editar funcionários (classificação `Funcionário`) |
| `Cadastro de Lançamento de RH` | `84` | Lançar os valores mensais |
| `Configuração RH` | `222` | Modelos recorrentes (salário base, encargos fixos) |
| `Holerite Excel` | `134` | Importar holerites de planilha |
| `Pessoa Rateio` | `133` | Modelos de rateio por pessoa |

> Para abrir qualquer tela: pressione **`F1`**, digite o **código** (ou parte do **nome**) e confirme.

---

## 📋 Checklist mensal

### 1. Cadastros (uma vez ou quando muda algo)

```
[ ] Funcionários ativos cadastrados em `Cadastro de Pessoas` (código 5)
[ ] Cada um marcado com classificação `Funcionário`
[ ] Centro de Custo configurado em cada cadastro
[ ] Funcionários desligados marcados como inativos
```

### 2. Recebimento dos valores

```
[ ] Planilha detalhada por funcionário recebida da contabilidade
[ ] Competência confirmada (mês/ano)
[ ] Eventos identificados (salário, encargos, descontos, benefícios)
```

### 3. Lançamento na tela 84

```
[ ] Abrir `Cadastro de Lançamento de RH` (F1 → 84)
[ ] Para cada funcionário:
    [ ] Aba Principal: definir Competência e selecionar Pessoas
    [ ] Inserir linhas (Valor, Plano de Contas, Centro de Custo, Tipo de Conta, Operação)
    [ ] Aba Rateio (se aplicável): distribuir o valor entre destinos
    [ ] Aba ContasPR - Manual (se aplicável): gerar o título financeiro
    [ ] Salvar
[ ] Repetir para todos os funcionários da planilha
```

### 4. Conferência

```
[ ] Filtrar lançamentos da competência pela aba Pesquisar da tela 84
[ ] Conferir que todos os funcionários aparecem
[ ] Conferir total geral contra a planilha da contabilidade
[ ] Validar distribuição no DRE
[ ] Conferir títulos criados em Contas a Pagar/Receber (quando aplicável)
```

---

## 🔄 Fluxo por funcionário

1. **`F1`** → digite `84` → abrir `Cadastro de Lançamento de RH`
2. Aba **Principal** → preencher `Competência` e `Pessoas`
3. Inserir uma linha por evento: `Valor`, `Plano de Contas`, `Centro de Custo`, `Tipo de Conta`, `Operação`
4. (Opcional) Aba **Rateio** → distribuir o valor entre centros de custo / planos de contas
5. (Opcional) Aba **ContasPR - Manual** → `Tipo de Documento`, `Portador`, `Vencimento` → botão `Criar`
6. **Salvar**
7. Selecionar próximo funcionário e repetir

---

## 📊 Exemplo rápido

Planilha da contabilidade — competência 03/2024:

```
João Silva
   Salário ............. R$ 5.000,00
   INSS patronal ....... R$ 1.000,00
   FGTS ................ R$   400,00

Maria Santos
   Salário ............. R$ 3.500,00
   Comissões ........... R$ 1.200,00
   INSS patronal ....... R$   940,00
   FGTS ................ R$   376,00
```

Lançamento de João Silva na tela `84`:

| Linha | Valor | Plano de Contas (D) | Plano de Contas (C) |
|-------|-------|---------------------|---------------------|
| Salário | 5.000,00 | 6.2.01 Salários | 2.1.2.01 Salários a Pagar |
| INSS patronal | 1.000,00 | 6.2.02 Encargos | 2.1.2.02 Encargos a Recolher |
| FGTS | 400,00 | 6.2.02 Encargos | 2.1.2.03 FGTS a Recolher |

Repetir para Maria Santos com os planos de contas de Vendas (6.1.x).

Para gerar o título do líquido a pagar no financeiro, use a aba `ContasPR - Manual` e clique em `Criar`.

---

## ⚠️ Problemas comuns

### Não consigo salvar o lançamento
Algum campo obrigatório está vazio (Competência, Pessoas, Valor, Plano de Contas) — confira a mensagem do sistema.

### Funcionário não aparece na pesquisa
Abra `Cadastro de Pessoas` (código `5`), confirme que o registro existe, está ativo e tem classificação `Funcionário`.

### Valor entrou no centro de custo errado no DRE
Ajuste o Centro de Custo no `Cadastro de Pessoas` (código `5`) para os próximos lançamentos. Para o lançamento já feito, edite e corrija o campo na linha — ou use rateio.

### Rateio não fecha
Confira o campo `Diferença` na aba `Rateio` da tela `84` — precisa estar em zero. Ajuste valores ou percentuais.

### Total diferente da contabilidade
Filtre os lançamentos da competência na aba `Pesquisar` da tela `84` e cruze funcionário a funcionário com a planilha.

### Contabilidade só passa valor total
Solicite o detalhamento por funcionário — sem isso o módulo não consegue alimentar o DRE por centro de custo nem gerar ContasPR individuais.

---

## 💡 Dicas

1. **Configure o Centro de Custo no cadastro da pessoa.** O lançamento herda automaticamente.
2. **Use `Configuração RH` (código `222`) para itens fixos.** Salário base e benefícios padrão entram como modelo recorrente.
3. **Lance por departamento.** Facilita conferir totais por centro de custo.
4. **Padronize descrições.** "INSS Patronal" sempre escrito do mesmo jeito ajuda em filtros e relatórios.
5. **Use a aba `Lançamento em Massa`** quando o mesmo evento se repete para vários funcionários (ex.: FGTS).
6. **Confira incrementalmente** — não espere terminar o mês inteiro para abrir o DRE.

---

## 🔗 Saiba mais

- **[Documentação completa](documentacao_folha_de_pagamento.md)** — campos, abas e integrações em detalhe
- **[Processo Mensal](processo_mensal.md)** — passo a passo do fechamento mensal
- **[FAQ](faq.md)** — perguntas frequentes

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 2.0
**🎯 Público-alvo**: Equipe de suporte e usuários do módulo RH

*Lembre-se: o atalho `F1` abre a pesquisa universal — qualquer tela do Sol.NET é acessada digitando seu **código** ou parte do **nome**.*
