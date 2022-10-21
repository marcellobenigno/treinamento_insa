# Aula 2 - Iniciando com o Django

Link da gravação: https://youtu.be/FEcUUEEQg0g

## 2.1 Criando o Projeto

Dentro do diretório `/home/code` (ou onde você preferir), crie uma pasta com o nome `siginsa` e siga os passos a seguir:

```bash
python -m venv .venv
source .venv/bin/activate
which python
pip install django
/home/marcello/code/siginsa/.venv/bin/python -m pip install --upgrade pip
pip install django
django-admin startproject siginsa .
python manage.py
```
## 2.2 Adicionando Shortcuts ao oh-my-zsh

Adicione no final do arquivo .zshrc:

```bash
# Python/Django
alias venv="python -m venv .venv && ve"
alias ve="source .venv/bin/activate"
alias vem="source .venv/bin/activate"
alias m='python $VIRTUAL_ENV/../manage.py'
alias mmm='m makemigrations'
alias mm='m migrate'
```

Lembre-se de dar um `source ~/.zshrc` para atualizar as configurações do arquivo.

## 2.3 Criando a app core

```bash
cd siginsa
m startapp core
```

Edite o arquivo `settings.py` adicionando a app `core`:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    # my apps
    'siginsa.core.apps.CoreConfig',
]
```

Altere o arquivo `siginsa/core/apps.py` para:

```python
from django.apps import AppConfig


class CoreConfig(AppConfig):
    default_auto_field = 'django.db.models.BigAutoField'
    name = 'siginsa.core'
```

Altere o arquivo `siginsa/urls.py` para:

```python
from django.conf import settings
from django.conf.urls.static import static
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('', include('siginsa.core.urls')),
    path('admin/', admin.site.urls),
]

if settings.DEBUG:
    urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

### 2.3.1 Criando a view index na app core

Alter o arquivo `siginsa/core/views.py` para:

```python
from django.shortcuts import render


def index(request):
	return render(request, 'core/index.html')
```

Crie dentro do diretório `core` outro diretório com o nome `templates`, em seguida, dentro deste último diretório, crie o arquivo `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>SIG-INSA</title>
</head>
<body>
	<h1>SIG-INSA</h1>
</body>
</html>
```

### 2.3.2 Criando o path da url na app core

Crie o arquivo `siginsa/core/urls.py` com o seguinte conteúdo:

```python
from django.urls import path
from . import views as v

app_name = 'core'

urlpatterns = [
	path('', v.index, name='index')
]
```

### 2.3.3 Visualizando o resultado

Com a virtualenv ativa, dentro da pasta do projeto, digite: 

```
m runserver
```

E verifique no navegador o resultado.



