
#### Comandos bash
##### 1. **`scrapy crawl`**
- Assume que a spider está registrada em um **projeto Scrapy válido**
- 
- Requer:
    - Arquivo `scrapy.cfg` na raiz do projeto
    - Spider definida em `spiders/` com `name = "nome_execução"`
    - Estrutura básica de projeto (settings.py, **init**.py, etc.)

- Usa as configurações do projeto (settings.py)


##### 2. **`scrapy runspider`**
- Espera um arquivo de spider **auto-contido**
- Não reconhece:
    - Caminhos relativos complexos (`Path(__file__).resolve().parent.parent.parent`)
    - Configurações personalizadas do projeto
    - Dependências de outros módulos do projeto

- Falha comum quando a spider:
    
    - Usa `__init__` para configurações
    - Depende de settings.py
    - Precisa de estrutura de pastas específica


### Resumo

|Comando|Melhor Para|Requisitos|Limitações|
|---|---|---|---|
|`crawl`|Projetos completos|Estrutura Scrapy válida|Precisa de configuração prévia|
|`runspider`|Spiders avulsas/rápidas|Arquivo auto-contido|Sem acesso a settings.py|
Use `crawl` para seu projeto e `runspider` apenas para testes isolados.

-----
