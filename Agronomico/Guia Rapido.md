# 📄 Guia Rápido - Receituário Agronômico - Sol.NET

## 🎯 Visão Geral

Referência objetiva para emitir, cancelar e administrar receituários agronômicos no Sol.NET. Para o passo a passo completo, consulte a **[Documentação Receituário Agronômico](Documentacao%20Receituario%20Agronomico.md)**.

---

## ⌨️ Atalhos Essenciais

| Atalho | Onde | O que faz |
|--------|------|-----------|
| **F9** | Tela de Movimentação | Abre o Receituário Agronômico já preenchido com cliente e itens da venda |
| **F4** | Listagens em geral | Novo registro |
| **F5** | Formulários | Salvar |
| **F6** | Movimentação | Finalizar processo |
| **Enter** | Campo "Cliente" / "Profissional" / "ART" | Abre lupa de pesquisa |

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

## 🚀 Fluxo Diário — Emissão Integrada à Venda

```
1. Lance a Movimentação normalmente
2. Adicione os itens (produtos com formulado vinculado vão exigir receita)
3. Pressione F9
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

---

## 📝 Fluxo — Emissão Avulsa

```
Menu > Movimentos > Agronômico > Receituário Agronômico → Novo
1. Selecione o Cliente
2. Selecione o Local de Aplicação
3. Profissional + ART
4. Adicione cada item: Formulado, Cultura, Diagnóstico, Dose, Área
5. Observações
6. Salve → Imprima
```

Use quando não há venda associada (recomendação técnica em campo, reemissão administrativa, etc.).

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

| Quero encontrar… | Onde |
|------------------|------|
| Receita emitida hoje | Movimentos > Agronômico > Receituário (filtro de data) |
| ARTs com saldo baixo | Cadastros > Gestão de ART/TRT — coluna "Saldo Atual" |
| Locais de um cliente | Cadastros > Locais de Aplicação (filtro por cliente) |
| Bula de um produto | Cadastros > Configuração de Bula (filtro por formulado) |
| Receitas de um cliente | Receituário Agronômico (filtro por cliente + período) |

> 💡 As pesquisas usam `WITH NOLOCK` para não travar a base. Resultados podem aparecer com pequena defasagem em vendas concorrentes.

---

## 🚨 Problemas Comuns

### "Não há ART disponível para a empresa atual"
**Causa:** nenhuma ART ativa, com saldo, vinculada à empresa logada.
**Solução:** cadastrar nova ART em `Cadastros > Gestão de ART/TRT`, com **Empresa = empresa atual**, **Situação = Ativa** e **Data de Validade** futura.

### "Combinação Produto × Cultura × Alvo não permitida"
**Causa:** não há entrada em Configuração de Bula para essa tríade.
**Solução:** verificar o rótulo do produto. Se houver bula registrada no MAPA, cadastre em `Cadastros > Configuração de Bula`. Se não houver, **não emita** — a aplicação é off-label.

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
**Solução:** completar o cadastro em `Cadastros > Profissionais`.

### Item da movimentação não dispara F9
**Causa:** o produto comercial não está vinculado a um Formulado.
**Solução:** abrir o `Cadastro de Produtos` → aba "Receituário Agronômico" → vincular ao formulado correspondente.

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
| Pressiona F9 | Cliente da Movimentação + Empresa logada |
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

- **Detalhes completos** → [Documentação Receituário Agronômico](Documentacao%20Receituario%20Agronomico.md)
- **Dúvidas específicas** → [FAQ](FAQ.md)
- **Voltar ao módulo** → [Índice do Módulo Agronômico](README.md)
- **Portal Sol.NET** → [Documentação Geral](../README.md)

---

**📅 Última atualização**: Abril de 2026
**📦 Versão**: 1.0
**🎯 Público-alvo**: Vendedores de revenda agropecuária, balconistas, responsáveis técnicos
