## Atalhos

### Terminal

| limpa o terminal          | Ctrl + L |                                                                                                                                                                                                        |
| ------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| move p/ inicio da linha   | Ctrl + A |                                                                                                                                                                                                        |
| move p/ final da linha    | Ctrl + E |                                                                                                                                                                                                        |
| apaga a linha             | Ctrl + U |                                                                                                                                                                                                        |
| apaga do cursor em diante | Ctrl + K |                                                                                                                                                                                                        |
| apaga uma palavra         | Ctrl + W |                                                                                                                                                                                                        |
| cola de volta             | Ctrl + Y | Isto irá colar o texto apagado que você viu com os atalhos Ctrl + W,Ctrl + U e Ctrl + K. Vem à mão no caso de você ter apagado o texto errado ou se você precisar usar o texto apagado em outro lugar. |
| segundo plano             | Ctrl + Z | Este atalho irá enviar um programa em execução em segundo plano. Normalmente, você pode conseguir isso antes de executar o programa usando a opção &, mas se você esqueceu de fazer isso.              |
| Comando “alias”           |          | Você digitou uma combinação de comandos legais que tem que repetir sempre? Use o comando alias para criar seu próprio atalho:                                                                          |

![exemplos comando alias](TI/Vida%20de%20T%20I/Básico%20do%20Linux/Untitled.png)

exemplos comando alias

### S.O

| Alternar entre aplicativos | Super+Tab ou o Alt+Tab |
| --- | --- |
| Bloquear a tela | Super+L ou Ctrl+Alt+L |
| Minimizar janelas abertas | Super+D ou Ctrl+Alt+D |
| Fechar todas as janelas | Ctrl+Q ou Ctrl+W. |
| Encerrar sessão (desligar) | Ctrl+Alt+Del |
| Redimensionar uma janela  . | Alt + F8  Arraste com o mouse para cima e para baixo, esquerda e direita para redimensionar a janela. |

### comandos básicos

entra e sai do diretório
```bash
$ cd {diretório}
$ cd .. (volta um pouco)
$ cd ~ (volta pra raiz da pasta)
```

Copia o caminho do diretório
```
$ pwd
```

abre o arquivo no editor de texto padrão gedit
```bash
 gedit {arquivo} 
```

muda nome do arquivo
```bash
 mv {nome_do_arquivo} {novo_nome_do_arquivo}
```

mostra conteúdo da pasta 
```bash
 ls
```


apaga arquivos
```bash
 rm
```

apaga a pasta, aqui “f” força a deleção de qualquer arquivo, porém somente o r basta dependendo dos arquivos r = recursivo f = forçar
```bash
 rm -rf {nome_da_pasta}
```

Mostra os processos em execução
```bash
 top
```

####  👩🏻‍💻 Copia a estruturação das pastas no VSCode
```bash
$ tree
```


## comandos levemente avançados com localização

```bash
 cd {pasta}/{arquivo}/{pasta_diferente}/. 
```

 copia o seguinte arquivo para outra pasta. O ponto no final indica que ele será colocado nessa pasta, não subistituido.

```bash
 cd ../{pasta_no_mesmo_diretorio}
```

volta o caminho já entrando em uma pasta de mesmo diretório 

```bash
 ls ../{pasta_no_mesmo_caminho}
```

possibilita voltar uma passo e ver o que tem dentro e outras pasta na mesma pasta. também funciona para $mv

![confuso? talvez essa imagem ajude](TI/Vida%20de%20T%20I/Básico%20do%20Linux/Untitled%201.png)

confuso? talvez essa imagem ajude

```bash
mv minha_primeira_pasta/arquivo minha_segunda_pasta/.
```

mv quando usado para arquivos que estão em pastas diferentes, move o arquivo entre elas, equivalente ao cortar e colar

```bash
mv ../{minha_segunda_pasta} {arquivo} ../{minha_segunda_pasta}/{arquivo_será_renomeado}
```

aqui estou mudando o **nome** de um arquivo estando em outra pasta no mesmo diretório, perceba que é necessário descrever a pasta a qual tem o arquivo duas vezes, se descrevesse apenas uma ele não iria renomear mas sim mover o arquivo para a pasta em que vc está

### Informações e elementos

![Untitled](TI/Vida%20de%20T%20I/Básico%20do%20Linux/Untitled%202.png)

![aqui estão seguidos: o n**ome do usuário** e o **grupo do usuário.**](TI/Vida%20de%20T%20I/Básico%20do%20Linux/Untitled%203.png)

aqui estão seguidos: o n**ome do usuário** e o **grupo do usuário.**

![Untitled](TI/Vida%20de%20T%20I/Básico%20do%20Linux/Untitled%204.png)

A primeira casa onde aparece um “d” e nas demais um traço, onde “d” significa diretório e traço significa arquivo, ou que não é um diretório

As três proximas letras significam seguidamente READ, WHITE e X significa poder de execução

R= 4

W= 2

X= 1

### CHMOD versus CHOWN

```bash
 chmod 777
```

onde o primeiro sete dá todas as permições para o dono do arquivo o segundo 7 dá todas as permições para esse  grupo e o terceiro 7 dá todas as permissões para qualquer pessoa que acessar.

![https://img-c.udemycdn.com/redactor/raw/2018-12-10_18-27-16-29defd757b7a679dc1232ec74e17c6f3.jpg](https://img-c.udemycdn.com/redactor/raw/2018-12-10_18-27-16-29defd757b7a679dc1232ec74e17c6f3.jpg)

**Mudando o dono de um arquivo**

```bash
 chown diego:diego arquivo.txt

 chmod -R 777 *
```

O parâmetro -R faz com que a alteração seja recursiva, isto é, afete 
todas as pastas e arquivos dentro de uma pasta especificada.

Neste exemplo o * indica tudo presente no diretório.

![Untitled](TI/Vida%20de%20T%20I/Básico%20do%20Linux/Untitled%205.png)

## Mais informações da Distro

```bash
 cat /etc/os-release
```

O arquivo /etc/os-release contém dados de identificação do sistema operacional, incluindo informações sobre a distribuição e sua versão de lançamento. Este arquivo é parte do pacote systemd e deve estar presente em todas as distribuições Linux modernas executando o systemd.

## Encontrando coisas no diretório

```bash
find / -name {nome_do_aarquivo} 2>/dev/null
```


## ssh Matheus

```bash
ssh Matheus@177.235.98.40 -p 8081
```


## man e --help


man 'comando' 
- mostra manual


