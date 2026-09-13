# Regressão Múltipla para Previsão de Preço de Carros

Este projeto usa regressão linear múltipla para estimar o preço de um carro a partir de várias características ao mesmo tempo. Diferente da regressão simples, que olha uma única variável, aqui o preço é previsto combinando vários fatores, como quilometragem, número de cilindros, número de portas e o modelo do carro. A ideia prática é entregar ao modelo o conjunto de atributos de um veículo e ele devolver uma estimativa de preço, aprendida a partir de muitos carros com preços conhecidos.

## Como funciona

A regressão múltipla segue a mesma lógica da simples, buscar a melhor relação entre entradas e saída, mas agora com várias entradas contribuindo juntas para a previsão. Cada feature ganha um peso próprio, que indica o quanto ela empurra o preço para cima ou para baixo, e o modelo aprende esses pesos observando os dados de treino.

Dois cuidados de pré-processamento aparecem no projeto. O primeiro é o tratamento da variável de modelo do carro, que vem como texto e não como número. Para que a regressão consiga usá-la, foi aplicado um LabelEncoder, que converte cada modelo em um código inteiro. O segundo é a padronização das features com o StandardScaler, colocando todas na mesma escala, o que é importante porque quilometragem e número de portas vivem em faixas de valor muito diferentes, e sem esse ajuste a comparação entre os pesos ficaria distorcida.

O projeto usa tanto o statsmodels, que gera um resumo estatístico detalhado da regressão e ajuda a interpretar a influência de cada variável, quanto o fluxo de previsão em si, onde um carro descrito por suas características é transformado no mesmo formato do treino e tem o preço estimado.

## Dados

A base traz 804 registros de carros, cada um com suas características e o preço correspondente. As features usadas na previsão foram quilometragem, número de cilindros, número de portas e o modelo do carro devidamente codificado.

## Resultados

O modelo produz estimativas de preço a partir do conjunto de características informado. Em um teste prático, ao descrever um carro específico com sua quilometragem, cilindros, portas e modelo, a regressão retornou um preço estimado por volta de 9,8 mil, mostrando o uso do modelo de ponta a ponta, das características até o valor previsto. O resumo estatístico gerado pelo statsmodels permite ainda olhar quais variáveis mais pesam na formação do preço.

| Item | Valor |
| --- | --- |
| Tipo | Regressão linear múltipla |
| Registros | 804 |
| Features | quilometragem, cilindros, portas, modelo |
| Pré-processamento | LabelEncoder no modelo, StandardScaler nas features |

## Como rodar

Instale as dependências:

```bash
pip install -r requirements.txt
```

Depois abra o notebook e execute as células em ordem:

```bash
jupyter notebook notebook/regressao_multipla.ipynb
```

## Estrutura do projeto

```
car-price-multiple-regression/
├── notebook/
│   └── regressao_multipla.ipynb   # preparo, regressao e previsao
├── requirements.txt
└── .gitignore
```

## Observações e próximos passos

Um ponto de atenção é o uso do LabelEncoder no modelo do carro, pois ele cria uma ordem numérica entre modelos que na verdade não existe, e isso pode confundir a regressão. Uma evolução natural é testar a codificação one-hot para essa variável, que trata cada modelo de forma independente. Também vale acrescentar métricas de erro como o R quadrado e o erro médio para medir de forma objetiva o quão boas são as previsões.
