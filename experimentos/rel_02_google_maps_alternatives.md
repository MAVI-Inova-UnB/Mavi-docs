# Pesquisa de alternativas ao Google Maps que sejam de código aberto ou livres

## Objetivos

Habituar-se com o ecossistema de alternativas open source ao Google Maps

## Resultados

Através da pesquisa realizada foi possível entender o básico a respeito da implementação das funcionalidades de mapas em aplicativos ou sites. Até o momento sabe-se da existência de 5 etapas. Sendo elas:
* Importação de rotas em Serviço de Roteamento (Routing service)
* Edição de General Transit Feed Specification ([GTFS](https://developers.google.com/transit/gtfs?hl=pt-br))
* Serviço de Roteamento ou Motor de Roteamento
* Visualização / agregador de serviços de rotas
* Serviço de pesquisa de lugares com autocomplete

Destas etapas a que têm maior impacto para o projeto, sendo atrelada a funcionalidade de sugestão de rotas, é o resultado gerado pelo serviço de roteamento. Pois dado o contexto do projeto deve-se apresentar as rotas em que somente ônibus e transportes públicos terrestres podem transitar. Além de propor uma rota possível dentro das rotas e horários que as companhias de ônibus oferecem.

Desta forma, houve um foco em entender e descobrir projetos que mostrassem resultados equivalentes ao que o Google Directions fornece e que utilizassem o [OpenStreetMap](https://www.openstreetmap.org/) como visualização do mapa. O [Documento](https://wiki.openstreetmap.org/wiki/Routing/online_routers) apresenta um compilado de serviços de roteamento o que facilitou a pesquisa em restringir a ferramentas  populares utilizadas pela comunidade ou que fossem de código aberto.

De forma superficial todas foram avaliadas em relação às suas demonstrações, esse critério foi utilizado pois entende-se que se houver facilidade ao acessar o que a ferramenta tem a oferecer isso demonstra a maturidade e a relevância dela na comunidade. Em casos que se fazia necessário configurar o ambiente e realizar instalações para que fosse possível testar os serviços localmente foram ignorados. Sendo somente avaliados os que já apresentavam uma instância do serviço integrado com a visualização no OpenStreetMap ou que apresentassem algo que poderia ser evoluído sem muito esforço.

### Ferramentas exploradas

#### [OpenRouteService - ORS](https://openrouteservice.org/)

Esse serviço mostrou-se o mais parecido com o resultado apresentado pelo Google Directions. Sendo até o seu acesso através de uma chave fornecida pela empresa para conseguir testar ou criar aplicações básicas que não realizam muitas requisições sem que haja algum custo. Porém, essa similaridade não é apresentada quando a pesquisa é realizada com a intenção de se obter uma rota utilizando meios de transportes públicos, pois essa não se propõe a isso. Ela possibilita realizar o calcula das rotas utilizando a pé a passeio ou correndo, cadeira de rodas, bicicleta, carros, veículos pesados. Funcionou bem com os testes realizados em Brasília.

#### [Valhalla](https://valhalla.github.io/valhalla/)

Utiliza os dados do OpenStreetMap e do [Transitland](https://www.transit.land/) - [By Referencia](https://valhalla.github.io/valhalla/api/)

Não faz estimativa por trânsito na região, porém tem um plugin que aparentemente possibilita isso mas não como não foi testado não temos essa certeza.

Infelizmente a ferramenta não apresenta dados para o Brasil, porém houve a exploração da mesma por apresentar boa documentação e parecer promissora. Para que os testes fossem possíveis, foi utilizado Paris. Segue um exemplo comparando os resultados do [Google Maps](https://www.google.com.br/maps/dir/Arco+do+Triunfo,+Pra%C3%A7a+Charles+de+Gaulle,+Paris,+Fran%C3%A7a/Torre+Eiffel,+Champ+de+Mars,+5+Av.+Anatole+France,+75007+Paris,+Fran%C3%A7a/@48.8659374,2.2881312,14.71z/data=!3m1!5s0x47e66fe1ee0293a1:0x213fe992eb6cca0c!4m17!4m16!1m5!1m1!1s0x47e66fec70fb1d8f:0xd9b5676e112e643d!2m2!1d2.2950682!2d48.873848!1m5!1m1!1s0x47e66e2964e34e2d:0x8ddca9ee380ef7e0!2m2!1d2.2944813!2d48.8583701!2m1!6e2!3e3!5i2) e do [Valhalla](https://valhalla.openstreetmap.de/directions?profile=bus&wps=2.2944990543196795%2C48.858260200000004%2C2.295037226037673%2C48.8737791), onde o resultado foi divergente.

Depois da realização de outros testes, foi entendido que não são consideradas as rotas de ônibus. O Valhalla realiza o cálculo da rota considerando que o meio de transporte utilizado é o ônibus e não como um meio de transporte público que deverá seguir rotas e horários pré-definidos. O que foi confirmado na [documentação](https://valhalla.github.io/valhalla/api/turn-by-turn/api-reference/) onde se afirma na [plataforma](https://valhalla.openstreetmap.de/) as opções de carro, bicicleta e etc. Sendo então os filtros apresentados, meios de definir um custo ao cálculo ou seja na hora de mostrar os caminhos ele restringe as ruas ou caminhos que o meio de transporte tem acesso seja por peso ou largura.

#### [OpenTripPlanner - OTP](https://docs.opentripplanner.org/en/v2.2.0/)

OpenTripPlanner é uma das duas opções apresentadas no documento da wiki do OST que apresentam suporte ao transporte público. Até o momento não foi identificada demonstrações que pudessem averiguar de fato esse suporte ao transporte público. Porém em sua documentação tem uma lista de aplicações que supostamente utilizam o OTP por debaixo dos panos. Sendo elas: [Exemplo OpenStreetMap](https://www.soundtransit.org/tripplanner/to/location:d0f8163dcc9fae7af13d69300a69cbaa/from/location:landmark_2400/now/1677250800000/travel-by/bus,train/route-option/fastest%20trip/max-walk/1609) e [Exemplo MapBox](https://entur.no/reisedetaljer/2cd2ee9c-6cb8-41ef-a539-48e86080bab2?source=travelResult)

A príncipio aparenta ser uma ferramenta promissora porém para se ter um opnião mais concreta será necessário explorar mais afundo. Tentando subir uma instância da aplicação e entendo como ela dispõe as funcionalidades descritas na documentação.


