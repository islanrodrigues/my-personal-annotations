### Primeiros Passos com o Docker
Após a instalação do Docker seguindo as orientações do site oficial, o comando `docker` deve ser reconhecido via terminal. Para verificar se o Docker está sendo executado de maneira correta, é possível fazer o simples teste do **hello-world** através do comando `docker container run hello-world`.

Exemplo: 
```bash
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

**Comandos interessantes de se conhecer** -- o Docker baseia fortemente a sintaxe de seus comandos na sintaxe do _bash_ de sistemas baseados em Unix.
+ **`docker container ps`** : verifica e exibe quais containers estão sendo executados no momento;
+ **`docker container ps -a`** : verifica e exibe todos os containers que foram executados independente do _status_.