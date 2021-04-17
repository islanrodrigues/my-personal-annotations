### Imagens em Docker
Todas as imagens - igualmente como os containers - possuem um identificador único, que são hashes humanamente difícies de serem decoradas. Por esse motivo, é muito comum as imagens possuírem tags para facilitar a identificação.

**_Tags_ nas imagens** -- as _tags_ funcionam como uma espécie de ponteiro, apontando para uma determinada imagem (_IMAGE ID_). É possível existir várias _tags_ apontando para uma mesma imagem. 

**Baixando e manipulando imagens no Docker** -- para baixar (_pull_) imagens Docker do _Registry_ basta utilizar o comando `image pull` seguido do nome da imagem. Também é possível informar a tag específica da imagem utilizando `<nome_da_imagem>:<nome_da_tag>`. Caso a _tag_ não seja fornecida, o Docker _engine_ entenderá a _latest_ como padrão.

Exemplo:
```bash
docker image pull debian  # O mesmo que debian:latest
```

Para listar todas as imagens existentes baixadas, basta executar `image ls`.

Exemplo:
```bash
docker image ls
```

Para inspecionar uma imagem em particular, trazendo diversas características a respeito da mesma em formato JSON, basta utilizar o comando `image inspect` seguido do nome - e _tag_, caso necessário - da imagem.

Exemplo:
```bash
docker image inspect debian:latest
```

Também é possível criar uma nova _tag_ para uma imagem em específico, utilizando o comando `image tag` e informando a imagem de referência e o nome da nova imagem e _tag_. Esse processo criará uma nova imagem contendo os mesmos apontamentos que a imagem de referência.

Exemplo:
```bash
docker image tag debian nova-imagem-debian:nova_tag
```

Para excluir uma imagem, basta utilizar o comando `image rm` e informando o nome e a _tag_, caso seja necessário.

Exemplo:
```bash
docker image rm debian nova-imagem-debian
```

**Criando uma imagem** -- para se construir imagens no Docker é preciso criar um arquivo descritor, chamado de `Dockerfile`. É a partir desse descritor que o Docker conseguirá interpretar e construir uma determinada imagem. 

Alguns Exemplos de `Dockerfile`:
```text
FROM nginx:latest
RUN echo '<h1>Hello World with Docker!</h1>' > /usr/share/nginx/html/index.html
```

```text
FROM debian
LABEL maintainer 'Islan Rodrigues'

ARG S3_BUCKET=files
ENV S3_BUCKET=${S3_BUCKET}
```

```text
FROM python:3.7
LABEL maintainer 'Islan Rodrigues'

RUN useradd www && \
    mkdir /app && \
    mkdir /log && \
    chown www /log

USER www
VOLUME /log
WORKDIR /app
EXPOSE 8000

ENTRYPOINT ["/usr/local/bin/python"]
CMD ["run.py"]
```

Após criação do `Dockerfile`, o _build_ pode ser realizado com o comando `image build`, acompanhado de possíveis opções de construção (vide documentação oficial) e o caminho relativo onde o `Dockerfile` se encontra.

Exemplos:
```bash
docker image build -t imagem-nginx:latest ./docker/
```

```bash
docker image build --build_arg S3_BUCKET=myApp -t imagem-debian ./docker/
```

Através do comando `image ls` vai ser possível enxergar a nova imagem criada sendo listada.

**Enviando imagens para o Docker Hub** -- para que seja possível o envio de imagens para o servidor do Docker Hub, é necessário criar uma conta de registro na plataforma. Após o cadastro, é possível realizar o _login_ na conta através do comando `login`, informando qual o _username_. Em sequência a este processo, a respectiva senha será solicitada.

Exemplo:
```bash
docker login --username=userdocker
```

Para que seja possível subir a imagem desejada, deve-se nomeá-la da seguinte maneira: `<seu_usuario>/<nome_da_imagem>:<tag>`. Por fim, basta utilizar o comando `image push` informando o nome da imagem.

Exemplo:
```bash
docker image push userdocker/myfirstimage:1.0
```
