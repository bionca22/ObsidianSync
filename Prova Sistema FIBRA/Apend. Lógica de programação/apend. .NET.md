
 📌**Conceito IL (Intermediate Language)**

Quando você escreve um programa em uma linguagem como **C#** (ou outra da plataforma .NET), o código **não é convertido diretamente em código de máquina** do processador.  
Em vez disso, ele é **compilado para uma linguagem intermediária**, chamada **IL (Intermediate Language)**.

❕**Como funciona na prática**

1. **Código-fonte (C# por exemplo):**  
    Você escreve o programa.
    
2. **Compilação para IL:**  
    O compilador transforma esse código em **IL**, que é um conjunto de instruções de baixo nível, mas ainda independentes do processador.  
    👉 Esse IL fica armazenado em arquivos `.exe` ou `.dll`.
    
3. **Execução pela CLR (Common Language Runtime):**  
    Quando você roda o programa, o IL não é executado diretamente.  
    Ele passa por outro passo chamado **JIT (Just-In-Time compilation)**, que traduz o IL para **código de máquina nativo**, específico do processador onde o programa está rodando.
    

---

❕ **Por que usar IL?**

- **Portabilidade:** o mesmo programa em IL pode rodar em diferentes sistemas e processadores (desde que tenham o .NET/CLR).
    
- **Segurança e otimização:** a CLR pode analisar e otimizar o código antes de transformar em código de máquina.
    
- **Interoperabilidade:** diferentes linguagens (C#, VB.NET, F#, etc.) podem ser compiladas para IL e trabalhar juntas, porque todas compartilham essa linguagem intermediária.