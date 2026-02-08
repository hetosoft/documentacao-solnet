# ❓ FAQ - Self Checkout Sol.NET

## 📋 Perguntas Frequentes

Este documento responde às dúvidas mais comuns sobre instalação, configuração e operação do Self Checkout Sol.NET.

---

## 🔧 Instalação e Configuração

### P: Onde baixo os arquivos necessários para instalação?

**R:** Verifique a pasta padrão de arquivos úteis, no caminho de instalação do Sol.NET. Caso não encontre pode utilizar os links diretos para download:
- **DLLs Skia**: [DLLs skia.zip](https://github.com/user-attachments/files/25111774/DLLs.skia.zip)
- **Fontes Poppins**: [Poppins.zip](https://github.com/user-attachments/files/25111757/Poppins.zip)
- **Manual Balança**: [Manual Toledo R7](https://github.com/user-attachments/files/25111795/Manual_do_Usurio_R7_Rev1.pdf)

---

### P: Para onde devo copiar as DLLs do Skia?

**R:** As DLLs devem ser copiadas para o diretório de instalação do Self Checkout:
- Diretório onde o executável do Self Checkout está localizado
- Use o local de instalação do sistema

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

**R:** O protocolo "TRN 2" é o padrão de comunicação que o Self Checkout Sol.NET utiliza para se comunicar com a balança Toledo. Este parametro diz para a balança enviar qualquer alteração de peso que houver, sem que haja a necessidade da aplicação ficar fazendo a leitura. Sem esta configuração:
- O Self Checkout não conseguirá ler o peso
- Haverá erros de timeout na comunicação

**CRÍTICO:** Esta é a configuração mais importante da balança.

**Referência:** [Configuração da Balança](Documentacao Instalacao.md#passo-3-configuração-da-balança-toledo-prix-r7)

---

### P: Posso usar qualquer marca de balança?

**R:** O Self Checkout foi desenvolvido para balanças com protocolo TRN 2. Qualquer marcas **pode** funcionar se:
- Suportarem o protocolo TRN 2
- Tiverem comunicação serial compatível
- Forem testadas e validadas

---

## 🐛 Problemas com DLLs e Fontes

### P: Aparece erro "SkiaSharp.dll não encontrada" ao iniciar

**R:** Causas e soluções:

1. **DLLs não estão no lugar correto**
   - Verifique se as DLLs estão no mesmo diretório do executável
   - Use o local de instalação do sistema

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
- [ ] Baud Rate = 2400
- [ ] Cabo conectado firmemente

**2. Configuração de Dispositivos no Self Checkout:**
- [ ] Porta COM correta configurada
- [ ] Protocolo = TRN 2
- [ ] Baud Rate = 2400
- [ ] Teste de conexão executado

**3. Drivers:**
- [ ] Driver USB-Serial instalado (se aplicável)
- [ ] Porta reconhecida no Gerenciador de Dispositivos

**Teste:** Configuração Dispositivos → Balança → Testar

**Referência:** [Problema: Balança não comunica](Documentacao Instalacao.md#-problema-balança-não-comunica)

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

4. **Teste:**
   - Teste comunicação antes de finalizar instalação
   - Verifique se porta não "desaparece" intermitentemente

---

## 🛒 Operação do Self Checkout

### P: Posso configurar múltiplas formas de pagamento?

**R:** Não! A aplicação foi desenvolvida para pagamento integral da venda.

---

### P: Como funciona a integração com o Sol.NET?

**R:** O Self Checkout é uma **aplicação separada** que integra com o Sol.NET através do Sync_PDV, assim como Sol.NET_PDV, e o processamento das operações são feitos no servidor através do Sync_SRV:

**Vendas:**
- Cada venda finalizada é registrada como movimento no Sol.NET
- Tipo de movimento configurável no Cadastro de Empresas
- Série fiscal configurável no Cadastro de Empresas

**Estoque:**
- Atualização automática ao finalizar venda
- Respeita regras de estoque do Sol.NET

**Financeiro:**
- Gera contas a receber
- Registro de quitações

---

### P: O que fazer se o Self Checkout travar durante uma venda?

**R:** Procedimento de recuperação:

1. **Não desligue imediatamente**
   - Aguarde 30 segundos
   - Sistema pode estar processando

2. **Se continuar travado:**
   - Anote o que estava acontecendo
   - Tire print da tela (se possível)
   - Feche pelo Gerenciador de Tarefas

3. **Reinicie o aplicativo**
   - Self Checkout deve recuperar sessão
   - Ou permita iniciar nova venda

4. **Verifique no Sol.NET**
   - Se a venda foi registrada
   - Se estoque foi atualizado

5. **Documente o problema**
   - Registre logs de erro
   - Descreva o cenário completo
   - Anote versões e configurações
   - Mantenha histórico para referência futura

---

### P: Onde encontro os logs de erro do Self Checkout?

**R:** Localização padrão dos logs:

```
.\Sol.NET\Arquivos\Geral\Logs\Sol.NET_SelfCheckout\
```

---

## 🎯 Dicas e Boas Práticas

### P: Qual o tempo médio de instalação do Self Checkout?

**R:** 
- **Técnico experiente**: 30-45 minutos
- **Primeira instalação**: 1-2 horas (incluindo testes)
- **Instalação em múltiplos terminais**: 20-30 min/terminal (após primeiro)

---

### P: O Self Checkout funciona em modo offline?

**R:** **Sim, e não.** 
- No sentido de depender de uma conexão com o servidor, o Self Checkout utiliza a mesma dinâmica do Sol.NET_PDV. As informações de cadastros e configurações são obtidas do servidor através do Sync_PDV. 
- As vendas são registradas localmente **sem que haja necessidade de conexão ininterrupta com o servidor**.
- Porém, como o único meio de pagamento é o TEF, que depende de conexão com a internet, neste sentido, não pode ser utilizado offline.

**Em caso de queda de conexão:**
- Se uma venda estiver em andamento e não for possível finalizar o pagamento no Self Checkout, o supervisor pode liberar a venda sem pagamento para que seja feito via POS.

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
**🎯 Público-alvo**: Equipe de suporte técnico  
**💬 Contribuições**: Documente novos problemas e soluções para atualização contínua
