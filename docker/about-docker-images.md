## Imagens em Docker
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

Exemplo de `Dockerfile`:
```text
FROM nginx:latest
RUN echo '<h1>Hello World with Docker!</h1>' > /usr/share/nginx/html/index.html
```

Após criação do `Dockerfile`, o _build_ pode ser realizado com o comando `image build`, acompanhado de possíveis opções de construção (vide documentação oficial) e o caminho relativo onde o `Dockerfile` se encontra.

Exemplo:
```bash
docker image build -t minha-primeira-imagem:latest ./docker/
```

Através do comando `image ls` vai ser possível enxergar a nova imagem criada sendo listada.
