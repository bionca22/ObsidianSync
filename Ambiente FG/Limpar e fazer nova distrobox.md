caso esteja começando do 0 pode ir direto para o **passo 2**
## Passo 1: O "Reset" de Emergência

Para conseguir deletar as pastas que estão dando erro, primeiro precisamos garantir que nenhum processo de container esteja rodando "fantasma" no fundo.

1. **Force a parada de tudo:**
    
    Bash
    
    ```
    distrobox stop --all
    podman kill --all
    ```
    
2. **Remova o Distrobox (se ele ainda existir):**
    
    Bash
    
    ```
    distrobox rm dev-station --force
    ```
    
3. **Remova as pastas "travadas" com privilégios de administrador:** Se o seu usuário não conseguiu deletar, vamos usar o `sudo`. **Cuidado:** Verifique bem o caminho antes de dar Enter.
    
    Bash
    
    ```
    sudo rm -rf /var/home/bianca/.local/share/containers/storage
    ```
    

---

## Passo 2: Configuração Limpa (O jeito certo no Bazzit)

Agora que o terreno está limpo, vamos criar o seu ambiente de desenvolvimento focado apenas em **Java, Node e Docker**, deixando IntelliJ e DBeaver para o sistema principal.

### 1. Criar o novo Distrobox:

Bash

```
distrobox create --name dev-station --image fedora:latest --additional-flags "--security-opt label=disable"
```

### 2. Entrar e instalar a Stack de Dev:

Bash

```
distrobox enter dev-station
```

Dentro do container, execute este "combo" de instalação:

Bash

```
# Essenciais
sudo dnf install -y curl zip unzip tar git podman-docker

# SDKMAN (Java 21)
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install java 21.0.2-tem

# NVM (Node & Angular)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install 22  # Versão LTS estável
npm install -g @angular/cli
```

---

## Passo 4: O Banco de Dados (PostgreSQL)

Agora que o armazenamento do Podman foi resetado, tente subir o banco novamente (no terminal do Bazzit):

Bash

```
podman run --name postgres \
  -e POSTGRES_PASSWORD=minhasenha \
  -p 5432:5432 \
  -d postgres:16
```
  
- para restartar o banco 
```Bash
podman start postgres
```

- para subir o contêiner do banco  sempre que inicializar o sistema 
```Bash
podman update --restart always postgres  
```
---

### Como você vai trabalhar agora:

- **No Terminal:** Você dá `distrobox enter dev-station` para rodar comandos do Angular (`ng serve`) ou compilar o Java (`mvn clean install`).
    
- **Na IDE:** Você abre o IntelliJ (Flatpak), aponta o projeto para a sua pasta na `/home` e, nas configurações de SDK, aponta para o Java que o SDKMAN instalou (geralmente em `.sdkman/candidates/java/current`).
    
- **No Banco:** O **DBeaver** (Flatpak) conecta direto em `localhost:5432`.

#### Como o seu código Java (dentro da Distrobox) vai achar o Banco?

Aqui está a mágica: Como a Distrobox usa a rede do host, para o seu Spring Boot, o banco está rodando "na mesma máquina".

No seu arquivo `src/main/resources/application.properties` (ou `.yml`), a configuração será exatamente esta:

Properties

```
spring.datasource.url=jdbc:postgresql://localhost:5432/nome_do_seu_banco
spring.datasource.username=postgres
spring.datasource.password=sua_senha
```

###  forma "Manual" (Via Spring Initializr) - Recomendada para iniciantes

Esta é a forma mais fácil porque você já baixa o projeto pronto para rodar.

1. No seu navegador, acesse [start.spring.io](https://start.spring.io).
    
2. Preencha as opções (Maven, Java 21).
    
3. No botão **Dependencies**, adicione: `Spring Web` e `Spring Data JPA`.
    
4. Clique em **Generate**. Ele vai baixar um arquivo `.zip`.
    
5. Extraia esse arquivo dentro da sua pasta `/var/home/bianca/IdeaProjects/`.
    
6. Abra essa pasta no IntelliJ.

Se você quer ser produtiva e fazer tudo pelo terminal da sua `dev-station`, você pode instalar o **Spring Boot CLI**.

1. Entre na sua distrobox: `distrobox enter dev-station`.
    
2. Use o **SDKMAN** (nosso melhor amigo aqui):
    
    Bash
    
    ```
    sdk install springboot
    ```

## Executar projeto via springboot
### Para rodar 
```
mvn spring-boot:run
```

### Para ver a origem do erro (`-e`)

Se você quer ver a lista completa de erros (o "caminho" que o erro percorreu no código):

Bash

```
./mvnw spring-boot:run -e
```

### Para o modo "Debug" total (`-X`)

Se o erro for estranho e você quiser ver tudo o que o Maven está fazendo nos bastidores (conexões, downloads, versões):

Bash

```
./mvnw spring-boot:run -X
```


**Caminho do Distrobox:** Você está tentando rodar o código de dentro da Distrobox? Lembre-se que, para o container `dev-station` enxergar o `localhost` do Bazzit, ele precisa ter sido criado com a flag `--host`. Se você não fez isso, use o IP da sua rede em vez de `localhost`.


# problemas springboot

Quando você cria um projeto com `spring-boot-starter-data-jpa`, o Spring **exige** saber onde está o banco. Se você não disse isso a ele, ele "morre" no primeiro segundo.

```
cat <<EOF > src/main/resources/application.properties
spring.application.name=demo
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=bianca
spring.datasource.password=minhasenha
spring.datasource.driver-class-name=org.postgresql.Driver
spring.jpa.hibernate.ddl-auto=update
EOF
```


### Inicializando o banco de dados junto com o sistema

O **Podman Compose** é a melhor escolha para gerenciar o banco. Ele mantém as configurações em um arquivo, facilitando subir e descer o serviço sem decorar comandos gigantes.

Aqui está o passo a passo para o seu ambiente:

### 1. O arquivo `compose.yaml`
para criar a pasta para o script do container, rode este comando rápido na raiz do projeto:

```
mkdir init-db
```

E agora, para o seu **`compose.yaml`** reconhecer tudo, certifique-se de que ele está na mesma pasta onde você deu o comando `mkdir`.

### Um detalhe sobre o Podman no Bazzit:

Como você está usando o Podman, ele é muito rigoroso com permissões. Ao rodar o seu `compose.yaml`, se ele reclamar de "Permission Denied" na pasta `init-db`, use o sufixo `:Z` no volume (como eu coloquei no exemplo anterior) para o Bazzit liberar o acesso.

```
services:
  db:
    image: postgres:latest
    container_name: meubanco
    restart: always  # Isso faz o container iniciar junto com o sistema
    environment:
      POSTGRES_USER: bianca
      POSTGRES_PASSWORD: minhasenha
      POSTGRES_DB: postgres
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data
      - ./init-db:/docker-entrypoint-initdb.d:Z # Scripts iniciais do banco

volumes:
  pgdata:
```

### 2. Inicializar o Banco via Java (O jeito Spring Boot)

Em vez de usar classes de teste manuais, o Spring Boot tem um recurso nativo que executa scripts SQL assim que a aplicação sobe. É a forma mais limpa de inicializar dados.

#### Passo A: Crie o script SQL

Crie um arquivo chamado `schema.sql` dentro de `src/main/resources/`:

SQL

```
-- src/main/resources/schema.sql
CREATE TABLE IF NOT EXISTS usuarios (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL
);

-- Você também pode criar um data.sql para inserir dados iniciais
INSERT INTO usuarios (nome, email) 
VALUES ('Bianca', 'bianca@exemplo.com') 
ON CONFLICT DO NOTHING;
```

#### Passo B: Configure o `application.properties`

Diga ao Spring para sempre rodar esses scripts ao iniciar:

Properties

```
# src/main/resources/application.properties
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=bianca
spring.datasource.password=minhasenha

# Inicialização do Banco
spring.sql.init.mode=always
```


### 3. Como colocar tudo para rodar

1. **Suba o Banco:** No terminal, onde está o seu arquivo compose, init-db digite:
    
    Bash
    
    ```
    podman-compose up -d
    ```
    
2. **Rode o Java:** Na raiz do projeto, dentro da distrobox, execute:
    
    Bash
    
    ```
    mvn spring-boot:run
    ```