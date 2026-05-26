
#### Constrains

- **`pg_constraint`**: É uma tabela oculta que o Postgres mantém para saber quais regras existem (Primary Keys, Foreign Keys, Checks).
	- **`conrelid`**: Esta coluna na `pg_constraint` guarda o ID da **tabela** à qual a restrição pertence.

- **`pg_constraintdef(oid)`**: O banco armazena a regra de forma interna. Essa função é o "tradutor" que reconstrói o comando `CHECK (valor > 0)`, por exemplo.

- **O Catálogo Nativo (`pg_catalog`)**: Este é o "cérebro" do PostgreSQL. É onde ficam as tabelas que começam com `pg_`. Elas são extremamente rápidas e detalhadas, mas usam nomes técnicos e muitas vezes precisam de funções como a `pg_constraintdef()` que você viu para se tornarem legíveis.
	As principais para investigação são:

- **`pg_class`**: O coração do catálogo. Contém entradas para cada tabela, índice, view e sequência do banco. Ele começa por aqui para achar o `oid` (o ID único) da tabela.
- **`pg_attribute`**: Guarda informações sobre as colunas (atributos) de cada tabela.
- **`pg_constraint`**: Como você descobriu, armazena todas as restrições (chaves primárias, estrangeiras e checks).
- **`pg_index`**: Detalhes técnicos sobre como os índices estão montados.
- **`pg_description`**: Onde ficam guardados os comentários (o comando `COMMENT ON...`) que os desenvolvedores deixam nas tabelas.

- **information_schema.referential_constraints:** Focada especificamente em entender as relações de Foreign Keys.

- **pg_catalog**: quando precisa de uma investigação profunda ou automatizar algo via script, pois ele dá acesso a IDs internos (`oid`) que permitem cruzar informações de forma muito precisa. Já o `information_schema` é ótimo para relatórios rápidos e legíveis sobre a estrutura.

- **::regclass** Em vez de você ter que descobrir qual é o número de ID da tabela `famga.fg_comite`, você escreve o nome dela entre aspas e usa `::regclass`. O banco converte automaticamente o nome para o ID interno (OID) daquela tabela específica.

#### Querys