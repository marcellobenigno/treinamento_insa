# Aula 1 - Instalação do Ambiente de Desenvolvimento

Link da gravação: [https://youtu.be/zVYt8Ld-fJY](https://youtu.be/zVYt8Ld-fJY)

## 1. Instalação do oh-my-zsh

Primeiro, atualize a lista de pacotes:

```bash
sudo apt-get update && sudo apt-get upgrade
```


Em seguida, instale o oh-my-zsh:

```bash
sudo apt  install curl zsh git
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
sudo chsh -s $(which zsh) $(whoami)
```

## 2. Instalação do Pyenv

Use o pyenv https://github.com/pyenv/pyenv para baixar, instalar e gerenciar múltiplas versões do INTERPRETADOR Python na sua máquina.

Primeiro instale as dependências:

Linux (Ubuntu):

Abra um terminal, apertando o atalho CRTL + ALT + T ou digite aperte a tecla do windows e digite terminal, ou clique com o botão direito na tela, e escolha a opção "Abrir Terminal" (somente para Ubuntu 15.10 ou superior, para 14.04 é necessário instalar o pacote nautilus-open-terminal e reiniciar)


Instale os pacotes básicos

```bash
sudo apt-get install -y make build-essential git libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev

```

depois:

```bash
curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash
```

logo após, edite o arquivo .zshrc localizado na "Pasta Pessoal" ou Home do seu usuário, com o comando:

```shell
nano .zshrc
```

adicione esses comandos ao final do arquivo:

```shell
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
```
Feito isso dê um control+x, confirme para salvar o arquivo, feche e abra novamente o terminal.

Você pode ver as versões do interpretador Python que podem ser instalados com o comando:

```bash
pyenv install -l
```

Instale o pyenv (vamos usar a versão 3.8.0):

```bash
pyenv install 3.10.0
```

logo após, defina o Python 3.10.0 como o python padrão do seu usuário:

```bash
pyenv global 3.10.0
```


## 3. Instalação e Configuração do GeoServer no Ubuntu

### 3.1 Instalação do Java

```shell
sudo apt update && sudo apt upgrade -y
sudo apt install default-jdk
```
### 3.2 Liberação da porta 8080

```shell
sudo ufw allow 8080
```

### 3.3 Instalação do Tomcat9

```shell
sudo apt install tomcat9 tomcat9-admin
```

**Opcional:** Edite o arquivo `tomcat-users.xml`:

```shell
sudo nano /etc/tomcat9/tomcat-users.xml
```

Adicione o conteúdo abaixo nesse arquivo:

```xml
<role rolename="admin-gui"/>
<role rolename="manager-gui"/>
<user username="tomcat" password="pass" roles="admin-gui,manager-gui"/>
```

```shell
sudo systemctl enable tomcat9
sudo service tomcat9 status
```

### 3.4 Instalação do GeoServer

```shell[]()
sudo service tomcat9 stop

wget https://sourceforge.net/projects/geoserver/files/GeoServer/2.21.1/geoserver-2.21.1-war.zip

sudo cp geoserver-2.21.1-war.zip /var/lib/tomcat9/webapps/

cd /var/lib/tomcat9/webapps

sudo unzip geoserver-2.21.1-war.zip

sudo rm geoserver-2.21.1-war.zip

sudo service tomcat9 start
```

Verifique se o tomcat subiu o serviço:

```shell
sudo service tomcat9 status
```

### 3.5 Habilitando o CORS e o JSONP no GeoServer

Descomente as linhas indicadas no próprio arquivo:

```shell
sudo nano /var/lib/tomcat9/webapps/geoserver/WEB-INF/web.xml
```

## 4. Instalação do PostgreSQL e do PostGIS

```shell
sudo apt-get install -y postgis postgresql-14-pgrouting-scripts postgresql-14-postgis-3 postgresql-14-postgis-3-scripts
```

Em seguida, deve ser alterada a senha do usuário postgres:

```bash
sudo passwd postgres
```

De preferência, coloque uma senha fácil, no meu caso, deixei como postgres a senha deste usuário.

Também altere a senha do usuário postgres, dentro do banco template1:

```bash
psql -c "ALTER USER postgres WITH PASSWORD 'postgres'" -d template1
```

E crie um usuário de banco para o seu usuário do sistema operacional:

```bash
sudo su
su postgres
createuser -W -s marcello
```

Onde **"marcello"** deve ser substituído pelo seu nome de usuário.


Crie o banco de dados siginsa e habilite a extensão espacial

```bash
createdb siginsa
psql siginsa
create extension postgis;
\q
```

## 5. Instalação do QGIS

O QGIS pode ser facilmente instalado pela loja de aplicativos (Ubuntu Software Center).

## 6. Instalação do Sublime (ou de outro editor)

A escolha do editor é uma questão pessoal, irei utilizar o Sublime. Vocês podem assistir o vídeo sobre a instalação do mesmo.
