
### Adicionar remotes

Criar pasta para o repositorio, entrar nela.
Cria repositório e clona na pasta atual:
```bash
git clone gitea:usuario/repositorio.git
```

Criar outra pasta para clonar o repositório existente, entrar nela.
Clonar repositório existente:
```bash
git clone gitea:usuario/repositorio.git
```
Lista os remotes (url do repositório)
```bash
git remote -v
```



Verificar se existem repositórios vinculados
```bash
git remote -v
```

```bash
git remote add origin gitea:bianca/teste.git
```

```bash
git remote add upstream gitea:usuario/repositorio-original.git
```

Depois de adicionar primeiro commit, checar branches (locais e remotas):
```bash
git branch -a
```

mudar de branch
```bash
git checkout nome-da-branch
```

### Clonar

```bash
git clone gitea:usuario/repositorio.git
```


```bash
git clone -b testes --single-branch gitea:matheus/ScrapyImoveis.git
```

### Alias Git Personalizado

### Criando novo projeto via terminal

Cria repositório e clona


```bash
git tea teste-repo
```


# VENV windows

criar venv
```powershell
python -m venv venv
```

ativar
```powershell
.\venv\Scripts\Activate.ps1
```

instalar dependencias
```powershell
pip install -r requirements.txt
```

sair
```powershell
deactivate
```

Adicionar no vscode
- crtl+shift+p
- python: select interpreter
- E:\Repo\ScrapyImoveis\venv (local do venv)



## Adicionando script como alias git Matheus bazzite

```bash
# 1. Remover o alias quebrado
git config --global --unset alias.create-gitea

# 2. Recriar corretamente (uma linha só!)
git config --global alias.create-gitea '!f() { echo "🚀 Criando repositório $1..."; response=$(curl -s -X POST "https://pc.llama-notothen.ts.net:3000/api/v1/user/repos" -H "Authorization: token c2a9401778a284a9a29f606ff6d55fa2a56c2129" -H "Content-Type: application/json" -d "{\"name\":\"$1\",\"description\":\"Repositório criado via Git alias\",\"auto_init\":true}"); if echo "$response" | grep -q "\"name\""; then echo "✅ Repositório criado com sucesso!"; echo "📦 Clonando..."; sleep 2; git clone gitea:$(whoami)/$1.git; else echo "❌ Erro ao criar repositório:"; echo "$response"; fi; }; f'
```

```
c2a9401778a284a9a29f606ff6d55fa2a56c2129
```
### Script windows

Comando para criar repositório e clonar
```powershell
git create-gitea teste-windwos
```
## Adicionando script como alias git Bianca

```
2648f25b3f09e5f4f34d8ba3f5501cf05a56e2ee
```
