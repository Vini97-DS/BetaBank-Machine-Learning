# Previsão de Churn de Clientes do Beta Bank

### Visão Geral do Projeto

Este projeto foca em resolver um desafio crítico de negócios para o Beta Bank: a perda de clientes (churn). Partindo da premissa de que reter clientes existentes é mais econômico do que adquirir novos, o objetivo foi desenvolver um modelo de machine learning capaz de prever com precisão quais clientes têm maior probabilidade de encerrar seus contratos.

O principal indicador de sucesso para o modelo foi o F1-Score, com uma meta mínima de 0.59 no conjunto de teste para garantir um equilíbrio eficaz entre precisão e recall, minimizando tanto a perda de clientes valiosos quanto o custo de ações de retenção desnecessárias.

### Análise Exploratória de Dados (EDA) e Insights
Antes da modelagem, foi realizada uma análise exploratória aprofundada para entender o comportamento dos clientes e identificar os principais fatores associados ao churn. As descobertas mais relevantes foram:

* Geografia: Embora a França tenha o maior número absoluto de clientes, a Alemanha apresenta a maior taxa proporcional de churn, indicando um mercado mais crítico para estratégias de retenção.

* Idade: O churn é significativamente maior na faixa etária de 30 a 40 anos, enquanto clientes entre 40 e 50 anos demonstram maior lealdade. Isso foi validado por um Teste de Hipótese (Teste t), que confirmou uma diferença estatisticamente significativa na idade média entre os grupos.

* Pontuação de Crédito: O pico de churn ocorre em clientes com score considerado bom (entre 650 e 700), diminuindo em scores mais altos.

* Salário Estimado: Observou-se um volume maior de cancelamentos na faixa de renda média-alta (entre $75.000 e $110.000 anuais), sugerindo que a perda de clientes valiosos é uma preocupação.

### Metodologia de Modelagem
O desenvolvimento do modelo seguiu uma abordagem estruturada para lidar com o principal desafio técnico dos dados: o desequilíbrio de classes.

1. Pré-processamento de Dados:

   * Limpeza e tratamento de valores ausentes (na coluna tenure).

   * Codificação de variáveis categóricas (geography, gender) utilizando a técnica de One-Hot Encoding.

   * Divisão dos dados em conjuntos de treinamento (60%), validação (20%) e teste (20%) para garantir uma avaliação robusta do modelo.

2. Tratamento do Desequilíbrio de Classes:

   * Modelos Baseline: Foram treinados modelos de Regressão Logística e Floresta Aleatória nos dados desbalanceados, que resultaram em um baixo F1-Score.

   * Técnicas de Balanceamento: Duas estratégias foram comparadas:

   * Ponderação de Classes (`class_weight='balanced'): Atribui pesos maiores à classe minoritária durante o treinamento.

   * Sobreamostragem (Upsampling): Aumenta o número de amostras da classe minoritária para equilibrar o conjunto de treinamento.

### Seleção e Otimização do Modelo:

A combinação de Upsampling com o modelo Floresta Aleatória apresentou a melhor performance no conjunto de validação.

Os hiperparâmetros do modelo Floresta Aleatória (n_estimators e max_depth) foram otimizados para maximizar o F1-Score.

### Resultados e Performance Final

O modelo final (Floresta Aleatória com Upsampling e hiperparâmetros otimizados) foi avaliado no conjunto de teste, que não foi utilizado durante o treinamento ou a validação, alcançando os seguintes resultados:

     `Métrica	Pontuação Final	Meta Atingida?
        F1-Score	0.5958	Sim (≥ 0.59)
        AUC-ROC	0.8516	N/A` 

O modelo atingiu a meta de F1-Score de 0.59, validando sua eficácia para a identificação de clientes com risco de churn. A alta pontuação de AUC-ROC também confirma a excelente capacidade do modelo em distinguir entre as classes.

### Conclusão e Impacto para o Negócio

Este projeto entregou com sucesso uma ferramenta de previsão de churn que atende aos requisitos técnicos e gera valor de negócio direto para o Beta Bank. O modelo final permite que a equipe de retenção:

Atue proativamente, identificando clientes com alto risco de cancelamento antes que eles deixem o banco.

Direcione esforços de forma eficiente, focando em perfis de clientes que, segundo a análise, são mais propensos ao churn (ex: clientes da Alemanha, na faixa dos 30-40 anos e com renda média-alta).

Reduza custos, otimizando o orçamento de marketing e retenção com ações mais assertivas.

### Tecnologias Utilizadas

* Python 3.9

* Pandas: Para manipulação e limpeza dos dados.

* Scikit-learn: Para pré-processamento, treinamento de modelos e avaliação de métricas.

* Matplotlib & Seaborn: Para visualização de dados e análise exploratória.

* SciPy: Para a realização de testes de hipótese.

* Jupyter Notebook: Como ambiente de desenvolvimento.

