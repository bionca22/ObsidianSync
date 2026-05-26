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

	**Teoria**: Garante a _invariante de classe_ (condições que sempre devem ser verdadeiras para o objeto), implementa _inicialização determinística_ [[apend. PHP & POO]]

	-  Atribuir valores iniciais aos atributos do objeto. 
	- Conectar-se a um banco de dados. 
	- Abrir um arquivo. 
	- Validar dados de entrada.

	**Exemplo:**
	```PHP
	class Point {  
		protected int $x;  
		protected int $y;  
  
		public function __construct(int $x, int $y = 0) {  
		$this->x = $x;  
		$this->y = $y;  
	}  
}
	```

#### ➡️Pilares da POO

 📌**Encapsulamento**

Princípio de ocultação de detalhes de implementação. Ele **esconder os detalhes internos** de um objeto e controlar o acesso aos seus dados. Garante:

- _Proteção de consistência_: Atributos são modificados apenas por métodos controlados
    
- _Baixo acoplamento_: Alterações internas não afetam consumidores externos
    
- _Interface vs. Implementação_: Separa _o que faz_ de _como faz_

Ele protege os atributos de serem modificados por um código externo de forma inesperada. O encapsulamento é gerenciado pelos **modificadores de acesso**:[[apend. PHP & POO]]

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
        
    - Podem conter métodos abstratos (que não têm implementação e devem ser implementados pelas classes filhas) e métodos concretos,ou seja, contém apenas suas assinaturas (nome, parâmetros e tipo de retorno)
    
    **Exemplo:**
    Uma classe abstrata `FormaGeometrica` pode ter um método abstrato `calcularArea()`. As classes `Circulo` e `Retangulo` herdam de `FormaGeometrica` e cada uma implementa o método `calcularArea()`  de forma diferente. Para quem usa as classes, a lógica de cálculo fica "abstraída", você apenas chama o método `calcularArea()` e a classe sabe como fazê-lo.
    
- **Interfaces**:
    - Contratos que definem _o que_ deve ser implementado
        
    - Sem implementação ou estado
        
- **Teoria**:
    - _Redução de complexidade_: Foco em aspectos relevantes
        
    - _Especificação de contratos_: Separa obrigação de implementação
        
    - _Inversão de dependência_: Classes dependem de abstrações, não de implementações

**Exemplo II:**
Ao usar um carro, você não precisa saber como o motor funciona para dirigir. Você interage com o carro através do volante, pedais e câmbio, que são a interface abstrata do veículo.

📌 **Herança**
Mecanismo de especialização onde uma classe (filha) herda membros de outra (pai):

- **Relação "é-um" (ou "is-a" em inglês)**: `Carro` é um `Veículo`
    
- **Teoria**:
    - _Reúso hierárquico_: Elimina duplicação de código
        
    - _Generalização/Especialização_: Classes abstratas definem comportamentos genéricos
        
    - _Limitação_: Herança múltipla não permitida em PHP (resolvida com interfaces). No entanto, o PHP resolve essa limitação utilizando interfaces, que permitem que uma classe implemente múltiplos contratos, obtendo um comportamento semelhante à herança múltipla sem os problemas associados.
    
	**Interfaces como Solução em PHP**

	- Em PHP, interfaces são classes abstratas que definem um conjunto de métodos que uma classe deve implementar. Ao contrário da herança, as interfaces não possuem implementação, apenas a assinatura dos métodos. 
	- Uma classe pode implementar múltiplas interfaces, o que significa que ela pode "herdar" a estrutura de múltiplos contratos (as interfaces). 
	- Isso permite que a classe obtenha um comportamento semelhante à herança múltipla sem os problemas de ambiguidade, pois a implementação de cada método é responsabilidade da própria classe.

	**Exemplo:**
	- Imagine uma classe `Veiculo` e duas interfaces `Motorizado` e `Navegavel`. A interface `Motorizado` define métodos como `acelerar()` e `frear()`, enquanto a interface `Navegavel` define métodos como `virarEsquerda()` e `virarDireita()`.
- Uma classe `Carro` pode implementar ambas as interfaces `Motorizado` e `Navegavel`, herdando a estrutura de ambos os contratos e implementando seus métodos de acordo. 
- Isso permite que a classe `Carro` possa ser tratada como um veículo motorizado e um veículo navegável, sem a necessidade de herança múltipla direta.


📌**Polimorfismo**

Significa **"muitas formas"**. Capacidade de objetos responderem de formas diferentes à mesma mensagem:

- **Sobrescrita de métodos**: Reimplementação em classe filha
    
- **Ligação tardia (late binding)**: Decisão de qual método executar ocorre em tempo de execução, com base no tipo real do objeto, e não no tipo declarado na variável.
	**Exemplo:**
	magine uma classe base "Animal" com um método "emitirSom()". As classes derivadas "Cachorro", "Gato" e "Passaro" herdam de "Animal" e sobrescrevem o método "emitirSom()" com suas implementações específicas. 


- **Teoria**:
    - _Substituição de Liskov_: Objetos de subclasses devem ser substituíveis por objetos da superclasse, **sem causar problemas no comportamento do sistema**.
        
    - _Abstração de comportamento_: Código cliente opera com interfaces genéricas
        
    - _Tipos por comportamento_: Implementado via herança ou interfaces

### Teoria de Relações entre Conceitos

|Conceito|Propósito Principal|Unidade de Implementação|
|---|---|---|
|Classe|Modelagem de entidades|Código fonte|
|Objeto|Representação de instâncias|Memória durante execução|
|Herança|Hierarquia e reuso|Relação entre classes|
|Interface|Contrato polimórfico|Assinatura de métodos|
|Encapsulamento|Gerenciamento de dependências|Modificadores de acesso|
|Abstração|Generalização de conceitos|Classes/interfaces|

### Regras Importantes para Provas Técnicas

1. **Construtores em Herança**:
    
    - Classes filhas devem invocar explicitamente o construtor pai usando `parent::__construct()`
        
    - Atributos privados da superclasse não são acessíveis diretamente nas subclasses
        
2. **Classes Abstratas vs. Interfaces**:

| Característica                                                        | Classe Abstrata     | Interface  |
| --------------------------------------------------------------------- | ------------------- | ---------- |
| Implementação                                                         | Parcial ou completa | Nenhuma    |
| Atributos                                                             | Permitidos          | Proibidos  |
| Métodos Concretos                                                     | Permitidos          | Proibidos* |
| Herança Múltipla                                                      | Não suportada       | Suportada  |
| Construtores                                                          | Permitidos          | Proibidos  |
| _* Interfaces podem ter métodos concretos usando `default` no PHP 8+_ |                     |            |


3. **Encapsulamento Ideal**:
    
    - Atributos sempre `private` ou `protected`
        
    - Acesso via métodos controlados (getters/setters)
        
    - Validações centralizadas nos setters
        
	