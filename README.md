# Rota Inteligente — Otimização de Entregas para "Sabor Express"

## 1. Descrição do problema
A “Sabor Express” enfrenta rotas manuais ineficientes em horários de pico, gerando atrasos, custos maiores (combustível/tempo) e insatisfação de clientes. O objetivo é sugerir rotas melhores e agrupar entregas próximas para reduzir tempo total e distância percorrida.

## 2. Objetivos
- Modelar a cidade como um grafo (nós = bairros/pontos; arestas = ruas com peso = tempo/distância).
- Agrupar pedidos próximos (K-Means) para atribuir zonas a entregadores.
- Encontrar rotas eficientes dentro de cada zona usando algoritmos de busca/heursticas (A*, shortest path + heurística de ordem: nearest neighbor).
- Avaliar desempenho com métricas: distância total, tempo estimado, tempo de execução e eficiência do agrupamento.

## 3. Abordagem adotada
### 3.1 Representação do mapa
- O mapa é representado por um grafo `networkx.Graph()` com coordenadas (x,y) em cada nó.
- As arestas recebem peso `distância euclidiana` (ou tempo estimado se multiplicado por fator).

### 3.2 Agrupamento de entregas (K-Means)
- Aplicado sobre coordenadas geográficas dos pedidos.
- Objetivo: agrupar pedidos próximos para que cada entregador execute uma rota concentrada em uma área.

### 3.3 Planejamento de rota dentro de cada cluster
- Para cada cluster:
  1. Seleciona-se um **depósito** (depot) como origem (ex.: cozinha).
  2. Calcula-se caminhos mais curtos entre pares de pontos usando `networkx.shortest_path_length` (peso = distância).
  3. Usa-se uma heurística **Nearest Neighbor (NN)** para ordenar entregas: a cada passo, ir para o ponto mais próximo ainda não visitado (baseado na distância de grafo).
  4. Para melhorar (e reduzir custo), pode-se aplicar 2-opt local (opcional) para ajustar a ordem (no código há referência/estrutura para 2-opt).

- Também demonstramos A* para encontrar caminho entre pontos (útil se houver heurística espacial).

### 3.4 Algoritmos implementados/demonstrados
- **A\*** — busca heurística entre nós (usando distância euclidiana como heurística admissível).
- **BFS / DFS** — demonstração de travessia do grafo.
- **K-Means** — agrupar entregas.
- **Nearest Neighbor + shortest-path** — rota heurística por cluster.

## 4. Diagrama do grafo
- O diagrama é gerado automaticamente pelo script (`matplotlib` + `networkx`) e salvo em `outputs/graph_map.png`.
- Visualiza nós (interseções), arestas (ruas), pedidos e rotas planejadas.

## 5. Métricas e análise dos resultados
- **Distância total percorrida**: soma das distâncias reais do grafo para todas as rotas.
- **Tempo estimado total**: distância / velocidade média (parâmetro).
- **Tempo de computação**: tempo gasto para executar clustering + roteamento.
- **Custo relativo**: custo estimado em combustível (proporcional à distância).
- **Coesão do cluster**: inércia do K-Means (menor é melhor).

### Interpretação típica dos resultados
- Redução da distância total comparada ao baseline (ordem aleatória ou manual).
- Trade-off: melhor clusterização reduz deslocamentos longos, mas aumenta o número de rotas paralelas (mais entregadores).

## 6. Limitações encontradas
- Dados são sintéticos (para avaliação; para produção, integrar com API de mapas e dados de tráfego).
- Heurísticas (NN, 2-opt) não garantem solução ótima (problema é equivalente ao VRP/TSP e NP-hard).
- Não há otimização de capacidade (nº máximo de pedidos por entregador) — possível extensão com MILP ou metaheurísticas.

## 7. Sugestões de melhoria
- Integrar dados de tráfego em tempo real (reduzir tempo de viagem).
- Resolver VRP com MILP (OR-Tools) ou metaheurísticas (ga, simulated annealing).
- Implementar balanceamento por capacidade e janelas de tempo (time windows).
- Usar APIs reais (OpenStreetMap / OSRM / GraphHopper / Google Maps) para pesos reais.

## 8. Como executar (resumo)
1. Criar ambiente:
