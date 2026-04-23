
Operadores 
Símbolos que Solicitam ao compilador realizar alguma operação.


 **Operadores Aritméticos**
 ![[Pasted image 20260423145908.png]]
 
 Existe uma diferença quando adicionado antes ou depois do objeto 
 
``` java
int resultado = 5;

System.out.println(resultado++);// resultado 5
// é a mesma coisa que 
System.out.println(resultado); 
resultado += 1; // ou
resultado = resultado +1;



System.out.println(++resultado); // resultado 6
// é a mesma coisa que
resultado +=1;
System.out.println(resultado);

```

 
 **Operadores Relacionais**
 
 ![[Pasted image 20260423152054.png|584]]

sempre retorna Boolean

 **Operadores Lógicos**

![[Pasted image 20260423153546.png]]
Em programação, curto-circuito ocorre quando operadores lógicos (AND/`&&`, OR/`||`) interrompem a avaliação de uma expressão assim que o resultado final é determinado, sem processar o restante.
==EX:==
**`&&` ou `and`** A expressão só é verdadeira se **ambos** forem verdadeiros. Se o primeiro for `false`, o segundo nem é avaliado, pois o resultado já é `false`

Tabela verdade![[Pasted image 20260423154731.png]]
 
**Operadores Assignment** e Precedência**
 ![[Pasted image 20260423160703.png]] 1. Postfix e Unário (O topo da pirâmide)

Estes agem sobre um único valor por vez e são resolvidos primeiro.

- **Postfix (`expr++`, `expr--`):** Incrementa ou decrementa o valor _depois_ da expressão ser usada.
- **Unário (`++expr`, `--expr`, `+`, `-`, `~`, `!`):** Operadores que alteram o sinal, invertem valores lógicos (como o `!` que transforma verdadeiro em falso) ou incrementam _antes_ do uso.
    
 2. Aritmética Básica

- **Multiplicativo (`*`, `/`, `%`):** Multiplicação, divisão e o resto da divisão (módulo). Têm prioridade sobre a soma.
- **Aditivo (`+`, `-`):** Soma e subtração.
    
 3. Shift (Deslocamento de Bits)
 
- **`<<`, `>>`, `>>>`:** Usados em manipulação de baixo nível para mover os bits de um número para a esquerda ou direita. É uma forma técnica de multiplicar ou dividir por potências de 2.

 4. Relacional e Igualdade (Comparações)

- **Relacional (`<`, `>`, `<=`, `>=`, `instanceof`):** Verificam se um valor é maior, menor ou se um objeto pertence a uma classe.
- **Igualdade (`==`, `!=`):** Verifica se dois valores são iguais ou diferentes. Note que eles vêm _depois_ dos relacionais.
    

5. Operadores Bitwise (Bit a Bit)

Estes comparam cada bit individual de dois números:

- **AND (`&`)**: "1" se ambos os bits forem 1.
- **XOR (`^`)**: "1" se os bits forem diferentes.
- **OR (`|`)**: "1" se pelo menos um dos bits for 1.

 6. Lógicos (Curto-circuito)

Muito usados em condicionais (`if`):
- **Lógico AND (`&&`):** Só é verdadeiro se ambos os lados forem verdadeiros.
- **Lógico OR (`||`):** É verdadeiro se pelo menos um dos lados for verdadeiro.

> **Dica:** O `&&` sempre é avaliado antes do `||`.

 7. Ternário (`? :`)

É um "if-else" de uma linha só.
- Exemplo: `(condição) ? valor_se_verdade : valor_se_falso;`
    

8. Assignment (Atribuição)

É o último da lista. Isso garante que todo o cálculo à direita seja resolvido antes de o resultado ser guardado na variável.
- Inclui as formas contraídas como `+=` (soma e atribui) ou `*=` (multiplica e atribui).