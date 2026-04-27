# 📄 Guia Rápido - Receituário Agronômico - Sol.NET

## 🎯 Visão Geral

Referência objetiva para emitir, cancelar e administrar receituários agronômicos no Sol.NET. Para o passo a passo completo, consulte a **[Documentação Receituário Agronômico](documentacao_receituario_agronomico.md)**.

---

## ⌨️ Atalho Essencial

| Atalho | Onde | O que faz |
|--------|------|-----------|
| **F1** | Em qualquer tela do Sol.NET | Abre a **pesquisa de telas** — digite o código identificador (`ID_FORMULARIO`) ou parte do nome para ir direto à função desejada |

> 💡 Outras ações do dia a dia (novo registro, salvar, abrir lupa de pesquisa em campos, finalizar processo da Movimentação) são feitas pelos **botões correspondentes em cada tela**. Os atalhos variam por tela e versão; consulte os títulos/dicas dos próprios botões no Sol.NET.

> 💡 **Não existe atalho dedicado para abrir o Receituário a partir da Movimentação.** Em movimentos fiscais com itens que exigem receita, o Sol.NET dispara a tela **automaticamente** durante o fluxo da venda. Para a emissão **avulsa**, abra a tela `Receituário Agronômico` (código **142**) pela pesquisa (F1).

---

## 📋 Checklist de Configuração Inicial

Faça uma vez antes de emitir a primeira receita:

```
[ ] Profissionais cadastrados (com CPF e nº de CREA/CFTA + UF)
[ ] ART/TRT de cada profissional, vinculada à empresa
[ ] Culturas atendidas
[ ] Diagnósticos (alvos) recorrentes
[ ] Tipos de Embalagem
[ ] Embalagens dos produtos
[ ] Formulados (com nº de registro MAPA)
[ ] Configuração de Bula (Produto × Cultura × Alvo + dose mín./máx.)
[ ] Locais de Aplicação dos clientes ativos
[ ] Quantidade de Aviso definida em cada ART (alerta de saldo baixo)
[ ] Texto de devolução de embalagens revisado
[ ] Layout do receituário no ReportBuilder validado (3 vias)
```

---

## 🚀 Fluxo Diário — Emissão Integrada à Venda (Gatilho Automático)

```
1. Lance a Movimentação fiscal normalmente
2. Adicione os itens (produtos com formulado vinculado vão exigir receita)
3. Avance no fluxo  → Sol.NET abre o Receituário automaticamente
4. Confirme: Profissional + ART (sugeridos)
5. Selecione o Local de Aplicação do cliente
6. Para cada item:
     - Cultura
     - Diagnóstico (alvo)
     - Modalidade de Aplicação
     - Dose Aplicada (L/ha, kg/ha…)
     - Área Tratada (ha)  → Quantidade Total calcula sozinha
7. Salve  → sistema valida e gera nº da receita
8. Imprima as vias
```

> ⚠️ O gatilho automático **só ocorre em movimentações do tipo fiscal**. Em movimentos não fiscais, use o fluxo avulso abaixo.

---

## 📝 Fluxo — Emissão Avulsa

```
F1 → Receituário Agronômico → Novo
1. (Opcional para cadastrar) Vincule a movimentação
2. Selecione o Cliente
3. Selecione o Local de Aplicação
4. Profissional + ART
5. Adicione cada item: Formulado, Cultura, Diagnóstico, Dose, Área
6. Observações
7. Salve  → cadastro feito
8. Para EMITIR/IMPRIMIR  → vincule a movimentação (obrigatório) → Imprima
```

Use quando não há movimentação fiscal associada no momento (recomendação técnica em campo, reemissão administrativa, etc.).

> ⚠️ **Regra do vínculo com movimentação:**
> - Para **lançar** o receituário avulso, vincular movimentação **NÃO é obrigatório**.
> - Para **emitir/imprimir**, o vínculo a uma movimentação **É obrigatório** — sem ele o sistema bloqueia a impressão definitiva.

---

## ↩️ Cancelar uma Receita Emitida

```
Abrir o receituário → Cancelar Receituário → Confirmar
```

**O que acontece:**
- Situação muda para **Cancelada**
- Saldo da ART **volta automaticamente**
- Número da receita **fica reservado** (não é reaproveitado)
- Movimentação é **desvinculada** da receita

---

## 🔍 Pesquisas Úteis

> 💡 Em todos os casos abaixo, abra a tela pela **pesquisa universal (F1)** digitando o nome ou o código identificador da tela.

| Quero encontrar… | Tela | Código (`ID_FORMULARIO`) |
|------------------|------|:---:|
| Receita emitida hoje | `Receituário Agronômico` (filtro de data) | **142** |
| ARTs com saldo baixo | `Gestão ART/TRT` — coluna "Saldo Atual" | **136** |
| Profissional habilitado | `Profissionais Externos` | **135** |
| Cultura cadastrada | `Cadastro Cultura Agronômica` | **138** |
| Diagnóstico cadastrado | `Cadastro Diagnóstico Agronômico` | **139** |
| Bula de um produto | `Cadastro Config Bula Agronômico` (filtro por formulado) | **141** |
| Formulado / produto MAPA | `Cadastro Formulado Agronômico` | **140** |
| Receitas de um cliente | `Receituário Agronômico` (filtro por cliente + período) | **142** |

> 💡 As pesquisas usam `WITH NOLOCK` para não travar a base. Resultados podem aparecer com pequena defasagem em vendas concorrentes.

---

## 🚨 Problemas Comuns

### "Não há ART disponível para a empresa atual"
**Causa:** nenhuma ART ativa, com saldo, vinculada à empresa logada.
**Solução:** abrir `Gestão ART/TRT` (F1, código **136**) e cadastrar nova ART, com **Empresa = empresa atual**, **Situação = Ativa** e **Data de Validade** futura.

### "Combinação Produto × Cultura × Alvo não permitida"
**Causa:** não há entrada em Configuração de Bula para essa tríade.
**Solução:** verificar o rótulo do produto. Se houver bula registrada no MAPA, cadastre na tela `Cadastro Config Bula Agronômico` (F1, código **141**). Se não houver, **não emita** — a aplicação é off-label.

### "Dosagem fora do permitido"
**Causa:** dose digitada está abaixo de `Dose Mínima` ou acima de `Dose Máxima`.
**Solução:** ajustar a dose. Se a bula está desatualizada, corrigir o cadastro com base no rótulo oficial atual.

### "ART vencida"
**Causa:** `Data de Validade` da ART selecionada já passou.
**Solução:** renovar a ART junto ao conselho, cadastrar nova ART e inativar a anterior.

### "Local de aplicação não pertence ao cliente"
**Causa:** o local selecionado está vinculado a outro cliente.
**Solução:** abrir o cadastro do local e ajustar o cliente, ou cadastrar um novo local para o cliente correto.

### "Cliente inválido para receituário"
**Causa:** cliente é o "consumidor padrão" do balcão, ou tem caracteres especiais inválidos.
**Solução:** identificar o produtor real (CPF/CNPJ) e usá-lo na venda.

### "Profissional sem registro válido"
**Causa:** cadastro do profissional sem CREA/CFTA + UF.
**Solução:** abrir a tela `Profissionais Externos` (F1, código **135**) e completar o cadastro.

### Movimentação fiscal não abre o Receituário automaticamente
**Causa:** o(s) produto(s) comercial(is) não estão vinculados a um Formulado, ou a movimentação não é de tipo fiscal.
**Solução:** abrir o `Cadastro de Produtos` (F1) → aba "Receituário Agronômico" → vincular ao formulado correspondente. Confirmar também que a movimentação foi lançada como movimento fiscal.

---

## 🧠 Dicas de Produtividade

- **Uma ART por empresa, por profissional**: simplifica a sugestão automática.
- **Quantidade de Aviso = 10% do bloco**: tempo razoável para renovar.
- **Padronize nomes de locais**: "Fazenda XYZ - T01" em vez de "Faz. XYZ T1".
- **Cadastre culturas e alvos antes da safra**: evita parar para cadastrar no balcão.
- **Atualize bulas a cada renovação MAPA**: dose e carência podem mudar.
- **Cadastre bulas antes de comprar o estoque**: assim o produto chega pronto para vender.

---

## 🧩 Vínculos com Outros Módulos

| Quando você… | … o sistema usa |
|--------------|-----------------|
| Lança um item de venda | Cadastro de Produtos → Formulado vinculado |
| Avança em movimentação fiscal com item que exige receita | Cliente da Movimentação + Empresa logada → abre o Receituário automaticamente |
| Seleciona ART | Filtra por **empresa** + **profissional** + **saldo > 0** + **dentro da validade** |
| Seleciona Local | Filtra por **cliente** da venda |
| Salva o item | Verifica **bula** (Formulado × Cultura × Diagnóstico) |
| Salva a receita | Decrementa **saldo da ART** e gera **nº sequencial** |
| Cancela a receita | Estorna saldo + desvincula movimentação |

---

## 📊 Relatórios

Acesso pelo botão **Relatórios** dentro da tela do Receituário (habilitado após salvar):

- **Receituário oficial** — modelo legal para impressão (3 vias)
- **Receituários por período**
- **Receituários por cliente**
- **Receituários por profissional**
- **Controle de ARTs** (saldo, validade, status)

---

## ✅ Boas Práticas

1. **Imprima na hora da venda** — o cliente sai com o documento.
2. **Arquive cancelamentos** — algumas defesas estaduais auditam.
3. **Treine atendentes sobre off-label** — bloqueio do sistema é a última camada, não a única.
4. **Revise mensalmente as ARTs** — saldo, validade, vínculo com empresa.
5. **Atualize bulas** — assim que receber notificação do fabricante ou do MAPA.

---

## 🔗 Próximos Passos

- **Detalhes completos** → [Documentação Receituário Agronômico](documentacao_receituario_agronomico.md)
- **Dúvidas específicas** → [FAQ](faq.md)
- **Voltar ao módulo** → [Índice do Módulo Agronômico](README.md)
- **Portal Sol.NET** → [Documentação Geral](../README.md)

---

**📅 Última atualização**: Abril de 2026
**📦 Versão**: 1.0
**🎯 Público-alvo**: Vendedores de revenda agropecuária, balconistas, responsáveis técnicos
