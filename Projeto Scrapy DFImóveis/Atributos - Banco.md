## **Requisitos Funcionais – Gestão de Tipos de Imóvel (com Validações Contextuais)**

### **1. Tipos de Imóvel**

- **RF01:** O sistema deve suportar **6 tipos primários de imóvel**:
    
    - `Casa`
        
    - `Sobrado`
        
    - `Apartamento`
        
    - `Sala Comercial`
        
    - `Terreno`
        
    - `Galpão`
        

---

### **2. Atributos Gerais (Todos os tipos)**

- **RF02:** O sistema deve permitir armazenar as seguintes informações comuns a todos os tipos de imóvel:
    
    - **Título do anúncio** _(obrigatório, texto até 255 caracteres)_
        
    - **Descrição do anúncio** _(opcional, texto longo)_
        
    - **Endereço** _(obrigatório)_
        
    - **Latitude** e **Longitude** _(opcional)_
        
    - **Área total** _(obrigatória, numérica, m²)_
        
    - **Área útil** _(opcional, numérica, m²)_
        
    - **Valor total** _(obrigatório, numérico com até 2 casas decimais)_
        
    - **Bairro** _(obrigatório)_
        
    - **Cidade** _(obrigatório)_
        
    - **Quantidade de quartos** _(numérico inteiro ≥ 0; obrigatório para residenciais)_
        
    - **Quantidade de suítes** _(numérico inteiro ≥ 0; obrigatório para residenciais)_
        
    - **Posição do sol** _(opcional; valores permitidos: `Nascente`, `Poente`, `Indefinido`)_
        
    - **Nome do condomínio** _(opcional; obrigatório caso “Condomínio” seja marcado como presente)_
        
    - **Nome do vendedor** _(obrigatório)_
        
    - **CRECI** _(obrigatório se o vendedor for corretor ou imobiliária)_
        
    - **Telefone/WhatsApp** _(obrigatório; formato E.164 ou padrão nacional)_
        
    - **URL do anúncio** _(obrigatório; formato válido de URL)_
        
    - **Data de publicação** _(obrigatória; formato ISO 8601)_
        
    - **Data da última atualização** _(preenchida automaticamente pelo sistema)_
        
    - **Disponibilidade para financiamento** _(opcional; valores permitidos: `Sim` ou `Não`)_
        

---

### **3. Atributos Específicos por Tipo**

- **RF03:** Para **Apartamento** e **Sala Comercial**:
    
    - **Nome do edifício** _(obrigatório; texto até 255 caracteres)_
        
    - **Total de andares do edifício** _(obrigatório; numérico inteiro ≥ 1)_
        
    - **Unidades por andar** _(obrigatório; numérico inteiro ≥ 1)_
        
    - **Vagas de garagem**:
        
        - Campo numérico inteiro ≥ 0
            
        - Obrigatório informar também o **Tipo de vaga** (`Privativa`, `Condomínio`, `Alugada`) caso o número seja > 0
            
- **RF04:** Para **Casa** ou **Sobrado**:
    
    - **Nome do condomínio** _(obrigatório se estiver dentro de condomínio)_
        
    - **Vagas de garagem** _(opcional; numérico inteiro ≥ 0, sem tipo obrigatório)_
        
- **RF05:** Para **Terreno**:
    
    - **Área útil** _(opcional; se informado, deve ser igual à área total)_
        
    - *_Atributos de quartos, suítes, vagas e edifício não são aplicáveis_
        
- **RF06:** Para **Galpão**:
    
    - **Vagas de garagem** _(opcional; numérico inteiro ≥ 0)_
        
    - *_Quartos e suítes não aplicáveis_
        

---

### **4. Validações de Bloqueio de Atributos Incompatíveis**

- **RF07:** O sistema deve impedir o preenchimento de atributos que não sejam compatíveis com o tipo de imóvel selecionado.
    
    - Exemplo: Campo “Unidades por andar” não pode ser preenchido para `Casa`, `Sobrado`, `Terreno` ou `Galpão`.
        
    - Exemplo: Campo “Nome do edifício” não pode ser preenchido para `Terreno` ou `Galpão`.
        

---

### **5. Características e Facilidades**

- **RF08:** O sistema deve permitir cadastrar múltiplas características (facilidades) para cada imóvel, podendo variar ou surgir novas durante o processo de raspagem.
    
    - Lista inicial de características: `Aceita Pets`, `Aquecimento Solar`, `Ar Condicionado`, `Cozinha Espaçosa`, `Cozinha com Armários`, `Despensa`, `Escritório`, `Interfone`, `Jardim`, `Lavabo`, `Mobiliado`, `Pintura Nova`, `Piscina`, `Piso em Porcelanato`, `Portão Eletrônico`, `Projeto de Iluminação`, `Salão Gourmet`, `Salão de Festas`, `Sauna`, `Varanda`, `Vista Livre`, `Área de Lazer`, `Área de Serviço`, `Área de Serviço Coberta`.
        
    - Características devem ser armazenadas em formato que permita expansão sem alteração da estrutura de dados.
        

---

### **Tabela de Regras de Validação Contextual**

| Campo                      | Tipo de dado                                                                    | Obrigatório para                                              | Opcional para                | Não aplicável para              | Restrições / Validação                        |
| -------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------- | ---------------------------- | ------------------------------- | --------------------------------------------- |
| Tipo de imóvel             | Lista (`Casa`, `Sobrado`, `Apartamento`, `Sala Comercial`, `Terreno`, `Galpão`) | Todos                                                         | —                            | —                               | Valor deve estar na lista pré-definida        |
| Título do anúncio          | Texto (≤ 255)                                                                   | Todos                                                         | —                            | —                               | Não pode estar vazio                          |
| Descrição do anúncio       | Texto longo                                                                     | —                                                             | Todos                        | —                               | —                                             |
| Endereço                   | Texto                                                                           | Todos                                                         | —                            | —                               | —                                             |
| Latitude                   | Decimal                                                                         | Todos                                                         | —                            | —                               | Formato decimal (-90 a 90)                    |
| Longitude                  | Decimal                                                                         | Todos                                                         | —                            | —                               | Formato decimal (-180 a 180)                  |
| Área total                 | Numérico (m²)                                                                   | Todos                                                         | —                            | —                               | > 0                                           |
| Área útil                  | Numérico (m²)                                                                   | Apartamento, Sala Comercial, Casa, Sobrado, Galpão            | Terreno (igual à área total) | —                               | ≥ 0                                           |
| Valor total                | Numérico (2 casas decimais)                                                     | Todos                                                         | —                            | —                               | ≥ 0                                           |
| Bairro                     | Texto                                                                           | Todos                                                         | —                            | —                               | —                                             |
| Cidade                     | Texto                                                                           | Todos                                                         | —                            | —                               | —                                             |
| Quartos                    | Inteiro ≥ 0                                                                     | Casa, Sobrado, Apartamento                                    | Galpão                       | Terreno, Sala Comercial         | —                                             |
| Suítes                     | Inteiro ≥ 0                                                                     | Casa, Sobrado, Apartamento                                    | —                            | Terreno, Galpão, Sala Comercial | —                                             |
| Posição do sol             | Lista (`Nascente`, `Poente`, `Indefinido`)                                      | —                                                             | Todos                        | —                               | —                                             |
| Nome do condomínio         | Texto                                                                           | Casa, Sobrado, Apartamento, Sala Comercial (se em condomínio) | —                            | Terreno, Galpão                 | —                                             |
| Nome do edifício           | Texto                                                                           | Apartamento, Sala Comercial                                   | —                            | Casa, Sobrado, Terreno, Galpão  | Obrigatório para Apartamento e Sala Comercial |
| Total de andares           | Inteiro ≥ 1                                                                     | Apartamento, Sala Comercial                                   | —                            | Casa, Sobrado, Terreno, Galpão  | —                                             |
| Unidades por andar         | Inteiro ≥ 1                                                                     | Apartamento, Sala Comercial                                   | —                            | Casa, Sobrado, Terreno, Galpão  | —                                             |
| Vagas de garagem           | Inteiro ≥ 0                                                                     | Apartamento, Sala Comercial (com tipo obrigatório se > 0)     | Casa, Sobrado, Galpão        | Terreno                         | —                                             |
| Tipo de vaga               | Lista (`Privativa`, `Condomínio`, `Alugada`)                                    | Apartamento, Sala Comercial (se vagas > 0)                    | —                            | Casa, Sobrado, Galpão, Terreno  | —                                             |
| Nome do vendedor           | Texto                                                                           | Todos                                                         | —                            | —                               | —                                             |
| CRECI                      | Texto                                                                           | Corretor / Imobiliária                                        | —                            | Vendedor particular             | —                                             |
| Telefone/WhatsApp          | Texto                                                                           | Todos                                                         | —                            | —                               | Formato E.164 ou nacional                     |
| URL do anúncio             | Texto (URL)                                                                     | Todos                                                         | —                            | —                               | Deve ser URL válida                           |
| Data de publicação         | Data                                                                            | Todos                                                         | —                            | —                               | Formato ISO 8601                              |
| Data da última atualização | Data                                                                            | Todos (preenchida automaticamente)                            | —                            | —                               | —                                             |
| Financiamento              | Booleano (`Sim`, `Não`)                                                         | Todos                                                         | —                            | —                               | —                                             |
| Características            | Lista de texto                                                                  | —                                                             | Todos                        | —                               | Lista aberta, permite valores novos           |

