
📌**Listas Ordenadas e Não Ordenadas**
	**Ordenadas:** Uma estrutura de dados onde a sequência dos elementos **não segue nenhuma relação de ordem predefinida** baseada em suas chaves ou valores. A posição de cada elemento é arbitrária e não carrega informação semântica sobre seu valor.
- 
	- **Inserção**: O(1) - Novos elementos são adicionados no início/fim.
	
	- **Busca por elemento**: O(n) - Requer busca sequencial.
	
	-  **Vantagem**: Inserções rápidas e simples
	
	- **Desvantagem**: Buscas ineficientes em grandes conjuntos.	

	**Não Ordenadas:** Estrutura onde os elementos **mantém uma sequência específica** baseada em uma chave de ordenação (numérica, alfabética, etc.). A posição de cada elemento é determinada por sua relação de ordem com os demais.
	
	- **Inserção**: O(n) - Deve encontrar a posição correta
    
	- **Busca por elemento**: O(log n) com busca binária (se acesso aleatório)
    
	- **Vantagem**: Buscas eficientes e travessia ordenada
    
	- **Desvantagem**: Inserções mais custosas


📌**Busca Sequencial (Linear Search)**
 Percorre cada elemento da estrutura (array, lista) sequencialmente, do início ao fim, até encontrar o elemento desejado ou chegar ao final.
    
- **Complexidade**:
    
    - **Pior Caso (O(n))**: O elemento não está presente ou está na última posição. Precisa percorrer todos os `n` elementos.
        
    - **Melhor Caso (Ω(1))**: O elemento está na primeira posição.
        
    - **Caso Médio (Θ(n))**: Em média, precisará percorrer `n/2` elementos.
    
    - - **Espaço**: O(1) - Não utiliza estrutura auxiliar.[[Apend. Algoritmos]]
    


📌 **Busca Binária (Binary Search):** Em vez de verificar um por um, a busca binária divide a lista ao meio. A lista deve estar ordenada.
- 
	-  Compara o elemento do meio com o alvo.

	- Se for igual, retorna.
	
	- Se o alvo for maior, busca na metade direita.
	
	- Se o alvo for menor, busca na metade esquerda.
	
- **Complexidade**:
    
    - **Pior Caso (O(log n))**: O elemento não está presente ou é encontrado na última divisão. O logaritmo é na base 2.
        
    - **Melhor Caso (Ω(1))**: O elemento está exatamente no meio.
        
    - **Caso Médio (Θ(log n))**: Similar ao pior caso.

➡️### **Algoritmos de Ordenação**

📌 **Quicksort**: Ele escolhe um elemento da lista, chamado de **pivô**. Em seguida, ele reorganiza os outros elementos para que todos os menores que o pivô fiquem à sua esquerda, e todos os maiores, à sua direita. O algoritmo então aplica o mesmo processo recursivamente nas sub-listas da esquerda e da direita.

>❕A busca binária é um algoritmo de busca que encontra a localização de um valor específico em uma lista ordenada, enquanto o quicksort é um algoritmo de ordenação que organiza uma lista em ordem crescente ou decrescente. Em resumo, um pesquisa e o outro ordena


📌**Mergesort:**