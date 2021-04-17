### Sobre Redes em Docker

**Tipos de redes**
+ **None Network** : container sem nenhum acesso a rede;
+ **Brigde Network (Padrão)** : modelo padrão, justamente a ponte que o Docker cria entre a máquina _host_ e o container;
+ **Host Network** : a camada de _bridge_ fornecida pelo Docker é removida, havendo a comunicação direta entre a máquina _host_ e o container;
+ **Overlay Network** : disponível apenas no _swarm mode_, que é o modo que o Docker disponibiliza para se trabalhar com containers clusterizados.

Através do comando `network ls` é possível visualizar todos os modelos de redes disponíveis citados acima (exceto o _Overlay Network_).

Exemplo:
```text
docker network ls

NETWORK ID     NAME      DRIVER    SCOPE
1677b5bf95ac   bridge    bridge    local
c29a941faf37   host      host      local
00ff1bc3cfd8   none      null      local
```

É possível associar um tipo específico de rede a um container através do comando `--net <nome_do_modelo>`.   

**Sobre o None Network** -- é o container que não possui nenhum tipo de rede. Containers criados com esse tipo de rede não possuem acesso entre si e nem ao mundo exterior. Pode ser acessado via terminal e possui acesso a volumes locais normalmente.

![Network None Model illustration](https://github.com/islanrodrigues/my-personal-annotations/blob/master/images/docker/network_none_model.png)

Exemplo:
```text
docker container run --rm --net none alpine ash -c "ifconfig"

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

**Sobre o Bridge Network** -- é justamente o modelo padrão de um container Docker. Containers criados com esse tipo de rede possuem uma camada intermediária entre as interfaces de rede do _host_ e as suas próprias, a qual é chamada de _bridge_.

![Network Bridge Model illustration](https://github.com/islanrodrigues/my-personal-annotations/blob/master/images/docker/network_bridge_model.png)

**Sobre o Host Network** -- é o modelo que elimina a ponte existente no modelo _bridge_. Containers criados com esse tipo de rede possuem interação direta com as interfaces de rede da máquina _host_. O nível de proteção obviamente se torna mais baixo pelo simples fato de se excluir uma camada de isolamento entre as redes, mas por outro lado, é possível ter uma velocidade de comunicação entre redes considerada maior uma vez que os acessos entre ambas são diretos.

Exemplo:
```bash
docker container run -d --name modelo_rede_host --net host alpine sleep 1000
```

**Criando uma nova rede** -- é possível fazer a criação de uma nova rede no Docker. Para isso, é preciso utilizar o comando `network create` informando o tipo de _driver_ a ser usado através da _flag_ `driver` seguido do nome que será atribuído a essa nova rede.

Exemplo:
```bash
docker network create --driver bridge nova_rede
```

**Outros comandos interessantes de se conhecer** -- o Docker baseia fortemente a sintaxe de seus comandos na sintaxe do _bash_ de sistemas baseados em Unix.
+ **`docker network inspect <nome_do_modelo>`** : permite carregar, em formato JSON, características relacionadas ao modelo em questão;
+ **`docker network connect <nome_da_rede> <nome_do_container>`** : permite que um determinado container, informado no espaço `<nome_do_container>` possa acessar uma rede diferente da qual ele foi criado, informada no espaço `<nome_da_rede>`;
+ **`docker network disconnect <nome_da_rede> <nome_do_container>`** : remove a conectividade previamente concedida a um determinado container, informando no espaço `<nome_do_container>` qual o container envolvido e no espaço `<nome_da_rede>` qual a rede a ser desvinculada. 