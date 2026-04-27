# 🚀 Guia Rápido - Instalação Self Checkout Sol.NET

## ⚡ Checklist de Instalação Rápida

### 📦 1. Downloads
- [ ] [DLLs Skia](https://github.com/user-attachments/files/25111774/DLLs.skia.zip) - extrair
- [ ] [Fontes Poppins](https://github.com/user-attachments/files/25111757/Poppins.zip) - extrair
- [ ] [Manual Balança R7](https://github.com/user-attachments/files/25111795/Manual_do_Usurio_R7_Rev1.pdf) - consulta

### 🔧 2. Instalação de Componentes

**DLLs Skia:**
- Copiar DLLs para o diretório de instalação do Self Checkout
- Colocar no mesmo diretório do executável

**Fontes Poppins:**
- Botão direito nos arquivos `.ttf` → "Instalar para todos os usuários"
- OU copiar para `C:\Windows\Fonts\`

### ⚖️ 3. Configuração da Balança Toledo

| Item | Configuração |
|------|--------------|
| **6º Parâmetro** | **TRN 2** ⚠️ CRÍTICO |
| **Baud Rate** | **2400** |
| **Porta** | Anotar número (ex: COM3) |
| **Paridade** | Nenhuma (N) |
| **Bits Dados** | 8 |
| **Bits Parada** | 1 |

### 🖥️ 4. Configuração Inicial - Servidor

**Primeiro acesso:** Configuração do Servidor (aparece automaticamente)

- [ ] Configurar conexão com servidor
- [ ] Testar conexão
- [ ] Confirmar que a carga de dados foi realizada

### 🏢 5. Configuração Padrão - Sol.NET

**Acesso:** Cadastro de Empresas no Sol.NET

| Item | Configuração |
|------|--------------|
| **Empresa** | Selecionar empresa/filial |
| **Tipo Movimento** | Definir tipo para vendas |
| **Série Fiscal** | Configurar série de documentos |

### 🔧 6. Configuração Dispositivos - Self Checkout

**Acesso:** Menu Configurações → Dispositivos no Self Checkout

**Dispositivos Essenciais:**

| Dispositivo | Configurações |
|-------------|---------------|
| **Balança** | Porta COM, Protocolo TRN 2, Baud 2400 |
| **Leitor Barras** | Conforme modelo |
| **Impressora Fiscal** | Porta e modelo |
| **Pinpad** | Drivers, se necessário |

---

## 🧪 Testes Rápidos

### ✅ Checklist Mínimo

1. **Interface**
   - [ ] Abre sem erros
   - [ ] Fonte Poppins aplicada
   - [ ] Gráficos nítidos

2. **Balança**
   - [ ] Teste: Configuração Dispositivos → Balança → Testar
   - [ ] Peso aparece em tempo real
   - [ ] Peso estável (não oscila muito)

3. **Fluxo Básico**
   - [ ] Ler código de barras
   - [ ] Pesar produto
   - [ ] Finalizar venda
   - [ ] Verificar no Sol.NET (venda registrada)

---

## 🔥 Problemas Comuns - Soluções Imediatas

### ❌ Erro: "SkiaSharp.dll não encontrada"
**Solução:**
- Verificar se DLLs estão no diretório do executável Self Checkout
- Executar como Administrador

### ❌ Fontes não aparecem
**Solução:**
```cmd
# Verificar instalação
dir C:\Windows\Fonts\Poppins*

# Reinstalar para todos os usuários (como Admin)
```

### ❌ Balança não comunica
**Solução:**
1. **Verificar porta COM:**
   - Gerenciador de Dispositivos → Portas (COM e LPT)
   - Anotar número da porta

2. **Verificar configuração balança:**
   - 6º parâmetro = TRN 2 ✓
   - Baud Rate = 2400 ✓

3. **Testar no Self Checkout:**
   - Configuração Dispositivos → Balança
   - Porta COM = [número correto]
   - Protocolo = TRN 2, Baud = 2400
   - Clicar em "Testar"

### ❌ Peso não aparece
**Checklist:**
- [ ] Cabo conectado firmemente
- [ ] Porta COM correta configurada
- [ ] Balança configurada (TRN 2, Baud 2400)
- [ ] Driver USB-Serial instalado (se usar adaptador)

---

## 📋 Checklist Pré-Produção

### Antes de Liberar o Terminal

- [ ] **Hardware testado**
  - [ ] Balança pesando corretamente
  - [ ] Leitor de código de barras funcionando
  - [ ] Impressora fiscal configurada
  - [ ] Terminal de pagamento (se houver)

- [ ] **Software validado**
  - [ ] Interface carrega sem erros
  - [ ] Fontes e gráficos corretos
  - [ ] Comunicação com balança estável

- [ ] **Integração confirmada**
  - [ ] Vendas registradas no Sol.NET
  - [ ] Estoque sendo atualizado
  - [ ] Cupom fiscal sendo emitido
  - [ ] Financeiro integrado

- [ ] **Documentação**
  - [ ] Porta COM anotada
  - [ ] Configurações específicas documentadas
  - [ ] Equipe treinada

---

**📅 Última atualização**: Fevereiro de 2026  
**📦 Versão**: 1.0  
**🎯 Público-alvo**: Técnicos de suporte  
**⏱️ Tempo médio de instalação**: 30-45 minutos
