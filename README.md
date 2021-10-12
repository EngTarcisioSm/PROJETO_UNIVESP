# CRIAÇÃO DO PROJETO DJANGO

## VERIFICAÇÃO DA VERSÃO PYTHON
* No prompt comando do windows ou no próprio terminal do editor de código, digitar o comando abaixo:
     ~~~python
     python --version 
     ~~~
* Após digitar isso o sistema retornará como output a versão do Python instalada.
     * Para que esse código funcione é necessário que o python esteja instalado caso o sistema operacional seja Windows, e com as variáveis de ambiente configuradas corretamente. Em distribuições linux o python costuma vir instalado em sua versão estável.

## INSTALAÇÃO DO FRAMEWORK DJANGO
* A instalação descrita abaixo não será utilizado ambientes virtuais para que o processo se torne o mais simples possivel apesar de ser recomendado a instalação com ambientes virtuais.
* No terminal digitar o seguinte comando 
     ~~~python
     pip  install django
     ~~~
* Verificar se o Django foi instalado corretamente e verificar a versão instalada e de uso.
     ~~~python
     python -m django --version
     ~~~
     * Será retornado a versão do módulo caso a instalação tenha sido instalada corretamente 
* Em projetos com multiplos participantes é necessário e recomendavel a instalação de uma versão comum do módulo. Para instalar uma versão específica do módulo segue abaixo o código integrado ao exemplo da instalação da versão 3.2.7
     ~~~python 
     pip install django==3.2.7
     ~~~
     * No exemplo acima a versão instalada foi a versão 3.2.7

## CRIAÇÃO DE PROJETO DJANGO
* No exemplo abaixo será criado um projeto django criando também uma template simples para o projeto bem como a página home do projeto.
* PASSO_01: Criar uma pasta para o projeto em um diretório de preferencia 
* PASSO_02: Através do cmd do Windows ou Terminal do editor de código acessar  a pasta principal do projeto criada no passo acima, tendo a seguinte aparencia no terminal 
     ~~~
     C:\projetos\python\django_example> 
     ~~~
     * O caminho acima é apenas um exemplo podendo variar do usuário para usuário se tratando apenas de um exemplo
* PASSO_04: Iniciando o projeto django com o comando abaixo no terminal com os passos anteriores feitos
     ~~~python 
     django-admin startproject meu_projeto .
     ~~~
     * No código acima "meu_projeto" se refere ao nome do projeto;
     * O ".' ao final do código é uma instrução que reduz a complexidade de diretórios criados pelo django
     * Alguns nomes e simbolos não são aceitos para nomes em projetos django 
     * Ao criar um projeto com sucesso uma pasta com o nome do projeto será criada  
* PASSO_05: Verificar se o projeto esta criado corretamente subindo um servidor local do projeto criado 
     * No terminal digitar:
          ~~~python 
          python manage.py runserver
          ~~~
     * Caso o projeto seja criado com sucesso será exibido a seguinte mensagem de output 
          ~~~
          Watching for file changes with StatReloader
          Performing system checks...

          System check identified no issues (0 silenced).

          You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.        
          Run 'python manage.py migrate' to apply them.
          October 12, 2021 - 07:18:06
          Django version 3.2.7, using settings 'meu_projeto.settings'
          Starting development server at http://127.0.0.1:8000/
          Quit the server with CTRL-BREAK.
          ~~~
     * clicando no link apresentado acima "http://127.0.0.1:8000/" será apresentado uma tela default do projeto django criado com sucesso.
* PASSO_06: Observação I
     * Todo site possui uma identidade visual que acompanha o site em todas suas páginas;
     * O django oferece suporte para esse template e até certo ponto facilitando esse processo, de contra partida ele também apresenta caracteristicas peculiares do proprio framework no existe de certa forma um html modificado na criação de aplicações com django
* PASSO_07: Criação da página template 
     * Dentro da pasta principal do projeto (aquela que leva o nome do projeto criado), criar uma pasta interna a esta com o nome de paginas
     * Dentro deste diretório criar uma pagina html que seráo template de todo o projeto, neste exemplo esse template leva o nome de base.html
* PASSO_08: Observação II
     * O template criado conta com regiões chamados de blocos ("blocks") onde ocorre a inserção de código dentro do html 
          ~~~python 
          {%block 'nome_do_bloco'%}{%endblock%}
          ~~~
          * Exemplo de um html composto por blocos django 
               ~~~html
               <!DOCTYPE html>
               <html lang="pt-BR">
                    <head>
                         <meta charset="UTF-8">
                         <meta http-equiv="X-UA-Compatible" content="IE=edge">
                         <meta name="viewport" content="width=device-width, initial-scale=1.0">
                         <title>{%block 'titulo'%}{%endblock%}</title>

                         <style>
                              body {
                                   font-size: 40px;
                                   font-family: Arial, Helvetica, sans-serif;
                                   background-color: brown;
                                   color: whitesmoke;
                              }
                         </style>
                    </head>
                    <body>
                         {%block 'conteudo'%}{%endblock%}     
                    </body>
               </html>
               ~~~
* PASSO_09: Criação de um app HOME 
     * No cmd ou terminal apontado para a pasta do projeto digitar o seguinte código 
          ~~~python
          python manage.py startapp home
          ~~~
     * Ao criar um novo app django (é assim como uma sessão de um site é chamado no django) uma nova pasta aparece no diretorio do projeto com o nome do app criado "home" é importante que os nomes sejam sempre em letra minuscula (apenas por convenção)
* PASSO_10: Observação III
     * Algumas descrições a partir dos proximos passos não serão tão aprofundadas com o objetivo de não alongar demais o tutorial 
* PASSO_11: Registro do app criado dentro do projeto 
     * O registro do app criado deve ser feito dentro do arquivo settings.py dentro do diretório principal do projeto "meu_projeto"
     * Dentro da linguagem de programação python não existe constantes, quando uma variável tem seu nome em letra maiuscula por convenção a comunidade encara essa variavel como uma constante 
     * Dentro de settings.py existe uma constante chamada INSTALLED_APPS, inserir o aplicativo criado com a seguinte linha 
          ~~~python 
          'home.apps.HomeConfig',
          ~~~
          ~~~python 
          #INSTALLED_APPS antes da inserção do novo app
          INSTALLED_APPS = [
               'django.contrib.admin',
               'django.contrib.auth',
               'django.contrib.contenttypes',
               'django.contrib.sessions',
               'django.contrib.messages',
               'django.contrib.staticfiles',
          ]
          #INSTALLED_APPS depois da inserção do novo app
          INSTALLED_APPS = [
               'django.contrib.admin',
               'django.contrib.auth',
               'django.contrib.contenttypes',
               'django.contrib.sessions',
               'django.contrib.messages',
               'django.contrib.staticfiles',
               'home.apps.HomeConfig',
          ]
          ~~~
* PASSO_12: Cadastro da página home dentro do arquivo urls.py (do diretório principal)
     * PASSO_12.1: Inserção de módulos necessários "include" e de views do novo app home 
          ~~~python 
          from django.urls import path, include
          from home import views
          ~~~
     * PASSO_12.2: Inserção do caminho para views do app home dentro do dicionario urlpatterns
          ~~~python 
          urlpatterns = [
               path('', views.index),
               path('admin/', admin.site.urls),
          ]
          ~~~
* PASSO_13: Criação da função que trata da requisição html e da renderização da página 
     ~~~python 
     from django.shortcuts import render

     # Create your views here.
     def index(request):
          return render(request, 'home/index.html')
     ~~~
* PASSO_14: Criar diretório templates/home dentro do app home 
* PASSO_15: Criar dentro do diretório templates/home o arquivo index.html
* PASSO_16: Dentro do arquivo home será inserido o conteúdo que deve conter dentro da pagina principal do projeto.
     * O conteúdo desse arquivo não é um html padrão e sim obedece a lógica do framework django
     * O visual da pagina será fornecido pelo arquivo base.html alocado dentro do diretorio principal
     * Conteúdo do arquivo index.html do home do projeto 
          ~~~html
          {%extends 'base.html'%}

          {%block 'titulo'%}
          TITULO DA MINHA HOME =D
          {%endblock%}

          {%block 'conteudo'%}
          <h1>Olá eu sou a HOME =D</h1>h1>
          <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Magnam sequi tempora perferendis officiis maxime vero natus, ducimus quam. Ut, sunt nulla esse accusamus culpa architecto dolores. Quaerat non sint optio.</p>
          {%endblock%}
          ~~~
* PASSO_17:
     * Incluir o caminho da template para o projeto principal 
     * Em settings nA constante TEMPLATES existe um campo de dicionário chamado 'DIRS' onde deve ser especificado o local onde a pagina de template esta alocada
     * O Django recentemente deixou de utilizar o modulo os para especificar caminhos o import do modulo os pode ainda ser feito pelo usuário para simplificar isso.  
     * Importando o modulo os 
          ~~~ python
          import os
          ~~~  
     * Inclusão do caminho 
          ~~~python 
          TEMPLATES = [
               {
                    'BACKEND': 'django.template.backends.django.DjangoTemplates',
                    'DIRS': [os.path.join(BASE_DIR,'paginas')], 
                    'APP_DIRS': True,
                    'OPTIONS': {
                         'context_processors': [
                              'django.template.context_processors.debug',
                              'django.template.context_processors.request',
                              'django.contrib.auth.context_processors.auth',
                              'django.contrib.messages.context_processors.messages',
                         ],
                    },
               },
          ]
          ~~~
          * Alteração de DIRS

