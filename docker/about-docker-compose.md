### Docker Compose
Definição do Docker Compose, segundo a documentação oficial: 
> Compose é uma ferramenta para definir e executar aplicações de vários containers. Com o Compose, você usa um arquivo YAML para configurar os serviços da sua aplicação. Então, com um único comando, você cria e inicia todos os serviços de sua configuração.

Em outras palavras, o Docker Compose é um orquestrador de containers. E essa orquestração se dá através da criação do arquivo `docker-compose.yml`, escrito em [YAML](https://pt.wikipedia.org/wiki/YAML).  
Segue abaixo uma representação deste arquivo.

```yml
version: "3.9"  # optional since v1.27.0
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/code
      - logvolume01:/var/log
    links:
      - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```
Neste arquivo é definido todos os serviços que precisarão ser orquestrados, quais imagens e volumes envolvidos etc.   
É possível usar o Docker Compose em todos os ambientes (_development_, _test_, _production_), bem como em _workflows_ de CI. 

**Instalando o Docker Compose** -- por se tratar de uma ferramenta para orquestração de containers Docker, é necessário que o Docker _engine_ já tenha sido instalado anteriormente.    
Para instalação da ferramenta de acordo com sistema operacional, [vide documentação oficial](https://docs.docker.com/compose/install/).

**Executando o Compose** -- estando no mesmo diretório que o arquivo `docker-compose.yml`, para executar o Compose basta rodar o comando `docker-compose up`. É possível usar a _flag_ `-d` para que a execução rode em _background_.

**Listando as aplicações** -- para listar todos os containers que foram executados pelo Compose, basta rodar o comando `docker-compose ps`. Esse comando também dispõe de algumas opções, como por exemplo `-q, --quiet` (exibir apenas IDs) e `--services` (exibir os serviços). Para mais informações acerca destas opções, [vide documentação oficial](https://docs.docker.com/compose/reference/ps/).

**Interrompendo o Compose** -- para interromper a execução antes criada pelo `up`, basta rodar o comando `docker-compose down`.

**Outros comandos interessantes de se conhecer**
+ **`docker-compose start <service>`** : Executa os containers pertecentes a um determinado serviço declarado no `docker-compose`;
+ **`docker-compose stop <service>`** : Interrompe a execução de containers pertencentes a um determinado serviço declarado no `docker-compose`;
+ **`docker-compose top`** : Exibe os processos em execução.
