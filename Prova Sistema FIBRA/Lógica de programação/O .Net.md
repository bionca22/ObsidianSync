A .NET é uma plataforma de desenvolvimento **open-source**, **cross-platform** e moderna da Microsoft, que permite construir diversos tipos de aplicações.

#### ➡️**Arquitetura e Componentes Principais**

📌  **.NET Runtimes**

- **CLR (Common Language Runtime)**:
    
    - "Máquina virtual" que executa código .NET
        
    - Responsável por: Gerenciamento de memória (Garbage Collection), Segurança, JIT Compilation
        
- **CoreCLR**: Runtime do .NET Core (cross-platform). É a **implementação moderna e oficial** do CLR. Tem como foco **performance, modularidade e portabilidade**.
    
- **Mono**: Runtime alternativo (usado em Xamarin para mobile). Foi muito usado para levar aplicações .NET para **Linux, macOS, iOS e Android**, numa época em que o .NET era restrito ao Windows. Ainda é usado em alguns cenários, como **Unity** (motor de jogos) e aplicações móveis mais antigas.

-  **Garbage Collection:** (Coleta de Lixo) no .NET é um processo automatizado de gerenciamento de memória que libera o espaço de objetos que não estão mais sendo utilizados pela aplicação. Em outras palavras, ele identifica e remove objetos que não possuem mais referências, evitando vazamentos de memória e otimizando o uso dos recursos.


📌  **Linguagens Suportadas**

- **C#** (Principal e mais popular)
    
- **F#** (Funcional)
    
- **VB.NET** (Visual Basic .NET)

📌  **Compilação**

1. **Compilação para IL (Intermediate Language)**: Código fonte → IL (.dll ou .exe)
    
2.  CLR -> usa o componente **JIT (Just-In-Time compiler)** para converter o IL em **código de máquina nativo** -> O código nativo é então executado pelo sistema operacional.

3. em alguns casos pode rodar em **AOT (Ahead-Of-Time)**, gerando código nativo já na compilação (muito usado em mobile).
	[[apend. .NET]]

####  ➡️**Principais "Flavors" do .NET**

a) .NET Framework** (Legado, Windows-only)

- Versão original
    
- Executa apenas no Windows
    
- Estável, mas em modo de manutenção

**b) .NET Core** (Moderno, Cross-Platform)

- Base do .NET 5+
    
- Executa em Windows, Linux, macOS
    
- Modular e de alto desempenho
    
- Foco em nuvem e containers

**c) .NET 5/6/7/8+** (Unificação)

- Unificação do .NET Framework, .NET Core e Xamarin
    
- **NET 6+**: Foco em produtividade e performance
    
- **LTS (Long-Term Support)**: Versões com suporte estendido

 **d) .NET Standard** (Especificação de APIs)

- Define um conjunto de APIs que todas as implementações .NET devem seguir
    
- Garante compatibilidade entre diferentes flavors

 ➡️ **Ecossistema e Ferramentas**

 📌**SDKs**
- **.NET SDK**: Ferramentas de linha de comando (dotnet CLI)
    
- Comandos principais:
    
    - `dotnet new`: Cria novo projeto
        
    - `dotnet build`: Compila o projeto
        
    - `dotnet run`: Executa o projeto
        
    - `dotnet test`: Executa testes
        
    - `dotnet publish`: Publica para produção
        

📌 **IDEs e Editores**

- **Visual Studio** (Windows, completo)
    
- **Visual Studio Code** (Cross-platform, leve)
    
- **Rider** (JetBrains, cross-platform)
    

📌**Gerenciamento de Pacotes**

- **NuGet**: Gerenciador de pacotes oficial
    
- Repositório central de bibliotecas .NET


➡️**Principais Tipos de Aplicações**

📌**Web**

- **ASP.NET Core**: Framework web moderno
    
    - **MVC** (Model-View-Controller)
        
    - **Web API** (APIs RESTful)
        
    - **Razor Pages** (Páginas com código C# embutido no HTML.)
        
    - **Blazor** (Web assembly - C# no browser)
        
    - **SignalR** (Comunicação em tempo real real entre servidor e cliente)
[[apend. .NET]]

#### 📌** Desktop**

- **WinForms** (Legado, Windows)
    
- **WPF (Windows Presentation Foundation)** (Windows, XAML)
    
- **Windows Forms** (.NET 6+ cross-platform preview)
    
- **Avalonia** (Cross-platform, community)
    
- **MAUI** (Multi-platform App UI)
    

#### 📌** Mobile**

- **Xamarin** (Legado)
    
- **.NET MAUI** (Sucessor do Xamarin, cross-platform)
    

#### 📌**Cloud e Microserviços**

- Integração nativa com Azure
    
- **Docker** e containers
    
- **Kubernetes** orchestration
    

##### 📌Outros

- **Console Applications**
    
- **Windows Services**
    
- **Machine Learning** (ML.NET). Permite treinar, construir e enviar modelos de machine learning personalizados usando C# ou F# em vários cenários de ML
    
- **IoT** (Internet of Things)
    
- **Games** (Unity usa C#)

##### **📌 Async/Await**

- Programaçāo assíncrona simplificada
    
- Não bloqueia threads
    
- Melhora escalabilidade

**Exemplo:**
```PHP
public async Task<string> GetDataAsync()
{
    return await httpClient.GetStringAsync("url");
}
```


##### 📌 LINQ (Language Integrated Query)

- Ele atua como um "tradutor" entre a linguagem de programação e o banco de dados, permitindo que os desenvolvedores trabalhem com objetos em vez de escrever consultas SQL diretamente.

- Consultas integradas à linguagem
    
- Syntax de consulta unificada para diferentes fontes


#####  📌Dependency Injection

- É um padrão de projeto de software que permite que classes recebam suas dependências de fontes externas, em vez de criá-las dentro da própria classe.

- Padrão embutido no ASP.NET Core
    
- Inversāo de controle
    
- Facilita testes e manutenção

❕Existem três formas principais de injetar dependências no .NET:

- **[Injeção via Construtor](https://www.google.com/search?sca_esv=63ad467223b51100&cs=1&sxsrf=AE3TifNknT_SNlNsEhcOo8lOtZQwy6RSMQ%3A1755633767908&q=Inje%C3%A7%C3%A3o+via+Construtor&sa=X&ved=2ahUKEwippJy41ZePAxVdrZUCHSIdDSUQxccNegQIDhAB&mstk=AUtExfARnflT0R-Vb0DTHARpCS--U3SO5FShfH6EmHViVC9Hm-t8xF36HrOcr6P0sJQsdYnfrAssNx8XWY80wdPj0l9J12jR13nl1X2hAb23f7wQ90xSGK_769yYyCNlYD_l2GFDIgY5LOEYHZ5V-0PmeekZxvYB_JUSV1xRy-JDacJDUVG4vQeE2D6YoQBFbXEVWIXjvrL9AVFBEziKh8R1Ng6RtDWJxQl_Iue9qaGFTuZfAwIM3G803Ur-jmN22H7MYwV38a_3VgKV5_i04rdwczPl&csui=3):** As dependências são fornecidas através do construtor da classe. 
- **[Injeção via Propriedade](https://www.google.com/search?sca_esv=63ad467223b51100&cs=1&sxsrf=AE3TifNknT_SNlNsEhcOo8lOtZQwy6RSMQ%3A1755633767908&q=Inje%C3%A7%C3%A3o+via+Propriedade&sa=X&ved=2ahUKEwippJy41ZePAxVdrZUCHSIdDSUQxccNegQIDxAB&mstk=AUtExfARnflT0R-Vb0DTHARpCS--U3SO5FShfH6EmHViVC9Hm-t8xF36HrOcr6P0sJQsdYnfrAssNx8XWY80wdPj0l9J12jR13nl1X2hAb23f7wQ90xSGK_769yYyCNlYD_l2GFDIgY5LOEYHZ5V-0PmeekZxvYB_JUSV1xRy-JDacJDUVG4vQeE2D6YoQBFbXEVWIXjvrL9AVFBEziKh8R1Ng6RtDWJxQl_Iue9qaGFTuZfAwIM3G803Ur-jmN22H7MYwV38a_3VgKV5_i04rdwczPl&csui=3):** As dependências são injetadas através de propriedades da classe. 
- **[Injeção via Método](https://www.google.com/search?sca_esv=63ad467223b51100&cs=1&sxsrf=AE3TifNknT_SNlNsEhcOo8lOtZQwy6RSMQ%3A1755633767908&q=Inje%C3%A7%C3%A3o+via+M%C3%A9todo&sa=X&ved=2ahUKEwippJy41ZePAxVdrZUCHSIdDSUQxccNegQIHRAB&mstk=AUtExfARnflT0R-Vb0DTHARpCS--U3SO5FShfH6EmHViVC9Hm-t8xF36HrOcr6P0sJQsdYnfrAssNx8XWY80wdPj0l9J12jR13nl1X2hAb23f7wQ90xSGK_769yYyCNlYD_l2GFDIgY5LOEYHZ5V-0PmeekZxvYB_JUSV1xRy-JDacJDUVG4vQeE2D6YoQBFbXEVWIXjvrL9AVFBEziKh8R1Ng6RtDWJxQl_Iue9qaGFTuZfAwIM3G803Ur-jmN22H7MYwV38a_3VgKV5_i04rdwczPl&csui=3):** As dependências são injetadas através de parâmetros de método.

```PHP
services.AddScoped<IUserService, UserService>();
```

#####  ➡️Performance e Otimização

##### 📌 Span<T> e Memory<T>

	- Acesso seguro a memória
    
	- Zero allocations
    
	- Alto desempenho

### 📌 Value Types

- struct ao invés de class
    
- Menos pressure no GC
    
- Stack allocation
    

 📌 ** Benchmarking**

- **BenchmarkDotNet**: Biblioteca para medição de performance
    
- Análise precisa de desempenho

 
➡️Segurança

📌 Autenticação e Autorização**

- **ASP.NET Core Identity**: Sistema de identidade
    
- **JWT Tokens**: APIs stateless
    
- **OAuth 2.0 / OpenID Connect**
    

📌 Data Protection**

- Criptografia de dados sensíveis
    
- Proteção contra XSS, CSRF
    

📌Secure Coding**

- Validação de input
    
- Parameterized queries (SQL injection prevention)
    

---

➡️8. DevOps e Deploy**

📌CI/CD Integration**

- GitHub Actions
    
- Azure DevOps
    
- Jenkins
    

📌 Containers**

- Docker support nativo
    
- Kubernetes orchestration
    

📌Cloud Deployment**

- Azure App Service
    
- AWS Elastic Beanstalk
    
- Self-hosted
    

---

Tendencias e Futuro**

📌.NET 9+**

- Maior performance
    
- Novas APIs
    
- Melhorias no AOT
    

📌 Cloud Native**

- Microservices
    
- Serverless (Azure Functions)
    
- Service mesh
    

📌AI Integration**

- ML.NET
    
- Azure AI integration
    
- Semantic Kernel










