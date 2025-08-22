
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
11. c) Definir múltiplas rotas RESTful para um  controlador, excluindo as rotas `create` e `edit`. X
12. d) Todas as alternativas acima estão corretas.
13. b) Aplicar um middleware a todas as rotas dentro do grupo, exigindo autenticação para acessá-las.
14. d) `Token: <token>`
15. d) `php artisan passport:generate-keys`


Laravel Sanctum é o pacote é mais indicado para uma API simples onde seu próprio frontend consome os dados, sem a complexidade do OAuth2. O Sanctum é mais leve e simples para tokens de API simples.

métodos 
- `where` : Adiciona uma condição de validação para um parâmetro de rota.
- `name`: Permitir a geração de URLs e redirecionamentos de forma dinâmica.
- `apiResource`: 

rotas
- `routes/api.php` é para rotas de API (stateless), e `routes/web.php` é para rotas web tradicionais.
- `php artisan route:list` : Lista todas as rotas, seus verbos, URIs, nomes e ações.
- `/oauth/token` : Esta é a rota padrão para o fluxo "password grant" do OAuth2.
- `Passport::routes()`

Passport
- `use HasApiTokens;` : Este trait é fornecido pelo Passport para gerenciar tokens.
- `middleware('auth:api')`: O guard `api` configurado para usar o Passport é acionado.