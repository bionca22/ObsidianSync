criado em 2022

a versão python 3.11 nessa distribuição é muito sensível e pode vir a gerar problemas, uma solução é trocar aversão utilizada do python. aqui vamos usar a versão 3.8

## instalar pacotes requeridos

```jsx
$sudo yum install gcc openssl-devel bzip2-devel libffi-devel zlib-devel
```

## baixar python3.8

```
$cd /opt
$wget https://www.python.org/ftp/python/3.8.12/Python-3.8.12.tgz
```

agora extraia o pacote

```jsx
$tar xzf Python-3.8.12.tgz
```

## compile o python

```
$cd Python-3.8.12
$sudo ./configure --enable-optimizations
$sudo make altinstall
```

-usamos o altinstall para previnir uma substituição abrupta da versão binaria padrão 

agora já pode remover a sorce archive file 

```jsx
$sudo rm Python-3.8.12.tgz
```

## check a versão

```jsx
$python 3.8
```

## agora vamos dar uma olhada nos link lógicos

```jsx
$ls -la /usr/bin/python*
```

provavelmente sairá alguma coisa como

```jsx
lrwxrwxrwx. 1 root root    18 Jan 30 11:37 /usr/bin/python -> /usr/bin/python3.11
lrwxrwxrwx. 1 root root    10 Jan 12 09:11 /usr/bin/python3 -> python3.11
```

então precisamos redefini-los para a versão 3.8

submeta um comando após o outro

```jsx
#para o python
$alias python='/usr/bin/python3.8'

#e para o python3
$sudo ln -sf /usr/bin/python3.8 /usr/bin/python3
```

deve resolver!