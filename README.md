# Extraindo Dados do Google Ads com Python! 🚀

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
