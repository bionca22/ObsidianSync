
### **1. Tabela `Imovel` (Tabela Principal)**

Armazena informações básicas do imóvel
```SQL
CREATE TABLE Imovel (
    imovel_id INT PRIMARY KEY AUTO_INCREMENT,
    cidade VARCHAR(100) NOT NULL,
    bairro VARCHAR(100) NOT NULL,
    endereco TEXT NOT NULL,
    quartos INT,
    suites INT,
    garagens INT,
    posicao_sol VARCHAR(50), -- Ex: Poente, Nascente
    area_util VARCHAR(50),    -- Ex: "150,00 m²"
    area_total VARCHAR(50),
    preco DECIMAL(15,2),
    latitude DECIMAL(10,7),
    longitude DECIMAL(10,7),
    publicado_dias VARCHAR(50),
    aceita_financiamento BOOLEAN, -- True/False
    posicao_imovel VARCHAR(50),   -- Ex: Frente, Fundos
    nome_edificio VARCHAR(255),
    ultima_atualizacao DATE,
    unidades_andar VARCHAR(50),
    total_andares_empr VARCHAR(50),
    titulo VARCHAR(255),
    descricao TEXT,
    url_origem VARCHAR(500),
    vendedor_id INT, -- FK para Vendedor
    edificio_id INT  -- FK para Edificio (se aplicável)
);
```
### **2. Tabela `Vendedor`**

Gerencia informações dos corretores
```SQL
CREATE TABLE Vendedor (
    vendedor_id INT PRIMARY KEY AUTO_INCREMENT,
    nome_vendedor VARCHAR(255) NOT NULL,
    creci VARCHAR(20) UNIQUE NOT NULL,
    whatsapp VARCHAR(20),
    telefone TEXT
);
```

### **3. Tabela `Caracteristica`**

Armazena características únicas dos imóveis (normalizado)
```SQL
CREATE TABLE Caracteristica (
    caracteristica_id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) UNIQUE NOT NULL -- Ex: "Piscina", "Varanda"
);
```

### **4. Tabela `Imovel_Caracteristica` (Tabela de Junção)**

Relaciona imóveis com suas características (N:M)
```SQL
CREATE TABLE Imovel_Caracteristica (
    imovel_id INT,
    caracteristica_id INT,
    PRIMARY KEY (imovel_id, caracteristica_id),
    FOREIGN KEY (imovel_id) REFERENCES Imovel(imovel_id),
    FOREIGN KEY (caracteristica_id) REFERENCES Caracteristica(caracteristica_id)
);
```

- **`REFERENCES Imovel(imovel_id)`**: Cria uma **chave estrangeira** que aponta para a tabela `imoveis`, garantindo que você não possa adicionar uma relação para um imóvel que não existe.
    
- **`REFERENCES Caracteristica(caracteristica_id)`**: Da mesma forma, cria uma chave estrangeira para a tabela `itens_imovel`.
    
- **`PRIMARY KEY (imovel_id, caracteristica_id)`**: Define uma chave primária composta, garantindo que um mesmo imóvel não possa ter o mesmo item listado duas vezes.
### **5. Tabela `Edificio` (Opcional)**

Para imóveis em condomínios/prédios
```SQL
CREATE TABLE Edificio (
    edificio_id INT PRIMARY KEY AUTO_INCREMENT,
    nome_edificio VARCHAR(255) UNIQUE NOT NULL,
    unidades_andar INT,
    total_andares INT
);
```

### **6. Tabela `Midia` (Para NoSQL)**

Armazenaria dados não estruturados (será usada no NoSQL)

Coleção: Midia
Campos:
- imovel_id (ref)
- video_url
- fotos [array]
- virtual_tour

---

### **Relacionamentos:**

- **1:N** entre `Vendedor` e `Imovel` (1 vendedor tem N imóveis)
    
- **N:M** entre `Imovel` e `Caracteristica` (via tabela de junção)
    
- **1:1** entre `Imovel` e `Edificio` (quando aplicável)
    

### **Observações:**

1. **Normalização:**
    
    - Características repetitivas ("Piscina", "Varanda") foram extraídas para tabela separada
    - Dados de vendedor desacoplados dos imóveis
    
2. **Flexibilidade para NoSQL:**
    
    - Campos como `descricao` e `fotos` podem ser migrados para NoSQL posteriormente
    - Dados geoespaciais (`latitude/longitude`) podem ser otimizados em bancos NoSQL
    
3. **Tratamento de Dados:**
    
    - Campos como `area_util` mantidos como VARCHAR para preservar formatação original
    - `aceita_financiamento` como BOOLEAN após limpeza dos dados ("Sim" → True)



