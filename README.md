# :house: House Rocket Project 
## Descrição
O objetivo deste projeto é fornecer ao time de negócios da **House Rocket**, seguindo algumas regras de negócio, uma lista de imóveis que possivelmente podem ser comprados. Essa lista irá auxiliar o time a tomar as melhores decisões para a empresa. Também são validadas algumas hipóteses de negócio que foram selecionadas visando o lucro máximo da empresa.

A principal ferramenta usada neste projeto foi o "Jupyter Notebook" com as bibliotecas do Pandas para a análise e exploração dos dados e Seaborn, Matplotlib para a visualização dos dados.

Em um resultados geral foram selecionados **9** imóveis que atendiam as regras de negócio selecionadas para um cenário específico. Tendo em conta que todas as compas e vendas foram realizadas esse é o resultado: 

|Número de imóveis | Preço de compra dos imóveis | Preço de venda dos imóveis | **Receita** |
|-------| ------------- | --------- | ------- |
| 9 | $ 3.576.492,00 | $ 4.649.439,60 | **$ 1.072.947,60** |

## :briefcase: Problema de negócio
A House Rocket é uma plataforma digital que tem como modelo de negócio, a compra e a venda de imóveis usando tecnologia. Os cientistas de dados contratos pela empresa são responsáveis por ajudar a encontrar as melhores oportunidades de negócio no mercado de imóveis. O CEO da House Rocket gostaria de maximizar a receita da empresa encontrando boas oportunidades de negócio. Por isso ele fez as seguintes perguntas de negócio:

1. Quais casas o CEO da House Rocket deveria comprar e por qual preço de compra?
2. Uma vez a casa em posse da empresa, qual o melhor momento para vendê-las e qual seria o preço da venda?

Sua principal estratégia é comprar boas casas em ótimas localizações com preços baixos e depois revendê-las posteriormente à preços mais altos. Quanto maior a diferença entre a compra e a venda, maior o lucro da empresa e portanto maior sua receita. Entretanto, as casas possuem muitos atributos que as tornam mais ou menos atrativas aos compradores e vendedores e a localização e o período do ano também podem influenciar os preços.

## :ledger: Os dados e seus atributos
Os dados para este problema podem ser encontrados em https://www.kaggle.com/harlfoxem/housesalesprediction. Na tabela abaixo temos a descrição das *features* contidas no Dataset

| Atributos	| Significado |
|---------|-------|
| id	| Numeração única de identificação de cada imóvel |
| date	| Data da venda da casa |
| price	| Preço que a casa está sendo vendida pelo proprietário |
| bedrooms	| Número de quartos |
| bathrooms	| Número de banheiros (0.5 = banheiro em um quarto, mas sem chuveiro) |
| sqft_living	| Medida (em pés quadrado) do espaço interior dos apartamentos |
| sqft_lot	| Medida (em pés quadrado)quadrada do espaço terrestre |
| floors	| Número de andares do imóvel |
| waterfront	| Variável que indica a presença ou não de vista para água (0 = não e 1 = sim) |
| view	| Um índice de 0 a 4 que indica a qualidade da vista da propriedade. Varia de 0 a 4, onde: 0 = baixa 4 = alta |
| condition	| Um índice de 1 a 5 que indica a condição da casa. Varia de 1 a 5, onde: 1 = baixo |-| 5 = alta |
| grade	| Um índice de 1 a 13 que indica a construção e o design do edifício. Varia de 1 a 13, onde: 1-3 = baixo, 7 = médio e 11-13 = alta |
| sqft_basement	| A metragem quadrada do espaço habitacional interior acima do nível do solo
| yr_built	| Ano de construção de cada imóvel |
| yr_renovated	| Ano de reforma de cada imóvel |
| zipcode	| CEP da casa |
| lat	| Latitude |
| long	| Longitude |
| sqft_livining15	| Medida (em pés quadrado) do espaço interno de habitação para os 15 vizinhos mais próximo |
| sqft_lot15	| Medida (em pés quadrado) dos lotes de terra dos 15 vizinhos mais próximo |

## :office_worker: Premissas de Negócio
Foram adotadas as seguintes premissas de negócio para a resolução desse problema:

* Os valores iguais a 0 em **yr_renovated** são casas que nunca foram reformadas.
* A coluna **price** significa o preço que a casa foi / será comprada pela empresa House Rocket
* As features **sqft_livining15** e **sqft_lot15** foram consideradas sem importância para o nosso projeto
* O design de construção do imóvel (grade), a vista do imóvel (view) e a condição do imóvel (condition), foram caracteristicas decisivas para a compra do imóvel
* A época do ano foi uma caracteristica decisiva para a venda do ano (season)

## :world_map: Estratégia para a solução
Para a solução do prolema de negócio foram seguidos os seguintes passos:
* Descrição dos dados: Nessa etapa foram usados conceitos estatísticos para entender como os meus dados estavam divididos
* Feature Engineering: Nessa etapa foram realizados os seguintes passos
   * Exclusão e criação de algumas features
   * Criação da lista de hipóteses
   * Derivação de features
* EDA - Analise Exploratória de Dados: Aqui foram validadas as hipóteses criadas na seção anterior
* Questões de Negócio: Nessa etapa Foram criados 3 cenários usando diferentes caracteristicas para responder as perguntas de negócio
* Evaluation dos cenários: Nessa etapa foram calculados os custos e lucros de cada cenário

## :bulb: Top 5 Insights
1. Casas que tem vista para a água são mais caras. **Verdade, até 50% mais caras**
2. Casas que possuem mais andares são mais caras. **Falso, Casas com mais andares não são necessariamente mais caras**
3. Casas com um melhor design são mais caras. **Verdade, Casas que tem um design melhor são mais caras**
4. Casas mais antigas são mais baratas. **Falsa, a casas mais aintigas não são mais baratas**
5. A época do ano tem influencia sobre o preço. **Verdade, a época do ano tem influencia sobre os preços das casas**

Nossa tabela de insights ficou assim:

| Hipótese | Resultados |
| ----- | ----- |
|**H01** Casas que estão perto da praia ou tem vista para o mar, são mais caras | **Verdade** |
|**H02** Casas em regiões nobres, são mais caras | **Verdade**|
|**H03** Casas que tem uma vista mais bonita, são mais caras |**Verdade** |
|**H04** Casas com mais andares são mais caras | **Falso**|
|**H05** Casas que tem um design de construção melhor são mais caras |**Verdade** |
|**H06** Casas que foram reformadas são mais caras |**Verdade** |
|**H07** Casas mais antigas são mais baratas | **Falso**|
|**H08** A sazonalidade interfere no preço das casas | **Verdade**|
|**H09** Casas em melhores condições são mais caras | **Falso**|

## :chart: Resultado de negócio
Como foi falado antes, foram criados 3 cenários, com diferentes caracteristicas para que o time de negócios pudessem ter várias visões sobre o mesmo problema, logo foram também avalidados os 3 cenários, sendo que o 1 foi mais abrangente logo o caixa da empresa tem que ser maior, porém o restorno também será maior, o segundo cenário é o mais específico nele foram selecionadas apenas 9 casas, mas que conseguem trazer **1 milhão** em lucro para a empresa, o terceiro foi intermediário.

Para escolher o imóvel foram seguidas as seguintes premissas, os imóveis foram agrupados por região e foi calculada a mediana de cada região (foi usada a mediana, pois imóveis podem variar muito de preço, levando assim a média para cima ou para baixo, por isso decidi usar a mediana). Logo após isso foram aplicadas, em cada cenário, as regras de negócio assim, foram selecionados os imóveis que estavam abaixo da mediana de preço e que atendiam as regras de negócio de cada cenário. Quando em posse da House Rocket, eram vendido na **primavera**, pois é a época do ano em que os preços estão mais elevados, usando sempre a margem de **30% para calcular o preço de venda dos imóveis**.

| Cenário | Custo de aquisição | Receita de venda | Lucro | Principais características |
| -----   | -----              | -----            | ----- | -----                      |
| Cenário 01 | $ 3.289.797.940,00 | $ 4.276.737.322,00 | $ 986.939.382,00 | **Design do imóvel** e **condição do imóvel**                       |
| Cenário 02 | $ 3.576.492,00     | $ 4.649.439,60     | $ 1.072.947,60   | **Visão para a água** e **condição do imóvel**                      |
| Cenário 03 | $ 22.151.890,00    | $ 28.797.457.0     | $ 6.645.567,00   | **Vista do imóvel**, **Design do imóvel**, e **Condição do imóvel** |

## :open_book: Lições Aprendidas
* Aprofundei meus conhecimentos em Python, Pandas e nas bibliotecas de visualização como Seaborn e Matplotlib
* Aprendi sobre regras de negócio e como focar sua análise de dados para responder as perguntas feitas
* Aprendi sobre o modelo de negócio de empresas digitais

## :footprints: Próximos passos
1. Para maximizar os ganhos, é possível fazer reformas para elevar os preços das casas, porém saber quando reformar vale a pena
2. Usar um algoritmo de *Machine Learning* para prever o melhor momento de valorização do imóvel















