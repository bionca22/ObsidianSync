
📌**Listas Ordenadas e Não Ordenadas**
	- **Ordenadas:** Uma estrutura de dados onde a sequência dos elementos **não segue nenhuma relação de ordem predefinida** baseada em suas chaves ou valores. A posição de cada elemento é arbitrária e não carrega informação semântica sobre seu valor.
		-**Inserção**: O(1) - Novos elementos são adicionados no início/fim.
		- 
		 - **Busca por elemento**: O(n) - Requer busca sequencial.
		 - 
		 - **Vantagem**: Inserções rápidas e simples.
		 - 
		 - **Desvantagem**: Buscas ineficientes em grandes conjuntos


📌**Busca Sequencial (Linear Search)**
 Percorre cada elemento da estrutura (array, lista) sequencialmente, do início ao fim, até encontrar o elemento desejado ou chegar ao final.
    
- **Complexidade**:
    
    - **Pior Caso (O(n))**: O elemento não está presente ou está na última posição. Precisa percorrer todos os `n` elementos.
        
    - **Melhor Caso (Ω(1))**: O elemento está na primeira posição.
        
    - **Caso Médio (Θ(n))**: Em média, precisará percorrer `n/2` elementos.
    
    - - **Espaço**: O(1) - Não utiliza estrutura auxiliar.[[Apend. Algoritmos]]
    


📌 Busca Binária (Binary Search)