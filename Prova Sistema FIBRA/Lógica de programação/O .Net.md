A .NET é uma plataforma de desenvolvimento **open-source**, **cross-platform** e moderna da Microsoft, que permite construir diversos tipos de aplicações.

#### ➡️**Arquitetura e Componentes Principais**

📌  **.NET Runtimes**

- **CLR (Common Language Runtime)**:
    
    - "Máquina virtual" que executa código .NET
        
    - Responsável por: Gerenciamento de memória (Garbage Collection), Segurança, JIT Compilation
        
- **CoreCLR**: Runtime do .NET Core (moderno, cross-platform)
    
- **Mono**: Runtime alternativo (usado em Xamarin para mobile)


📌  **Linguagens Suportadas**

- **C#** (Principal e mais popular)
    
- **F#** (Funcional)
    
- **VB.NET** (Visual Basic .NET)

📌  **Compilação**

1. **Compilação para IL (Intermediate Language)**: Código fonte → IL (.dll ou .exe)
    
2. **JIT Compilation (Just-In-Time)**: IL → Código nativo da máquina durante a execução
    
3. **AOT (Ahead-of-Time)**: Compilação direta para nativo (melhor startup time)