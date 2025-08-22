
#### **1. O que são Rotas?**

As rotas são **URLs** que sua aplicação responde. Elas definem os **endpoints** da sua API ou as páginas do seu site, mapeando uma requisição HTTP para um método de um **Controller** ou para uma função anônima (closure).

#### **2. Definição Básica de Rotas**

As rotas são definidas no arquivo `routes/web.php` (para aplicações web) e `routes/api.php` (para APIs).

|Verbo HTTP|Método Laravel|Exemplo de Uso|Descrição|
|---|---|---|---|
|**GET**|`Route::get()`|`Route::get('/posts', [PostController::class, 'index']);`|Recupera recursos (páginas, dados).|
|**POST**|`Route::post()`|`Route::post('/posts', [PostController::class, 'store']);`|Cria um novo recurso.|
|**PUT/PATCH**|`Route::put()`|`Route::put('/posts/{id}', [PostController::class, 'update']);`|Atualiza um recurso existente.|
|**DELETE**|`Route::delete()`|`Route::delete('/posts/{id}', [PostController::class, 'destroy']);`|Exclui um recurso.|
|**ANY**|`Route::any()`|`Route::any('/contato', function() { ... });`|Responda a qualquer verbo HTTP.|

### ➡️**Autenticação no Laravel**


####📌 **. Autenticação Básica (Pacote `laravel/ui` ou `laravel/breeze`)**

O Laravel oferece um sistema de autenticação pronto para aplicações web tradicionais (com sessões).

o Breeze é a opção mais moderna e recomendada, oferecendo um scaffolding de autenticação com Tailwind CSS e modelos Blade, sendo ideal para quem busca simplicidade ou um ponto de partida para um novo projeto. O UI, por outro lado, é uma versão mais antiga, que utiliza Bootstrap e tem suporte mais limitado, sendo apropriado apenas para projetos legados ou se precisar especificamente de Bootstrap

📌**Comando para scaffold (andaime):**

No Laravel, "scaffolding" refere-se ao processo de geração de uma estrutura básica ou código padrão para um aplicativo, particularmente para funcionalidades comuns como autenticação ou predefinições de front-end.

```PHP
composer require laravel/ui
php artisan ui bootstrap --auth
npm install && npm run dev
```

- **O que isso cria?**
    
    - Rotas: `/login`, `/register`, `/logout`, `/password/reset`, etc.
        
    - Views: `auth/login.blade.php`, `auth/register.blade.php`
        
    - Controller: `AuthController` (não visível, mas rotas definidas)

```PHP
Route::get('/dashboard', function () {
    // Apenas usuários autenticados podem acessar...
})->middleware('auth');
```

----

**"Como você protegeria uma rota de API no Laravel para que apenas usuários autenticados possam acessar?"**

> **Resposta:** Utilizando o middleware `auth:api`. Primeiro, é necessário configurar um driver de autenticação para API, como o Passport ou Sanctum, no arquivo `config/auth.php`. Após a instalação e configuração do pacote escolhido, as rotas da API podem ser agrupadas dentro de um grupo que aplica o middleware `auth:api`, que exige que um token de acesso válido seja enviado no cabeçalho da requisição HTTP (no formato `Authorization: Bearer <token>`).


1.  c) Route::post('/users', ...) V
2.  a) Define onde o controlador está localizado.  X
3. b) Permitir a geração de URLs e redirecionamentos de forma dinâmica e semântica. V
4. b) `routes/api.php` é para rotas de API (stateless), e `routes/web.php` é para rotas web tradicionais (stateful com sessões). V
5. a) `php artisan route:list` V
6. a) `use Notifiable;` X
7. a) `/oauth/authorize` V
8. a) `middleware('auth')` X
9. d) Laravel Breeze X
10. d) Habilita as rotas de autenticação web padrão do Laravel. X
11. c) Definir múltiplas rotas RESTful para um  controlador, excluindo as rotas `create` e `edit`. V
12. d) Todas as alternativas acima estão corretas. V
13. b) Aplicar um middleware a todas as rotas dentro do grupo, exigindo autenticação para acessá-las. V
14. d) `Token: <token>`
15. d) `php artisan passport:generate-keys`


Laravel Sanctum é o pacote é mais indicado para uma API simples onde seu próprio frontend consome os dados, sem a complexidade do OAuth2. O Sanctum é mais leve e simples para tokens de API simples.

métodos 
- `where` : Adiciona uma condição de validação para um parâmetro de rota.
- `name`: Permitir a geração de URLs e redirecionamentos de forma dinâmica.
- `apiResource`: Definir múltiplas rotas RESTful, excluindo `create` e `edit`.
- `$request->input('id')`, `request()->id`,  `$id` (definindo-o como argumento do método do controlador) : O Laravel injeta automaticamente os parâmetros de rota na requisição e nos métodos.

rotas
- `routes/api.php` é para rotas de API (stateless), e `routes/web.php` é para rotas web tradicionais.
- `php artisan route:list` : Lista todas as rotas, seus verbos, URIs, nomes e ações.
- `/oauth/token` : Esta é a rota padrão para o fluxo "password grant" do OAuth2.
- `Passport::routes()`: Essa única linha de código é responsável por registrar todas as rotas de autenticação OAuth2
- `Route::middleware(['auth'])->group(...)`: Aplicar um middleware a todas as rotas dentro do grupo, exigindo autenticação para acessá-las. V

Passport
- `use HasApiTokens;` : Este trait é fornecido pelo Passport para gerenciar tokens.
- `middleware('auth:api')`: O guard `api` configurado para usar o Passport é acionado.
- `php artisan passport:install` :Este comando gera as chaves de criptografia e cria clientes OAuth.


**1. Em PHP, qual é a função usada para exibir um texto no navegador?**  
a) `print_r()` X
b) `echo()`  
c) `display()`  
d) `show()`

**2. No Laravel, qual comando Artisan é usado para criar um novo controlador?**  
a) `php artisan make:controller`  
b) `php artisan create:controller`  
c) `php artisan new:controller`  
d) `php artisan generate:controller`

**3. No .NET, qual namespace é usado para trabalhar com entidades de banco de dados no Entity Framework?**  
a) `System.Data.Entity`  
b) `Microsoft.EntityFrameworkCore`  
c) `System.Data.SqlClient`  
d) `Microsoft.Data.Entity`

**4. Em bancos de dados relacionais, qual comando SQL é usado para inserir um novo registro em uma tabela?**  
a) `INSERT INTO`  
b) `ADD RECORD`  
c) `CREATE ROW`  
d) `NEW ENTRY`

**5. Qual serviço de computação em nuvem da AWS oferece armazenamento de objetos?**  
a) Amazon S3  
b) Amazon RDS  
c) Amazon EC2  
d) Amazon VPC

**6. Em DevOps, qual é o objetivo principal do CI/CD?**  
a) Automatizar o processo de desenvolvimento e entrega de software.  
b) Gerenciar a equipe de desenvolvimento.  
c) Monitorar o desempenho da aplicação.  
d) Criar documentação técnica.

**7. No Git, qual comando é usado para criar uma nova branch?**  
a) `git branch nova-branch`  
b) `git checkout nova-branch`  
c) `git create branch nova-branch`  
d) `git new branch nova-branch`

**8. Em segurança da informação, qual ataque envolve a inserção de código malicioso em um site?**  
a) SQL Injection  
b) DDoS  
c) Phishing  
d) Man-in-the-Middle

**9. Na análise de requisitos, o que é uma "regra de negócio"?**  
a) Uma restrição ou diretriz específica do domínio do problema.  
b) Um diagrama de sequência do sistema.  
c) Um caso de uso do usuário.  
d) Um protótipo de interface.

**10. Qual norma governa as licitações públicas no Brasil?**  
a) Lei nº 14.133/2021  
b) Lei nº 8.666/1993  
c) Lei nº 12.527/2011  
d) Lei nº 9.610/1998

**11. Em PHP, qual é o operador de espaçonave?**  
a) `<=>`  
b) `==`  
c) `===`  
d) `->`

**12. No Laravel, qual é a função do middleware?**  
a) Filtrar requisições HTTP.  
b) Definir rotas da aplicação.  
c) Criar modelos de banco de dados.  
d) Gerar views.

**13. No .NET, qual método é usado para definir uma rota em um controlador Web API?**  
a) `[HttpGet]`  
b) `[Route]`  
c) `[Endpoint]`  
d) `[Url]`

**14. Em SQL, qual comando é usado para atualizar registros em uma tabela?**  
a) `UPDATE`  
b) `MODIFY`  
c) `ALTER`  
d) `CHANGE`

**15. Qual serviço da Azure é usado para executar containers?**  
a) Azure Container Instances  
b) Azure Virtual Machines  
c) Azure App Service  
d) Azure Functions

**16. Em DevOps, qual ferramenta é usada para automação de build?**  
a) Jenkins  
b) Docker  
c) Kubernetes  
d) Terraform

**17. No Git, qual comando desfaz alterações não commitadas?**  
a) `git restore`  
b) `git undo`  
c) `git reset`  
d) `git revert`

**18. Qual é o princípio de segurança que garante que apenas usuários autorizados acessem recursos?**  
a) Confidencialidade  
b) Integridade  
c) Disponibilidade  
d) Autenticidade

**19. Em engenharia de software, o que é um "caso de uso"?**  
a) Uma descrição de como o sistema interage com atores para atingir um objetivo.  
b) Um diagrama de classes do sistema.  
c) Um requisito não funcional.  
d) Um teste de unidade.

**20. Qual é o valor máximo para dispensa de licitação para obras e serviços de engenharia?**  
a) R$ 220.000,00  
b) R$ 88.000,00  
c) R$ 150.000,00  
d) R$ 500.000,00

**21. Em PHP, qual superglobal contém dados de formulários enviados via POST?**  
a) `$_POST`  
b) `$_GET`  
c) `$_REQUEST`  
d) `$_FORM`

**22. No Laravel, qual comando é usado para criar uma migration?**  
a) `php artisan make:migration`  
b) `php artisan create:migration`  
c) `php artisan generate:migration`  
d) `php artisan new:migration`

**23. No .NET, qual é o método padrão para lidar com requisições GET em um controlador MVC?**  
a) `Index()`  
b) `Get()`  
c) `Get()`  
d) `View()`

**24. Em SQL, qual função agrega valores para calcular a média?**  
a) `AVG()`  
b) `SUM()`  
c) `COUNT()`  
d) `MAX()`

**25. Qual serviço AWS é um banco de dados relacional gerenciado?**  
a) Amazon RDS  
b) Amazon DynamoDB  
c) Amazon Redshift  
d) Amazon S3

**26. Em DevOps, qual é a prática de gerenciar configurações como código?**  
a) Infrastructure as Code (IaC)  
b) Continuous Integration  
c) Continuous Deployment  
d) Monitoring as Code

**27. No Git, qual comando lista o histórico de commits?**  
a) `git log`  
b) `git history`  
c) `git list`  
d) `git show`

**28. Qual ataque explora vulnerabilidades de entrada não validadas?**  
a) SQL Injection  
b) DDoS  
c) Phishing  
d) Ransomware

**29. O que é um "requisito não funcional"?**  
a) Uma característica de qualidade do sistema.  
b) Uma funcionalidade específica do usuário.  
c) Um caso de uso.  
d) Uma regra de negócio.

**30. Qual modalidade de licitação é usada para compras de baixo valor?**  
a) Dispensa de licitação  
b) Concorrência  
c) Tomada de preços  
d) Pregão

**31. Em PHP, como você define uma constante?**  
a) `define("CONSTANTE", valor);`  
b) `const CONSTANTE = valor;`  
c) Ambas estão corretas.  
d) Nenhuma das anteriores.

**32. No Laravel, qual facade é usada para enviar e-mails?**  
a) `Mail`  
b) `Email`  
c) `SendMail`  
d) `Message`

**33. No .NET, qual é a interface usada para injeção de dependência?**  
a) `IServiceProvider`  
b) `IServiceCollection`  
c) `IDependencyInjection`  
d) `IServiceScope`

**34. Em SQL, qual comando remove um registro de uma tabela?**  
a) `DELETE`  
b) `REMOVE`  
c) `DROP`  
d) `ERASE`

**35. Qual serviço Azure é usado para hospedar aplicações .NET?**  
a) Azure App Service  
b) Azure Virtual Machines  
c) Azure Container Instances  
d) Azure Functions

**36. Em DevOps, qual ferramenta é usada para orquestração de containers?**  
a) Kubernetes  
b) Docker  
c) Jenkins  
d) Ansible

**37. No Git, qual comando mescla uma branch à branch atual?**  
a) `git merge`  
b) `git combine`  
c) `git join`  
d) `git integrate`

**38. Qual protocolo é usado para comunicação segura na web?**  
a) HTTPS  
b) HTTP  
c) FTP  
d) SMTP

**39. O que é um "diagrama de sequência"?**  
a) Um diagrama que mostra a interação entre objetos ao longo do tempo.  
b) Um diagrama de classes do sistema.  
c) Um diagrama de estados.  
d) Um diagrama de atividades.

**40. Qual é o prazo mínimo para convocação na modalidade concurso?**  
a) 45 dias  
b) 30 dias  
c) 60 dias  
d) 15 dias

**41. Em PHP, qual função retorna o tamanho de uma string?**  
a) `strlen()`  
b) `count()`  
c) `size()`  
d) `length()`

**42. No Laravel, qual comando executa as migrations?**  
a) `php artisan migrate`  
b) `php artisan run:migration`  
c) `php artisan db:migrate`  
d) `php artisan migration:run`

**43. No .NET, qual atributo é usado para validar modelos?**  
a) `[Required]`  
b) `[Validate]`  
c) `[Check]`  
d) `[Validation]`

**44. Em SQL, qual comando altera a estrutura de uma tabela?**  
a) `ALTER TABLE`  
b) `MODIFY TABLE`  
c) `CHANGE TABLE`  
d) `UPDATE TABLE`

**45. Qual serviço AWS é usado para computação sem servidor?**  
a) AWS Lambda  
b) Amazon EC2  
c) Amazon S3  
d) Amazon RDS

**46. Em DevOps, qual ferramenta é usada para versionamento de código?**  
a) Git  
b) Jenkins  
c) Docker  
d) Kubernetes

**47. No Git, qual comando descarta alterações locais?**  
a) `git checkout -- .`  
b) `git undo changes`  
c) `git discard`  
d) `git reset --hard`

**48. Qual é o princípio de segurança que garante que os recursos estejam acessíveis?**  
a) Disponibilidade  
b) Confidencialidade  
c) Integridade  
d) Autenticidade

**49. O que é um "protótipo de baixa fidelidade"?**  
a) Um rascunho não interativo da interface.  
b) Um diagrama de classes.  
c) Um caso de uso detalhado.  
d) Um teste de usabilidade.

**50. Qual modalidade de licitação é eletrônica?**  
a) Pregão  
b) Concorrência  
c) Tomada de preços  
d) Convite

**51. Em PHP, qual função ordena um array em ordem decrescente?**  
a) `rsort()`  
b) `sort()`  
c) `asort()`  
d) `ksort()`

**52. No Laravel, qual facade é usada para autenticação?**  
a) `Auth`  
b) `Authentication`  
c) `User`  
d) `Login`

**53. No .NET, qual método é assíncrono?**  
a) `async Task`  
b) `void`  
c) `static`  
d) `public`

**54. Em SQL, qual comando cria um índice em uma tabela?**  
a) `CREATE INDEX`  
b) `ADD INDEX`  
c) `MAKE INDEX`  
d) `INDEX CREATE`

**55. Qual serviço Azure é um banco de dados NoSQL?**  
a) Azure Cosmos DB  
b) Azure SQL Database  
c) Azure Database for MySQL  
d) Azure Database for PostgreSQL

**56. Em DevOps, qual ferramenta é usada para gerenciar infraestrutura?**  
a) Terraform  
b) Jenkins  
c) Docker  
d) Kubernetes

**57. No Git, qual comando altera a mensagem do último commit?**  
a) `git commit --amend`  
b) `git change commit`  
c) `git edit commit`  
d) `git modify commit`

**58. Qual ataque envolve o envio de e-mails falsos?**  
a) Phishing  
b) SQL Injection  
c) DDoS  
d) Ransomware

**59. O que é um "teste de unidade"?**  
a) Um teste que verifica uma unidade de código isoladamente.  
b) Um teste de integração entre módulos.  
c) Um teste de desempenho.  
d) Um teste de usabilidade.

**60. Qual é o valor máximo para dispensa de licitação para outras compras e serviços?**  
a) R$ 88.000,00  
b) R$ 220.000,00  
c) R$ 150.000,00  
d) R$ 500.000,00

**61. Em PHP, qual função remove espaços em branco no início e fim de uma string?**  
a) `trim()`  
b) `strip()`  
c) `clean()`  
d) `removeSpace()`

**62. No Laravel, qual comando cria um novo modelo?**  
a) `php artisan make:model`  
b) `php artisan create:model`  
c) `php artisan new:model`  
d) `php artisan generate:model`

**63. No .NET, qual é o container de injeção de dependência?**  
a) `IServiceCollection`  
b) `IServiceProvider`  
c) `IDependencyContainer`  
d) `IServiceContainer`

**64. Em SQL, qual comando retorna valores distintos?**  
a) `SELECT DISTINCT`  
b) `SELECT UNIQUE`  
c) `SELECT DIFFERENT`  
d) `SELECT ONLY`

**65. Qual serviço AWS é usado para monitoramento?**  
a) Amazon CloudWatch  
b) Amazon S3  
c) Amazon RDS  
d) Amazon EC2

**66. Em DevOps, qual prática integra código frequentemente?**  
a) Continuous Integration  
b) Continuous Deployment  
c) Infrastructure as Code  
d) Monitoring

**67. No Git, qual comando mostra as diferenças entre commits?**  
a) `git diff`  
b) `git show diff`  
c) `git changes`  
d) `git compare`

**68. Qual protocolo criptografa dados em trânsito?**  
a) TLS  
b) HTTP  
c) FTP  
d) SMTP

**69. O que é um "teste de integração"?**  
a) Um teste que verifica a interação entre módulos.  
b) Um teste de unidade.  
c) Um teste de desempenho.  
d) Um teste de usabilidade.

**70. Qual modalidade de licitação é usada para compras de valores altos?**  
a) Concorrência  
b) Dispensa de licitação  
c) Tomada de preços  
d) Convite

**71. Em PHP, qual função converte um array em JSON?**  
a) `json_encode()`  
b) `json_convert()`  
c) `array_to_json()`  
d) `encode_json()`

**72. No Laravel, qual comando inicia um servidor local?**  
a) `php artisan serve`  
b) `php artisan start`  
c) `php artisan run`  
d) `php artisan local`

**73. No .NET, qual é o método para retornar um status HTTP 200?**  
a) `Ok()`  
b) `Success()`  
c) `Good()`  
d) `Ok200()`

**74. Em SQL, qual comando agrupa registros?**  
a) `GROUP BY`  
b) `ORDER BY`  
c) `SORT BY`  
d) `ARRANGE BY`

**75. Qual serviço Azure é usado para CDN?**  
a) Azure CDN  
b) Azure Blob Storage  
c) Azure Front Door  
d) Azure Traffic Manager

**76. Em DevOps, qual ferramenta é usada para automação de testes?**  
a) Selenium  
b) Jenkins  
c) Docker  
d) Kubernetes

**77. No Git, qual comando clona um repositório?**  
a) `git clone`  
b) `git copy`  
c) `git download`  
d) `git pull`

**78. Qual é o princípio de segurança que garante que os dados não sejam alterados?**  
a) Integridade  
b) Confidencialidade  
c) Disponibilidade  
d) Autenticidade

**79. O que é um "teste de regressão"?**  
a) Um teste que verifica se novas alterações quebraram funcionalidades existentes.  
b) Um teste de unidade.  
c) Um teste de desempenho.  
d) Um teste de usabilidade.

**80. Qual é o prazo mínimo para convocação na modalidade pregão?**  
a) 8 dias  
b) 15 dias  
c) 30 dias  
d) 45 dias

**81. Em PHP, qual função retorna a data atual?**  
a) `date()`  
b) `now()`  
c) `current_date()`  
d) `getdate()`

**82. No Laravel, qual facade é usada para cache?**  
a) `Cache`  
b) `Storage`  
c) `Session`  
d) `Cookie`

**83. No .NET, qual é a classe base para controladores MVC?**  
a) `Controller`  
b) `ControllerBase`  
c) `MvcController`  
d) `BaseController`

**84. Em SQL, qual comando calcula o número de registros?**  
a) `COUNT()`  
b) `SUM()`  
c) `AVG()`  
d) `TOTAL()`

**85. Qual serviço AWS é usado para entrega de conteúdo?**  
a) Amazon CloudFront  
b) Amazon S3  
c) Amazon RDS  
d) Amazon EC2

**86. Em DevOps, qual ferramenta é usada para integração contínua?**  
a) Jenkins  
b) Docker  
c) Kubernetes  
d) Terraform

**87. No Git, qual comando adiciona alterações ao staging?**  
a) `git add`  
b) `git stage`  
c) `git commit`  
d) `git push`

**88. Qual ataque sobrecarrega um servidor com tráfego?**  
a) DDoS  
b) SQL Injection  
c) Phishing  
d) Ransomware

**89. O que é um "teste de desempenho"?**  
a) Um teste que mede o tempo de resposta do sistema.  
b) Um teste de unidade.  
c) Um teste de integração.  
d) Um teste de usabilidade.

**90. Qual modalidade de licitação é usada para serviços técnicos especializados?**  
a) Concurso  
b) Pregão  
c) Tomada de preços  
d) Convite

**91. Em PHP, qual função abre um arquivo para leitura?**  
a) `fopen()`  
b) `open_file()`  
c) `file_open()`  
d) `read_file()`

**92. No Laravel, qual comando cria um novo middleware?**  
a) `php artisan make:middleware`  
b) `php artisan create:middleware`  
c) `php artisan new:middleware`  
d) `php artisan generate:middleware`

**93. No .NET, qual é a interface para logging?**  
a) `ILogger`  
b) `ILog`  
c) `Logger`  
d) `Logging`

**94. Em SQL, qual comando remove uma tabela?**  
a) `DROP TABLE`  
b) `DELETE TABLE`  
c) `REMOVE TABLE`  
d) `ERASE TABLE`

**95. Qual serviço Azure é usado para máquinas virtuais?**  
a) Azure Virtual Machines  
b) Azure App Service  
c) Azure Functions  
d) Azure Container Instances

**96. Em DevOps, qual ferramenta é usada para containers?**  
a) Docker  
b) Jenkins  
c) Kubernetes  
d) Terraform

**97. No Git, qual comando atualiza o repositório local?**  
a) `git pull`  
b) `git fetch`  
c) `git update`  
d) `git sync`

**98. Qual é o princípio de segurança que verifica a identidade?**  
a) Autenticação  
b) Autorização  
c) Confidencialidade  
d) Integridade

**99. O que é um "teste de usabilidade"?**  
a) Um teste que avalia a experiência do usuário.  
b) Um teste de unidade.  
c) Um teste de integração.  
d) Um teste de desempenho.

**100. Qual é o valor máximo para tomada de preços para obras e serviços de engenharia?**  
a) R$ 3.300.000,00  
b) R$ 1.430.000,00  
c) R$ 220.000,00  
d) R$ 88.000,00

---