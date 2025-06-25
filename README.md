# projeto-django

https://padlet.com/deboramatipac/framework-django-h51u2t2e9v0t9no8

# Projeto Django com Templates HTML

Este repositório contém um exemplo mínimo de um projeto Django configurado para servir um template HTML simples. O objetivo é demonstrar a estrutura básica do Django, a criação de uma aplicação e a renderização de um arquivo HTML.

## Sumário

1.  [Pré-requisitos](#pré-requisitos)
2.  [Estrutura Inicial do Projeto Django](#estrutura-inicial-do-projeto-django)
3.  [Passo a Passo para Criação e Execução](#passo-a-passo-para-criação-e-execução)
    * [1. Configuração do Ambiente Virtual](#1-configuração-do-ambiente-virtual)
    * [2. Criação do Projeto Django](#2-criação-do-projeto-django)
    * [3. Criação de uma Aplicação](#3-criação-de-uma-aplicação)
    * [4. Registro da Aplicação](#4-registro-da-aplicação)
    * [5. Configuração do Diretório de Templates](#5-configuração-do-diretório-de-templates)
    * [6. Criação do Template HTML](#6-criação-do-template-html)
    * [7. Criação da View](#7-criação-da-view)
    * [8. Configuração das URLs da Aplicação](#8-configuração-das-urls-da-aplicação)
    * [9. Inclusão das URLs da Aplicação no Projeto Principal](#9-inclusão-das-urls-da-aplicação-no-projeto-principal)
    * [10. Execução das Migrações](#10-execução-das-migrações)
    * [11. Inicialização do Servidor de Desenvolvimento](#11-inicialização-do-servidor-de-desenvolvimento)
    * [12. Acesso no Navegador](#12-acesso-no-navegador)
4.  [Estrutura Final do Projeto](#estrutura-final-do-projeto)

## Pré-requisitos

Certifique-se de ter o Python 3.x instalado em sua máquina.

## Estrutura Inicial do Projeto Django

Quando você cria um projeto Django usando `django-admin startproject meu_projeto_web`, a estrutura inicial se assemelha a:

```bash
meu_projeto_web/
├── meu_projeto_web/    # Diretório do pacote Python do projeto
│   ├── init.py     # Indica que é um pacote Python
│   ├── settings.py     # Configurações do seu projeto Django
│   ├── urls.py         # Mapeamento de URLs do projeto principal
│   ├── wsgi.py         # Ponto de entrada para servidores web compatíveis com WSGI
│   └── asgi.py         # Ponto de entrada para servidores web compatíveis com ASGI (assíncrono, opcional)
└── manage.py           # Utilitário de linha de comando para interagir com o projeto
```


## Passo a Passo para Criação e Execução

Siga os passos abaixo para configurar e executar o projeto.

### 1. Configuração do Ambiente Virtual

É uma boa prática criar um ambiente virtual para isolar as dependências do projeto.

```bash
# Cria um ambiente virtual chamado 'venv'
python -m venv venv
```

```bash
# Ativa o ambiente virtual
.\venv_django\Scripts\activate
```

### 2. Criação do Projeto Django

Instale o Django e crie o projeto inicial.

# Instala o Django no ambiente virtual ativo
pip install django

# Cria um novo projeto Django chamado 'meu_projeto_web'
django-admin startproject meu_projeto_web

# Navega para o diretório raiz do projeto
cd meu_projeto_web

### 3. Criação de uma Aplicação

Crie uma aplicação Django dentro do projeto. Aplicativos são módulos que encapsulam funcionalidades específicas.

# Cria uma nova aplicação Django chamada 'minha_app'
python manage.py startapp minha_app

Estrutura após a criação da aplicação (minha_app):

```bash
meu_projeto_web/
├── meu_projeto_web/
│   ├── ... (arquivos do projeto)
├── minha_app/          # Diretório da sua aplicação
│   ├── migrations/     # Armazena arquivos de migração de banco de dados
│   ├── __init__.py     # Indica que é um pacote Python
│   ├── admin.py        # Para registrar modelos no painel de administração do Django
│   ├── apps.py         # Configuração da aplicação
│   ├── models.py       # Onde você define os modelos de dados (tabelas do banco)
│   ├── tests.py        # Onde você escreve os testes automatizados para a aplicação
│   └── views.py        # Contém as funções/classes que processam requisições e retornam respostas
└── manage.py
```

### 4. Registro da Aplicação

Adicione a nova aplicação à lista de INSTALLED_APPS nas configurações do seu projeto para que o Django a reconheça.

Abra o arquivo meu_projeto_web/settings.py e adicione 'minha_app' à lista INSTALLED_APPS:

# meu_projeto_web/settings.py

```bash
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'minha_app',  # <-- Adicione esta linha para registrar sua aplicação
]
```

### 5. Configuração do Diretório de Templates

Informe ao Django onde encontrar seus arquivos HTML (templates).

No mesmo meu_projeto_web/settings.py, adicione ou modifique a configuração DIRS dentro de TEMPLATES:

# meu_projeto_web/settings.py

import os # <-- Certifique-se que esta linha esteja no topo do arquivo se não estiver

```bash
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'templates')], # <-- Define o diretório 'templates' na raiz do projeto
        'APP_DIRS': True, # Permite que o Django procure templates dentro das pastas de apps também (ex: minha_app/templates/)
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
```

### 6. Criação do Template HTML

Crie o diretório templates na raiz do seu projeto (ao lado de manage.py e das pastas meu_projeto_web e minha_app) e adicione seu arquivo HTML.

# Na raiz do seu projeto (meu_projeto_web/)
mkdir templates
cd templates

Edite o arquivo meu_projeto_web/templates/meu_primeiro_html.html com o seguinte conteúdo:

```bash
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meu Primeiro Template Django</title>
</head>
<body>
    <h1>Olá, Mundo!</h1>
    <p>Este é o meu primeiro HTML servido por um template Django.</p>
    <p>A data e hora atuais são: {{ data_e_hora }}</p>
</body>
</html>
```

### 7. Criação da View

Defina uma função de view em sua aplicação (minha_app/views.py) que processará a requisição e renderizará o template HTML.

Abra o arquivo minha_app/views.py e adicione o código:

# minha_app/views.py
from django.shortcuts import render
from datetime import datetime

def home_view(request):
    """
    Renderiza a página inicial com um template HTML, passando a data e hora atuais como contexto.
    """
    context = {
        'data_e_hora': datetime.now() # Variável Python que será acessível no template HTML
    }
    return render(request, 'meu_primeiro_html.html', context) # Renderiza o template especificado

### 8. Configuração das URLs da Aplicação

Crie um arquivo urls.py dentro da sua aplicação (minha_app/) para organizar as URLs específicas dela.

# Navegue para a pasta da sua aplicação (minha_app/)
cd minha_app

# minha_app/urls.py
from django.urls import path
from . import views # <-- Importa as views do arquivo views.py desta aplicação

urlpatterns = [
    path('', views.home_view, name='home'), # Mapeia a URL raiz desta aplicação ('' ) para a função home_view
]

### 9. Inclusão das URLs da Aplicação no Projeto Principal

Inclua as URLs da sua aplicação no arquivo urls.py principal do projeto para que sejam acessíveis.

# Volte para a raiz do seu projeto (meu_projeto_web/)
cd ..

Abra o arquivo meu_projeto_web/urls.py e adicione a linha path('minha-pagina/', include('minha_app.urls')):

# meu_projeto_web/urls.py
from django.contrib import admin
from django.urls import path, include # <-- Importe 'include' para incluir URLs de outras apps

urlpatterns = [
    path('admin/', admin.site.urls), # URL padrão para o painel de administração do Django
    path('minha-pagina/', include('minha_app.urls')), # Inclui as URLs definidas em 'minha_app/urls.py' sob o prefixo '/minha-pagina/'
]

### 10. Execução das Migrações

Execute as migrações de banco de dados para criar as tabelas necessárias para as aplicações padrão do Django (como autenticação e administração).

# Na raiz do seu projeto (meu_projeto_web/)
python manage.py migrate

### 11. Inicialização do Servidor de Desenvolvimento

Inicie o servidor de desenvolvimento do Django.

# Na raiz do seu projeto (meu_projeto_web/)
python manage.py runserver

Você verá uma mensagem indicando que o servidor foi iniciado, geralmente em http://127.0.0.1:8000/ ou http://localhost:8000/.

### 12. Acesso no Navegador

Abra seu navegador web e acesse a URL que configuramos para o seu templ

http://localhost:8000/minha-pagina/

Você deverá ver o conteúdo do seu meu_primeiro_html.html renderizado, incluindo a data e hora atuais.

Estrutura Final do Projeto
Após seguir todos os passos, a estrutura de pastas do seu projeto Django será a seguinte:

meu_projeto_web/
├── meu_projeto_web/                # Diretório do pacote Python do projeto
│   ├── __init__.py                 # Indica que é um pacote Python
│   ├── settings.py                 # Configurações do projeto
│   ├── urls.py                     # Mapeamento de URLs do projeto principal
│   ├── wsgi.py                     # Ponto de entrada WSGI para servidores web
│   └── asgi.py                     # Ponto de entrada ASGI (opcional, para assíncrono)
│
├── minha_app/                      # Diretório da sua aplicação
│   ├── migrations/                 # Arquivos de migração do banco de dados (gerados)
│   │   └── __init__.py             # Indica que é um pacote Python
│   ├── __init__.py                 # Indica que é um pacote Python
│   ├── admin.py                    # Registro de modelos para o admin Django
│   ├── apps.py                     # Configuração da aplicação
│   ├── models.py                   # Definição dos modelos de dados
│   ├── tests.py                    # Testes automatizados da aplicação
│   ├── views.py                    # Funções/classes que processam requisições e renderizam templates
│   └── urls.py                     # Mapeamento de URLs ESPECÍFICAS para minha_app (criado por você)
│
├── templates/                      # Diretório customizado para templates HTML (criado por você)
│   └── meu_primeiro_html.html      # Seu arquivo HTML (criado por você)
│
├── db.sqlite3                      # Arquivo do banco de dados padrão SQLite (gerado após migrate)
└── manage.py                       # Utilitário de linha de comando do Django
