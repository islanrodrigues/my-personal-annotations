### Primeiros Passos com o Docker
Após a instalação do Docker seguindo as orientações do site oficial, o comando `docker` deve ser reconhecido via terminal. Para verificar se o Docker está sendo executado de maneira correta, é possível fazer o simples teste do **hello-world** através do comando `docker container run hello-world`.

Exemplo: 
```text
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete
Digest: sha256:95ddb6c31407e84e91a986b004aee40975cb0bda14b5949f6faac5d2deadb4b9
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

 ```

 O exemplo acima informa que a imagem não foi encontrada na máquina local e por isso foi necessário baixar do _Registry_ do Docker. Isso significa que o Docker está executando corretamente.


**O comando `run`** -- é justamente a porta de entrada para o mundo do Docker porque a partir dele é possível agrupar uma série de outros comandos. Em outras palavras, o comando `run` é a contatenação de quatro outros comandos.
+ **`docker image pull`** : é o passo de baixar a imagem do _Registry_ para a máquina local;
+ **`docker container create`** : é o passo de criação de um container;
+ **`docker container start`** : é o passo de inicialização do container;
+ **`docker container exec`** : é o passo de execução do container em modo interativo.

O método `run` cria sempre um novo container no momento em que é executado.

**Modos de execução de containers** -- existem dois modos básicos no Docker que podem ser usados para a execução de containers.
+ **modo daemon** : é o modo no qual um container é executado e fica rodando como um processo em _background_;
+ **modo interativo** : é o modo que serve para entrar no container e realizar algum tipo de experimento, verificação, teste ou se um determinado ajuste de configuração surtiu o efeito desejado.

**Nomeando containers** -- para nomear um container é usado a _flag_ `--name`. Essa funcionalidade torna possível a reutilização de containers criados, uma vez que o comando `run` sempre cria um novo container.

Exemplo: 
```bash
docker container run --name myDebian debian
```

Containers devem possuir nomes únicos. Caso tente criar um novo container com um nome já existente, o Docker irá impedir a ação e informar o erro.

**Reutilizando containers** -- é altamente recomendado que seja utilizado nomes relevantes para nomeação dos containers. Para que se possa reutilizar um container previamente criado basta invocar o comando `start`.

Exemplo:
Digamos que o nome de um container criado seja **myFirstContainer**. 
```bash
docker container start myFirstContainer
```

Caso haja a necessidade de reiniciar a execução do container, basta invocar o comando `restart`.

Exemplo:
```bash
docker container restart myFirstContainer
```

**Mapeando portas de um container** -- para mapeamento de portas de um container é usado a _flag_ `-p`. Como parâmetro para a _flag_ é passado duas portas que devem ser separadas por `:`. A porta informada antes dos dois-pontos será a porta externa ao container, ou seja, a porta pela qual iremos acessar o serviço. A porta informada depois dos dois-pontos será a porta interna do container, onde de fato será feito o _start_ do serviço.

Exemplo: 
```bash
docker container run -p 8080:80 nginx
```

**Mapeando diretórios para um container** -- para mapeamento de diretórios externos para dentro de um container é usado a _flag_ `-v`. Como parâmetro para a _flag_ é passado dois caminhos absolutos que devem ser separados por `:`. O caminho informado antes dos dois-pontos será o caminho absoluto do diretório da máquina _host_ o qual deseja mapear para dentro do container. O caminho informado depois dos dois-pontos será justamente o caminho absoluto do diretório do container que irá enxergar esse mapeamento.

Exemplo:
```bash
docker container run -p 8080:80 -v $(pwd)/meu_volume/html:/usr/share/nginx/html nginx
```

**Rodando e gerenciando um container em _background_** -- para executar um container no modo _daemon_ é usado a _flag_ `-d`. Após execução do container, é possível verificar o seu funcionamento em _background_ através da _flag_ `ps` (vide seção *__"Outros comandos interessantes de se conhecer"__*).

Exemplo:
```bash
docker container run -d --name my-nginx -p 8080:80 -v $(pwd)/meu_volume/html:/usr/share/nginx/html nginx
```
Para parar a execução em modo _daemon_ basta utilizar a _flag_ `stop` seguido do nome ou do ID do container. Por isso é essencial que os containers sejam nomeados de forma relevante, não deixando isso a cargo do Docker.

Exemplo:
```bash
docker container stop my-nginx
```

Para ter acesso a lista de _logs_ gerados por um determinado container, basta utilizar a _flag_ `logs` seguido do nome do container.

Exemplo:
```bash
docker container logs my-nginx
```

Para examinar informações inerentes a um determinado container, basta utilizar a _flag_ `inspect`. Através desse comando é possível trazer, em formato JSON, diversas características do container como tipo de imagem, diretório de log, informações sobre rede etc.

Exemplo:
```bash
docker container inspect my-nginx
```

**Outros comandos interessantes de se conhecer** -- o Docker baseia fortemente a sintaxe de seus comandos na sintaxe do _bash_ de sistemas baseados em Unix.
+ **`docker container run --help`** : traz uma lista de todas as possíveis opções de _flags_ que podem ser utilizadas;
+ **`docker container ls` ou `docker container ps`**: verifica e exibe quais containers estão sendo executados no momento;
+ **`docker container ls -a` ou `docker container ps -a`** : verifica e exibe todos os containers que foram executados independente do _status_;
+ **`docker container -i -t` ou `docker container -it`** : a _flag_ `i` informa que o container será executado no modo interativo e a _flag_ `t` informa que o usuário terá acesso ao terminal.
