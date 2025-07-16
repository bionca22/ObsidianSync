# Requirements

import pandas as pd
import numpy as np
import os
import re
from google_api import get_address


# Extrair URLs

```spiders/extrair_urls.py```

```bash
scrapy crawl extrair_urls -o json_txt/urls.json && python json_txt/json_txt.py
```

>[!info] 
>Esse comando roda a spider "extrair_urls" e se não der erros, roda o script json_txt.py para criar o arquivo links_imoveis.txt

```python
base_url = "https://www.dfimoveis.com.br/venda/df/ceilandia/ceilandia-norte/casa"
```

A variável ```base_url``` é a pagina onde serão extraídos os links dos anúncios. 
a função ```def_parse() ```  faz um loop na pagina percorrendo da pagina 1 à ultima disponível, extraindo os links da seguinte forma:

```python
links_imoveis = [
            f"https://www.dfimoveis.com.br{link}" for link in links if link.startswith("/imovel/")
        ]

```


![[brave_H9y2Xu1y6S.png]]
![[brave_wZuPfeqMY6.png]]

>[!info]
O resultado é um arquivo json com os links extraidos separados por página

# Formatar Json para txt com um link por linha

```json_txt.py``` -> Formata o arquivo Json gerado na etapa anterior para ficar um link por linha no arquivo ```links_imoveis.txt```

# Extrair info

```extrair_info.py```


Criou-se um data frame ```df``` com os dados do arquivo ```links_imoveis.txt``` em uma coluna chamada "links"

```python
df = pd.read_csv("./json_txt/links_imoveis.txt", header=None, names=["links"]) 
```

Carregou data frame em uma lista ```start_urls``` 


A função ```parse()``` faz um loop nos itens da lista ```start_urls``` raspando os dados dos seletores css.

Regex é utilizado para formatar valores extraídos (remover espaços, filtrar caracteres, procurar palavras específicas, cortar strings...)


> [!info]
> As configurações de raspagem podem ser editadas no arquivo ```settings.py```.
> Verificar a documentação do scrapy!
> 
> Essas configurações são importantes para não prejudicar o site raspado com requisições em excesso. Nem ter o IP banido do servidor.
> 
> Essas configurações vão regular o delay, a frequência e o numero de requisições simultâneas (dentre outras opções mais complexas como "middlewares")



Essa spider é executada com o seguinte comando:

```bash
scrapy crawl extrair_info -o resultados/imoveis.csv
```

após a execução é gerado um arquivo na pasta resultados com nome ```imoveis.csv```

# 📂Estrutura das Pastas 
├── __init__.py
├── items.py
├── middlewares.py
├── pipelines.py
├── settings.py
└── spiders
    ==├── extrair_info.py==
    ==├── extrair_urls.py==
    ├── __init__.py
    ├── json_txt
    │   ├── json_txt.py
    │   ├── links_imoveis.txt
    │   └── urls.json
    ├── resultados
    │   ├── imoveis.csv
    │   └── imoveis.ods
    ==└── tratar==
        ==├── google_api.py==
        ==├── processamento.py==
        ==└── tratamento.py==

[^1]: 
