# Django
## Ambiente
Instale o Pyenv

Instale uma versão atual do python ```pyenv install 3.9.10``` (por exemplo)

Defina e configure um diretório de trabalho

Crie um diretório ```mkdir meu_projeto```

Acesse o diretório recém criado ```cd meu_projeto```

Defina a versão padrão do python para este projeto ```pyenv local 3.9.10```.

Para verificar se funcionou, execute ```python -V``` e a resposta tem que ser a mesma utilizada no **pyenv local** (3.9.10 no exemplo anterior)

Crie um ambiente virtual para o projeto ```python -m venv .venv``` 

> Esta técnica é utilizada para criar um contexto para a aplicação, ou seja todas as dependencias serão vinculadas somente ao projeto, não influenciando no sistema operacional ou em outros projetos.

Ative o ambiente virtual criado ```source .venv/bin/activate```

> A partir deste momento aparecerá um *(.venv)* antes do seu nome_de_usuário@hostname. Este é o indicativo de que o virtualenv está ativado.

## Instalação e configuração
Dentro do seu diretório do projeto, com o *virtualenv* ativado faça o seguinte:

Instale o django
```shell 
pip install django==3.2.14
```
Uma vez que o django esteja instalado, o comando **django-admin** será disponibilizado. É a partir deste comando que serão realizadas ações envolvendo a estrutura do django.

Crie o projeto básico
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
Execute o projeto
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
4. Após criado o projeto, crie um app. Dentro do Django é uma boa prática subdividir seu projetos em vários apps desacoplados. Para o inicio de desenvolvimento, crie um app chamado **core** dentro da pasta do django (no exemplo é nome_do_projeto)

```shell 
cd nome_do_projeto
django-admin startapp core
```
Neste ponto a estrutura terá um diretório a mais e, dentro dele, alguns arquivos. Note que o app fica dentro do diretório do projeto.
```shell 
.
├── db.sqlite3
├── manage.py
└── nome_do_projeto
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

Configure o ambiente do projeto

Instale e inclua o python-decouple

Instale e inclua o dj-database-url
    
Crie um arquivo .env
    
Configure a variável de ambiente SECRET_KEY
    
Configure a variável de ambiente DEBUG
    
Configure a variável de ambiente DATABASE_URL
    
Configure a variável de ambiente ALLOWED_HOSTS

Configure STATIC_ROOT = usando os.path.join(BASE_DIR, 'staticfiles')
        
Utilizar, temporariamente, o dj_static (instalar pip install dj-static, incluir no wsgi.py e envolver o get_wsgi_application() com o Cling importado do dj_static)
    
Em INSTALLED_APPS: 
    
Adicione uma linha configurada da seguinte forma 'meusite.core.apps.CoreConfig,' (atente para a vírgula no final). **meusite** é o nome do seu projeto django e **core** é o nome do app. 
    
Encontre o arquivo apps.py, contido dentro do diretório **core** (é sempre **nome_do_projeto/nome_do_app/apps.py**). Neste arquivo altere o atributo *name* com o valor **nome_do_projeto.core**, ou seja, fica assim: ``` name = 'meusite.core'

Salve as dependências
```shell
pip freeze > requirements.txt
```
A partir deste momento as dependências do projeto estarão armazenadas no arquivo requirements.txt

Criando a primeira página

No arquivo urls.py, adicione uma nova rota da seguinte forma:
```python
# Adicione esta linha
import meusite.core.views
# Inclua esste path à lista de urlpatterns
    path('', meusite.core.views.home),
```
O trecho alterado faz a configuração que redireciona as requisição feitas à página inicial para o método **home** presente no arquivo views.py

O arquivo **views.py**, localizado dentro do diretório **core** deve conter a seguinte função:

```python
# ...
def home(request):
    return render(request,'index.html')
```

Dentro de **core** crie um diretório chamado **templates** e, dentro dele, um arquivo **index.html**. Dentro do arquivo, crie um conteúdo básico html.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Projeto Exemplo</title>
</head>
<body>
    Projeto Exemplo
</body>
</html>
```
Para melhorar a organização, crie um arquivo urls.py dentro do diretório core. Dentro do arquivo crie o seeguinte código:
