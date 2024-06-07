# Extraindo Dados utilizando a API Google Ads com Python! 🚀

  - Documentação Google ADS API: https://developers.google.com/google-ads/api/docs/start?hl=pt-br

Este script foi desenvolvido em Python para extrair dados do Google Ads de forma automatizada. Ele se conecta à API do Google Ads utilizando credenciais armazenadas, define um período de análise de 365 dias a partir da data atual, e executa uma consulta para obter dados detalhados sobre campanhas e grupos de anúncios, incluindo métricas como cliques, custo, impressões, e muito mais.

Os dados retornados pela API são processados e armazenados em um DataFrame do Pandas, facilitando a análise e manipulação posterior. Esse processo automatizado não só economiza tempo, mas também garante a eficiência e precisão na coleta de grandes volumes de dados. Utilizei tecnologias como Python, a API do Google Ads e Pandas para alcançar esses resultados. Este script é uma ferramenta poderosa para qualquer profissional de marketing que busca insights profundos e detalhados sobre suas campanhas de Google Ads.

# 📊 O que o script faz:
***Conexão com a API do Google Ads:*** Utiliza credenciais armazenadas para inicializar o cliente da API.

***Definição de Período:*** Configura um intervalo de datas para análise (últimos 365 dias, definido por regra de negócio!).

***Execução de Consulta:*** Realiza uma consulta SQL para obter dados de campanhas, grupos de anúncios e métricas.

***Tratamento de Dados:*** Coleta, converte e armazena os dados em listas.
  - Foi criado uma função para extração da UF
    
***Criação de DataFrame:*** Organiza todos os dados em um DataFrame do Pandas para análise e manipulação posterior.

# 📈 Benefícios:
***Automação:*** Reduz o tempo gasto na extração manual de dados.

***Eficiência:*** Processa grandes volumes de dados rapidamente.

***Flexibilidade:*** Fácil de adaptar para diferentes períodos ou métricas.

# 🛠️ Tecnologias Utilizadas:
***Python:*** Linguagem de programação.

***Google Ads API:*** Para acesso aos dados.

***Pandas:*** Para manipulação e análise de dados.

# 🌟 Valor da entrega:
Um DataFrame do Pandas repleto de insights valiosos sobre suas campanhas de Google Ads, pronto para ser explorado e analisado!

  ***Documentação das métricas consultadas.***
  
  - campaign.name = O nome da campanha. Este campo é obrigatório e não deve ficar vazio ao criar novas campanhas
  - campaign.id = O ID da campanha. Somente saída
  - adgroup.name = O nome do grupo de anúncios. Este campo é obrigatório e não deve ficar vazio ao criar novos grupos de anúncios.
  - adgroup.id = O ID do grupo de anúncios.
  - metrics.clicks = O número de clicks.
  - metrics.costmicros = A soma dos custos de custo por clique (CPC) e custo por mil impressões (CPM) durante esse período.
  - metrics.average_cpc = O custo total de todos os cliques dividido pelo número total de cliques recebidos.
  - metrics.impressions = Count of how often your ad has appeared on a search results page or website on the Google Network.
  - metrics.interactions = O número de interações. Uma interação é a principal ação do usuário associada a um formato de anúncio: cliques em anúncios de texto e de compras, visualizações de anúncios em vídeo e assim por diante.
  - customer.currency_code = Imutável. A moeda em que a conta opera. É suportado um subconjunto de códigos de moeda do padrão ISO 4217.
  - segments.date = Data à qual as métricas se aplicam. Formato yyyy-MM-dd, por exemplo, 17/04/2018.
  - segments.day_of_week = Dia da semana, por exemplo, SEGUNDA-FEIRA.
  - segments.hour = Hora do dia como um número entre 0 e 23.

# Script por etapas:


#### pip install google-ads
 - Utilizado para instalar a biblioteca oficial do Google Ads

### from google.ads.googleads.client import GoogleAdsClient
  - O que é: O cliente principal para interagir com a API do Google Ads.
  - Uso: Inicializa e autentica a conexão com o Google Ads para realizar consultas e operações.

### from google.ads.googleads.errors import GoogleAdsException
  - O que é: Classe para tratar exceções específicas da API do Google Ads.
  - Uso: Captura e lida com erros que podem ocorrer ao fazer chamadas à API.

### from google_auth_oauthlib.flow import InstalledAppFlow
  - O que é: Utilitário para facilitar o processo de OAuth 2.0 para aplicações instaladas.
  - Uso: Ajuda a autenticar a aplicação usando credenciais de usuário para acessar a API do Google Ads.

### from google.oauth2 import service_account
  - O que é: Fornece suporte para autenticação usando contas de serviço.
  - Uso: Permite autenticação automática com credenciais de conta de serviço para acesso programático.

### from datetime import datetime, timedelta, date
  - O que é: Classes para manipulação de datas e horas.
  - Uso: Facilita a definição de períodos de tempo, como o intervalo de 365 dias utilizado no script.

### from google.protobuf import json_format
  - O que é: Utilitário para converter entre mensagens Protobuf e JSON.
  - Uso: Transforma respostas da API (em formato Protobuf) para JSON, facilitando a manipulação.

### import json
  - O que é: Módulo padrão do Python para trabalhar com JSON.
  - Uso: Converte strings JSON em dicionários Python e vice-versa.

### import pandas as pd
  - O que é: Biblioteca poderosa para manipulação e análise de dados.
  - Uso: Cria DataFrames para organizar e analisar dados extraídos da API do Google Ads.

### import re
  - O que é: Módulo padrão do Python para trabalhar com expressões regulares.
  - Uso: Facilita a busca e manipulação de strings usando padrões (não utilizado diretamente no script).


### client = GoogleAdsClient.load_from_storage("credentials.yml")
  - Aqui, as credenciais do Google Ads são carregadas de um arquivo credentials.yml e um cliente da API é inicializado.

### hoje = date.today()
### data_inicio = hoje - timedelta(days=365)
  - Definem a data de hoje (hoje) e a data de início (data_inicio), que é 365 dias antes da data atual.
```
 try:
 
  customer_id = 'xxxxxxxxxxxx'
  
  ga_service = client.get_service("GoogleAdsService", version="v15")  # Certifique-se de usar a versão correta da API

  query = """SELECT ad_group.name, campaign.name, campaign.id, ad_group.id,\
      metrics.average_cpc, metrics.clicks, metrics.cost_micros,\
      metrics.impressions, metrics.interactions, segments.date, customer.currency_code,\
      segments.day_of_week, segments.hour\
      FROM ad_group\
      WHERE segments.date BETWEEN '{}' AND '{}'\
      AND ad_group.status = 'ENABLED'\
      ORDER BY ad_group.id""".format(data_inicio, hoje)

  response = ga_service.search(customer_id=customer_id, query=query)
```
  - Aqui, a query SQL é criada para buscar dados de campanhas, grupos de anúncios, métricas e segmentos dentro do período definido, e apenas para grupos de anúncios que estão habilitados. A consulta é executada com o serviço GoogleAdsService.
  -   - Está parte é utilizada para extrair dados do GROUP.

```
  campaign_name, campaign_id, adgroup_name, adgroup_id, clicks, costmicros, currency_code, average_Cpc, impressions, interactions, date, hour, day_of_week = [[] for _ in range(13)]

  for dados_api in response:
    # Função que converte cada item em uma string formatada em JSON.
    json_str = json_format.MessageToJson(dados_api)
    # Transforma essa string formatada em JSON em Dicionário.
    dict_bruto = json.loads(json_str)


    campaign_name.append(str(dict_bruto["campaign"]["name"]))
    campaign_id.append(int(dict_bruto["campaign"]["id"]))
    adgroup_name.append(str(dict_bruto["adGroup"]["name"]))
    adgroup_id.append(int(dict_bruto["adGroup"]["id"]))
    clicks.append(int(dict_bruto["metrics"]["clicks"]))
    costmicros.append((float(dict_bruto["metrics"]["costMicros"]) / 1000000))
    currency_code.append(str(dict_bruto["customer"]["currencyCode"]))
    impressions.append(int(dict_bruto["metrics"]["impressions"]))
    interactions.append(int(dict_bruto["metrics"]["interactions"]))
    date.append(datetime.strptime(dict_bruto["segments"]["date"], "%Y-%m-%d").date())
    hour.append(int(dict_bruto["segments"]["hour"]))
    day_of_week.append(str(dict_bruto["segments"]["dayOfWeek"]))

    # Alguns valores estavam como nulos, causando um erro ao inserir os dados no DataFrame.
    if "metrics" in dict_bruto and "averageCpc" in dict_bruto["metrics"]:
        average_Cpc.append(dict_bruto["metrics"]["averageCpc"])
    else:
        average_Cpc.append(0.0)
```

  - Este bloco de código itera sobre a resposta da consulta. Para cada item na resposta:
  - Converte os dados para uma string JSON.
  - Converte a string JSON para um dicionário Python.
  - Extrai os dados relevantes e os adiciona às listas apropriadas.
  - Trata casos onde valores podem estar ausentes (averageCpc).

```
 except GoogleAdsException as ex:
    print(f"Ocorreu um erro: {ex.error.message}")
```
  - Se ocorrer uma exceção durante a execução da consulta, a mensagem de erro será impressa.

```
df = pd.DataFrame({"Campaign_Name" : campaign_name, "Campaign_ID" : campaign_id,
                      "adGroup_Name" : adgroup_name, "adGroup_ID" : adgroup_id,
                      "Clicks" : clicks, "CostMicros" : costmicros, "Hour" : hour,
                      "Moeda" : currency_code, "Average_Cpc" : average_Cpc,
                      "Impressions" : impressions, "Interactions" : interactions,
                      "Date" : date, "Day_of_Week" : day_of_week})
```
  - Todas as listas são combinadas em um DataFrame do Pandas, que facilita a análise e manipulação dos dados.

### Função para extrair o UF do nome da campanha, utilizando expressão regular.

```
def extrair_uf(nome_campanha):
    padrao = r'\b([A-Z]{2})\b'  # Procura por duas letras maiúsculas consecutivas que representam a UF
    resultado = re.search(padrao, nome_campanha)
    if resultado:
        return resultado.group(1)
    else:
        return ''
```
### df['UF'] = df['Campaign_Name'].apply(extrair_uf)
  - Adicionando a coluna UF e aplicando a função na coluna 'Campaign_Name'

```
try:
    # Substitua 'customer_id' pelo ID do cliente do Google Ads ao qual você deseja acessar
  customer_id = 'xxxxxxxxxx'
  ga_service = client.get_service("GoogleAdsService", version="v15")  # Certifique-se de usar a versão correta da API

  query_budget = """SELECT campaign.id ,campaign_budget.amount_micros, segments.date, segments.hour\
      FROM campaign\
      WHERE segments.date BETWEEN '{}' AND '{}'\
      ORDER BY campaign.id""".format(data_inicio, hoje)


  # Correção: Use ga_service.search() em vez de client.service.google_ads.search()
  response = ga_service.search(customer_id=customer_id, query=query_budget)

  # Criando listas vazias
  campaign_id, date, campaignBudget, hour = [[] for _ in range(4)]

  for dados_api in response:
    # Função que converte cada item em uma string formatada em JSON.
    json_str = json_format.MessageToJson(dados_api)
    # Transforma essa string formatada em JSON em Dicionário.
    dict_bruto = json.loads(json_str)

    # print(dict_bruto)

    campaign_id.append(int(dict_bruto["campaign"]["id"]))
    hour.append(int(dict_bruto["segments"]["hour"]))
    campaignBudget.append(dict_bruto["campaignBudget"]["amountMicros"])
    date.append(datetime.strptime(dict_bruto["segments"]["date"], "%Y-%m-%d").date())

except GoogleAdsException as ex:
    print(f"Ocorreu um erro: {ex.error.message}")

```
  - Está parte é utilizada para extrair dados da CAMPANHA.

## Resumo
  - Este código se conecta à API do Google Ads, executa uma consulta para obter dados de desempenho de campanhas e grupos de anúncios, coleta esses dados em listas, trata valores nulos e finalmente cria um DataFrame do Pandas para fácil manipulação e análise.
