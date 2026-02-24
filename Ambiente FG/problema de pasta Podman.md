O problema persiste porque o Podman está "confuso" entre o caminho simbólico (`/home/bianca`) e o caminho físico real do Bazzit (`/var/home/bianca`). No Bazzit, o `/home` é apenas um atalho.

Para setar o **static dir** (e o **graphroot**) para o lugar certo de forma definitiva, você precisa criar ou editar o arquivo de configuração de armazenamento do Podman.

Siga estes passos exatamente:

---

## 1. Descubra o seu ID de Usuário (UID)

A maioria das vezes é `1000`, mas vamos garantir. Digite no terminal:

Bash

```
id -u
```

_Guarde esse número (provavelmente é 1000)._

---

## 2. Configure o arquivo `storage.conf`

Vamos forçar o Podman a usar o caminho físico (`/var/home/...`) para que ele nunca mais veja o "mismatch".

1. **Crie a pasta de configuração:**
    
    Bash
    
    ```
    mkdir -p ~/.config/containers
    ```
    
2. **Abra o arquivo para edição (ou crie-o):**
    
    Bash
    
    ```
    nano ~/.config/containers/storage.conf
    ```
    
3. **Cole o conteúdo abaixo, trocando `bianca` pelo seu usuário e `1000` pelo seu UID:**
    


```
[storage]
driver = "overlay"
# O graphroot é onde ficam as imagens e containers (Caminho FÍSICO)
graphroot = "/var/home/bianca/.local/share/containers/storage"

[storage.options]
# O runroot é onde ficam os arquivos de execução temporários
runroot = "/run/user/1000/containers"
```

_Pressione `Ctrl+O`, `Enter` para salvar e `Ctrl+X` para sair._

---

## 3. O "Golpe de Misericórdia" (Limpeza Forçada)

Como o banco de dados anterior está corrompido com o caminho errado, você **precisa** deletar a pasta de armazenamento antes de tentar rodar o Podman com a nova configuração.

Se o `rm -rf` falhou antes, é porque o Podman ainda tinha montagens ativas. Use este comando especial:

Bash

```
# Isso força o desmonte de qualquer camada de container travada
podman unshare rm -rf /var/home/bianca/.local/share/containers/storage
```

Se o comando acima falhar, tente com `sudo` apenas para limpar a pasta:

Bash

```
sudo rm -rf /var/home/bianca/.local/share/containers/storage
```

---

## 4. Verifique se funcionou

Agora, tente rodar o comando de informação do Podman:

Bash

```
podman info
```

Procure nas primeiras linhas por **"static dir"** e **"graphroot"**. Eles devem agora apontar para o caminho que você definiu no arquivo (`/var/home/bianca/...`).



# Limpar Compose

**Siga estes passos no terminal do Bazzit:**

1. **Pare tudo e remova o container problemático:**
    
    Bash
    
    ```
    podman-compose down
    ```
    
2. **Remova o volume de dados (Onde está o erro de formato):**
    
    Bash
    
    ```
    podman volume rm demo_pgdata
    ```
    
    _Nota: Se o comando disser que o volume não existe, verifique o nome correto com `podman volume ls`._
    
3. **Suba o banco novamente:**
    
    Bash
    
    ```
    podman-compose up -d
    ```