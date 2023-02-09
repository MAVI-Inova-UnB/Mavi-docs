# Relatório do estudo das funcionalidades do Google Maps

## Pesquisa das funcionalidades oferecidas pelas APIs do Google Maps

### Objetivos

- Obter os possíveis trajetos de ônibus, de uma determinada empresa, entre dois pontos de interesse escolhidos pelo usuário.
- Mapear as informações que as APIs do Google Maps dispõem no contexto de transportes públicos.

# Experimentos

O __primeiro experimento__ foi determinar se todas as funcionalidades apresentadas na aplicação do [Google Maps](https://www.google.com/maps/) estão disponíveis através de APIs.
A constatação negativa veio após a tentativa de obter as informações de quais linhas de ônibus passavam por determinada parada utilizando a [API Places](https://developers.google.com/maps/documentation/places/web-service?hl=pt-br), como no [Exemplo](https://www.google.com.br/maps/place/DF-480,+km+1,9+norte+-+UnB+Campus+Gama/@-15.9896048,-48.0465862,17z/data=!4m12!1m6!3m5!1s0x935a2a8c49ce3677:0x447f05b6f05fa281!2sUniversidade+de+Bras%C3%ADlia+-+Campus+Gama!8m2!3d-15.98961!4d-48.0443975!3m4!1s0x935a2a8b48d272b9:0xbfc09a0bab0c2ebc!8m2!3d-15.98791!4d-48.04469) apresentado no Google Maps a lista de linhas de ônibus em uma parada. A confirmação da não implementação dessa feature da API foi obtida através do post na [Issue Tracker](https://issuetracker.google.com/issues/35827961).
Com essa funcionalidade ficaria simples, do ponto de vista computacional do cliente, de determinar se os ônibus de determinada empresa passam no ponto de ônibus desejado.

O __segundo experimento__ foi realizar uma requisição na [API Directions](https://developers.google.com/maps/documentation/directions?hl=pt-br), especificando parâmetros que restringe ao meio de transporte ônibus, com a expectativa de retornar os possíveis trajetos que o usuário deveria percorrer para chegar ao destino desejado. A constatação desse experimento foi positiva, obtendo-se além dos trajetos informações a respeito do custo financeiro do trajeto, o tempo de saída e chegada, a distância percorrida, a duração do trajeto, informações detalhadas a respeito das rotas a pé e realizada pelo ônibus, assim como informações sobre a linha do ônibus que será utilizado no trajeto e quantidade de paradas estimadas.

Obter as informações das linhas dos ônibus através dos trajetos é uma forma de contornar o problema relatado no experimento anterior, porém com uma maior custo computacional pois para obter essas informações é necessário percorrer a lista de todos os trajetos sugeridos pela API Directions e dentro desta percorrer a lista da rota. Com essa informação é possível realizar um filtro utilizando a string do nome da empresa para comparar com os nomes das empresas e rejeitar os trajetos que não tenham a mesma, apesar de ser um parâmetro sensível, uma vez que utilizar a string do nome da empresa não é equivalente ao um identificador único de uma empresa, tomando os devidos cuidados no tratamento e comparação das strings é uma funcionalidade que pode ser implementada.

Algumas das limitações observadas foram o não controle total sobre os dados, a API apresenta diferentes sugestões de trajetos em diferentes horários do dia e limita isso na resposta da requisição. Ela não possibilita escolher uma rota definindo uma linha de ônibus de preferência.

Pesquisar os pontos de partida e chegada através da [API Places Autocomplete](https://developers.google.com/maps/documentation/places/web-service/autocomplete?hl=pt-br), apresentou um resultado de alta confiabilidade. Sendo possível obter uma lista de lugares que correspondem com os parâmetros passados na pesquisa e em todos os casos testados foi apresentando o lugar desejado.

[Exemplo da requisição utilizada nos testes](https://maps.googleapis.com/maps/api/directions/json?key=ADD_AQUI_SUA_API_KEY&origin=Universidade+Cat%C3%B3lica+de+Bras%C3%ADlia+-+C%C3%A2mpus+Taguatinga&destination=UnB+Universidade+de+Bras%C3%ADlia+-+Campus+Gama+-+Gama+Leste,+Bras%C3%ADlia+-+DF&region=br&language=pt-BR&alternatives=true&mode=transit&transit_mode=bus&units=metric) - Substitua no parâmetro _key_ a sua chave fornecida pelo Google. Essa requisição possui os parâmetros utilizados na requisição realizada nos testes.

# Custos

Para que fosse possível realizar os testes foi gerada uma chave da API (_API KEY_) na plataforma da Google Maps vinculando com uma conta Google. Através das requisições utilizando essa chave é feita a cobrança dos serviços utilizados. Nesse [link](https://mapsplatform.google.com/pricing/?hl=pt-br) é possível ver os preços que variam para cada serviço utilizado

