# Django
## Ambiente
1. Instale o Pyenv
2. Instale uma versão atual do python ```pyenv install 3.9.10``` (por exemplo)
3. Defina e configure um diretório de trabalho

    3.1. Crie um diretório ```mkdir meu_projeto```

    3.2. Acesse o diretório recém criado ```cd meu_projeto```

    3.3. Defina a versão padrão do python para este projeto ```pyenv local 3.9.10```.

        3.3.1. Para verificar se funcionou, execute ```python -V``` e a resposta tem que ser a mesma utilizada no **pyenv local** (3.9.10 no exemplo anterior)

    3.4. Crie um ambiente virtual para o projeto ```python -m venv .venv``` 

    > Esta técnica é utilizada para criar um contexto para a aplicação, ou seja todas as dependencias serão vinculadas somente ao projeto, não influenciando no sistema operacional ou em outros projetos.

    3.5. Ative o ambiente virtual criado ```source .venv/bin/activate```

    > A partir deste momento aparecerá um *(.venv)* antes do seu nome_de_usuário@hostname. Este é o indicativo de que o virtualenv está ativado.

## Instalação e configuração
Dentro do seu diretório do projeto, com o *virtualenv* ativado faça o seguinte:

1. Instale o django
```shell 
pip install django==3.2.14
```
Uma vez que o django esteja instalado, o comando **django-admin** será disponibilizado. É a partir deste comando que serão realizadas ações envolvendo a estrutura do django.

2. Crie o projeto básico
```shell 
django-admin startproject nome_do_meuprojeto .
```
Neste ponto a estrutura do projeto é a seguinte:
```shell 
.
├── manage.py
└── nome_do_projeto
    ├── asgi.py
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

3. Criado o projeto, crie um app. Dentro do Django é uma boa prática subdividir seu projetos em vários apps desacoplados. Para o inicio de desenvolvimento, crie um app chamado **core** dentro da pasta do django (no exemplo é nome_do_projeto)

```shell 
cd nome_do_projeto
django-admin startapp core
```
Neste ponto a estrutura terá um diretório a mais, com alguns arquivos.
```shell 
.
├── db.sqlite3
├── manage.py
└── nome_do_rojeto
    ├── asgi.py
    ├── core
    │   ├── admin.py
    │   ├── apps.py
    │   ├── __init__.py
    │   ├── migrations
    │   │   └── __init__.py
    │   ├── models.py
    │   ├── tests.py
    │   └── views.py
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py

```
4. Execute o projeto
Para executar o projeto e ver a página inicial de confirmação, execute o seguinte comando:
```shell
python manage.py runserver
```
Se tudo correu bem, acesse a url informada no terminal (geralmente http://127.0.0.1:8000/ )

```shell
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
July 13, 2022 - 14:10:03
Django version 3.2.14, using settings 'nome_do_projeto.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

5. Configure o ambiente do projeto

    5.1. Instale e inclua o python-decouple

    5.2. Instale e inclua o dj-database-url
    
    5.3. Crie um arquivo .env
    
    5.4. Configure a variável de ambiente SECRET_KEY
    
    5.5. Configure a variável de ambiente DEBUG
    
    5.6. Configure a variável de ambiente DATABASE_URL
    
    5.7. Configure a variável de ambiente ALLOWED_HOSTS

    5.8. Configure STATIC_ROOT = usando os.path.join(BASE_DIR, 'staticfiles')
        
        5.8.1. Utilizar, temporariamente, o dj_static (instalar pip install dj-static, incluir no wsgi.py e envolver o get_wsgi_application() com o Cling importado do dj_static)
    
6. Salve as dependências
```shell
pip freeze > requirements.txt
```