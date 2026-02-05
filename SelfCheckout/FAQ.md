# ❓ FAQ - Self Checkout Sol.NET

## 📋 Perguntas Frequentes

Este documento responde às dúvidas mais comuns sobre instalação, configuração e operação do Self Checkout Sol.NET.

---

## 🔧 Instalação e Configuração

### P: Quais são os pré-requisitos mínimos para instalar o Self Checkout?

**R:** 
- **Hardware**: Processador Intel Core i3 ou superior, 4 GB RAM, 500 MB espaço livre
- **Software**: Windows 10 64 bits, .NET Framework 4.7.2+, Sol.NET ERP instalado
- **Periféricos**: Balança Toledo Prix R7 (ou compatível), leitor de código de barras (recomendado)

**Referência:** [Pré-requisitos do Sistema](Documentacao Instalacao.md#-pré-requisitos-do-sistema)

---

### P: Onde baixo os arquivos necessários para instalação?

**R:** Links diretos para download:
- **DLLs Skia**: [DLLs skia.zip](https://github.com/user-attachments/files/25111774/DLLs.skia.zip)
- **Fontes Poppins**: [Poppins.zip](https://github.com/user-attachments/files/25111757/Poppins.zip)
- **Manual Balança**: [Manual Toledo R7](https://github.com/user-attachments/files/25111795/Manual_do_Usurio_R7_Rev1.pdf)

---

### P: Para onde devo copiar as DLLs do Skia?

**R:** As DLLs devem ser copiadas para o diretório de instalação do Self Checkout:
- **Caminho padrão**: `C:\Program Files\Hetosoft\Sol.NET\SelfCheckout\`
- **Alternativa**: Diretório onde o executável do Self Checkout está localizado

**Importante**: As DLLs devem estar na mesma pasta que o arquivo `.exe` do Self Checkout.

**Referência:** [Instalação das DLLs Skia](Documentacao Instalacao.md#passo-1-instalação-das-dlls-skia)

---

### P: Como instalo as fontes Poppins corretamente?

**R:** Existem três métodos:

**Método Recomendado (mais simples):**
1. Selecione todos os arquivos `.ttf` ou `.otf` extraídos
2. Clique com botão direito → "Instalar para todos os usuários"
3. Aguarde a conclusão

**IMPORTANTE:** Sempre instale "para todos os usuários" para que o Self Checkout possa acessar as fontes.

**Referência:** [Instalação das Fontes Poppins](Documentacao Instalacao.md#passo-2-instalação-das-fontes-poppins)

---

### P: Por que preciso configurar o 6º parâmetro da balança como "TRN 2"?

**R:** O protocolo "TRN 2" é o padrão de comunicação que o Self Checkout Sol.NET utiliza para se comunicar com a balança Toledo. Sem esta configuração:
- O Self Checkout não conseguirá ler o peso
- Produtos pesáveis não funcionarão
- Haverá erros de timeout na comunicação

**CRÍTICO:** Esta é a configuração mais importante da balança.

**Referência:** [Configuração da Balança](Documentacao Instalacao.md#passo-3-configuração-da-balança-toledo-prix-r7)

---

### P: Posso usar outra marca de balança que não seja Toledo?

**R:** O Self Checkout foi desenvolvido para balanças Toledo com protocolo TRN 2. Outras marcas **podem** funcionar se:
- Suportarem o protocolo TRN 2
- Tiverem comunicação serial compatível
- Forem testadas e validadas

**Recomendação:** Entre em contato com o suporte Hetosoft para validar compatibilidade antes de adquirir balanças de outras marcas.

---

## 🐛 Problemas com DLLs e Fontes

### P: Aparece erro "SkiaSharp.dll não encontrada" ao iniciar

**R:** Causas e soluções:

1. **DLLs não estão no lugar correto**
   - Verifique se as DLLs estão no mesmo diretório do executável
   - Caminho esperado: `C:\Program Files\Hetosoft\Sol.NET\SelfCheckout\`

2. **DLLs de arquitetura incorreta**
   - Use a versão 64 bits das DLLs para Windows 64 bits
   - Baixe novamente o pacote correto

3. **Permissões insuficientes**
   - Execute o Self Checkout como Administrador
   - Verifique permissões de leitura/execução nas DLLs

**Referência:** [Problema: DLLs Skia não encontradas](Documentacao Instalacao.md#-problema-dlls-skia-não-encontradas)

---

### P: A interface não mostra as fontes Poppins, está usando fonte padrão

**R:** Checklist de verificação:

1. **Fontes instaladas para todos os usuários?**
   - Verifique em: Painel de Controle → Fontes
   - Procure por "Poppins" - devem aparecer vários pesos

2. **Sistema reiniciado após instalação?**
   - Reinicie o computador ou pelo menos o Self Checkout

3. **Self Checkout executando com usuário correto?**
   - Se instalou só para um usuário, não funcionará para outros

**Solução rápida:**
```cmd
# Reinstalar para todos os usuários (como Administrador)
# Botão direito nos arquivos .ttf → Instalar para todos os usuários
```

**Referência:** [Problema: Fontes Poppins não aparecem](Documentacao Instalacao.md#-problema-fontes-poppins-não-aparecem)

---

## ⚖️ Integração com Balança

### P: Como descobrir qual porta COM a balança está usando?

**R:** 

**Windows:**
1. Abra o "Gerenciador de Dispositivos" (Win + X → Gerenciador de Dispositivos)
2. Expanda "Portas (COM e LPT)"
3. Procure pela balança ou adaptador USB-Serial
4. Anote o número da porta (ex: COM3, COM4, etc.)

**Se usar adaptador USB-Serial:**
- O número pode mudar se trocar a porta USB
- Anote sempre a mesma porta USB para consistência

**Dica:** Tire um print da tela para referência futura.

---

### P: A balança está conectada mas o peso não aparece no sistema

**R:** Checklist de diagnóstico:

**1. Configuração da balança:**
- [ ] 6º parâmetro = TRN 2 ✓
- [ ] Baud Rate = 9600
- [ ] Cabo conectado firmemente

**2. Configuração do Self Checkout:**
- [ ] Porta COM correta configurada
- [ ] Protocolo = TRN 2
- [ ] Baud Rate = 9600
- [ ] Teste de conexão executado

**3. Drivers:**
- [ ] Driver USB-Serial instalado (se aplicável)
- [ ] Porta reconhecida no Gerenciador de Dispositivos

**Teste:** Menu → Configurações → Testar Balança

**Referência:** [Problema: Balança não comunica](Documentacao Instalacao.md#-problema-balança-não-comunica)

---

### P: O peso fica oscilando muito, não estabiliza

**R:** Possíveis causas:

1. **Calibração da balança**
   - Balança precisa ser calibrada conforme manual
   - Use peso padrão certificado

2. **Ambiente**
   - Corrente de ar afetando a balança
   - Vibração da superfície
   - Interferência elétrica

3. **Configuração de estabilidade**
   - Ajuste o timeout no Self Checkout (padrão 5000ms)
   - Verifique configurações de estabilização na balança

**Solução:** Consulte o manual da balança para procedimento de calibração.

---

### P: Uso adaptador USB-Serial, há alguma configuração especial?

**R:** Sim, algumas considerações:

1. **Drivers:**
   - Instale os drivers oficiais do fabricante do adaptador
   - Evite drivers genéricos do Windows quando possível

2. **Porta consistente:**
   - Use sempre a mesma porta USB
   - Marque fisicamente a porta (etiqueta)

3. **Compatibilidade:**
   - Alguns adaptadores baratos podem ter problemas
   - Prefira marcas conhecidas (FTDI, Prolific, etc.)

4. **Teste:**
   - Teste comunicação antes de finalizar instalação
   - Verifique se porta não "desaparece" intermitentemente

---

## 🛒 Operação do Self Checkout

### P: Como configurar produtos pesáveis?

**R:** Três requisitos:

**1. No cadastro do produto (Sol.NET):**
- Marcar produto como "Pesável"
- Unidade de medida = KG ou G
- Código de barras deve começar com prefixo configurado

**2. No Self Checkout:**
- Configurar prefixo de produtos pesáveis (geralmente "2")
- Aba: Produtos → Prefixo produtos pesáveis

**3. Código de barras:**
- Formato típico: `2XXXXXYYYY` onde:
  - `2` = prefixo de pesável
  - `XXXXX` = código do produto
  - `YYYY` = peso ou preço (dependendo da configuração)

**Referência:** [Problema: Produtos pesáveis não funcionam](Documentacao Instalacao.md#-problema-produtos-pesáveis-não-funcionam)

---

### P: Posso configurar múltiplas formas de pagamento?

**R:** Sim! Configure na aba "Pagamento":
- ✅ Dinheiro (cálculo automático de troco)
- ✅ Cartão de Crédito/Débito (com ou sem integração TEF)
- ✅ PIX (conforme configuração do Sol.NET)
- ✅ Vale/Ticket (se configurado)
- ✅ Múltiplas formas na mesma venda

**Importante:** Integração com TEF requer configuração adicional e equipamento compatível.

---

### P: Como funciona a integração com o Sol.NET?

**R:** O Self Checkout integra em tempo real:

**Vendas:**
- Cada venda finalizada é registrada como movimento no Sol.NET
- Tipo de movimento configurável
- Série fiscal configurável

**Estoque:**
- Atualização automática ao finalizar venda
- Respeita regras de estoque do Sol.NET

**Financeiro:**
- Gera contas a receber (se configurado)
- Integra com portadores de pagamento
- Registro de quitações

**Fiscal:**
- Emissão de cupom fiscal conforme legislação
- Numeração sequencial controlada
- Integração com impressora fiscal

---

## 🔄 Manutenção e Atualizações

### P: Com que frequência devo fazer manutenção no Self Checkout?

**R:** Rotina recomendada:

**Diariamente:**
- Verificar logs de erro
- Testar comunicação com balança
- Verificar impressora fiscal

**Semanalmente:**
- Limpeza física (tela, leitor, teclado)
- Verificar espaço em disco
- Backup de configurações

**Mensalmente:**
- Verificar atualizações do Sol.NET
- Revisar logs para problemas recorrentes
- Calibração da balança (se necessário)

---

### P: Como atualizo o Self Checkout?

**R:** Processo de atualização:

1. **Verifique compatibilidade**
   - Versão do Self Checkout compatível com Sol.NET
   - Verifique notas de release

2. **Backup**
   - Faça backup das configurações
   - Anote todas as configurações específicas

3. **Atualize em horário de baixo movimento**
   - Preferencialmente fora do horário comercial

4. **Teste antes de liberar**
   - Execute todos os testes de validação
   - Verifique integração com Sol.NET

**IMPORTANTE:** Entre em contato com suporte antes de atualizar versões principais.

---

### P: O que fazer se o Self Checkout travar durante uma venda?

**R:** Procedimento de recuperação:

1. **Não desligue imediatamente**
   - Aguarde 30 segundos
   - Sistema pode estar processando

2. **Se continuar travado:**
   - Anote o que estava acontecendo
   - Tire foto da tela (se possível)
   - Feche pelo Gerenciador de Tarefas

3. **Reinicie o aplicativo**
   - Self Checkout deve recuperar sessão
   - Ou permita iniciar nova venda

4. **Verifique no Sol.NET**
   - Se a venda foi registrada
   - Se estoque foi atualizado

5. **Relate ao suporte**
   - Forneça logs de erro
   - Descreva o cenário

---

## 🔐 Segurança e Permissões

### P: Preciso executar o Self Checkout como Administrador?

**R:** Não necessariamente, mas depende:

**Primeira execução:**
- Pode requerer privilégios de administrador
- Para criação de arquivos de configuração

**Uso diário:**
- Usuário padrão deve funcionar
- Se configurado corretamente durante instalação

**Se precisar sempre de Admin:**
- Verifique permissões da pasta de instalação
- Ajuste permissões para usuários padrão poderem executar

---

### P: Como proteger as configurações do Self Checkout?

**R:** Boas práticas:

1. **Backup regular**
   - Copie arquivos de configuração periodicamente
   - Mantenha em local seguro

2. **Documentação**
   - Anote todas as configurações específicas
   - Porta COM, IPs, senhas, etc.

3. **Controle de acesso**
   - Defina permissões adequadas no Windows
   - Limite acesso às configurações

4. **Senha no Sol.NET**
   - Configure senha para acesso ao menu de configurações
   - Não compartilhe com usuários finais

---

## 📞 Suporte

### P: Quando devo entrar em contato com o suporte técnico?

**R:** Entre em contato se:

❌ **Problemas não resolvidos pela documentação**
- Consultou FAQ, Guia de Instalação e Guia Rápido
- Tentou soluções sugeridas sem sucesso

❌ **Erros críticos**
- Self Checkout não inicia
- Perda de dados
- Problemas de integração com Sol.NET

❌ **Dúvidas sobre compatibilidade**
- Hardware não listado na documentação
- Versões específicas de software

✅ **ANTES de contatar, tenha em mãos:**
- Versão do Sol.NET e Self Checkout
- Versão do Windows
- Descrição detalhada do problema
- Prints de erros
- Logs (se disponíveis)
- Configurações anotadas (porta COM, etc.)

---

### P: Onde encontro os logs de erro do Self Checkout?

**R:** Localização padrão dos logs:

```
C:\ProgramData\Hetosoft\Sol.NET\SelfCheckout\Logs\
```

**Ou:**

```
C:\Users\[Usuario]\AppData\Local\Hetosoft\Sol.NET\SelfCheckout\Logs\
```

**Como enviar para suporte:**
1. Navegue até a pasta de logs
2. Localize os arquivos mais recentes
3. Compacte em ZIP
4. Envie junto com descrição do problema

---

## 🎯 Dicas e Boas Práticas

### P: Qual o tempo médio de instalação do Self Checkout?

**R:** 
- **Técnico experiente**: 30-45 minutos
- **Primeira instalação**: 1-2 horas (incluindo testes)
- **Instalação em múltiplos terminais**: 20-30 min/terminal (após primeiro)

**Dica:** Prepare um pendrive com todos os arquivos necessários para agilizar.

---

### P: Posso usar o Self Checkout em modo offline?

**R:** **Não.** O Self Checkout requer conexão constante com o Sol.NET para:
- Consultar produtos e preços
- Atualizar estoque em tempo real
- Registrar vendas
- Integrar financeiro

**Em caso de queda de conexão:**
- Sistema alertará o usuário
- Vendas em andamento podem ser perdidas
- Não é possível continuar operando

**Recomendação:** Mantenha conexão estável e redundante.

---

## 🔗 Links Úteis

### Documentação Relacionada
- **[Documentação Completa de Instalação](Documentacao Instalacao.md)**
- **[Guia Rápido](Guia Rapido.md)**
- **[Índice do Módulo](README.md)**

### Downloads
- **[DLLs Skia](https://github.com/user-attachments/files/25111774/DLLs.skia.zip)**
- **[Fontes Poppins](https://github.com/user-attachments/files/25111757/Poppins.zip)**
- **[Manual Balança Toledo R7](https://github.com/user-attachments/files/25111795/Manual_do_Usurio_R7_Rev1.pdf)**

---

**📅 Última atualização**: Fevereiro de 2026  
**📦 Versão**: 1.0  
**🎯 Público-alvo**: Equipe de suporte e usuários finais  
**💬 Contribuições**: Envie novas perguntas para atualização deste FAQ
