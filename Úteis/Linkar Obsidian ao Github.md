criado em 2025
### Criar Tolken

1. No canto superior direito de qualquer página do GitHub, clique na sua foto de perfil e depois em **Settings** (Configurações).

2. No menu lateral esquerdo, clique em **Developer settings** (Configurações de desenvolvedor).

3. Em seguida, clique em **Personal access tokens** (Tokens de acesso pessoal).

4. Escolha 
    - **Tokens (classic)** (Tokens clássicos): Clique em **Generate new token (classic)** e configure o nome, expiração e escopos necessários. Mais detalhes em [Criar um token de acesso pessoal clássico](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-personal-access-token-classic).

ou pelo link:
https://github.com/settings/tokens/new

____

### Plugin Git

>Vá até settings -> habilite os plugins de da comunidade -> browser -> instale o o plugin Git e habilite.



> fora da aba de plugins aperte ctrl + p ->  procure a opção `clone` do plugin Git e coloque a seguinte estrutura:

```bash
http://<seu tolken>@<endereço do repositório já criado>.git
```

>Dê enter


>Na proxima sessão coloque o nome que deseja para a pasta no meu caso foi "ObsidianSync". Dê enter.

> A seguir a melhor opção é deixar essa ultima parte em branco e dê enter para concluir. 

Prontinho seu repositório já vai estar pronto para subir!

> use ctrl + P para abrir o menu de pesquisa e digite "commit

_____

### Para  deixar o commit e pull automáticos


> Vá até settings, plugin Git e altere os seguintes campos 
> ![[Linkar Obsidian ao Github-20260527112322430.png|684]]
> 
 Deixe a quantidade em minutos que deseja para atualizar os commits

>Também considero positivo deixar essa opção acionada 
![[Linkar Obsidian ao Github-20260527112440612.png]]