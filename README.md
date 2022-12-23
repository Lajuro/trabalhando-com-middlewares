# **Desafio 02 - Trabalhando com middlewares**

Nesse desafio, será criado middlewares para validar o cadastro de usuários e de *todos*, assim como também verificar se o usuário possui um plano pro ou gratuito e assim permitir ou não a criação de mais de 10 *todos*.

O intuito desse desafio é botar em prática o uso de middlewares para fortalecer o conhecimento sobre o assunto.

## Middlewares

- **checksExistsUserAccount**: Middleware que será utilizado nas rotas que precisam de um usuário autenticado na aplicação. Esse middleware recebe o `username` do usuário pelo header da requisição e verifica se o usuário existe. Caso exista, o usuário é colocado no `request.user` e a requisição é passada para o próximo middleware. Caso o usuário não exista, retorna um erro.
- **checksCreateTodosUserAvailability**: Middleware que será utilizado nas rotas de criação de *todos*. Esse middleware recebe o `username` do usuário pelo header da requisição e verifica se o usuário existe. Caso exista, verifica se o usuário é pro ou não. Caso seja pro, permite a criação de um novo *todo* sem limites. Caso não seja pro, verifica se já existem 10 *todos* cadastrados. Caso existam, retorna um erro. Caso não existam, permite a criação de um novo *todo*.
- **checksTodoExists**: Middleware que será utilizado nas rotas que precisam de um *todo* existente na aplicação. Esse middleware recebe o `username` e o `id` do *todo* pelo header da requisição e verifica se o *todo* existe e o usuário existe. Caso existam, o *todo* e o usuário são colocados no `request.todo` e `request.user` e a requisição é passada para o próximo middleware. Caso o *todo* ou o usuário não existam, retorna um erro.
- **findUserById**: Middleware que será utilizado nas rotas que precisam de um usuário autenticado na aplicação. Esse middleware recebe o `id` do usuário pelo header da requisição e verifica se o usuário existe. Caso exista, o usuário é colocado no `request.user` e a requisição é passada para o próximo middleware. Caso o usuário não exista, retorna um erro.

## Específicação dos testes

Para esse desafio temos os seguintes testes:

### checksExistsUserAccount

- **should be able to find user by username in header and pass it to request.user**: Para que esse teste passe, a aplicação deve permitir que um usuário seja encontrado através do username passado no header da requisição e colocar esse usuário dentro do `request.user`;
- **should not be able to find a non existing user by username in header**: Para que esse teste passe, a aplicação deve retornar um erro quando não for encontrado um usuário com o username passado no header da requisição.

### checksCreateTodosUserAvailability

- **should be able to let user create a new todo when is in free plan and have less than ten todos**: Para que esse teste passe, a aplicação deve permitir que um usuário com plano gratuito possa criar um novo *todo* quando ele já tiver menos de 10 *todos* cadastrados;
- **should not be able to let user create a new todo when is not Pro and already have ten todos**: Para que esse teste passe, a aplicação deve retornar um erro quando um usuário com plano gratuito tentar criar um novo *todo* quando ele já tiver 10 *todos* cadastrados;
- **should be able to let user create infinite new todos when is in Pro plan**: Para que esse teste passe, a aplicação deve permitir que um usuário com plano pro possa criar um novo *todo* sem limites.

### checksTodoExists

- **should be able to put user and todo in request when both exits**: Para que esse teste passe, a aplicação deve permitir que um usuário e um *todo* sejam encontrados através do username e id passados no header da requisição e colocar esses dados dentro do `request.user` e `request.todo`;
- **should not be able to put user and todo in request when user does not exists**: Para que esse teste passe, a aplicação deve retornar um erro quando não for encontrado um usuário com o username passado no header da requisição;
- **should not be able to put user and todo in request when todo id is not uuid**: Para que esse teste passe, a aplicação deve retornar um erro quando o id do *todo* passado no header da requisição não for um uuid válido;
- **should not be able to put user and todo in request when todo does not exists**: Para que esse teste passe, a aplicação deve retornar um erro quando não for encontrado um *todo* com o id passado no header da requisição.

### findUserById

- **should be able to find user by id route param and pass it to request.user**: Para que esse teste passe, a aplicação deve permitir que um usuário seja encontrado através do id passado nos parâmetros da rota e colocar esse usuário dentro do `request.user`;
- **should not be able to pass user to request.user when it does not exists**: Para que esse teste passe, a aplicação deve retornar um erro quando não for encontrado um usuário com o id passado nos parâmetros da rota.
