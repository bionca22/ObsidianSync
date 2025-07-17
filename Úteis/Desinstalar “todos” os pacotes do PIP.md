
```
pip freeze > requirementstmp.txt

```

Isso vai gerar um arquivo `requirementstmp.txt`.

Com este arquivo basta desinstalar todos os pacotes:

```
pip uninstall -r requirementstmp.txt -y

```

Também pode ser resolvido fazendo a remoção do 
ambiente virtual e criar ele novamente. Para executar estes passos estou
 supondo que está com o ambiente virtual ativo.

```
deactivate
rm -rf <diretório-do-ambiente-virtual>

```

E depois criar o ambiente virtual novo

```
python -m venv <novo_venv>
source <novo_venv>/bin/activate

```