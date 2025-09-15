# 🚚 Rota Inteligente: Otimização de Entregas com Algoritmos de IA

## 1. Descrição do Problema
A Sabor Express enfrenta atrasos nas entregas devido a rotas ineficientes.  
Este projeto aplica **algoritmos de grafos (A\*)** e **clustering (K-Means)** para otimizar rotas de entregadores, reduzindo custos e aumentando a satisfação dos clientes.

---

## 2. Objetivos
- Representar a cidade como grafo, com pontos de entrega e restaurante.  
- Usar **A\*** para encontrar rotas mais curtas.  
- Usar **K-Means** para agrupar entregas em zonas eficientes.  
- Avaliar resultados com métricas de distância e inércia do clustering.  

---

## 3. Algoritmos Utilizados
- **A\*** → busca heurística para encontrar menor caminho entre pontos.  
- **K-Means** → aprendizado não supervisionado para agrupar entregas.  

---

## 4. Estrutura do Projeto
/src
main.py
/data
(opcional: mapas ou pedidos em CSV)
/outputs
map_routes.png
results.json
requirements.txt
README.md


---

## 5. Execução

### Instalar dependências
```bash
pip install -r requirements.txt


No Google Colab:

!pip install networkx matplotlib scikit-learn numpy

Rodar
python src/main.py

6. Outputs

outputs/map_routes.png → grafo da cidade com clusters e rota calculada.

outputs/results.json → resultados numéricos, clusters e custo da rota.

Exemplo de saída em JSON:

{
  "clusters": {
    "0": ["ClienteA", "ClienteE"],
    "1": ["ClienteB", "ClienteC", "ClienteD"]
  },
  "inercia_kmeans": 7.92,
  "rota_exemplo": ["Restaurante", "ClienteB", "ClienteD"],
  "custo_rota": 8.2
}

7. Resultados e Discussão

O algoritmo A* encontra caminhos mais curtos que rotas manuais.

O K-Means permite dividir os clientes em zonas, reduzindo tempo médio de entrega.

Limitações: não considera tráfego em tempo real nem múltiplos entregadores simultâneos.

8. Melhorias Futuras

Adicionar dados reais de tráfego.

Implementar algoritmos genéticos ou aprendizado por reforço para otimização dinâmica.

Suporte para múltiplos veículos e entregadores em paralelo.

9. Referências

UPS ORION — sistema de otimização de rotas.

Medium: “Optimizing Logistics: Clustering and MILP”.

ResearchGate: AI-Powered Route Optimization.


---

👉 Ou seja:  
- No `requirements.txt` apenas 4 libs.  
- No `README.md` o fluxo de execução foi atualizado para refletir o **novo script e os novos outputs (`map_routes.png` e `results.json`)**.  

Quer que eu monte também um **diagrama do grafo (em imagem estática)** já pronto para você incluir no README como exemplo?
