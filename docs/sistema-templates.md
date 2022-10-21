# Aula 3 - Sistema de Templates e Arquivos Estáticos


Para que o Django sirva os arquivos estáticos e de media (arquivos de upload) de forma correta, iremos realizar duas alterações.

* No arquivo `settings.py`:

Na linha 12, adicione:

```python
import os
```

E na seção dos arquivos estáticos (procure pelo comentário abaixo):

```python
# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/4.1/howto/static-files/

STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'mediafiles')
```

* E no arquivo `siginsa/urls.py`

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

## 3.1 Criando o Arquivo `base.html`

Baixe o Boostrap5 neste [link](https://getbootstrap.com/docs/5.2/getting-started/download/). Descompacte a pasta dentro do diretório `siginsa/core/static/libs`

```html

```




