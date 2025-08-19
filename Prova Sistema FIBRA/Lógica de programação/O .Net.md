A .NET é uma plataforma de desenvolvimento **open-source**, **cross-platform** e moderna da Microsoft, que permite construir diversos tipos de aplicações.

#### ➡️**Arquitetura e Componentes Principais**

📌  **.NET Runtimes**

- **CLR (Common Language Runtime)**:
    
    - "Máquina virtual" que executa código .NET
        
    - Responsável por: Gerenciamento de memória (Garbage Collection), Segurança, JIT Compilation
        
- **CoreCLR**: Runtime do .NET Core (cross-platform). É a **implementação moderna e oficial** do CLR. Tem como foco **performance, modularidade e portabilidade**.
    
- **Mono**: Runtime alternativo (usado em Xamarin para mobile). Foi muito usado para levar aplicações .NET para **Linux, macOS, iOS e Android**, numa época em que o .NET era restrito ao Windows. Ainda é usado em alguns cenários, como **Unity** (motor de jogos) e aplicações móveis mais antigas.


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
        
    - **Razor Pages** (Páginas com código embutido)
        
    - **Blazor** (Web assembly - C# no browser)
        
    - **SignalR** (Comunicação em tempo real)