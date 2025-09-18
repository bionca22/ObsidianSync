
#### Copiando um Repositório Local 
Usamos o modelo de fork. Nele existe um repositório principal de onde deve vir as atualizações e commits de atualizações devem estar ser feitos via pull request.

existe um [tutorial](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo)para se fazer Fork usando a interface gráfica do Git. Por linha de código pode ser feito assim:


➡️ Após isso use o comando para checar a conexão com o repositório principal:
```bash
git remote -v
```

 Aqui temos 4 informações:
 
 ```bash  
origin  gitea:<SeuUsuário/SeuRepositórioforkado> (fetch)
origin  gitea:<SeuUsuário/SeuRepositórioforkado> (push)
```

Informação sobre a origem dos meus commites locais, e:

```bash 
upstream        gitea:Usuário/RepositórioUpstream.git (fetch)
upstream        gitea:Usuário/RepositórioUpstream.git (push)
```

Informações sobre o upstream, o repositório principal. Se a resposta mostrar apenas informações do seu repositório local (2), isso significa que não está conectado ao repositório principal. 

➡️Esse problema pode ser facilmente resolvido setando o Upstream manualmente.
```bash
git remote add upstream gitea:<Usuário/RepositórioUpstream>.git
```

teste novamente usando `git remoute -v`

Agora que seu repositório local está preparado vamos a alguns fatores importantes.

➡️Atualize sua branch local com as últimas mudanças da branch main no upstream
```bash
git checkout main #entra na branch main local
git fetch upstream
```

`git fetch` é o comando mais seguro e menos destrutivo para se atualizar. Ele faz as seguinte ações:

- **Baixa as informações:** Ele vai até o repositório remoto e baixa todas as branches, tags e informações mais recentes.
    
- **Não altera seu código:** Ele armazena as atualizações em uma "área de staging" temporária no seu repositório local. **Ele não aplica essas mudanças na sua branch atual de trabalho**.

É como dar uma "olhadinha" no que há de novo no repositório remoto sem realmente misturar nada com o que você já está fazendo. 

➡️Se você rodar o `git fetch upstream` e não houver nenhuma nova alteração no repositório remoto, o Git não exibirá nada. A tela ficará completamente em branco após o comando, indicando que não há nada para baixar.

Se houver mudanças elas aparecerão no formato de commit:
```bash
From gitea:matheus/ScrapyImoveis
 * branch            main       -> FETCH_HEAD
   b6563c6..d9a7109  main       -> upstream/main
 ```

- **`* branch main -> FETCH_HEAD`**: O Git está baixando as informações da branch `main` e as armazenando em um "ponteiro" temporário chamado `FETCH_HEAD`.
    
- **`b6563c6..d9a7109 main -> upstream/main`**: mostra que sua branch `main` local está sendo atualizada com a versão remota (`upstream/main`). O `b6563c6..d9a7109` são os IDs de commit que o Git baixou.

➡️Esses logs também podem ser acessados via:
```bash
git log upstream/main
```

>[!tip]
>##### Outros comandos úteis dentro do `git log`:- **Seta para cima/baixo** → rola linha por linha.
>- **Barra `/`** + texto → busca dentro do log.
>- **Espaço** → avança uma página.
>- **b** → volta uma página.
>- **q** → sai.

➡️Dê uma olhada nos commits feitos por parte de outros colegas de equipe e baixe as informações em sua cópia local:

```bash
git merge upstream/main
#ou 
git rebase upstream/main
#dependendo da sua necessidade
```

➡️Envie essas mudanças para o seu fork online:
```bash
git push origin main
```

➡️Verifique se está tudo funcionando como deveria - e prontinho. não esqueça de mudar de branch antes de começar a codar!

```bash
git checkout -b developer
```

> [!warning] 
> Esse comando cria e muda pra a branch developer se essa não existir. Se já tiver uma branch developer, apenas remova o marcador `-b`

➡️Para a branch ser reconhecida no repositório remoto ela também deve estar setada pelo comando remote

```bash
git push --set-upstream origin develop
```

----
### Sobre Merge 

A branch em que está é a branch que recebe as mudanças. 

(adere a mudança) main <- develop (passa as mudanças)

Então se por exemplo se quer passar as mudanças de uma branch develop para a main, primeiro deve dar checkout na branch main parar executar o merge. aqui um fluxo simples:

```bash
# 1. Mude para a branch principal 
git checkout main

# 2. Puxe as últimas atualizações
git pull origin main 

# 3. Faça a mesclagem da branch develop
git merge develop 

# 4. Envie as mudanças para o repositório remoto
git push origin main
```


-----
### Descartando mudanças no Projeto

Quando as mudanças estão fresquinha e não foram commitadas um simples restore deve resolver

```bash
git restore .
```

Para descartar todas as alterações em todos os arquivos 

##### Para alterações já **commitadas**

Temos `git reset --soft` e `git reset --hard` o reset da cabeça mole e da cabeça dura.


```bash
git reset --soft <commit>
```

Vai mover o ponteiro (HEAD) da sua branch de volta para o commit que você especificou. E Manter as alterações nos commits "desfeitos" em área de staging.

```bash
git reset --hard <commit>
```

Vai, assim como o `--soft`, mover o ponteiro da sua branch para o commit que especificou. Porém, ele **descarta completamente** todas as alterações que foram feitas nos commits "desfeitos", esses são removidas do seu diretório de trabalho e da área de staging.
