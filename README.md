# Desafio Técnico - Engenharia de Dados

Repositório contendo a solução para os 4 desafios propostos em SQL para saneamento de relatórios financeiros, rankings comerciais, detecção de anomalias e análise de produtos.

## Estrutura do Repositório

```text
.
├── dados/
│   ├── buyers.csv
│   ├── orders.csv
│   ├── order_items.csv
│   ├── payments.csv
│   ├── products.csv
│   └── sellers.csv
├── Teste/
│   └── teste_tecnico.ipynb      # Notebook executável com as resoluções e validações comentadas
└── README.md                    
```

## Como Executar

As consultas foram desenvolvidas em SQL e executadas no notebook utilizando pandasql (dialeto SQLite).

**Requisitos**:
- Python 3.x
- Pandas
- pandasql
- Jupyter Notebook, VS Code ou Google Colab

**Passos**:
1. Mantenha os arquivos .csv no diretório dados/.
3. Abra Teste/teste_tecnico.ipynb.
4. Execute as células sequencialmente.

O notebook centraliza o caminho dos arquivos por meio de DATA_DIR, facilitando a execução em diferentes ambientes.

## Principais Decisões Técnicas

- **Desafio 1 — Faturamento Mensal**:
Foi considerada uma janela móvel dos últimos 12 meses em curso (01/12/2023 a 29/11/2024), utilizando apenas pedidos completed e delivered.

O faturamento bruto é recalculado a partir de order_items (qty * unit_price), e a quantidade de pedidos utiliza COUNT(DISTINCT ...).


- **Desafio 2 — Crescimento de GMV**:
O GMV foi representado por orders.total_value, com pedidos completed e delivered como definição operacional adotada para o exercício.

O trimestre atual (Q4/2024) é parcial, com dados até 29/11/2024. A consulta compara esse período com o trimestre anterior e considera apenas sellers com pelo menos 50 pedidos em ambos os períodos.


- **Desafio 3 — Descontos Abusivos**:
O valor bruto e o desconto total são calculados a partir de order_items. Pedidos cancelled são excluídos e são identificados aqueles cujo desconto representa mais de 40% do valor bruto.

Também foi incluída uma validação agregada dos resultados.


- **Desafio 4 — Análise Anômala de Produtos**:
Foi utilizada RANK() para identificar o item de maior valor unitário em cada pedido.

A consulta retorna 0 registros na base fornecida. Uma validação adicional mostra que todos os produtos atingem Rank 1 em pelo menos um pedido, indicando uma limitação da regra para esta base, especialmente pela presença de pedidos com apenas um item.

## Considerações

O uso de pandasql foi adotado exclusivamente para execução do desafio. Em ambiente produtivo, as consultas seriam executadas diretamente no Data Warehouse utilizado pela empresa.

As validações apresentadas no notebook foram incluídas para conferir os resultados e demonstrar as premissas adotadas durante a análise.
