#### **1. Conceitos Fundamentais**

- **Repositório (Repo)**: Diretório onde o Git rastreia as alterações dos arquivos.
    
- **Commit**: "foto" das alterações, com um histórico versionado.
    
- **Branch (Ramificação)**: Linha independente de desenvolvimento. A branch padrão é `main` ou `master`.
    
- **Working Directory**: Diretório de trabalho local.
    
- **Staging Area (Index)**: Área onde as alterações são preparadas para serem commitadas.

#### **2. Comandos Essenciais do Ciclo de Vida**

|Comando|Função|Exemplo de Uso|
|---|---|---|
|**`git init`**|Inicializa um repositório Git local.|`git init`|
|**`git clone`**|Baixa um repositório remoto para a máquina local.|`git clone https://github.com/usuario/repo.git`|
|**`git add`**|Adiciona alterações ao Staging Area.|`git add arquivo.txt` (arquivo específico)  <br>`git add .` (todos os arquivos)|
|**`git commit`**|Salva as alterações do Staging Area em um commit.|`git commit -m "Mensagem descritiva"`|
|**`git status`**|Mostra o estado das alterações (tracked/untracked).|`git status`|
|**`git log`**|Exibe o histórico de commits.|`git log --oneline` (visão simplificada)|

#### **3. Sincronização com Repositório Remoto**

|Comando|Função|Exemplo|
|---|---|---|
|**`git push`**|Envia commits locais para o repositório remoto.|`git push origin main`|
|**`git pull`**|Atualiza o repositório local com alterações do remoto.  <br>(Equivale a `git fetch` + `git merge`)|`git pull origin main`|
|**`git fetch`**|Busca alterações do repositório remoto, mas não aplica.|`git fetch origin`|

#### **4. Ramificação (Branching) e Mesclagem (Merging)**

| Comando            | Função                                        | Exemplo                                      |
| ------------------ | --------------------------------------------- | -------------------------------------------- |
| **`git branch`**   | Lista, cria ou deleta branches.               | `git branch feature-x` (cria branch)         |
| **`git checkout`** | Muda para uma branch ou restaura arquivos.    | `git checkout feature-x`                     |
| **`git switch`**   | Alterna entre branches (versão mais moderna). | `git switch main`                            |
| **`git merge`**    | Mescla uma branch à branch atual.             | `git switch main`  <br>`git merge feature-x` |

## Úteis

| Comando                  | Função                                                                                            | Exemplo                                                                                                                                                                                    |
| ------------------------ | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **`git commit --amend`** | Corrigi o último commit                                                                           | `git commit --amend -m "Nova mensagem"`                                                                                                                                                    |
| // //                    | Para adicionar arquivos que não foram incluídos no último commit                                  | `git add <nome-do-arquivo>` e depois `git commit --amend`                                                                                                                                  |
| **`git rebase -i`**      | Isso abrirá um editor (como Vim ou Nano) com uma lista dos seus commits e comandos disponíveis:   | `git checkout minha-feature`em seguida<br>`git rebase -i main`                                                                                                                             |
| **`git stash`**          | Uma "gaveta" temporária para suas alterações. Permite que você volte a um estado de commit limpo. | `git stash push -m "Minha mensagem descritiva"`                                                                                                                                            |
| **`git cherry-pick`**    | Aplica alterações de um commite específico de uma branch em outra                                 | 1. Encontre o hash do commit que deseja trazer (usando `git log`).<br>    <br>2. Mude para a branch de destino.<br>    <br>3. Execute:<br>`git checkout main`<br>`git cherry-pick a1b2c3d` |
> [!abstract] Mais sobre o git rebase -i
>Este comando é mais complexo e poderoso. Ele significa: 
>- **`rebase`**: "Rebasear" é mover a base de sua branch para a ponta de outra branch. Em outras palavras, ele pega todos os seus commits (que estão em `minha-feature`) e os "reaplica" no topo da branch `main`. O resultado é que sua branch `minha-feature` parecerá que foi criada a partir do ponto mais recente da `main`, mantendo um histórico de commits mais limpo e linear.
> **`-i`**: A flag `-i` significa "interativo". Isso é o que torna o comando tão útil. Ao usar o `-i`, o Git abre um editor de texto com uma lista dos commits da sua branch. Nesse editor, você pode interagir com os commits, podendo:
> - **`pick`**: Manter o commit como está.
> - **`reword`**: Alterar a mensagem do commit.
> - **`squash`**: Combinar um commit com o commit anterior, unindo-os em um só.
> - **`fixup`**: Combinar um commit com o anterior, mas descartando a mensagem do commit atual.
> - **`reorder`**: Mudar a ordem dos commits.
> - **`drop`**: Excluir um commit.
> ##### Exemplo de saida:
> ```bash
pick a1b2c3d Adiciona funcionalidade X
pick e4f5g6h Corrige bug na funcionalidade X
pick i7j8k9l Adiciona testes para X








## Boas Praticas
- **Git Tags**: Marque versões estáveis:
```bash
git tag -a v1.0.0 -m "Versão 1.0.0"
git push origin --tags
```

### **Fluxos de Trabalho (Workflows) Comuns**
1. **GitFlow**:
    
    - Branches fixas: `main` (produção), `develop` (integração), `feature/`, `release/`, `hotfix/`.
        
    - Ideal para projetos com versões planejadas.
    
2. **GitHub Flow**:
    
    - Simples: `main` sempre deployável, branches de feature com PRs.
        
    - Mais ágil para integração contínua.

-----

### ** Estados de um Arquivo no Git**

O Git tem um sistema que classifica os arquivos em seu diretório de trabalho em diferentes estados. Entender isso é crucial para saber o que cada comando faz.

Imagine um cenário onde você tem um repositório Git. Um arquivo pode estar em um destes estados:

![[Pasted image 20250821170853.png]]**Por que isso é importante?**

- **`git status`** usa esses termos para te dizer o que está acontecendo.
    
- Os comandos **`git add`** e **`git commit`** movem os arquivos entre esses estados.

### ** Conflito de Merge (Merge Conflict)**

#### **O que é?**

Um **conflito de merge** ocorre quando o Git tenta **automaticamente** combinar (mesclar) alterações de duas branches diferentes, mas encontra **alterações conflitantes na mesma parte do mesmo arquivo**. Como o Git não pode adivinhar qual alteração é a correta, ele interrompe o processo e pede que um **humano** resolva manualmente o impasse.

#### **Quando acontece?**

É mais comum em dois cenários:

1. **Fazendo `git merge`** de uma branch (ex.: `feature/login`) na sua branch (ex.: `main`).
    
2. **Fazendo `git pull`** (que é um `git fetch` + `git merge`) quando você e outra pessoa commitarem alterações diferentes na mesma parte do mesmo arquivo no repositório remoto.
    

#### **Como o Git sinaliza um conflito?**

O Git modifica o arquivo com problemas, inserindo **marcadores especiais** que delimitam as alterações conflitantes.

- **`<<<<<<< HEAD`**: Tudo abaixo desta linha é a alteração que está na sua branch atual (onde você está fazendo o merge).
    
- **`=======`**: Separa as duas alterações conflitantes.
    
- **`>>>>>>> nome-da-outra-branch`**: Tudo abaixo desta linha é a alteração que veio da branch que você está tentando mergar.
    

#### **Passo a Passo para Resolver um Conflito de Merge**

1. **Identifique os arquivos com conflito**:  
    O próprio Git irá te dizer após o comando `git merge` ou `git pull` falhar:  
    `Automatic merge failed; fix conflicts and then commit the result.`  
    Use `git status` para ver a lista de arquivos marcados como "both modified".
    
2. **Abra cada arquivo listado** em um editor de código.  
    Você verá os marcadores `<<<<<<<`, `=======`, `>>>>>>>`.
    
3. **Edite o arquivo para resolver o conflito**:  
    Sua tarefa é:
    
    - **Decidir** qual código ficar (o de cima, o de baixo, uma mistura dos dois, ou um código totalmente novo).
        
    - **Remover TODOS os marcadores** deixados pelo Git (`<<<<<<<`, `=======`, `>>>>>>>`).  
        O arquivo final deve parecer com um código normal e funcional, exatamente como você quer que ele fique.
        
Após resolver o conflito em um arquivo, você precisa dizer ao Git que o problema foi resolvido. Use `git add`:

```
git add caminho/do/arquivo/resolvido.html
```

  
**Finalize o merge**:  
    Depois de adicionar TODOS os arquivos que estavam em conflito, finalize o processo com um commit:


## **Estados de um Arquivo no Git (File Status Lifecycle)**

O Git possui um sistema de classificação que monitora o ciclo de vida de cada arquivo em seu diretório de trabalho. Entender esses estados é crucial para saber qual comando usar e em que momento.

Imagine um fluxo de estados pelos quais um arquivo pode passar. O diagrama abaixo ilustra esse ciclo:

![[Pasted image 20250821171911.png]]

Agora, vamos detalhar cada um desses estados:

#### **1. Untracked (Não Rastreado)**

- **O que é?** Um arquivo que existe na sua pasta do projeto, mas que **o Git ainda não está monitorando**. Ele não estava presente no último commit (ou `snapshot`) do repositório.
    
- **Como identificar?** Ao executar `git status`, ele aparecerá na seção **"Untracked files"**.
    
- **Exemplo:** Você acabou de criar um novo arquivo `script.js` ou adicionou um PDF da pasta de downloads.
    
- **Próximo passo:** Para que o Git comece a monitorar as alterações desse arquivo, você deve usar `git add`.
Um "snapshot" de um repositório é uma cópia instantânea de todo o conteúdo e estado de um sistema ou conjunto de dados em um momento específico, servindo como um ponto de recuperação ou um clone para uso futuro.

#### **2. Tracked (Rastreado)**

Este não é um estado único, mas sim uma **categoria ampla** que engloba três estados (Unmodified, Modified, Staged). Um arquivo "Tracked" é qualquer arquivo que o Git **já conhece** e que estava presente no último commit.

#### **3. Unmodified (Não Modificado)**

- **O que é?** Um arquivo que está sendo rastreado (Tracked) e **não sofreu nenhuma alteração** desde o último commit. É uma cópia idêntica do que está no repositório.
    
- **Como identificar?** É o estado "default". O `git status` não mostrará esses arquivos, a menos que você use a flag `-u all`. A mensagem será simplesmente `nothing to commit, working tree clean`.
    
- **Exemplo:** O arquivo `index.html` que você comitou ontem e não mexeu desde então.
    
- **Próximo passo:** Se você editar esse arquivo, ele se tornará "Modified".

#### **4. Modified (Modificado)**

- **O que é?** Um arquivo que está sendo rastreado (Tracked) e que **foi alterado** em seu diretório de trabalho, mas essas alterações ainda **não foram preparadas** (não foram para a Staging Area) para o próximo commit.
    
- **Como identificar?** Ao executar `git status`, ele aparecerá na seção **"Changes not staged for commit"**.
    
- **Exemplo:** Você abriu o `index.html`, adicionou uma nova tag `<p>` e salvou.
    
- **Próximo passo:** Para incluir essas alterações no próximo commit, você deve usar `git add`. Para descartar as alterações e voltar ao estado Unmodified, use `git restore <arquivo>`.

#### **5. Staged (Preparado / Indexado)**

- **O que é?** Um arquivo Modified (ou um novo arquivo Untracked) que foi **preparado** com o comando `git add`. Suas alterações atuais estão na **Staging Area** ( Index), prontas para serem "fotografadas" no próximo commit.
    
- **Como identificar?** Ao executar `git status`, ele aparecerá na seção **"Changes to be committed"**.
    
- **Exemplo:** Você editou o `index.html` e executou `git add index.html`.
    
- **Próximo passo:** Para consolidar essas alterações no histórico, execute `git commit`. Se você se arrepender, pode usar `git restore --staged <arquivo>` para remover o arquivo da Staging Area, fazendo-o voltar ao estado Modified (se era trackeado) ou Untracked (se era novo).

### **Resumo Visual com `git status`**

A saída do comando `git status` é um mapa perfeito desses estados:


```bash
$ git status
On branch main

# Área de STAGING: Alterações que serão commitadas
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   novo.txt          # Arquivo NOVO que foi 'git add' (foi de Untracked -> Staged)
        modified:   existente.txt     # Arquivo MODificado que foi 'git add' (foi de Modified -> Staged)

# Diretório de Trabalho: Alterações que NÃO estão preparadas
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   produto.txt       # Arquivo MODificado que ainda NÃO foi 'git add' (Modified)

# Arquivos que o Git nem conhece ainda
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        relatorio.pdf                 # Arquivo totalmente novo, não rastreado (Untracked)
```


##### Fluxo de Trabalho 

1. Um arquivo novo começa como `Untracked`.
    
2. `git add` o leva para `Staged`.
    
3. `git commit` o leva para `Unmodified`.
    
4. Editar o arquivo o leva para `Modified`.
    
5. `git add` novamente o traz de volta para `Staged`.
    

Esse ciclo é o coração do funcionamento básico do Git.


---
