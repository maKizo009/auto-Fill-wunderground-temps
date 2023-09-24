# tempLog
Automatizador de planilhas em 

Por favor, leia a pequena documentação abaixo

## É desenvolvedor e gostaria de contribuir com o projeto? 

 O código está bem comentado e deve ser relativamente fácil entender como ele funciona e os problemas. Consulte a área de bugs e problemas aqui . Se você não é desenvolvedor, mesmo assim é importante olhar tanto a área de bugs, quanto a área seguinte:

# IMPORTANTE: Esse programa serve para mim?

    Esse programa serve para você se:

    - Você quer automatizar a coleta de um conjunto de estções do Wunderground: (Se você quer automatizar apenas uma estação, o repositório "Autofill Wunderground" estará disponível muito em breve);
    - Sua planilha tem abas com o nome "MesANO": Por exemplo: "Setembro2023". Ele verifica se existe uma aba com o nome do mês atual e ano atual e, se tiver, abre e adiciona os dados. Se não tiver, ele duplica a anterior e renomeia com o nome do mês atual. Isso funciona, contanto que você não tenha nehuma formatação condicional ou não se importa com isso, pois parece que implementar tal função seria bem mais difícil e confesso que me falta conhecimento técnico para tal;
    - Os dados da sua planilha começam na linha 4 e coluna B, com cada estação separada por  colunas: Sua planilha tem uma estação que ocupa duas colunas, uma para mínima e outra para máxima? Ela tem dados de várias estações em uma única aba e você gostaria de automatizar a coleta desses dados? Se sim, então esse projeto tem grandes chances de se adequar às suas necessidades. Observe o exemplo:

    "ESTACAO1 - WUNDERGROUND UTC		ESTCAO2 - WUNDERGROUND		ESTACAO3 WUNDERGROUND"
    	MIN	        MAX                     MIN         MAX             MIN         MAX

        Nesse exemplo, temos três estações, e todas elas estão separadas por colunas que, por sua vez, são divididas em subcolunas de mínima e máxima.


    - Se você precisa apenas pegar a temperatura mínima e máxima do dia anterior: Com esse script até o momento só é possível adicionar as temperaturas. A funcionalidade de precipitação é perfeitamente possível de ser feita e seria relativamente mais fácil de implementar. No entanto, não vejo muita demanda disso no momento, então não mexi nisso;


## Todas as características desse projeto

    - Capacidade de pegar dados de um grande conjunto de estações meteorológicas do Wunderground;
    - Capacidade de anotar as temperaturas com base em dia, mês e no ano (note: Ele sempre vai anotar o dia anterior para evitar mínimas invertidas);
    - Capacidade de criar uma nova aba caso não encontre o mês e ano atual: Isso é experimental e pode não funcionar bem se você precisa de formatação condicional;

    Tudo isso é suficiente para tornar a anotação de temperaturas automatizada sem grandes problemas. 
    
    
    Falando em problemas, vamos a eles:



## Possíveis bugs e problemas: {#bugs}

    Primeiro de tudo, teste em uma cópia da sua planilha: Mesmo com todos os pontos mencionados na primeira parte da documentação, pode ser que esse script não seja para você. Os problemas que podem ocorrer são:

    - Formatação condicional não funciona em planilha copiada: Isso é fácil resolver. Basta você mesmo fazer a cópia da planilha, as renomeando com o "MesANO", como eu mencionei no início;
    - Problemas no dia 1 e mês de janeiro: Por favor, teste se os dias 1 de cada mês estão sendo preenchidos corretamente. No começo eu tinha notado isso, então implementei uma estrutura condicional de que:

    Pseudocódigo:
    
    variável dia recebe dia de hoje
    Se variável dia for diferente de 1,
    variável dia receberá dia de hoje - 1
    variável mes também receberá mes atual - 1
    
    (se o dia for de 2 a 31, por exemplo, ele irá pegar o dia anterior. Se for dia 1, ele deve pular para o mês anterior, mas não sei se isso é perfeitamente funcional).
    
    Nos meus testes controlados, colocando "variavel dia recebe 1", funcionou perfeitamente, mas não custa ter cautela, visto que os dados são armazenas como formato datetime. Então fica a dúvida: Quando eu colocar mes - 1 e dia - 1, ele irá pegar o dia 30(ou 31) do mês anterior? 

    - Valores nulos: Durante a leitura, muitas estações podem esar fora do ar, com isso o valor retornado será "**". Talvez você queira fazer umas 5 leituras no dia, e em uma das leituras a estação em si esteja fora. E agora? Então. Ainda não consegui encontrar uma forma de fazer com que esses valores sejam simplesmente ignorados pelo código, ou pior, que um valor já preenchido seja preenchido por outro nulo.
