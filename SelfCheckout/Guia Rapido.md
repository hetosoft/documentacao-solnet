# 🚀 Guia Rápido - Instalação Self Checkout Sol.NET

## ⚡ Checklist de Instalação Rápida

### 📦 1. Downloads
- [ ] [DLLs Skia](https://github.com/user-attachments/files/25111774/DLLs.skia.zip) - extrair
- [ ] [Fontes Poppins](https://github.com/user-attachments/files/25111757/Poppins.zip) - extrair
- [ ] [Manual Balança R7](https://github.com/user-attachments/files/25111795/Manual_do_Usurio_R7_Rev1.pdf) - consulta

### 🔧 2. Instalação de Componentes

**DLLs Skia:**
```cmd
# Copiar DLLs para o diretório do Self Checkout
C:\Program Files\Hetosoft\Sol.NET\SelfCheckout\
```

**Fontes Poppins:**
- Botão direito nos arquivos `.ttf` → "Instalar para todos os usuários"
- OU copiar para `C:\Windows\Fonts\`

### ⚖️ 3. Configuração da Balança Toledo

| Item | Configuração |
|------|--------------|
| **6º Parâmetro** | **TRN 2** ⚠️ CRÍTICO |
| **Baud Rate** | 9600 |
| **Porta** | Anotar número (ex: COM3) |
| **Paridade** | Nenhuma (N) |
| **Bits Dados** | 8 |
| **Bits Parada** | 1 |

### 🖥️ 4. Configuração Sol.NET

**Acesso:** Menu → Configurações → Módulos → Self Checkout

**Abas Obrigatórias:**

| Aba | Configurações Essenciais |
|-----|-------------------------|
| **Geral** | Nome terminal, Empresa, Tipo movimento |
| **Balança** | Porta COM, Protocolo TRN 2, Baud 9600 |
| **Interface** | Tela cheia ✓, Tema, Fonte |
| **Pagamento** | Métodos disponíveis, TEF (se houver) |
| **Produtos** | Código barras ✓, Prefixo pesáveis |

---

## 🧪 Testes Rápidos

### ✅ Checklist Mínimo

1. **Interface**
   - [ ] Abre sem erros
   - [ ] Fonte Poppins aplicada
   - [ ] Gráficos nítidos

2. **Balança**
   - [ ] Teste: Menu → Config → Testar Balança
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
```cmd
# Verificar se DLLs estão no diretório correto
dir "C:\Program Files\Hetosoft\Sol.NET\SelfCheckout\*.dll"

# Executar como Administrador
```

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

3. **Testar no Sol.NET:**
   - Config → Balança → Porta = [número correto]
   - Clicar em "Testar Conexão"

### ❌ Peso não aparece
**Checklist:**
- [ ] Cabo conectado firmemente
- [ ] Porta COM correta no Self Checkout
- [ ] Balança configurada (TRN 2)
- [ ] Driver USB-Serial instalado (se usar adaptador)

### ❌ Produtos pesáveis não funcionam
**Verificar:**
1. Prefixo configurado (geralmente "2")
2. Produto marcado como "Pesável" no Sol.NET
3. Unidade de medida = KG ou G
4. Código de barras inicia com prefixo

---

## 🎯 Configuração em Múltiplos Terminais

### Script Batch - Instalação Automática Fontes

```batch
@echo off
echo Instalando fontes Poppins para todos os usuarios...

cd /d "C:\Temp\Poppins"

for %%f in (*.ttf *.otf) do (
    echo Instalando %%f...
    copy "%%f" "C:\Windows\Fonts\" /Y
    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Fonts" /v "Poppins (%%~nf)" /t REG_SZ /d "%%f" /f
)

echo.
echo Instalacao concluida!
pause
```

### PowerShell - Verificação de Componentes

```powershell
# Verificar DLLs Skia
$dllPath = "C:\Program Files\Hetosoft\Sol.NET\SelfCheckout"
if (Test-Path "$dllPath\SkiaSharp.dll") {
    Write-Host "✓ SkiaSharp.dll encontrada" -ForegroundColor Green
} else {
    Write-Host "✗ SkiaSharp.dll NAO encontrada" -ForegroundColor Red
}

# Verificar Fontes Poppins
$fonts = Get-ChildItem "C:\Windows\Fonts\Poppins*"
if ($fonts) {
    Write-Host "✓ Fontes Poppins instaladas: $($fonts.Count)" -ForegroundColor Green
} else {
    Write-Host "✗ Fontes Poppins NAO encontradas" -ForegroundColor Red
}

# Listar portas COM disponíveis
Write-Host "`nPortas COM disponiveis:"
Get-WmiObject Win32_SerialPort | Select-Object DeviceID, Description
```

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
  - [ ] Procedimentos de backup definidos

---

## ⌨️ Atalhos Úteis (Sol.NET)

| Atalho | Função |
|--------|--------|
| **F5** | Salvar configurações |
| **ESC** | Cancelar/Voltar |
| **Alt + F4** | Fechar aplicativo |

---

## 📞 Suporte Rápido

### Informações Necessárias para Suporte

Antes de contatar, tenha em mãos:
- ✅ Versão do Sol.NET
- ✅ Versão do Windows
- ✅ Número da porta COM usada
- ✅ Modelo da balança
- ✅ Mensagem de erro completa (print)
- ✅ Log de erro (se disponível)

### Links Úteis
- **[Documentação Completa](Documentacao Instalacao.md)** - guia detalhado
- **[FAQ](FAQ.md)** - perguntas frequentes
- **[Índice](README.md)** - visão geral

---

## 💡 Dicas de Produtividade

### Para Instaladores

1. **Crie um pendrive** com todos os arquivos necessários:
   - DLLs Skia
   - Fontes Poppins
   - Scripts de instalação
   - Documentação offline

2. **Use checklist impresso** para cada instalação

3. **Documente configurações** específicas de cada terminal

4. **Tire fotos** das configurações da balança

5. **Teste TUDO** antes de liberar para produção

### Para Suporte

1. **Sempre verifique primeiro**:
   - Porta COM configurada
   - 6º parâmetro da balança = TRN 2
   - DLLs e fontes instaladas

2. **Mantenha backup** dos arquivos de configuração

3. **Documente problemas** novos para atualizar FAQ

---

**📅 Última atualização**: Fevereiro de 2026  
**📦 Versão**: 1.0  
**🎯 Público-alvo**: Técnicos de suporte  
**⏱️ Tempo médio de instalação**: 30-45 minutos
