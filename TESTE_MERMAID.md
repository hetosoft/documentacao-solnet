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

## 🧰 Leva-piloto de diagramas — rascunhos a validar

Diagramas em validação antes de irem pros docs finais (PR #36, conteúdo paralelo à reescrita do trio Movimentos 201/202/203).

### Rascunho 1 — Ciclo de vida de um Movimento

Setas sólidas = transição de estado. Setas pontilhadas = operação que gera artefato sem mudar o estado do movimento.

```mermaid
flowchart TD
  E[Em edição] -->|Gravar| L[Lançado]
  L -->|F6 Finalizar| F[Finalizado]
  L -->|F7 Mudar| M[Novo movimento<br/>com outro Tipo]
  F -->|F7 Mudar| M
  F -->|F11 Estornar| X[Estornado]
  F -. F8 Quitar .-> Q[(Quita títulos)]
  F -. F10 NF-e .-> NF[(Emite documento fiscal)]
  F -. F9 Imprimir .-> P[(Impressão)]
```

### Rascunho 2 — Ciclo Orçamento → Pedido → NFC-e

```mermaid
flowchart TD
  O["ORÇAMENTO<br/>(sem efeito no estoque<br/>nem no financeiro)"] -->|F7 Mudar| P["PEDIDO<br/>(estoque baixa<br/>financeiro aberto)"]
  P -->|F7 Mudar| N["NFC-E CUPOM FISCAL<br/>(quitação dispara<br/>emissão fiscal inicia)"]
```

### Rascunho 3 — Fluxo de Produção

```mermaid
flowchart TD
  R[Fórmula cadastrada<br/>na tela 143] -. pré-requisito .-> F[Nova Produção<br/>na tela 144]
  F -->|Iniciar Produção| I[Status: Iniciada]
  I -->|Finalizar Produção| OK[Status: Finalizada]
  I -->|Cancelar| C[Status: Cancelada]
  OK --> M1[Movimento de saída<br/>dos ingredientes]
  OK --> M2[Movimento de entrada<br/>do produto acabado]
  OK --> M3[Movimento de perda<br/>quando a fórmula tem perdas]
  M1 --> T{Vão para a tela<br/>operacional do Tipo<br/>de Movimento configurado}
  M2 --> T
  M3 --> T
  T --> T1[201 Compras]
  T --> T2[202 Vendas]
  T --> T3[203 Outros]
```

## ✅ Verificação

Se você consegue ver os diagramas renderizados acima (e não apenas o código), então o suporte Mermaid está funcionando corretamente! 🎉
