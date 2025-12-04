# 🧪 Teste de Renderização Mermaid

Este arquivo é usado para testar a renderização de diagramas Mermaid no GitHub Pages.

## 📊 Exemplo de Diagrama de Fluxo

```mermaid
graph TD
    A[Início] --> B{Decisão}
    B -->|Sim| C[Ação 1]
    B -->|Não| D[Ação 2]
    C --> E[Fim]
    D --> E
```

## 🗺️ Exemplo de Mindmap

```mermaid
mindmap
  root)Documentação Sol.NET(
    Financeiro
      DRE
      Portadores
      Reforma Tributária
    Movimentação
      Tipos de Movimento
      Fluxo de Trabalho
    RH
      Folha de Pagamento
      Processo Mensal
```

## ⏱️ Exemplo de Linha do Tempo

```mermaid
timeline
    title Cronograma de Implementação
    2026 : Início da Transição
         : CBS substitui PIS/COFINS
    2027 : Período de Adaptação
         : Ajustes no Sistema
    2033 : Conclusão
         : IBS totalmente implementado
```

## ✅ Verificação

Se você consegue ver os diagramas renderizados acima (e não apenas o código), então o suporte Mermaid está funcionando corretamente! 🎉
