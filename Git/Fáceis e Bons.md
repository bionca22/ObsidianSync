
Você pode incluir alterações adicionais ao commit atual antes de enviá-lo para o repositório remoto. Para isso, você precisa adicionar as alterações nos arquivos e, em seguida, confirmar as alterações usando a flag `--amend`. Para manter a mensagem do commit anterior, basta usar a flag `--no-edit`.

```
$ git add . 
$ git commit --amend --no-edit
```

-----

Para desfazer um commit no Git, você pode usar o comando `revert`. No entanto, esse comando não remove nenhum commit. Em vez disso, ele cria um novo commit que desfaz as alterações feitas pelo commit original.

Usaremos o comando `log` com a flag `--oneline` para visualizar o histórico de commits de forma mais concisa. 

```
$ git log --oneline
```

-----

Salvar com nome

```
$ git stash save new-idea
```

```
stash@{n}: On master: new-idea
```

Nosso acervo de "novas ideias" está salvo no índice 0. Para recuperá-lo, use este comando:

```
$ git stash apply n
```

----

Para retornar ao branch em que estava pouco antes de mudar

```
$ git checkout -
```

----

sinceramente, se você estiver usando algo muito mais complicado que os comandos básicos, provavelmente você está fazendo algo estranho ou sua equipe está trabalhando em algo avançado e você não vai aprender isso no fim de semana.

Mas de qualquer forma, aqui estão algumas coisas que eu pessoalmente acho úteis;

obter as últimas alterações remotas
```
git fetch
``` 

---

atualizar sua main local para corresponder à main remota (contanto que você não tenha a main em checkout). Main é, claro, um exemplo, você pode fazer isso em qualquer branch.
```
git fetch origin main:main
```

---
  
  sobrescrever seu último commit com as alterações em staging sem alterar a mensagem do commit
```
git commit --amend --no-edit
```

---

`git blame` 