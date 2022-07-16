# curso-django-projeto1

live#01.html
Quem pode acessar

Propriedades do sistema
Tipo
HTML
Tamanho
97 KB
Armazenamento usado
97 KB
Local
Live #01 - Projeto dia organizado (Python e Django)
Proprietário
Matheus Dias
Modificado
26 de abr. de 2021 por Matheus Dias
Aberto
21:19 por mim
Criado em
29 de abr. de 2021
Sem descrição
Os leitores podem fazer o download
<!doctype html>
<html lang="en" class="h-100">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="prism.css">
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-eOJMYsd53ii+scO/bJGFsiCZc+5NDVN2yr8+0RDqr0Ql0h+rP48ckxlpbzKgwra6" crossorigin="anonymous">

    <title>Live #01</title>
  </head>
  <body class="h-100 text-left text-white bg-dark">
    <div class="container d-flex w-100 h-100 p-3 mx-auto flex-column">
      <header class="mb-auto">
        <div>
          <h3 class="float-md-start mb-0">Live #01 - Criando um organizador de tarefas com python</h3>
        </div>
      </header>
      <div style="margin-top:30px"></div>

      <h1>Passo 1: Criar e ativar o ambiente virtual do projeto</h1>
      <p>Com a distribuição do Python <b>Anaconda</b> instalada, podemos criar
        um novo ambiente virtual através do seguinte comando (executado no Prompt
        de Comando ou Anaconda Prompt):</p>

      <pre class="language-python">
        <code class="language-python">
          conda create -n dia_organizado python
        </code>
      </pre>

      <p>O comando anterior cria um novo ambiente virtual chamado "dia_organizado".
      Para ativar o ambiente criado, utilizamos o seguinte comando:</p>

      <pre class="language-python">
        <code class="language-python">
          conda activate dia_organizado
        </code>
      </pre>
      <hr>

      <h1>Passo 2: Instalar o Django no ambiente virtual criado</h2>
      <p>Com o ambiente virtual ativado, podemos baixar o Django através do pip:</p>
      <pre class="language-python">
        <code class="language-python">
          pip install django
        </code>
      </pre>
      <hr>

      <h1>Passo 3: Criar o projeto</h1>
      <p>Com as configurações iniciais realizadas, podemos criar a estrutura inicial
      do projeto através do seguinte comando:</p>
      <pre class="language-python">
        <code class="language-python">
          django-admin startproject dia_organizado
        </code>
      </pre>
      <p>O comando acima criará um novo diretório com a estrutura inicial de um projeto
      Django. Lembre-se de que a pasta será criada no diretório que estava ativo no
      momento em que o comando foi executado. Então, se você quiser criar o projeto
      em sua área de trabalho, por exemplo, primeiro precisa mudar o diretório ativado
      para o diretório da área de trabalho.</p>
      <p>Você pode navegar entre diretórios através do comando <b>cd</b> no prompt
      de Comando.</p>
      <p>O comando criará uma nova pasta, com o nome que você deu ao projeto
        (dia_organizado). Dentro dessa pasta, haverá um arquivo Python chamado <i>manage.py</i>
        e uma outra pasta, com o mesmo nome do projeto, contendo mais alguns arquivos. O projeto
        terá a seguinte estrutura:</p>
      <pre>
        <code class="language-treeview">
          dia_organizado/
          |-- dia_organizado/
          |   |-- __init__.py
          |   |-- asgi.py
          |   |-- settings.py
          |   |-- urls.py
          |   `-- wsgi.py
          `-- manage.py

        </code>
      </pre>

      <p>
        Adicione o diretório do projeto ao seu editor de texto preferido (eu
        gosto do <a href="https://atom.io/">Atom</a>) e vamos começar a programar.
      </p>
      <hr>

      <h1>Passo 4: Criar o app do projeto</h1>
      <p>
        Um projeto Django deve ser dividido em apps, onde cada app agrupa
        uma funcionalidade específica. Em nosso projeto existirá apenas um app,
        que será chamado <i>tarefas</i>. Podemos criá-lo executando o seguinte
        comando:
      </p>
      <pre class="language-python">
        <code class="language-python">
          python manage.py startapp tarefas
        </code>
      </pre>
      <p>
        Para o comando funcionar, será necessário estar com o diretório do projeto
        (aquele que contém o arquivo <i>manage.py</i>) ativo.
      </p>
      <p>
        O comando vai criar uma nova pasta com o nome do app (tarefas) dentro do
        diretório principal do projeto. Essa pasta vai conter todos os recursos
        necessários para a funcionalidade específica do app.
      </p>
      <pre>
        <code class="language-treeview">
          dia_organizado/
          |-- dia_organizado/
          |   |-- __init__.py
          |   |-- asgi.py
          |   |-- settings.py
          |   |-- urls.py
          |   `-- wsgi.py
          |-- tarefas/
          |   |-- migrations/
          |   |   `-- __init__.py
          |   |-- __init__.py
          |   |-- admin.py
          |   |-- apps.py
          |   |-- models.py
          |   |-- tests.py
          |   `-- views.py
          `-- manage.py

        </code>
      </pre>
      <p>
        Uma vez criado o app, precisamos adicioná-lo à lista de apps instalados
        presente no arquivo <i>settings.py</i>, que fica na pasta <i>dia_organizado</i>.
      </p>
      <pre data-line="11">
        <code class=" language-python">
          # dia_organizado/settings.py


          INSTALLED_APPS = [
              'django.contrib.admin',
              'django.contrib.auth',
              'django.contrib.contenttypes',
              'django.contrib.sessions',
              'django.contrib.messages',
              'django.contrib.staticfiles',
              'tarefas.apps.TarefasConfig', # novo
          ]
        </code>
      </pre>
      <hr>
      <h1>Passo 5: Criando o modelo Tarefa</h1>
      <p>
        Os modelos são utilizados para definir o esquema de dados de um projeto.
        O objetivo do nosso projeto é gerenciar tarefas, isto é, adicionar, remover
        e verificar tarefas cadastradas.
      </p>
      <p>
        Para que a nossa aplicação possa armazenar essas tarefas, é necessário que exista
        um modelo que "ensine" ao Python como uma tarefa deve ser criada, isto é,
        um modelo que define os atributos e os métodos de uma tarefa.
      </p>
      <p>
        Uma tarefa possuirá uma descrição (que descreve a tarefa em si), uma data
        de criação (quando a tarefa foi cadastrada), uma categoria ('urgente',
         'importante' ou 'precisa ser feito') e um status ('concluído', 'pendente' ou 'adiado').
      </p>
      <p>
        Todos os modelos de uma aplicação são definidos em um arquivo <i>models.py</i>,
        criado automaticamente pelo Python no momento da criação de um app.
      </p>
      <h3>Modelo tarefa</h3>
      <pre>
        <code class=" language-python">
          # tarefas/models.py


          from django.db import models

          class Tarefa(models.Model):

              OPCOES_STATUS = (
                  ('concluído', 'Concluído'),
                  ('pendente', 'Pendente'),
                  ('adiado', 'Adiado'),
              )

              OPCOES_CATEGORIA = (
                  ('urgente', 'Urgente'),
                  ('importante', 'Importante'),
                  ('precisa ser feito', 'Precisa ser feito'),
              )

              descricao = models.CharField(max_length=400)
              criacao = models.DateTimeField(auto_now_add=True)
              categoria = models.CharField(max_length=25, choices=OPCOES_CATEGORIA,
                                           default='importante')
              status = models.CharField(max_length=25, choices=OPCOES_STATUS,
                                        default='pendente')
        </code>
      </pre>
      <p>
        Outra maneira de visualizar um modelo é como uma tabela. Podemos imaginar
        que <i>Tarefa</i> é o nome de uma tabela, e que cada atributo que nós definimos
        é uma coluna dessa tabela. Uma vez que o modelo está definido, ou, uma vez
        que a tabela está criada, nós podemos adicionar os objetos nela, isto é, podemos
        adicionar as tarefas em si.
      </p>
      <table class="table table-dark table-striped">
        <h3>Tarefas</h3>
        <thead>
          <th>Descrição</th>
          <th>Criação</th>
          <th>Categoria</th>
          <th>Status</th>
        </thead>
        <tbody>
          <tr>
            <td>Comprar pão</td>
            <td>21/04/2021</td>
            <td>Importante</td>
            <td>Pendente</td>
          </tr>
          <tr>
            <td>Estudar matemática</td>
            <td>20/04/2021</td>
            <td>Urgente</td>
            <td>Pendente</td>
          </tr>
          <tr>
            <td>Arrumar o quarto</td>
            <td>22/04/2021</td>
            <td>Precisa ser feito</td>
            <td>Pendente</td>
          </tr>
        </tbody>
      </table>

      <hr>

      <h1>Passo 6: Criar o arquivo de migrações e aplicar as migrações</h1>
      <p>
        Sempre que criamos um novo modelo, ou modificamos um modelo existente
        precisamos criar um arquivo com instruções de migrações para o Django,
        e depois precisamos aplicar essas migrações. Isso é necessário para que
        as tabelas de dados da nossa aplicação reflita o estado real definido
        no arquivo models.py.
      </p>
      <h4>Primeiro, criamos um novo arquivo com instruções de migrações:</h4>
      <pre class="language-python">
        <code class="language-python">
          python manage.py makemigrations
        </code>
      </pre>
      <h4>Em seguida, aplicamos as migrações:</h4>
      <pre class="language-python">
        <code class="language-python">
          python manage.py migrate
        </code>
      </pre>
      <hr>

      <h1>Passo 7: Registrar o modelo criado no Admin</h1>
      <p>
        O Django possui um site para criação, exclusão e visualização de modelos,
        o Admin. Porém, antes de poder ter acesso a um modelo através de Admin,
        é necessário registrar esse modelo lá. Fazemos isso através do arquivo
        <i>admin.py</i>, presente no diretório do app <i>tarefas.</i>
      </p>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/admin.py


          from django.contrib import admin
          from .models import Tarefa

          # Register your models here.
          admin.site.register(Tarefa)
        </code>
      </pre>
      <hr>

      <h1>Passo 8: Criar um superuser</h1>
      <p>
        Para poder ter acesso ao Admin, precisamos criar um <i>superuser</i>, isto é,
        um usuário com todas as permissões de administrador. Fazemos isso através
        do seguinte comando:
      </p>
      <pre class="language-python">
        <code class="language-python">
          python manage.py createsuperuser
        </code>
      </pre>
      <p>
        Em seguida, é só seguir as instruções, fornecendo um nome de usuário,
        email e senha.
      </p>
      <hr>

      <h1>Passo 9 (didático): Iniciar o servidor de desenvolvimento</h1>
      <p>
        O Django possui um servidor de desenvolvimento que nos permite testar
        a nossa aplicação sem a necessidade de se configurar um servidor
        para produção.
      </p>
      <p>
        Para iniciar o servidor de desenvolvimento é necessário executar o
        seguinte comando:
      </p>
      <pre class="language-python">
        <code class="language-python">
          python manage.py runserver
        </code>
      </pre>
      <p>
        Em seguida, basta copiar o endereço retornado (algo parecido com 'http://127.0.0.1:8000/')
        e colar na barra de URL do seu navegador.
      </p>
      <p>
        O resultado será uma página semelhante  à página representada na seguinte imagem:
      </p>
      <img src="imagens/img1.jpg" style="width:800px;height:600px">
      <br>
      <p>
        Para visualizar o site Admin, acrescente '/admin' na URL atual. A URL
        resultante será parecida com 'http://127.0.0.1:8000/admin'. A página
        seguinte vai solicitar um login e uma senha, entre com os dados do superuser
        que você criou no passo 8. (se você esqueceu os dados do seu superuser
        basta criar outro, repetindo os procedimentos descritos no passo 8)
      </p>
      <img src="imagens/img2.jpg" style="width:500px;height:400px">
      <br>
      <p>
        Uma vez logado no Admin, a página principal terá a seguinte aparência:
      </p>
      <img src="imagens/img3.jpg" style="width:800;height:300">
      <br>
      <p>
        À esquerda, vemos alguns modelos do projeto. Clicando em 'Tarefas' será
        possível incluir, excluir e visualizar as tarefas cadastradas. Adicione
        algumas tarefas, pois no próximo passo vamos criar uma página que lista
        as tarefas cadastradas.
      </p>
      <hr>

      <h1>Passo 10: Editar arquivo urls.py do projeto</h1>
      <p>
        Vamos adicionar um caminho de urls com o padrão 'HOST/tarefas/' para um
        arquivo de urls dentro do app tarefas.
      </p>
      <h4>Incluindo o caminho '/tarefas/'</h4>
      <pre class="language-python">
        <code class="language-python">
          # urls.py

          from django.contrib import admin
          from django.urls import path, include # novo

          urlpatterns = [
              path('admin/', admin.site.urls),
              path('tarefas/', include('tarefas.urls')), # novo
          ]
        </code>
      </pre>
      <p>
        Assim, sempre que alguma urls do tipo 'HOST/tarefas/' for requisitada,
        o mapeamento da URL será feito por um arquivo 'urls.py' presente no
        diretório do app <i>tarefas</i>. Este arquivo ainda não existe, ou seja,
        é necessário criá-lo em seguida.
      </p>

      <h4>Criando o arquivo 'urls.py' do app <i>tarefas</i></h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/urls.py


          from django.urls import path, include
          from . import views

          urlpatterns = [
              path('', views.tarefas_pendentes_list, name='tarefas_pendentes_list' ),
          ]
        </code>
      </pre>

      <p>
        No código acima nós especificamos que quando a URL 'HOST/tarefas/' for
        requisitada, a função (view) <i>tarefas_pendentes_list</i> deverá ser
        chamada. É na função que nós descrevemos a lógica do que deverá ser
        entregue como resposta quando a URL for requisitada. Além disso, nós
        damos um nome à URL para que ela possa ser referenciada em templates, ou,
        falando de outra maneira, para criarmos um link para essa URL.
      </p>
      <p>
        No caminho que nós acabamos de descrever, chamamos uma função que ainda
        não existe. Então, o próximo passo é criar essa função no arquivo
        <i>views.py</i> do app <i>tarefas</i>.
      </p>

      <h1>Passo 11 (didático):  Criando a view <i>tarefas_pendentes_list</i></h1>
      <p>Este passo serve para entender melhor a lógica entre urls, views,
        templates e modelos. Primeiramente vamos criar uma view que puxa
        as tarefas que estão com o status de pendente salvas no banco de dados
        da aplicação. Em seguida, a função vai renderizar um template (um arquivo
        html) e passar para ele os objetos recuperados do banco de dados (tarefas
        pendentes).
      </p>
      <p>
        Você vai perceber que vamos fazer referência a um template que ainda não
        existe, isso é normal, vamos criá-lo no próximo passo.
      </p>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/views.py


          from django.shortcuts import render
          from .models import Tarefa

          def tarefas_pendentes_list(request):
              tarefas_pendentes = Tarefa.objects.filter(status='pendente')
              return render(request, 'tarefas/tarefas_pendentes.html',
                            {'tarefas_pendentes':tarefas_pendentes})
        </code>
      </pre>
      <hr>

      <h1>Passo 12 (didático): Criando o template <i>tarefas_pendentes.html</i></h1>
      <p>
        Dando sequência ao passo anterior, vamos agora criar o template
        <i>tarefas_pendentes.html</i>, referenciado no passo anterior.
      </p>
      <p>
        Onde o template deverá estar salvo? Observando a função <i>render</i>
        da view criada, vemos que o template deverá estar dentro de um diretório
        chamado tarefas. E onde fica esse diretório? Por padrão, o Django vai
        procurar uma pasta chamada 'templates' dentro do diretório do app tarefas.
        Sendo assim, a estrutura deverá ser a seguinte:
      </p>
      <pre>
        <code class="language-treeview">
          dia_organizado/
          |-- dia_organizado/
          |-- tarefas/
          |   |-- ...
          |   |-- templates/
          |   |   |-- tarefas/
          |   |   |   `-- tarefas_pendentes.html
          `-- manage.py
        </code>
      </pre>
      <h4>tarefas_pendentes.html</h4>
      <pre>
        <code class="language-markup">
          # tarefas/templates/tarefas/tarefas_pendentes.html

          &lt;!DOCTYPE html>
          &lt;html lang="en" dir="ltr">
            &lt;head>
              &lt;meta charset="utf-8">
              &lt;title>&lt;/title>
            &lt;/head>
            &lt;body>
              &lt;h1>Tarefas Pendentes:&lt;/h1>
              {% for tarefa in tarefas_pendentes %}
                &lt;p>&lt;b>Descrição:&lt;/b> {{ tarefa.descricao }}&lt;/p>
                &lt;p>&lt;b>Categoria:&lt;/b> {{ tarefa.categoria }}&lt;/p>
                &lt;p>&lt;b>Criação:&lt;/b> {{ tarefa.criacao }}&lt;/p>
                &lt;hr>
              {% endfor %}
            &lt;/body>
          &lt;/html>
        </code>
      </pre>
      <hr>

      <h1>Passo 13: Criar um template base para ser utilizado por todos os
        outros templates
      </h1>
      <p>
        Pode ser que existam seções em um site que se repitam em diversas
        páginas. Para que não seja necessário repetir o mesmo código em
        diversas páginas diferentes, podemos criar um template base, e
        utilizar o código desse template nos outros templates do projeto.
      </p>
      <p>
        Vamos criar um novo arquivo HTML na pasta templates do app tarefas.
      </p>
      <pre>
        <code class="language-treeview">
          dia_organizado/
          |-- dia_organizado/
          |-- tarefas/
          |   |-- ...
          |   |-- templates/
          |   |   |-- base.html
          |   |   |-- tarefas/
          |   |   |   `-- tarefas_pendentes.html
          `-- manage.py
        </code>
      </pre>
      <p>
        Em todas as páginas do nosso projeto vamos querer mostrar um navbar
        (barra de navegação), e em todas as páginas vamos utilizar elementos
        Bootstrap.
      </p>
      <p>
        Para aqueles que nunca utilizaram, o Bootstrap é um framework para
         desenvolvimento front-end de aplicações web. Podemos facilmente
         utilizar os componentes definidos pelo Bootstrap simplesmente
         adicionando classes nos elementos HTML dos nossos templates.
         Para que seja possível utilizar o Bootstrap, precisamos de alguns
         códigos específicos, que podem ser encontrados no <a href="https://getbootstrap.com/">site</a>
         oficial do framework. Podemos copiar o starter template e criar as nossas páginas
         a partir dele.
      </p>
      <p>
        Já que vamos precisar do código para o Bootstrap e para o Navbar em
        todos os templates do projeto, vamos adicioná-lo em nosso template base.
      </p>
      <h4>base.html</h4>
      <pre>
        <code class="language-markup">
          # tarefas/templates/base.html

          &lt;!doctype html>
          &lt;html lang="en">
            &lt;head>
              &lt;!-- Required meta tags -->
              &lt;meta charset="utf-8">
              &lt;meta name="viewport" content="width=device-width, initial-scale=1">

              &lt;!-- Bootstrap CSS -->
              &lt;link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-eOJMYsd53ii+scO/bJGFsiCZc+5NDVN2yr8+0RDqr0Ql0h+rP48ckxlpbzKgwra6" crossorigin="anonymous">

              &lt;title>{% block title %}{% endblock %}&lt;/title>
            &lt;/head>
            &lt;body style="padding-top:70px">
              &lt;nav class="navbar fixed-top navbar-expand-lg navbar-dark bg-dark">
                &lt;div class="container-fluid">
                  &lt;a class="navbar-brand" href="#">DiaOrganizado&lt;/a>
                  &lt;button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                    &lt;span class="navbar-toggler-icon">&lt;/span>
                  &lt;/button>
                  &lt;div class="collapse navbar-collapse" id="navbarSupportedContent">
                    &lt;ul class="navbar-nav me-auto mb-2 mb-lg-0">
                      &lt;li class="nav-item">
                        &lt;a class="nav-link active" aria-current="page" href="#">Tarefas&lt;/a>
                      &lt;/li>
                      &lt;li class="nav-item dropdown">
                        &lt;a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                          Outras tarefas
                        &lt;/a>
                        &lt;ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                          &lt;li>&lt;a class="dropdown-item" href="#">Adiadas&lt;/a>&lt;/li>
                          &lt;li>&lt;a class="dropdown-item" href="#">Concluídas&lt;/a>&lt;/li>
                        &lt;/ul>
                      &lt;/li>
                    &lt;/ul>
                  &lt;/div>
                &lt;/div>
              &lt;/nav>

              &lt;div class="container">
                {% block content %}
                {% endblock %}
              &lt;/div>

              &lt;!-- Option 1: Bootstrap Bundle with Popper -->
              &lt;script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/js/bootstrap.bundle.min.js" integrity="sha384-JEW9xMcG8R+pH31jmWH6WWP0WintQrMb4s7ZOdauHnUtxwoG2vI5DkLtS3qm9Ekf" crossorigin="anonymous">&lt;/script>
            &lt;/body>
          &lt;/html>

        </code>
      </pre>
      <p>
        Com o template base criado, podemos utilizá-lo em outros templates do
        projeto.
      </p>
      <hr>

      <h1>Passo 14: Extendendo o código do template base</h1>
      <p>
        Vamos editar o template <i>tarefas_pendentes.html</i> para que este
        herde o código do template base que nós criamos.
      </p>
      <pre>
        <code class="language-markup">
          # tarefas/templates/tarefas/tarefas_pendentes.html

          {% extends 'base.html' %}

          {% block title %}Tarefas pendentes{% endblock %}

          {% block content %}
            &lt;h1>Tarefas Pendentes:&lt;/h1>
            {% for tarefa in tarefas_pendentes %}
              &lt;p>&lt;b>Descrição:&lt;/b> {{ tarefa.descricao }}&lt;/p>
              &lt;p>&lt;b>Categoria:&lt;/b> {{ tarefa.categoria }}&lt;/p>
              &lt;p>&lt;b>Criação:&lt;/b> {{ tarefa.criacao }}&lt;/p>
              &lt;hr>
            {% endfor %}
          {% endblock %}

        </code>
      </pre>
      <hr>

      <h1>Passo 15: Modificando o front-end da lista de tarefas pendentes</h1>
      <p>
        Vamos melhorar a visualização das tarefas pendentes do projeto.
      </p>
      <h4>Adicionando <i>list-group</i></h4>
      <p>
        <i>list-group</i> é um componente para mostrar uma lista de conteúdo.
        Em nosso caso, vamos utilizá-lo para mostrar a lista de tarefas pendentes.
        Cada tarefa será apresentada como um botão.
      </p>
      <pre>
        <code class="language-markup">
          # tarefas/templates/tarefas/tarefas_pendentes.html

          {% extends 'base.html' %}

          {% block title %}Tarefas pendentes{% endblock %}

          {% block content %}
            &lt;h1>Tarefas Pendentes:&lt;/h1>
            &lt;div class="list-group">
              {% for tarefa in tarefas_pendentes %}
                &lt;!-- Button trigger modal -->
                &lt;button type="button" class="list-group-item list-group-item-action">
                  &lt;h5>{{ tarefa.descricao }}&lt;/h5>
                  &lt;small>Criado em: {{ tarefa.criacao.day }}/{{ tarefa.criacao.month }}/{{ tarefa.criacao.year }}&lt;/small>
                &lt;/button>
              {% endfor %}
            &lt;/div>
          {% endblock %}

        </code>
      </pre>

      <p>
         Cada tarefa é apresentada através de um botão. Os
         botões serão responsáveis por carregar um outro componente, o <i>modal</i>.
         O modal é como uma caixa de diálogo, que será carregada quando clicarmos
         nos botões utilizados para mostrar as tarefas.
      </p>
      <p>
        Também será necessário editar os botões para que eles possam carregar
        os modais.
      </p>
      <h4>Editando botões e adicionando modais</h4>
      <pre>
        <code class="language-markup">
          # tarefas/templates/tarefas/tarefas_pendentes.html

          {% extends 'base.html' %}

          {% block title %}Tarefas pendentes{% endblock %}

          {% block content %}
            &lt;h1>Tarefas Pendentes:&lt;/h1>
            &lt;div class="list-group">
              {% for tarefa in tarefas_pendentes %}
                &lt;!-- Button trigger modal -->
                &lt;button type="button" class="list-group-item list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                  &lt;h5>{{ tarefa.descricao }}&lt;/h5>
                  &lt;small>Criado em: {{ tarefa.criacao.day }}/{{ tarefa.criacao.month }}/{{ tarefa.criacao.year }}&lt;/small>
                &lt;/button>
                &lt;!-- Modal -->
                &lt;div class="modal fade" id="modal{{ tarefa.id }}" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                  &lt;div class="modal-dialog">
                    &lt;div class="modal-content">
                      &lt;div class="modal-header">
                        &lt;h5 class="modal-title" id="exampleModalLabel">{{ tarefa.descricao }} | {{ tarefa.categoria|capfirst }}&lt;/h5>
                        &lt;button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close">&lt;/button>
                      &lt;/div>
                      &lt;div class="modal-body">
                        &lt;p>
                          Modal Body
                        &lt;/p>
                      &lt;/div>
                    &lt;/div>
                  &lt;/div>
                &lt;/div>
              {% endfor %}
            &lt;/div>
          {% endblock %}

        </code>
      </pre>
      <p>
        Para modificar a aparência de cada botão, vamos adicionar condições
        ao template. O objetivo das condições é testar a categoria de cada
        tarefa e alterar a classe de cada botão de acordo com sua categoria.
      </p>

      <h4>Modificando a aparência dos botões</h4>
      <pre>
        <code class="language-markup">
          # tarefas/templates/tarefas/tarefas_pendentes.html

          {% extends 'base.html' %}

          {% block title %}Tarefas pendentes{% endblock %}

          {% block content %}
            &lt;h1>Tarefas Pendentes:&lt;/h1>
            &lt;div class="list-group">
              {% for tarefa in tarefas_pendentes %}
                {% if tarefa.categoria == 'urgente' %}
                  &lt;button type="button" class="list-group-item list-group-item-danger list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                {% else %}
                  {% if tarefa.categoria == 'importante' %}
                    &lt;button type="button" class="list-group-item list-group-item-warning list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                  {% else %}
                    &lt;button type="button" class="list-group-item list-group-item-primary list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                  {% endif %}
                {% endif %}
                  &lt;h5>{{ tarefa.descricao }}&lt;/h5>
                  &lt;small>Criado em: {{ tarefa.criacao.day }}/{{ tarefa.criacao.month }}/{{ tarefa.criacao.year }}&lt;/small>
                &lt;/button>
                &lt;!-- Modal -->
                &lt;div class="modal fade" id="modal{{ tarefa.id }}" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                  &lt;div class="modal-dialog">
                    &lt;div class="modal-content">
                      &lt;div class="modal-header">
                        &lt;h5 class="modal-title" id="exampleModalLabel">{{ tarefa.descricao }} | {{ tarefa.categoria|capfirst }}&lt;/h5>
                        &lt;button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close">&lt;/button>
                      &lt;/div>
                      &lt;div class="modal-body">
                        &lt;p>
                          Modal Body
                        &lt;/p>
                      &lt;/div>
                    &lt;/div>
                  &lt;/div>
                &lt;/div>
              {% endfor %}
            &lt;/div>
          {% endblock %}

        </code>
      </pre>
      <hr>

      <h1>Passo 16: Criando um formulário para inclusão de novas tarefas</h1>
      <p>
        Um formulário é a ferramenta através da qual uma aplicação web aceita
        dados fornecidos por usuários. Neste passo, vamos criar um formulário
        que recebe informações necessárias para criação de novas tarefas.
      </p>
      <p>
        Sempre que nós vamos criar um formulário que está atrelado a um modelo
        (neste caso, o formulário estará atrelado ao modelo Tarefa), podemos
        utilizar a classe <i>django.forms.ModelForm</i> para criar formulários
        a partir de modelos. Através dessa classe, só precisamos especificar
        o modelo a partir do qual o formulário será criado, e quais atributos
        desse modelo devem ser apresentados no formulários.
      </p>
      <p>
        Para criação do formulário, vamos criar um novo arquivo no diretório do
        app <i>Tarefas</i>, <i>forms.py</i>. Este arquivo será utilizado para
        armazenar os formulários da aplicação.
      </p>
      <h4>Criando o arquivo <i>forms.py</i></h4>
      <pre>
        <code class="language-treeview">
          dia_organizado/
          |-- dia_organizado/
          |   `-- ...
          |-- tarefas/
          |   |-- migrations/
          |   |   `-- ...
          |   |-- templates/
          |   |   `-- ...
          |   |-- __init__.py
          |   |-- admin.py
          |   |-- apps.py
          |   |-- models.py
          |   |-- tests.py
          |   |-- urls.py
          |   |-- forms.py
          |   `-- views.py
          `-- manage.py
        </code>
      </pre>

      <p>
        Dentro do arquivo criado, vamos criar uma nova classe, <i>AdicionarTarefa</i>,
        que herda de <i>django.forms.ModelForm</i>. A classe representará o
        formulário para inserção de novas tarefas. Dentro da classe criada,
        especificamos o modelo gerador e quais os campos devem aparecer no formulário.
      </p>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/forms.py


          from django import forms
          from .models import Tarefa

          class AdicionarTarefa(forms.ModelForm):
              class Meta:
                  model = Tarefa
                  fields = ('descricao', 'categoria')
        </code>
      </pre>
      <p>
        Note que nós não especificamos os campos <i>criacao</i>, pois este é
        adicionado automaticamente sempre que uma nova instância do modelo
        Tarefa é criado, e <i>categoria</i>, pois este campo vem automaticamente
        como <i>'pendente'</i>, afinal, se uma tarefa é adicionada numa lista
        de tarefas, pressupõe-se que esta ainda não foi concluída.
      </p>
      <hr>

      <h1>Passo 17: Tratando o formulário e enviando-o para o template</h1>
      <p>
        Uma vez definido o formulário, precisamos criar a lógica para tratá-lo
        corretamente, além de fazer com que o formulário apareça no template.
        Como sempre, a lógica da aplicação é definida através das
        views, isso significa que vamos precisar editar a view
        <i>tarefas_pendentes_list</i>, criada anteriormente.
      </p>
      <p>
        Para entender como um formulário é tratado, precisamos ter uma noção
        básica de como funciona a comunicação entre o usuário de uma aplicação
        web e o servidor onde a aplicação está hospedada.
      </p>
      <h4>Uma noção básica do processo de comunicação entre cliente e servidor</h4>
      <p>
        Quando um usuário (cliente) tenta acessar uma página do seu site, através de uma
        URL, o navegador cliente envia uma espécie de mensagem para o servidor da
        aplicação solicitando os dados dessa página. Por enquanto, tudo que
        precisamos saber é que essa mensagem possui um método, e os métodos
        mais comuns são GET e POST.
      </p>
      <h5>GET vs POST</h5>
      <p>
        O método GET é utilizado quando o cliente apenas solicita os dados de
        uma página web. Por exemplo, quando você visita o site www.google.com,
        o método que o seu navegador utiliza para solicitar as informações do
        servidor do Google é o GET, afinal, você só quer acessar uma página.
      </p>
      <p>
        O método POST, por sua vez, é utilizado quando o cliente quer enviar
        dados para o servidor da aplicação. Ou seja, quando você digita alguns
        caracteres na barra de pesquisa do Google e clica em pesquisar, você
        está enviando dados para o servidor da aplicação.
      </p>
      <p>
        É justamente essa lógica que nós vamos utilizar para tratar o formulário
        <i>AdicionarTarefa</i>, criado no passo anterior. Quando um usuário
        tentar acessar a página associada com a URL <i>HOST/tarefas</i>, o método
        será o GET, pois o cliente quer apenas acessar as informações nessa página.
        Nessa situação, tudo que nós vamos fazer é mostrar o formulário vazio,
        pronto para receber os dados de uma tarefa para ser adicionada ao banco
        de dados da aplicação.
      </p>
      <p>
        Por outro lado, quando o usuário preencher os campos do formulário e
        clicar em um botão para envio do formulário, o método será o POST, e o
        cliente estará enviando informações para o servidor da aplicação. Nessa
        situação, nós utilizaremos os dados fornecidos para a criação de uma nova
        instância do modelo Tarefa. Em outras palavras, estaremos inserindo uma
        nova tarefa no banco de dados da aplicação.
      </p>
      <h4>Editando a view <i>tarefas_pendentes_list</i></h4>
      <pre class='language-python'>
        <code class="language-python">
          # tarefas/views.py


          from django.shortcuts import render, redirect
          from .models import Tarefa
          from .forms import AdicionarTarefa

          def tarefas_pendentes_list(request):
              tarefas_pendentes = Tarefa.objects.filter(status='pendente')
              if request.method == 'POST':
                  form = AdicionarTarefa(data=request.POST)
                  if form.is_valid():
                      form.save()
                      return redirect('tarefas_pendentes_list')
              else:
                  form = AdicionarTarefa()
              return render(request, 'tarefas/tarefas_pendentes.html',
                            {'tarefas_pendentes':tarefas_pendentes,
                             'form':form})

        </code>
      </pre>
      <p>
        Quando o cliente tentar acessar a página através de um GET, nós apenas
        criamos uma instância vazia do formulário <i>AdicionarTarefa</i> e a
        enviamos para o template. Por outro lado, quando o método for POST, nós
        criamos uma intância do formulário com os dados fornecidos pelo usuário,
        e, se este for válido, nós criamos uma nova instância do modelo <i>Tarefa</i>,
        isto é, inserimos uma nova tarefas no banco de tarefas da aplicação.
      </p>
      <p>
        Agora precisamos alterar o template <i>tarefas_pendentes.html</i> para
        que este mostre o formulário que nós criamos.
      </p>
      <h4>tarefas_pendentes.html</h4>
      <pre>
        <code class="language-markup">
          # tarefas/templates/tarefas/tarefas_pendentes.html


          {% extends 'base.html' %}

          {% block title %}Tarefas pendentes{% endblock %}

          {% block content %}
            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Adicionar Tarefa&lt;/h1>
              &lt;form method="post">
                {% csrf_token %}
                {{ form.as_p }}
                &lt;br>
                &lt;input type="submit" value="Salvar">
              &lt;/form>
            &lt;/div>

            &lt;h1>Tarefas Pendentes:&lt;/h1>
            &lt;div class="list-group">
              {% for tarefa in tarefas_pendentes %}
                {% if tarefa.categoria == 'urgente' %}
                  &lt;button type="button" class="list-group-item list-group-item-danger list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                {% else %}
                  {% if tarefa.categoria == 'importante' %}
                    &lt;button type="button" class="list-group-item list-group-item-warning list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                  {% else %}
                    &lt;button type="button" class="list-group-item list-group-item-primary list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                  {% endif %}
                {% endif %}
                  &lt;h5>{{ tarefa.descricao }}&lt;/h5>
                  &lt;small>Criado em: {{ tarefa.criacao.day }}/{{ tarefa.criacao.month }}/{{ tarefa.criacao.year }}&lt;/small>
                &lt;/button>
                &lt;!-- Modal -->
                &lt;div class="modal fade" id="modal{{ tarefa.id }}" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                  &lt;div class="modal-dialog">
                    &lt;div class="modal-content">
                      &lt;div class="modal-header">
                        &lt;h5 class="modal-title" id="exampleModalLabel">{{ tarefa.descricao }} | {{ tarefa.categoria|capfirst }}&lt;/h5>
                        &lt;button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close">&lt;/button>
                      &lt;/div>
                      &lt;div class="modal-body">
                        &lt;p>
                          Modal Body
                        &lt;/p>
                      &lt;/div>
                    &lt;/div>
                  &lt;/div>
                &lt;/div>
              {% endfor %}
            &lt;/div>
          {% endblock %}

        </code>
      </pre>
      <hr>

      <h1>Passo 18: Melhorando o front-end da lista de tarefas</h1>
      <p>
        Podemos melhorar a aparência da aplicação com algumas mudanças básicas.
        Vamos utilizar um pacote para melhorar a aparência do formulário,
        alterar a aparência do botão <i>Salvar</i> com uma classe Bootstrap
        e inserir a lista de tarefas dentro de um div particular.
      </p>
      <h4>Instalando o pacote <i>django-crispy-forms</i></h4>
      <pre class="language-python">
        <code class="language-python">
          pip install django-crispy-forms
        </code>
      </pre>

      <h4>Adicionado <i>crispy-forms</i> nos <i>installed apps</i> do projeto</h4>
      <pre>
        <code class=" language-python">
          # dia_organizado/settings.py


          INSTALLED_APPS = [
              'django.contrib.admin',
              'django.contrib.auth',
              'django.contrib.contenttypes',
              'django.contrib.sessions',
              'django.contrib.messages',
              'django.contrib.staticfiles',
              'crispy_forms', #novo
              'tarefas.apps.TarefasConfig',
          ]

          # django-crispy-forms
          CRISPY_TEMPLATE_PACK = 'bootstrap4' #novo
        </code>
      </pre>

      <h4>Carregando formulário como um <i>crispy_form</i> no template tarefas_pendentes.html</h4>
      <pre>
        <code class="language-markup">
          {% extends 'base.html' %}
          {% load crispy_forms_tags %}

          {% block title %}Tarefas pendentes{% endblock %}

          {% block content %}
            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Adicionar Tarefa&lt;/h1>
              &lt;form method="post">
                {% csrf_token %}
                {{ form|crispy }}
                &lt;br>
                &lt;input type="submit" value="Salvar">
              &lt;/form>
            &lt;/div>

            &lt;h1>Tarefas Pendentes:&lt;/h1>
            &lt;div class="list-group">
              {% for tarefa in tarefas_pendentes %}
                {% if tarefa.categoria == 'urgente' %}
                  &lt;button type="button" class="list-group-item list-group-item-danger list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                {% else %}
                  {% if tarefa.categoria == 'importante' %}
                    &lt;button type="button" class="list-group-item list-group-item-warning list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                  {% else %}
                    &lt;button type="button" class="list-group-item list-group-item-primary list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                  {% endif %}
                {% endif %}
                  &lt;h5>{{ tarefa.descricao }}&lt;/h5>
                  &lt;small>Criado em: {{ tarefa.criacao.day }}/{{ tarefa.criacao.month }}/{{ tarefa.criacao.year }}&lt;/small>
                &lt;/button>
                &lt;!-- Modal -->
                &lt;div class="modal fade" id="modal{{ tarefa.id }}" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                  &lt;div class="modal-dialog">
                    &lt;div class="modal-content">
                      &lt;div class="modal-header">
                        &lt;h5 class="modal-title" id="exampleModalLabel">{{ tarefa.descricao }} | {{ tarefa.categoria|capfirst }}&lt;/h5>
                        &lt;button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close">&lt;/button>
                      &lt;/div>
                      &lt;div class="modal-body">
                        &lt;p>
                          Modal Body
                        &lt;/p>
                      &lt;/div>
                    &lt;/div>
                  &lt;/div>
                &lt;/div>
              {% endfor %}
            &lt;/div>
          {% endblock %}
        </code>
      </pre>

      <h4>Modificando a aparência do botão <i>Salvar</i></h4>
      <pre>
        <code class="language-markup">
          {% extends 'base.html' %}
          {% load crispy_forms_tags %}

          {% block title %}Tarefas pendentes{% endblock %}

          {% block content %}
            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Adicionar Tarefa&lt;/h1>
              &lt;form method="post">
                {% csrf_token %}
                {{ form|crispy }}
                &lt;br>
                &lt;input class="btn btn-success" type="submit" value="Salvar">
              &lt;/form>
            &lt;/div>

            &lt;h1>Tarefas Pendentes:&lt;/h1>
            &lt;div class="list-group">
              {% for tarefa in tarefas_pendentes %}
                {% if tarefa.categoria == 'urgente' %}
                  &lt;button type="button" class="list-group-item list-group-item-danger list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                {% else %}
                  {% if tarefa.categoria == 'importante' %}
                    &lt;button type="button" class="list-group-item list-group-item-warning list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                  {% else %}
                    &lt;button type="button" class="list-group-item list-group-item-primary list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                  {% endif %}
                {% endif %}
                  &lt;h5>{{ tarefa.descricao }}&lt;/h5>
                  &lt;small>Criado em: {{ tarefa.criacao.day }}/{{ tarefa.criacao.month }}/{{ tarefa.criacao.year }}&lt;/small>
                &lt;/button>
                &lt;!-- Modal -->
                &lt;div class="modal fade" id="modal{{ tarefa.id }}" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                  &lt;div class="modal-dialog">
                    &lt;div class="modal-content">
                      &lt;div class="modal-header">
                        &lt;h5 class="modal-title" id="exampleModalLabel">{{ tarefa.descricao }} | {{ tarefa.categoria|capfirst }}&lt;/h5>
                        &lt;button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close">&lt;/button>
                      &lt;/div>
                      &lt;div class="modal-body">
                        &lt;p>
                          Modal Body
                        &lt;/p>
                      &lt;/div>
                    &lt;/div>
                  &lt;/div>
                &lt;/div>
              {% endfor %}
            &lt;/div>
          {% endblock %}
        </code>
      </pre>

      <h4>Inserindo a lista de tarefas dentro de um div próprio</h4>
      <pre>
        <code class="language-markup">
          {% extends 'base.html' %}
          {% load crispy_forms_tags %}

          {% block title %}Tarefas pendentes{% endblock %}

          {% block content %}
            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Adicionar Tarefa&lt;/h1>
              &lt;form method="post">
                {% csrf_token %}
                {{ form|crispy }}
                &lt;br>
                &lt;input type="submit" value="Salvar">
              &lt;/form>
            &lt;/div>

            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Tarefas Pendentes:&lt;/h1>
              &lt;div class="list-group">
                {% for tarefa in tarefas_pendentes %}
                  {% if tarefa.categoria == 'urgente' %}
                    &lt;button type="button" class="list-group-item list-group-item-danger list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                  {% else %}
                    {% if tarefa.categoria == 'importante' %}
                      &lt;button type="button" class="list-group-item list-group-item-warning list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                    {% else %}
                      &lt;button type="button" class="list-group-item list-group-item-primary list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                    {% endif %}
                  {% endif %}
                    &lt;h5>{{ tarefa.descricao }}&lt;/h5>
                    &lt;small>Criado em: {{ tarefa.criacao.day }}/{{ tarefa.criacao.month }}/{{ tarefa.criacao.year }}&lt;/small>
                  &lt;/button>
                  &lt;!-- Modal -->
                  &lt;div class="modal fade" id="modal{{ tarefa.id }}" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                    &lt;div class="modal-dialog">
                      &lt;div class="modal-content">
                        &lt;div class="modal-header">
                          &lt;h5 class="modal-title" id="exampleModalLabel">{{ tarefa.descricao }} | {{ tarefa.categoria|capfirst }}&lt;/h5>
                          &lt;button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close">&lt;/button>
                        &lt;/div>
                        &lt;div class="modal-body">
                          &lt;p>
                            Modal Body
                          &lt;/p>
                        &lt;/div>
                      &lt;/div>
                    &lt;/div>
                  &lt;/div>
                {% endfor %}
              &lt;/div>
            &lt;/div>

          {% endblock %}

        </code>
      </pre>
      <hr>

      <h1>Passo 19: Implementar a funcionalidade do botão de conclusão de tarefas</h1>
      <p>
        Agora nós vamos implementar a funcionalidade de conclusão de tarefas.
        Quando um usuário clicar em uma tarefa, o modal oferecerá ao usuário
        a opção de conclusão desta tarefa, através de um botão.
      </p>
      <p>
        Uma forma de implementar a funcionalidade de um botão é através de uma
        <i>anchor tag</i>. Uma anchor tag é um elemento HTML que permite a
        criação de um hyperlink. Ou seja, através dele podemos navegar de uma
        página para outra. Podemos adicionar classes bootstrap para dar a este
        elemento a aparência de um botão. Ao clicar neste botão, o usuário será
        redirecionado para uma nova URL. A URL, por sua vez, estará conectada a
        uma view, que será responsável por "concluir a tarefa."
      </p>
      <p>
        Primeiramente, vamos criar uma nova view, <i>concluir_tarefa()</i>, que
        será responsável pela lógica de conclusão de tarefas. Tudo que nós faremos
        na view é alterar o valor do status de uma determinada tarefa de 'pendente'
        para 'concluído'. Para que a view saiba qual tarefa deverá ser concluída,
        ela deverá receber como argumento o valor do 'id' da tarefa a ser concluída.
        'id' é um campo adicionado automaticamente pelo Django e utilizado para
        tornar única cada instância do modelo Tarefa. A primeira tarefa adicionada
        possui o valor de id igual a 1, a segunda igual a 2, a terceira igual a 3,
        e assim por diante. Quem vai passar o valor do 'id' para a view é a URL
        (que ainda será criada) responsável por chamar essa view.
      </p>
      <h4>Criando a view <i>concluir_tarefa()</i> </h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/views.py


          from django.shortcuts import render, redirect, get_object_or_404 # novo
          from .models import Tarefa
          from .forms import AdicionarTarefa

          def tarefas_pendentes_list(request):
              tarefas_pendentes = Tarefa.objects.filter(status='pendente')
              if request.method == 'POST':
                  form = AdicionarTarefa(data=request.POST)
                  if form.is_valid():
                      form.save()
                      return redirect('tarefas_pendentes_list')
              else:
                  form = AdicionarTarefa()
              return render(request, 'tarefas/tarefas_pendentes.html',
                            {'tarefas_pendentes':tarefas_pendentes,
                             'form':form})

          # novo
          def concluir_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.status = 'concluído'
              tarefa.save()
              return redirect('tarefas_pendentes_list')

        </code>
      </pre>

      <p>
        Agora, vamos definir a URL responsável por chamar a view criada e passar
        para ela o id da tarefa a ser concluída. Fazemos isso por adicionar
        mais um <i>path</i> no arquivo <i>urls.py</i> do app <i>Tarefas</i>.
      </p>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/urls.py


          from django.urls import path, include
          from . import views

          urlpatterns = [
              path('', views.tarefas_pendentes_list, name='tarefas_pendentes_list' ),
              path('&lt;int:tarefa_id>/concluir/', views.concluir_tarefa, name='concluir_tarefa'), # novo
          ]

        </code>
      </pre>
      <p>
        Com a view e a URL definidas, precisamos fornecer a opção para o usuário
        concluir a tarefa. Faremos isso modificando o template <i>tarefas_pendentes.html</i>.
      </p>

      <pre>
        <code class="language-markup">
          # tarefas/templates/tarefas/tarefas_pendentes.html


          {% extends 'base.html' %}
          {% load crispy_forms_tags %}

          {% block title %}Tarefas pendentes{% endblock %}

          {% block content %}
            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Adicionar Tarefa&lt;/h1>
              &lt;form method="post">
                {% csrf_token %}
                {{ form|crispy }}
                &lt;br>
                &lt;input class="btn btn-success" type="submit" value="Salvar">
              &lt;/form>
            &lt;/div>

            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Tarefas Pendentes:&lt;/h1>
              &lt;div class="list-group">
                {% for tarefa in tarefas_pendentes %}
                  {% if tarefa.categoria == 'urgente' %}
                    &lt;button type="button" class="list-group-item list-group-item-danger list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                  {% else %}
                    {% if tarefa.categoria == 'importante' %}
                      &lt;button type="button" class="list-group-item list-group-item-warning list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                    {% else %}
                      &lt;button type="button" class="list-group-item list-group-item-primary list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                    {% endif %}
                  {% endif %}
                    &lt;h5>{{ tarefa.descricao }}&lt;/h5>
                    &lt;small>Criado em: {{ tarefa.criacao.day }}/{{ tarefa.criacao.month }}/{{ tarefa.criacao.year }}&lt;/small>
                  &lt;/button>
                  &lt;!-- Modal -->
                  &lt;div class="modal fade" id="modal{{ tarefa.id }}" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                    &lt;div class="modal-dialog">
                      &lt;div class="modal-content">
                        &lt;div class="modal-header">
                          &lt;h5 class="modal-title" id="exampleModalLabel">{{ tarefa.descricao }} | {{ tarefa.categoria|capfirst }}&lt;/h5>
                          &lt;button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close">&lt;/button>
                        &lt;/div>
                        &lt;div class="modal-body">
                          &lt;p>
                            &lt;a class="btn btn-success" href="{% url 'concluir_tarefa' tarefa.id %}">Concluir&lt;/a> # novo
                          &lt;/p>
                        &lt;/div>
                      &lt;/div>
                    &lt;/div>
                  &lt;/div>
                {% endfor %}
              &lt;/div>
            &lt;/div>

          {% endblock %}

        </code>
      </pre>

      <h1>Passo 20: Implementar a funcionalidade do botão do exclusão de tarefas</h1>
      <p>
        Agora que a nossa aplicação já é capaz de concluir tarefas, vamos
        criar uma lógica bem parecida para a exclusão de tarefas.
      </p>
      <h4>Criando a view <i>excluir_tarefa()</i> </h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/views.py


          from django.shortcuts import render, redirect, get_object_or_404 # novo
          from .models import Tarefa
          from .forms import AdicionarTarefa

          def tarefas_pendentes_list(request):
              tarefas_pendentes = Tarefa.objects.filter(status='pendente')
              if request.method == 'POST':
                  form = AdicionarTarefa(data=request.POST)
                  if form.is_valid():
                      form.save()
                      return redirect('tarefas_pendentes_list')
              else:
                  form = AdicionarTarefa()
              return render(request, 'tarefas/tarefas_pendentes.html',
                            {'tarefas_pendentes':tarefas_pendentes,
                             'form':form})

          def concluir_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.status = 'concluído'
              tarefa.save()
              return redirect('tarefas_pendentes_list')

          # novo
          def excluir_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.delete()
              return redirect('tarefas_pendentes_list')

        </code>
      </pre>

      <h4>Adicionando URL para exclusão de tarefas</h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/urls.py


          from django.urls import path, include
          from . import views

          urlpatterns = [
              path('', views.tarefas_pendentes_list, name='tarefas_pendentes_list' ),
              path('&lt;int:tarefa_id>/concluir/', views.concluir_tarefa, name='concluir_tarefa'),
              path('&lt;int:tarefa_id>/excluir/', views.excluir_tarefa, name='excluir_tarefa'), # novo
          ]

        </code>
      </pre>

      <h4>Adicionado a opção para exclusão de tarefas no template <i>tarefas_pendentes.html</i></h4>
      <pre>
        <code class="language-markup">
          # tarefas/templates/tarefas/tarefas_pendentes.html


          {% extends 'base.html' %}
          {% load crispy_forms_tags %}

          {% block title %}Tarefas pendentes{% endblock %}

          {% block content %}
            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Adicionar Tarefa&lt;/h1>
              &lt;form method="post">
                {% csrf_token %}
                {{ form|crispy }}
                &lt;br>
                &lt;input class="btn btn-success" type="submit" value="Salvar">
              &lt;/form>
            &lt;/div>

            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Tarefas Pendentes:&lt;/h1>
              &lt;div class="list-group">
                {% for tarefa in tarefas_pendentes %}
                  {% if tarefa.categoria == 'urgente' %}
                    &lt;button type="button" class="list-group-item list-group-item-danger list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                  {% else %}
                    {% if tarefa.categoria == 'importante' %}
                      &lt;button type="button" class="list-group-item list-group-item-warning list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                    {% else %}
                      &lt;button type="button" class="list-group-item list-group-item-primary list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                    {% endif %}
                  {% endif %}
                    &lt;h5>{{ tarefa.descricao }}&lt;/h5>
                    &lt;small>Criado em: {{ tarefa.criacao.day }}/{{ tarefa.criacao.month }}/{{ tarefa.criacao.year }}&lt;/small>
                  &lt;/button>
                  &lt;!-- Modal -->
                  &lt;div class="modal fade" id="modal{{ tarefa.id }}" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                    &lt;div class="modal-dialog">
                      &lt;div class="modal-content">
                        &lt;div class="modal-header">
                          &lt;h5 class="modal-title" id="exampleModalLabel">{{ tarefa.descricao }} | {{ tarefa.categoria|capfirst }}&lt;/h5>
                          &lt;button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close">&lt;/button>
                        &lt;/div>
                        &lt;div class="modal-body">
                          &lt;p>
                            &lt;a class="btn btn-success" href="{% url 'concluir_tarefa' tarefa.id %}">Concluir&lt;/a>
                            &lt;a class="btn btn-danger" href="{% url 'excluir_tarefa' tarefa.id %}">Excluir&lt;/a> # novo
                          &lt;/p>
                        &lt;/div>
                      &lt;/div>
                    &lt;/div>
                  &lt;/div>
                {% endfor %}
              &lt;/div>
            &lt;/div>

          {% endblock %}

        </code>
      </pre>

      <h1>Passo 21: Implementar a funcionalidade do botão de adiamento de tarefas</h1>
      <h4>Criando a view <i>adiar_tarefa()</i></h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/views.py


          from django.shortcuts import render, redirect, get_object_or_404 # novo
          from .models import Tarefa
          from .forms import AdicionarTarefa

          def tarefas_pendentes_list(request):
              tarefas_pendentes = Tarefa.objects.filter(status='pendente')
              if request.method == 'POST':
                  form = AdicionarTarefa(data=request.POST)
                  if form.is_valid():
                      form.save()
                      return redirect('tarefas_pendentes_list')
              else:
                  form = AdicionarTarefa()
              return render(request, 'tarefas/tarefas_pendentes.html',
                            {'tarefas_pendentes':tarefas_pendentes,
                             'form':form})

          def concluir_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.status = 'concluído'
              tarefa.save()
              return redirect('tarefas_pendentes_list')

          def excluir_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.delete()
              return redirect('tarefas_pendentes_list')

          # novo
          def adiar_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.status = 'adiado'
              tarefa.save()
              return redirect('tarefas_pendentes_list')


        </code>
      </pre>

      <h4>Criando URL para adiamento de tarefas</h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/urls.py


          from django.urls import path, include
          from . import views

          urlpatterns = [
              path('', views.tarefas_pendentes_list, name='tarefas_pendentes_list' ),
              path('&lt;int:tarefa_id>/concluir/', views.concluir_tarefa, name='concluir_tarefa'),
              path('&lt;int:tarefa_id>/excluir/', views.excluir_tarefa, name='excluir_tarefa'),
              path('&lt;int:tarefa_id>/adiar/', views.adiar_tarefa, name='adiar_tarefa'), # novo
          ]

        </code>
      </pre>

      <h4>Adicionando a opção para adiamento de tarefas no template <i>tarefas_pendentes.html</i></h4>
      <pre>
        <code class="language-markup">
          # tarefas/templates/tarefas/tarefas_pendentes.html


          {% extends 'base.html' %}
          {% load crispy_forms_tags %}

          {% block title %}Tarefas pendentes{% endblock %}

          {% block content %}
            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Adicionar Tarefa&lt;/h1>
              &lt;form method="post">
                {% csrf_token %}
                {{ form|crispy }}
                &lt;br>
                &lt;input class="btn btn-success" type="submit" value="Salvar">
              &lt;/form>
            &lt;/div>

            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Tarefas Pendentes:&lt;/h1>
              &lt;div class="list-group">
                {% for tarefa in tarefas_pendentes %}
                  {% if tarefa.categoria == 'urgente' %}
                    &lt;button type="button" class="list-group-item list-group-item-danger list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                  {% else %}
                    {% if tarefa.categoria == 'importante' %}
                      &lt;button type="button" class="list-group-item list-group-item-warning list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                    {% else %}
                      &lt;button type="button" class="list-group-item list-group-item-primary list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                    {% endif %}
                  {% endif %}
                    &lt;h5>{{ tarefa.descricao }}&lt;/h5>
                    &lt;small>Criado em: {{ tarefa.criacao.day }}/{{ tarefa.criacao.month }}/{{ tarefa.criacao.year }}&lt;/small>
                  &lt;/button>
                  &lt;!-- Modal -->
                  &lt;div class="modal fade" id="modal{{ tarefa.id }}" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                    &lt;div class="modal-dialog">
                      &lt;div class="modal-content">
                        &lt;div class="modal-header">
                          &lt;h5 class="modal-title" id="exampleModalLabel">{{ tarefa.descricao }} | {{ tarefa.categoria|capfirst }}&lt;/h5>
                          &lt;button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close">&lt;/button>
                        &lt;/div>
                        &lt;div class="modal-body">
                          &lt;p>
                            &lt;a class="btn btn-success" href="{% url 'concluir_tarefa' tarefa.id %}">Concluir&lt;/a>
                            &lt;a class="btn btn-danger" href="{% url 'excluir_tarefa' tarefa.id %}">Excluir&lt;/a>
                            &lt;a class="btn btn-warning" href="{% url 'adiar_tarefa' tarefa.id %}">Adiar&lt;/a> # novo
                          &lt;/p>
                        &lt;/div>
                      &lt;/div>
                    &lt;/div>
                  &lt;/div>
                {% endfor %}
              &lt;/div>
            &lt;/div>

          {% endblock %}

        </code>
      </pre>
      <hr>

      <h1>Passo 22: Implementar a funcionalidade de edição de tarefas</h1>
      <p>
        Talvez um usuário queira editar a descrição ou a categoria de uma
        tarefa já adicionada ao banco de dados da aplicação. Para isso, vamos
        implementar a funcionalidade de edição de tarefas.
      </p>
      <p>
        Primeiramente, vamos criar um novo formulário para receber os dados de
        entrada da usuário para edição da tarefa. Este formulário será criado
        através de uma classe definida no arquivo <i>forms.py</i> do app
        <i>Tarefas.</i>
      </p>
      <h4>Criando o form <i>EditarTarefaForm</i></h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/forms.py


          from django import forms
          from .models import Tarefa

          class AdicionarTarefa(forms.ModelForm):
              class Meta:
                  model = Tarefa
                  fields = ('descricao', 'categoria')

          # novo
          class EditarTarefaForm(forms.Form):
              OPCOES_CATEGORIA = (
                  ('urgente', 'Urgente'),
                  ('importante', 'Importante'),
                  ('precisa ser feito', 'Precisa ser feito')
              )
              tarefa = forms.CharField(max_length=400)
              categoria = forms.ChoiceField(choices=OPCOES_CATEGORIA)
        </code>
      </pre>
      <p>
        Com o form definido, podemos agora criar uma view para tratar o form
        e enviar informações para o template (que ainda será criado) utilizado
        para editar tarefas existentes.
      </p>
      <h4>Criando a view <i>editar_tarefa()</i></h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/views.py


          from django.shortcuts import render, redirect, get_object_or_404 # novo
          from .models import Tarefa
          from .forms import AdicionarTarefa, EditarTarefaForm

          def tarefas_pendentes_list(request):
              tarefas_pendentes = Tarefa.objects.filter(status='pendente')
              if request.method == 'POST':
                  form = AdicionarTarefa(data=request.POST)
                  if form.is_valid():
                      form.save()
                      return redirect('tarefas_pendentes_list')
              else:
                  form = AdicionarTarefa()
              return render(request, 'tarefas/tarefas_pendentes.html',
                            {'tarefas_pendentes':tarefas_pendentes,
                             'form':form})

          def concluir_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.status = 'concluído'
              tarefa.save()
              return redirect('tarefas_pendentes_list')

          def excluir_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.delete()
              return redirect('tarefas_pendentes_list')

          def adiar_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.status = 'adiado'
              tarefa.save()
              return redirect('tarefas_pendentes_list')

          # novo
          def editar_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              if request.method == 'POST':
                  form = EditarTarefaForm(request.POST)
                  if form.is_valid():
                      cd = form.cleaned_data
                      tarefa.descricao = cd['tarefa']
                      tarefa.categoria = cd['categoria']
                      tarefa.save()
                      return redirect('tarefas_pendentes_list')
              else:
                  form = EditarTarefaForm(initial={'tarefa':tarefa.descricao, 'categoria':tarefa.categoria})
              return render(request, 'tarefas/editar_tarefa.html', {'tarefa':tarefa, 'form':form})

        </code>
      </pre>
      <p>
        Ainda precisamos de uma URL para chamar a view recém criada e de criar
        o template renderizado pela view, <i>tarefas/editar_tarefa.html</i>.
      </p>

      <h4>Adicionando a URL para chamar a view <i>editar_tarefa()</i></h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/urls.py


          from django.urls import path, include
          from . import views

          urlpatterns = [
              path('', views.tarefas_pendentes_list, name='tarefas_pendentes_list' ),
              path('&lt;int:tarefa_id>/concluir/', views.concluir_tarefa, name='concluir_tarefa'),
              path('&lt;int:tarefa_id>/excluir/', views.excluir_tarefa, name='excluir_tarefa'),
              path('&lt;int:tarefa_id>/adiar/', views.adiar_tarefa, name='adiar_tarefa'),
              path('&lt;int:tarefa_id>/editar/', views.editar_tarefa, name='editar_tarefa'), # novo
          ]

        </code>
      </pre>

      <p>
        O último passo é criar um novo template dentro no caminho <i>tarefas/templates/tarefas</i>
        chamado <i>editar_tarefa.html</i>.
      </p>
      <pre>
        <code class="language-treeview">
          dia_organizado/
          |-- dia_organizado/
          |   `-- ...
          |-- tarefas/
          |   |-- migrations/
          |   |   `-- ...
          |   |-- templates/
          |   |   |-- ...
          |   |   `-- editar_tarefa.html
          |   |-- __init__.py
          |   |-- admin.py
          |   |-- apps.py
          |   |-- models.py
          |   |-- tests.py
          |   |-- urls.py
          |   |-- forms.py
          |   `-- views.py
          `-- manage.py
        </code>
      </pre>

      <h4>Template <i>editar_tarefa.html</i></h4>
      <pre>
        <code class="language-markup">
          # tarefas/templates/tarefas/editar_tarefa.html


          {% extends 'base.html' %}
          {% load crispy_forms_tags %}

          {% block title %}{{ tarefa.descricao }}{% endblock %}

          {% block content %}
            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Editar {{ tarefa.descricao }}&lt;/h1>
              &lt;form method="post">
                {% csrf_token %}
                {{ form|crispy }}
                &lt;br>
                &lt;input class="btn btn-success" type="submit" value="Salvar alterações">
                &lt;a class="btn btn-danger" href="{% url 'tarefas_pendentes_list' %}">Cancelar&lt;/a>
              &lt;/form>
            &lt;/div>

          {% endblock %}

        </code>
      </pre>


      <p>
        Por fim, vamos adicionar a opção de edição de tarefas ao tamplate <i>tarefas_pendentes.html</i>
      </p>
      <pre>
        <code class="language-markup">
          # tarefas/templates/tarefas/tarefas_pendentes.html


          {% extends 'base.html' %}
          {% load crispy_forms_tags %}

          {% block title %}Tarefas pendentes{% endblock %}

          {% block content %}
            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Adicionar Tarefa&lt;/h1>
              &lt;form method="post">
                {% csrf_token %}
                {{ form|crispy }}
                &lt;br>
                &lt;input class="btn btn-success" type="submit" value="Salvar">
              &lt;/form>
            &lt;/div>

            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Tarefas Pendentes:&lt;/h1>
              &lt;div class="list-group">
                {% for tarefa in tarefas_pendentes %}
                  {% if tarefa.categoria == 'urgente' %}
                    &lt;button type="button" class="list-group-item list-group-item-danger list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                  {% else %}
                    {% if tarefa.categoria == 'importante' %}
                      &lt;button type="button" class="list-group-item list-group-item-warning list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                    {% else %}
                      &lt;button type="button" class="list-group-item list-group-item-primary list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                    {% endif %}
                  {% endif %}
                    &lt;h5>{{ tarefa.descricao }}&lt;/h5>
                    &lt;small>Criado em: {{ tarefa.criacao.day }}/{{ tarefa.criacao.month }}/{{ tarefa.criacao.year }}&lt;/small>
                  &lt;/button>
                  &lt;!-- Modal -->
                  &lt;div class="modal fade" id="modal{{ tarefa.id }}" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                    &lt;div class="modal-dialog">
                      &lt;div class="modal-content">
                        &lt;div class="modal-header">
                          &lt;h5 class="modal-title" id="exampleModalLabel">{{ tarefa.descricao }} | {{ tarefa.categoria|capfirst }}&lt;/h5>
                          &lt;button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close">&lt;/button>
                        &lt;/div>
                        &lt;div class="modal-body">
                          &lt;p>
                            &lt;a class="btn btn-success" href="{% url 'concluir_tarefa' tarefa.id %}">Concluir&lt;/a>
                            &lt;a class="btn btn-danger" href="{% url 'excluir_tarefa' tarefa.id %}">Excluir&lt;/a>
                            &lt;a class="btn btn-warning" href="{% url 'adiar_tarefa' tarefa.id %}">Adiar&lt;/a>
                            &lt;a class="btn btn-primary" href="{% url 'editar_tarefa' tarefa.id %}">Editar&lt;/a> # novo
                          &lt;/p>
                        &lt;/div>
                      &lt;/div>
                    &lt;/div>
                  &lt;/div>
                {% endfor %}
              &lt;/div>
            &lt;/div>

          {% endblock %}

        </code>
      </pre>

      <h1>Passo 23: Visualizando tarefas concluídas</h1>
      <p>
        Agora que nossa aplicação já sabe como concluir tarefas, podemos querer
        visualizar as tarefas que já foram concluídas. Para isso, precisaremos
        de uma nova URL, uma nova view e um novo template.
      </p>
      <p>
        A URL será requisitada pelo usuário da aplicação e estará conectada com
        uma view. A view vai puxar do banco de dados da aplicação todas as
        tarefas que têm o status 'concluído' e enviar para um template que
        mostrará a lista de tarefas concluídas.
      </p>
      <h4>Definindo a URL de tarefas concluídas</h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/urls.py


          from django.urls import path, include
          from . import views

          urlpatterns = [
              path('', views.tarefas_pendentes_list, name='tarefas_pendentes_list' ),
              path('&lt;int:tarefa_id>/concluir/', views.concluir_tarefa, name='concluir_tarefa'),
              path('&lt;int:tarefa_id>/excluir/', views.excluir_tarefa, name='excluir_tarefa'),
              path('&lt;int:tarefa_id>/adiar/', views.adiar_tarefa, name='adiar_tarefa'),
              path('&lt;int:tarefa_id>/editar/', views.editar_tarefa, name='editar_tarefa'),
              path('concluidas/', views.tarefas_concluidas_list, name='tarefas_concluidas_list'), # novo
          ]
        </code>
      </pre>

      <h4>Criando a view <i>tarefas_concluidas_list()</i></h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/views.py


          from django.shortcuts import render, redirect, get_object_or_404 # novo
          from .models import Tarefa
          from .forms import AdicionarTarefa, EditarTarefaForm

          def tarefas_pendentes_list(request):
              tarefas_pendentes = Tarefa.objects.filter(status='pendente')
              if request.method == 'POST':
                  form = AdicionarTarefa(data=request.POST)
                  if form.is_valid():
                      form.save()
                      return redirect('tarefas_pendentes_list')
              else:
                  form = AdicionarTarefa()
              return render(request, 'tarefas/tarefas_pendentes.html',
                            {'tarefas_pendentes':tarefas_pendentes,
                             'form':form})

          def concluir_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.status = 'concluído'
              tarefa.save()
              return redirect('tarefas_pendentes_list')

          def excluir_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.delete()
              return redirect('tarefas_pendentes_list')

          def adiar_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.status = 'adiado'
              tarefa.save()
              return redirect('tarefas_pendentes_list')

          def editar_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              if request.method == 'POST':
                  form = EditarTarefaForm(request.POST)
                  if form.is_valid():
                      cd = form.cleaned_data
                      tarefa.descricao = cd['tarefa']
                      tarefa.categoria = cd['categoria']
                      tarefa.save()
                      return redirect('tarefas_pendentes_list')
              else:
                  form = EditarTarefaForm(initial={'tarefa':tarefa.descricao, 'categoria':tarefa.categoria})
              return render(request, 'tarefas/editar_tarefa.html', {'tarefa':tarefa, 'form':form})

          # novo
          def tarefas_concluidas_list(request):
              tarefas_concluidas = Tarefa.objects.filter(status='concluído')
              return render(request, 'tarefas/tarefas_concluidas.html', {'tarefas_concluidas':tarefas_concluidas})

        </code>
      </pre>

      <h4>Criando o template <i>tarefas_concluidas.html</i></h4>
      <pre>
        <code class="language-markup">
          # tarefas/templates/tarefas/tarefas_concluidas.html


          {% extends 'base.html' %}

          {% block title %}Tarefas Concluídas{% endblock %}

          {% block content %}
            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Tarefas Concluídas&lt;/h1>
              &lt;div class="list-group">
                {% for tarefa in tarefas_concluidas %}
                  &lt;button type="button" class="list-group-item list-group-item-success list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                    &lt;h5>{{ tarefa.descricao }}&lt;/h5>
                    &lt;small>Criado em: {{ tarefa.criacao.day }}/{{ tarefa.criacao.month }}/{{ tarefa.criacao.year }}&lt;/small>
                  &lt;/button>
                  &lt;!-- Modal -->
                  &lt;div class="modal fade" id="modal{{ tarefa.id }}" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                    &lt;div class="modal-dialog">
                      &lt;div class="modal-content">
                        &lt;div class="modal-header">
                          &lt;h5 class="modal-title" id="exampleModalLabel">{{ tarefa.descricao }} | {{ tarefa.categoria|capfirst }}&lt;/h5>
                          &lt;button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close">&lt;/button>
                        &lt;/div>
                        &lt;div class="modal-body">
                          &lt;p>
                            &lt;a class="btn btn-danger" href="{% url 'excluir_tarefa' tarefa.id %}">Excluir&lt;/a>
                          &lt;/p>
                        &lt;/div>
                      &lt;/div>
                    &lt;/div>
                  &lt;/div>
                {% empty %}
                  &lt;h2>Nenhuma tarefa foi concluída&lt;/h2>
                {% endfor %}
              &lt;/div>
            &lt;/div>
          {% endblock content %}

        </code>
      </pre>

      <p>
        Agora, ao visitar a URL <i>HOST/tarefas/concluidas/</i> será possível
        ver uma lista com todas as tarefas que já foram concluídas. Nessa página,
        é possível clicar nas tarefas e excluí-las do banco de dados da aplicação.
      </p>
      <hr>

      <h1>Passo 24: Visualizando tarefas adiadas</h1>
      <p>
        Vamos agora implementar uma funcionalidade parecida com a do passo anterior.
        A diferença é que agora queremos visualizar as tarefas que foram adiadas.
        Também vamos criar uma view para alterar o status das tarefas adiadas de
        modo que eles retornem para a lista de tarefas pendentes.
      </p>

      <h4>Definindo a URL de tarefas adiadas</h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/urls.py


          from django.urls import path, include
          from . import views

          urlpatterns = [
              path('', views.tarefas_pendentes_list, name='tarefas_pendentes_list' ),
              path('&lt;int:tarefa_id>/concluir/', views.concluir_tarefa, name='concluir_tarefa'),
              path('&lt;int:tarefa_id>/excluir/', views.excluir_tarefa, name='excluir_tarefa'),
              path('&lt;int:tarefa_id>/adiar/', views.adiar_tarefa, name='adiar_tarefa'),
              path('&lt;int:tarefa_id>/editar/', views.editar_tarefa, name='editar_tarefa'),
              path('concluidas/', views.tarefas_concluidas_list, name='tarefas_concluidas_list'),
              path('adiadas/', views.tarefas_adiadas_list, name='tarefas_adiadas_list'), # novo
          ]
        </code>
      </pre>

      <h4>Criando a view <i>tarefas_adiadas_list()</i></h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/views.py


          from django.shortcuts import render, redirect, get_object_or_404 # novo
          from .models import Tarefa
          from .forms import AdicionarTarefa, EditarTarefaForm

          def tarefas_pendentes_list(request):
              tarefas_pendentes = Tarefa.objects.filter(status='pendente')
              if request.method == 'POST':
                  form = AdicionarTarefa(data=request.POST)
                  if form.is_valid():
                      form.save()
                      return redirect('tarefas_pendentes_list')
              else:
                  form = AdicionarTarefa()
              return render(request, 'tarefas/tarefas_pendentes.html',
                            {'tarefas_pendentes':tarefas_pendentes,
                             'form':form})

          def concluir_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.status = 'concluído'
              tarefa.save()
              return redirect('tarefas_pendentes_list')

          def excluir_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.delete()
              return redirect('tarefas_pendentes_list')

          def adiar_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.status = 'adiado'
              tarefa.save()
              return redirect('tarefas_pendentes_list')

          def editar_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              if request.method == 'POST':
                  form = EditarTarefaForm(request.POST)
                  if form.is_valid():
                      cd = form.cleaned_data
                      tarefa.descricao = cd['tarefa']
                      tarefa.categoria = cd['categoria']
                      tarefa.save()
                      return redirect('tarefas_pendentes_list')
              else:
                  form = EditarTarefaForm(initial={'tarefa':tarefa.descricao, 'categoria':tarefa.categoria})
              return render(request, 'tarefas/editar_tarefa.html', {'tarefa':tarefa, 'form':form})

          def tarefas_concluidas_list(request):
              tarefas_concluidas = Tarefa.objects.filter(status='concluído')
              return render(request, 'tarefas/tarefas_concluidas.html', {'tarefas_concluidas':tarefas_concluidas})

          # novo
          def tarefas_adiadas_list(request):
              tarefas_adiadas = Tarefa.objects.filter(status='adiado')
              return render(request, 'tarefas/tarefas_adiadas.html', {'tarefas_adiadas':tarefas_adiadas})


        </code>
      </pre>

      <h4>Criando o template <i>tarefas_adiadas.html</i></h4>
      <pre>
        <code class="language-markup">
          # tarefas/templates/tarefas/tarefas_adiadas.html


          {% extends 'base.html' %}

          {% block title %}Tarefas Concluídas{% endblock %}

          {% block content %}
            &lt;div class="h-100 p-5 bg-light border rounded-3">
              &lt;h1>Tarefas Adiadas&lt;/h1>
              &lt;div class="list-group">
                {% for tarefa in tarefas_adiadas %}
                  &lt;button type="button" class="list-group-item list-group-item-warning list-group-item-action" data-bs-toggle="modal" data-bs-target="#modal{{ tarefa.id }}">
                    &lt;h5>{{ tarefa.descricao }}&lt;/h5>
                    &lt;small>Criado em: {{ tarefa.criacao.day }}/{{ tarefa.criacao.month }}/{{ tarefa.criacao.year }}&lt;/small>
                  &lt;/button>
                  &lt;!-- Modal -->
                  &lt;div class="modal fade" id="modal{{ tarefa.id }}" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                    &lt;div class="modal-dialog">
                      &lt;div class="modal-content">
                        &lt;div class="modal-header">
                          &lt;h5 class="modal-title" id="exampleModalLabel">{{ tarefa.descricao }} | {{ tarefa.categoria|capfirst }}&lt;/h5>
                          &lt;button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close">&lt;/button>
                        &lt;/div>
                        &lt;div class="modal-body">
                          &lt;p>
                            &lt;a class="btn btn-success" href="{% url 'mover_para_tarefas' tarefa.id %}">Mover para lista de tarefas&lt;/a>
                            &lt;a class="btn btn-danger" href="{% url 'excluir_tarefa' tarefa.id %}">Excluir&lt;/a>
                            &lt;a class="btn btn-primary" href="{% url 'editar_tarefa' tarefa.id %}">Editar&lt;/a>

                          &lt;/p>
                        &lt;/div>
                      &lt;/div>
                    &lt;/div>
                  &lt;/div>
                {% empty %}
                  &lt;h2>Nenhuma tarefa foi adiada&lt;/h2>
                {% endfor %}
              &lt;/div>
            &lt;/div>
          {% endblock content %}



        </code>
      </pre>

      <h4>Criar a view <i>mover_para_tarefas()</i></h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/views.py


          from django.shortcuts import render, redirect, get_object_or_404 # novo
          from .models import Tarefa
          from .forms import AdicionarTarefa, EditarTarefaForm

          def tarefas_pendentes_list(request):
              tarefas_pendentes = Tarefa.objects.filter(status='pendente')
              if request.method == 'POST':
                  form = AdicionarTarefa(data=request.POST)
                  if form.is_valid():
                      form.save()
                      return redirect('tarefas_pendentes_list')
              else:
                  form = AdicionarTarefa()
              return render(request, 'tarefas/tarefas_pendentes.html',
                            {'tarefas_pendentes':tarefas_pendentes,
                             'form':form})

          def concluir_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.status = 'concluído'
              tarefa.save()
              return redirect('tarefas_pendentes_list')

          def excluir_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.delete()
              return redirect('tarefas_pendentes_list')

          def adiar_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.status = 'adiado'
              tarefa.save()
              return redirect('tarefas_pendentes_list')

          def editar_tarefa(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              if request.method == 'POST':
                  form = EditarTarefaForm(request.POST)
                  if form.is_valid():
                      cd = form.cleaned_data
                      tarefa.descricao = cd['tarefa']
                      tarefa.categoria = cd['categoria']
                      tarefa.save()
                      return redirect('tarefas_pendentes_list')
              else:
                  form = EditarTarefaForm(initial={'tarefa':tarefa.descricao, 'categoria':tarefa.categoria})
              return render(request, 'tarefas/editar_tarefa.html', {'tarefa':tarefa, 'form':form})

          def tarefas_concluidas_list(request):
              tarefas_concluidas = Tarefa.objects.filter(status='concluído')
              return render(request, 'tarefas/tarefas_concluidas.html', {'tarefas_concluidas':tarefas_concluidas})

          def tarefas_adiadas_list(request):
              tarefas_adiadas = Tarefa.objects.filter(status='adiado')
              return render(request, 'tarefas/tarefas_adiadas.html', {'tarefas_adiadas':tarefas_adiadas})

          # novo
          def mover_para_tarefas(request, tarefa_id):
              tarefa = get_object_or_404(Tarefa, id=tarefa_id)
              tarefa.status = 'pendente'
              tarefa.save()
              return redirect('tarefas_pendentes_list')

        </code>
      </pre>

      <h4>Adicionar URL para chamar a view <i>mover_para_tarefas()</i></h4>
      <pre class="language-python">
        <code class="language-python">
          # tarefas/urls.py


          from django.urls import path, include
          from . import views

          urlpatterns = [
              path('', views.tarefas_pendentes_list, name='tarefas_pendentes_list' ),
              path('&lt;int:tarefa_id>/concluir/', views.concluir_tarefa, name='concluir_tarefa'),
              path('&lt;int:tarefa_id>/excluir/', views.excluir_tarefa, name='excluir_tarefa'),
              path('&lt;int:tarefa_id>/adiar/', views.adiar_tarefa, name='adiar_tarefa'),
              path('&lt;int:tarefa_id>/editar/', views.editar_tarefa, name='editar_tarefa'),
              path('concluidas/', views.tarefas_concluidas_list, name='tarefas_concluidas_list'),
              path('adiadas/', views.tarefas_adiadas_list, name='tarefas_adiadas_list'),
              path('&lt;int:tarefa_id>/mover-para-lista-de-tarefas/', views.mover_para_tarefas, name='mover_para_tarefas'), # novo
          ]
        </code>
      </pre>
      <hr>

      <h1>Passo 25: Adicionando caminhos para o Navbar</h1>
      <p>
        Por enquanto, os links definidos na barra de navegação da aplicação não
        levam a lugar nenhum. Vamos corrigir este problema e a aplicação estará
        finalizada.
      </p>
      <h4>Editando o template base</h4>
      <pre>
        <code class="language-markup">
          # tarefas/templates/base.html


          &lt;!doctype html>
          &lt;html lang="en">
            &lt;head>
              &lt;!-- Required meta tags -->
              &lt;meta charset="utf-8">
              &lt;meta name="viewport" content="width=device-width, initial-scale=1">

              &lt;!-- Bootstrap CSS -->
              &lt;link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-eOJMYsd53ii+scO/bJGFsiCZc+5NDVN2yr8+0RDqr0Ql0h+rP48ckxlpbzKgwra6" crossorigin="anonymous">

              &lt;title>{% block title %}{% endblock %}&lt;/title>
            &lt;/head>
            &lt;body style="padding-top:70px">
              &lt;nav class="navbar fixed-top navbar-expand-lg navbar-dark bg-dark">
                &lt;div class="container-fluid">
                  &lt;a class="navbar-brand" href="{% url 'tarefas_pendentes_list' %}">DiaOrganizado&lt;/a> # novo
                  &lt;button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                    &lt;span class="navbar-toggler-icon">&lt;/span>
                  &lt;/button>
                  &lt;div class="collapse navbar-collapse" id="navbarSupportedContent">
                    &lt;ul class="navbar-nav me-auto mb-2 mb-lg-0">
                      &lt;li class="nav-item">
                        &lt;a class="nav-link active" aria-current="page" href="{% url 'tarefas_pendentes_list' %}">Tarefas&lt;/a> # novo
                      &lt;/li>
                      &lt;li class="nav-item dropdown">
                        &lt;a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                          Outras tarefas
                        &lt;/a>
                        &lt;ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                          &lt;li>&lt;a class="dropdown-item" href="{% url 'tarefas_adiadas_list' %}">Adiadas&lt;/a>&lt;/li> # novo
                          &lt;li>&lt;a class="dropdown-item" href="{% url 'tarefas_concluidas_list' %}">Concluídas&lt;/a>&lt;/li> # novo
                        &lt;/ul>
                      &lt;/li>
                    &lt;/ul>
                  &lt;/div>
                &lt;/div>
              &lt;/nav>

              &lt;div class="container">
                {% block content %}
                {% endblock %}
              &lt;/div>

              &lt;!-- Option 1: Bootstrap Bundle with Popper -->
              &lt;script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/js/bootstrap.bundle.min.js" integrity="sha384-JEW9xMcG8R+pH31jmWH6WWP0WintQrMb4s7ZOdauHnUtxwoG2vI5DkLtS3qm9Ekf" crossorigin="anonymous">&lt;/script>
            &lt;/body>
          &lt;/html>

        </code>
      </pre>

      <h1>Obrigado</h1>
      <p>
        Parabéns por ter chegado até aqui! Nos vemos no próximo tutorial.
      </p>
      <h3>Nossas redes sociais</h3>
      <a href="https://www.youtube.com/channel/UCSqHHdFpadrJNu6UnYdUhzw">Youtube</a>
      <a href="https://www.instagram.com/universipython/">Instagram</a>

      <footer class="mt-auto text-white-50 text-center">
        <p>UniversiPython</p>
      </footer>
    </div>

    <script src="prism.js"></script>
    <!-- Option 1: Bootstrap Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/js/bootstrap.bundle.min.js" integrity="sha384-JEW9xMcG8R+pH31jmWH6WWP0WintQrMb4s7ZOdauHnUtxwoG2vI5DkLtS3qm9Ekf" crossorigin="anonymous"></script>
  </body>
</html>
