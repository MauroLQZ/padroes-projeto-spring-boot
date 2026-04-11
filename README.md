Date do projeto padrões de projeto utilizando o Spring Boot.

- Utilizando o conceito de padrões de projetos na prática:

1- Singleton(padrão criacional):
- permite que uma determinada instância seja criada de forma única, e que essa instância seja reutilizada em aplicações posteriores daquele determinado objeto.
- utilizado o @bean e @autowired, para inversão de controle e injeção de dependência para gerenciar o consumo de memória dentro da aplicação. 

2- strategy(padrão comportamental):
- Simplificar a variação de algoritmos através de uma mesma interface, que encapsula(contrato de um determinado algoritmo) com uma ou mais implementações, disponibilizando variações dessa mesma estratégia.
- o repository(repositório), que tem uma relação direta com abstração de camada de persistência do próprio Spring para implementar de uma maneira concreta. 

3- facade(padrão estrutural):
- Prove uma interface que reduz a complexidade nas integrações com sub-sistemas, abstraindo toda a complexidade de interação com esses sistemas para consumo de informções.
- integrando no projeto o spring data jpa para persistência e uma api externa ViaCep que consumida via openfeign que é um client rest declarativo, onde foi criado um cliente http por meio de uma api externa.
- além do banco em memória H2.

- O projeto foi definido com os seguintes pacotes:

1- model: Cliente, ClienteRepository, Endereco e EnderecoRepository.
- modelos entidades de dominio da aplicação.
- a idéia é que a api faça o cadastro dos clientes buscando os endereços deles na api ViaCEP e complementando essas informações para que o cliente seja armazenado com esses dados.
- o cliente é uma @Entity e tem o id automatico.
- o cep é a chave primaria do Endereco, pois foi consumida a api ViaCep com o cep do endereço, onde vai ser retornado as informações do endereço.
- ClienteRepository e EnderecoRepository que estendem do CrudRepository, são interfaces para persistência dos dados.

2- service:ClienteService e ViaCepService.
- camada de negócio que cria as regras do negócio.
- ClienteService interface que define o padrão Strategy no domínio de cliente com as operações de Crud para a persistência dos dados.
- ViaCepService uma interface Client HTTP, criado via OpenFeign, para o consumo da API do ViaCEP.

3- impl: ClienteServiceImpl.
- implementa os métodos da interface ClienteService que são as operações de crud, está classe vai ser o coração do sistema.

4- controller: ClienteRestController.
- camada de controle que tem a annotation @RequestMapping("clientes"), a mesma que usada no OpenFeign.
- tem todas as operações básicas get, get por id, post, put e delete. 

- Executamos a aplicação através openapi-swagger-ui.
- Quando executamos a aplicação o primeiro componente a ser acionado é o ClienteRestController, porque ele expõe os endpoints, interface de consumo que temos visualmente no swagger. 
