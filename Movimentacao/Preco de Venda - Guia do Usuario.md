# Preço de venda na Movimentação

Este guia explica, de forma prática, como o Sol.NET determina o preço de venda de um produto na tela de Movimentação. Use-o para entender por que um item ficou com determinado preço e como configurar o sistema para chegar ao valor desejado.

## O que influencia o preço
O preço de um item na Movimentação é calculado a partir de:
- Empresa selecionada (define base de cálculo padrão e permissões de Tabela de Preço).
- Tabela de Preço (regras por produto/família/grupo/marca/pessoas etc.).
- Condição de Pagamento (à vista x a prazo) e quantidade de parcelas.
- Cliente (pode ter percentuais próprios e participar de vínculos).
- Promoções ativas (prioridade, vínculos e restrições por forma de pagamento/tabela/base).
- Moedas dos preços 1 a 8 (se configuradas, há conversão automática).
- Preferência para substituir preço “0,00” por um preço base (quando ativado).

## Entradas consideradas no cálculo
- Produto, Empresa, Cliente, Condição de Pagamento e Parcelas, Data atual da venda.
- Parâmetros opcionais: Tabela de Preço fixa e Promoção específica.

## Sequência de cálculo (visão simples)
1) Carrega Preços Base e Custos do produto
- Preço 1 … Preço 8 (com conversão de moeda quando houver).
- Custos (Custo Inicial, Unitário, Médio, Último Preço de Compra etc.).

2) Encontra Tabela de Preço aplicável (se houver)
- Verifica vínculos por Produto, Família/Grupo/Subgrupo, Marca, e por Pessoa/Status/Tipo/Ramo/Região.
- Se a Tabela não remover o produto/cliente e houver motivo válido (há regra para produto e para pessoas):
  - Se houver Preço Fixo, usa esse valor como “Preço da Tabela”.
  - Senão, calcula “Preço da Tabela” aplicando o Percentual da Tabela sobre a Base de Cálculo definida na Tabela (pode ser Preço 1..8 ou algum Custo).
- Se não houver Tabela válida, pode haver “fallback”:
  - Buscar o preço da Base de Cálculo da Tabela (se estiver habilitado).
  - Se esse valor não existir e a opção “Buscar Preço 1 quando base estiver zerada” estiver ativa, usa o Preço 1.

3) Aplica a Condição de Pagamento
- Se a Tabela usar “à vista x a prazo” e a condição for a prazo, o sistema escolhe os percentuais de acréscimo/desc. específicos de prazo quando existirem.
- O acréscimo/desc. pode vir:
  - Da Pessoa (quando configurado para aplicar na pessoa); ou
  - Da própria Condição de Pagamento (quando configurada para aplicar dentro da movimentação).
- Esse percentual multiplica o Preço da Tabela e os Preços Base antes de considerar promoção.

4) Define o Preço Sem Promoção
- Se existe Tabela de Preço aplicável, o “Preço Sem Promoção” é o Preço da Tabela (já ajustado pela condição).
- Caso contrário, usa-se a Base de Cálculo solicitada (por padrão, Preço 1), também já ajustada pela condição.

5) Aplica Promoções (quando habilitado)
- Procura promoções ativas para a Empresa, Tabela/Base de Cálculo, Condição de Pagamento e vínculos de Produto/Pessoa.
- Escolhe a promoção válida de maior prioridade.
- Se a promoção tiver Preço Fixo, usa esse valor; se for Percentual, aplica sobre o Preço da Tabela ou sobre a Base de Cálculo (o que for definido pela promoção), sempre após o ajuste da condição.
- Resultado vira o “Preço Com Promoção”. Dependendo da configuração, o preço promocional pode substituir o preço base no item.

6) Arredondamento
- O sistema formata os valores conforme as casas decimais de preço configuradas na Empresa.

## Regras importantes
- Tabela de Preço só vale quando houver regra que atenda ao produto e ao público (ex.: “Todos os produtos” e “Todas as pessoas”, ou regras específicas), e não houver marcação de “remover”.
- Base de Cálculo pode ser um dos Preços 1..8 ou um dos Custos; a Tabela escolhe a base e aplica um percentual de acréscimo/desc.
- Condição de Pagamento pode aumentar ou diminuir o preço (pessoa ou condição), e esse ajuste vem antes da promoção.
- Promoção pode ser Preço Fixo ou Percentual, com prioridade e vínculos semelhantes aos da Tabela de Preço.
- Se algum preço base estiver 0,00 e a opção “substituir por Preço 1” estiver ativa, o sistema usa o Preço 1 como reserva.
- Preços 1..8 podem estar em moedas diferentes; a conversão é automática pelo valor da moeda configurado.

## Exemplos do dia a dia
Os exemplos abaixo usam valores hipotéticos apenas para ilustrar a lógica.

1) Varejo balcão, 2x no cartão (acréscimo de 3%)
- Sem Tabela especial para o produto/cliente.
- Preço 1 do produto = 100,00.
- Condição “Cartão 2x” com acréscimo de 3%.
- Resultado: Preço Sem Promoção = 100,00 × 1,03 = 103,00. Sem promoções, este é o preço final do item.

2) Cliente atacado com Tabela “Atacado” (-10%)
- Tabela de Preço “Atacado” válida para o cliente e produto.
- Base de Cálculo da Tabela = Preço 1; Percentual = -10%.
- Preço 1 = 100,00; Condição à vista (0%).
- Resultado: Preço da Tabela = 100,00 × 0,90 = 90,00 → Preço Sem Promoção = 90,00.

3) Delivery com Tabela e Promoção percentual
- Pedido de canal Delivery com Tabela “Delivery” que define Preço Fixo do produto = 50,00.
- Condição à vista (0%).
- Promoção ativa “-5% no Delivery” para esse produto/tabela.
- Passo 1: Preço da Tabela (ajustado pela condição) = 50,00.
- Passo 2: Promoção -5% sobre o preço da tabela = 50,00 × 0,95 = 47,50.
- Resultado: Preço Com Promoção = 47,50. Dependendo da configuração, o item já fica com esse preço final.

4) Empresa com base de cálculo em Custo Médio
- Empresa configurada para usar “Custo Médio Unitário” como base quando não houver Tabela.
- Custo Médio Unitário do produto na empresa = 30,00; Condição à vista com desconto de 2%.
- Resultado: Base (30,00) × 0,98 = 29,40 → Preço Sem Promoção = 29,40.

5) Base escolhida zerada, com fallback para Preço 1
- Tabela escolhe Base = Preço 2, mas o Preço 2 do produto está 0,00.
- Opção “Buscar Preço 1 quando base estiver zerada” ativa.
- Preço 1 = 80,00; Percentual da Tabela = +5%; Condição a prazo +2%.
- Passo 1: Fallback para Preço 1 = 80,00.
- Passo 2: Tabela (+5%) → 80,00 × 1,05 = 84,00.
- Passo 3: Condição (+2%) → 84,00 × 1,02 = 85,68 → Preço Sem Promoção.

## Como conferir no sistema
- Tabela de Preço aplicada: na Movimentação, ver a informação de tabela/descrição do preço (quando exibida) ou abrir o cadastro da Tabela para revisar vínculos e base.
- Condição de Pagamento: confira se está marcada como a prazo/à vista e se o percentual aplica “na pessoa” ou “na movimentação”.
- Promoção: confira se há promoção válida na data, se atende a empresa/produto/pessoa/condição e qual a prioridade.
- Moedas: verifique a moeda associada aos Preços 1..8 do produto e o valor da moeda configurado.

## Dicas práticas
- Precisa de um preço específico por canal (e-commerce, delivery, balcão)? Crie uma Tabela de Preço por canal e vincule às empresas/canais desejados.
- Quer aplicar preços por cliente (VIP, atacado, região)? Use os vínculos de Pessoas (Pessoa, Status, Tipo, Ramo, Região) na Tabela.
- Para campanhas, prefira Promoções com prioridade e validade; se necessário, use Preço Fixo para garantir o valor final.
- Se muitos produtos têm Preço 2..8 zerados, ative o fallback para Preço 1 nas Tabelas que usam essas bases.

---
Este documento resume o comportamento padrão observado no cálculo de preço. Ajustes finos podem existir por configuração específica em cada ambiente.
