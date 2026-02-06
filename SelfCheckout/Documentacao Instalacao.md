# 🛒 Instalação do Self Checkout - Sol.NET

## 🎯 Visão Geral

O **Self Checkout** é uma aplicação que faz parte do ecossistema Sol.NET ERP, permitindo aos clientes realizarem autoatendimento em operações de checkout, proporcionando maior agilidade e autonomia no processo de compra. Este documento fornece instruções completas para instalação e configuração do sistema.

**Importante:** O Self Checkout não é o Sol.NET, mas uma aplicação separada que se integra com o sistema principal.

### Principais Características:
- ✅ **Interface intuitiva** para autoatendimento
- ✅ **Integração com balança** para produtos pesáveis
- ✅ **Suporte a múltiplos métodos de pagamento**
- ✅ **Sincronização em tempo real** com o sistema Sol.NET
- ✅ **Interface otimizada** com fontes Poppins
- ✅ **Renderização gráfica** de alta qualidade com Skia

---

## 📋 Pré-requisitos do Sistema

### Hardware Mínimo Recomendado:
- **Processador**: Intel Core i3 ou superior (ou equivalente AMD)
- **Memória RAM**: 4 GB (recomendado 8 GB)
- **Espaço em Disco**: 500 MB livres
- **Tela**: Monitor touchscreen (recomendado) ou mouse/teclado
- **Balança**: Modelo compatível Toledo Prix R7 ou similar

### Software Necessário:
- **Sistema Operacional**: Windows 10 ou superior (64 bits)
- **.NET Framework**: Versão 4.7.2 ou superior
- **Sol.NET ERP**: Sistema principal instalado e configurado
- **Drivers**: Driver da balança Toledo (ou modelo compatível)

### Periféricos:
- ✅ Balança digital Toledo Prix R7 (configurada)
- ✅ Leitor de código de barras (recomendado)
- ✅ Impressora térmica para cupom fiscal (conforme legislação)
- ✅ Terminal de pagamento (se houver integração)

---

## 🔧 Processo de Instalação

### Passo 1: Instalação das DLLs Skia

As bibliotecas Skia são essenciais para renderização gráfica de alta qualidade da interface do Self Checkout.

#### 📦 Obtenção das DLLs:
1. **Baixe o pacote**: [DLLs skia.zip](https://github.com/user-attachments/files/25111774/DLLs.skia.zip)
2. **Extraia o conteúdo** do arquivo ZIP

#### 📂 Instalação:
1. **Localize o diretório de instalação** do Self Checkout
   - Conforme definido durante a instalação do sistema
   - Exemplo de estrutura: `[Local de instalação do sistema]\`

2. **Copie as DLLs** para o diretório do aplicativo:
   - Coloque as DLLs no mesmo diretório do executável do Self Checkout
   - Arquivos necessários: `libSkiaSharp.dll`, `SkiaSharp.dll` e outras DLLs do pacote

3. **Verifique as permissões**:
   - As DLLs devem ter permissão de leitura e execução
   - Se necessário, execute como Administrador

#### ✅ Validação:
- Execute o aplicativo Self Checkout temporariamente
- Verifique se não há erros relacionados a "Skia" ou renderização
- A interface deve carregar normalmente com elementos gráficos nítidos

---

### Passo 2: Instalação das Fontes Poppins

A fonte Poppins é utilizada para garantir uma interface moderna e de fácil leitura no Self Checkout.

#### 📦 Obtenção das Fontes:
1. **Baixe o pacote**: [Poppins.zip](https://github.com/user-attachments/files/25111757/Poppins.zip)
2. **Extraia o conteúdo** do arquivo ZIP
3. Você terá múltiplos arquivos `.ttf` ou `.otf` com diferentes pesos da fonte

#### 📂 Instalação no Windows:

**Método 1 - Instalação por arquivo (recomendado):**
1. **Selecione todos os arquivos de fonte** extraídos
2. **Clique com o botão direito** em um dos arquivos
3. **Selecione "Instalar para todos os usuários"** (requer privilégios de administrador)
4. Aguarde a conclusão da instalação

**Método 2 - Instalação manual:**
1. **Abra o Painel de Controle** → Aparência e Personalização → Fontes
2. **Arraste os arquivos de fonte** para a janela de Fontes
3. Ou clique em "Arquivo" → "Instalar Nova Fonte" e navegue até os arquivos

**Método 3 - Via linha de comando (para instalação em múltiplos dispositivos):**
```cmd
rem Execute como Administrador
cd C:\caminho\para\fontes\extraidas
for %f in (*.ttf *.otf) do (
    copy "%f" "C:\Windows\Fonts\"
    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Fonts" /v "Poppins (%~nf)" /t REG_SZ /d "%f" /f
)
```

#### ✅ Validação:
1. **Abra um editor de texto** (Word, Notepad, etc.)
2. **Procure por "Poppins"** na lista de fontes
3. Confirme que os diferentes pesos estão disponíveis:
   - Poppins Thin
   - Poppins Light
   - Poppins Regular
   - Poppins Medium
   - Poppins SemiBold
   - Poppins Bold
   - Poppins ExtraBold
   - Poppins Black
4. **Reinicie o aplicativo Self Checkout** se já estiver em execução

---

### Passo 3: Configuração da Balança Toledo Prix R7

A balança é essencial para pesagem de produtos no Self Checkout.

#### 📖 Documentação de Referência:
- **Manual completo**: [Manual do Usuário R7 Rev1.pdf](https://github.com/user-attachments/files/25111795/Manual_do_Usurio_R7_Rev1.pdf)
- **Foco**: Tópico 5 - Configurações

#### ⚙️ Configuração Necessária:

**Acesso ao Menu de Configurações:**
1. **Ligue a balança** Toledo Prix R7
2. **Acesse o menu de configurações** (consulte manual específico do modelo)
3. **Navegue até**: Configurações → Comunicação

**Parâmetro Crítico - 6º Parâmetro:**

| Parâmetro | Configuração | Valor |
|-----------|--------------|-------|
| **6º Parâmetro** | **Tipo de Comunicação** | **TRN 2** |

#### 📝 Configuração Passo a Passo:

1. **Entre no modo de configuração** da balança:
   - Pressione e segure a tecla de configuração
   - Ou use a sequência de teclas conforme manual (geralmente `MENU` → `Senha` → `Config`)

2. **Navegue até o 6º parâmetro**:
   - Use as setas ou teclas numéricas para navegar
   - Procure por "Tipo de Comunicação" ou "Protocolo"

3. **Selecione "TRN 2"**:
   - Este é o protocolo de comunicação compatível com o Self Checkout
   - Opções disponíveis podem incluir: TRN 1, TRN 2, Toledo, etc.
   - **IMPORTANTE**: Certifique-se de selecionar exatamente "TRN 2"

4. **Configure parâmetros adicionais**:
   - **Porta de Comunicação**: Verifique qual porta serial (COM1, COM2, etc.) está sendo usada
   - **Baud Rate**: 2400 bps
   - **Paridade**: Nenhuma (N)
   - **Bits de Dados**: 8
   - **Bits de Parada**: 1

5. **Salve as configurações**:
   - Pressione a tecla de confirmação (geralmente `Enter` ou `OK`)
   - A balança pode reiniciar automaticamente

#### 🔌 Conexão Física:

1. **Identifique a porta serial** no computador Self Checkout
   - Se não houver porta serial nativa, use um adaptador USB-Serial
   - Anote o número da porta COM (ex: COM3)

2. **Conecte o cabo serial** da balança ao computador
   - Use cabo serial DB9 ou conforme especificação
   - Certifique-se de que a conexão está firme

3. **Instale drivers** (se necessário):
   - Para adaptadores USB-Serial, instale os drivers do fabricante
   - Verifique no Gerenciador de Dispositivos se a porta é reconhecida

#### ✅ Validação:

**Teste de Comunicação:**
1. **Coloque um peso** sobre a balança
2. **Verifique se o display** mostra o peso corretamente
3. **No Self Checkout**:
   - Acesse a Configuração de Dispositivos → Balança → Testar
   - Verifique se o peso é exibido corretamente no sistema
   - Teste múltiplas pesagens para confirmar estabilidade

**Resolução de Problemas:**
- Se o peso não aparecer: Verifique porta COM configurada na Configuração de Dispositivos do Self Checkout
- Se peso incorreto: Calibre a balança conforme manual
- Se comunicação instável: Verifique cabos e configuração do Baud Rate (deve ser 2400)

---

### Passo 4: Configuração Inicial do Self Checkout

Após instalar os componentes físicos e de software, configure o Self Checkout.

#### 🚀 Primeiro Acesso - Configuração do Servidor

Ao abrir o Self Checkout pela primeira vez (ou quando não configurado), você será direcionado para a tela de **Configuração do Servidor**.

**Esta é a primeira tela que o suporte encontrará ao iniciar um Self Checkout não configurado.**

1. **Configure a conexão com o banco de dados**:
   - Servidor/Host do banco de dados
   - Nome do banco de dados
   - Credenciais de acesso
   - Porta de conexão

2. **Teste a conexão** antes de prosseguir

3. **Salve as configurações**

**Importante:** O Self Checkout só pode ser iniciado após o banco de dados receber a "carga" de dados do Sol.NET.

---

### Passo 5: Configuração no Sol.NET - Cadastro de Empresas

As **configurações padrão do Self Checkout** são definidas no Sol.NET através do **Cadastro de Empresas**.

#### 🖥️ Acesso:

1. **Abra o Sol.NET ERP**
2. **Navegue até**: Cadastro de Empresas
3. Localize a seção de configurações do Self Checkout

#### ⚙️ Configurações Padrão:

No Cadastro de Empresas, configure:
- **Empresa Padrão**: Selecione a empresa/filial vinculada
- **Tipo de Movimento**: Configure o tipo de movimento para vendas do Self Checkout
- **Série de Documentos**: Defina a série fiscal para cupons/notas
- **Métodos de Pagamento Padrão**: Defina quais métodos estarão disponíveis
- **Regras de Negócio**: Configure validações e permissões específicas

#### 💾 Salvar Configurações:
1. **Revise todas as configurações**
2. **Salve** (geralmente F5)
3. As configurações serão aplicadas ao Self Checkout

---

### Passo 6: Configuração de Dispositivos no Self Checkout

Após a configuração inicial do servidor e das configurações padrão no Sol.NET, é necessário configurar os **dispositivos periféricos** no próprio Self Checkout.

**Os dispositivos não são configurados no Sol.NET**, pois cada terminal pode ter dispositivos diferentes.

#### 🖥️ Acesso à Configuração de Dispositivos:

1. **Abra o Self Checkout**
2. **Acesse**: Menu de Configurações → Dispositivos
   - Ou use o atalho/opção de configuração disponível

#### ⚙️ Dispositivos a Configurar:

**Balança:**
- **Porta COM**: Selecione a porta onde a balança está conectada (ex: COM3)
- **Protocolo**: TRN 2 (conforme configurado na balança)
- **Baud Rate**: 2400
- **Timeout**: 5000 ms (padrão)
- **Teste**: Use a função de teste para validar a comunicação

**Leitor de Código de Barras:**
- Configure o leitor conforme o modelo
- Teste a leitura de códigos

**Impressora Fiscal:**
- Configure impressora para cupom fiscal
- Defina porta e modelo

**Terminal de Pagamento (TEF):**
- Configure se houver integração TEF
- Defina modelo e parâmetros de comunicação

**Outras Configurações:**
- **Tema**: Selecione o tema visual (claro/escuro)
- **Tamanho da Fonte**: Médio (ajuste conforme tamanho da tela)
- **Modo Tela Cheia**: Ativado (recomendado para terminais dedicados)
- **Tempo de Inatividade**: 120 segundos (retorna à tela inicial)
- **Busca por Código de Barras**: Ativada
- **Exibir Imagens**: Ativado (melhora experiência do cliente)
- **Produtos Pesáveis**: Configurar prefixo (ex: produtos que começam com "2")

#### 💾 Salvar Configurações:
1. **Revise todas as configurações de dispositivos**
2. **Salve as configurações**
3. **Teste cada dispositivo** individualmente antes de usar em produção

---

## 🧪 Testes e Verificação

Antes de colocar o Self Checkout em produção, realize testes completos:

### ✅ Checklist de Testes:

**Teste 1: Interface Gráfica**
- [ ] Interface carrega corretamente
- [ ] Fontes Poppins exibidas corretamente
- [ ] Elementos gráficos nítidos (Skia funcionando)
- [ ] Tela cheia funcionando
- [ ] Transições suaves entre telas

**Teste 2: Balança**
- [ ] Peso exibido corretamente em tempo real
- [ ] Peso estabiliza adequadamente
- [ ] Tara funciona corretamente
- [ ] Produtos pesáveis identificados pelo prefixo

**Teste 3: Leitor de Código de Barras**
- [ ] Leitura de códigos EAN-13
- [ ] Leitura de códigos de produtos pesáveis
- [ ] Som de confirmação de leitura
- [ ] Produtos adicionados corretamente ao carrinho

**Teste 4: Fluxo de Venda Completo**
- [ ] Adicionar produtos por código de barras
- [ ] Adicionar produtos pesáveis
- [ ] Editar quantidade de produtos
- [ ] Remover produtos do carrinho
- [ ] Visualizar total corretamente
- [ ] Aplicar descontos (se habilitado)

**Teste 5: Pagamento**
- [ ] Pagamento em dinheiro (calcular troco)
- [ ] Pagamento com cartão (integração TEF)
- [ ] Pagamento com PIX (se configurado)
- [ ] Múltiplas formas de pagamento

**Teste 6: Emissão de Documentos**
- [ ] Cupom fiscal impresso corretamente
- [ ] Informações fiscais corretas
- [ ] Numeração sequencial funcionando

**Teste 7: Integração com Sol.NET**
- [ ] Venda registrada no sistema principal
- [ ] Estoque atualizado corretamente
- [ ] Financeiro integrado (contas a receber)
- [ ] Histórico de vendas disponível

---

## ❓ Solução de Problemas Comuns

### 🔧 Problema: DLLs Skia não encontradas

**Sintomas:**
- Erro ao iniciar: "SkiaSharp.dll não encontrada"
- Interface não carrega

**Solução:**
1. Verifique se as DLLs estão no diretório correto do aplicativo
2. Certifique-se de usar a versão 64 bits das DLLs (para Windows 64 bits)
3. Execute o aplicativo como Administrador
4. Reinstale as DLLs do pacote original

---

### 🔧 Problema: Fontes Poppins não aparecem

**Sintomas:**
- Interface usa fonte padrão do sistema
- Layout desconfigurado

**Solução:**
1. Verifique se as fontes foram instaladas para "todos os usuários"
2. Reinicie o computador após instalar as fontes
3. Confirme instalação: Painel de Controle → Fontes → procure "Poppins"
4. Se necessário, reinstale as fontes com privilégios de administrador

---

### 🔧 Problema: Balança não comunica

**Sintomas:**
- Peso não aparece no sistema
- Erro de timeout ao pesar produtos

**Solução:**
1. **Verifique a porta COM**:
   - Gerenciador de Dispositivos → Portas (COM e LPT)
   - Anote o número correto da porta
   - Configure a mesma porta no Self Checkout

2. **Verifique configuração da balança**:
   - 6º parâmetro deve estar em "TRN 2"
   - Baud Rate deve ser 2400

3. **Verifique configuração no Self Checkout**:
   - Acesse Configuração de Dispositivos → Balança
   - Confirme porta COM, protocolo TRN 2 e Baud Rate 2400

3. **Teste o cabo**:
   - Verifique se o cabo serial está bem conectado
   - Teste com outro cabo se disponível

4. **Drivers do adaptador USB-Serial**:
   - Se usar adaptador, reinstale os drivers
   - Alguns adaptadores podem não ser compatíveis

---

### 🔧 Problema: Self Checkout não inicia

**Sintomas:**
- Aplicativo não abre
- Erro ao carregar configurações

**Solução:**
1. **Verifique .NET Framework**:
   - Versão 4.7.2 ou superior instalada
   - Atualize se necessário

2. **Verifique conexão com banco de dados**:
   - Banco de dados deve estar acessível
   - Verifique se a "carga" de dados foi realizada
   - Rede/conexão com banco de dados funcionando

3. **Arquivos de configuração**:
   - Verifique se arquivo `app.config` ou `settings.json` existe
   - Restaure de backup se corrompido

4. **Permissões**:
   - Execute como Administrador
   - Verifique permissões de pasta

---

### 🔧 Problema: Produtos pesáveis não funcionam

**Sintomas:**
- Produto pesável não é reconhecido
- Peso não é capturado automaticamente

**Solução:**
1. **Verifique prefixo de produtos pesáveis**:
   - Configuração de Dispositivos no Self Checkout → Produtos → Prefixo (geralmente "2")
   - Código de barras deve começar com o prefixo configurado

2. **Teste a balança**:
   - Use a função de teste na Configuração de Dispositivos → Balança
   - Confirme que peso está sendo lido corretamente

3. **Cadastro de produtos**:
   - No Sol.NET, produto deve estar marcado como "Pesável"
   - Unidade de medida deve ser KG ou G

---

## 📚 Informações Adicionais

### 🔗 Links Úteis:
- **Manual da Balança Toledo**: Consulte documentação específica do modelo
- **Suporte Hetosoft**: Entre em contato para suporte técnico especializado
- **Documentação Sol.NET**: Consulte outros módulos do sistema

### 📞 Suporte Técnico:
- Para dúvidas ou problemas não cobertos neste guia
- Mantenha em mãos: número de série do produto, versão do Sol.NET
- Descreva o problema com detalhes e prints se possível

### 🔄 Atualizações:
- Mantenha o Self Checkout sempre atualizado
- Atualizações podem incluir novos recursos e correções
- Verifique compatibilidade antes de atualizar

---

## 📋 Checklist Final de Instalação

Use este checklist para garantir que todos os passos foram concluídos:

- [ ] **Pré-requisitos verificados**
  - [ ] Hardware adequado
  - [ ] Sistema operacional compatível
  - [ ] Sol.NET ERP instalado e funcionando

- [ ] **DLLs Skia instaladas**
  - [ ] Download do pacote realizado
  - [ ] DLLs copiadas para diretório correto
  - [ ] Teste de renderização bem-sucedido

- [ ] **Fontes Poppins instaladas**
  - [ ] Download do pacote realizado
  - [ ] Fontes instaladas para todos os usuários
  - [ ] Verificação de disponibilidade concluída

- [ ] **Balança configurada**
  - [ ] 6º parâmetro configurado como "TRN 2"
  - [ ] Baud Rate configurado como 2400
  - [ ] Conexão física estabelecida
  - [ ] Teste de comunicação bem-sucedido

- [ ] **Configuração Inicial do Self Checkout**
  - [ ] Configuração do Servidor realizada (primeiro acesso)
  - [ ] Conexão com banco de dados testada
  - [ ] Carga de dados do BD confirmada

- [ ] **Configurações Padrão no Sol.NET**
  - [ ] Cadastro de Empresas configurado
  - [ ] Tipo de movimento definido
  - [ ] Série fiscal configurada
  - [ ] Métodos de pagamento padrão definidos

- [ ] **Configuração de Dispositivos no Self Checkout**
  - [ ] Balança configurada (porta COM, protocolo TRN 2, Baud Rate 2400)
  - [ ] Leitor de código de barras configurado
  - [ ] Impressora fiscal configurada
  - [ ] TEF configurado (se aplicável)
  - [ ] Prefixo de produtos pesáveis definido

- [ ] **Testes realizados**
  - [ ] Teste completo de interface
  - [ ] Teste de balança e produtos pesáveis
  - [ ] Teste de fluxo de venda completo
  - [ ] Teste de integração com Sol.NET

- [ ] **Documentação**
  - [ ] Anotadas configurações específicas do terminal
  - [ ] Equipe de suporte treinada
  - [ ] Procedimentos de backup definidos

---

**📅 Última atualização**: Fevereiro de 2026  
**📦 Versão**: 1.0  
**🎯 Público-alvo**: Equipe de suporte e técnicos de implantação  
**👨‍💻 Elaborado por**: Equipe Hetosoft - Documentação Sol.NET
