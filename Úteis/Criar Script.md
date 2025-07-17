
## primeiro uma introdução!

se você digitar:

```jsx
$ which bash
```

provavelmente aparecerá a seguinte saida 

```jsx
/usr/bin/bash
```

isso significa que poderá usar esse tutorial independente de sua Distro ou SO

### muito bem

você pode ir em algum lugar específico para ficar mais organizado, mas realmente tanto faz. Eu irei para documentos e criar uma pasta de script 

```jsx
$cd Documentos

$mkdir scripts

$cd script
```

agora a criação do script, usarei o comando nano

```jsx
$nano hello.sh
```

deve abrir o seguinte plano.

![Untitled](TI/Vida%20de%20T%20I/Criar%20Script/Untitled.png)

agora digite o caminho do bash e depois qualquer coisa que quiser, eu só irei dizer “hello world”  

```jsx
#!/usr/bin/bash

echo "hello world!"
```

agora para salvar digite crtl + x

(o comando q! força a saida sem salvar)

ele perguntará se quer modificar o arquivo, pode clicar em Y ou S dependendo da linguagem que usar.

depois perguntará se quer mudar o nome do arquivo, se quiser que continue o mesmo basta clicar em Enter.

se digitar o comando:

```jsx
$ls -al
```

conseguirá ver os documentos na pasta:

![Untitled](TI/Vida%20de%20T%20I/Criar%20Script/Untitled%201.png)

no meu caso tinha esses dois.

agora vamos deixar o script executável 

qualquer um desses dois comando faz isso 

```jsx
$chmod +x hello.sh

$chmod 755 hello.sh
```

agora se digitar o comando que mostra os arquivos na pasta 

```jsx
$ls -al
```

verá que o arquivo mudou para a cor verde:

![Untitled](TI/Vida%20de%20T%20I/Criar%20Script/Untitled%202.png)

a  seguir para executar o script digite:

```jsx
$./hello.sh
```

e prontinho!

![Untitled](TI/Vida%20de%20T%20I/Criar%20Script/Untitled%203.png)