import pandas as pd
import matplotlib.pyplot as plt
import numpy

#IMPORTANDO E FAZENDO O TRATAMENTO DE DATA
df = pd.read_csv('projeto_puc.csv')
df['data'] = pd.to_datetime(df['data'] , format='%d/%m/%Y')

df.head()

df['ano'] = df['data'].dt.year
df['mes'] = df['data'].dt.month

#VALIDANDO AS COLUNAS
df.info()

print('A analise é de 2006 a 2017!')

data_inicio = input("Digite a data inicial (YYYY-MM-DD): ")
data_fim = input("Digite a data final (YYYY-MM-DD): ")

dados_filtrados = df[(df['data'] >= data_inicio) & (df['data'] <= data_fim)]




#CÓDIGO CHAMA O MAIOR VALOR DE PRECIPITAÇÃO DO PERIODO SOLICITADO
precip = (dados_filtrados)['precip'].max()

#CÓDIGO CHAMA O MENOR VALOR DE TEMPERATURA MINIMA DO PERIODO SOLICITADO
temp_min = (dados_filtrados)['minima'].min()

#CÓDIGO CHAMA O VALOR DA MÉDIA DE TEMPERATURA MINIMA DO PERIODO SOLICITADO
temp_media_min = (dados_filtrados)['minima'].mean()

#CÓDIGO CHAMA O MAIOR VALOR DE TEMPERATURA DO PERIODO SOLICITADO
temp_maxima = (dados_filtrados )['maxima'].max()

#CÓDIGO CHAMA O MAIOR VALOR DE UMIDADE DO PERIODO SOLICITADO
umidade = (dados_filtrados )['um_relativa'].max()

#CÓDIGO CHAMA O MAIOR VELOCIDADE DE VENTO DO PERIODO SOLICITADO
velocidade_vento = (dados_filtrados)['vel_vento'].max()

mes = (dados_filtrados)['precip'].max()


    
print("Escolha o tipo de dado que deseja visualizar:")
print("1) Todos os dados")
print("2) Apenas os de precipitação")
print("3) Apenas os de temperatura")
print("4) Apenas os de umidade e vento")
tipo_dado = int(input("Digite o número correspondente ao tipo de dado: "))

if tipo_dado == 1:
    print(dados_filtrados).head(10)
elif tipo_dado == 2:
    print(f"O mês mais chuvoso foi {mes} com {precip} mm de precipitação.")
elif tipo_dado == 3:
    print(f'A temperatura minima foi {temp_min} °C, e a temperatura maxima foi {temp_maxima} °C')
elif tipo_dado == 4:
    print(f'A média de umidade dos período solicitado é{umidade}, e a média da velocidade de vento é {velocidade_vento}')
else:
    print("Tipo de dado inválido.")


meses = dados_filtrados.groupby('mes')['minima'].mean().plot.bar()
anos = dados_filtrados.groupby('ano')['minima'].mean().plot.bar()
