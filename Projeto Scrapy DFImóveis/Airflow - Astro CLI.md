
#### **Primeiro**: certifique-se de que você tem as seguintes ferramentas instaladas:

- **Docker:** É a tecnologia que vamos usar para rodar o Airflow em contêineres. Você pode baixá-lo aqui: [https://www.docker.com/](https://www.docker.com/). ou em qualquer loja de aplicativos.

mas já deixando mastigadinho para o Gnome
```bash
sudo dnf install gnome-terminal
```
e em seguida
```bash
sudo dnf install ./docker-desktop-x86_64.rpm
```


- **Astro CLI:** É a ferramenta que simplifica a criação e a execução do ambiente local do Airflow. Você pode instalá-lo seguindo as instruções oficiais: [https://docs.astro.io/astro-cli/install-cli](https://www.google.com/search?q=https://docs.astro.io/astro-cli/install-cli).

```bash
curl -sSL install.astronomer.io | sudo bash -s
```
baixa a última versão direto do PATH
```bash
astro version
```
verifica a instalação

#### **Segundo**: com o Astro CLI instalado, você pode criar a estrutura de projeto do Airflow com um único comando:

- Navegue até o diretório onde você quer criar o seu projeto.
- Execute o seguinte comando:

```bash
astro dev init
```

Esse comando vai criar uma série de arquivos e pastas essenciais para o seu projeto Airflow, como:

- **`dags/`**: A pasta onde você vai colocar todos os seus arquivos de DAGs (`.py`).
    
- **`docks/`**: Contém os arquivos `docker-compose.yaml` e `Dockerfile` que definem o seu ambiente local do Airflow.
    
- **`include/`**: Para armazenar arquivos auxiliares, como scripts ou templates que suas tarefas precisam.
    
- **`packages.txt`**: Para especificar pacotes Python adicionais que você precisa instalar no seu ambiente do Airflow.
    
- **`requirements.txt`**: Para instalar bibliotecas Python que suas tarefas precisam, como `requests` para raspagem de dados.

#### **Terceiro:** Agora que a estrutura está pronta, você pode escrever o seu DAG de raspagem dentro da pasta **`dags/`**.

#### **Quarto:** Execute o comando para iniciar o ambiente do Airflow:

```bash
astro dev start
```

certifique-se de que você está no diretório raiz do seu projeto (onde você executou o `astro dev init`).

Esse comando ira:

- Construir as imagens Docker.

- Baixar as dependências necessárias.

- Iniciar os contêineres do Airflow (servidor web, agendador, etc.).

Depois de alguns minutos, você verá um aviso no terminal informando que o ambiente está pronto e a URL da interface do usuário do Airflow.

#### **Quinto:** Acessando a Interface do Airflow

6. Abra um navegador e acesse o endereço fornecido no terminal (geralmente `http://localhost:8080/`).
    
7. Use as credenciais padrão para fazer login. Por padrão, o Astro CLI usa:
    
    - **Usuário:** `admin`
        
    - **Senha:** `admin`
        
8. Na interface do Airflow, você verá uma lista de DAGs. Encontre o seu DAG chamado `web_scraping_flow`. Ele deve estar com o status de **Ativado**.
    
9. Clique no nome do DAG para ver o seu fluxo de trabalho, o agendamento e o status das execuções. Você também pode acionar uma execução manual clicando no botão de **play** no canto superior direito.
    

Pronto! Agora você tem um ambiente Airflow local e funcional para desenvolver e testar seus fluxos de trabalho de raspagem de dados.