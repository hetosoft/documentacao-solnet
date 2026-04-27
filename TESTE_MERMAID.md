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

## 🏭 Fluxograma Produção (subseção Movimentação/Produção)

```mermaid
flowchart LR
    A[Cadastro do produto acabado] --> B[Fórmula de Produto<br/>Tela 143]
    B --> C[Produção de Produto<br/>Tela 144]
    C -->|Iniciar Produção| D[Status: EM PRODUÇÃO]
    D -->|Finalizar Produção| E{Gera 3 movimentos}
    E --> F[Movimento de SAÍDA<br/>insumos consumidos]
    E --> G[Movimento de ENTRADA<br/>produto acabado]
    E --> H[Movimento de PERDA<br/>quando houver]
    F -.vínculo.- G
    F -.vínculo.- H
```

## 🔁 Diagrama de Estados — Status da Produção

```mermaid
stateDiagram-v2
    [*] --> EM_ESPERA
    EM_ESPERA --> EM_PRODUCAO: Iniciar Produção
    EM_PRODUCAO --> FINALIZADO: Finalizar Produção<br/>(gera os 3 movimentos)
    EM_ESPERA --> CANCELADO: Cancelar Produção
    EM_PRODUCAO --> CANCELADO: Cancelar Produção
    FINALIZADO --> CANCELADO: somente se os movimentos<br/>vinculados estiverem cancelados
    CANCELADO --> [*]
    FINALIZADO --> [*]
```

## ✅ Verificação

Se você consegue ver os diagramas renderizados acima (e não apenas o código), então o suporte Mermaid está funcionando corretamente! 🎉
