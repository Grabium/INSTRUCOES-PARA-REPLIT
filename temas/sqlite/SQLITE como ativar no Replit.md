# Como conectar o SQLite3 ao Laravel no Replit sem erros!

Como usar o SQLite3 de uma forma prática no Replit Laravel com poucos passos:

## **Passo 1 - Crie o banco de dados:**
Antes, intale o **sqlite.bin**:
```
sqlite3
```
Uma vez dentro do prompt do sqlite3, irá aparecer **" sqlite> "**. Digite

```
.open NomeDoBancoDeDados.db
```
Pronto. O banco de dados aparecerá na pasta raiz do projeto.

&nbsp;
Saia com **" .quit "** para seguir o tutorial.

## **Passo - 2 - Descubra o caminho absoluto do BD:**
Você pode querer mudar o local do DB ou ele já pode ter sido criado antes, ou pode estar desenvolvendo num servidor como Replit. Será necessário obter o caminho absoluto para funcionar corretamente. Provavelmente será algo do tipo (no linux):

&nbsp;
**/home/runner/Nome-do-projeto/NomeDoBancoDeDados.db**

&nbsp;

Para ter certeza, no cmd, acesse o Tinker e depois chame o método base_path():
```
php artisan tinker
$var = base_path('NomeDoBancoDeDados.db');
```
Caso o banco esteja em uma pasta (que não seja a raiz do projeto) como "database", por exemplo, siga o modelo:
```
$var = base_path('database/NomeDoBancoDeDados.db');
```
Mantenha o cmd a vista mas pode sair do tinker com **" exit "**.


## **Passo 3 - configure o " .laravel.env: "**
 Talvez o arquivo não apareça porque esteja oculto. O Replit tem sua plataforma no linux. Então confirme o nome do arquivo fazendo a listagem dos arquivos ocultos na pasta raiz do projeto:
 ```
ls -a
 ```
confirme a presença do arquivo  **" .laravel.env "** e o renomeie retirando o ponto:
 ```
mv .laravel.env laravel.env
 ```
Agora o arquivo está visível.


- Atualize o driver de conexão;
- Indique o endereço absoluto do banco incluindo a extenção;
- Para chave estrangeira, adicione a cláusula **DB_FOREIGN_KEY=true**.

```
DB_CONNECTION=sqlite
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=/home/runner/Nome-do-projeto/NomeDoBancoDeDados.db
DB_USERNAME=root
DB_PASSWORD=
DB_FOREIGN_KEY=true   
```

Esta última cláusula é para futuro uso de foreign keys, a serem programadas através das migrations no db, esta linha não vem originalmente escrita.
Após isso, retorne o então arquivo **" laravel.env "** para seu nome anterior, onde ele retorna à visibilidade oculta. O  **" .laravel.env "** .
 ```
mv laravel.env .laravel.env
 ```

## **Passo 4 - Instale o PDO da Replit:** 
Estamos falando do **Doctrine/DBAL**. Você pode forçar a instalação tentando imprimir as tabelas do bd no cmd:

```
php artisan db:show
```

O prompt irá dizer que o PDO Doctrine/DBAL ainda não está instalado e perguntar se deseja instalar. Digite **" yes "**. Então será instalada, mas o comando que você usou (php artisan db:show) ainda não será executado, mas não há problema, ele será executado no passo 5.

## **Passo 5- Instale a tabela que registra as migrations:**

Antes, Pode-se constatar que ainda não há nehnuma tabela instalada:

```
php artisan db:show
```
Nas informações deve aparecer:

>...
>
> Tables...............0
>
>...

A tabela **migrations** deve ser instalada antes de qualquer migrate rodar para registrá-las. Faça:

```
php artisan migrate:install
```
Agora veja que vai aparecer uma tabela chamada migrations.


&nbsp;
Pronto! Devidamente conectado.

# Como usar o SGBD do SQLite (prompt sqlite.bin)

Embora é recomendado, a depender do estágio do projeto, usar o Tinker (Eloquent) para alteração e query no bd, talvez, por uma questão de praticidade ou possibilidade, o desenvolvedor precise usar o **sqlite.bin**. 
Para realizar QUERIES e COMANDOS:DDL,DML,DLC,TLC e UTF acesse pelo prompt:

```
sqlite3 NomeDoBancoDeDados.db
```
## Uso do prompt:

Vai aparecer **sqlite>**.
VC pode usar estes comandos como uma interface interativa:

&nbsp;
**.help**

&nbsp;
**.quit**

&nbsp;
**.mode table**

&nbsp;
**.schema**

&nbsp;
**.table**



&nbsp;
Entre outros que vc verá em **" .help "**.

## Queries e Comandos SQL:
Para digitar QUERY ou COMANDOS SQL basta começar a digitar.
Ao clicar **`Enter`** aparecerá **" ...> "** é apenas uma nova linha. 
Para encerrar esta seção SQL basta digitar **" ; "**. Se houver uma query válida, será realizada, senão, apenas retorna à seção anterior.

