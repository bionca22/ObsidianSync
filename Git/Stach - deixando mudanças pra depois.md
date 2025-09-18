
A melhor alternativa para deixar de trabalhar, temporariamente, em mudanças incompletas é usar o comando **`git stash`**. Ele pega todas as alterações não-commitadas e as armazena em uma pilha temporária, limpando o seu diretório de trabalho. Isso permite que você mude de branch, corrija um bug rápido ou trabalhe em outra coisa sem perder suas mudanças.

1. **Salve suas mudanças incompletas:** Estando na sua branch de trabalho (`minha-feature`, por exemplo), use o comando:

```bash
git stash push -m "Início da feature X, alteração incompleta"
```

 O comando irá "limpar" sua branch, deixando-a exatamente como estava no último commit. As mudanças salvas ficarão seguras na pilha de `stashes`.

2. **Mude de branch e faça o que precisar:** 

```bash
git checkout main
```


 Agora que sua branch está limpa, você pode voltar para a `main`, criar uma nova branch, ou fazer o que for necessário.
 
 
3. **Volte para a sua branch e restaure as mudanças:** Quando estiver pronto para continuar seu trabalho na branch original, volte para ela e restaure as mudanças que você salvou.

```bash 
git checkout minha-feature
git stash pop
```

 O comando `pop` irá restaurar as alterações e remover o "stash" da pilha, deixando seu código exatamente como estava antes.


A principal vantagem de usar o `git stash` é que ele mantém o histórico do seu código limpo, evitando que você precise fazer commits com mensagens como "trabalho em progresso" ou "quase pronto".