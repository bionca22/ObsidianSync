
📍Construtor
- **Invariante de classe**: são regras que sempre precisam ser verdadeiras para um objeto existir de forma "correta".  
    👉 Exemplo: pense em uma classe **ContaBancária**. Uma regra pode ser: _o saldo nunca pode ser negativo_. Essa é uma invariante da classe, porque deve ser válida o tempo todo.
    
- **Inicialização determinística**: significa que, quando você cria um objeto, ele **sempre começa em um estado válido e previsível**, sem depender do acaso ou de deixar campos "soltos".  
    👉 Exemplo: quando você cria uma **ContaBancária**, o saldo começa sempre em 0 ou em um valor informado, nunca indefinido.
----

 📍Encapsulamento
 
➡️ A ideia é que, sem encapsulamento, qualquer código externo poderia mudar os atributos diretamente, quebrando as **regras do objeto** (as invariantes que falamos antes).

### Situação que o texto descreve:

Imagine uma classe **ContaBancária**:

```PHP
class ContaBancaria {
    private double saldo; // atributo encapsulado

    public ContaBancaria(double saldoInicial) {
        this.saldo = saldoInicial;
    }

    // método controlado
    public void depositar(double valor) {
        if (valor > 0) {
            saldo += valor;
        }
    }

    // método controlado
    public void sacar(double valor) {
        if (valor > 0 && valor <= saldo) {
            saldo -= valor;
        }
    }

    public double getSaldo() {
        return saldo;
    }
}

```

Se **saldo** fosse público (`public double saldo;`), qualquer outro código poderia fazer:
```PHP
ContaBancaria c = new ContaBancaria(100);
c.saldo = -999999; // quebra a regra do objeto (saldo não deveria ser negativo!)

```
👉 Com encapsulamento (`private`), o atributo não pode ser alterado livremente; só pelos métodos **depositar** e **sacar**, que já verificam as condições corretas.