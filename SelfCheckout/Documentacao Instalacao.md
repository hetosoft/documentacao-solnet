# 🛒 Instalação do Self Checkout - Sol.NET

## 🎯 Visão Geral

O **Self Checkout** é uma aplicação que faz parte do ecossistema Sol.NET ERP, permitindo aos clientes realizarem autoatendimento em operações de checkout, proporcionando maior agilidade e autonomia no processo de compra. Este documento fornece instruções completas para instalação e configuração do sistema.

**Importante:** O Self Checkout não é o Sol.NET, mas uma aplicação separada que se integra com o sistema principal.

### Principais Características:
- ✅ **Interface intuitiva** para autoatendimento
- ✅ **Integração com balança** para produtos pesáveis
- ✅ **Suporte a múltiplos métodos de pagamento**
- ✅ **Interface otimizada** com fontes Poppins
- ✅ **Renderização gráfica** de alta qualidade com Skia

---

## 🔧 Processo de Instalação

### Passo 1: Configuração no Sol.NET - Cadastro de Empresas

As **configurações padrão do Self Checkout** são definidas no Sol.NET através do **Cadastro de Empresas**.

#### 🖥️ Acesso:

1. **Abra o Sol.NET ERP**
2. **Navegue até**: Cadastro de Empresas
3. Seleciona a Empresa para a qual o Self Checkout será configurado
4. Edite o registro
5. Localize a seção de configurações do PDV

#### ⚙️ Configurações Padrão:
Na Aba de Configurações Gerais, defina:
- **Tipo de Movimento**: Configure o tipo de movimento para vendas do Self Checkout
- Na sessão de PDVs cadastrados, insira um novo registro
- Configure o registro como o padrão de configuração de PDV
- **Tipo Sistema**: Em tipo sistema, selecione `Self Checkout`

#### 💾 Salvar Configurações:
1. **Revise todas as configurações**
2. **Salve** (F5)
3. **Código Autenticação**: Acesse o cadastro da empresa novamente e localize o PDV recém-cadastrado. Copie o código de autenticação gerado para usar posteriormente.

---

### Passo 2: Configuração Inicial do Self Checkout

#### 🚀 Primeiro Acesso - Configuração do Servidor

1. **Instalação do sistema**
- Utilize o `Sol.NET_PDV_Instalador` para obter a pasta padrão do Sol.NET_PDV.
- Copie os executaveis `SolNET_SyncPDV.exe`, `SolNET_PDV_Inicializar.exe`, `SolNET_SyncAuxPDV.exe` e `SolNET_SelfCheckout.exe` para pasta raiz da instalçao.
---

### Passo 3: Configurações de ambiente
#### Passo 3.1: Instalação das DLLs Skia

As bibliotecas Skia são essenciais para renderização gráfica de alta qualidade da interface do Self Checkout.

#### 📦 Obtenção das DLLs:
1. **Copiar DLL**: Na pasta de instalação do Sol.NET, navegue para `Geral\Drivers\Diversos\Skia` e encontre o arquivo `skia.zip`. Caso o arquivo não esteja disponível, você pode [baixá-lo aqui](https://github.com/user-attachments/files/25111774/DLLs.skia.zip)   
2. **Extraia o conteúdo** do arquivo ZIP

#### 📂 Instalação:
1. **Localize o diretório de instalação** do Self Checkout
   - Conforme definido durante a instalação do sistema
   - Exemplo de estrutura: `[Local de instalação do sistema]\`

2. **Copie as DLLs** para o diretório do aplicativo:
   - Verifique a arquitetura do executável do Self Checkout (32 ou 64-bits) e copie a dll da pasta equivalente
   - Arquivos necessários: `sk4d.dll`

#### ✅ Validação:
- Execute o aplicativo Self Checkout temporariamente
- Se ao abrir a aplicação, for acusado `runtime error`, a arquitetura da dll pode estar invertida, ou o arquivo pode estar corrompido. Tente copiar e colar novamente.

#### Passo 3.2: Instalação das Fontes Poppins

A fonte Poppins é utilizada para garantir uma interface moderna e de fácil leitura no Self Checkout.

#### 📦 Obtenção das Fontes:
1. **Baixe o pacote**: [Poppins.zip](https://github.com/user-attachments/files/25111757/Poppins.zip)
2. **Extraia o conteúdo** do arquivo ZIP
3. Você terá múltiplos arquivos `.ttf` ou `.otf` com diferentes pesos da fonte

#### 📂 Instalação no Windows:

**Método 1 - Instalação por arquivo (recomendado):**
1. **Selecione todos os arquivos de fonte** extraídos
2. **Clique com o botão direito** em um dos arquivos
3. **Selecione "Instalar"**
4. Aguarde a conclusão da instalação

**Método 2 - Instalação manual:**
1. **Abra o Painel de Controle** → Aparência e Personalização → Fontes
2. **Arraste os arquivos de fonte** para a janela de Fontes
3. Ou clique em "Arquivo" → "Instalar Nova Fonte" e navegue até os arquivos

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

#### Passo 3.3 Configuração do ambiente de pagamento

💳 Realize os passos de configuração de acordo com o Modelo TEF (CliSitef, Destaxa)

#### Passo 3.4: Configuração da Balança R7

A balança é essencial para pesagem de produtos no Self Checkout.

#### 📖 Documentação de Referência:
- **Manual completo**: [Manual do Usuário R7 Rev1.pdf](https://github.com/user-attachments/files/25111795/Manual_do_Usurio_R7_Rev1.pdf)
- **Foco**: Tópico 5 - Configurações

#### ⚙️ Configuração Necessária:

**Acesso ao Menu de Configurações:**
1. **Ligue a balança** R7
2. **Acesse o menu de configurações** (consulte manual específico do modelo)
3. **Navegue até**: Configurações → Comunicação

**Parâmetro Crítico - 6º Parâmetro:**

| Parâmetro | Configuração | Valor |
|-----------|--------------|-------|
| **6º Parâmetro** | **Tipo de Comunicação** | **TRN 2** |

#### 📝 Configuração Passo a Passo:

1. **Entre no modo de configuração** da balança.

2. **Navegue até o 6º parâmetro**:
   - Use as setas ou teclas numéricas para navegar
   - Procure por "Tipo de Comunicação" 

3. **Selecione "TRN 2"**:
   - Este é o protocolo de comunicação compatível com o Self Checkout
   - Opções disponíveis podem incluir: TRN 1, TRN 2, TRN3, etc.
   - Certifique-se de selecionar exatamente "TRN 2"

4. **Configure parâmetros adicionais**:
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

### Passo 4: Configurações no Self Checkout

Ao abrir o Self Checkout pela primeira vez (ou quando não configurado), você será direcionado para a tela de **Configuração do Servidor**.

**Esta é a primeira tela que o suporte encontrará ao iniciar um Self Checkout não configurado.**

#### ⚙️ Configuração Necessária:
**Configure a conexão com o servidor**:
   - Servidor/Host do serviço Apache
   - Porta de conexão
   - Código Autenticação (Código copiado do registro do PDV em Empresas)
   - Clique em `Vincular Self Checkout`

#### ✅ Validação:
Faça uma consulta no Cadastro de empresas, localize o registro de PDV criado para o Self Checkout, confira o campo `Identificador Dispositivo`.
O preenchimento deste campo indica sucesso no vínculo. Isso impede que um mesmo PDV seja instalado em mais de um computador simultaneamente (novo método padrão para todos os PDVs)

**Importante:** Aguarde o Sincronizador PDV receber a primeira carga de dados para prosseguir.

---


### Passo 5: Configuração de Dispositivos no Self Checkout

Após a configuração inicial do servidor e das configurações padrão no Sol.NET, é necessário configurar os **dispositivos periféricos** no próprio Self Checkout.

**Os dispositivos não são configurados no Sol.NET**, pois cada terminal pode ter dispositivos diferentes.

#### 🖥️ Acesso à Configuração de Dispositivos:

1. **Abra o Self Checkout**
2. **Acesse**: Menu de Configurações . Ícone de engrenagem no canto superior direito.

#### ⚙️ Dispositivos a Configurar:

> 📝 Nota: Antes de inicar as configurações, é necessário saber que a aplicação não consegue verificar se o dispositivo na porta COM realmente é uma balança, leitor ou qualquer tipo de dispositivo serial, apenas confirmar se é possível anexar um processo à porta COM selecionada.

**🏁 Leitor de Código de Barras:**
- **Porta COM**: Defina a porta
- **Teste**: Uma conexão com a porta COM será solicitada e o ícone indicará se a conexão foi bem sucedida ou não. Caso a conexão tenha sido bem sucedida, confirme se a porta conectada se refere ao leitor fazendo uma leitura de código de barras e conferindo o campo `Código Lido`

**⚖️ Balança:**
- **Porta COM**: Defina a porta
- **Teste**: Uma conexão com a porta COM será solicitada e o ícone indicará se a conexão foi bem sucedida e se a solicitação de leitura de peso retornou um valor maior ou igual a zero. Para confirmar o status da balança, o campo `Peso Lido` pode ser usado para conferencia.

**💳Pinpad:**
- **Porta COM**: Defina a porta
- **Teste**: Não é possível validar a comunicação, clique em definir para salvar a porta

**🚦Sinaleiro:**
- **Porta COM**: Defina a porta
- **Teste**: Uma conexão com a porta COM será solicitada e o ícone indicará se a conexão foi bem sucedida ou não. Caso a conexão tenha sido bem sucedida, a aplicação tentará enviar o sinal das cores vermelho, amarelo e verde. Confira visualmente se o sinaleiro piscará alternando entre as cores.

**🖨️ Impressora:**
- Escolha a impressora da lista de dispositivos lidos do Windows

**Importante**: 
- Caso um dispositivo seja conectado à uma porta COM indevida, a porta COM só ficará disponível para ser utilizada por outro dispositivo quando for desconectada. Caso seja necessário reatribuir as portas, utilize a opção `Rescan portas` para que o sistema desconecte todos os dispositivos e faça a leitura novamente das portas disponíveis. 
- Há 2 tipos de conexões COM: A simulada, onde o dispositivo se conecta ao computador via porta USB com uma COM virtual gerada, ou a conexão via cabo RS-232, que seria a COM "real". Caso o Rescan não consiga mostrar uma porta COM "real", isso significa que a porta está ocupada com algum processo no qual o sistema não consegue desconectar. Nesse caso, a única solução para acessar novamente a porta, é desconectar e reconectar o cabo (o que as vezes pode ser difícil devido a grande quantidade de conexões que tem no self checkout), ou reiniciar o computador.

---

## 🧪 Testes e Verificação

Antes de colocar o Self Checkout em produção, realize testes completos:

### ✅ Checklist de Testes:

**Teste 1: Interface Gráfica**
- [ ] Interface carrega corretamente
- [ ] Fontes Poppins exibidas corretamente
- [ ] Elementos gráficos nítidos
- [ ] Tela cheia funcionando

**Teste 2: Balança**
- [ ] Peso exibido corretamente em tempo real
- [ ] Peso estabiliza adequadamente
- [ ] Tara funciona corretamente
- [ ] Produtos pesáveis identificados pelo prefixo

**Teste 3: Leitor de Código de Barras**
- [ ] Leitura de códigos EAN-13
- [ ] Leitura de códigos de produtos pesáveis
- [ ] Som de confirmação de leitura

**Teste 4: Pagamento**
- [ ] Pagamento com cartão (integração TEF)
- [ ] Pagamento com PIX (se configurado)

**Teste 5: Emissão de Documentos**
- [ ] Cupom fiscal impresso corretamente

---

## ❓ Solução de Problemas Comuns

### 🔧 Problema: DLLs Skia não encontradas

**Sintomas:**
- Erro ao iniciar: "runtime error"
- Interface não carrega

**Solução:**
1. Verifique se as DLLs estão no diretório correto do aplicativo
2. Certifique-se de usar a versão 32 ou 64 bits das DLLs corretamente
3. Reinstale as DLLs do pacote original

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
   - Confirme porta COM

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
1. **Verifique conexão com banco de dados**:
   - Banco de dados deve estar acessível
   - Verifique se a "carga" de dados foi realizada
   - Rede/conexão com servidor funcionando

---

### 🔧 Problema: Produtos pesáveis não funcionam

**Sintomas:**
- Produto pesável não é reconhecido
- Peso não é capturado automaticamente

**Solução:**
1. **Teste a balança**:
   - Use a função de teste na Configuração de Dispositivos → Balança
   - Confirme que peso está sendo lido corretamente

---

## 📚 Informações Adicionais

### 🔗 Links Úteis:
- **Manual da Balança Toledo**: Consulte documentação específica do modelo
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

- [ ] **Configurações Padrão no Sol.NET**
  - [ ] Cadastro de Empresas configurado
  - [ ] Tipo de movimento definido
  - [ ] Série fiscal configurada
  - [ ] Métodos de pagamento padrão definidos

- [ ] **Configuração Inicial do Self Checkout**
  - [ ] Configuração do Servidor realizada (primeiro acesso)
  - [ ] Conexão com banco de dados testada
  - [ ] Carga de dados do BD confirmada

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

---

**📅 Última atualização**: Fevereiro de 2026  
**📦 Versão**: 1.0  
**🎯 Público-alvo**: Equipe de suporte e técnicos de implantação  
**👨‍💻 Elaborado por**: Equipe Hetosoft - Documentação Sol.NET
