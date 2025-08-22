
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