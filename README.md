# WEWEW


O script verificar_csv.py tem como objetivo recalcular os valores das parcelas (valor presente) de contratos de empréstimo consignado usando o método financeiro PRICE invertido, com base em arquivos .csv. Ele organiza os dados por pessoa, realiza cálculos financeiros e salva os resultados em novos arquivos processados.

📌 O que o script faz:
Percorre todos os arquivos .csv em uma pasta chamada ./planilhas.

Identifica pessoas e suas parcelas:

Linhas com 1 na coluna G (ou M) são identificadas como pessoas.

Linhas com 11 são identificadas como parcelas.

A identificação é feita com base nos valores das colunas 6 ou 12 (índices 6 e 12).

Calcula novos valores de parcelas com base em fluxo de caixa descontado, usando a função npf.rate() da biblioteca numpy_financial.

🧮 Cálculo matemático utilizado:
É usado o modelo de amortização PRICE, de forma invertida:

Fórmula usada para cada parcela recalculada:

PMT
𝑖
=
𝑉
𝑃
⋅
𝑖
⋅
(
1
+
𝑖
)
𝑛
−
𝑖
−
1
(
1
+
𝑖
)
𝑛
−
1
PMT 
i
​
 = 
(1+i) 
n
 −1
VP⋅i⋅(1+i) 
n−i−1
 
​
 
Onde:

VP = Valor Presente (somatório das parcelas abertas)

PMT_i = parcela de número i

i = taxa de juros mensal (calculada via npf.rate)

n = número total de parcelas abertas

Esse modelo assume que o valor presente foi pago de forma adiantada e distribui proporcionalmente a nova série de pagamentos com base nessa taxa.

📥 Colunas geradas no arquivo final:
Coluna	Significado
Nova Parcela Nº	Sequência da parcela
Novo Fluxo de Valor Presente	Valor da nova parcela recalculada
Valor Futuro	PMT × número de parcelas
Valor Presente	Soma dos VPs originais (parcelas abertas)
Qtd Parcelas	Quantidade de parcelas abertas
Taxa	Taxa de desconto usada no cálculo
