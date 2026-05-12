# ⚡ Guia Rápido — API Externa - Sol.NET

Cartão de referência do suporte para gerar uma credencial da **API Externa** durante o atendimento. Para o passo a passo completo, veja a [documentação principal](documentacao_api_externa.md).

---

## ✅ Antes de abrir a tela — colete do parceiro

- [ ] Nome do parceiro e nome da pessoa responsável
- [ ] E-mail e telefone
- [ ] **IPs públicos** que vão consumir a API (todos, se houver mais de um)
- [ ] **Contextos** combinados (Produtos, Estoque, Pessoas, Movimentos, etc.)
- [ ] **Verbos** combinados (`GET` para consulta — padrão atual)
- [ ] **Limite de requisições/minuto** combinado (folga sobre o pico esperado)
- [ ] Há **prazo de validade**? (POC, contrato com data)
- [ ] Tem ciência da **URL da API**? (não fica nesta tela — peça ao time técnico do cliente)

---

## 🛠️ Na tela `Cadastro de Acessos WebAPI Externa` (`150`)

1. `F1` → digite `150` → abre a tela.
2. Clique em **Novo**. O sistema preenche **Client ID** e **Secret Key** automaticamente.
3. Preencha **Nome do Cliente**, **E-mail**, **Contato**, **Telefone**, **Descrição**.
4. Preencha **IP Whitelist** com os IPs do parceiro.
5. Preencha **Limite de Requisições/minuto**.
6. Em **Permissões**, para cada contexto combinado:
   - Clique em **Novo**.
   - Escolha o **Contexto**.
   - Marque os **verbos** combinados (normalmente só `GET`).
   - Preencha **Data de expiração** se for acesso temporário.
   - Salve a permissão.
7. **Salve** a credencial.

---

## 📤 Entrega ao parceiro

- **Client ID** — pode ir por qualquer canal (informação pública)
- **Secret Key** — só foi mostrada uma vez, no salvamento; enviada por e-mail OU disponível na área de transferência (se o e-mail falhou). Encaminhe pelo canal mais seguro disponível.
- **URL da API** — solicite ao time técnico do cliente Sol.NET
- **Resumo dos contextos liberados** — assim o parceiro sabe o que pode chamar

---

## 🚨 Pontos críticos

- ⚠️ **A Secret Key não pode ser recuperada depois.** Se perder, é preciso criar uma nova credencial. Não existe função de "mostrar Secret Key de novo".
- 📡 **A URL é local de cada cliente Sol.NET.** Não há URL única da Hetosoft. Sempre obtenha do time técnico responsável pela instalação.
- 🔒 **IP Whitelist vazia = qualquer IP.** Em produção, sempre preencha.
- ⏱️ **Limite de requisições vazio = sem proteção.** Defina um valor coerente com o uso.

---

## 🔄 Operações comuns durante o atendimento

| Quero... | Faço... |
|---|---|
| Bloquear acesso de um parceiro temporariamente | Marco **Inativo** em cada permissão dele |
| Liberar de volta após bloqueio | Desmarco **Inativo** nas permissões |
| Adicionar um novo contexto a um parceiro existente | Abro a credencial, **Novo** em Permissões, escolho contexto, marco verbos, salvo |
| Remover permissão sem perder histórico | Marco **Inativo** (em vez de excluir) |
| Trocar Secret Key (parceiro perdeu) | Crio **nova credencial** com mesma configuração; descarto a antiga (inativar ou excluir) |
| Mudar IPs autorizados do parceiro | Abro a credencial, atualizo **IP Whitelist**, salvo |
| Aumentar/diminuir limite por minuto | Abro a credencial, ajusto **Limite de Requisições/minuto**, salvo |

---

**📅 Última atualização**: Maio de 2026
**📦 Versão**: 1.0
**🎯 Público-alvo**: Equipe de suporte Hetosoft
