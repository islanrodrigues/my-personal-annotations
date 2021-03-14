### O que é uma virtualenv
Um ambiente virtual (ou _virtualenv_) serve para gerenciar as dependências de cada projeto. Em outras palavras, cada projeto deve ter sua própria _virtualenv_, impedindo assim que ocorra conflitos de versões de uma mesma dependência em diferentes projetos. Basicamente, uma _virtualenv_ empacota todas as dependências que um projeto precisa e armazena em um diretório, fazendo com que nenhum pacote seja instalado diretamente no SO.

**Criando uma _virtualenv_** -- para criação de uma _virtualenv_, basta invocar o comando do Python com os parâmetros `-m venv` e informar o diretório de destino.

Exemplo:
_Para Windows_
```bash
# será criado um diretório chamado venv dentro do caminho no qual o comando foi invocado
python -m venv venv
```

_Para Linux ou MacOS_
```bash
# será criado um diretório chamado venv dentro do caminho no qual o comando foi invocado
python3 -m venv venv
```

**Ativando uma _virtualenv_** -- para que seja possível instalar pacotes necessários para o projeto, é preciso que haja a ativação da _virtualenv_, o que pode ser feito de diferentes formas dependendo do sistema operacional.

Exemplo: 
_Para Windows_
```bash
# O comando é -> <source> <nome_da_virtualenv>/Scripts/activate
# Suponhamos que o nome da virtualenv seja venv e que estamos no diretório onde ela foi criada
. venv/Scripts/activate
```

_Para Linux ou MacOS_
```bash
# O comando é -> <source> <nome_da_virtualenv>/bin/activate
# Suponhamos que o nome da virtualenv seja venv e que estamos no diretório onde ela foi criada
. venv/bin/activate
```

**Desativando uma _virtualenv_** -- para desativar uma _virtualenv_, basta utilizar o comando `deactivate`.