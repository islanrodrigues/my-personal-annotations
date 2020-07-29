### Iniciando projeto com GatsbyJS
GatsbyJS é um _framework_ baseado em React para construção de sites estáticos.

**Instalando o CLI do Gatsby** -- O CLI do Gatsby permite criar uma estrutura pré-configurada e rodar comandos necessários para o desenvolvimento do projeto.
Necessário realizar a instalação do pacote globalmente. é necessário já possuir o Git e o NodeJS instalados.

```bash
npm install -g gatsby-cli
```

**Iniciando um projeto com Gatsby**
```bash
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```
Onde, 
O `new` é o comando para criar um novo projeto em Gatsby; 
O`hello-world` é um título arbitrário, ou seja, é o nome que você desejar. O CLI do Gatsby irá entender isso como um novo diretório e irá configurar o projeto a partir dele;
A URL no final do comando aponta para o repositório onde será buscado todas as informações necessárias para o _starter_. Se essa informação for omitida, o Gatsby irá gerar o projeto a partir de uma _starter_ padrão (_default_). Para visualizar todos os existentes, basta acessar a [biblioteca de starters](https://www.gatsbyjs.org/starters/?v=2).


**Iniciando o modo de desenvolvimento** -- 
```bash
gatsby develop
```
Esse comando inicia um servidor local para desenvolvimento. Por padrão esse servidor será iniciado na porta 8000.
Pra visualizar o site, só acessar: `http://localhost:8000/`. 