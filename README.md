# Configuração do MySql no Windows
 
Como configurar o MySQL no windows. E usar nas aplicações Django.

Primeiro você que não tem o MySQL instalado no seu Windows. Veja esse vídeo abaixo.

[https://www.youtube.com/watch?v=8c4WqGP3cvU](https://www.youtube.com/watch?v=8c4WqGP3cvU)

Primeiro, gosto de usar o mysql [https://dev.mysql.com/downloads/installer/](https://dev.mysql.com/downloads/installer/)

Faça uma instalação modo dev. Completa. No momento da instalação vai pedir para colocar a senha de um root. Não se esqueça de colocar. Feito isso pode avançar com as opções e finalizar normalmente. 
 
Abra o terminal do mysql. Entre com sua senha root que você criou no momento da instalação. 

Vamos fazer 3 passos para criar um banco de dados.

1 - Criar o banco de dados. Onde está *mynamedb* é nome do seu database pode ser qualquer um.

```sql
CREATE DATABASE saturno CHARACTER SET = utf8mb4 COLLATE utf8mb4_unicode_ci;
```

Para visualizar `show databases;`

2 - Vamos criar uma senha para esse banco de dados que acabamos de criar. Onde está *myuser* criar um usuario e *mypassword (com aspas simples)* colocar uma senha **poderosa**. (se for base de teste pode usar 123123 rsrs). 

Antes de criar o usuário pode ser os que já tem.

```sql
use mysql;
select user,host from user;
```

Para criar usuário.

```sql
CREATE USER 'jedi'@'localhost' IDENTIFIED WITH mysql_native_password BY 'jedi123123@';
```

3 - Nessa etapa vamos aplicar as permissões de acesso para esse usuario que criamos. O que ele pode fazer no banco de dados. Nesse caso eu coloquei todos os direitos. 

```sql
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,CREATE TEMPORARY TABLES,DROP,INDEX,ALTER ON saturno.* TO 'jedi'@'localhost';
ou
GRANT ALL PRIVILEGES ON saturno.* TO 'jedi'@'localhost' WITH GRANT OPTION;
```

**é praticamente isso**, ai para usar esse banco de dados nas suas aplicações Django. Basta colocar essas configuraçoes.  

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'mynamedb',
        'USER': 'myuser',
        'PASSWORD': 'mypassword',
        'HOST': 'localhost',
        'PORT': '3306',
        'OPTIONS': {
        'charset’: ’utf8mb4’,
        'init_command': "SET sql_mode='STRICT_TRANS_TABLES'",
        }
    }
}
```

Para usar o Mysql Workbench como plataforma para gerenciar suas databases. A configuração é bem simples. 

Criar uma nova conexão. Com suas credenciais e clica em Ok. 

Não tenho nenhuma tabela criada. Mas é isso.
