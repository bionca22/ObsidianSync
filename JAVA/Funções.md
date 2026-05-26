
### HashSet
Para cada número pelo qual ele passa, é salvo o número e qual número falta para completar a requisição.

**"Qual número falta para chegar no meu alvo?"**
- Se o alvo é **7** e você está segurando o **2**, você sabe que o que falta é o **5** (7 - 2 = 5)

---
### Operador Ternário

```Java
return (expressao) ? true : false;
```

Aqui você está dizendo: _"Java, teste essa expressão. Se for verdade, me devolva `true`. Se for mentira, me devolva `false`."_

Ele é útil quando você quer retornar **outras coisas** que não sejam `true` ou `false`. Por exemplo:

```Java
// Se a for 10, retorna a palavra "Ganhou", senão retorna "Perdeu"
return (a == 10) ? "Ganhou" : "Perdeu";
```

---
### Math.abs()

Imagine que o `Math.abs()` olha para o número e pensa assim:

- **O número é negativo?** (Ex: -10). Ele retira o sinal de menos e o torna positivo (10).
    
- **O número já é positivo ou zero?** (Ex: 10 ou 0). Ele não faz nada, deixa como está.

#### Exemplos no código:

```Java
int a = Math.abs(-5);  // O resultado será 5
int b = Math.abs(5);   // O resultado continuará sendo 5
int c = Math.abs(0);   // O resultado será 0
```