#### ➡️**Classes e Objetos**

- 📌 **Classe**:  
    Modelo abstrato que define a estrutura e comportamento de entidades. É um modelo que especifica: Atributos (dados)  Métodos (operações). 
	    ❕**Exemplo:** `class Carro { ... }`

	- **Entidade:** é um objeto ou conceito do mundo real sobre o qual se deseja armazenar informações.
	
	- **Atributo:** é uma propriedade ou característica que descreve uma entidade.
		❕**Exemplo:** `public $cor;` dentro da classe `Carro`.
	
    - **Método:** São os **comportamentos** ou ações que um objeto pode realizar. Em PHP, são funções definidas dentro da classe.
	    ❕**Exemplo:** `public function ligar() { ... }` dentro da classe `Carro`.
    
    - A Classe Não ocupa memória até ser instanciada.

 -  📌**Objeto**:  
    Instância concreta de uma classe. Possui: atributos (ou propriedade ), Comportamento (métodos). 
    
    - Identidade única
    
	**Exemplo:** `$meuCarro = new Carro();`


	**Teoria**: Classes são _tipos de dados definidos pelo usuário_. Objetos são _entidades de tempo de execução_ que interagem entre si.

- 📌**Construtor**
	Método especial invocado automaticamente na instanciação. Ele é usado para configurar o objeto, como atribuir valores iniciais aos seus atributos ou executar outras tarefas necessárias para preparar o objeto para uso. Responsável por:
	
	- Inicializar atributos
    
	- Validar parâmetros
    
	- Garantir estado válido do objeto

	**Teoria**: Garante a _invariante de classe_ (condições que sempre devem ser verdadeiras para o objeto), implementa _inicialização determinística_

	-  Atribuir valores iniciais aos atributos do objeto. 
	- Conectar-se a um banco de dados. 
	- Abrir um arquivo. 
	- Validar dados de entrada.

	**Exemplo:**
	`public function __construct($cor, $modelo) { 
	`$this->cor = $cor;`
	`$this->modelo = $modelo; }`

#### ➡️Pilares da POO

 📌**Encapsulamento**

Princípio de ocultação de detalhes de implementação. Ele **esconder os detalhes internos** de um objeto e controlar o acesso aos seus dados. Garante:

- _Proteção de consistência_: Atributos são modificados apenas por métodos controlados
    
- _Baixo acoplamento_: Alterações internas não afetam consumidores externos
    
- _Interface vs. Implementação_: Separa _o que faz_ de _como faz_

Ele protege os atributos de serem modificados por um código externo de forma inesperada. O encapsulamento é gerenciado pelos **modificadores de acesso**:

 - **`public`**: O atributo ou método é acessível de qualquer lugar.
    
- **`private`**: O atributo ou método é acessível apenas dentro da própria classe.
    
- **`protected`**: O atributo ou método é acessível dentro da classe e por classes que herdam dela (classes filhas).

Uma classe abstrata pode definir métodos que são declarados, mas não implementados. Isso força as subclasses a fornecerem suas próprias implementações, enquanto o usuário da classe interage apenas com a interface definida pela classe abstrata.

- **Exemplo:**
    Em uma classe "Conta", o saldo seria um atributo encapsulado. O acesso ao saldo seria controlado por métodos como "depositar" e "sacar", que modificam o valor do saldo de forma segura e controlada, em vez de permitir acesso direto.


📌**Abstração**

Modelagem de conceitos essenciais, omitindo detalhes irrelevantes:

- **Classes abstratas**:
    - Não podem ser instanciadas
        
    - Podem conter métodos abstratos (que não têm implementação e devem ser implementados pelas classes filhas) e métodos concretos.
        
- **Interfaces**:
    - Contratos que definem _o que_ deve ser implementado
        
    - Sem implementação ou estado
        
- **Teoria**:
    
    - _Redução de complexidade_: Foco em aspectos relevantes
        
    - _Especificação de contratos_: Separa obrigação de implementação
        
    - _Inversão de dependência_: Classes dependem de abstrações, não de implementações