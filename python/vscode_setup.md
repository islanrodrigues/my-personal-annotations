# Configuração do VSCode para se trabalhar com Python
Um descritivo sobre _plugins_ importantes para uso e configurações relevantes.

**Instalação de _plugins_** 
+ **`Code Runner (Jun Han)`** : interessante para que possamos executar os _scripts_ gerados em Python;
+ **`Python (Microsoft)`** : vai permitir suportar o desenvolvimento com a linguagem Python.

**Criação da _virtualenv_** -- criação do ambiente virtual onde será gravada todas as dependências específicas do projeto. Para este passo basta acessar [aqui](https://github.com/islanrodrigues/my-personal-annotations/blob/master/python/whats_virtualenv.md#o-que-%C3%A9-uma-virtualenv).

**Configurações globais do VSCode** -- adição de configurações globais através da manipulação do arquivo `settings.json`.
```json
{
  "code-runner.ignoreSelection": true,
  "code-runner.runInTerminal": true,

  "python.linting.mypyEnabled": true,
  "python.linting.flake8Enabled": true,
  "python.testing.unittestEnabled": true,

  "[python]": {
      "editor.formatOnSave": true
  }
}
```

**Configurações locais do VSCode** -- Ao se trabalhar com Python no VSCode, possa ser que haja a necessidade de adição de configurações locais, ou seja, que não faz sentido estarem aplicadas de forma global mas sim por projeto em específico. Para isso, é necessário dizer ao VSCode que será escolhido a versão do Python instalada na _virtualenv_, clicando no canto inferior esquerdo, onde está escrito o nome da linguagem e a versão.

![Select Python Version illustration](https://github.com/islanrodrigues/my-personal-annotations/blob/master/images/python/select_python_version_vscode.png)

Após isso, será exibido um _pop up_ para escolha da versão desejada.

![Select Python Venv Option illustration](https://github.com/islanrodrigues/my-personal-annotations/blob/master/images/python/select_python_venv_option.png)

Ao selecionar a opção, um diretório `.vscode` será automaticamente criado no projeto onde dentro dele haverá um arquivo `settings.json`. É neste arquivo onde irá as configurações locais desejadas.

Exemplo para Windows
```json
{
  "python.pythonPath": "venv/Scripts/python.exe",
  "code-runner.executorMap": {
    "python": "venv/Scripts/python.exe",
  }
}
```

Exemplo para Linux ou MacOS
```json
{
  "python.pythonPath": "venv/bin/python",
  "code-runner.executorMap": {
    "python": "venv/bin/python",
  }
}
```

**Informações adicionais** -- Através dessa configuração, possivelmente o _plugin_ do Python solicitará a instalação de outros _plugins_ necessários. Quando essa solicitação for disparada, só clicar para permitir.



