# Projeto de Análise de Dados em Python

Este projeto tem como objetivo analisar uma base de dados de cancelamentos de serviços, identificar as causas principais dos cancelamentos e propor soluções baseadas nas análises realizadas.

---

## Estrutura do Projeto

### 1. Instalação de Dependências

Certifique-se de instalar as bibliotecas necessárias para executar o projeto:
```bash
pip install pandas numpy openpyxl nbformat ipykernel plotly
```

### 2. Etapas da Análise

#### 2.1 Importação da Base de Dados
A base de dados `cancelamentos.csv` é carregada usando a biblioteca `pandas`:
```python
import pandas as pd

tabela = pd.read_csv("cancelamentos.csv")
```

#### 2.2 Visualização Inicial da Base de Dados
A tabela é visualizada para entender a estrutura dos dados e identificar problemas, como informações irrelevantes:
```python
tabela = tabela.drop(columns="CustomerID")
display(tabela)
```

#### 2.3 Tratamento de Dados
Foram removidos valores vazios para garantir a qualidade dos dados:
```python
display(tabela.info())

tabela = tabela.dropna()
display(tabela.info())
```

#### 2.4 Análise Inicial dos Dados
Identificamos o total de cancelamentos e a porcentagem de cancelamentos:
```python
display(tabela["cancelou"].value_counts())
display(tabela["cancelou"].value_counts(normalize=True))
```

#### 2.5 Análise de Causas
Comparamos diversas colunas com a coluna de cancelamento para identificar padrões:
```python
import plotly.express as px

for coluna in tabela.columns:
    grafico = px.histogram(tabela, x=coluna, color="cancelou", text_auto=True)
    grafico.show()
```

### 3. Propostas de Melhoria

Com base nos resultados da análise:

1. **Contrato Mensal**: Usuários com contrato mensal cancelam frequentemente.
   - **Ação**: Incentivar contratos anuais e trimestrais com descontos.

2. **Call Center**: Usuários que ligaram mais de 4 vezes ao call center cancelaram.
   - **Ação**: Criar um processo de retenção para usuários que ultrapassem 4 ligações.

3. **Atraso no Pagamento**: Usuários com atrasos superiores a 20 dias cancelaram.
   - **Ação**: Implementar alertas para atrasos superiores a 15 dias.

### 4. Aplicando Filtros
Filtramos a base de dados para simular um cenário otimizado:
```python
tabela = tabela[tabela["duracao_contrato"]!="Monthly"]
tabela = tabela[tabela["ligacoes_callcenter"] <= 4]
tabela = tabela[tabela["dias_atraso"] <= 20]

display(tabela["cancelou"].value_counts(normalize=True))
```

### 5. Resultados
A análise permitiu identificar e aplicar soluções que reduziriam a taxa de cancelamento de clientes, criando um impacto positivo no serviço oferecido.

---

## Requisitos

- Python 3.8+
- Bibliotecas: pandas, plotly

---

## Como Executar

1. Instale as dependências listadas.
2. Coloque o arquivo `cancelamentos.csv` no mesmo diretório do script.
3. Execute o script para visualizar a análise e os gráficos gerados.

---

## Autor
Thiago Brandão da Silva

Se tiver dúvidas ou sugestões, entre em contato!

---

## Licença
Este projeto está sob a licença MIT.

