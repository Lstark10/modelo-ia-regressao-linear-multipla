# Predição de Níveis de Colesterol - Regressão Linear Múltipla

Este projeto implementa um modelo de **Regressão Linear Múltipla** para predizer níveis de colesterol com base em características pessoais e estilo de vida dos indivíduos.

## 📊 Sobre o Projeto

O objetivo é desenvolver um modelo preditivo que estime os níveis de colesterol de uma pessoa considerando variáveis como:
- Grupo sanguíneo
- Hábito de fumar
- Nível de atividade física
- Idade
- Peso
- Altura

## 🗂️ Estrutura do Projeto

```
regressao-linear-multipla/
│
├── dataset_colesterol.csv      # Dataset com os dados de treinamento
├── modelo_colesterol.ipynb     # Notebook principal com análise e modelagem
├── app_gradio_colesterol.ipynb # Interface Gradio para o modelo
├── modelo_colesterol.pkl       # Modelo treinado salvo
├── requirements.txt           # Dependências do projeto
└── README.md                 # Este arquivo
```

## 📋 Dataset

O dataset contém **1000 registros** com as seguintes colunas:
- **Id**: Identificador único
- **Grupo Sanguíneo**: A, B, AB, O
- **Fumante**: Sim/Não
- **Nível de Atividade**: Baixo, Moderado, Alto
- **Idade**: Idade em anos
- **Peso**: Peso em kg
- **Altura**: Altura em cm
- **Colesterol**: Nível de colesterol (variável target)

## 🔬 Metodologia

### 1. Análise Exploratória de Dados (EDA)
- Verificação da estrutura dos dados
- Detecção e tratamento de valores ausentes
- Análise de outliers
- Visualizações para entender relações entre variáveis
- Análise de correlação

### 2. Pré-processamento
- **Imputação de valores ausentes**:
  - Variáveis categóricas: moda
  - Variáveis numéricas: mediana
- **Remoção de outliers**: pessoas com peso < 40kg
- **Encoding de variáveis categóricas**:
  - One-Hot Encoding para variáveis nominais (grupo sanguíneo, fumante)
  - Ordinal Encoding para variáveis ordinais (nível de atividade física)
- **Padronização**: StandardScaler para variáveis numéricas

### 3. Modelagem
- **Algoritmo**: Regressão Linear Múltipla
- **Pipeline**: Integração completa de pré-processamento e modelo
- **Divisão**: 70% treino / 30% teste
- **Random State**: 51 (para reprodutibilidade)

### 4. Avaliação
- **R² Score**: Coeficiente de determinação
- **MAE**: Erro Absoluto Médio
- **RMSE**: Raiz do Erro Quadrático Médio

### 5. Análise de Resíduos
- Verificação de linearidade
- Teste de homocedasticidade
- Testes de normalidade:
  - Shapiro-Wilk
  - Kolmogorov-Smirnov
  - Lilliefors
  - Anderson-Darling
- Teste de Goldfeld-Quandt para homocedasticidade

## 🚀 Como Usar
OBS: Caso queira optar por executar em ambientes como Google collab ou Anaconda jupyter, basta descomentar a primeira célula do arquivo ipynb e executar o arquivo caso esteja faltando alguma dependencia. É uma alternativa ao arquivo requirements.txt.

### Pré-requisitos
```bash
pip install -r requirements.txt
```

### Executando o Projeto

1. **Análise e Treinamento**:
   ```bash
   jupyter notebook modelo_colesterol.ipynb
   ```

2. **Interface Gradio** (se disponível):
   ```bash
   jupyter notebook app_gradio_colesterol.ipynb
   ```

### Predição Individual

```python
import joblib
import pandas as pd

# Carregar o modelo
model = joblib.load('modelo_colesterol.pkl')

# Exemplo de predição
predicao = {
    'grupo_sanguineo': 'O',
    'fumante': 'Não',
    'nivel_atividade_fisica': 'Alto',
    'idade': 40,
    'peso': 70,
    'altura': 180
}

sample_df = pd.DataFrame(predicao, index=[0])
resultado = model.predict(sample_df)
print(f"Nível de colesterol previsto: {resultado[0]:.2f}")
```

## 📈 Resultados

O modelo apresenta métricas de avaliação que podem ser consultadas no notebook principal, incluindo:
- Coeficiente de determinação (R²)
- Erro absoluto médio (MAE)
- Raiz do erro quadrático médio (RMSE)

## 🛠️ Tecnologias Utilizadas

- **Python 3.12+**
- **Pandas**: Manipulação de dados
- **NumPy**: Operações numéricas
- **Scikit-learn**: Machine Learning
- **Seaborn/Matplotlib**: Visualizações
- **Scipy**: Testes estatísticos
- **Statsmodels**: Análises estatísticas avançadas
- **Pingouin**: Testes estatísticos
- **Joblib**: Serialização do modelo

## 📝 Análises Realizadas

### Bucketing
- **Idade**: Faixas etárias (20-29, 30-39, ..., 70-79)
- **Peso**: Faixas de peso (40-49, 50-59, ..., 150-159)

### Visualizações
- Boxplots para análise de outliers
- Scatter plots para relações entre variáveis
- Mapas de calor para correlações
- Pairplot para análise multivariada
- QQ plot para normalidade dos resíduos

## 🔍 Insights

O projeto permite identificar quais variáveis têm maior impacto nos níveis de colesterol, auxiliando na compreensão dos fatores de risco cardiovascular.

## 📄 Licença

Este projeto é desenvolvido para fins educacionais e de pesquisa.

