#1) Observe o trecho de código abaixo: int INDICE = 13, SOMA = 0, K = 0;
#Enquanto K < INDICE faça { K = K + 1; SOMA = SOMA + K; } Imprimir(SOMA); 
#Ao final do processamento, qual será o valor da variável SOMA?

INDICE = 13
SOMA = 0
K = 0

while K < INDICE:
    K = K + 1
    SOMA = SOMA + K

print(SOMA)    


#2) Dado a sequência de Fibonacci, onde se inicia por 0 e 1 e o próximo 
#valor sempre será a soma dos 2 valores anteriores 
#(exemplo: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34...),
#escreva um programa na linguagem que desejar onde, 
#informado um número, ele calcule a sequência de Fibonacci e retorne 
#uma mensagem avisando se o número informado pertence ou não a sequência.

def pertence_fibonacci(n):
    a, b = 0, 1

    if n == 0 or n == 1:
        return True

    while b <= n:
        if b == n:
            return True
        a, b = b, a + b
    
    return False

numero = int(input("Informe um número: "))

if pertence_fibonacci(numero):
    print(f"O número {numero} pertence à sequência de Fibonacci.")
else:
    print(f"O número {numero} não pertence à sequência de Fibonacci.")



    #3) Dado um vetor que guarda o valor de faturamento diário de uma distribuidora, 
#faça um programa, na linguagem que desejar, que calcule e retorne:
#• O menor valor de faturamento ocorrido em um dia do mês;
#• O maior valor de faturamento ocorrido em um dia do mês;
#• Número de dias no mês em que o valor de faturamento diário foi superior à média mensal.

import pandas as pd
from google.colab import files
files.upload()

faturamento_diario = pd.read_json('dados.json')
faturamento_diario.head()

def menor_faturamento(faturamento):
    
    faturamento['valor'] = pd.to_numeric(faturamento['valor'], errors='coerce')
    
    valores_validos = [valor for valor in faturamento['valor'] if valor > 0]  
    
    return min(valores_validos) if valores_validos else float('nan')

def maior_faturamento(faturamento):
    
    faturamento['valor'] = pd.to_numeric(faturamento['valor'], errors='coerce')
    
    return max(faturamento['valor'])


def media_faturamento(faturamento):
    
    faturamento['valor'] = pd.to_numeric(faturamento['valor'], errors='coerce')
    
    dias_com_faturamento = [valor for valor in faturamento['valor'] if valor > 0]
    
    return sum(dias_com_faturamento) / len(dias_com_faturamento) if dias_com_faturamento else float('nan')

def dias_acima_da_media(faturamento):
    
    media = media_faturamento(faturamento)  
    
    faturamento['valor'] = pd.to_numeric(faturamento['valor'], errors='coerce') 
    
    return len([valor for valor in faturamento['valor'] if valor > media]) 

menor_valor = menor_faturamento(faturamento_diario.copy()) 
maior_valor = maior_faturamento(faturamento_diario.copy()) 
dias_acima_media = dias_acima_da_media(faturamento_diario.copy()) 

print(f"Menor valor de faturamento em um dia: R$ {menor_valor:.2f}")
print(f"Maior valor de faturamento em um dia: R$ {maior_valor:.2f}")
print(f"Número de dias com faturamento acima da média mensal: {dias_acima_media} dias")



#4) Dado o valor de faturamento mensal de uma distribuidora, detalhado por estado:
#• SP – R$67.836,43
#• RJ – R$36.678,66
#• MG – R$29.229,88
#• ES – R$27.165,48
#• Outros – R$19.849,53
#Escreva um programa na linguagem que desejar onde 
#calcule o percentual de
#representação que cada estado teve dentro do 
#valor total mensal da distribuidora. 

sp = 67836.43
rj = 36678.66
mg = 29229.88
es = 27165.48
outros = 19849.53

faturamento_mensal = sp + rj + mg + es + outros

percentual_sp = (sp / faturamento_mensal) * 100
percentual_rj = (rj / faturamento_mensal) * 100
percentual_mg = (mg / faturamento_mensal) * 100
percentual_es = (es / faturamento_mensal) * 100
percentual_outros = (outros / faturamento_mensal) * 100

print(f"Percentual SP: {percentual_sp:.2f}%")
print(f"Percentual RJ: {percentual_rj:.2f}%")
print(f"Percentual MG: {percentual_mg:.2f}%")
print(f"Percentual ES: {percentual_es:.2f}%")
print(f"Percentual Outros: {percentual_outros:.2f}%")



#5) Escreva um programa que inverta os caracteres de um string.
#IMPORTANTE:
#a) Essa string pode ser informada através de qualquer entrada 
#de sua preferência ou pode ser previamente definida no código;
#b) Evite usar funções prontas, como, por exemplo, reverse;

def inverter_string(string):
    string_invertida = ""
    
    for i in range(len(string) - 1, -1, -1):
        string_invertida += string[i]
    
    return string_invertida

string = input("Informe a string para ser invertida: ")

string_invertida = inverter_string(string)
print(f"String invertida: {string_invertida}")
