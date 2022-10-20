# Aula 2 - Iniciando com o Django

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

Adicione no final do arquivo .zshrc

```bash
# Python/Django
alias venv="python -m venv .venv && ve"
alias ve="source .venv/bin/activate"
alias vem="source .venv/bin/activate"
alias m='python $VIRTUAL_ENV/../manage.py'
alias mmm='m makemigrations'
alias mm='m migrate'
```
