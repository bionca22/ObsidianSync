## Info
Na pasta teste tem um exemplo de repositório com um commit e push que foi enviado para o gitea pela tailscale

Na pasta teste2 tem um exemplo de repositorio criado com o comando ```git tea teste-repo```
Esse comando cria remotamente um repositório no gitea e clona ele localmente já com o remote adicionado para efetuar push.

#### Clonar repositório 
```bash
git fork gitea:matheus/ScrapyImoveis.git
```
esse comando clona exatamente o projeto certo.
### Adicionar remotes

Verificar se existem repositórios vinculados
```bash
git remote -v
```

Adicionar remote gitea
```bash
git remote add origin gitea:bianca/teste.git
```

Caso precise adicionar upstream
```bash
git remote add upstream gitea:usuario/repositorio-original.git
```

Depois de adicionar primeiro commit, checar branches (locais e remotas):
```bash
git branch -a
```

### Clonar

```bash
git clone gitea:usuario/nome_repositorio.git
```

clonar uma branch especifica
```bash
git clone -b nome-branch --single-branch gitea:usuario/repositorio.git
```
