# Projeto de Detecção de Incêndio com Validação Cruzada

Este projeto visa desenvolver um modelo de classificação para prever a ocorrência de incêndios (`Fire Alarm`) com base em variáveis ambientais coletadas por sensores IoT. Utilizamos validação cruzada para avaliar a performance do modelo, garantindo sua robustez e generalização.

## Sumário do Projeto

O objetivo principal é criar um sistema que possa alertar sobre a possibilidade de um incêndio, analisando dados como temperatura, umidade, concentrações de gases (TVOC, eCO2), e partículas (PM1.0, PM2.5, NC0.5, NC1.0, NC2.5).

## Conjunto de Dados

O conjunto de dados `smoke_detection_iot.csv` contém as seguintes variáveis:

- `Unnamed: 0`: Um índice ou identificador de registro.
- `UTC`: Carimbo de data/hora no formato UTC.
- `Temperature[C]`: Temperatura em graus Celsius.
- `Humidity[%]`: Umidade relativa em porcentagem.
- `TVOC[ppb]`: Concentração total de compostos orgânicos voláteis em partes por bilhão.
- `eCO2[ppm]`: Concentração equivalente de dióxido de carbono em partes por milhão.
- `Raw H2`: Leitura bruta do sensor de hidrogênio.
- `Raw Ethanol`: Leitura bruta do sensor de etanol.
- `Pressure[hPa]`: Pressão atmosférica em hectopascais.
- `PM1.0`, `PM2.5`: Concentrações de partículas finas (material particulado) de 1.0 e 2.5 micrômetros, respectivamente.
- `NC0.5`, `NC1.0`, `NC2.5`: Concentrações numéricas de partículas de 0.5, 1.0 e 2.5 micrômetros.
- `CNT`: Contador de ciclos ou eventos.
- `Fire_Alarm`: Variável alvo, indicando a presença (1) ou ausência (0) de incêndio.

## Análise e Pré-processamento de Dados

1.  **Carregamento e Visualização**: Os dados foram carregados utilizando a biblioteca `pandas` e uma visualização inicial foi realizada para entender a estrutura.
2.  **Renomeação da Variável Alvo**: A coluna 'Fire Alarm' foi renomeada para 'Fire_Alarm' para facilitar o uso.
3.  **Verificação de Tipos de Dados e Valores Ausentes**: Não foram encontrados valores ausentes, e os tipos de dados estavam consistentes.
4.  **Análise de Outliers**: Foi realizada uma análise de outliers para as variáveis `Unnamed: 0`, `Temperature[C]`, `Humidity[%]`, e `TVOC[ppb]` utilizando box plots e inspeção de percentagens. Observou-se a presença de outliers em `Temperature[C]`, `Humidity[%]` e `TVOC[ppb]`. No entanto, para `Humidity[%]` e `TVOC[ppb]`, a grande parte dos dados se enquadrava fora do intervalo interquartil, sugerindo que esses 'outliers' representavam a distribuição real dos dados e foram mantidos.

## Matriz de Correlação

Uma matriz de correlação foi gerada para entender a relação entre as variáveis e a variável alvo `Fire_Alarm`. Os principais insights foram:

-   **Altas Correlações Positivas**: Variáveis como `TVOC[ppb]`, `eCO2[ppm]`, `Raw H2`, `Raw Ethanol`, `PM1.0`, `PM2.5`, `NC0.5`, `NC1.0` e `NC2.5` apresentaram forte correlação positiva com `Fire_Alarm`, o que é esperado em cenários de incêndio.
-   **Correlação Positiva Moderada**: `Temperature[C]` mostrou uma correlação positiva moderada.
-   **Correlação Negativa Moderada**: `Humidity[%]` apresentou uma correlação negativa moderada.
-   **Variáveis Irrelevantes**: `Unnamed: 0`, `UTC` e `CNT` demonstraram correlações muito baixas com `Fire_Alarm`, indicando que podem ser removidas ou ter seu impacto reavaliado em modelos futuros.

<img width="871" height="776" alt="image" src="https://github.com/user-attachments/assets/9bd1d555-29b6-4527-b2e8-b6b354d48c3f" />


## Seleção do Modelo: Regressão Logística

A Regressão Logística foi escolhida para este problema de classificação binária ('Fire_Alarm' = 0 ou 1) devido a:

-   **Natureza da Variável Alvo**: Ideal para prever resultados dicotômicos.
-   **Modelagem de Probabilidades**: Capaz de estimar a probabilidade de um incêndio, não apenas sua ocorrência.
-   **Interpretabilidade**: Coeficientes do modelo são fáceis de interpretar, mostrando a influência de cada variável.
-   **Eficiência e Robustez**: Algoritmo computacionalmente eficiente e adequado para diversas distribuições de preditores.

## Validação Cruzada

Para avaliar a performance do modelo de forma robusta, foi utilizada a validação cruzada K-Fold com `k=5` folds. Isso garante que o modelo seja testado em diferentes subconjuntos dos dados, fornecendo uma estimativa mais confiável de sua performance de generalização.

## Resultados

O modelo de Regressão Logística foi treinado e avaliado utilizando validação cruzada. As pontuações de acurácia por fold foram:

-   **Pontuações por fold**: `[0.97612965 0.97581031 0.98826441 0.98642823 0.97684816]`
-   **Média Final do Modelo**: `0.9207408590132523`

Estes resultados indicam uma alta acurácia média, sugerindo que o modelo de Regressão Logística é eficaz na previsão de incêndios com base nas variáveis fornecidas.

## Próximos Passos (Sugestões)

-   Remover as colunas `Unnamed: 0`, `UTC` e `CNT` que foram identificadas como irrelevantes.
-   Realizar feature engineering, como criação de novas variáveis ou interações entre as existentes.
-   Explorar outros modelos de classificação (e.g., Random Forest, Gradient Boosting) e comparar suas performances.
-   Otimizar hiperparâmetros do modelo utilizando técnicas como `GridSearchCV` ou `RandomizedSearchCV`.
-   Analisar outras métricas de avaliação, como precisão, recall, F1-score e curva ROC, especialmente se houver desbalanceamento de classes.
-   Investigar a remoção ou tratamento de outliers mais agressivo para variáveis como `Temperature[C]` caso a análise posterior justifique.

 
**Gostou da Análise?** Conecte-se para trocarmos experiências e ideias sobre projetos de dados!

🔗 **Meu LinkedIn:** [https://www.linkedin.com/in/diego-kaique-9ba3697b]

📧 **Contato:** [kaique_0208@hotmail.com]
